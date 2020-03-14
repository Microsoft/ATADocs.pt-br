---
title: Arquitetura do Advanced Threat Analytics | Microsoft Docs
description: Descreve a arquitetura da Advanced Threat Analytics (ATA)
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 09/08/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 892b16d2-58a6-49f9-8693-1e5f69d8299c
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 179cf31a6f9c8c62670ea96d671f209712325f56
ms.sourcegitcommit: 05f23a0add8d24ae92176e13c2a4ae8ada1844da
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79319199"
---
# <a name="ata-architecture"></a>Arquitetura do ATA

*Aplica-se a: Advanced Threat Analytics versão 1.9*

A arquitetura da Advanced Threat Analytics é detalhada neste diagrama:

![Diagrama de topologia da arquitetura do ATA](media/ATA-architecture-topology.jpg)

O ATA monitora o tráfego de rede do controlador de domínio utilizando o espelhamento de porta para um Gateway do ATA usando comutadores físicos ou virtuais. Se você implantar o Gateway Lightweight do ATA diretamente em seus controladores de domínio, ele eliminará a necessidade de espelhamento de porta. Além disso, o ATA pode aproveitar os eventos do Windows (encaminhados diretamente de seus controladores de domínio ou de um servidor SIEM) e analisar os dados em relação a ataques e ameaças.
Esta seção descreve o fluxo de rede e a captura de eventos e descreve detalhadamente a funcionalidade dos componentes principais do ATA: o Gateway do ATA, o Gateway Lightweight do ATA (que tem a mesma funcionalidade básica do Gateway do ATA) e o Centro do ATA.


![Diagrama de fluxo de tráfego de ATA](media/ATA-traffic-flow.jpg)

## <a name="ata-components"></a>Componentes de ATA
O ATA é formado pelos seguintes componentes:

-   **Centro do ATA** <br>
A Central do ATA receberá dados de qualquer Gateway do ATA e/ou Gateway Lightweight do ATA que você implantar.
-   **Gateway do ATA**<br>
O Gateway do ATA está instalado em um servidor dedicado que monitora o tráfego de seus controladores de domínio usando o espelhamento de porta ou uma TAP de rede.
-   **Gateway Lightweight do ATA**<br>
O Gateway Lightweight do ATA está instalado diretamente em seus controladores de domínio e monitora o tráfego diretamente, sem a necessidade de uma configuração de espelhamento de porta ou um servidor dedicado. É uma alternativa ao Gateway do ATA.

Uma implantação do ATA pode consistir em uma único Centro do ATA conectado a todos os Gateways do ATA, a todos os Gateways Lightweight do ATA ou a uma combinação de Gateways do ATA e Gateways Lightweight do ATA.


## <a name="deployment-options"></a>Opções de implantação
Você pode implantar o ATA usando a seguinte combinação de gateways:

-   **Usando somente os Gateways do ATA** <br>
Sua implantação do ATA pode conter apenas Gateways do ATA, sem os Gateways Lightweight do ATA: todos os controladores de domínio devem ser configurados para habilitar o espelhamento de porta para um Gateway do ATA ou TAPs de rede devem estar em funcionamento.
-   **Usando somente Gateways Lightweight do ATA**<br>
Sua implantação do ATA pode conter somente Gateways Lightweight do ATA: eles são implantados em cada controlador de domínio e não há a necessidade de servidores adicionais ou de configuração de espelhamento de porta.
-   **Usando tanto Gateways do ATA quanto Gateways Lightweight do ATA**<br>
Sua implantação do ATA inclui Gateways do ATA e Gateways Lightweight do ATA. Os Gateways Lightweight do ATA são instalados em alguns de seus controladores de domínio (por exemplo, todos os controladores de domínio em seus sites de branch). Ao mesmo tempo, outros controladores de domínio são monitorados pelos Gateways do ATA (por exemplo, os maiores controladores de domínio em seus data centers principais).

Em todos os três cenários, todos os gateways enviam seus dados para o Centro do ATA.


## <a name="ata-center"></a>Centro de ATA
O **Centro de ATA** executa as seguintes funções:

