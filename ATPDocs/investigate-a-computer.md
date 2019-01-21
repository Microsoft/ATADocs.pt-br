---
title: Tutorial de investigação de computador do ATP do Azure | Microsoft Docs
d|Description: This article explains how to use Azure ATP security alerts to investigate a suspicious computer.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/14/2019
ms.topic: tutorial
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 64424c6c2b2b0f627099ab479831f4b289eb9605
ms.sourcegitcommit: 1ee052c4c6b04b290e2d5384c24b65a108b1f1f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2019
ms.locfileid: "54253377"
---
# <a name="tutorial-investigate-a-computer"></a>Tutorial: Investigar um computador

A evidência de alerta do ATP do Azure fornece indicações claras de quando computadores foram envolvidos em atividades suspeitas ou de quando há informações de que um computador está comprometido. Use as sugestões de investigação para identificar o risco para a organização, decidir como corrigir e determinar a melhor maneira de evitar ataques semelhantes no futuro.  

## <a name="investigation-steps-for-suspicious-computers"></a>Etapas de investigação para computadores suspeitos

Para acessar a página de perfil do computador, clique no computador específico mencionado no alerta que você deseja investigar. Para ajudar na investigação, a evidência de alerta lista todos os computadores (e [usuários](investigate-a-user.md)) conectados a cada atividade suspeita.

Verifique e investigue o perfil do computador para obter as atividades e os detalhes a seguir:

- O que aconteceu no momento da atividade suspeita?  
    1. Qual [usuário](investigate-a-user.md) estava conectado ao computador?
    2. Esse usuário normalmente faz logon ou acessa o computador de origem ou de destino?
    3. Quais recursos foram acessados? Por quais usuários?
            – Se foram acessados recursos, eles eram de alto valor?
    4. O usuário deveria acessar esses recursos?
    5. O [usuário](investigate-a-user.md) que acessou o computador executou outras atividades suspeitas?


- Atividades suspeitas adicionais a serem investigadas:
    1. Havia outros alertas abertos ao mesmo tempo que este alerta no ATP do Azure ou em outras ferramentas de segurança, como o Windows Defender ATP, a Central de Segurança do Azure e/ou o Microsoft CAS?
    2. Houve logons com falha?


- Se a integração do Windows Defender ATP estiver habilitada, clique no selo do Windows Defender ATP para investigar o computador. No Windows Defender ATP, você pode ver quais processos e alertas ocorreram no mesmo período que o alerta.
    1. Novos programas foram implantados ou instalados?

## <a name="see-also"></a>Consulte Também

- [Investigar um usuário](investigate-a-user.md)
- [Trabalhando com alertas de segurança](working-with-suspicious-activities.md)
- [Trabalhando com caminhos de movimento lateral](use-case-lateral-movement-path.md)
- [Alertas de reconhecimento](atp-reconnaissance-alerts.md)
- [Alertas de credencial comprometida](atp-compromised-credentials-alerts.md)
- [Alertas de movimento lateral](atp-lateral-movement-alerts.md)
- [Alertas de predominância de domínio](atp-domain-dominance-alerts.md)
- [Alertas de exfiltração](atp-exfiltration-alerts.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
