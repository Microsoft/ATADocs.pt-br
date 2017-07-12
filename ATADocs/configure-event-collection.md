---
title: Configurar o Encaminhamento de Eventos do Windows no Advanced Threat Analytics | Microsoft Docs
description: "Descreve suas opções para configurar o Encaminhamento de Eventos do Windows com o ATA"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/2/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 6469f602d2da833e96bba72003aad3fe2b67eb48
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*



<a id="configuring-windows-event-forwarding" class="xliff"></a>

# Configuração do encaminhamento de eventos do Windows

Para aprimorar os recursos de detecção, o ATA precisa dos seguintes eventos do Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757. Eles podem ser lidos automaticamente pelo Gateway Lightweight do ATA ou no caso de o Gateway Lightweight do ATA não estar implantado, podem ser encaminhados para o Gateway do ATA de duas maneiras: configurando o Gateway do ATA para escutar o SIEM ou [Configurando o Encaminhamento de Eventos do Windows](#configuring-windows-event-forwarding).

> [!NOTE]
> Para as versões 1.8 e mais recentes do ATA, a configuração de coleta de eventos não é mais necessária para Gateways Lightweight do ATA. O Gateway Lightweight do ATA poderá ler eventos localmente, sem a necessidade de configurar o encaminhamento de eventos.

<a id="wef-configuration-for-ata-gateways-with-port-mirroring" class="xliff"></a>

### Configuração de WEF para Gateway do ATA com o espelhamento de porta

Após a configuração do espelhamento de porta nos controladores de domínio para o Gateway do ATA, siga as instruções abaixo para configurar o Encaminhamento de eventos do Windows usando a configuração Iniciada pela Origem. Essa é uma maneira para configurar o Encaminhamento de eventos do Windows. 

**Etapa 1: Adicionar a conta de serviço de rede ao Grupo de Leitores de Log de Eventos do domínio.** 

Nesse cenário, supomos que o Gateway ATA seja membro do domínio.

1.  Abra os Usuários e Computadores do Active Directory, navegue até a pasta **BuiltIn** e clique duas vezes em **Leitores de Log de Eventos**. 
2.  Selecione **Membros**.
4.  Se **Serviço de Rede** não estiver listado, clique em **Adicionar**, digite **Serviço de Rede** no campo **Digite os nomes de objeto a serem selecionados** . Depois, clique em **Verificar Nomes** e clique em **OK** duas vezes. 

Observe que após adicionar o **Serviço de Rede** no grupo **Leitores de Log de Eventos** é necessário reiniciar os controladores de domínio para que a alteração tenha efeito.

**Etapa 2: Criar uma política nos controladores de domínio para definir a configuração Configurar Gerenciador de Assinaturas de destino.** 
> [!Note] 
> Você pode criar uma política de grupo para essas configurações e aplicá-la a cada controlador de domínio monitorado pelo Gateway do ATA. As etapas a seguir modificarão a política local do controlador de domínio.     

1.  Execute o seguinte comando em cada controlador de domínio: *winrm quickconfig*
2.  Em um prompt de comando, digite *gpedit.msc*.
3.  Expanda **Configuração do Computador > Modelos Administrativos > Componentes do Windows > Encaminhamento de Evento**

 ![Imagem do editor de grupo de política local](media/wef 1 local group policy editor.png)

4.  Clique duas vezes em **Configurar Gerenciador de assinatura de destino**.
   
    1.  Selecione **Habilitado**.
    2.  Em **Opções**, clique em **Mostrar**.
    3.  Em **SubscriptionManagers**, insira o seguinte valor e clique em **OK**:  *Server=http://<fqdnATAGateway>:5985/wsman/SubscriptionManager/WEC,Refresh=10* (Por exemplo: Server=http://atagateway9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10)
 
   ![Configurar a imagem de assinatura de destino](media/wef 2 config target sub manager.png)
   
    5.  Clique em **OK**.
    6.  Em um prompt de comandos com privilégios elevados, digite *gpupdate /force*. 

**Etapa 3: Executar as seguintes etapas no Gateway do ATA** 

1.  Em um prompt de comandos com privilégios elevados, digite *wecutil qc*
2.  Abra o **Visualizador de Eventos**. 
3.  Clique com o botão direito em **Assinaturas** e selecione **Criar Assinatura**. 

   1.   Insira um nome e uma descrição para a assinatura. 
   2.   Para **Log de Destino** confirme se **Eventos Encaminhados** está selecionado. Para o ATA ler os eventos, o log de destino deve ser **Eventos Encaminhados**. 
   3.   Selecione **Iniciado pelo computador de origem** e clique em **Selecionar Grupos de Computadores**.
        1.  Clique em **Adicionar Computador do Domínio**.
        2.  Insira o nome do controlador de domínio no campo **Digite o nome do objeto a ser selecionado**. Depois, clique em **Verificar Nomes** e clique em **OK**. 
       
        ![Imagem do Visualizador de Eventos](media/wef3 event viewer.png)
   
        
        3.  Clique em **OK**.
   4.   Clique em **Selecionar Eventos**.

        1. Clique em **Pelo log** e selecione **Segurança**.
        2. No campo **Inclui/Exclui ID do Evento**, digite o número do evento e clique em **OK**. 

 ![Imagem do filtro de consulta](media/wef 4 query filter.png)

   5.   Clique com o botão direito na assinatura criada e selecione **Status de Tempo de Execução** para verificar se há problemas com o status. 
   6.   Depois de alguns minutos, verifique se os eventos definidos para serem encaminhados aparecem nos Eventos Encaminhados no Gateway do ATA.


Para obter mais informações, confira: [Configurar computadores para encaminhar e coletar eventos](https://technet.microsoft.com/library/cc748890)

<a id="see-also" class="xliff"></a>

## Consulte Também
- [Instalar o ATA](install-ata-step1.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
