---
title: Arquitetura da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Descreve a arquitetura do Azure ATP (Proteção Avançada contra Ameaças)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/30/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f23ae083ea09150849f95b58d1ab441af061f7bf
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166588"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*


# <a name="azure-atp-architecture"></a>Arquitetura do Azure ATP
Arquitetura da Proteção Avançada contra Ameaças do Azure:

![Diagrama de topologia da arquitetura do Azure ATP](media/atp-architecture-topology.png)

O Azure ATP monitora o tráfego de rede do controlador de domínio utilizando o espelhamento de porta para um sensor autônomo do Azure ATP usando comutadores físicos ou virtuais. Se você implantar o sensor do Azure ATP diretamente em seus controladores de domínio, ele eliminará a necessidade de espelhamento de porta. Além disso, o Azure ATP pode aproveitar os eventos do Windows (encaminhados diretamente de seus controladores de domínio ou de um servidor SIEM) e analisar os dados em relação a ataques e ameaças. O Azure ATP recebe tráfego analisado do sensor do Azure ATP e do sensor autônomo do Azure ATP. O Azure ATP realiza então a criação de perfil, executa detecção determinística e executa algoritmos comportamentais e de aprendizado de máquina para conhecer sua rede, permitindo a detecção de anomalias e avisando sobre atividades suspeitas.

Esta seção descreve o fluxo de rede e a captura de eventos e descreve detalhadamente a funcionalidade dos componentes principais do ATP: o sensor do Azure ATP, o sensor autônomo do Azure ATP (que tem a mesma funcionalidade básica do sensor autônomo do Azure ATP, mas requer um hardware adicional, o espelhamento de porta, a configuração e não tem suporte para detecções baseadas no Rastreamento de Eventos para Windows) e o serviço de nuvem do Azure ATP. 

Instalado diretamente em controladores de domínio, o sensor do ATP acessa os logs de eventos necessários diretamente do controlador de domínio. Após a análise desses logs e do tráfego de rede pelo sensor, o Azure ATP envia apenas essas informações analisadas ao serviço do Azure ATP (nem todos os logs).

## <a name="azure-atp-components"></a>Componentes do Azure ATP
O Azure ATP é formado pelos seguintes componentes:

-   **Portal de gerenciamento de espaço de trabalho do Azure ATP** <br>
O portal de gerenciamento de espaço de trabalho do Azure ATP permite criar e gerenciar espaços de trabalho e habilita a integração com outros serviços da Microsoft.

-   **Portal de espaço de trabalho do Azure ATP** <br>
O portal de espaço de trabalho do Azure ATP recebe dados de sensores e de sensores autônomos do ATP. Ele monitora, gerencia e investiga ameaças em seu ambiente.

-   **Sensor do Azure ATP**<br>
O sensor do Azure ATP está instalado diretamente em seus controladores de domínio e monitora o tráfego diretamente, sem a necessidade de uma configuração de espelhamento de porta ou um servidor dedicado. 

-   **Sensor autônomo do Azure ATP**<br>
O sensor autônomo do Azure ATP está instalado em um servidor dedicado que monitora o tráfego de seus controladores de domínio usando o espelhamento de porta ou uma TAP de rede. Essa é uma alternativa ao sensor do Azure ATP que requer hardware, espelhamento de porta e configuração adicionais. Os sensores autônomos do Azure ATP não têm suporte para detecções baseadas no Rastreamento de Eventos para Windows compatíveis com o sensor do ATP. 

## <a name="deployment-options"></a>Opções de implantação
Você pode implantar o Azure ATP usando a seguinte combinação de sensores:

-   **Usando somente sensores do Azure ATP**<br>
Sua implantação do Azure ATP pode conter somente sensores do Azure ATP: eles são implantados diretamente em cada controlador de domínio e não há a necessidade de servidores adicionais ou de configuração de espelhamento de porta.

-   **Usando somente sensores autônomos do Azure ATP** <br>
Sua implantação do Azure ATP pode conter somente sensores autônomos do Azure ATP, sem nenhum sensor do Azure ATP: todos os controladores de domínio devem estar configurados para habilitar o espelhamento de porta para um sensor autônomo do Azure ATP ou TAPs de rede devem estar em vigor.

