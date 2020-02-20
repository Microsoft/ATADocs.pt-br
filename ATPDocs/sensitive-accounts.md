---
title: Marcar contas confidenciais com o Azure ATP | Microsoft Docs
description: Descreve como marcar contas confidenciais usando o Azure ATP (Proteção Avançada contra Ameaças)
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 02/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: cf29a41139973742d6a1be96643104e1cfad0703
ms.sourcegitcommit: 173b9fc26592efec2113c6ee585b04311ddfdbf1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/17/2020
ms.locfileid: "77422006"
---
# <a name="working-with-sensitive-accounts"></a>Trabalhando com contas confidenciais

## <a name="sensitive-entities"></a>Entidades confidenciais

A lista de grupos a seguir é considerada **Confidencial** pelo ATP do Azure. Toda entidade membro de um desses grupos é considerada confidencial:

- Administradores
- Usuários avançados
- Opers. de contas
- Operadores de Servidores
- Operadores de Impressão
- Operadores de cópia
- Replicadores
- Operadores de Configuração de Rede
- Criadores de confiança de floresta de entrada
- Administradores do domínio
- Controladores de Domínio
- Proprietários criadores de política de grupo
- Controladores de domínio somente leitura
- Controladores de domínio somente leitura da empresa
- Administradores de esquemas
- Administrador corporativo
- Servidores do Microsoft Exchange

  > [!NOTE]
  > Até setembro de 2018, usuários da Área de Trabalho Remota eram automaticamente considerados confidenciais pelo ATP do Azure. Entidades ou grupos da Área de Trabalho Remota adicionados após essa data não são mais marcados como confidenciais automaticamente, enquanto as entidades e grupos da Área de Trabalho Remota adicionados antes dessa data podem permanecer marcados como Confidenciais. Essa configuração Confidencial agora pode ser alterada manualmente.

Além desses grupos, o ATP do Azure identifica os seguintes servidores de ativos de alto valor e os marca automaticamente como **Confidenciais**:

- Servidor da Autoridade de Certificação
- Servidor DHCP
- Servidor DNS
- Microsoft Exchange Server

## <a name="tagging-sensitive-accounts"></a>Marcando contas confidenciais

Além desses grupos, você pode marcar manualmente grupos ou contas como confidenciais para aprimorar as detecções. Isso é importante porque algumas detecções do ATP do Azure, como a detecção de modificação de grupos confidenciais e os caminhos de movimentação lateral, dependem de quais grupos e contas são considerados confidenciais. Você pode marcar manualmente outros usuários ou grupos como confidenciais, como membros da diretoria, executivos ou diretores de vendas da empresa, entre outros, e o Azure ATP os considerará como confidenciais.

1. No portal do Azure ATP, clique na engrenagem de **Configuração** na barra de menus.

1. Em **Detecção**, clique em **Marcas de entidade**.

    ![Marcas de entidade do Azure ATP](media/entity-tags.png)

1. Na seção **Confidencial**, digite o nome das **Contas confidenciais** e **Grupos confidenciais** e, em seguida, clique no sinal **+** para adicioná-las.

    ![Exemplo de conta confidencial do Azure ATP](media/sensitive-account-sample.png)

1. Clique em **Salvar**.

## <a name="see-also"></a>Consulte também

- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
