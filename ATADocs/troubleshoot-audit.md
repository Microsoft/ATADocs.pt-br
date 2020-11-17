---
title: Trabalhando com logs de auditoria do ATA
description: Este artigo descreve como trabalhar com os logs de auditoria do ATA no Log de Eventos do Windows.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 60819b4e941de53820f7ef858a73716a9f56bfa2
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690067"
---
# <a name="working-with-ata-audit-logs"></a>Trabalhando com logs de auditoria do ATA


[!INCLUDE [Banner for top of topics](includes/banner.md)]

Os logs de auditoria do ATA são mantidos nos Logs de Eventos do Windows em **Aplicativos e Serviços** e **Microsoft ATA** tanto nos computadores do Gateway do ATA quanto no Centro do ATA.

O log de auditoria do Centro do ATA contém:
- Informações de atividade suspeita
- Alertas de integridade (página de integridade)
- Logons do Console do ATA
- Todas as alterações de configuração*

O log de auditoria do Gateway do ATA contém:
- Alterações de configuração do Gateway* 

(Todas as alterações de configuração do Gateway do ATA são configuradas no Centro do ATA, mas ainda são auditadas no próprio computador do Gateway.)

*O log de auditoria de alterações de configuração contém a configuração anterior e a nova configuração.


## <a name="see-also"></a>Consulte Também
- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
