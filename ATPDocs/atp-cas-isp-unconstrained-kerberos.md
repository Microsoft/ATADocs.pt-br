---
title: Avaliação de situação de segurança de identidade irrestrita de Kerberos da Proteção Avançada contra Ameaças do Azure
description: Neste artigo, você tem uma visão geral dos relatórios de avaliação da situação de segurança de identidade irrestrita de Kerberos da ATP do Azure.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 09/15/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 7eea354b-7a50-40d9-bfa7-dcccaef23179
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4938c5a222e6a8c20444ca73e3e119636ed59e83
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2020
ms.locfileid: "79413903"
---
# <a name="security-assessment-unsecure-kerberos-delegation"></a>Avaliação de segurança: delegação de Kerberos não segura


## <a name="what-is-kerberos-delegation"></a>O que é uma delegação Kerberos? 

É uma configuração de delegação que permite que os aplicativos solicitem credenciais de acesso para o usuário final acessar recursos em nome do usuário de origem.  

## <a name="what-risk-does-unsecure-kerberos-delegation-pose-to-an-organization"></a>Qual risco a delegação de Kerberos não segura representa para uma organização? 

Com a delegação de Kerberos não segura, uma entidade pode representar você em qualquer outro serviço escolhido. Por exemplo, imagine que você tem um site de IIS e a conta do pool de aplicativos está configurada com a delegação irrestrita. O site de IIS também tem a Autenticação do Windows habilitada, o que permite à autenticação Kerberos nativa e ao site usar um SQL Server de back-end para dados corporativos. Com a conta do administrador do domínio, navegue até o site de IIS para fazer a autenticação. Com a delegação irrestrita, o site pode receber um tíquete de serviço de um controlador de domínio para o serviço SQL e fazer isso em seu nome.

O principal problema da delegação de Kerberos é que você precisa confiar que o aplicativo sempre tomará a decisão correta. Em vez disso, agentes mal-intencionados podem forçar o aplicativo a errar. Se você estiver conectado como **administrador de domínio**, o site poderá criar o tíquete para qualquer outro serviço, como se fosse você, o **administrador de domínio**. Por exemplo, o site pode escolher um controlador de domínio e alterar o grupo de **admins corporativos**. Do mesmo modo, o site poderia adquirir o hash da conta KRBTGT ou baixar um arquivo interessante do departamento de Recursos Humanos. O risco é claro e as possibilidades com a delegação não segura são quase infinitas. 

 
## <a name="how-do-i-use-this-security-assessment"></a>Como usar a avaliação de segurança?

1. Use a tabela de relatório para descobrir quais das entidades que não estão no controlador de domínio estão configuradas para **delegação de Kerberos não segura**.    
    <br>![Avaliação de segurança da delegação de Kerberos não segura](media/atp-cas-isp-kerberos-delegation-2.png)
1. Tome a medida adequada em relação aos usuários em risco, como remover o atributo irrestrito ou alterá-lo para uma delegação restrita mais segura.

## <a name="remediation"></a>Remediação

Para saber mais sobre como corrigir esses tipos de conta, confira [Remover contas que usam a delegação irrestrita de Kerberos](https://blogs.technet.microsoft.com/389thoughts/2017/04/18/get-rid-of-accounts-that-use-kerberos-unconstrained-delegation/).

## <a name="next-steps"></a>Próximas etapas
- [Filtrar atividades da ATP do Azure no Cloud App Security](atp-activities-filtering-mcas.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