-   Gerencia as definições de configuração de Gateway do ATA e de Gateway Lightweight do ATA

-   Recebe dados de Gateways do ATA e de Gateways Lightweight do ATA 

-   Detecta atividades suspeitas

-   Executa algoritmos de aprendizado de máquina comportamental do ATA para detectar comportamentos anômalos

-   Executa vários algoritmos determinísticos para detectar ataques avançados com base na cadeia de eliminação de ataque

-   Executa o Console do ATA.

-   Opcional: o Centro de ATA pode ser configurado para enviar emails e eventos quando uma atividade suspeita é detectada.

O Centro do ATA recebe tráfego analisado do Gateway do ATA e do Gateway Lightweight do ATA. Ele realiza então a criação de perfil, executa detecção determinística e executa algoritmos comportamentais e de aprendizado de máquina para conhecer sua rede, permitindo a detecção de anomalias e avisando sobre atividades suspeitas.

|||
|-|-|
|Receptor de Entidade|Recebe lotes de entidades de todos os Gateways do ATA e Gateways Lightweight do ATA.|
|Processador de atividade de rede|Processa todas as atividades de rede em cada lote recebido. Por exemplo, a correspondência entre as diversas etapas do Kerberos executadas em computadores potencialmente diferentes|
|Criador de perfil de entidade|Cria o perfil de todas as entidades exclusivas de acordo com o tráfego e os eventos. Por exemplo, o ATA atualiza a lista de computadores conectados para cada perfil do usuário.|
|Banco de dados central|Gerencia o processo de gravação de atividades de rede e os eventos no banco de dados. |
|Banco de dados|O ATA utiliza o MongoDB para armazenar todos os dados no sistema:<br /><br />-   Atividade de rede<br />-   Atividades evento<br />-   Entidades exclusivas<br />-   Atividades suspeitas<br />-   Configuração do ATA|
|Detectores|Os detectores usam algoritmos de aprendizado de máquina e regras determinísticas para localizar atividades suspeitas e comportamento anormal do usuário em sua rede.|
|Console do ATA|O Console do ATA é para configurar o ATA e monitorar atividades suspeitas detectadas pelo ATA em sua rede. O Console do ATA não é dependente do serviço do Centro do ATA e é executado mesmo quando o serviço é interrompido, contanto que ele possa se comunicar com o banco de dados.|

Considere os seguintes critérios ao decidir quantos Centros do ATA você quer implantar em sua rede:

-   Um Centro de ATA pode monitorar uma única floresta do Active Directory. Se você tiver mais de uma floresta do Active Directory, será necessário pelo menos um Centro do ATA por floresta do Active Directory.

-    Em grandes implantações do Active Directory, um único Centro de ATA pode não ser capaz de lidar com todo o tráfego de todos os controladores de domínio. Nesse caso, serão necessários vários Centros do ATA. O número de Centros de ATA devem ser determinados pelo [planejamento de capacidade de ATA](ata-capacity-planning.md).

## <a name="ata-gateway-and-ata-lightweight-gateway"></a>Gateway do ATA e Gateway Lightweight do ATA

### <a name="gateway-core-functionality"></a>Funcionalidade básica do gateway
O **Gateway do ATA** e o **Gateway Lightweight do ATA** têm a mesma funcionalidade básica:

-   Capturar e inspecionar o tráfego de rede do controlador de domínio. Este é o tráfego espelhado da porta para Gateways do ATA e tráfego local do controlador de domínio em Gateways Lightweight do ATA. 

-   Receber eventos do Windows de servidores SIEM ou Syslog ou de controladores de domínio usando o Encaminhamento de eventos do Windows

-   Recuperar dados sobre usuários e computadores do domínio do Active Directory

-   Executar a resolução de entidades de rede (usuários, grupos e computadores)

-   Transferir os dados relevantes para o Centro do ATA

-   Monitorar vários controladores de domínio de um único Gateway do ATA ou monitorar um único controlador de domínio para um Gateway Lightweight do ATA.

