---
title: Grupos de funções avançadas do Threat Analytics para gerenciamento de acesso
description: Explica passo a passo como trabalhar com grupos de função do ATA.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: cdb1d66513f785b71b73b21aaf096ab5b5d3ad81
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90908750"
---
# <a name="ata-role-groups"></a>Grupos de função do ATA


[!INCLUDE [Banner for top of topics](includes/banner.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Os grupos de função permitem o gerenciamento de acesso para o ATA. Com os grupos de função, você pode separar as tarefas dentro de sua equipe de segurança e conceder apenas a quantidade de acesso que os usuários precisam para realizar seus trabalhos. Este artigo explica o gerenciamento de acesso e a autorização de função do ATA, e ajuda você a colocar em funcionamento os grupos de função no ATA.

> [!NOTE]
> Qualquer administrador local no ATA Center é automaticamente um Administrador do Microsoft Advanced Threat Analytics.

## <a name="types-of-ata-role-groups"></a>Tipos de Grupos de função do ATA 

O ATA apresenta três tipos de Grupos de função: Administradores do ATA, Usuários do ATA e Visualizadores do ATA. A tabela a seguir descreve o tipo de acesso no ATA disponível por função. Dependendo de qual função você atribuir, várias telas e opções de menu no ATA não estarão disponíveis. Veja a seguir:

|Atividade |Administradores do Microsoft Advanced Threat Analytics|Usuários do Microsoft Advanced Threat Analytics|Visualizadores do Microsoft Advanced Threat Analytics|
|----|----|----|----|
|Logon|Disponível|Disponível|Disponível|
|Fornecer informações sobre atividades suspeitas|Disponível|Disponível|Não disponível|
|Alterar o status de atividades suspeitas|Disponível|Disponível|Não disponível|
|Compartilhar/Exportar atividade suspeita por email/link|Disponível|Disponível|Não disponível|
|Alterar o status dos alertas de integridade|Disponível|Disponível|Não disponível|
|Atualizar a configuração do ATA|Disponível|Não disponível|Não disponível|
|Gateway – Adicionar|Disponível|Não disponível|Não disponível|
|Gateway – Excluir |Disponível|Não disponível|Não disponível|
|CD Monitorado – Adicionar |Disponível|Não disponível|Não disponível|
|CD Monitorado – Excluir|Disponível|Não disponível|Não disponível|
|Exibir alertas e atividades suspeitas|Disponível|Disponível|Disponível|


Quando os usuários tentam acessar uma página que não está disponível para seus grupos de função, são redirecionados à página não autorizada do ATA. 

## <a name="add--remove-users---ata-role-groups"></a>Adicionar\Remover usuários - Grupos de função do ATA 

O ATA usa grupos locais do Windows como base para os grupos de função. Os grupos de função devem ser gerenciados no servidor do ATA Center.
Para adicionar ou remover usuários, use os **Usuários e Grupos Locais** MMC (Lusrmgr.msc). Em um computador associado ao domínio, você pode adicionar contas de domínio, bem como contas locais. 

