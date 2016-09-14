---
title: "Solução de problemas do ATA usando os logs do ATA | Microsoft ATA"
description: "Descreve como você pode usar os logs do ATA para solucionar problemas"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b8ad5511-8893-4d1d-81ee-b9a86e378347
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ee5f60e43f50562e7a7309eafa3b52cf946b0d3b
ms.openlocfilehash: 493f255ae09b51d27079a186bb802f0f3f9706bc


---

*Aplica-se a: Advanced Threat Analytics versão 1.7*



# Solução de problemas do ATA usando os logs do ATA
Os logs do ATA fornecem informações sobre o que cada componente do ATA está fazendo a qualquer hora.

## Logs do Gateway do ATA
Nesta seção, todas as referências ao Gateway do ATA são relevantes também para o Gateway Lightweight do ATA. 

Os logs do Gateway do ATA estão localizados em uma subpasta chamada **Logs**, no local onde o ATA está instalada; o local padrão é:. No local de instalação padrão, ela pode ser encontrada em: **C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Gateway\Logs**.

O Gateway do ATA tem os seguintes logs:

-   **Microsoft.Tri.Gateway.log** – Esse log contém tudo o que acontece no Gateway do ATA (inclusive resolução e erros). Usado principalmente para obter o status geral de todas as operações em ordem cronológica de ocorrência.

-   **Microsoft.Tri.Gateway Resolution.log** – Esse log contém os detalhes da resolução das entidades vistas no tráfego pelo Gateway do ATA. Usado principalmente para investigar problemas de resolução de entidades.

-   **Microsoft.Tri.Gateway-Errors.log** – Esse log contém apenas os erros que são detectados pelo Gateway do ATA. Usado principalmente para executar verificações de integridade e investigar problemas que precisam estar correlacionados a horários específicos.

-   **Microsoft.Tri.Gateway-ExceptionStatistics.log** – Esse log agrupa todos os erros e exceções semelhantes e mede sua contagem.
    Esse arquivo começa vazio sempre que o serviço do Gateway do ATA é iniciado, e é atualizado a cada minuto. Seu uso principal é entender se há erros ou problemas novos com o Gateway do ATA (como os erros são agrupados fica mais fácil ler e entender rapidamente se há novos problemas).
-   **Microsoft.Tri.Gateway.Updater.log** - Esse log é usado para o processo do atualizador de gateway, que é responsável por atualizar o gateway, se estiver configurado para fazer isso automaticamente. Para o Gateway Lightweight do ATA, o processo do atualizador de gateway também é responsável pelas limitações de recursos do Gateway Lightweight do ATA.
-   **Microsoft.Tri.Gateway.Updater-ExceptionStatistics.log** - Esse log agrupa todos os erros e exceções semelhantes e mede sua contagem. Esse arquivo começa vazio sempre que o serviço do Atualizador do ATA é iniciado, e é atualizado a cada minuto. Ele permite que você entenda se há erros ou problemas novos com o Atualizador do ATA. Os erros são agrupados para facilitar uma compreensão rápida se algum erro ou problema for detectado.

> [!NOTE]
> Os três primeiros arquivos de log têm um tamanho máximo de até 50 MB. Quando esse tamanho é atingido, um novo arquivo de log é aberto e o anterior é renomeado como "&lt;nome do arquivo original&gt;-Archived-00000". Esse número aumenta a cada renomeação. Por padrão, se já houver mais de 10 arquivos do mesmo tipo, os mais antigos serão excluídos.

## Logs do Centro do ATA
Os logs do Centro do ATA estão localizados em uma subpasta chamada **Logs**. No local de instalação padrão, ela pode ser encontrada em: **C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\Logs**.
> [!Note]
> Os logs do console do ATA, que estavam nos logs do IIS, agora estão localizados nos logs da Central do ATA.

O Centro do ATA tem os seguintes logs:

-   **Microsoft.Tri.Center.log** – Esse log contém tudo o que acontece no Centro do ATA, inclusive detecções e erros. Usado principalmente para obter o status geral de todas as operações em ordem cronológica de ocorrência.

-   **Microsoft.Tri.Center-Detection.log** – esse log contém apenas os detalhes de detecção do Centro do ATA. Usado principalmente para investigar problemas de detecção.

-   **Microsoft.Tri.Center-Errors.log** – Esse log contém apenas os erros que são detectados pelo Centro do ATA. Usado principalmente para executar verificações de integridade e investigar problemas que precisam estar correlacionados a horários específicos.

-   **Microsoft.Tri.Center-ExceptionStatistics.log** – Esse log agrupa todos os erros e exceções semelhantes e mede sua contagem.
    Esse arquivo começa vazio sempre que o serviço do Centro do ATA é iniciado, e é atualizado a cada minuto. Usado principalmente para entender se há erros ou problemas novos com a Central do ATA - como os erros são agrupados, fica mais fácil entender rapidamente se há um novo tipo de problema ou erro.

> [!NOTE]
> Os três primeiros arquivos de log têm um tamanho máximo de até 50 MB. Quando esse tamanho é atingido, um novo arquivo de log é aberto e o anterior é renomeado como "&lt;nome do arquivo original&gt;-Archived-00000". Esse número aumenta a cada renomeação. Por padrão, se já houver mais de 10 arquivos do mesmo tipo, os mais antigos serão excluídos.


## Logs de implantação do ATA
Os logs de implantação do ATA estão localizados no diretório temp do usuário que instalou o produto. No local de instalação padrão, ele pode ser encontrado em: **C:\Usuários\Administrator\AppData\Local\Temp** (ou um diretório acima de %temp%).

Logs de implantação do Centro do Ata

-   **Microsoft Advanced Threat Analytics Center_20150601104213.log** - Esse log lista as etapas no processo de implantação do Centro do ATA. Usado principalmente para acompanhar o processo de implantação do Centro do ATA.

-   **Microsoft Advanced Threat Analytics Center_20150601104213_0_MongoDBPackage.log** - Esse log lista as etapas no processo de implantação do MongoDB no Centro do ATA. Usado principalmente para acompanhar o processo de implantação do MongoDB.

-   **Microsoft Advanced Threat Analytics Center_20150601104213_1_MsiPackage.log** - Esse log lista as etapas no processo de implantação dos binários do Centro do ATA. Usado principalmente para acompanhar a implantação dos binários do Centro do ATA.

Logs de implantação do Gateway do ATA e do Gateway Lightweight do ATA:

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801.log** - Esse log lista as etapas no processo de implantação do Gateway do ATA. Usado principalmente para acompanhar o processo de implantação do Gateway do ATA.

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801_001_MsiPackage.log** - Esse log lista as etapas no processo de implantação dos binários do Gateway do ATA. Usado principalmente para acompanhar a implantação dos binários do Gateway do ATA.


## Consulte também
- [Pré-requisitos do ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planejamento da capacidade de ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurar coleta de eventos](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configuração do encaminhamento de eventos do Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->