-   **Usando sensores autônomos do Azure ATP e sensores do Azure ATP**<br>
Sua implantação do Azure ATP inclui sensores autônomos do Azure ATP e sensores do Azure ATP. Os sensores do Azure ATP são instalados em alguns de seus controladores de domínio (por exemplo, todos os controladores de domínio em seus sites de branch). Ao mesmo tempo, outros controladores de domínio são monitorados pelos sensores autônomos do Azure ATP, por exemplo, os maiores controladores de domínio nos data centers principais. 


### <a name="azure-atp-management-portal"></a>Portal de gerenciamento do Azure ATP

O portal de gerenciamento do Azure ATP permite:

-   Criar e gerenciar espaços de trabalho do Azure ATP

-   Integrar a outros serviços de segurança da Microsoft

> [!NOTE]
> - Atualmente, o Azure ATP oferece suporte à criação de apenas um espaço de trabalho. Depois de excluir um espaço de trabalho, você pode entrar em contato com o suporte para reativá-lo. Você pode ter no máximo três espaços de trabalho excluídos. Para aumentar o número de espaços de trabalho salvos e excluídos, entre em contato com o suporte do Azure ATP.
> - Se nenhum sensor for instalado no seu espaço de trabalho dentro de 60 dias, o espaço de trabalho poderá ser excluído e será necessário criá-lo novamente.



### <a name="azure-atp-workspace-portal"></a>Portal de espaço de trabalho do Azure ATP

O espaço de trabalho do Azure ATP permite que você gerencie a seguinte funcionalidade do Azure ATP:

-   Gerenciar definições de configuração do sensor e do sensor autônomo do Azure ATP

-   Exibir dados recebidos de sensores autônomos do Azure ATP e sensores do Azure ATP 

-   O monitor detectou atividades suspeitas com base em algoritmos comportamentais de machine learning para detectar comportamento anormal e algoritmos determinísticos para detectar ataques avançados com base na cadeia de invasão do ataque

-   Opcional: o portal de gerenciamento de espaço de trabalho pode ser configurado para enviar emails e eventos quando atividades suspeitas ou eventos de integridade forem detectados.


|||
|-|-|
|Portal de gerenciamento do Azure ATP|Gerencia o espaço de trabalho do Azure ATP.|
|Portal de espaço de trabalho do Azure ATP|O espaço de trabalho do Azure ATP é usado para configurar o Azure ATP e monitorar atividades suspeitas detectadas pelo Azure ATP em sua rede. O espaço de trabalho do Azure ATP não é dependente do sensor do Azure ATP e é executado mesmo quando o serviço do sensor do Azure ATP está parado. |
|Detectores|Os detectores usam algoritmos de aprendizado de máquina e regras determinísticas para localizar atividades suspeitas e comportamento anormal do usuário em sua rede.|


## <a name="azure-atp-sensor-and-azure-atp-standalone-sensor"></a>Sensor do Azure ATP e sensor autônomo do Azure ATP

O **sensor do Azure ATP** e o **sensor autônomo do Azure ATP** têm a mesma funcionalidade básica:

-   Capturar e inspecionar o tráfego de rede do controlador de domínio. Este é o tráfego local do controlador de domínio em sensores do Azure ATP e o tráfego espelhado da porta para sensores autônomos do Azure ATP. 

-   Receber eventos do Windows diretamente dos controladores de domínio (para sensores do ATP) ou de servidores de SIEM ou Syslog (para sensores autônomos do ATP)

-   Receber informações de contabilidade RADIUS de seu provedor de VPN

-   Recuperar dados sobre usuários e computadores do domínio do Active Directory

-   Executar a resolução de entidades de rede (usuários, grupos e computadores)

-   Transferir dados relevantes para o serviço de nuvem do Azure ATP

-   Monitore um único controlador de domínio para um sensor do Azure ATP ou monitore vários controladores de domínio de um único sensor autônomo do Azure ATP.

Por padrão, o Azure ATP é compatível com até 100 sensores. Caso deseje instalar mais, entre em contato com o suporte do Azure ATP.

O sensor autônomo do Azure ATP recebe o tráfego de rede espelhado e os eventos do Windows da sua rede e processa-os nos seguintes componentes principais:

