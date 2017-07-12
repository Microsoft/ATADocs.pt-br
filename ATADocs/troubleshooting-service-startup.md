---
title: "Solução de problemas do Advanced Threat Analytics usando os logs | Microsoft Docs"
description: "Descreve como você pode usar os logs do ATA para solucionar problemas"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/26/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1291281273188a21b61b29f06a5220eee589767c
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*



<a id="troubleshooting-ata-center-service-startup" class="xliff"></a>

# Solução de problemas de inicialização de serviço do Centro de ATA

Se seu Centro de ATA não for iniciado, execute o seguinte procedimento de solução de problemas:

1.  Execute o seguinte comando do Windows PowerShell: Get-Service Pla | Selecione Status para garantir que o serviço de contador de desempenho está em execução. Se não estiver, é um problema de plataforma e você precisa se certificar de que o serviço está em execução novamente.
2.  Se ele estava em execução, tente reiniciá-lo e veja se isso resolve o problema: Restart-Service Pla
3.  Tente criar um novo coletor de dados manualmente (qualquer um será suficiente, até mesmo coletar a CPU do computador, por exemplo).
Se ele puder ser iniciado, provavelmente a plataforma está OK, se não, esse ainda é um problema de plataforma.

4.  Tente recriar manualmente o coletor de dados do ATA, usando um prompt com privilégios elevados, executando esses comandos: sc stop ATACenter logman stop "Microsoft ATA Center" logman export "Microsoft ATA Center" -xml c:\center.xml logman delete "Microsoft ATA Center" logman import "Microsoft ATA Center" -xml c:\center.xml logman start "Microsoft ATA Center" sc start ATACenter



<a id="see-also" class="xliff"></a>

## Consulte Também
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Planejamento da capacidade do ATA](ata-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
