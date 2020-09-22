---
title: Avaliações de atributos de histórico de SID não seguro da Proteção Avançada contra Ameaças do Azure
description: Este artigo fornece uma visão geral das entidades do ATP do Azure com um relatório de avaliação da postura de segurança de identidades de atributos do Histórico de SID não seguro.
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
ms.openlocfilehash: 7819bf79ca70068be21f0aae0b08ff920d7a1605
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912740"
---
# <a name="security-assessment-unsecure-sid-history-attributes"></a>Avaliação de segurança: atributos do Histórico de SID não seguro

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="what-is-an-unsecure-sid-history-attribute"></a>O que é um atributo de Histórico de SID não seguro?

O Histórico de SID é um atributo que dá suporte a [cenários de migração](/previous-versions/windows/it-pro/windows-server-2003/cc779590(v=ws.10)). Cada conta de usuário tem uma [SID (Identificador de Segurança)](/windows/win32/secauthz/security-identifiers) usada para acompanhar a entidade de segurança e o acesso que a conta tem ao se conectar aos recursos. O Histórico de SID permite que o acesso a outra conta seja clonado efetivamente para outra e é extremamente útil para verificar se os usuários mantêm o acesso quando movidos (migrados) de um domínio para outro.

A avaliação verifica se há contas com atributos de Histórico de SID que o ATP do Azure analisa como sendo de risco.

## <a name="what-risk-does-unsecure-sid-history-attribute-pose"></a>Que risco o atributo de Histórico de SID não seguro apresenta?

As organizações que não conseguem proteger os atributos de conta deixam a porta aberta para atores mal-intencionados.

Agentes mal-intencionados, como ladrões, geralmente procuram a maneira mais fácil e discreta de entrar em um ambiente. Contas configuradas com um atributo de Histórico de SID não seguro são oportunidades para invasores e podem apresentar riscos.

Por exemplo, uma conta não confidencial em um domínio pode conter a SID de administrador corporativo no Histórico de SID dela em outro domínio na floresta do Active Directory, “elevando”, portanto, o acesso da conta de usuário a um Administrador de Domínio efetivo em todos os domínios da floresta. Além disso, se você tiver uma relação de confiança de floresta sem o Filtro de SID habilitado (também chamado de Quarentena), será possível injetar uma SID de outra floresta e ela será adicionada ao token de usuário quando autenticado e usada para avaliações de acesso.

## <a name="how-do-i-use-this-security-assessment"></a>Como usar a avaliação de segurança?

1. Use a tabela de relatório para descobrir quais contas suas têm um atributo de Histórico de SID não seguro.
    ![Examinar as principais entidades afetadas e criar um plano de ação](media/atp-cas-isp-unsecure-sid-history-attribute-1.png)
1. Execute a ação apropriada para remover o atributo de Histórico de SID das contas que usam o PowerShell usando as seguintes etapas:

    1. Identifique a SID no atributo SIDHistory na conta.

        ```powershell
        Get-ADUser -Identity <account> -Properties SidHistory | Select-Object -ExpandProperty SIDHistory
        ```

    2. Remova o atributo SIDHistory usando a SID identificada anteriormente.

        ```powershell
        Set-ADUser -Identity <account> -Remove @{SIDHistory='S-1-5-21-...'}
        ```

> [!NOTE]
> Essa avaliação é atualizada quase em tempo real.

## <a name="see-also"></a>Consulte Também

- [Filtrar atividades da ATP do Azure no Cloud App Security](activities-filtering-mcas.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
