---
title: Solução de problemas da Proteção Avançada contra Ameaças ao Azure usando os logs | Microsoft Docs
description: Descreve como você pode usar os logs do Azure ATP para solucionar problemas
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: de796346-647d-48e1-970a-8f072e990f1e
ms.reviewer: ''
ms.suite: ''
ms.openlocfilehash: 2cd1d7b070818044e74838178b0fab5838ab46ef
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783246"
---
*Aplica-se a: Proteção Avançada contra Ameaças*



# <a name="troubleshooting-azure-advanced-threat-protection-atp-sensor-using-the-atp-logs"></a>Solução de problemas do sensor do ATP (Proteção Avançada contra Ameaças) ao Azure usando os logs do ATP
Os logs do ATP fornecem informações sobre o que cada componente do sensor do Azure ATP está fazendo a qualquer hora.


Os logs do Azure ATP estão localizados na subpasta **Logs**, na qual o ATP está instalado; o local padrão é: **C:\Program Files\Azure Advanced Threat Protection Sensor\\**. No local de instalação padrão, ela pode ser encontrada em: **C:\Program Files\Azure Advanced Threat Protection Sensor\version number\Logs**.

O sensor do Azure ATP tem os seguintes logs:

-   **Microsoft.Tri.Sensor.log** – Esse log contém tudo o que acontece no sensor do Azure ATP (inclusive resolução e erros). Usado principalmente para obter o status geral de todas as operações em ordem cronológica de ocorrência.

-   **Microsoft.Tri.Sensor-Resolution.log** – Esse log contém os detalhes da resolução das entidades vistas no tráfego pelo sensor do ATP. Usado principalmente para investigar problemas de resolução de entidades.

-   **Microsoft.Tri.Sensor-Errors.log** – Esse log contém apenas os erros que são detectados pelo sensor do ATP. Usado principalmente para executar verificações de integridade e investigar problemas que precisam estar correlacionados a horários específicos.

-   **Microsoft.Tri.Sensor.Updater.log** – Esse log é usado para o processo do atualizador de sensor, que é responsável por atualizar o sensor do ATP, se estiver configurado para fazer isso automaticamente. 


> [!NOTE]
> Os três primeiros arquivos de log têm um tamanho máximo de até 50 MB. Quando esse tamanho é atingido, um novo arquivo de log é aberto e o anterior é renomeado como "&lt;nome do arquivo original&gt;-Archived-00000". Esse número aumenta a cada renomeação. Por padrão, se já houver mais de 10 arquivos do mesmo tipo, os mais antigos serão excluídos.

## <a name="azure-atp-deployment-logs"></a>Logs de implantação do Azure ATP
Os logs de implantação do Azure ATP estão localizados no diretório temp do usuário que instalou o produto. No local de instalação padrão, ele pode ser encontrado em: **C:\Usuários\Administrator\AppData\Local\Temp** (ou um diretório acima de %temp%).

Logs de implantação do sensor do Azure ATP:

-   **Azure Advanced Threat Protection Sensor_YYYYMMDDHHMMSS.log** – Esse log lista as etapas no processo de implantação do sensor do Azure ATP. Usado principalmente para acompanhar o processo de implantação do sensor do Azure ATP.

-   **Azure Advanced Threat Protection Sensor_YYYYMMDDHHMMSS_001_MsiPackage.log** – Esse arquivo de log lista as etapas no processo de implantação dos binários do sensor do Azure ATP. Usado principalmente para acompanhar a implantação dos binários do sensor do Azure ATP.


> [!NOTE] 
> Além dos logs de implantação mencionados aqui, há outros logs que começam com "Proteção Avançada contra Ameaças ao Azure" que também pode fornecer informações adicionais sobre o processo de implantação.


## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Confira o fórum do Azure ATP!](https://aka.ms/azureatpcommunity)