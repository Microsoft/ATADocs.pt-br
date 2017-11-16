---
title: Trabalhando com logs de auditoria do ATA | Microsoft Docs
description: Este artigo descreve como trabalhar com os logs de auditoria do ATA no Log de Eventos do Windows.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 287bb370f216c2f921eb954dfd4a34ceb8f095c7
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*

# <a name="working-with-ata-audit-logs"></a>Trabalhando com logs de auditoria do ATA

Os logs de auditoria do ATA são mantidos nos Logs de Eventos do Windows em **Aplicativos e Serviços** e **Microsoft ATA** tanto nos computadores do Gateway do ATA quanto no Centro do ATA.

O log de auditoria do Centro do ATA contém:
-   Informações de atividade suspeita
-   Alertas de monitoramento (página de integridade)
-   Logons do Console do ATA
-   Todas as alterações de configuração*

O log de auditoria do Gateway do ATA contém:
-   Alterações de configuração do Gateway* 

(Todas as alterações de configuração do Gateway do ATA são configuradas no Centro do ATA, mas ainda são auditadas no próprio computador do Gateway.)

*O log de auditoria de alterações de configuração contém a configuração anterior e a nova configuração.


## <a name="see-also"></a>Consulte também
- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
