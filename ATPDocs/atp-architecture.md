---
title: Arquitetura do Azure Advanced Threat Protection
description: Descreve a arquitetura do Azure ATP (Proteção Avançada contra Ameaças)
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 09/23/2019
ms.topic: article
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a6ae76dcee7b6a54f7721c77277387ac4f2e7fbb
ms.sourcegitcommit: 8d5cd330564eeaf4bc9560db7814c85e71e0fb60
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/05/2020
ms.locfileid: "80666229"
---
# <a name="azure-atp-architecture"></a>Arquitetura do ATP do Azure

O ATP do Azure monitora seus controladores de domínio capturando e analisando o tráfego de rede e aproveitando os eventos do Windows diretamente de seus controladores de domínio, em seguida, analisa os dados em busca de ataques e ameaças. Utilizando criação de perfil, detecção determinística, aprendizado de máquina e algoritmos comportamentais que do Azure ATP aprende sobre sua rede, habilita a detecção de anomalias e avisa sobre atividades suspeitas.

Arquitetura da Proteção Avançada contra Ameaças do Azure:

![Diagrama de topologia da arquitetura do Azure ATP](media/atp-architecture-topology.png)

Esta seção descreve como o fluxo de captura de eventos e rede do ATP do Azure funciona e descreve detalhadamente as funcionalidades dos componentes principais: o portal do ATP do Azure, o sensor do ATP do Azure e o serviço de nuvem do ATP do Azure. 

Instalado diretamente em seus controladores de domínio, o sensor do ATP do Azure acessa os logs de eventos necessários diretamente do controlador de domínio. Depois que o tráfego de rede e os logs forem analisados pelo sensor, o Azure ATP enviará apenas as informações analisadas ao serviço de nuvem do Azure ATP (apenas um percentual dos logs é enviado). 

## <a name="azure-atp-components"></a>Componentes da Azure ATP
O Azure ATP é formado pelos seguintes componentes:

-    **Portal do Azure ATP** <br>
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

 
## <a name="azure-atp-sensor-features"></a>Funcionalidades do sensor do Azure ATP

O sensor do Azure ATP lê eventos localmente, sem necessidade de comprar e manter hardware ou configurações adicionais. O sensor do ATP do Azure também dá suporte para o Rastreamento de Eventos para Windows (ETW), o qual fornece as informações de log para várias detecções. As detecções baseadas no ETW incluem Suspeita de ataques de DCShadow tentados usando a promoção do controlador de domínio e as solicitações de replicação do controlador de domínio.

### <a name="domain-synchronizer-process"></a>Processo sincronizador de domínio

O processo sincronizador de domínio é responsável por sincronizar todas as entidades de um determinado domínio do Active Directory de forma proativa (semelhante ao mecanismo utilizado pelos próprios controladores de domínio para replicação). Um sensor é automaticamente escolhido de forma aleatória entre todos os seus sensores qualificados para servir como o sincronizador de domínio. 

Se o sincronizador de domínio estiver offline por mais de 30 minutos, outro sensor será escolhido automaticamente em seu lugar. 
    
### <a name="resource-limitations"></a>Limitações de recursos

O sensor do ATP do Azure inclui um componente de monitoramento que avalia a capacidade de computação e de memória disponível no controlador de domínio no qual ele está sendo executado. O processo de monitoramento é executado a cada 10 segundos e atualiza dinamicamente a cota de utilização de CPU e memória no processo de sensor do Azure ATP. O processo de monitoramento verifica se o controlador de domínio sempre tem pelo menos 15% de recursos de computação e memória livres disponíveis.

Não importa o que ocorra no controlador de domínio, o processo de monitoramento libera continuamente os recursos para garantir que a funcionalidade principal do controlador de domínio nunca seja afetada.

Se o processo de monitoramento fizer o sensor do ATP do Azure ficar sem recursos, apenas parte do tráfego será monitorado e o alerta de integridade "Tráfego de rede espelhado na porta descartado" será exibido na página Integridade do portal do ATP do Azure.

### <a name="windows-events"></a>Eventos do Windows

Para melhorar a cobertura de detecção da ATP do Azure relacionada a autenticações NTLM, modificações a grupos confidenciais e criação de serviços suspeitos, a ATP do Azure precisa analisar os logs dos seguintes eventos do Windows: 4776,4732,4733,4728,4729,4756,4757,7045 e 8004. Esses eventos são lidos automaticamente pelos sensores do Azure ATP com as [configurações corretas de política de auditoria avançada](atp-advanced-audit-policy.md). Para [verificar se o evento 8004 do Windows foi auditado](configure-windows-event-collection.md#ntlm-authentication-using-windows-event-8004) conforme necessário pelo serviço, examine as [configurações de auditoria do NTLM](https://blogs.technet.microsoft.com/askds/2009/10/08/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7/).

## <a name="next-steps"></a>Próximas etapas

- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Ferramenta de dimensionamento do Azure ATP](https://aka.ms/trisizingtool)
- [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md)
- [Configurar o encaminhamento de eventos](configure-event-forwarding.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
