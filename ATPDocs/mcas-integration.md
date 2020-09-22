---
title: Proteção Avançada contra Ameaças do Azure no Microsoft Cloud App Security
description: Visão geral dos recursos do ATP do Azure no Microsoft Cloud App Security.
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
ms.openlocfilehash: c1c3b18606b38902217a320663ef91191e34f185
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90910167"
---
# <a name="using-azure-atp-with-microsoft-cloud-app-security"></a>Usando o ATP do Azure com o Microsoft Cloud App Security

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Este artigo foi criado para ajudá-lo a compreender e navegar a experiência de investigação aprimorada ao usar o portal do Microsoft Cloud App Security com o ATP do Azure.

Aproveitando as detecções de locais existentes e a análise de comportamento anormal, acessar o Azure ATP usando o portal do Microsoft Cloud App Security fornece a capacidade adicional para detectar e alertar sobre o vazamento de dados confidenciais em sua empresa, bem como as atividades de filtro e criar políticas acionáveis. Essa oferta híbrida analisa a atividade e os alertas com base na análise de comportamento da entidade e de usuário (UEBA) para determinar os comportamentos de risco e fornece uma pontuação de prioridade de investigação para simplificar a resposta a incidentes para identidades comprometidas.

Neste artigo, você aprenderá sobre:

> [!div class="checklist"]
>
> - Visão geral do serviço
> - Novas maneiras de acessar o ATP do Azure
> - Pré-requisitos de licenciamento
> - Onde encontrar as atividades rastreadas do ATP do Azure no Cloud App Security

## <a name="service-overview"></a>Visão geral do serviço

A integração com o ATP do Azure e o portal do Cloud App Security fornece alertas e informações sobre:

- O Microsoft Cloud App Security, que identifica ataques em uma sessão de nuvem, abrangendo produtos da Microsoft e aplicativos de terceiros
- A Proteção Avançada contra Ameaças do Azure, que usa análise comportamental e aprendizado de máquina para identificar ataques na rede local
- O Azure Active Directory Identity Protection, que detecta e impede proativamente os riscos de usuário e de entrada para identidades na nuvem

## <a name="access-azure-atp"></a>Acessar o ATP do Azure

Escolha continuar a usar o ATP do Azure dentro do portal do ATP do Azure ou você pode acessar alertas e a pontuação de identidade do ATP do Azure usando o portal do Microsoft Cloud App Security. Os fluxo de trabalho e as tarefas de configuração do ATP do Azure continuam a ser tratados dentro do portal do ATP do Azure.

## <a name="prerequisites"></a>Pré-requisitos

Para fazer uma investigação completa sobre os recursos no ambiente híbrido, é necessário:

- Uma licença válida do Microsoft Cloud App Security
- Uma licença válida do ATP do Azure vinculada à instância do Azure Active Directory

>[!NOTE]
>
> - Se você não tiver uma assinatura do Cloud App Security, ainda poderá usar o portal do Cloud App Security para investigar os alertas do ATP do Azure e faça uma análise aprofundada sobre os usuários e suas atividades gerenciadas locais, mas não receberá informações relacionadas de seus aplicativos na nuvem.
> - Os administradores do ATP do Azure podem exigir novas permissões para acessar o Cloud App Security. Para saber como atribuir permissões ao Cloud App Security, confira [Gerenciar o acesso de administrador](/cloud-app-security/manage-admins).

Confira [Integração do ATP do Azure](/cloud-app-security/aatp-integration) para aprender a habilitar rapidamente o ATP do Azure no Cloud App Security.

## <a name="azure-atp-in-cloud-app-security"></a>ATP do Azure no Cloud App Security

Confira o [Início rápido do Cloud App Security](/cloud-app-security/getting-started-with-cloud-app-security) para se familiarizar com os fundamentos básicos de como usar o portal do Cloud App Security.

Acesse seus dados do ATP do Azure e novos recursos híbridos em páginas de usuário, atividades e alertas do Cloud App Security.

## <a name="alerts"></a>Alertas

Os alertas do ATP do Azure são exibidos dentro da fila de **Alertas** do Cloud App Security. As opções de filtragem de alerta adicionais estão disponíveis somente ao exibir alertas usando o Cloud App Security. Os alertas do ATP do Azure são filtrados usando o filtro de aplicativo para o **Active Directory**.

## <a name="alert-management"></a>Gerenciamento de alertas

Ao usar o ATP do Azure com o Cloud App Security, fechar alertas em um serviço não os fechará automaticamente em outro serviço. Decida onde gerenciar e corrigir os alertas para evitar a duplicação de esforços.

## <a name="siem-notification"></a>Notificação de SIEM

Se seus dois serviços (ATP do Azure e Cloud App Security) estiverem atualmente configurados para enviar notificações de alerta para um SIEM, após habilitar a integração do ATP do Azure no Cloud App Security, você começará a receber notificações de SIEM duplicadas para o mesmo alerta. Um alerta será emitido de cada serviço e eles terão diferentes IDs de alerta. Para evitar a duplicação e a confusão, decida onde você pretende executar o gerenciamento de alertas e, em seguida, interrompa o envio de notificações de SIEM de outro serviço.

## <a name="activities"></a>Atividades

Os alertas do ATP do Azure são exibidos dentro do **Log de atividades** do Cloud App Security. As opções de filtragem de atividades e os recursos adicionais estão disponíveis somente ao exibir alertas usando o Cloud App Security. Ver [Atividades do ATP do Azure usando o Microsoft Cloud App Security](activities-filtering-mcas.md) para saber como filtrar e criar novas políticas de atividade.

## <a name="user-pages"></a>Páginas do usuário

As páginas de usuário contêm a [Pontuação de prioridade de investigação](/cloud-app-security/tutorial-ueba) de cada usuário e um log de atividades de todas as ações.

Para acessar uma página de usuário de um usuário do sistema:
1. Abra **Alertas** no menu principal.
1. Selecione e filtre a fila de alertas para um usuário específico usando o campo **Nome de Usuário**.

 ou

1. No menu **Investigar**, selecione **Log de atividades**.
1. Filtre a fila do log de atividades por usuário.

    ![Log de atividades](media/atp-mcas-activity-filter.png)

## <a name="next-steps"></a>Próximas etapas

Ver [Atividades do ATP do Azure usando o Microsoft Cloud App Security](activities-filtering-mcas.md) para saber como filtrar e criar novas políticas de atividade.

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o ATP do Azure e a segurança relacionada com outras pessoas? Participe da [Comunidade do ATP do Azure](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) hoje mesmo!