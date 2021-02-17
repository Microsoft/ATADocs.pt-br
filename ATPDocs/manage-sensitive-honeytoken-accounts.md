---
title: Gerenciar contas confidenciais ou honeytoken com o Microsoft defender para identidade
description: Descreve como gerenciar contas confidenciais ou honeytoken usando o Microsoft defender para identidade
ms.date: 02/17/2021
ms.topic: how-to
ms.openlocfilehash: 7078e93ad384d81d59a13ff4b527ca59bc678ad2
ms.sourcegitcommit: f92dca4dc3d8a25b1a06f68ac7a9f8318105bcd8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/17/2021
ms.locfileid: "100630757"
---
# <a name="manage-sensitive-or-honeytoken-accounts"></a>Gerenciar contas confidenciais ou honeytoken

Este artigo explica como aplicar marcas de entidade a contas confidenciais. Isso é importante porque algumas [!INCLUDE [Short long](includes/product-short.md)] detecções, como detecção de modificação de grupo confidencial e caminho de movimento lateral, contam com o status de sensibilidade de uma entidade.

[!INCLUDE [Product short](includes/product-short.md)] também habilita a configuração de contas do honeytoken, que são usadas como interceptações para atores mal-intencionados – qualquer autenticação associada a essas contas do honeytoken (normalmente inativas), dispara um alerta.

## <a name="sensitive-entities"></a>Entidades confidenciais

A lista de grupos a seguir é considerada **Confidencial** pelo [!INCLUDE [Short long](includes/product-short.md)]. Qualquer entidade que seja membro de um desses grupos de Azure Active Directory é considerada confidencial:

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
- Controladores de Domínio somente leitura
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

## <a name="manually-tagging-entities"></a>Marcando entidades manualmente

Você também pode marcar manualmente as entidades como contas confidenciais ou honeytoken. Se você marcar manualmente usuários ou grupos adicionais, como membros do quadro, executivos da empresa e diretores de vendas, [!INCLUDE [Product short](includes/product-short.md)] eles serão considerados confidenciais.

### <a name="to-manually-tag-entities"></a>Para marcar manualmente as entidades

Para marcar as entidades, faça o seguinte:

1. No portal do [!INCLUDE [Product short](includes/product-short.md)], selecione **Configuração**.

    ![[! INCLUIR definições de configuração [produto curto] (inclui/produto-curto. MD)]](media/config-menu.png)

1. Em **detecção**, selecione **marcas de entidade**.

    ![Marcas de entidade do [!INCLUDE [Product short](includes/product-short.md)]](media/entity-tags.png)

1. Para cada conta que você deseja configurar, faça o seguinte:
    1. Em **contas do Honeytoken** ou **confidenciais**, insira o nome da conta.
    1. Clique no ícone de adição **(+)**.

    > [!TIP]
    > O campo de conta confidencial ou honeytoken é pesquisável e fará preenchimento automático com entidades em sua rede.

    ![Exemplo de conta confidencial do [!INCLUDE [Product short](includes/product-short.md)]](media/sensitive-account-sample.png)

1. Clique em **Salvar**.

## <a name="see-also"></a>Veja também

- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
