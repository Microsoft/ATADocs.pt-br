---
title: Avaliações de segurança de entidades inativas da Proteção Avançada contra Ameaças do Azure
description: Neste artigo, você tem uma visão geral do relatório de avaliação da situação de segurança de identidade de grupos confidenciais nas entidades inativas da ATP do Azure.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: db289191d8520a478867c3a2ff3c1b47267e82f1
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90913175"
---
# <a name="security-assessment-dormant-entities-in-sensitive-groups"></a>Avaliação de segurança: entidades inativas em grupos **confidenciais**

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="what-are-sensitive-dormant-entities"></a>O que são entidades inativas **confidenciais**?

A ATP do Azure descobre se determinados usuários são **confidenciais** e fornece atributos que indicam se eles estão inativos, desabilitados ou expirados.

No entanto, as contas **confidenciais** também poderão se tornar *inativas* se não forem usadas por um período de 180 dias. As [entidades inativas](sensitive-accounts.md) são oportunidades para agentes mal-intencionados terem acesso confidencial à sua organização.

## <a name="what-risk-do-dormant-entities-create-in-sensitive-groups"></a>Qual risco as entidades inativas criam nos grupos **confidenciais**?

As organizações que não protegem as contas de usuário inativas deixam uma porta aberta para seus dados confidenciais.

Agentes mal-intencionados, como ladrões, geralmente procuram a maneira mais fácil e discreta de entrar em um ambiente. O caminho mais fácil e discreto para sua organização são os usuários **confidenciais** e as contas de serviço inativas.

Não importa se o motivo é a rotatividade de funcionários ou uma má gestão de recursos – ignorar esta etapa deixa as entidades mais confidenciais da organização vulneráveis e expostas.

## <a name="how-do-i-use-this-security-assessment"></a>Como usar a avaliação de segurança?

1. Use a tabela do relatório para descobrir quais das suas contas confidenciais estão inativas.
1. Tome a medida adequada em relação a essas contas de usuário removendo os direitos de acesso com privilégios delas ou excluindo-as.

> [!NOTE]
> Essa avaliação é atualizada quase em tempo real.

## <a name="see-also"></a>Consulte Também

- [Filtrar atividades da ATP do Azure no Cloud App Security](activities-filtering-mcas.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
