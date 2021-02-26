---
title: Arquitetura do Microsoft Defender para Identidade
description: Descreve a arquitetura do Microsoft Defender para Identidade
ms.date: 12/23/2020
ms.topic: overview
ms.openlocfilehash: 920c4fa99ebe2dad211fd7edae9ed928c1426510
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533878"
---
# <a name="microsoft-defender-for-identity-architecture"></a>Arquitetura do Microsoft Defender para Identidade

O [!INCLUDE [Product long](includes/product-long.md)] monitora seus controladores de domínio capturando e analisando o tráfego de rede e aproveitando os eventos do Windows diretamente dos controladores de domínio. Em seguida, ele analisa os dados em busca de ataques e ameaças. Utilizando criação de perfil, detecção determinística, machine learning e algoritmos comportamentais, o [!INCLUDE [Product short](includes/product-short.md)] aprende mais sobre a sua rede, habilita a detecção de anomalias e alerta você sobre atividades suspeitas.

Arquitetura do [!INCLUDE [Product short](includes/product-short.md)]:

![Diagrama de topologia da arquitetura do [!INCLUDE [Product short](includes/product-short.md)]](media/architecture-topology.png)

Esta seção descreve como funciona o fluxo de captura de eventos e rede do [!INCLUDE [Product short](includes/product-short.md)] e descreve detalhadamente as funcionalidades dos componentes principais: o portal do [!INCLUDE [Product short](includes/product-short.md)], o sensor do [!INCLUDE [Product short](includes/product-short.md)] e o serviço de nuvem do [!INCLUDE [Product short](includes/product-short.md)].

Instalado diretamente em seu controlador de domínio ou servidores dos AD FS, o sensor do [!INCLUDE [Product short](includes/product-short.md)] acessa os logs de eventos necessários diretamente dos servidores. Depois que o tráfego de rede e os logs são analisados pelo sensor, o [!INCLUDE [Product short](includes/product-short.md)] envia apenas as informações analisadas ao serviço de nuvem do [!INCLUDE [Product short](includes/product-short.md)] (somente um percentual dos logs é enviado).

## <a name="defender-for-identity-components"></a>Componentes do Microsoft Defender para Identidade

O [!INCLUDE [Product short](includes/product-short.md)] é formado pelos seguintes componentes:

- **Portal do [!INCLUDE [Product short](includes/product-short.md)]**  
O portal do [!INCLUDE [Product short](includes/product-short.md)] permite a criação da sua instância do [!INCLUDE [Product short](includes/product-short.md)], exibe os dados recebidos dos sensores do [!INCLUDE [Product short](includes/product-short.md)] e permite que você monitore, gerencie e investigue as ameaças no seu ambiente de rede.

- **Sensor do [!INCLUDE [Product short](includes/product-short.md)]**  
Os sensores do [!INCLUDE [Product short](includes/product-short.md)] podem ser instalados diretamente nos seguintes servidores:
  - **Controladores de domínio**: O sensor monitora diretamente o tráfego do controlador de domínio sem a necessidade de um servidor dedicado ou configuração de espelhamento de porta.
  - **AD FS**: O sensor monitora diretamente o tráfego de rede e os eventos de autenticação.
- **Serviço de nuvem do [!INCLUDE [Product short](includes/product-short.md)]**  
O serviço de nuvem do [!INCLUDE [Product short](includes/product-short.md)] é executado na infraestrutura do Azure e é atualmente implantado nos EUA, na Europa e na Ásia. O serviço de nuvem do [!INCLUDE [Product short](includes/product-short.md)] está conectado ao grafo de segurança inteligente da Microsoft.

## <a name="defender-for-identity-portal"></a>Portal do Defender para Identidade

Use o portal do [!INCLUDE [Product short](includes/product-short.md)] para:

- Criar sua instância do [!INCLUDE [Product short](includes/product-short.md)]
- Integrar a outros serviços de segurança da Microsoft
- Gerenciar as definições de configuração do sensor do [!INCLUDE [Product short](includes/product-short.md)]
- Ver os dados recebidos dos sensores do [!INCLUDE [Product short](includes/product-short.md)]
- Monitorar atividades suspeitas detectadas e ataques suspeitos com base no modelo de cadeia de eliminação de ataque
- **Opcional**: o portal também pode ser configurado para enviar emails e eventos quando forem detectados problemas de integridade ou alertas de segurança

