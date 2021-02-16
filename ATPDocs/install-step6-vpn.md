---
title: Instalar a integração de VPN do Microsoft defender para identidade
description: Colete informações de contabilidade do Microsoft defender para identidade integrando uma VPN.
ms.date: 12/23/2020
ms.topic: how-to
ms.openlocfilehash: 3b86ee864e08998fd532b39a30d566b83e928edf
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533997"
---
# <a name="integrate-vpn"></a>Integrar a VPN

[!INCLUDE [Product long](includes/product-long.md)] pode coletar informações de contabilidade de soluções de VPN. Quando configurada, a página de perfil do usuário inclui informações de conexões de VPN, tais como os endereços IP e os locais de origem das conexões. Isso complementa o processo de investigação, fornecendo informações adicionais sobre a atividade de usuário, bem como uma nova detecção para conexões de VPN anormais. A chamada para resolver um endereço IP externo de um local é anônima. Nenhuma identificação pessoal será enviada nesta chamada.

[!INCLUDE [Product short](includes/product-short.md)] integra-se com sua solução de VPN ouvindo eventos de contabilidade RADIUS encaminhados para os [!INCLUDE [Product short](includes/product-short.md)] sensores. Este mecanismo é baseado em Contabilização RADIUS padrão ([RFC 2866](https://tools.ietf.org/html/rfc2866)) e têm suporte dos seguintes fornecedores de VPN:

- Microsoft
- F5
- Check Point
- Cisco ASA

## <a name="prerequisites"></a>Pré-requisitos

Para habilitar a integração de VPN, verifique se você definiu os seguintes parâmetros:

- Abra a porta UDP 1813 em seus [!INCLUDE [Product short](includes/product-short.md)] sensores e/ou [!INCLUDE [Product short](includes/product-short.md)] sensores autônomos.

> [!NOTE]
>
> - Ao habilitar a **contabilização RADIUS**, o [!INCLUDE [Product short](includes/product-short.md)] sensor habilitará uma política de firewall do Windows previamente provisionada chamada **[!INCLUDE [Product long](includes/product-long.md)] sensor** para permitir a contabilização Radius de entrada na porta UDP 1813.
> - A integração de VPN não tem suporte em ambientes que aderem a FIPS (Federal Information Processing Standards)

O exemplo abaixo usa o Servidor de Roteamento e Acesso Remoto (RRAS) da Microsoft para descrever o processo de configuração de VPN.

Se estiver usando uma solução de VPN de terceiros, confira a documentação para ver instruções de como habilitar a Contabilização RADIUS.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Configurar a Contabilização de RADIUS no sistema de VPN

Execute as seguintes etapas em seu servidor RRAS.

1. Abra o console de Roteamento e Acesso Remoto.
1. Clique com o botão direito do mouse no nome do servidor e clique em **Propriedades**.
1. Na guia **Segurança**, em **Provedor de contabilização**, selecione **Contabilização RADIUS** e clique em **Configurar**.

    ![Configuração RADIUS](media/radius-setup.png)

1. Na janela **Adicionar servidor RADIUS** , digite o **nome do servidor** do sensor mais próximo [!INCLUDE [Product short](includes/product-short.md)] (que tem conectividade de rede). Para alta disponibilidade, você pode adicionar [!INCLUDE [Product short](includes/product-short.md)] sensores adicionais como servidores RADIUS. Em **Porta**, verifique se o padrão de 1813 está configurado. Clique em **Alterar** e digite uma nova cadeia de caracteres alfanuméricos secreta compartilhada. Anote a nova cadeia de caracteres secreta compartilhada, pois você precisará preenchê-la posteriormente durante a [!INCLUDE [Product short](includes/product-short.md)] configuração. Marque a caixa **Enviar mensagens de conta habilitada e de contabilização desabilitada do RADIUS** e, em seguida, clique em **OK** em todas as caixas de diálogo abertas.

    ![Configuração de VPN](media/vpn-set-accounting.png)

### <a name="configure-vpn-in-defender-for-identity"></a>Configurar VPN no defender para identidade

[!INCLUDE [Product short](includes/product-short.md)] coleta dados de VPN que ajudam a criar um perfil dos locais a partir dos quais os computadores se conectam à rede e conseguirem detectar conexões VPN suspeitas.

Para configurar dados de VPN no [!INCLUDE [Product short](includes/product-short.md)] :

1. No [!INCLUDE [Product short](includes/product-short.md)] portal, clique na configuração engrenagem e em **VPN**.
1. Ativar **Contabilização Radius** e digite o **Segredo Compartilhado** configurado anteriormente em seu servidor VPN do RRAS. Em seguida, clique em **Salvar**.

    ![Configurar o [! INCLUIR [produto curto] (inclui/produto-curto. MD)] VPN](media/vpn-radius.png)

Depois que isso for habilitado, todos os [!INCLUDE [Product short](includes/product-short.md)] sensores escutarão na porta 1813 para eventos de contabilidade RADIUS e a configuração de VPN será concluída.

 Depois que o [!INCLUDE [Product short](includes/product-short.md)] sensor recebe os eventos de VPN e os envia para o [!INCLUDE [Product short](includes/product-short.md)] serviço de nuvem para processamento, o perfil de entidade indicará locais de VPN e atividades acessadas distintos no perfil indicará locais.

## <a name="see-also"></a>Consulte Também

- [Ferramenta de dimensionamento do [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/aatpsizingtool)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
