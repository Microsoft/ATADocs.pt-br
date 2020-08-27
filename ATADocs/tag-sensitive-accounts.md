---
title: Marcar contas confidenciais com o ATA
description: Descreve como marcar contas confidenciais usando o ATA (Advanced Threat Analytics)
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 6/14/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 40a1c5c4-b8d6-477c-8ae5-562b37661624
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ba1cf2cb1d9cceaa07dfa1db9df533d7c57dae64
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88956458"
---
# <a name="tag-sensitive-accounts"></a>Marcar contas confidenciais


*Aplica-se a: Advanced Threat Analytics versão 1.9*

Você pode marcar manualmente grupos ou contas como confidenciais para aprimorar as detecções. É importante verificar se ele está atualizado porque algumas detecções do ATA, como a detecção de modificação de grupos confidenciais e o caminho de movimento lateral, dependem de quais grupos e contas são considerados confidenciais. Antes, o ATA considerava automaticamente uma entidade *confidencial* se ela fosse membro de uma lista específica de grupos. Agora, você pode marcar manualmente outros usuários ou grupos como confidenciais, como membros da diretoria, executivos ou diretores de vendas da empresa, entre outros, e o ATA os considerará confidenciais.

1. No console do ATA, clique na engrenagem de **Configuração** na barra de menus.

1. Em **Detecção**, clique em **Marcas das entidades**.

    ![Marcas das entidades do ATA](media/entity-tags.png)

1. Na seção **Confidencial**, digite o nome das **Contas confidenciais** e **Grupos confidenciais** e, em seguida, clique no sinal **+** para adicioná-las.

    ![Exemplo de conta confidencial do ATA](media/sensitive-account-sample.png)

1. Clique em **Save** (Salvar).

1. Acesse a página do perfil da entidade clicando no nome da entidade. Aqui, você poderá ver por que a entidade é considerada confidencial, seja devido à associação a um grupo, seja devido à marcação manual como confidencial.


## <a name="sensitive-groups"></a>Grupos confidenciais

A lista de grupos a seguir é considerada Confidencial pelo ATA. Qualquer entidade que é um membro desses grupos é considerada confidencial:

- Administradores
- Usuários avançados
- Opers. de contas
- Opers. de servidores
- Operadores de Impressão
- Operadores de cópia
- Replicadores
- Usuários da Área de Trabalho Remota 
- Operadores de configuração de rede 
- Criadores de confiança de floresta de entrada
- Administradores de Domínio
- Controladores de Domínio
- Proprietários criadores de política de grupo 
- Controladores de domínio somente leitura 
- Controladores de domínio somente leitura da empresa 
- Administradores de esquemas 
- Administradores Corporativos
     
## <a name="see-also"></a>Confira também
[Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
