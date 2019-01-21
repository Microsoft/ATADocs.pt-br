---
title: Tutorial de investigação de usuário do ATP do Azure | Microsoft Docs
d|Description: This article explains how to user Azure ATP security alerts to investigate a suspicious user.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/14/2019
ms.topic: tutorial
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: e9cf68d2-36bd-4b0d-b36e-7cf7ded2618e
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 126653dd2831e0e3dbd9c777d84d32b1c2e74bd9
ms.sourcegitcommit: 1ee052c4c6b04b290e2d5384c24b65a108b1f1f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2019
ms.locfileid: "54253394"
---
# <a name="tutorial-investigate-a-user"></a>Tutorial: investigar um usuário

A evidência de alerta e os caminhos de movimento lateral do ATP do Azure fornecem indicações claras de quando os usuários executaram atividades suspeitas ou de quando existem indicações de que sua conta foi comprometida. Use as sugestões de investigação para identificar o risco para a organização, decidir como corrigir e determinar a melhor maneira de evitar ataques semelhantes no futuro.  

## <a name="recommended-investigation-steps-for-suspicious-users"></a>Etapas de investigação recomendadas para usuários suspeitos

Verifique e investigue o perfil do usuário quanto às atividades e aos detalhes a seguir:

1. Quem é o [usuário](entity-profiles.md)?
     1. Ele é um [usuário confidencial](sensitive-accounts.md) (como administrador ou presente em uma watchlist, etc.)?  
     2. Qual é a função dele na organização?
     3. Ele é significativo na árvore organizacional?

2. Atividades suspeitas a serem [investigadas](investigate-entity.md):
     1. O usuário tem outros alertas abertos no ATP do Azure ou em outras ferramentas de segurança, como o Windows Defender ATP, a Central de Segurança do Azure e/ou o Microsoft CAS?
     2. O usuário teve entradas com falha?
     3. Quais recursos o usuário acessou?  
     4. O usuário acessou recursos de alto valor?  
     5. O usuário deveria acessar os recursos acessados?  
     6. Em quais computadores o usuário entrou? 
     7. O usuário deveria entrar nesses computadores?
     8. Há um [LMP](use-case-lateral-movement-path.md) (caminho de movimento lateral) entre o usuário e um usuário confidencial?


## <a name="see-also"></a>Consulte Também

- [Investigar um computador](investigate-a-computer.md)
- [Trabalhando com alertas de segurança](working-with-suspicious-activities.md)
- [Trabalhando com caminhos de movimento lateral](use-case-lateral-movement-path.md)
- [Alertas de reconhecimento](atp-reconnaissance-alerts.md)
- [Alertas de credencial comprometida](atp-compromised-credentials-alerts.md)
- [Alertas de movimento lateral](atp-lateral-movement-alerts.md)
- [Alertas de predominância de domínio](atp-domain-dominance-alerts.md)
- [Alertas de exfiltração](atp-exfiltration-alerts.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
