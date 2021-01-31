---
title: Avaliações de atributos de conta desprotegidas do Microsoft defender para identidade
description: Este artigo fornece uma visão geral do Microsoft defender para entidades de identidade com atributos não seguros relatório de avaliação de postura de segurança de identidade.
ms.date: 01/18/2021
ms.topic: how-to
ms.openlocfilehash: 64aa95a423d0c8fc0bb210c2c10bc63f8c33bca4
ms.sourcegitcommit: 14f7228dbe6af353e81f20d2047dad24043840b4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2021
ms.locfileid: "99217695"
---
# <a name="security-assessment-unsecure-account-attributes"></a>Avaliação de segurança: Atributos de conta não seguros

## <a name="what-are-unsecure-account-attributes"></a>O que são atributos de conta não seguros?

[!INCLUDE [Product long](includes/product-long.md)] monitora continuamente seu ambiente para identificar contas com valores de atributo que expõem um risco de segurança e relatórios sobre essas contas para ajudá-lo a proteger seu ambiente.

## <a name="what-risk-do-unsecure-account-attributes-pose"></a>Que risco representam os atributos de conta não seguros?

As organizações que não conseguem proteger os atributos de conta deixam a porta aberta para atores mal-intencionados.

Agentes mal-intencionados, como ladrões, geralmente procuram a maneira mais fácil e discreta de entrar em um ambiente. As contas configuradas com atributos não seguros são janelas de oportunidade para invasores e podem expor riscos.

Por exemplo, se o atributo *PasswordNotRequired* estiver habilitado, um invasor poderá acessar a conta com facilidade. O risco fica ainda maior se a conta tiver acesso privilegiado a outros recursos.

## <a name="how-do-i-use-this-security-assessment"></a>Como usar a avaliação de segurança?

1. Use a tabela de relatório para descobrir quais das suas contas têm atributos não seguros.
    ![Examinar as principais entidades afetadas e criar um plano de ação](media/cas-isp-unsecure-account-attributes-1.png)
1. Tome medidas apropriadas nessas contas de usuário modificando ou removendo os atributos relevantes.

> [!NOTE]
>
> - Essa avaliação é atualizada quase em tempo real.
> - Essa avaliação poderá conter entidades excluídas anteriormente se os [pré-requisitos](prerequisites.md#before-you-start) do [!INCLUDE [Product long](includes/product-long.md)] não forem atendidos.

## <a name="remediation"></a>Remediação

Use a correção apropriada para o atributo relevante, conforme descrito na tabela a seguir.

| Ação recomendada | Remediação | Motivo |
| --- | --- | --- |
| Remover não requer pré-autenticação Kerberos| Remover essa configuração das propriedades da conta no AD (Active Directory) | A remoção dessa configuração requer uma pré-autenticação do Kerberos para a conta, o que resulta em maior segurança. |
| Remover a configuração Armazenar senha usando criptografia reversível | Remover essa configuração das propriedades da conta no AD | A remoção dessa configuração impede a descriptografia simples da senha da conta. |
| Remover a configuração Senha não obrigatória | Remover essa configuração das propriedades da conta no AD | A remoção dessa configuração torna obrigatório o uso de senha na conta e ajuda a impedir o acesso não autorizado aos recursos. |
| Remover a configuração Senha armazenada com criptografia fraca | Redefinir a senha da conta | Alterar a senha da conta permite que algoritmos de criptografia mais fortes sejam usados para a proteção da conta. |
| Habilitar o suporte à criptografia AES no Kerberos | Habilitar recursos AES nas propriedades da conta no AD | Habilitar AES128_CTS_HMAC_SHA1_96 ou AES256_CTS_HMAC_SHA1_96 na conta ajuda a impedir o uso de criptografias mais fracas para a autenticação do Kerberos. |
| Remover a configuração Usar tipos de criptografia Kerberos DES para esta conta | Remover essa configuração das propriedades da conta no AD | A remoção dessa configuração permite o uso de algoritmos de criptografia mais fortes para a senha da conta. |

## <a name="see-also"></a>Consulte Também

- [[!INCLUDE [Product short](includes/product-short.md)] filtragem de atividades no Cloud App Security](activities-filtering-mcas.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
