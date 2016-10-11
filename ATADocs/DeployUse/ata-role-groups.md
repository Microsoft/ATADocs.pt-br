---
title: "Como trabalhar com grupos de funções - Completo | Microsoft ATA"
description: "Explica passo a passo como trabalhar com grupos de função do ATA."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 09/20/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d47d9e7be294c68d764710c15c4bb78539e42f62
ms.openlocfilehash: 869d8f830d5dc70c927f172d77642b0c97bdcd84


---

*Aplica-se a: Advanced Threat Analytics versão 1.7*




# Grupos de função do ATA

Os grupos de função permitem o gerenciamento de acesso para o ATA. Com os grupos de função, você pode separar as tarefas dentro de sua equipe de segurança e conceder apenas a quantidade de acesso que os usuários precisam para realizar seus trabalhos. Este artigo explica o gerenciamento de acesso e a autorização de função do ATA, e ajuda você a colocar em funcionamento os grupos de função no ATA.
## Tipos de Grupos de função do ATA 

O ATA apresenta três tipos de Grupos de função: Administradores do ATA, Analista do ATA e Executivo do ATA. A tabela a seguir descreve o tipo de acesso no ATA disponível por função. Dependendo de qual função você atribuir, várias telas e opções de menu no ATA não estarão disponíveis. Veja a seguir:

|Atividade |Administrador do Microsoft Advanced Threat Analytics|Analista do Microsoft Advanced Threat Analytics|Executivo do Microsoft Advanced Threat Analytics|
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

## Adicionar\Remover usuários - Grupos de função do ATA 

O ATA usa grupos locais do Windows como base para os grupos de função. Para adicionar ou remover usuários, use os **Usuários e Grupos Locais** MMC (Lusrmgr.msc). Em um computador associado ao domínio, você pode adicionar contas de domínio, bem como contas locais. 




<!--HONumber=Sep16_HO4-->