|||
|-|-|
|Ouvinte de Rede|O Ouvinte de Rede captura o tráfego de rede e o analisa. Essa é uma tarefa com uso intenso da CPU, portanto, é muito importante verificar os [Pré-requisitos do Azure ATP](atp-prerequisites.md) ao planejar seu sensor ou sensor autônomo do Azure ATP.|
|Ouvinte de Evento|O Ouvinte de Eventos captura e analisa Eventos do Windows encaminhados de um servidor SIEM na sua rede.|
|Leitor de Log de Eventos do Windows|O Leitor de Log de Eventos do Windows lê e analisa Eventos do Windows encaminhados ao Log de Eventos do Windows do sensor autônomo do Azure ATP nos controladores de domínio.|
|Conversor de Atividade de Rede | Converte o tráfego analisado em uma representação lógica do tráfego usado pelo Azure ATP (NetworkActivity).
|Resolvedor de Entidade|O Resolvedor de Entidade utiliza os dados analisados (tráfego de rede e eventos) e resolve os dados com o Active Directory para localizar informações de conta e identidade. Em seguida, ele é correspondido com os endereços IP encontrados nos dados analisados. O Resolvedor de Entidade inspeciona os cabeçalhos de pacote com eficiência, permite analisar pacotes de autenticação para nomes, propriedades e identidades de computadores. O Resolvedor de Entidade combina os pacotes de autenticação analisado com os dados no pacote real.|
|Remetente de Entidade|O Remetente de Entidade envia os dados analisados e correspondentes para o serviço de nuvem do Azure ATP.|

## <a name="azure-atp-sensor-features"></a>Funcionalidades do sensor do Azure ATP

Os recursos a seguir funcionam de modo diferente dependendo de você estar executando um sensor ou um sensor autônomo do Azure ATP.

-   O sensor do Azure ATP lê os eventos localmente, sem a necessidade de comprar e manter hardware adicionais ou configurar encaminhamentos de eventos necessários com os sensores autônomos do ATP. O sensor do Azure ATP também tem suporte para o ETW, o que fornece as informações de log para várias detecções. As detecções baseadas no ETW incluem tanto a Solicitação de Replicação Suspeita quanto a Promoção de Controlador de Domínio Suspeita, ambas são possíveis ataques DCShadow e não tem suporte nos sensores autônomos do ATP.  

-   **Candidato ao sincronizador de domínio**<br>
O candidato de sincronizador de domínio é responsável por sincronizar todas as entidades de um determinado domínio do Active Directory de forma proativa (semelhante ao mecanismo utilizado pelos próprios controladores de domínio para replicação). Um sensor é escolhido aleatoriamente, na lista de candidatos, para servir como sincronizador de domínio. <br><br>
Se o sincronizador estiver offline por mais de 30 minutos, outro candidato é escolhido em seu lugar. Se não houver nenhum sincronizador de domínio disponível para um domínio específico, o Azure ATP não poderá sincronizar entidades e suas alterações proativamente. No entanto, o Azure ATP recuperará novas entidades reativamente conforme elas forem detectadas no tráfego monitorado. 
<br>Se nenhum sincronizador de domínio estiver disponível e você pesquisar por uma entidade que não tem qualquer tráfego relacionado a ela, nenhum resultado será exibido.<br><br>
Por padrão, todos os sensores autônomos do Azure ATP são candidatos a sincronizador.<br><br>
Sensores do Azure ATP não são candidatos a sincronizador por padrão.


-   **Limitações de recursos**<br>
O sensor do Azure ATP inclui um componente de monitoramento que avalia a capacidade de computação e de memória disponível no controlador de domínio no qual ele está sendo executado. O processo de monitoramento é executado a cada 10 segundos e atualiza dinamicamente a cota de utilização de CPU e memória no processo do sensor do Azure ATP para garantir que a qualquer hora o controlador de domínio tenha pelo menos 15% de recursos de computação e memória livres.<br><br>
Não importa o que acontece no controlador de domínio, esse processo sempre libera os recursos para fazer com que a funcionalidade principal do controlador de domínio não seja afetada.<br><br>
Se isso fizer com que o sensor do Azure ATP fique sem recursos, apenas o tráfego parcial será monitorado e o alerta de monitoramento "Tráfego de rede espelhado na porta descartado" será exibido na página Integridade.

