---
title: Tutorial de investigação de usuário do Microsoft Defender para Identidade
description: Este artigo explica como usar os alertas de segurança do Microsoft Defender para Identidade para investigar um usuário suspeito.
ms.date: 10/26/2020
ms.topic: tutorial
ms.openlocfilehash: 783b2b4cc12bfa84812810f754deedb70c1718bb
ms.sourcegitcommit: f92dca4dc3d8a25b1a06f68ac7a9f8318105bcd8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/17/2021
ms.locfileid: "100630519"
---
# <a name="tutorial-investigate-a-user"></a>Tutorial: investigar um usuário

> [!NOTE]
> Os recursos do [!INCLUDE [Product long](includes/product-long.md)] explicados nesta página também podem ser acessados usando o novo [portal](https://portal.cloudappsecurity.com).

A evidência de alerta e os caminhos de movimentação lateral do [!INCLUDE [Product long](includes/product-long.md)] fornecem indicações claras de quando os usuários executaram atividades suspeitas ou de quando existem indicações de que a sua conta foi comprometida. Neste tutorial, você usará as sugestões de investigação para identificar o risco para a organização, decidir como corrigir e determinar a melhor maneira de evitar ataques futuros semelhantes.

> [!div class="checklist"]
>
> - Reúna mais informações sobre o usuário.
> - Investigue as atividades que o usuário executou.
> - Investigue os recursos que o usuário acessou.
> - Investigue os caminhos de movimento lateral.

## <a name="recommended-investigation-steps-for-suspicious-users"></a>Etapas de investigação recomendadas para usuários suspeitos

Verifique e investigue o perfil do usuário quanto às atividades e aos detalhes a seguir:

1. Quem é o [usuário](entity-profiles.md)?
    1. Ele é um [usuário confidencial](manage-sensitive-honeytoken-accounts.md) (como administrador ou presente em uma watchlist, etc.)?
    1. Qual é a função dele na organização?
    1. Ele é significativo na árvore organizacional?

1. Atividades suspeitas a serem [investigadas](investigate-entity.md):
    1. O usuário tem outros alertas abertos no [!INCLUDE [Product short](includes/product-short.md)] ou em outras ferramentas de segurança, como o Microsoft Defender para Ponto de Extremidade, a Central de Segurança do Azure e/ou o Microsoft CAS?
    1. O usuário teve entradas com falha?
    1. Quais recursos o usuário acessou?
    1. O usuário acessou recursos de alto valor?
    1. O usuário deveria acessar os recursos acessados?
    1. Em quais computadores o usuário entrou?
    1. O usuário deveria entrar nesses computadores?
    1. Há um [LMP](use-case-lateral-movement-path.md) (caminho de movimento lateral) entre o usuário e um usuário confidencial?

## <a name="see-also"></a>Consulte Também

- [Investigar um computador](investigate-a-computer.md)
- [Trabalhando com alertas de segurança](working-with-suspicious-activities.md)
- [Trabalhando com caminhos de movimento lateral](use-case-lateral-movement-path.md)
- [Alertas de reconhecimento](reconnaissance-alerts.md)
- [Alertas de credencial comprometida](compromised-credentials-alerts.md)
- [Alertas de movimento lateral](lateral-movement-alerts.md)
- [Alertas de predominância de domínio](domain-dominance-alerts.md)
- [Alertas de exfiltração](exfiltration-alerts.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
