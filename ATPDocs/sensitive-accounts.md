---
title: Marcar contas confidenciais com o Azure ATP | Microsoft Docs
description: Descreve como marcar contas confidenciais usando o Azure ATP (Proteção Avançada contra Ameaças)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/12/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ccb87ab6b3fabed5edaf7c32324701c74259f098
ms.sourcegitcommit: 5ff50807f855db1051b977a64eb6e90487ea196c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/17/2018
ms.locfileid: "45750430"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*



# <a name="working-with-sensitive-accounts"></a>Trabalhando com contas confidenciais

## <a name="sensitive-groups"></a>Grupos confidenciais

A lista de grupos a seguir é considerada confidencial pelo Azure ATP. Qualquer entidade que é um membro desses grupos é considerada confidencial:

-   Administradores
-   Usuários avançados
-   Opers. de contas
-   Operadores de Servidores
-   Operadores de Impressão
-   Operadores de cópia
-   Replicadores
-   Operadores de Configuração de Rede 
-   Criadores de confiança de floresta de entrada
-   Administradores do domínio
-   Controladores de Domínio
-   Proprietários criadores de política de grupo 
-   Controladores de domínio somente leitura 
-   Controladores de domínio somente leitura da empresa 
-   Administradores de esquemas 
-   Administrador corporativo

 > [!NOTE]
 > Até setembro de 2018, usuários da Área de Trabalho Remota eram considerados confidenciais automaticamente pelo Azure ATP. Entidades ou grupos da Área de Trabalho Remota adicionados após essa data não são mais marcados como confidenciais automaticamente, enquanto as entidades e grupos da Área de Trabalho Remota adicionados antes dessa data podem permanecer marcados como Confidenciais. Essa configuração Confidencial agora pode ser alterada manualmente.  

## <a name="tagging-sensitive-accounts"></a>Marcando contas confidenciais

Além desses grupos, você pode marcar manualmente grupos ou contas como confidenciais para aprimorar as detecções. Isso é importante porque algumas detecções do Azure ATP, como a detecção de modificação de grupos confidenciais e o caminho de movimentação lateral, dependem de quais grupos e contas são consideradas confidenciais. Você pode marcar manualmente outros usuários ou grupos como confidenciais, como membros da diretoria, executivos ou diretores de vendas da empresa, entre outros, e o Azure ATP os considerará como confidenciais.

1.  No portal de espaço de trabalho do Azure ATP, clique na engrenagem de **Configuração** na barra de menus.

2.  Em **Detecção**, clique em **Marcas de entidade**.

    ![Marcas de entidade do Azure ATP](media/entity-tags.png)

3.  Na seção **Confidencial**, digite o nome das **Contas confidenciais** e **Grupos confidenciais** e, em seguida, clique no sinal **+** para adicioná-las.

    ![Exemplo de conta confidencial do Azure ATP](media/sensitive-account-sample.png)

4. Clique em **Salvar**.

    
## <a name="see-also"></a>Consulte também

- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)