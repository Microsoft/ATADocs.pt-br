---
title: Microsoft defender para identidade configurar exclusões de detecção e contas do honeytoken
description: Configuração de exclusões de detecção e contas de usuário honeytoken.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fb4aa3b26c9026a62aac81bd1a88b50b95141ecd
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848475"
---
# <a name="configure-detection-exclusions-and-honeytoken-accounts"></a>Configurar exclusões de detecção e contas de honeytoken

[!INCLUDE [Product long](includes/product-long.md)] permite a exclusão de endereços IP ou usuários específicos de várias detecções.

Por exemplo, uma **exclusão por Reconhecimento de DNS** poderia ser um verificador de segurança que usa o DNS como um mecanismo de verificação. A exclusão ajuda a [!INCLUDE [Product short](includes/product-short.md)] ignorar esses scanners.

[!INCLUDE [Product short](includes/product-short.md)] também habilita a configuração de contas do honeytoken, que são usadas como interceptações para atores mal-intencionados – qualquer autenticação associada a essas contas do honeytoken (normalmente inativas), dispara um alerta.

Para configurar, execute estas etapas:

1. No portal do [!INCLUDE [Product short](includes/product-short.md)], clique no ícone de engrenagem e selecione **Configuração**.

    ![[! INCLUIR definições de configuração [produto curto] (inclui/produto-curto. MD)]](media/config-menu.png)

1. Em **Detecção**, clique em **Marcas de entidade**.

1. Em **Contas de honeytoken**, insira o nome da conta de honeytoken e clique no sinal **+** . O campo de contas Honeytoken é pesquisável e exibe automaticamente entidades em sua rede. Clique em **Salvar**.

    ![Honeytoken](media/honeytoken-sensitive.png)

1. Clique em **Exclusões**. Insira uma conta de usuário ou endereço IP a ser excluído da detecção, para cada tipo de ameaça.
1. Clique no sinal *mais*. O campo **Adicionar entidade** (usuário ou computador) é pesquisável e será preenchido automaticamente com entidades na sua rede. Para obter mais informações, confira [Excluindo entidades das detecções](excluding-entities-from-detections.md) e o [Guia de alerta de segurança](suspicious-activity-guide.md).

    ![Excluindo entidades de detecções](media/exclusions.png)

1. Clique em **Salvar**.

Parabéns, você implantou com êxito [!INCLUDE [Product long](includes/product-long.md)] !

Verifique a linha do tempo de ataque para visualizar os alertas de segurança gerados das atividades detectadas e procure os usuários ou computadores exibindo os perfis deles.

[!INCLUDE [Product short](includes/product-short.md)] a verificação é iniciada imediatamente. Algumas detecções, como [adições suspeitas a grupos confidenciais](domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024), exigem um período de aprendizado e não estão disponíveis imediatamente após a [!INCLUDE [Product short](includes/product-short.md)] implantação. O período de aprendizagem para cada alerta é listado no [Guia de alerta de segurança](suspicious-activity-guide.md)detalhado.

## <a name="see-also"></a>Consulte Também

- [Ferramenta de dimensionamento do [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/aatpsizingtool)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
