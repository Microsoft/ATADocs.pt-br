---
title: Trabalhando com logs de auditoria do ATA | Microsoft Docs
description: Este artigo descreve como trabalhar com os logs de auditoria do ATA no Log de Eventos do Windows.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 630045525ce344920032ef0245692ed9ca5e5ef1
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54839515"
---
# <a name="working-with-ata-audit-logs"></a>Trabalhando com logs de auditoria do ATA


*Aplica-se a: Advanced Threat Analytics versão 1.9*

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


## <a name="see-also"></a>Consulte Também
- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
