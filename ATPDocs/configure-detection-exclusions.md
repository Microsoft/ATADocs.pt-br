---
title: Microsoft defender para identidade configurar exclusões de detecção
description: Configuração de exclusões de detecção.
ms.date: 02/17/2021
ms.topic: how-to
ms.openlocfilehash: 6e771e2a2755845fe4f02fb9d21750720bbbe37d
ms.sourcegitcommit: f92dca4dc3d8a25b1a06f68ac7a9f8318105bcd8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/17/2021
ms.locfileid: "100630761"
---
# <a name="configure-detection-exclusions"></a>Configurar exclusões de detecção

[!INCLUDE [Product long](includes/product-long.md)] permite a exclusão de endereços IP, computadores ou usuários específicos de várias detecções.

Por exemplo, uma **exclusão por Reconhecimento de DNS** poderia ser um verificador de segurança que usa o DNS como um mecanismo de verificação. A exclusão ajuda a [!INCLUDE [Product short](includes/product-short.md)] ignorar esses scanners.

## <a name="how-to-add-detection-exclusions"></a>Como adicionar exclusões de detecção

Há duas maneiras de excluir manualmente usuários, computadores ou endereços IP para uma detecção. Isso pode ser feito na página de **configuração** em **exclusões** ou diretamente do alerta de segurança.

### <a name="from-the-configuration-page"></a>Na página de configuração

Para configurar exclusões na página configuração, faça o seguinte:

1. No portal do [!INCLUDE [Product short](includes/product-short.md)], selecione **Configuração**.

    ![[! INCLUIR definições de configuração [produto curto] (inclui/produto-curto. MD)]](media/config-menu.png)

1. Em **detecção**, selecione **exclusões**.
1. Para cada detecção que você deseja configurar, faça o seguinte:
    1. Insira um endereço IP, computador ou conta de usuário a ser excluído da detecção
    1. Clique no ícone de adição **(+)**.

    > [!TIP]
    > O campo usuário ou computador é pesquisável e fará preenchimento automático com entidades em sua rede. Para obter mais informações, confira [Excluindo entidades das detecções](excluding-entities-from-detections.md) e o [Guia de alerta de segurança](suspicious-activity-guide.md).

    ![Excluindo entidades de detecções](media/exclusions.png)

1. Clique em **Salvar**.

### <a name="from-a-security-alert"></a>De um alerta de segurança

Para configurar exclusões de um alerta de segurança, faça o seguinte:

1. No [!INCLUDE [Product short](includes/product-short.md)] portal, selecione **linha do tempo**.
1. Identifique um alerta em uma atividade para um usuário, computador ou endereço IP que **tenha** permissão para executar a atividade específica.

1. À direita do alerta, selecione **mais [...]**  >  **Fechar e excluir**. A ação fecha o alerta e ele não está mais listado na lista **abrir** eventos na **linha do tempo do alerta**. A ação também adiciona o usuário, o computador ou o endereço IP à lista de exclusões para esse alerta.

    ![Excluir entidades](media/exclude-in-sa.png)

[!INCLUDE [Product short](includes/product-short.md)] a verificação é iniciada imediatamente. Algumas detecções, como [adições suspeitas a grupos confidenciais](domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024), exigem um período de aprendizado e não estão disponíveis imediatamente após a [!INCLUDE [Product short](includes/product-short.md)] implantação. O período de aprendizagem para cada alerta é listado no [Guia de alerta de segurança](suspicious-activity-guide.md)detalhado.

## <a name="see-also"></a>Consulte Também

- [Configurar coleta de eventos](configure-event-collection.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
