---
title: Microsoft defender para filtragem e políticas de atividade de identidade no Microsoft Cloud App Security
description: Visão geral do Microsoft defender para filtragem e políticas de atividade de identidade com Microsoft Cloud App Security.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 589b7bc0ae95d6ff9dcc82fba930bc579d5b19b7
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533963"
---
# <a name="use-activity-filters-and-create-action-policies-with-microsoft-defender-for-identity-in-microsoft-cloud-app-security"></a>Usar filtros de atividade e criar políticas de ação com o Microsoft defender para identidade no Microsoft Cloud App Security

Este artigo foi criado para ajudá-lo a entender como filtrar e criar políticas de ação para [!INCLUDE [Product short](includes/product-short.md)] atividades usando Microsoft Cloud app Security.

Para obter mais informações sobre como concluir sua integração, consulte [ [!INCLUDE [Product short](includes/product-short.md)] integração com o Cloud app Security](/cloud-app-security/aatp-integration).

[!INCLUDE [Product short](includes/product-short.md)]O uso do com o Microsoft Cloud app Security oferece análise de atividade e alertas com base na análise de comportamento de usuário e entidade (Ueba), identificando os comportamentos de difuso em sua empresa, fornecendo uma pontuação de prioridade de investigação abrangente, bem como a filtragem de atividades e políticas de atividade personalizáveis.

## <a name="prerequisites"></a>Pré-requisitos

Para fazer uma investigação completa sobre os recursos no ambiente híbrido, é necessário:

- Uma licença válida do Microsoft Cloud App Security
- Uma licença válida para [!INCLUDE [Product long](includes/product-long.md)] conectado à sua instância do Active Directory

>[!NOTE]
>Se você não tiver uma assinatura para Cloud App Security, poderá usar o portal de Cloud App Security para investigar [!INCLUDE [Product short](includes/product-short.md)] alertas e aprofundar-se sobre os usuários e suas atividades gerenciadas no local, no entanto, as informações relacionadas aos seus aplicativos de nuvem permanecerão indisponíveis.

## <a name="filter-defender-for-identity-activities-in-cloud-app-security"></a>Filtrar o defender para atividades de identidade no Cloud App Security

[!INCLUDE [Product short](includes/product-short.md)] as atividades podem ser acessadas no menu principal Cloud App Security **investigar** selecionando o submenu **log de atividades** ou no menu **alertas** por status, categoria, severidade, aplicativo, nome de usuário ou política.

Para acessar [!INCLUDE [Product short](includes/product-short.md)] atividades por usuário:

1. Filtre a fila **Alertas** usando o campo NOME DE USUÁRIO.
    ![Filtrar alertas por nome de usuário](media/mcas-alerts-queue.png)
1. Clique no nome de usuário em qualquer um dos alertas na lista resultante para abrir a **Página de usuário** do usuário que você deseja investigar.

1. Filtre as atividades do usuário usando os campos disponíveis ou adicione uma nova regra de filtro usando o botão +.
    ![Filtrar atividades do usuário](media/mcas-activity-filter.png)

## <a name="create-activity-policies-in-cloud-app-security"></a>Criar políticas de atividade no Cloud App Security

Após filtrar as atividades e identificar as políticas de atividade que você gostaria de implementar ou a não conformidade em sua organização, use a opção **Criar política de atividade** do menu de filtro para criar imediatamente uma nova política personalizada por usuário, dispositivo ou locatário.

Para criar uma nova política de atividade:

1. Em qualquer página do **Log de atividades**, aplique um filtro (como Aplicativo, Nome de Usuário, Tipo de atividade) etc.
    - Para filtrar as atividades de [!INCLUDE [Product short](includes/product-short.md)] Selecione a opção **Active Directory** no filtro de aplicativo.
    ![Criar nova política de atividade](media/mcas-create-new-policy.png)
1. Clique no botão **Nova política da pesquisa**.
1. Adicione um **Nome da política**.
    ![Criar nova política de atividade -etapa 2](media/mcas-create-policy.png)
1. Adicione uma **Descrição** da política.
1. Atribua a **severidade** da política.
1. Selecione uma **categoria** para a política.
1. Escolha ou modifique os filtros para criar e atribuir da política.
1. Refine ou adicione mais filtros.
1. Salve e aplique a nova política.

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre os recursos adicionais e de pontuação de prioridade de investigação da funcionalidade do [Microsoft Cloud App Security](/cloud-app-security/).

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou quer discutir sobre o [!INCLUDE [Product short](includes/product-short.md)] e a segurança relacionada com outras pessoas? Participe da Comunidade [[!INCLUDE [Product short](includes/product-short.md)]](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) hoje mesmo!