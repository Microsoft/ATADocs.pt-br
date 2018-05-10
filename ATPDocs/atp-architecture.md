---
title: Arquitetura da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Descreve a arquitetura do Azure ATP (Proteção Avançada contra Ameaças)
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/29/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 838c5ce470bdf78ec81aed5d6fa1cf2407abc6f9
ms.sourcegitcommit: 5c0f914b44bfb8e03485f12658bfa9a7cd3d8bbc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/30/2018
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*


# <a name="azure-atp-architecture"></a>Arquitetura do Azure ATP
A arquitetura da Proteção Avançada contra Ameaças do Azure é detalhada neste diagrama:

![Diagrama de topologia da arquitetura do Azure ATP](media/atp-architecture-topology.png)

O Azure ATP monitora o tráfego de rede do controlador de domínio utilizando o espelhamento de porta para um sensor autônomo do Azure ATP usando comutadores físicos ou virtuais. Se você implantar o sensor do Azure ATP diretamente em seus controladores de domínio, ele eliminará a necessidade de espelhamento de porta. Além disso, o Azure ATP pode aproveitar os eventos do Windows (encaminhados diretamente de seus controladores de domínio ou de um servidor SIEM) e analisar os dados em relação a ataques e ameaças. O Azure ATP recebe tráfego analisado do sensor autônomo do Azure ATP e do sensor do Azure ATP. Ele realiza então a criação de perfil, executa detecção determinística e executa algoritmos comportamentais e de aprendizado de máquina para conhecer sua rede, permitindo a detecção de anomalias e avisando sobre atividades suspeitas.

Esta seção descreve o fluxo de rede e a captura de eventos e descreve detalhadamente a funcionalidade dos componentes principais do ATP: o sensor autônomo do Azure ATP, o sensor do Azure ATP (que tem a mesma funcionalidade básica do sensor autônomo do Azure ATP) e o serviço de nuvem do Azure ATP. 

Quando instalado diretamente em controladores de domínio, o sensor acessa os logs de eventos necessários diretamente do controlador de domínio. Após a análise desses logs e do tráfego de rede pelo sensor, o Azure ATP envia apenas essas informações analisadas ao serviço do Azure ATP (nem todos os logs).

## <a name="azure-atp-components"></a>Componentes do Azure ATP
O Azure ATP é formado pelos seguintes componentes:

-   **Portal de gerenciamento de espaço de trabalho do Azure ATP** <br>
O portal de gerenciamento de espaço de trabalho do Azure ATP permite criar espaços de trabalho e habilita a integração com outros serviços da Microsoft.

> [!NOTE]
> Somente os sensores de uma única floresta do Active Directory podem se conectar a um único espaço de trabalho.

-   **Portal de espaço de trabalho do Azure ATP** <br>
O portal de espaço de trabalho do Azure ATP recebe dados de sensores e de sensores autônomos do ATP. Ele monitora, gerencia e investiga ameaças em seu ambiente.

-   **Sensor do Azure ATP**<br>
O sensor do Azure ATP está instalado diretamente em seus controladores de domínio e monitora o tráfego diretamente, sem a necessidade de uma configuração de espelhamento de porta ou um servidor dedicado. 

-   **Sensor autônomo do Azure ATP**<br>
O sensor autônomo do Azure ATP está instalado em um servidor dedicado que monitora o tráfego de seus controladores de domínio usando o espelhamento de porta ou uma TAP de rede. É uma alternativa ao sensor do Azure ATP.

## <a name="deployment-options"></a>Opções de implantação
Você pode implantar o Azure ATP usando a seguinte combinação de sensores:

-   **Usando somente sensores do Azure ATP**<br>
Sua implantação do Azure ATP pode conter somente sensores do Azure ATP: eles são implantados em cada controlador de domínio e não há a necessidade de servidores adicionais ou de configuração de espelhamento de porta.

-   **Usando somente sensores autônomos do Azure ATP** <br>
Sua implantação do Azure ATP pode conter somente sensores autônomos do Azure ATP, sem nenhum sensor do Azure ATP: todos os controladores de domínio devem estar configurados para habilitar o espelhamento de porta para um sensor autônomo do Azure ATP ou TAPs de rede devem estar em vigor.

