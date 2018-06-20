---
title: Marcar contas confidenciais com o Azure ATP | Microsoft Docs
description: Descreve como marcar contas confidenciais usando o Azure ATP (Proteção Avançada contra Ameaças)
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4270ebda76309e19518f9d49b72bbce7f9bb5f32
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2018
ms.locfileid: "29444952"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure versão 1.9*



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
-   Usuários da Área de Trabalho Remota 
-   Operadores de Configuração de Rede 
-   Criadores de confiança de floresta de entrada
-   Administradores do domínio
-   Controladores de Domínio
-   Proprietários criadores de política de grupo 
-   Controladores de domínio somente leitura 
-   Controladores de domínio somente leitura da empresa 
-   Administradores de esquemas 
-   Administrador corporativo


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