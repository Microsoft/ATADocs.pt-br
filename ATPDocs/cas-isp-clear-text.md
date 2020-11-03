---
title: Avaliação de exposição de texto não criptografado do Microsoft defender para identidade
description: Este artigo fornece uma visão geral do relatório de avaliação de postura de segurança de identidade de exposição de texto não criptografado do Microsoft defender.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9586c5441f09959970752a15cfff3c2f953f1842
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93277594"
---
# <a name="security-assessment-entities-exposing-credentials-in-clear-text"></a>Avaliação de segurança: entidades que expõem credenciais em texto não criptografado

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

![Impedir a exposição das credenciais de texto não criptografado no Cloud App Security](media/cas-isp-clear-text-1.png)

## <a name="what-information-does-the-prevent-clear-text-security-assessment-provide"></a>Quais informações a avaliação de segurança de texto não criptografado fornece?

Essa avaliação de segurança monitora o tráfego para quaisquer entidades que exponham credenciais em texto não criptografado e alerta você para os riscos atuais de exposição (entidades mais afetadas) na sua organização com as correções sugeridas.

## <a name="why-is-clear-text-credential-exposure-risky"></a>Por que a exposição de credenciais de texto não criptografado é arriscada?

As entidades que expõem credenciais de texto não criptografado são arriscadas não somente por causa da entidade exposta em questão, mas também para toda a organização.

O maior risco é o tráfego não seguro, pois a associação simples com a LDAP é altamente suscetível a interceptação por meio de ataques attacker-in-the-middle. Esses tipos de ataques resultam em atividades mal-intencionadas, incluindo a exposição de credenciais, em que um invasor pode usar as credenciais para fins mal-intencionados.

## <a name="how-do-i-use-this-security-assessment-to-improve-my-organizational-security-posture"></a>Como usar esta avaliação de segurança para aprimorar minha situação de segurança organizacional?

1. Analise a avaliação de segurança para as entidades afetadas.
    ![Examinar as principais entidades afetadas e criar um plano de ação](media/cas-isp-clear-text-2.png)
1. Pesquise por que essas entidades estão usando LDAP em texto não criptografado.
1. Corrija os problemas e interrompa a exposição.
1. Após confirmar a correção, é recomendável solicitar uma assinatura LDAP no nível de controlador de domínio. Para saber mais sobre a assinatura de servidor LDAP, confira [Requisitos de assinatura de servidor LDAP do controlador de domínio](/windows/security/threat-protection/security-policy-settings/domain-controller-ldap-server-signing-requirements).

> [!NOTE]
> Essa avaliação é atualizada quase em tempo real.

## <a name="next-steps"></a>Próximas etapas

- [[!INCLUDE [Product short](includes/product-short.md)] filtragem de atividades no Cloud App Security](activities-filtering-mcas.md)
- [Confira o [!INCLUDE [Product short](includes/product-short.md)] Fórum!](https://aka.ms/MDIcommunity)