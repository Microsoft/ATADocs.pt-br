---
title: Configurar o encaminhamento de eventos do Windows no Microsoft Defender para Identidade
description: Descreve suas opções de configuração do Encaminhamento de Eventos do Windows com o Microsoft Defender para Identidade
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: f3a11a3d39972b3bdb3df38669ef2fa4b10cc5fb
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96543528"
---
# <a name="configuring-windows-event-forwarding"></a>Configuração do encaminhamento de eventos do Windows

> [!NOTE]
> O sensor do [!INCLUDE [Product long](includes/product-long.md)] lê os eventos de forma automática localmente, sem a necessidade de configurar o encaminhamento de eventos.

Para aprimorar as funcionalidades de detecção, o [!INCLUDE [Product short](includes/product-short.md)] precisa dos eventos do Windows listados na seção [Configurar coleta de eventos](configure-windows-event-collection.md#configure-event-collection). Eles podem ser lidos automaticamente pelo sensor do [!INCLUDE [Product short](includes/product-short.md)] ou, caso o sensor do [!INCLUDE [Product short](includes/product-short.md)] não esteja implantado, podem ser encaminhados para o sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] de duas maneiras: configurando o sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] para escutar eventos de SIEM ou configurando o Encaminhamento de Eventos do Windows.

> [!NOTE]
>
> - Os sensores autônomos do [!INCLUDE [Product short](includes/product-short.md)] não dão suporte à coleção de entradas de log do ETW (Rastreamento de Eventos para Windows) que fornecem dados para várias detecções. Para cobertura completa do seu ambiente, recomendamos implantar o sensor do [!INCLUDE [Product short](includes/product-short.md)].
> - Verifique se o controlador de domínio está configurado corretamente para capturar os eventos necessários.

## <a name="wef-configuration-for-product-short-standalone-sensors-with-port-mirroring"></a>Configuração do WEF dos sensores autônomos do [!INCLUDE [Product short](includes/product-short.md)] com espelhamento de porta

Após configurar o espelhamento de porta dos controladores de domínio para o sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)], siga as instruções abaixo para configurar o Encaminhamento de Eventos do Windows usando a configuração Iniciada pela Origem. Essa é uma maneira para configurar o Encaminhamento de eventos do Windows.

**Etapa 1: adicionar a conta de serviço de rede ao Grupo de Leitores de Log de Eventos do domínio.**

Neste cenário, suponha que o sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] seja membro do domínio.

1. Abra os Usuários e Computadores do Active Directory, navegue até a pasta **BuiltIn** e clique duas vezes em **Leitores de Log de Eventos**.
1. Selecione **Membros**.
1. Se **Serviço de Rede** não estiver listado, clique em **Adicionar**, digite **Serviço de Rede** no campo **Digite os nomes de objeto a serem selecionados** . Depois, clique em **Verificar Nomes** e clique em **OK** duas vezes.

Após adicionar o **Serviço de Rede** ao grupo **Leitores de Log de Eventos**, reinicie os controladores de domínio para que a alteração tenha efeito.

**Etapa 2: criar uma política nos controladores de domínio para definir a configuração Configurar Gerenciador de Assinaturas de destino.**

> [!Note]
> Você pode criar uma política de grupo para essas configurações e aplicá-la a cada controlador de domínio monitorado pelo sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)]. As etapas a seguir modificam a política local do controlador de domínio.

1. Execute o seguinte comando em cada controlador de domínio: *winrm quickconfig*
1. Em um prompt de comando, digite *gpedit.msc*.
1. Expanda **Configuração do Computador > Modelos Administrativos > Componentes do Windows > Encaminhamento de Evento**

    ![Imagem do editor de grupo de política local](media/wef-1-local-group-policy-editor.png)

1. Clique duas vezes em **Configurar Gerenciador de assinatura de destino**.

    1. Selecione **Habilitado**.
    1. Em **Opções**, clique em **Mostrar**.
    1. Em **SubscriptionManagers**, insira o seguinte valor e clique em **OK**:  `Server=http\://\<fqdnMicrosoftDefenderForIdentitySensor>:5985/wsman/SubscriptionManager/WEC,Refresh=10` (Por exemplo: `Server=http\://atpsensor9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10`)

    ![Configurar a imagem de assinatura de destino](media/wef-2-config-target-sub-manager.png)

1. Clique em **OK**.
1. Em um prompt de comandos com privilégios elevados, digite *gpupdate /force*.

**Etapa 3: executar estas etapas no sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)]**

1. Em um prompt de comandos com privilégios elevados, digite *wecutil qc*
1. Abra o **Visualizador de Eventos**.
1. Clique com o botão direito do mouse em **Assinaturas** e selecione **Criar Assinatura**.

    1. Insira um nome e uma descrição para a assinatura.
    1. Para **Log de Destino** confirme se **Eventos Encaminhados** está selecionado. Para o [!INCLUDE [Product short](includes/product-short.md)] ler os eventos, o log de destino deve ser **Eventos Encaminhados**.
    1. Selecione **Iniciado pelo computador de origem** e clique em **Selecionar Grupos de Computadores**.
        1. Clique em **Adicionar Computador do Domínio**.
        1. Insira o nome do controlador de domínio no campo **Digite o nome do objeto a ser selecionado**. Depois, clique em **Verificar Nomes** e clique em **OK**.
        1. Clique em **OK**.
        ![Imagem do Visualizador de Eventos](media/wef-3-event-viewer.png)
    1. Clique em **Selecionar Eventos**.
        1. Clique em **Pelo log** e selecione **Segurança**.
        1. No campo **Inclui/Exclui ID do Evento**, digite o número do evento e clique em **OK**. Por exemplo, digite 4776, como no exemplo a seguir:<br/>
        ![Imagem do filtro de consulta](media/wef-4-query-filter.png)
    1. Clique com o botão direito do mouse na assinatura criada e selecione **Status de Runtime** para verificar se há problemas com o status.
    1. Depois de alguns minutos, verifique se os eventos definidos para encaminhamento aparecem nos Eventos Encaminhados no sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)].

Para obter mais informações, consulte: [Configurar computadores para encaminhar e coletar eventos](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc748890(v=ws.11))

## <a name="see-also"></a>Consulte Também

- [Instalar o [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
