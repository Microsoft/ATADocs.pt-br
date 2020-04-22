---
title: Tutorial de investigação de computador do ATP do Azure
d|Description: This article explains how to use Azure ATP security alerts to investigate a suspicious computer.
keywords: ''
author: shsagir
ms.author: shsagir
ms.date: 09/15/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 038b31aa221f2807a149998e657065289a82c4a3
ms.sourcegitcommit: 63be53de5b84eabdeb8c006438dab45bd35a4ab7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2020
ms.locfileid: "80669488"
---
# <a name="tutorial-investigate-a-computer"></a>Tutorial: Investigar um computador

> [!NOTE]
> Os recursos do ATP do Azure explicados nesta página também podem ser acessados usando o novo [portal](https://portal.cloudappsecurity.com).

A evidência de alerta do ATP do Azure fornece indicações claras de quando computadores foram envolvidos em atividades suspeitas ou de quando há informações de que um computador está comprometido. Neste tutorial, você usará as sugestões de investigação para identificar o risco para a organização, decidir como corrigir e determinar a melhor maneira de evitar ataques semelhantes no futuro.  

> [!div class="checklist"]
> * Verifique o computador quanto ao usuário conectado.
> * Verifique se o usuário normalmente acessa os computadores.
> * Investigue as atividades suspeitas do computador.
> * Houve outros alertas por volta do mesmo horário?


## <a name="investigation-steps-for-suspicious-computers"></a>Etapas de investigação para computadores suspeitos

Para acessar a página de perfil do computador, clique no computador específico mencionado no alerta que você deseja investigar. Para ajudar na investigação, a evidência de alerta lista todos os computadores (e [usuários](investigate-a-user.md)) conectados a cada atividade suspeita.

Verifique e investigue o perfil do computador para obter as atividades e os detalhes a seguir:

- O que aconteceu no momento da atividade suspeita?  
  1. Qual [usuário](investigate-a-user.md) estava conectado ao computador?
  2. Esse usuário normalmente faz logon ou acessa o computador de origem ou de destino?
  3. Quais recursos foram acessados? Por quais usuários?
      - Se os recursos foram acessados, eles eram de alto valor?
  4. O usuário deveria acessar esses recursos?
  5. O [usuário](investigate-a-user.md) que acessou o computador executou outras atividades suspeitas?

- Atividades suspeitas adicionais a serem investigadas:
    1. Havia outros alertas abertos ao mesmo tempo que este alerta no ATP do Azure ou em outras ferramentas de segurança, como o Microsoft Defender ATP, a Central de Segurança do Azure e/ou o Microsoft CAS?
    2. Houve logons com falha?


- Se a integração do Microsoft Defender ATP estiver habilitada, clique na notificação do Microsoft Defender ATP para investigar o computador em mais detalhes. No Microsoft Defender ATP, você pode ver quais processos e alertas ocorreram no mesmo período que o alerta.
    1. Novos programas foram implantados ou instalados?

## <a name="next-steps"></a>Próximas etapas

- [Investigar um usuário](investigate-a-user.md)
- [Trabalhando com alertas de segurança](working-with-suspicious-activities.md)
- [Trabalhando com caminhos de movimento lateral](use-case-lateral-movement-path.md)
- [Alertas de reconhecimento](atp-reconnaissance-alerts.md)
- [Alertas de credencial comprometida](atp-compromised-credentials-alerts.md)
- [Alertas de movimento lateral](atp-lateral-movement-alerts.md)
- [Alertas de predominância de domínio](atp-domain-dominance-alerts.md)
- [Alertas de exfiltração](atp-exfiltration-alerts.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
