---
title: Tutorial de investigação de computador do Microsoft Defender para Identidade
description: Este artigo explica como usar os alertas de segurança do Microsoft Defender para Identidade para investigar um computador suspeito.
keywords: ''
author: shsagir
ms.author: shsagir
ms.date: 10/26/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 070c578f03887f6afdc10117d6886b4f269c830d
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93276035"
---
# <a name="tutorial-investigate-a-computer"></a>Tutorial: Investigar um computador

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

> [!NOTE]
> Os recursos do [!INCLUDE [Product long](includes/product-long.md)] explicados nesta página também podem ser acessados usando o novo [portal](https://portal.cloudappsecurity.com).

A evidência de alerta do [!INCLUDE [Product long](includes/product-long.md)] fornece indicações claras de quando computadores foram envolvidos em atividades suspeitas ou de quando há informações de que um computador está comprometido. Neste tutorial, você usará as sugestões de investigação para identificar o risco para a organização, decidir como corrigir e determinar a melhor maneira de evitar ataques semelhantes no futuro.  

> [!div class="checklist"]
>
> - Verifique o computador quanto ao usuário conectado.
> - Verifique se o usuário normalmente acessa os computadores.
> - Investigue as atividades suspeitas do computador.
> - Houve outros alertas por volta do mesmo horário?

## <a name="investigation-steps-for-suspicious-computers"></a>Etapas de investigação para computadores suspeitos

Para acessar a página de perfil do computador, clique no computador específico mencionado no alerta que você deseja investigar. Para ajudar na investigação, a evidência de alerta lista todos os computadores (e [usuários](investigate-a-user.md)) conectados a cada atividade suspeita.

Verifique e investigue o perfil do computador para obter as atividades e os detalhes a seguir:

- O que aconteceu no momento da atividade suspeita?  
    1. Qual [usuário](investigate-a-user.md) estava conectado ao computador?
    1. Esse usuário normalmente faz logon ou acessa o computador de origem ou de destino?
    1. Quais recursos foram acessados? Por quais usuários?
      - Se os recursos foram acessados, eles eram de alto valor?
    1. O usuário deveria acessar esses recursos?
    1. O [usuário](investigate-a-user.md) que acessou o computador executou outras atividades suspeitas?

- Atividades suspeitas adicionais a serem investigadas:
    1. Havia outros alertas abertos ao mesmo tempo que este alerta no [!INCLUDE [Product short](includes/product-short.md)] ou em outras ferramentas de segurança, como o Microsoft Defender para Ponto de Extremidade, a Central de Segurança do Azure e/ou o Microsoft CAS?
    1. Houve logons com falha?

- Se a integração do Microsoft Defender para Ponto de Extremidade estiver habilitada, clique na notificação do Microsoft Defender para Ponto de Extremidade para investigar o computador mais detalhadamente. No Microsoft Defender para Ponto de Extremidade, você pode ver quais processos e alertas ocorreram no mesmo período que o alerta.
    - Novos programas foram implantados ou instalados?

## <a name="next-steps"></a>Próximas etapas

- [Investigar um usuário](investigate-a-user.md)
- [Trabalhando com alertas de segurança](working-with-suspicious-activities.md)
- [Trabalhando com caminhos de movimento lateral](use-case-lateral-movement-path.md)
- [Alertas de reconhecimento](reconnaissance-alerts.md)
- [Alertas de credencial comprometida](compromised-credentials-alerts.md)
- [Alertas de movimento lateral](lateral-movement-alerts.md)
- [Alertas de predominância de domínio](domain-dominance-alerts.md)
- [Alertas de exfiltração](exfiltration-alerts.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
