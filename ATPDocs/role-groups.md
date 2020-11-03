---
title: Microsoft defender para grupos de funções de identidade para gerenciamento de acesso
description: Percorre como trabalhar com o Microsoft defender para grupos de funções de identidade.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 02/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 269343e6cdc5ceba875d5b6de1c740415a862eca
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93275302"
---
# <a name="product-long-role-groups"></a>[!INCLUDE [Product long](includes/product-long.md)] grupos de funções

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

[!INCLUDE [Product long](includes/product-long.md)] oferece segurança baseada em função para proteger dados de acordo com as necessidades específicas de segurança e conformidade de uma organização. [!INCLUDE [Product short](includes/product-short.md)] suporte a três funções separadas: administradores, usuários e visualizadores.

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

Grupos de funções permitem o gerenciamento de acesso para o [!INCLUDE [Product short](includes/product-short.md)] . Com os grupos de função, você pode separar as tarefas dentro de sua equipe de segurança e conceder apenas a quantidade de acesso que os usuários precisam para realizar seus trabalhos. Este artigo explica o gerenciamento de acesso, [!INCLUDE [Product short](includes/product-short.md)] a autorização de função e ajuda você a colocar em funcionamento os grupos de funções no [!INCLUDE [Product short](includes/product-short.md)] .

> [!NOTE]
> Qualquer administrador global ou administrador de segurança na Azure Active Directory do locatário é automaticamente um [!INCLUDE [Product short](includes/product-short.md)] administrador.

## <a name="accessing-the-product-short-portal"></a>Acessando o [!INCLUDE [Product short](includes/product-short.md)] Portal

O acesso ao [!INCLUDE [Product short](includes/product-short.md)] Portal (Portal.ATP.Azure.com) só pode ser realizado por um usuário do Azure AD que tenha a função de diretório do administrador global ou administrador de segurança. Depois de inserir o portal com a função necessária, você pode criar sua [!INCLUDE [Product short](includes/product-short.md)] instância. [!INCLUDE [Product short](includes/product-short.md)] o serviço cria três grupos de segurança em seu locatário de Azure Active Directory: administradores, usuários e visualizadores.

> [!NOTE]
> O acesso ao [!INCLUDE [Product short](includes/product-short.md)] portal é concedido somente aos usuários dentro dos [!INCLUDE [Product short](includes/product-short.md)] grupos de segurança, dentro de seu Azure Active Directory, bem como aos administradores globais e de segurança do locatário.

## <a name="types-of-product-short-security-groups"></a>Tipos de [!INCLUDE [Product short](includes/product-short.md)] grupos de segurança

[!INCLUDE [Product short](includes/product-short.md)] o fornece três tipos de grupos de segurança: administradores do Azure ATP *(nome da instância)* , usuários do Azure ATP *(nome da instância)* e visualizadores do Azure ATP *(nome da instância)* . A tabela a seguir descreve o tipo de acesso no [!INCLUDE [Product short](includes/product-short.md)] portal disponível para cada função. Dependendo da função que você atribuir, várias telas e opções de menu no [!INCLUDE [Product short](includes/product-short.md)] portal não estarão disponíveis para esses usuários, da seguinte maneira:

|Atividade |Administradores do Azure ATP *(nome da instância)*|Usuários do Azure ATP *(nome da instância)*|Visualizadores do Azure ATP *(nome da instância)*|
|----|----|----|----|
|Alterar o status dos alertas de integridade|Disponível|Não disponível|Não disponível|
|Alterar o status de Alertas de Segurança (abrir novamente, fechar, excluir, suprimir)|Disponível|Disponível|Não disponível|
|Excluir instância|Disponível|Não disponível|Não disponível|
|Baixar um relatório|Disponível|Disponível|Disponível|
|Fazer logon|Disponível|Disponível|Disponível|
|Compartilhar/Exportar alertas de segurança (por email, obter o link, baixar detalhes)|Disponível|Disponível|Disponível|
|Atualizar [!INCLUDE [Product short](includes/product-short.md)] configuração-atualizações|Disponível|Não disponível|Não disponível|
|Atualizar [!INCLUDE [Product short](includes/product-short.md)] configuração – marcas de entidade (sensitive e honeytoken)|Disponível|Disponível|Não disponível|
|Atualizar [!INCLUDE [Product short](includes/product-short.md)] configuração-exclusões|Disponível|Disponível|Não disponível|
|Atualizar [!INCLUDE [Product short](includes/product-short.md)] a configuração-idioma|Disponível|Disponível|Não disponível|
|Atualizar [!INCLUDE [Product short](includes/product-short.md)] configuração-notificações (email e syslog)|Disponível|Disponível|Não disponível|
|Atualizar [!INCLUDE [Product short](includes/product-short.md)] configuração – detecções de visualização|Disponível|Disponível|Não disponível|
|Atualizar [!INCLUDE [Product short](includes/product-short.md)] configuração-relatórios agendados|Disponível|Disponível|Não disponível|
|Atualizar [!INCLUDE [Product short](includes/product-short.md)] configuração-fontes de dados (serviços de diretório, Siem, VPN WD-ATP)|Disponível|Não disponível|Não disponível|
|Atualizar [!INCLUDE [Product short](includes/product-short.md)] configuração-sensores (baixar, regenerar chave, configurar, excluir)|Disponível|Não disponível|Não disponível|
|Exibir perfis de entidade e alertas de segurança|Disponível|Disponível|Disponível|

Quando os usuários tentam acessar uma página que não está disponível para seu grupo de funções, eles são redirecionados para a [!INCLUDE [Product short](includes/product-short.md)] página não autorizada.

## <a name="add-and-remove-users"></a>Adicionar e remover usuários

[!INCLUDE [Product short](includes/product-short.md)] usa grupos de segurança do Azure AD como base para grupos de funções. Os grupos de funções podem ser gerenciados na [página de gerenciamento de grupos](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups). Somente os usuários do Azure AD podem ser adicionados ou removidos de grupos de segurança.

## <a name="see-also"></a>Consulte Também

- [[!INCLUDE [Product short](includes/product-short.md)] ferramenta de dimensionamento](https://aka.ms/aatpsizingtool)
- [[!INCLUDE [Product short](includes/product-short.md)] arquitectura](architecture.md)
- [Pré-instalação [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [Confira o [!INCLUDE [Product short](includes/product-short.md)] Fórum!](https://aka.ms/MDIcommunity)