O Gateway do ATA recebe o tráfego de rede espelhado e os eventos do Windows da sua rede e processa-os nos seguintes componentes principais:

|||
|-|-|
|Ouvinte de Rede|O Ouvinte de Rede captura o tráfego de rede e o analisa. Essa é uma tarefa de CPU intensa, portanto, é muito importante verificar os [Pré-requisitos do ATA](ata-prerequisites.md) ao planejar seu Gateway do ATA ou Gateway Lightweight do ATA.|
|Ouvinte de Evento|O Ouvinte de Eventos captura e analisa Eventos do Windows encaminhados de um servidor SIEM na sua rede.|
|Leitor de Log de Eventos do Windows|O Leitor de Log de Eventos do Windows lê e analisa Eventos do Windows encaminhados ao Log de Eventos do Windows do Gateway do ATA nos controladores de domínio.|
|Conversor de Atividade de Rede | Converte o tráfego analisado em uma representação lógica do tráfego usado pelo ATA (NetworkActivity).
|Resolvedor de Entidade|O Resolvedor de Entidade utiliza os dados analisados (tráfego de rede e eventos) e resolve os dados com o Active Directory para localizar informações de conta e identidade. Em seguida, ele é correspondido com os endereços IP encontrados nos dados analisados. O Resolvedor de Entidade inspeciona os cabeçalhos de pacote com eficiência, permite analisar pacotes de autenticação para nomes, propriedades e identidades de computadores. O Resolvedor de Entidade combina os pacotes de autenticação analisado com os dados no pacote real.|
|Remetente de Entidade|O Remetente de Entidade envia os dados analisados e correspondentes para o Centro do ATA.|

## <a name="ata-lightweight-gateway-features"></a>Recursos do Gateway Lightweight do ATA

Os recursos a seguir funcionam de modo diferente dependendo de você estar executando um Gateway do ATA ou um Gateway Lightweight do ATA.

-   O Gateway Lightweight do ATA pode ler eventos localmente, sem a necessidade de configurar o encaminhamento de eventos.

-   **Candidato ao sincronizador de domínio**<br>
O gateway sincronizador de domínio é responsável por sincronizar todas as entidades de um determinado domínio do Active Directory de forma proativa (semelhante ao mecanismo utilizado pelos próprios controladores de domínio para replicação). Um gateway é escolhido aleatoriamente, na lista de candidatos, para servir como sincronizador de domínio. <br><br>
Se o sincronizador estiver offline por mais de 30 minutos, outro candidato é escolhido em seu lugar. Se não houver nenhum candidato do sincronizador de domínio disponível para um domínio específico, o ATA sincronizará as entidades e suas alterações proativamente. no entanto, o ATA recuperará novas entidades reativamente conforme elas forem detectadas no tráfego monitorado. 
<br>Quando nenhum sincronizador de domínio está disponível, a pesquisa de uma entidade sem tráfego relacionado a ela não exibe nenhum resultado.<br><br>
Por padrão, todos os gateways do ATA são candidatos ao sincronizador de domínio.<br><br>
Como todos os Gateways Lightweight do ATA têm maior probabilidade de serem implantados em filiais e em pequenos controladores de domínio, eles não são candidatos a sincronizador por padrão. <br><br>Em um ambiente com apenas gateways leves, é recomendável atribuir dois dos gateways como candidatos do sincronizador, em que um gateway Lightweight é o candidato do sincronizador padrão e um é o backup, caso o padrão esteja offline por mais de 30 alguns. 


-   **Limitações de recursos**<br>
O Gateway Lightweight do ATA inclui um componente de monitoramento que avalia a capacidade de computação e de memória disponível no controlador de domínio no qual ele está sendo executado. O processo de monitoramento é executado a cada 10 segundos e atualiza dinamicamente a cota de utilização de CPU e memória no processo de Gateway Lightweight do ATA para garantir que a qualquer hora o controlador de domínio tenha pelo menos 15% de recursos de computação e memória livres.<br><br>
Não importa o que acontece no controlador de domínio, esse processo sempre libera os recursos para fazer com que a funcionalidade principal do controlador de domínio não seja afetada.<br><br>
Se isso faz com que o Gateway Lightweight do ATA fique sem recursos, apenas o tráfego parcial é monitorado e o alerta de monitoramento "Tráfego de rede espelhado na porta descartado" é exibido na página Integridade.

