---
title: Arquitetura da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Descreve a arquitetura do Azure ATP (Proteção Avançada contra Ameaças)
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 1/27/2019
ms.topic: article
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ac10508d7120f6c643c4f8cd0ad59b32ed09bcb0
ms.sourcegitcommit: c48db18274edb2284e281960c6262d97f96e01d2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56264212"
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
O portal do ATP do Azure permite a criação da sua instância do ATP do Azure, exibe os dados recebidos de sensores do ATP do Azure e permite monitorar, gerenciar e investigar ameaças em seu ambiente de rede.  
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

O candidato de sincronizador de domínio é responsável por sincronizar todas as entidades de um determinado domínio do Active Directory de forma proativa (semelhante ao mecanismo utilizado pelos próprios controladores de domínio para replicação). Um sensor é escolhido aleatoriamente, na lista de candidatos, para servir como sincronizador de domínio. 

Se o sincronizador estiver offline por mais de 30 minutos, outro candidato é escolhido em seu lugar. Se não houver nenhum sincronizador de domínio disponível para um domínio específico, o ATP do Azure sincronizará proativamente entidades e suas alterações, no entanto, o ATP do Azure recuperará novas entidades reativamente conforme elas forem detectadas no tráfego monitorado.
    
Se nenhum sincronizador de domínio estiver disponível e você pesquisar por uma entidade que não tem qualquer tráfego relacionado a ela, nenhum resultado da pesquisa será exibido.

Por padrão, sensores do ATP do Azure não são candidatos a sincronizador. Para definir manualmente um sensor do ATP do Azure como um candidato a sincronizador de domínio, siga as etapas no [fluxo de trabalho de instalação do Azure ATP](install-atp-step5.md).

### <a name="resource-limitations"></a>Limitações de recursos

O sensor do ATP do Azure inclui um componente de monitoramento que avalia a capacidade de computação e de memória disponível no controlador de domínio no qual ele está sendo executado. O processo de monitoramento é executado a cada 10 segundos e atualiza dinamicamente a cota de utilização de CPU e memória no processo de sensor do Azure ATP. O processo de monitoramento verifica se o controlador de domínio sempre tem pelo menos 15% de recursos de computação e memória livres disponíveis.

Não importa o que ocorra no controlador de domínio, o processo de monitoramento libera continuamente os recursos para garantir que a funcionalidade principal do controlador de domínio nunca seja afetada.

Se o processo de monitoramento fizer o sensor do Azure ATP ficar sem recursos, apenas tráfego parcial será monitorado e o alerta de monitoramento "Tráfego de rede espelhado na porta descartado" será exibido na página Integridade do portal do Azure ATP.

### <a name="windows-events"></a>Eventos do Windows

Para aprimorar a cobertura de detecção do ATP do Azure de suspeita de roubo de identidade (pass-the-hash), falhas de autenticação suspeitas, modificação de grupos confidenciais, criação de serviços suspeitos e tipos ataque de atividade de Honeytoken, o ATP do Azure precisa analisar os logs dos seguintes eventos do Windows: 4776,4732,4733,4728,4729,4756,4757 e 7045. Esses eventos são lidos automaticamente pelos sensores do Azure ATP com as [configurações corretas de política de auditoria avançada](atp-advanced-audit-policy.md). 

## <a name="next-steps"></a>Próximas etapas

- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/trisizingtool)
- [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md)
- [Configurar o encaminhamento de eventos](configure-event-forwarding.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
