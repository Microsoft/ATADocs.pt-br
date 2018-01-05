---
title: "Solução de problemas de inicialização de serviço do Advanced Threat Analytics | Microsoft Docs"
description: "Descreve como é possível solucionar problemas de inicialização do ATA"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 12/20/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 33ff11f592984b754521c562414ffeabd2d1f255
ms.sourcegitcommit: 91158e5e63ce2021a1f5f85d47de03d963b7cb70
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*



# <a name="troubleshooting-service-startup"></a>Solução de problemas de inicialização do serviço

## <a name="troubleshooting-ata-center-service-startup"></a>Solução de problemas de inicialização de serviço do Centro de ATA

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

## <a name="troubleshooting-ata-lightweight-gateway-startup"></a>Solução de problemas de inicialização do Gateway Lightweight do ATA

**Sintoma**

Seu Gateway do ATA não inicia e você receberá esse erro:<br></br>
*System.Net.Http.HttpRequestException: o código de status de resposta não indica êxito: 500 (erro interno do servidor)*

**Descrição**

Isso acontece porque, como parte do processo de instalação do Gateway Lightweight, o ATA aloca um limite de CPU que permite que o Gateway Lightweight use a CPU com um buffer de 15%. Se você tiver definido independentemente um limite usando a chave do Registro: esse conflito impedirá que o Gateway Lightweight seja iniciado. 

**Resolução**

1. Nas chaves de registro, se houver um valor DWORD chamado **Desabilitar os Contadores de Desempenho** certifique-se de que ele seja definido como **0**: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfOS\Performance\` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfProc\Performance`
 
2. Em seguida, reinicie o serviço de PLA. O Gateway Lightweight do ATA automaticamente detectará a mudança e reiniciará o serviço.


## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Planejamento da capacidade do ATA](ata-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
