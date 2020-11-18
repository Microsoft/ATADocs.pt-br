---
title: Avaliações de caminhos de movimento lateral do Microsoft defender para identidade difuso
description: Este artigo fornece uma visão geral do Microsoft defender para entidades confidenciais de identidade com o relatório de avaliação de postura de segurança de identidades de caminhos de movimento difuso lateral.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 40175ace8046ae7b0edb77f4cac6e036eed997e7
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848339"
---
# <a name="security-assessment-riskiest-lateral-movement-paths-lmp"></a>Avaliação de segurança: LMP (caminhos de movimento lateral) mais arriscados

## <a name="what-are-risky-lateral-movement-paths"></a>O que são caminhos de movimento lateral arriscados?

[!INCLUDE [Product long](includes/product-long.md)] monitora continuamente seu ambiente para identificar contas **confidenciais** com caminhos de movimento lateral difuso que expõem um risco de segurança e relatórios sobre essas contas para ajudá-lo a gerenciar seu ambiente. Os caminhos serão considerados arriscados se tiverem três ou mais contas não confidenciais capazes de expor a conta **confidencial** a roubo de credenciais por atores mal-intencionados.

Saiba mais sobre LMP:

- [[!INCLUDE [Product short](includes/product-short.md)] LMPs (caminhos de movimento lateral)](use-case-lateral-movement-path.md)
- [Movimento lateral do MITRE ATT&CK](https://attack.mitre.org/tactics/TA0008/)

## <a name="what-risk-do-risky-lateral-movement-paths-pose"></a>Que risco representam os caminhos de movimento lateral arriscados?

As organizações que não conseguem proteger as contas **confidenciais** deixam a porta aberta para atores mal-intencionados.

Agentes mal-intencionados, como ladrões, geralmente procuram a maneira mais fácil e discreta de entrar em um ambiente. Contas confidenciais com caminhos de movimento lateral arriscados são janelas de oportunidade para invasores e podem representar riscos.

Por exemplo, os caminhos mais arriscados ficam mais visíveis ao invasor e, se comprometidos, podem fornecer ao invasor acesso às entidades mais confidenciais da organização.

## <a name="how-do-i-use-this-security-assessment"></a>Como usar a avaliação de segurança?

1. Use a tabela de relatório para descobrir quais das suas contas **confidenciais** têm LMPs arriscados.
    ![Examinar as principais entidades afetadas e criar um plano de ação](media/cas-isp-riskiest-lmp-1.png)
1. Tome medidas apropriadas:
    - Remova a entidade do grupo, conforme especificado na recomendação.
    - Remova as permissões de administrador local para a entidade do dispositivo especificado na recomendação.

    > [!NOTE]
    > Aguarde 24 horas e verifique se a recomendação deixou de aparecer na lista.

> [!NOTE]
> Essa avaliação é atualizada a cada 24 horas.

## <a name="see-also"></a>Consulte Também

- [[!INCLUDE [Product short](includes/product-short.md)] filtragem de atividades no Cloud App Security](activities-filtering-mcas.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
