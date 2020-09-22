---
title: Avaliações de atributos de conta não seguros da Proteção Avançada contra Ameaças do Azure
description: Este artigo fornece uma visão geral das entidades do ATP do Azure com um relatório de avaliação da postura de segurança de identidades dos atributos não seguros.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d0f415d58026fe0e44b365d7f8a6f995226532bc
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912752"
---
# <a name="security-assessment-unsecure-account-attributes"></a>Avaliação de segurança: Atributos de conta não seguros

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="what-are-unsecure-account-attributes"></a>O que são atributos de conta não seguros?

O ATP do Azure monitora continuamente o ambiente para identificar contas com valores de atributo que expõem um risco de segurança e para identificar relatórios sobre essas contas a fim de ajudar você a proteger o ambiente.

## <a name="what-risk-do-unsecure-account-attributes-pose"></a>Que risco representam os atributos de conta não seguros?

As organizações que não conseguem proteger os atributos de conta deixam a porta aberta para atores mal-intencionados.

Agentes mal-intencionados, como ladrões, geralmente procuram a maneira mais fácil e discreta de entrar em um ambiente. Contas configuradas com atributos não seguros são janelas de oportunidade para invasores e podem representar riscos.

Por exemplo, se o atributo *PasswordNotRequired* estiver habilitado, um invasor poderá acessar a conta com facilidade. O risco fica ainda maior se a conta tiver acesso privilegiado a outros recursos.

## <a name="how-do-i-use-this-security-assessment"></a>Como usar a avaliação de segurança?

1. Use a tabela de relatório para descobrir quais das suas contas têm atributos não seguros.
    ![Examinar as principais entidades afetadas e criar um plano de ação](media/atp-cas-isp-unsecure-account-attributes-1.png)
1. Tome medidas apropriadas nessas contas de usuário modificando ou removendo os atributos relevantes.

> [!NOTE]
> Essa avaliação é atualizada quase em tempo real.

## <a name="remediation"></a>Remediação

Use a correção apropriada para o atributo relevante, conforme descrito na tabela a seguir.

| Ação recomendada | Remediação | Motivo |
| --- | --- | --- |
| Remover a configuração Usar tipos de criptografia Kerberos DES para esta conta| Remover essa configuração das propriedades da conta no AD (Active Directory) | A remoção dessa configuração requer uma pré-autenticação do Kerberos para a conta, o que resulta em maior segurança. |
| Remover a configuração Armazenar senha usando criptografia reversível | Remover essa configuração das propriedades da conta no AD | A remoção dessa configuração impede a descriptografia simples da senha da conta. |
| Remover a configuração Senha não obrigatória | Remover essa configuração das propriedades da conta no AD | A remoção dessa configuração torna obrigatório o uso de senha na conta e ajuda a impedir o acesso não autorizado aos recursos. |
| Remover a configuração Senha armazenada com criptografia fraca | Redefinir a senha da conta | Alterar a senha da conta permite que algoritmos de criptografia mais fortes sejam usados para a proteção da conta. |
| Habilitar o suporte à criptografia AES no Kerberos | Habilitar recursos AES nas propriedades da conta no AD | Habilitar AES128_CTS_HMAC_SHA1_96 ou AES256_CTS_HMAC_SHA1_96 na conta ajuda a impedir o uso de criptografias mais fracas para a autenticação do Kerberos. |
| Remover a configuração Usar tipos de criptografia Kerberos DES para esta conta | Remover essa configuração das propriedades da conta no AD | A remoção dessa configuração permite o uso de algoritmos de criptografia mais fortes para a senha da conta. |

## <a name="see-also"></a>Consulte Também

- [Filtrar atividades da ATP do Azure no Cloud App Security](activities-filtering-mcas.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
