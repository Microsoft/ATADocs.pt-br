---
title: Marcar contas confidenciais com o ATA | Microsoft Docs
description: Descreve como marcar contas confidenciais usando o ATA (Advanced Threat Analytics)
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 40a1c5c4-b8d6-477c-8ae5-562b37661624
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: d9666c0a4fb3aad027ac1f85719bc533e919d75a
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2018
---
*Aplica-se a: Advanced Threat Analytics versão 1.9*



# <a name="tag-sensitive-accounts"></a>Marcar contas confidenciais

Você pode marcar manualmente grupos ou contas como confidenciais para aprimorar as detecções. É importante verificar se ele está atualizado porque algumas detecções do ATA, como a detecção de modificação de grupos confidenciais e o caminho de movimento lateral, dependem de quais grupos e contas são considerados confidenciais. Antes, o ATA considerava automaticamente uma entidade *confidencial* se ela fosse membro de uma lista específica de grupos. Agora, você pode marcar manualmente outros usuários ou grupos como confidenciais, como membros da diretoria, executivos ou diretores de vendas da empresa, entre outros, e o ATA os considerará confidenciais.

1.  No console do ATA, clique na engrenagem de **Configuração** na barra de menus.

2.  Em **Detecção**, clique em **Marcas das entidades**.

    ![Marcas das entidades do ATA](media/entity-tags.png)

3.  Na seção **Confidencial**, digite o nome das **Contas confidenciais** e **Grupos confidenciais** e, em seguida, clique no sinal **+** para adicioná-las.

    ![Exemplo de conta confidencial do ATA](media/sensitive-account-sample.png)

4. Clique em **Salvar**.

5. Acesse a página do perfil da entidade clicando no nome da entidade. Aqui, você poderá ver por que a entidade é considerada confidencial, seja devido à associação a um grupo, seja devido à marcação manual como confidencial.

     
## <a name="see-also"></a>Consulte também
[Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
