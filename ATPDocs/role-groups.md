---
title: Microsoft defender para grupos de funções de identidade para gerenciamento de acesso
description: Percorre como trabalhar com o Microsoft defender para grupos de funções de identidade.
ms.date: 02/27/2020
ms.topic: conceptual
ms.openlocfilehash: 9ff271c8f417d3f2c15e3e6809b62986a7825db4
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533351"
---
# <a name="microsoft-defender-for-identity-role-groups"></a>Microsoft defender para grupos de funções de identidade

[!INCLUDE [Product long](includes/product-long.md)] oferece segurança baseada em função para proteger dados de acordo com as necessidades específicas de segurança e conformidade de uma organização. [!INCLUDE [Product short](includes/product-short.md)] suporte a três funções separadas: administradores, usuários e visualizadores.

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

Grupos de funções permitem o gerenciamento de acesso para o [!INCLUDE [Product short](includes/product-short.md)] . Com os grupos de função, você pode separar as tarefas dentro de sua equipe de segurança e conceder apenas a quantidade de acesso que os usuários precisam para realizar seus trabalhos. Este artigo explica o gerenciamento de acesso, [!INCLUDE [Product short](includes/product-short.md)] a autorização de função e ajuda você a colocar em funcionamento os grupos de funções no [!INCLUDE [Product short](includes/product-short.md)] .

> [!NOTE]
> Qualquer administrador global ou administrador de segurança na Azure Active Directory do locatário é automaticamente um [!INCLUDE [Product short](includes/product-short.md)] administrador.

## <a name="accessing-the-defender-for-identity-portal"></a>Acessando o defender para o portal de identidade

O acesso ao [!INCLUDE [Product short](includes/product-short.md)] Portal (Portal.ATP.Azure.com) só pode ser realizado por um usuário do Azure AD que tenha a função de diretório do administrador global ou administrador de segurança. Depois de inserir o portal com a função necessária, você pode criar sua [!INCLUDE [Product short](includes/product-short.md)] instância. [!INCLUDE [Product short](includes/product-short.md)] o serviço cria três grupos de segurança em seu locatário de Azure Active Directory: administradores, usuários e visualizadores.

> [!NOTE]
> O acesso ao [!INCLUDE [Product short](includes/product-short.md)] portal é concedido somente aos usuários dentro dos [!INCLUDE [Product short](includes/product-short.md)] grupos de segurança, dentro de seu Azure Active Directory, bem como aos administradores globais e de segurança do locatário.

## <a name="types-of-defender-for-identity-security-groups"></a>Tipos de defender para grupos de segurança de identidade

[!INCLUDE [Product short](includes/product-short.md)] o fornece três tipos de grupos de segurança: administradores do Azure ATP *(nome da instância)* , usuários do Azure ATP *(nome da instância)* e visualizadores do Azure ATP *(nome da instância)* . A tabela a seguir descreve o tipo de acesso no [!INCLUDE [Product short](includes/product-short.md)] portal disponível para cada função. Dependendo da função que você atribuir, várias telas e opções de menu no [!INCLUDE [Product short](includes/product-short.md)] portal não estarão disponíveis para esses usuários, da seguinte maneira:

|Atividade |Administradores do Azure ATP *(nome da instância)*|Usuários do Azure ATP *(nome da instância)*|Visualizadores do Azure ATP *(nome da instância)*|
|----|----|----|----|
|Alterar o status dos alertas de integridade|Disponível|Não disponível|Não disponível|
|Alterar o status de Alertas de Segurança (abrir novamente, fechar, excluir, suprimir)|Disponível|Disponível|Não disponível|
|Excluir instância|Disponível|Não disponível|Não disponível|
|Baixar um relatório|Disponível|Disponível|Disponível|
|Logon|Disponível|Disponível|Disponível|
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

- [Ferramenta de dimensionamento do [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/aatpsizingtool)
- [Arquitetura do [!INCLUDE [Product short](includes/product-short.md)]](architecture.md)
- [Instalar o [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