-   **Usando sensores autônomos do Azure ATP e sensores do Azure ATP**<br>
Sua implantação do Azure ATP inclui sensores autônomos do Azure ATP e sensores do Azure ATP. Os sensores do Azure ATP são instalados em alguns de seus controladores de domínio (por exemplo, todos os controladores de domínio em seus sites de branch). Ao mesmo tempo, outros controladores de domínio são monitorados pelos sensores autônomos do Azure ATP (por exemplo, os maiores controladores de domínio em seus data centers principais).


### <a name="azure-atp-workspace-management-portal"></a>Portal de gerenciamento de espaço de trabalho do Azure ATP

O portal de gerenciamento de espaço de trabalho do Azure ATP permite:

-   Criar e gerenciar espaços de trabalho do Azure ATP

-   Integrar a outros serviços de segurança da Microsoft

Definir seu espaço de trabalho principal como **Primário**. Somente um espaço de trabalho pode ser definido como primário. Definir um espaço de trabalho como primário afeta as integrações – você só pode integrar o Azure ATP com o Windows Defender ATP para seu espaço de trabalho primário. Você pode alterar qual espaço de trabalho é primário posteriormente, mas, para fazer isso, você precisará remover as integrações já definidas para o espaço de trabalho primário atual.

> [!NOTE]
> Atualmente, a ATP do Azure rem suporte para criação de dois espaços de trabalho. Recomendamos criar um espaço de trabalho principal para o ambiente de produção e um espaço de trabalho adicional como um ambiente de preparo.
> Depois de excluir um espaço de trabalho, você pode entrar em contato com o suporte para reativá-lo. É possível ter um máximo de três espaços de trabalho excluídos. Para aumentar o número de espaços de trabalho salvos e excluídos, entre em contato com o suporte do Azure ATP.


### <a name="azure-atp-workspace-portal"></a>Portal de espaço de trabalho do Azure ATP

O espaço de trabalho do Azure ATP permite que você gerencie a seguinte funcionalidade do Azure ATP:

-   Gerenciar definições de configuração do sensor e do sensor autônomo do Azure ATP

-   Exibir dados recebidos de sensores autônomos do Azure ATP e sensores do Azure ATP 

-   O monitor detectou atividades suspeitas com base em algoritmos comportamentais de machine learning para detectar comportamento anormal e algoritmos determinísticos para detectar ataques avançados com base na cadeia de invasão do ataque

-   Opcional: o portal de gerenciamento de espaço de trabalho pode ser configurado para enviar emails e eventos quando atividades suspeitas ou eventos de integridade forem detectados.


|||
|-|-|
|Receptor de Entidade|Recebe lotes de entidades de todos os sensores do Azure ATP e sensores autônomos do Azure ATP.|
|Processador de atividade de rede|Processa todas as atividades de rede em cada lote recebido. Por exemplo, a correspondência entre as diversas etapas do Kerberos executadas em computadores potencialmente diferentes|
|Criador de perfil de entidade|Cria o perfil de todas as entidades exclusivas de acordo com o tráfego e os eventos. Por exemplo, o Azure ATP atualiza a lista de computadores conectados para cada perfil do usuário.|
|Portal de gerenciamento de espaço de trabalho do Azure ATP|Gerencia seus espaços de trabalho do Azure ATP.|
|Portal de espaço de trabalho do Azure ATP|O espaço de trabalho do Azure ATP é usado para configurar o Azure ATP e monitorar atividades suspeitas detectadas pelo Azure ATP em sua rede. O espaço de trabalho do Azure ATP não é dependente do sensor do Azure ATP e é executado mesmo quando o serviço do sensor do Azure ATP está parado. |
|Detectores|Os detectores usam algoritmos de aprendizado de máquina e regras determinísticas para localizar atividades suspeitas e comportamento anormal do usuário em sua rede.|

Considere os seguintes critérios ao decidir quantos espaços de trabalho do Azure ATP você quer implantar em sua rede:

-   Um espaço de trabalho do Azure ATP pode monitorar uma única floresta do Active Directory. Se você tiver mais de uma floresta do Active Directory, será necessário pelo menos um serviço de nuvem do Azure ATP por floresta do Active Directory.


