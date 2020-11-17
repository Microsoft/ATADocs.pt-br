---
title: Solucionando problemas de inicialização do serviço do Advanced Threat Analytics
description: Descreve como é possível solucionar problemas de inicialização do ATA
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3f23eb1aa2adc49b3913ab1e4218653a5b8c874d
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94689914"
---
# <a name="troubleshooting-service-startup"></a>Solução de problemas de inicialização do serviço

[!INCLUDE [Banner for top of topics](includes/banner.md)]

## <a name="troubleshooting-ata-center-service-startup"></a>Solução de problemas de inicialização de serviço do Centro de ATA

Se seu Centro de ATA não for iniciado, execute o seguinte procedimento de solução de problemas:

1. Execute o seguinte comando do Windows PowerShell: `Get-Service Pla | Select Status`
   para verificar se o serviço do contador de desempenho está em execução. Se não estiver, é um problema de plataforma e você precisa se certificar de que o serviço está em execução novamente.
1. Se ele estava em execução, tente reiniciá-lo e veja se ele resolve o problema:  `Restart-Service Pla`
1. Tente criar um novo coletor de dados manualmente (qualquer um será suficiente, até mesmo coletar a CPU do computador, por exemplo).
Se puder iniciar, provavelmente a plataforma estará bem. Caso contrário, a plataforma ainda será o problema.

1. Tente recriar manualmente o coletor de dados de ATA usando um prompt de comandos com privilégios elevados, executando estes comandos:

```dos
sc stop ATACenter
logman stop "Microsoft ATA Center"
logman export "Microsoft ATA Center" -xml c:\center.xml
logman delete "Microsoft ATA Center"
logman import "Microsoft ATA Center" -xml c:\center.xml
logman start "Microsoft ATA Center"
sc start ATACenter
```

## <a name="troubleshooting-ata-lightweight-gateway-startup"></a>Solução de problemas de inicialização do Gateway Lightweight do ATA

**Sintoma**

Seu Gateway do ATA não inicia e você receberá esse erro:<br></br>
*System.Net.Http.HttpRequestException: o código de status de resposta não indica êxito: 500 (erro interno do servidor)*

**Descrição**

Isso acontece porque, como parte do processo de instalação do Gateway Lightweight, o ATA aloca um limite de CPU que permite que o Gateway Lightweight use a CPU com um buffer de 15%. Se você tiver definido independentemente um limite usando a chave do Registro: esse conflito impedirá que o Gateway Lightweight seja iniciado. 

**Resolução**

1. Nas chaves do registro, se houver um valor DWORD chamado **desabilitar contadores de desempenho** , verifique se ele está definido como **0**:

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfOS\Performance\
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfProc\Performance
```

1. Em seguida, reinicie o serviço de PLA. O Gateway Lightweight do ATA automaticamente detectará a mudança e reiniciará o serviço.

## <a name="see-also"></a>Consulte Também

- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Planejamento da capacidade do ATA](ata-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-collection.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
