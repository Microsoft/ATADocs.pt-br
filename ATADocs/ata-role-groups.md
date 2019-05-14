---
title: Grupos de função do Advanced Threat Analytics para gerenciamento de acesso | Microsoft Docs
description: Explica passo a passo como trabalhar com grupos de função do ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3f4a3bed481fcd9ca789057f0b45fc25a30d01ad
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196231"
---
# <a name="ata-role-groups"></a>Grupos de função do ATA


*Aplica-se a: Advanced Threat Analytics versão 1.9*

Os grupos de função permitem o gerenciamento de acesso para o ATA. Com os grupos de função, você pode separar as tarefas dentro de sua equipe de segurança e conceder apenas a quantidade de acesso que os usuários precisam para realizar seus trabalhos. Este artigo explica o gerenciamento de acesso e a autorização de função do ATA, e ajuda você a colocar em funcionamento os grupos de função no ATA.

> [!NOTE]
> Qualquer administrador local no ATA Center é automaticamente um Administrador do Microsoft Advanced Threat Analytics.

## <a name="types-of-ata-role-groups"></a>Tipos de Grupos de função do ATA 

O ATA apresenta três tipos de grupos de Função: administradores do ATA, usuários do ATA e visualizadores do ATA. A tabela a seguir descreve o tipo de acesso no ATA disponível por função. Dependendo de qual função você atribuir, várias telas e opções de menu no ATA não estarão disponíveis. Veja a seguir:

|Atividade |Administradores do Microsoft Advanced Threat Analytics|Usuários do Microsoft Advanced Threat Analytics|Visualizadores do Microsoft Advanced Threat Analytics|
|----|----|----|----|
|Fazer logon|Disponível|Disponível|Disponível|
|Fornecer informações sobre atividades suspeitas|Disponível|Disponível|Não disponível|
|Alterar o status de atividades suspeitas|Disponível|Disponível|Não disponível|
|Compartilhar/Exportar atividade suspeita por email/link|Disponível|Disponível|Não disponível|
|Alterar o status dos Alertas de monitoramento|Disponível|Disponível|Não disponível|
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