A tabela abaixo fornece um exemplo de um controlador de domínio com recurso de computação suficiente disponível para permitir uma cota maior de recursos de computação necessária no momento, de forma que todo o tráfego é monitorado:

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Sensor do Azure ATP (Microsoft.Tri.sensor.exe)|Diversos (outros processos) |Cota do sensor do Azure ATP|O sensor está descartando tráfego?|
|30%|20%|10%|45%|Não|

Se o Active Directory precisa de mais capacidade de computação, a cota demandada pelo sensor do Azure ATP é reduzida. No exemplo a seguir, o sensor do Azure ATP precisa de mais do que a cota alocada e descarta parte do tráfego (monitorando apenas o tráfego parcial):

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Sensor do Azure ATP (Microsoft.Tri.sensor.exe)|Diversos (outros processos) |Cota do sensor do Azure ATP|O sensor está descartando tráfego?|
|60%|15%|10%|15%|Sim|


## <a name="your-network-components"></a>Componentes da sua rede
Verifique se os seguintes componentes estão configurados para funcionar com o Azure ATP.

### <a name="port-mirroring"></a>Espelhamento de porta
Se você estiver usando sensores autônomos do Azure ATP, é preciso configurar o espelhamento de porta para os controladores de domínio que são monitorados. Defina o sensor autônomo do Azure ATP como o destino usando os comutadores físicos ou virtuais. Outra opção é usar TAPs de rede. O Azure ATP funcionará se alguns e não todos, controladores de domínio forem monitorados, mas a detecção é menos eficiente.

Enquanto o espelhamento de portas espelha todo o tráfego de rede do controlador de domínio para o sensor autônomo do Azure ATP, apenas um pequeno percentual desse tráfego é compactada e enviada para o serviço de nuvem do Azure ATP para análise.

Seus controladores de domínio e o sensor autônomo do Azure ATP podem ser físicos ou virtuais. Para saber mais, confira [Configurar o espelhamento de porta](configure-port-mirroring.md).


### <a name="events"></a>Eventos
Para melhorar a cobertura de detecção do Azure ATP de Pass-the-Hash, Falhas de autenticação suspeitas, Modificação de grupos confidenciais, Criação de serviços suspeitos e Tipos ataque de atividade de Honey Token, o Azure ATP precisa analisar os logs dos seguintes eventos do Windows: 4776,4732,4733,4728,4729,4756,4757 e 7045. Esses eventos são lidos automaticamente pelos sensores do Azure ATP com as configurações corretas de política de auditoria avançada. Em situações em que os sensores autônomos do Azure ATP são implantados, os eventos de log podem ser encaminhados para o sensor autônomo de duas maneiras: configurando o sensor autônomo do Azure ATP para escutar eventos do SIEM ou [Configurando o Encaminhamento de Eventos do Windows](configure-event-forwarding.md). 

> [!NOTE]
> - O encaminhamento de eventos do Windows para sensores autônomos não oferece suporte para o Rastreamento de Eventos para Windows (ETW). As detecções baseadas no ETW incluem tanto a solicitação de replicação suspeita quanto a promoção de controlador de domínio suspeita, ambas são possíveis ataques DCShadow.  

-   Configuração do sensor autônomo do Azure ATP para escutar eventos de SIEM <br>Configure o SIEM para encaminhar eventos específicos do Windows para o ATA. O Azure ATP dá suporte a vários fornecedores SIEM. Confira mais informações em [Configurar Encaminhamento de Eventos do Windows](configure-event-forwarding.md).

-   Configuração do encaminhamento de eventos do Windows<br>Outra maneira do Azure ATP conseguir obter seus eventos é configurando seus controladores de domínio para encaminhar eventos do Windows 4776, 4732, 4733, 4728, 4729, 4756, 4757 e 7045 para seu sensor autônomo do Azure ATP. Isso é especialmente útil se você não tiver um SIEM ou se o SIEM não tiver suporte atualmente do ATP. Para obter mais informações sobre o Encaminhamento de Eventos do Windows no ATP, confira [Configurando o encaminhamento de eventos do Windows](configure-event-forwarding.md). Isso se aplica somente aos sensores autônomos físicos do Azure ATP – não ao sensor do Azure ATP.


## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/trisizingtool)
- [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md)
- [Configurar o encaminhamento de eventos](configure-event-forwarding.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)