> [!NOTE]
> Se nenhum sensor for instalado na sua instância do [!INCLUDE [Product short](includes/product-short.md)] em até 60 dias, ela poderá ser excluída e você precisará recriá-la.

## <a name="defender-for-identity-sensor"></a>Sensor do Microsoft Defender para Identidade

O sensor do [!INCLUDE [Product short](includes/product-short.md)] tem as seguintes funcionalidades principais:

- Capturar e inspecionar o tráfego de rede de controlador de domínio (tráfego local do controlador de domínio)
- Receber Eventos do Windows diretamente dos controladores de domínio
- Receber informações de contabilidade RADIUS de seu provedor de VPN
- Recuperar dados sobre usuários e computadores do domínio do Active Directory
- Executar a resolução de entidades de rede (usuários, grupos e computadores)
- Transferir dados relevantes para o serviço de nuvem do [!INCLUDE [Product short](includes/product-short.md)]

## <a name="defender-for-identity-sensor-features"></a>Recursos do sensor do Microsoft Defender para Identidade

O sensor do [!INCLUDE [Product short](includes/product-short.md)] lê eventos localmente, sem a necessidade de comprar e manter nenhum hardware ou configurações adicionais. O sensor do [!INCLUDE [Product short](includes/product-short.md)] também dá suporte ao Rastreamento de Eventos para Windows (ETW), que fornece as informações de log para várias detecções. As detecções baseadas no ETW incluem Suspeita de ataques de DCShadow tentados usando a promoção do controlador de domínio e as solicitações de replicação do controlador de domínio.

### <a name="domain-synchronizer-process"></a>Processo sincronizador de domínio

O processo sincronizador de domínio é responsável por sincronizar todas as entidades de um determinado domínio do Active Directory de forma proativa (semelhante ao mecanismo utilizado pelos próprios controladores de domínio para replicação). Um sensor é automaticamente escolhido de forma aleatória entre todos os seus sensores qualificados para servir como o sincronizador de domínio.

Se o sincronizador de domínio estiver offline por mais de 30 minutos, outro sensor será escolhido automaticamente em seu lugar.

### <a name="resource-limitations"></a>Limitações de recursos

O sensor do [!INCLUDE [Product short](includes/product-short.md)] inclui um componente de monitoramento que avalia a capacidade de computação e de memória disponível no controlador de domínio no qual ele está sendo executado. O processo de monitoramento é executado a cada 10 segundos e atualiza dinamicamente a cota de utilização de CPU e memória no processo do sensor do [!INCLUDE [Product short](includes/product-short.md)]. O processo de monitoramento verifica se o controlador de domínio sempre tem pelo menos 15% de recursos de computação e memória livres disponíveis.

Não importa o que ocorra no controlador de domínio, o processo de monitoramento libera continuamente os recursos para garantir que a funcionalidade principal do controlador de domínio nunca seja afetada.

Se o processo de monitoramento fizer o sensor do [!INCLUDE [Product short](includes/product-short.md)] ficar sem recursos, apenas parte do tráfego será monitorado e o alerta de integridade "Tráfego de rede espelhado na porta removido" será exibido na página Integridade do portal do [!INCLUDE [Product short](includes/product-short.md)].

### <a name="windows-events"></a>Eventos do Windows

Para aprimorar a cobertura de detecção do [!INCLUDE [Product short](includes/product-short.md)] relacionada a autenticações NTLM, modificações a grupos confidenciais e criação de serviços suspeitos, o [!INCLUDE [Product short](includes/product-short.md)] precisa analisar os logs dos seguintes eventos do Windows: 4776,4732,4733,4728,4729,4756,4757,7045 e 8004. Esses eventos são lidos automaticamente pelos sensores do [!INCLUDE [Product short](includes/product-short.md)] com as [configurações corretas de política de auditoria avançada](configure-windows-event-collection.md). Para [verificar se o evento 8004 do Windows foi auditado](configure-windows-event-collection.md#ntlm-authentication-using-windows-event-8004) conforme necessário pelo serviço, examine as [configurações de auditoria do NTLM](/archive/blogs/askds/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7).

## <a name="next-steps"></a>Próximas etapas

- [Pré-requisitos do [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Ferramenta de dimensionamento do [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/trisizingtool)
- [Planejamento de capacidade do [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md)
- [Configurar o encaminhamento de eventos](configure-event-forwarding.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
