---
title: Avaliação de exposição de texto não criptografado da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Neste artigo, você tem uma visão geral do relatório de avaliação da situação de segurança de identidade da exposição de texto não criptografado da ATP do Azure.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 124957bb-5882-4fcf-bab2-b74b0c69571d
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8e99ab22e65538aba6f645d6bb7929330244cafc
ms.sourcegitcommit: 475df3e87d8476ff13e48ebc7a722f46f29dab70
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/16/2019
ms.locfileid: "71007536"
---
# <a name="security-assessment-entities-exposing-credentials-in-clear-text-----preview"></a>Avaliação de segurança: entidades expondo credenciais em texto não criptografado – versão prévia

![Impedir a exposição das credenciais de texto não criptografado no Cloud App Security](media/atp-cas-isp-clear-text-1.png)

## <a name="what-information-does-the-prevent-clear-text-security-assessment-provide"></a>Quais informações a avaliação de segurança de texto não criptografado fornece? 

Essa avaliação de segurança monitora o tráfego para quaisquer entidades que exponham credenciais em texto não criptografado e alerta você para os riscos atuais de exposição (entidades mais afetadas) na sua organização com as correções sugeridas. 

## <a name="why-is-clear-text-credential-exposure-risky"></a>Por que a exposição de credenciais de texto não criptografado é arriscada?  
As entidades que expõem credenciais de texto não criptografado são arriscadas não somente por causa da entidade exposta em questão, mas também para toda a organização.  

O maior risco é o tráfego não seguro, pois a associação simples com a LDAP é altamente suscetível a interceptação por meio de ataques attacker-in-the-middle. Esses tipos de ataques resultam em atividades mal-intencionadas, incluindo a exposição de credenciais, em que um invasor pode usar as credenciais para fins mal-intencionados. 

## <a name="how-do-i-use-this-security-assessment-to-improve-my-organizational-security-posture"></a>Como usar esta avaliação de segurança para aprimorar minha situação de segurança organizacional? 

1. Analise a avaliação de segurança para as entidades afetadas. 
    ![Examinar as principais entidades afetadas e criar um plano de ação](media/atp-cas-isp-clear-text-2.png)
1. Pesquise por que essas entidades estão usando LDAP em texto não criptografado. 
1. Corrija os problemas e interrompa a exposição. 
1. Após confirmar a correção, é recomendável solicitar uma assinatura LDAP no nível de controlador de domínio. Para saber mais sobre a assinatura de servidor LDAP, confira [Requisitos de assinatura de servidor LDAP do controlador de domínio](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/domain-controller-ldap-server-signing-requirements). 
 

## <a name="next-steps"></a>Próximas etapas
- [Filtrar atividades da ATP do Azure no Cloud App Security](atp-activities-filtering-mcas.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
