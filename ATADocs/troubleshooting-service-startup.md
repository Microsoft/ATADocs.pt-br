---
title: "Solução de problemas do Advanced Threat Analytics usando os logs | Microsoft Docs"
description: "Descreve como você pode usar os logs do ATA para solucionar problemas"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 125376b1e3530481a3b9f62c4661dd10dce13f22
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*



# <a name="troubleshooting-ata-center-service-startup"></a>Solução de problemas de inicialização de serviço do Centro de ATA

Se seu Centro de ATA não for iniciado, execute o seguinte procedimento de solução de problemas:

1.  Execute o seguinte comando do Windows PowerShell: `Get-Service Pla | Select Status` para garantir que o serviço de contador de desempenho está em execução. Se não estiver, é um problema de plataforma e você precisa se certificar de que o serviço está em execução novamente.
2.  Se ele estava em execução, tente reiniciá-lo e veja se isso resolve o problema: `Restart-Service Pla`
3.  Tente criar um novo coletor de dados manualmente (qualquer um será suficiente, até mesmo coletar a CPU do computador, por exemplo).
Se puder iniciar, provavelmente a plataforma estará bem. Caso contrário, a plataforma ainda será o problema.

4.  Tente recriar manualmente o coletor de dados de ATA usando um prompt de comandos com privilégios elevados, executando estes comandos:

        sc stop ATACenter
        logman stop "Microsoft ATA Center"
        logman export "Microsoft ATA Center" -xml c:\center.xml
        logman delete "Microsoft ATA Center"
        logman import "Microsoft ATA Center" -xml c:\center.xml
        logman start "Microsoft ATA Center"
        sc start ATACenter



## <a name="see-also"></a>Consulte também
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Planejamento da capacidade do ATA](ata-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
