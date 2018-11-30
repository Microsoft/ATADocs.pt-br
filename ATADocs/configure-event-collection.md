---
title: Configurar o Encaminhamento de Eventos do Windows no Advanced Threat Analytics | Microsoft Docs
description: Descreve suas opções para configurar o Encaminhamento de Eventos do Windows com o ATA
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 93c49b71ea5fb67e57d505fb0b7c2e69314de4f9
ms.sourcegitcommit: e2a89030c31376c6798697a62b484f45ed54e679
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52501114"
---
*Aplica-se a: Advanced Threat Analytics versão 1.9*



# <a name="configuring-windows-event-forwarding"></a>Configuração do encaminhamento de eventos do Windows

> [!NOTE]
> Para as versões 1.8 e mais recentes do ATA, a configuração de coleta de eventos não é mais necessária para Gateways Lightweight do ATA. O Gateway Lightweight do ATA realiza a leitura de eventos localmente, sem a necessidade de configurar o encaminhamento de eventos.

Para aprimorar as funcionalidades de detecção, o ATA precisa dos seguintes eventos do Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757 e 7045. Eles podem ser lidos automaticamente pelo Gateway Lightweight do ATA ou no caso de o Gateway Lightweight do ATA não estar implantado, podem ser encaminhados para o Gateway do ATA de duas maneiras: configurando o Gateway do ATA para escutar os eventos do SIEM ou configurando o Encaminhamento de Eventos do Windows.

> [!NOTE]
> Se você estiver usando o Server Core, o [wecutil](https://docs.microsoft.com/windows-server/administration/windows-commands/wecutil) poderá ser usado para criar e gerenciar assinaturas de eventos que são encaminhados de computadores remotos.

### <a name="wef-configuration-for-ata-gateways-with-port-mirroring"></a>Configuração de WEF para Gateway do ATA com o espelhamento de porta

Após a configuração do espelhamento de porta dos controladores de domínio para o Gateway do ATA, siga as instruções a seguir para configurar o Encaminhamento de Eventos do Windows usando a configuração Iniciada pela Origem. Essa é uma maneira para configurar o Encaminhamento de eventos do Windows. 

**Etapa 1: Adicionar a conta de serviço de rede ao Grupo de Leitores de Log de Eventos do domínio.** 

Neste cenário, supomos que o Gateway ATA seja membro do domínio.

1.  Abra os Usuários e Computadores do Active Directory, navegue até a pasta **BuiltIn** e clique duas vezes em **Leitores de Log de Eventos**. 
2.  Selecione **Membros**.
3.  Se **Serviço de Rede** não estiver listado, clique em **Adicionar**, digite **Serviço de Rede** no campo **Digite os nomes de objeto a serem selecionados** . Depois, clique em **Verificar Nomes** e clique em **OK** duas vezes. 

Após adicionar o **Serviço de Rede** ao grupo **Leitores de Log de Eventos**, reinicie os controladores de domínio para que a alteração tenha efeito.

**Etapa 2: Criar uma política nos controladores de domínio para definir a configuração Configurar Gerenciador de Assinaturas de destino.** 
> [!Note] 
> Você pode criar uma política de grupo para essas configurações e aplicá-la a cada controlador de domínio monitorado pelo Gateway do ATA. As etapas a seguir modificarão a política local do controlador de domínio.     

1.  Execute o seguinte comando em cada controlador de domínio: *winrm quickconfig*
2.  Em um prompt de comando, digite *gpedit.msc*.
3.  Expanda **Configuração do Computador > Modelos Administrativos > Componentes do Windows > Encaminhamento de Evento**

  ![Imagem do editor de grupo de política local](media/wef%201%20local%20group%20policy%20editor.png)

4.  Clique duas vezes em **Configurar Gerenciador de assinatura de destino**.
   
    1.  Selecione **Habilitado**.
    2.  Em **Opções**, clique em **Mostrar**.
    3.  Em **SubscriptionManagers**, digite o seguinte valor e clique em **OK**: *Server=http://<fqdnATAGateway>:5985/wsman/SubscriptionManager/WEC,Refresh=10* 
      
         *(Por exemplo: Server=`http://atagateway9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10`)*
      
         ![Configurar a imagem de assinatura de destino](media/wef%202%20config%20target%20sub%20manager.png)
      
    4.  Clique em **OK**.
    5.  Em um prompt de comandos com privilégios elevados, digite *gpupdate /force*. 

**Etapa 3: Executar as seguintes etapas no Gateway do ATA** 

1.  Em um prompt de comandos com privilégios elevados, digite *wecutil qc*
2.  Abra o **Visualizador de Eventos**. 
3.  Clique com o botão direito do mouse em **Assinaturas** e selecione **Criar Assinatura**. 

    1.  Insira um nome e uma descrição para a assinatura. 
    2.  Para **Log de Destino** confirme se **Eventos Encaminhados** está selecionado. Para o ATA ler os eventos, o log de destino deve ser **Eventos Encaminhados**. 
    3.  Selecione **Iniciado pelo computador de origem** e clique em **Selecionar Grupos de Computadores**.
        1.  Clique em **Adicionar Computador do Domínio**.
        2.  Insira o nome do controlador de domínio no campo **Digite o nome do objeto a ser selecionado**. Depois, clique em **Verificar Nomes** e clique em **OK**.  
          ![Imagem do Visualizador de Eventos](media/wef3%20event%20viewer.png)  
        3.  Clique em **OK**.
    4.  Clique em **Selecionar Eventos**.
        1. Clique em **Pelo log** e selecione **Segurança**.
        2. No campo **Inclui/Exclui ID do Evento**, digite o número do evento e clique em **OK**. Por exemplo, digite 4776, conforme no exemplo a seguir.

        ![Imagem do filtro de consulta](media/wef%204%20query%20filter.png)

    5.  Clique com o botão direito do mouse na assinatura criada e selecione **Status de Tempo de Execução** para verificar se há problemas com o status. 
    6.  Depois de alguns minutos, verifique se os eventos definidos para serem encaminhados aparecem nos Eventos Encaminhados no Gateway do ATA.


Para saber mais, confira: [Configurar computadores para encaminhar e coletar eventos](https://technet.microsoft.com/library/cc748890)

## <a name="see-also"></a>Consulte Também
- [Instalar o ATA](install-ata-step1.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
