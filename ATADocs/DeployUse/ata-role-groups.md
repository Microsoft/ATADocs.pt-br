---
title: "Como trabalhar com grupos de funções — completo | Microsoft Docs"
description: "Explica passo a passo como trabalhar com grupos de função do ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/23/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 3ba53b7b1c34359f00da9fc9717496cfc7d4271d
ms.openlocfilehash: b49906802bf0cae86178cbdcc34e4178691d39e4


---

*Aplica-se a: Advanced Threat Analytics versão 1.7*




# <a name="ata-role-groups"></a>Grupos de função do ATA

Os grupos de função permitem o gerenciamento de acesso para o ATA. Com os grupos de função, você pode separar as tarefas dentro de sua equipe de segurança e conceder apenas a quantidade de acesso que os usuários precisam para realizar seus trabalhos. Este artigo explica o gerenciamento de acesso e a autorização de função do ATA, e ajuda você a colocar em funcionamento os grupos de função no ATA.
## <a name="types-of-ata-role-groups"></a>Tipos de Grupos de função do ATA 

O ATA apresenta três tipos de Grupos de função: Administradores do ATA, Usuários do ATA e Visualizadores do ATA. A tabela a seguir descreve o tipo de acesso no ATA disponível por função. Dependendo de qual função você atribuir, várias telas e opções de menu no ATA não estarão disponíveis. Veja a seguir:

|Atividade |Administradores do Microsoft Advanced Threat Analytics|Usuários do Microsoft Advanced Threat Analytics|Visualizadores do Microsoft Advanced Threat Analytics|
|----|----|----|----|
|Fazer logon|Disponível|Disponível|Disponível|
|Fornecer informações sobre atividades suspeitas|Disponível|Disponível|Não disponível|
|Alterar o status de atividades suspeitas|Disponível|Disponível|Não disponível|
|Compartilhar/Exportar atividade suspeita por email/link|Disponível|Disponível|Não disponível|
|Adicionar/Editar notas de atividades suspeitas|Disponível|Disponível|Não disponível|
|Alterar o status dos Alertas de monitoramento|Disponível|Disponível|Não disponível|
|Atualizar a configuração do ATA|Disponível|Não disponível|Não disponível|
|Gateway – Adicionar|Disponível|Não disponível|Não disponível|
|Gateway – Excluir |Disponível|Não disponível|Não disponível|
|CD Monitorado – Adicionar |Disponível|Não disponível|Não disponível|
|CD Monitorado – Excluir|Disponível|Não disponível|Não disponível|

Quando os usuários tentam acessar uma página que não está disponível para seus grupos de função, ele é redirecionado à página não autorizada do ATA. 

## <a name="add-remove-users---ata-role-groups"></a>Adicionar\Remover usuários - Grupos de função do ATA 

O ATA usa grupos locais do Windows como base para os grupos de função. Para adicionar ou remover usuários, use os **Usuários e Grupos Locais** MMC (Lusrmgr.msc). Em um computador associado ao domínio, você pode adicionar contas de domínio, bem como contas locais. 




<!--HONumber=Nov16_HO4-->


