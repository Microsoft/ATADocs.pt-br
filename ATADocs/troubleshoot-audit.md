---
title: Trabalhando com logs de auditoria do ATA | Microsoft Docs
description: Este artigo descreve como trabalhar com os logs de auditoria do ATA no Log de Eventos do Windows.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 020ae7a28e2120c51c873b5e67adb14436c56ad1
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56076471"
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
