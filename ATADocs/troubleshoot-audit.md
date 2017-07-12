---
title: Trabalhando com logs de auditoria do ATA | Microsoft Docs
description: Este artigo descreve como trabalhar com os logs de auditoria do ATA no Log de Eventos do Windows.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 54f17bc4775868e380586822456330dfc2d45c29
ms.sourcegitcommit: 53b56220fa761671442da273364bdb3d21269c9e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*

<a id="working-with-ata-audit-logs" class="xliff"></a>

# Trabalhando com logs de auditoria do ATA

Os logs de auditoria do ATA são mantidos nos Logs de Eventos do Windows em **Aplicativos e Serviços** e **Microsoft ATA** tanto nos computadores do Gateway do ATA quanto no Centro do ATA.

O log de auditoria do Centro do ATA contém:
-   Informações de atividade suspeita
-   Alertas de monitoramento (página de integridade)
-   Logons do Console do ATA
-   Todas as alterações de configuração*

O log de auditoria do Gateway do ATA contém:
-   Alterações de configuração do Gateway* 

(Todas as alterações de configuração do Gateway do ATA são configuradas no Centro do ATA, mas ainda são auditadas no próprio computador do Gateway.)

*O log de auditoria de alterações de configuração conterá a configuração anterior e a nova configuração.


<a id="see-also" class="xliff"></a>

## Consulte Também
- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
