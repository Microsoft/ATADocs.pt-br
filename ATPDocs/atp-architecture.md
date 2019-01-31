---
title: Arquitetura da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Descreve a arquitetura do Azure ATP (Proteção Avançada contra Ameaças)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/27/2019
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6988b41b64dc3d8afef5f7af614f78b41501e2af
ms.sourcegitcommit: 19ff0ed88e450506b5725bbcbb0d0bd2f0c5e4bb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/27/2019
ms.locfileid: "55085309"
---
# <a name="azure-atp-architecture"></a>Arquitetura do Azure ATP

O ATP do Azure monitora seus controladores de domínio capturando e analisando o tráfego de rede e aproveitando os eventos do Windows diretamente de seus controladores de domínio, em seguida, analisa os dados em busca de ataques e ameaças. Utilizando criação de perfil, detecção determinística, aprendizado de máquina e algoritmos comportamentais que do Azure ATP aprende sobre sua rede, habilita a detecção de anomalias e avisa sobre atividades suspeitas.

Arquitetura da Proteção Avançada contra Ameaças do Azure:

![Diagrama de topologia da arquitetura do Azure ATP](media/atp-architecture-topology.png)

Esta seção descreve como o fluxo de captura de eventos e rede do ATP do Azure funciona e descreve detalhadamente as funcionalidades dos componentes principais: o portal do ATP do Azure, o sensor do ATP do Azure e o serviço de nuvem do ATP do Azure. 

Instalado diretamente em seus controladores de domínio, o sensor do ATP do Azure acessa os logs de eventos necessários diretamente do controlador de domínio. Depois que o tráfego de rede e os logs forem analisados pelo sensor, o Azure ATP enviará apenas as informações analisadas ao serviço de nuvem do Azure ATP (apenas um percentual dos logs é enviado). 

## <a name="azure-atp-components"></a>Componentes do Azure ATP
O Azure ATP é formado pelos seguintes componentes:

-   **Portal do Azure ATP** <br>
O portal do ATP do Azure permite a criação da sua instância do ATP do Azure, exibe os dados recebidos de sensores do ATP Azure e permite monitorar, gerenciar e investigar ameaças em seu ambiente de rede.  
-   **Sensor do Azure ATP**<br>
Sensores do Azure ATP são instalados diretamente em seus controladores de domínio. O sensor monitora diretamente o tráfego do controlador de domínio sem a necessidade de um servidor dedicado ou configuração de espelhamento de porta.

-   **Serviço de nuvem do Azure ATP**<br>
O serviço de nuvem do Azure ATP é executado na infraestrutura do Azure e implantado no momento nos EUA, na Europa e na Ásia. O serviço de nuvem do Azure ATP está conectado ao gráfico de segurança inteligente da Microsoft. 

## <a name="azure-atp-portal"></a>Portal do Azure ATP 
Use o portal do Azure ATP para:
- Criar sua instância do Azure ATP
- Integrar a outros serviços de segurança da Microsoft 
- Gerenciar definições de configuração do sensor do Azure ATP 
- Exibir dados recebidos de sensores do Azure ATP
- Monitorar atividades suspeitas detectadas e ataques suspeitos com base no modelo de cadeia de eliminação de ataque
- **Opcional**: o portal também pode ser configurado para enviar emails e eventos quando forem detectados problemas de integridade ou alertas de segurança

> [!NOTE]
> - Se nenhum sensor for instalado em sua instância do ATP do Azure em até 60 dias, ela poderá ser excluída e você precisará recriá-la.

## <a name="azure-atp-sensor"></a>Sensor do Azure ATP
O sensor do Azure ATP tem as seguintes funcionalidades principais:
- Capturar e inspecionar o tráfego de rede de controlador de domínio (tráfego local do controlador de domínio)
- Receber Eventos do Windows diretamente dos controladores de domínio 
- Receber informações de contabilidade RADIUS de seu provedor de VPN
- Recuperar dados sobre usuários e computadores do domínio do Active Directory
- Executar a resolução de entidades de rede (usuários, grupos e computadores)
- Transferir dados relevantes para o serviço de nuvem do Azure ATP

 
## <a name="azure-atp-sensor-features"></a>Funcionalidades do Sensor do Azure ATP
O sensor do Azure ATP lê eventos localmente, sem necessidade de comprar e manter hardware ou configurações adicionais. O sensor do ATP do Azure também dá suporte para o Rastreamento de Eventos para Windows (ETW), o qual fornece as informações de log para várias detecções. As detecções baseadas no ETW incluem Suspeita de ataques de DCShadow tentados usando a promoção do controlador de domínio e as solicitações de replicação do controlador de domínio.

### <a name="domain-synchronizer-candidate"></a>Candidato ao sincronizador de domínio

    The domain synchronizer candidate is responsible for synchronizing all entities from a specific Active Directory domain proactively (similar to the mechanism used by the domain controllers themselves for replication). One sensor is chosen randomly, from the list of candidates, to serve as the domain synchronizer. 

    If the synchronizer is offline for more than 30 minutes, another candidate is chosen instead. If there is no domain synchronizer available for a specific domain, Azure ATP proactively synchronizes entities and their changes, however Azure ATP retrieves new entities as they are detected in the monitored traffic. 
    
    If there is no domain synchronizer available, and you search for an entity that did not have any traffic related to it, no search results are displayed.

    By default, Azure ATP sensors are not synchronizer candidates. To manually set an Azure ATP sensor as a domain synchronizer candidate, follow the steps in the [Azure ATP installation workflow](install-atp-step5.md#configure-azure-atp-sensor-settings).

### <a name="resource-limitations"></a>Limitações de recursos

    The Azure ATP sensor includes a monitoring component that evaluates the available compute and memory capacity on the domain controller on which it is running. The monitoring process runs every 10 seconds and dynamically updates the CPU and memory utilization quota on the Azure ATP sensor process. The monitoring process makes sure the domain controller always has at least 15% of free compute and memory resources available.

    No matter what occurs on the domain controller, the monitoring process continually frees up resources to make sure the domain controller's core functionality is never affected.

    If the monitoring process causes the Azure ATP sensor to run out of resources, only partial traffic is monitored and the monitoring alert "Dropped port mirrored network traffic" appears in the Azure ATP portal Health page.

### <a name="windows-events"></a>Eventos do Windows

    To enhance Azure ATP detection coverage of suspected identity theft (pass-the-hash), suspicious authentication failures,modifications to sensitive groups, creation of suspicious services, and Honeytoken activity types of attack, Azure ATP needs to analyze the logs of the following Windows events: 4776,4732,4733,4728,4729,4756,4757, and 7045. These events are read automatically by Azure ATP sensors with correct [advanced audit policy settings](atp-advanced-audit-policy.md). 

## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/trisizingtool)
- [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md)
- [Configurar o encaminhamento de eventos](configure-event-forwarding.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
