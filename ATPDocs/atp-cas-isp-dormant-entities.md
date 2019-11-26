---
title: Avaliações de segurança de entidades inativas da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Neste artigo, você tem uma visão geral do relatório de avaliação da situação de segurança de identidade de grupos confidenciais nas entidades inativas da ATP do Azure.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 158f714602f3add5e23b12a2f3713e9feb4a4bc3
ms.sourcegitcommit: be4525a93601d9356a4e487398262a2ffaf8c202
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2019
ms.locfileid: "74206209"
---
# <a name="security-assessment-dormant-entities-in-sensitive-groups"></a>Avaliação de segurança: entidades inativas em grupos **confidenciais** 

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


## <a name="see-also"></a>Consulte Também
- [Filtrar atividades da ATP do Azure no Cloud App Security](atp-activities-filtering-mcas.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