A tabela abaixo fornece um exemplo de um controlador de domínio com recurso de computação suficiente disponível para permitir uma cota maior de recursos de computação necessária no momento, de forma que todo o tráfego é monitorado:

||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Gateway Lightweight do ATA (Microsoft.Tri.Gateway.exe)|Diversos (outros processos) |Cota do Gateway Lightweight do ATA|Descarte de gateway|
|30%|20%|10%|45%|Não|

Se o Active Directory precisa de mais de computação, a cota necessária do Gateway Lightweight do ATA é reduzida. No exemplo a seguir, o Gateway Lightweight do ATA precisa de mais do que a cota alocada e descarta parte do tráfego (monitorando apenas o tráfego parcial):

||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Gateway Lightweight do ATA (Microsoft.Tri.Gateway.exe)|Diversos (outros processos) |Cota do Gateway Lightweight do ATA|O gateway está descartando|
|60%|15%|10%|15%|Sim|


## <a name="your-network-components"></a>Componentes da sua rede
Para trabalhar com ATA, verifique se os seguintes componentes estão configurados.

### <a name="port-mirroring"></a>Espelhamento de porta
Se você estiver usando Gateways do ATA, precisará configurar o espelhamento de porta para os controladores de domínio que serão monitorados e definir o Gateway do ATA como o destino usando os comutadores físicos ou virtuais. Outra opção é usar TAPs de rede. O ATA funcionará se alguns, e não todos, controladores de domínio forem monitorados, mas a detecção é menos eficiente.

Enquanto o espelhamento de portas espelha todo o tráfego de rede do controlador de domínio para o Gateway do ATA, apenas uma pequena porcentagem desse tráfego é compactada e enviada para o Centro do ATA para análise.

Os controladores de domínio e os Gateways de ATA podem ser físicos ou virtuais, consulte [Configurar o espelhamento de porta](configure-port-mirroring.md) para obter mais informações.


### <a name="events"></a>Eventos
Para melhorar a detecção do ATA de Pass-the-Hash, Força Bruta, Modificação para grupos confidenciais e Honey Tokens, o ATA precisa dos seguintes eventos do Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757. Eles podem ser lidos automaticamente pelo Gateway Lightweight do ATA ou no caso de o Gateway Lightweight do ATA não estar implantado, podem ser encaminhados para o Gateway do ATA de duas maneiras: configurando o Gateway do ATA para escutar o SIEM ou [Configurando o Encaminhamento de Eventos do Windows](configure-event-collection.md).

-   Configuração do Gateway de ATA para escutar eventos SIEM <br>Configure o SIEM para encaminhar eventos específicos do Windows para o ATA. O ATA oferece suporte a vários fornecedores SIEM. Para obter mais informações, confira [Configurar coleta de eventos](configure-event-collection.md).

-   Configuração do encaminhamento de eventos do Windows<br>Outra maneira de o ATA conseguir obter seus eventos é configurando seus controladores de domínio para encaminhar eventos do Windows 4776, 4732, 4733, 4728, 4729, 4756 and 4757 para seu Gateway do ATA. Isso é especialmente útil se você não tiver um SIEM ou se o SIEM não for atualmente suportado pelo ATA. Para completar a configuração do Encaminhamento de Eventos do Windows no ATA, confira [Configurando o encaminhamento de eventos do Windows](configure-event-collection.md). Isso se aplica apenas a Gateways do ATA físicos, não ao Gateway Lightweight do ATA.

## <a name="related-videos"></a>Vídeos relacionados
- [Como escolher o tipo certo de Gateway do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Confira Também
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Ferramenta de dimensionamento do ATA](https://aka.ms/atasizingtool)
- [Planejamento da capacidade do ATA](ata-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-collection.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

