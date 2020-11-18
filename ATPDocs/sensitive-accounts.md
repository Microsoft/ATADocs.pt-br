---
title: Marcar contas como confidenciais com o Microsoft Defender para Identidade
description: Descreve como marcar contas como confidenciais usando o Microsoft Defender para Identidade
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 3f32d974b9dcfb946279b14eebc116ca74b5b3f5
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94846911"
---
# <a name="working-with-sensitive-accounts"></a>Trabalhando com contas confidenciais

## <a name="sensitive-entities"></a>Entidades confidenciais

A lista de grupos a seguir é considerada **Confidencial** pelo [!INCLUDE [Product long](includes/product-long.md)]. Toda entidade membro de um desses grupos é considerada confidencial:

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
  > Até setembro de 2018, usuários da Área de Trabalho Remota eram automaticamente considerados confidenciais pelo [!INCLUDE [Product short](includes/product-short.md)]. Entidades ou grupos da Área de Trabalho Remota adicionados após essa data não são mais marcados como confidenciais automaticamente, enquanto as entidades e grupos da Área de Trabalho Remota adicionados antes dessa data podem permanecer marcados como Confidenciais. Essa configuração Confidencial agora pode ser alterada manualmente.

Além desses grupos, o [!INCLUDE [Product short](includes/product-short.md)] identifica os seguintes servidores de ativos de alto valor e os marca automaticamente como **Confidenciais**:

- Servidor da Autoridade de Certificação
- Servidor DHCP
- Servidor DNS
- Microsoft Exchange Server

## <a name="tagging-sensitive-accounts"></a>Marcando contas confidenciais

Além desses grupos, você pode marcar manualmente grupos ou contas como confidenciais para aprimorar as detecções. Isso é importante porque algumas detecções do [!INCLUDE [Product short](includes/product-short.md)], como a detecção de modificação de grupos confidenciais e os caminhos de movimentação lateral, dependem de quais grupos e contas são considerados confidenciais. Você pode marcar manualmente outros usuários ou grupos como confidenciais, por exemplo, membros da diretoria, executivos, diretores de vendas da empresa, entre outros, e o [!INCLUDE [Product short](includes/product-short.md)] os considerará como confidenciais.

1. No portal do [!INCLUDE [Product short](includes/product-short.md)], selecione **Configuração**.

1. Em **Detecção**, clique em **Marcas de entidade**.

    ![Marcas de identidade do [!INCLUDE [Product short](includes/product-short.md)]](media/entity-tags.png)

1. Na seção **Confidencial**, digite o nome das **Contas confidenciais** e **Grupos confidenciais** e, em seguida, clique no sinal **+** para adicioná-las.

    ![Exemplo de conta confidencial do [!INCLUDE [Product short](includes/product-short.md)]](media/sensitive-account-sample.png)

1. Clique em **Salvar**.

## <a name="see-also"></a>Veja também

- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
