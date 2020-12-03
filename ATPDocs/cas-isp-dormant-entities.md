---
title: Avaliações de segurança de entidades inativas do Microsoft defender for Identity inativos
description: Este artigo fornece uma visão geral das entidades inativas do Microsoft defender for Identity inativos em grupos confidenciais relatório de avaliação de postura de segurança de identidade.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: e96b7af917f898c7ef9f701b7e7ffda1cf001598
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96544191"
---
# <a name="security-assessment-dormant-entities-in-sensitive-groups"></a>Avaliação de segurança: entidades inativas em grupos **confidenciais**

## <a name="what-are-sensitive-dormant-entities"></a>O que são entidades inativas **confidenciais**?

[!INCLUDE [Product long](includes/product-long.md)] descobre se usuários específicos são **confidenciais** junto com o fornecimento de atributos que se encontram inativos, desabilitados ou expirados.

No entanto, as contas **confidenciais** também poderão se tornar *inativas* se não forem usadas por um período de 180 dias. As [entidades inativas](sensitive-accounts.md) são oportunidades para agentes mal-intencionados terem acesso confidencial à sua organização.

## <a name="what-risk-do-dormant-entities-create-in-sensitive-groups"></a>Qual risco as entidades inativas criam nos grupos **confidenciais**?

As organizações que não protegem as contas de usuário inativas deixam uma porta aberta para seus dados confidenciais.

Agentes mal-intencionados, como ladrões, geralmente procuram a maneira mais fácil e discreta de entrar em um ambiente. Um caminho fácil e silencioso em sua organização é por meio de contas de usuário e serviço **confidenciais** que não estão mais em uso.

Não importa se o motivo é a rotatividade de funcionários ou uma má gestão de recursos – ignorar esta etapa deixa as entidades mais confidenciais da organização vulneráveis e expostas.

## <a name="how-do-i-use-this-security-assessment"></a>Como usar a avaliação de segurança?

1. Use a tabela do relatório para descobrir quais das suas contas confidenciais estão inativas.
    ![Corrigir grupos confidenciais do ini de entidades inativas](media/cas-isp-dormant-entities-sensitive-groups-1.png)
1. Tome a medida adequada em relação a essas contas de usuário removendo os direitos de acesso com privilégios delas ou excluindo-as.

> [!NOTE]
> Essa avaliação é atualizada quase em tempo real.

## <a name="see-also"></a>Consulte Também

- [[!INCLUDE [Product short](includes/product-short.md)] filtragem de atividades no Cloud App Security](activities-filtering-mcas.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
