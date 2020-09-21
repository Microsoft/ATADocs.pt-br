---
title: Configurar o Encaminhamento de Eventos do Windows na Proteção Avançada contra Ameaças do Azure
description: Descreve suas opções para configurar o Encaminhamento de Eventos do Windows com o Azure ATP
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/18/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 3547519f-8d9c-40a9-8f0e-c7ba21081203
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8580988514434b03cd932edd054ba4f80af7f501
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90826491"
---
# <a name="configuring-windows-event-forwarding"></a>Configuração do encaminhamento de eventos do Windows

> [!NOTE]
> O sensor do Azure ATP lê automaticamente os eventos localmente, sem a necessidade de configurar o encaminhamento de eventos.

Para aprimorar as funcionalidades de detecção, o ATP do Azure precisa dos eventos do Windows listados em [Configurar coleta de eventos](configure-windows-event-collection.md#configure-event-collection). Eles podem ser lidos automaticamente pelo sensor do Azure ATP ou, caso o sensor do Azure ATP não esteja implantado, ele poderá ser encaminhado para o sensor autônomo do Azure ATP de duas maneiras: configurando o sensor autônomo do Azure ATP para escutar eventos do SIEM ou configurando o Encaminhamento de Eventos do Windows.

> [!NOTE]
>
> - Os sensores autônomos do ATP do Azure não dão suporte à coleção de entradas de log do ETW (Rastreamento de Eventos para Windows) que fornecem os dados para várias detecções. Para cobertura completa do seu ambiente, é recomendável implantar o sensor do ATP do Azure.
> - Verifique se o controlador de domínio está configurado corretamente para capturar os eventos necessários.

## <a name="wef-configuration-for-azure-atp-standalone-sensors-with-port-mirroring"></a>Configuração do WEF para o sensor autônomo do Azure ATP com espelhamento de porta

Após configurar o espelhamento de porta dos controladores de domínio para o Azure ATP, siga as instruções a seguir para configurar o Encaminhamento de Eventos do Windows usando a configuração Origem Iniciada. Essa é uma maneira para configurar o Encaminhamento de eventos do Windows.

**Etapa 1: adicionar a conta de serviço de rede ao Grupo de Leitores de Log de Eventos do domínio.**

Neste cenário, suponha que o sensor autônomo do Azure ATP seja membro do domínio.

1. Abra os Usuários e Computadores do Active Directory, navegue até a pasta **BuiltIn** e clique duas vezes em **Leitores de Log de Eventos**.
1. Selecione **Membros**.
1. Se **Serviço de Rede** não estiver listado, clique em **Adicionar**, digite **Serviço de Rede** no campo **Digite os nomes de objeto a serem selecionados** . Depois, clique em **Verificar Nomes** e clique em **OK** duas vezes.

Após adicionar o **Serviço de Rede** ao grupo **Leitores de Log de Eventos**, reinicie os controladores de domínio para que a alteração tenha efeito.

**Etapa 2: criar uma política nos controladores de domínio para definir a configuração Configurar Gerenciador de Assinaturas de destino.**

> [!Note]
> Você pode criar uma política de grupo para essas configurações e aplicá-la a cada controlador de domínio monitorado pelo sensor autônomo do Azure ATP. As etapas a seguir modificam a política local do controlador de domínio.

1. Execute o seguinte comando em cada controlador de domínio: *winrm quickconfig*
1. Em um prompt de comando, digite *gpedit.msc*.
1. Expanda **Configuração do Computador > Modelos Administrativos > Componentes do Windows > Encaminhamento de Evento**

    ![Imagem do editor de grupo de política local](media/wef%201%20local%20group%20policy%20editor.png)

1. Clique duas vezes em **Configurar Gerenciador de assinatura de destino**.

    1. Selecione **Habilitado**.
    1. Em **Opções**, clique em **Mostrar**.
    1. Em **SubscriptionManagers**, insira o seguinte valor e clique em **OK**:  Server= http\://\<fqdnATPSensor>:5985/wsman/SubscriptionManager/WEC,Refresh=10` (Por exemplo: Server=http\://atpsensor9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10)

    ![Configurar a imagem de assinatura de destino](media/wef%202%20config%20target%20sub%20manager.png)

1. Clique em **OK**.
1. Em um prompt de comandos com privilégios elevados, digite *gpupdate /force*.

**Etapa 3: executar as seguintes etapas no sensor autônomo do ATP do Azure**

1. Em um prompt de comandos com privilégios elevados, digite *wecutil qc*
1. Abra o **Visualizador de Eventos**.
1. Clique com o botão direito do mouse em **Assinaturas** e selecione **Criar Assinatura**.

    1. Insira um nome e uma descrição para a assinatura.
    1. Para **Log de Destino** confirme se **Eventos Encaminhados** está selecionado. Para o Azure ATP ler os eventos, o log de destino deve ser **Eventos Encaminhados**.
    1. Selecione **Iniciado pelo computador de origem** e clique em **Selecionar Grupos de Computadores**.
        1. Clique em **Adicionar Computador do Domínio**.
        1. Insira o nome do controlador de domínio no campo **Digite o nome do objeto a ser selecionado**. Depois, clique em **Verificar Nomes** e clique em **OK**.
        1. Clique em **OK**.
        ![Imagem do Visualizador de Eventos](media/wef3%20event%20viewer.png)
    1. Clique em **Selecionar Eventos**.
        1. Clique em **Pelo log** e selecione **Segurança**.
        1. No campo **Inclui/Exclui ID do Evento**, digite o número do evento e clique em **OK**. Por exemplo, digite 4776, como no exemplo a seguir:<br/>
        ![Imagem do filtro de consulta](media/wef-4-query-filter.png)
    1. Clique com o botão direito do mouse na assinatura criada e selecione **Status de Runtime** para verificar se há problemas com o status.
    1. Depois de alguns minutos, verifique se os eventos definidos para serem encaminhados aparecem nos Eventos Encaminhados no sensor autônomo do Azure ATP.

Para obter mais informações, consulte: [Configurar computadores para encaminhar e coletar eventos](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc748890(v=ws.11))

## <a name="see-also"></a>Consulte Também

- [Instalar o Azure ATP](install-step1.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)