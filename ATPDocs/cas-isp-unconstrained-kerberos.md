---
title: Avaliação de postura de segurança de identidade Kerberos não restringida do Microsoft defender para identidade
description: Este artigo fornece uma visão geral do Microsoft defender para relatórios de avaliação de postura de segurança de identidade Kerberos irrestrito da identidade.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 796dd3539f26ace93bd36a60f88c292d65de24b0
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96543579"
---
# <a name="security-assessment-unsecure-kerberos-delegation"></a>Avaliação de segurança: delegação de Kerberos não segura

## <a name="what-is-kerberos-delegation"></a>O que é uma delegação Kerberos?

É uma configuração de delegação que permite que os aplicativos solicitem credenciais de acesso para o usuário final acessar recursos em nome do usuário de origem.

## <a name="what-risk-does-unsecure-kerberos-delegation-pose-to-an-organization"></a>Qual risco a delegação de Kerberos não segura representa para uma organização?

Com a delegação de Kerberos não segura, uma entidade pode representar você em qualquer outro serviço escolhido. Por exemplo, imagine que você tem um site de IIS e a conta do pool de aplicativos está configurada com a delegação irrestrita. O site de IIS também tem a Autenticação do Windows habilitada, o que permite à autenticação Kerberos nativa e ao site usar um SQL Server de back-end para dados corporativos. Com a conta do administrador do domínio, navegue até o site de IIS para fazer a autenticação. O site, usando a delegação irrestrita, pode obter um tíquete de serviço de um controlador de domínio para o serviço do SQL e fazer isso em seu nome.

O principal problema da delegação de Kerberos é que você precisa confiar que o aplicativo sempre tomará a decisão correta. Em vez disso, agentes mal-intencionados podem forçar o aplicativo a errar. Se você estiver conectado como **administrador de domínio**, o site poderá criar um tíquete para qualquer outro serviço que desejar, agindo como você, o **administrador de domínio**. Por exemplo, o site pode escolher um controlador de domínio e fazer alterações no grupo de **Administração de empresa** . Do mesmo modo, o site poderia adquirir o hash da conta KRBTGT ou baixar um arquivo interessante do departamento de Recursos Humanos. O risco é claro e as possibilidades com a delegação não segura são quase infinitas.

Veja a seguir uma descrição do risco representado por tipos diferentes de delegação:

- **Delegação irrestrita**: qualquer serviço poderá ser explorado se uma das entradas de delegação for confidencial.
- **Delegação restrita**: entidades restritas poderão ser exploradas se uma das entradas de delegação for confidencial.
- **RBCD (delegação restrita baseada em recursos)** : entidades restritas baseadas em recursos poderão ser exploradas se a entidade em questão for confidencial.

## <a name="how-do-i-use-this-security-assessment"></a>Como usar a avaliação de segurança?

1. Use a tabela de relatório para descobrir quais das entidades que não estão no controlador de domínio estão configuradas para **delegação de Kerberos não segura**.

    ![Avaliação de segurança da delegação de Kerberos não segura](media/cas-isp-kerberos-delegation-2.png)
1. Tome a medida adequada em relação aos usuários em risco, como remover o atributo irrestrito ou alterá-lo para uma delegação restrita mais segura.

> [!NOTE]
> Essa avaliação é atualizada a cada 24 horas.

## <a name="remediation"></a>Remediação

Use a correção apropriada para o tipo de delegação.

### <a name="unconstrained-delegation"></a>Delegação irrestrita

Desabilite a delegação ou use um dos seguintes tipos de KCD (delegação restrita de Kerberos):

- **Delegação restrita:** restringe os serviços que a conta pode representar.

    1. Selecione **Confiar no computador para delegação apenas a serviços especificados**.

        ![Correção de delegação irrestrita de Kerberos](media/cas-isp-unconstrained-kerberos-1.png)

    2. Especifique os **Serviços aos quais esta conta pode apresentar credenciais delegadas**.

- **Delegação restrita baseada em recursos:** restringe as entidades que podem representar a conta.  
A KCD baseada em recursos é configurada no PowerShell. Use os cmdlets [Set-ADComputer](/powershell/module/addsadministration/set-adcomputer?view=win10-ps&preserve-view=true) ou [Set-ADUser](/powershell/module/addsadministration/set-aduser?view=win10-ps&preserve-view=true) de acordo com o tipo da conta de representação (por exemplo, conta de computador, conta de usuário ou conta de serviço).

### <a name="constrained-delegation"></a>Delegação restrita

Examine os usuários confidenciais listados nas recomendações e remova-os dos serviços nos quais a conta afetada pode apresentar credenciais delegadas.

![Correção de delegação restrita de Kerberos](media/cas-isp-unconstrained-kerberos-2.png)

### <a name="resource-based-constrained-delegation-rbcd"></a>RBCD (delegação restrita baseada em recursos)

Examine os usuários confidenciais listados nas recomendações e remova-os do recurso. Para saber mais sobre como configurar a RBCD, confira [Configurar a KCD (delegação restrita de Kerberos) no Azure Active Directory Domain Services](/azure/active-directory-domain-services/deploy-kcd).

## <a name="next-steps"></a>Próximas etapas

- [[!INCLUDE [Product short](includes/product-short.md)] filtragem de atividades no Cloud App Security](activities-filtering-mcas.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
