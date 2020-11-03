---
title: Microsoft defender para identidade no Microsoft Cloud App Security
description: Visão geral do Microsoft defender para recursos de identidade no Microsoft Cloud App Security.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 01/05/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5051900ef8eb21f85a4f31723f455d3ae18ff36e
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93275092"
---
# <a name="using-product-long-with-microsoft-cloud-app-security"></a>Usando [!INCLUDE [Product long](includes/product-long.md)] com Microsoft Cloud app Security

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Este artigo foi criado para ajudá-lo a entender e navegar na experiência de investigação avançada ao usar o portal de Microsoft Cloud App Security com o [!INCLUDE [Product long](includes/product-long.md)] .

Aproveitando as detecções locais existentes e a análise de comportamento anormal, o acesso ao [!INCLUDE [Product short](includes/product-short.md)] uso do portal de Microsoft Cloud app Security fornece a capacidade adicional de detectar e alertar sobre vazamento de dados confidenciais em toda a empresa, bem como as atividades de filtro e criar políticas acionáveis. Essa oferta híbrida analisa a atividade e os alertas com base na análise de comportamento da entidade e de usuário (UEBA) para determinar os comportamentos de risco e fornece uma pontuação de prioridade de investigação para simplificar a resposta a incidentes para identidades comprometidas.

Neste artigo, você aprenderá sobre:

> [!div class="checklist"]
>
> - Visão geral do serviço
> - Novas maneiras de acessar [!INCLUDE [Product short](includes/product-short.md)]
> - Pré-requisitos de licenciamento
> - Onde encontrar [!INCLUDE [Product short](includes/product-short.md)] atividades rastreadas no Cloud app Security

## <a name="service-overview"></a>Visão geral do serviço

Com a integração com [!INCLUDE [Product short](includes/product-short.md)] o, o portal de Cloud app Security fornece alertas e informações de:

- O Microsoft Cloud App Security, que identifica ataques em uma sessão de nuvem, abrangendo produtos da Microsoft e aplicativos de terceiros
- [!INCLUDE [Product long](includes/product-long.md)], que usa aprendizado de máquina e análise comportamental para identificar ataques em sua rede local
- O Azure Active Directory Identity Protection, que detecta e impede proativamente os riscos de usuário e de entrada para identidades na nuvem

## <a name="access-product-short"></a>Às [!INCLUDE [Product short](includes/product-short.md)]

Opte por continuar a usar [!INCLUDE [Product short](includes/product-short.md)] no [!INCLUDE [Product short](includes/product-short.md)] portal ou, você pode acessar [!INCLUDE [Product short](includes/product-short.md)] alertas e pontuação de identidade usando o portal de Microsoft Cloud app Security. Em qualquer fluxo de trabalho, [!INCLUDE [Product short](includes/product-short.md)] as tarefas de instalação e configuração continuam a ser manipuladas no [!INCLUDE [Product short](includes/product-short.md)] Portal.

## <a name="prerequisites"></a>Pré-requisitos

Para fazer uma investigação completa sobre os recursos no ambiente híbrido, é necessário:

- Uma licença válida do Microsoft Cloud App Security
- Uma licença válida para [!INCLUDE [Product long](includes/product-long.md)] conectado à sua instância do Active Directory

>[!NOTE]
>
> - Se você não tiver uma assinatura para Cloud App Security, ainda poderá usar o portal de Cloud App Security para investigar [!INCLUDE [Product short](includes/product-short.md)] alertas e aprofundar-se sobre os usuários e suas atividades gerenciadas no local, mas você não receberá informações relacionadas de seus aplicativos de nuvem.
> - [!INCLUDE [Product short](includes/product-short.md)] os administradores podem exigir novas permissões para acessar Cloud App Security. Para saber como atribuir permissões ao Cloud App Security, confira [Gerenciar o acesso de administrador](/cloud-app-security/manage-admins).

Consulte [ [!INCLUDE [Product short](includes/product-short.md)] integração](/cloud-app-security/aatp-integration) para saber como habilitar rapidamente o [!INCLUDE [Product short](includes/product-short.md)] em Cloud app Security.

## <a name="product-short-in-cloud-app-security"></a>[!INCLUDE [Product short](includes/product-short.md)] em Cloud App Security

Confira o [Início rápido do Cloud App Security](/cloud-app-security/getting-started-with-cloud-app-security) para se familiarizar com os fundamentos básicos de como usar o portal do Cloud App Security.

Acesse seus [!INCLUDE [Product short](includes/product-short.md)] dados e novos recursos híbridos dentro de Cloud app Security alertas, atividades e páginas de usuário.

## <a name="alerts"></a>Alertas

[!INCLUDE [Product short](includes/product-short.md)] os alertas são exibidos na fila **alertas** de Cloud app Security. As opções de filtragem de alerta adicionais estão disponíveis somente ao exibir alertas usando o Cloud App Security. [!INCLUDE [Product short](includes/product-short.md)] os alertas são filtrados usando o filtro de aplicativo para **Active Directory**.

## <a name="alert-management"></a>Gerenciamento de alertas

Ao usar o [!INCLUDE [Product short](includes/product-short.md)] com o Cloud app Security, o fechamento de alertas em um serviço não os fechará automaticamente no outro serviço. Decida onde gerenciar e corrigir os alertas para evitar a duplicação de esforços.

## <a name="siem-notification"></a>Notificação de SIEM

Se seus serviços ( [!INCLUDE [Product short](includes/product-short.md)] e Cloud app Security) estiverem atualmente configurados para enviar notificações de alerta para um Siem, depois de habilitar a [!INCLUDE [Product short](includes/product-short.md)] integração no Cloud app Security, você começará a receber notificações do Siem duplicadas para o mesmo alerta. Um alerta será emitido de cada serviço e eles terão diferentes IDs de alerta. Para evitar a duplicação e a confusão, decida onde você pretende executar o gerenciamento de alertas e, em seguida, interrompa o envio de notificações de SIEM de outro serviço.

## <a name="activities"></a>Atividades

[!INCLUDE [Product short](includes/product-short.md)] os alertas são exibidos no **log de atividades** do Cloud app Security. As opções de filtragem de atividades e os recursos adicionais estão disponíveis somente ao exibir alertas usando o Cloud App Security. Consulte [ [!INCLUDE [Product short](includes/product-short.md)] atividades usando Microsoft Cloud app Security](activities-filtering-mcas.md) para saber como filtrar e criar novas políticas de atividade.

## <a name="user-pages"></a>Páginas do usuário

As páginas de usuário contêm a [Pontuação de prioridade de investigação](/cloud-app-security/tutorial-ueba) de cada usuário e um log de atividades de todas as ações.

Para acessar uma página de usuário de um usuário do sistema:

1. Abra **Alertas** no menu principal.
1. Selecione e filtre a fila de alertas para um usuário específico usando o campo **Nome de Usuário**.

 ou

1. No menu **Investigar** , selecione **Log de atividades**.
1. Filtre a fila do log de atividades por usuário.

    ![Log de atividades](media/mcas-activity-filter.png)

## <a name="next-steps"></a>Próximas etapas

Consulte [ [!INCLUDE [Product short](includes/product-short.md)] atividades usando Microsoft Cloud app Security](activities-filtering-mcas.md) para saber como filtrar e criar novas políticas de atividade.

## <a name="join-the-community"></a>Participe da comunidade

Você tem mais perguntas ou um interesse em discutir [!INCLUDE [Product short](includes/product-short.md)] e segurança relacionada com outras pessoas? Junte-se à [ [!INCLUDE [Product short](includes/product-short.md)] comunidade](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) hoje mesmo!