## <a name="azure-atp-sensor-and-azure-atp-standalone-sensor"></a>Sensor do Azure ATP e sensor autônomo do Azure ATP

O **sensor do Azure ATP** e o **sensor autônomo do Azure ATP** autônomo têm a mesma funcionalidade básica:

-   Capturar e inspecionar o tráfego de rede do controlador de domínio. Este tráfego é espelhado da porta para sensores autônomos do Azure ATP e o tráfego local do controlador de domínio em sensores do Azure ATP. 

-   Receber eventos do Windows diretamente dos controladores de domínio (para sensores do ATP) ou de servidores de SIEM ou Syslog (para sensores autônomos do ATP)

-  Receber informações de contabilidade RADIUS de seu provedor de VPN

-   Recuperar dados sobre usuários e computadores do domínio do Active Directory

-   Executar a resolução de entidades de rede (usuários, grupos e computadores)

-   Transferir dados relevantes para o serviço de nuvem do Azure ATP

-   Monitorar vários controladores de domínio de um único sensor autônomo do Azure ATP ou monitorar um único controlador de domínio para um sensor do Azure ATP.

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

-   O sensor do Azure ATP pode ler eventos localmente, sem a necessidade de configurar o encaminhamento de eventos.

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
Para trabalhar com Azure ATP, verifique se os seguintes componentes estão configurados.

### <a name="port-mirroring"></a>Espelhamento de porta
Se você estiver usando sensores autônomos do Azure ATP, precisará configurar o espelhamento de porta para os controladores de domínio que serão monitorados e definir o sensor autônomo do Azure ATP como o destino usando os comutadores físicos ou virtuais. Outra opção é usar TAPs de rede. O Azure ATP funcionará se alguns e não todos, controladores de domínio forem monitorados, mas a detecção é menos eficiente.

Enquanto o espelhamento de portas espelha todo o tráfego de rede do controlador de domínio para o sensor autônomo do Azure ATP, apenas um pequeno percentual desse tráfego é compactada e enviada para o serviço de nuvem do Azure ATP para análise.

Seus controladores de domínio e o sensor autônomo do Azure ATP podem ser físicos ou virtuais. Para saber mais, confira [Configurar o espelhamento de porta](configure-port-mirroring.md).


### <a name="events"></a>Eventos
Para aprimorar a detecção do Azure ATP de Pass-the-Hash, força bruta, modificação de grupos confidenciais, criação de serviços suspeitos e modificações de Honey Tokens, o Azure ATP precisa dos seguintes eventos do Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757 e 7045. Eles podem ser lidos automaticamente pelo sensor do Azure ATP ou, caso o sensor do Azure ATP não esteja implantado, ele poderá ser encaminhado para o sensor autônomo do Azure ATP de duas maneiras: configurando o sensor autônomo do Azure ATP para escutar eventos do SIEM ou [Configurando o Encaminhamento de Eventos do Windows](configure-event-forwarding.md).

-   Configuração do sensor autônomo do Azure ATP para escutar eventos de SIEM <br>Configure o SIEM para encaminhar eventos específicos do Windows para o ATP. O Azure ATP dá suporte a vários fornecedores SIEM. Para obter mais informações, confira [Configurar encaminhamento de eventos](configure-event-forwarding.md).

-   Configuração do encaminhamento de eventos do Windows<br>Outra maneira do Azure ATP conseguir obter seus eventos é configurando seus controladores de domínio para encaminhar eventos do Windows 4776, 4732, 4733, 4728, 4729, 4756, 4757 e 7045 para seu sensor autônomo do Azure ATP. Isso é especialmente útil se você não tiver um SIEM ou se o SIEM não tiver suporte atualmente do ATP. Para obter mais informações sobre o Encaminhamento de Eventos do Windows no ATP, confira [Configurando o encaminhamento de eventos do Windows](configure-event-forwarding.md). Isso se aplica somente aos sensores autônomos físicos do Azure ATP – não ao sensor do Azure ATP.


## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/trisizingtool)
- [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md)
- [Configurar o encaminhamento de eventos](configure-event-forwarding.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md)

- - [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)
