---
title: Arquitetura de ATA | Microsoft Advanced Threat Analytics
description: Descreve a arquitetura da Advanced Threat Analytics (ATA)
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 892b16d2-58a6-49f9-8693-1e5f69d8299c
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 2d753060f30cbcc7d16959355b86d64fdaa2ecd8


---

# Arquitetura do ATA
A arquitetura da Advanced Threat Analytics é detalhada neste diagrama:

![Diagrama de topologia da arquitetura de ATA](media/ATA-architecture-topology.jpg)

O ATA monitora o tráfego de rede do controlador de domínio utilizando o espelhamento de porta para um Gateway do ATA que use comutadores físicos ou virtuais ou implantando o Gateway Lightweight do ATA diretamente em seus controladores de domínio, o que acaba com o requisito de espelhamento de porta. Além disso, o ATA pode aproveitar os eventos do Windows (encaminhados diretamente de seus controladores de domínio ou de um servidor SIEM) e analisar os dados em relação a ataques e ameaças.
Esta seção descreve o fluxo de rede e a captura de evento e descreve detalhadamente a funcionalidade dos componentes principais do ATA: o Gateway do ATA, o Gateway Lightweight do ATA (que tem a mesma funcionalidade básica do Gateway do ATA) e o Centro do ATA.


![Diagrama de fluxo de tráfego de ATA](media/ATA-traffic-flow.jpg)

## Componentes de ATA
O ATA consiste no seguinte:

-   **Centro de ATA** <br>
A Central do ATA receberá dados de qualquer Gateway do ATA e/ou Gateway Lightweight do ATA que você implantar.
-   **Gateway do ATA**<br>
O Gateway do ATA está instalado em um servidor dedicado que monitora o tráfego de seus controladores de domínio usando o espelhamento de porta ou uma TAP de rede.
-   **Gateway Lightweight do ATA**<br>
O Gateway Lightweight do ATA está instalado diretamente em seus controladores de domínio e monitora o tráfego diretamente, sem a necessidade de uma configuração de espelhamento de porta ou um servidor dedicado. É uma alternativa ao Gateway do ATA.

Uma implantação do ATA pode consistir em uma único Centro do ATA conectada a todos os Gateways do ATA, a todos os Gateways Lightweight do ATA ou a uma combinação de Gateways do ATA e Gateways Lightweight do ATA.


## Opções de implantação
Você pode implantar o ATA usando a seguinte combinação de gateways:

-   **Usando somente os Gateways do ATA** <br>
Se sua implantação do ATA contém apenas Gateways do ATA, sem os Gateways Lightweight do ATA, todos os controladores de domínio devem ser configurados para habilitar o espelhamento de porta para um Gateway do ATA ou uma TAP de rede deve estar em funcionamento.
-   **Usando somente Gateways Lightweight do ATA**<br>
Se sua implantação do ATA contém somente Gateways Lightweight do ATA, estes são implantados em cada controlador de domínio e não há a necessidade de servidores adicionais ou de configuração de espelhamento de porta.
-   **Usando tanto Gateways do ATA quanto Gateways Lightweight do ATA**<br>
Se sua implantação do ATA inclui Gateways do ATA e Gateways Lightweight do ATA, e o Gateway Lightweight do ATA está instalado em alguns de seus controladores de domínio (por exemplo, todos os controladores de domínio em seus sites de filial) ao passo que outros controladores de domínio são monitorados pelos Gateways do ATA (por exemplo, os maior controladores de domínio em seus data centers principais).

Em todos os três cenários, todos os gateways enviam seus dados para o Centro do ATA.




## Centro de ATA
O **Centro de ATA** executa as seguintes funções:

-   Gerencia as definições de configuração de Gateway do ATA e de Gateway Lightweight do ATA

-   Recebe dados de Gateways do ATA e de Gateways Lightweight do ATA 

-   Detecta atividades suspeitas

-   Executa algoritmos de aprendizado de máquina comportamental do ATA para detectar comportamentos anômalos

-   Executa vários algoritmos determinísticos para detectar ataques avançados com base na cadeia de eliminação de ataque

-   Executa o Console do ATA.

-   Opcional: o Centro de ATA pode ser configurado para enviar emails e eventos quando uma atividade suspeita é detectada.

A Central do ATA recebe tráfego analisado do Gateway do ATA e do Gateway Lightweight do ATA, realiza a criação de perfil, executa detecção determinística e executa algoritmos comportamentais e de aprendizado de máquina para conhecer sua rede, permitindo a detecção de anomalias e avisando sobre atividades suspeitas.

|||
|-|-|
|Receptor de Entidade|Recebe lotes de entidades de todos os Gateways do ATA e Gateways Lightweight do ATA.|
|Processador de atividade de rede|Processa todas as atividades de rede em cada lote recebido. Por exemplo, a correspondência entre as diversas etapas do Kerberos executadas em computadores potencialmente diferentes|
|Criador de perfil de entidade|Cria o perfil de todas as entidades exclusivas de acordo com o tráfego e os eventos. Por exemplo, este é o local onde o ATA atualiza a lista de computadores logados para cada perfil de usuário.|
|Banco de dados central|Gerencia o processo de gravação de atividades de rede e os eventos no banco de dados. |
|Banco de dados|O ATA utiliza o MongoDB para armazenar todos os dados no sistema:<br /><br />-   Atividade de rede<br />-   Atividades evento<br />-   Entidades exclusivas<br />-   Atividades suspeitas<br />-   Configuração do ATA|
|Detectores|Os detectores usam algoritmos de aprendizado de máquina e regras determinísticas para localizar atividades suspeitas e comportamento anormal do usuário em sua rede.|
|Console do ATA|O Console do ATA é para configurar o ATA e monitorar atividades suspeitas detectadas pelo ATA em sua rede. O Console do ATA não é dependente do serviço do Centro de ATA e será executado mesmo quando o serviço for interrompido, desde que ele possa se comunicar com o banco de dados.|
Considere o seguinte ao decidir quantos Centros de ATA você quer implantar em sua rede:

-   Um Centro de ATA pode monitorar uma única floresta do Active Directory. Se você tiver mais de uma floresta do Active Directory, será necessário pelo menos um Centro de ATA por floresta do Active Directory.

-    Em implantações do Active Directory muito grandes, uma único Centro do ATA pode não ser capaz de lidar com todo o tráfego de todos os controladores de domínio. Nesse caso, serão necessárias várias Centrais do ATA. O número de Centrais do ATA deve ser determinado pelo [planejamento de capacidade do ATA](ata-capacity-planning.md).

## Gateway do ATA e Gateway Lightweight do ATA

### Funcionalidade básica do gateway
O **Gateway do ATA** e o **Gateway Lightweight do ATA** têm a mesma funcionalidade básica:

-   Capturar e inspecionar o tráfego de rede do controlador de domínio (tráfego de porta espelhada no caso de um Gateway do ATA e tráfego local do controlador de domínio no caso de um Gateway Lightweight do ATA) 

-   Receber eventos do Windows de servidores SIEM ou Syslog ou de controladores de domínio usando o Encaminhamento de eventos do Windows

-   Recuperar dados sobre usuários e computadores do domínio do Active Directory

-   Executar a resolução de entidades de rede (usuários, grupos e computadores)

-   Transferir os dados relevantes para o Centro do ATA

-   Monitorar vários controladores de domínio de um único Gateway do ATA ou monitorar um único controlador de domínio para um Gateway Lightweight do ATA.

O Gateway do ATA recebe o tráfego de rede espelhado e os eventos do Windows da sua rede e processa-os nos seguintes componentes principais:

|||
|-|-|
|Ouvinte de Rede|O Ouvinte de Rede é responsável por capturar o tráfego de rede e analisar o tráfego. Essa é uma tarefa de CPU intensa, portanto, é muito importante verificar os [Pré-requisitos do ATA](ata-prerequisites.md) ao planejar seu Gateway do ATA ou Gateway Lightweight do ATA.|
|Ouvinte de Evento|O Ouvinte de Eventos é responsável por capturar e analisar eventos do Windows encaminhados de um servidor SIEM na sua rede.|
|Leitor de Log de Eventos do Windows|O Leitor de Log de Eventos do Windows é responsável por ler e analisar eventos do Windows encaminhados ao log de eventos do Windows do Gateway de ATA a partir dos controladores de domínio.|
|Conversor de Atividade de Rede | Converte o tráfego analisado em uma representação lógica do tráfego usado pelo ATA (NetworkActivity).
|Resolvedor de Entidade|O Resolvedor de Entidade utiliza os dados analisados (tráfego de rede e eventos) e resolve os dados com o Active Directory para localizar informações de conta e identidade. Em seguida, ele é correspondido com os endereços IP encontrados nos dados analisados. O Resolvedor de Entidade inspeciona os cabeçalhos de pacote com eficiência, permite analisar pacotes de autenticação para nomes, propriedades e identidades de computadores. O Resolvedor de Entidade combina os pacotes de autenticação analisado com os dados no pacote real.|
|Remetente de Entidade|O Remetente de Entidade é responsável por enviar os dados analisados e correspondentes para o Centro de ATA.|

## Recursos do Gateway Lightweight do ATA

Os recursos a seguir funcionam de modo diferente dependendo de você estar executando um Gateway do ATA ou um Gateway Lightweight do ATA.

-   **Candidato ao sincronizador de domínio**<br>
O gateway sincronizador de domínio é responsável por sincronizar todas as entidades de um determinado domínio do Active Directory de forma proativa (semelhante ao mecanismo utilizado pelos próprios controladores de domínio para replicação). Um gateway é escolhido aleatoriamente, na lista de candidatos, para servir como sincronizador de domínio. <br><br>
Se o sincronizador estiver offline por mais de 30 minutos, outro candidato é escolhido em seu lugar. Se não houver nenhum sincronizador de domínio disponível para um domínio específico, o ATA não poderá sincronizar entidades e suas alterações proativamente. No entanto, o ATA recuperará novas entidades reativamente conforme elas forem detectadas no tráfego monitorado. 
<br>Se nenhum sincronizador de domínio estiver disponível e você pesquisar por uma entidade que não tem qualquer tráfego relacionado a ela, nenhum resultado será exibido.<br><br>
Por padrão, todos os Gateways do ATA são candidatos a sincronizador.<br><br>
Como todos os Gateways Lightweight do ATA têm maior probabilidade de serem implantados em filiais e em pequenos controladores de domínio, eles não são candidatos a sincronizador por padrão.


-   **Limitações de recursos**<br>
O Gateway Lightweight do ATA inclui um componente de monitoramento que avalia a capacidade de computação e de memória disponível no controlador de domínio no qual ele está sendo executado. O processo de monitoramento é executado a cada 10 segundos e atualiza dinamicamente a cota de utilização de CPU e memória no processo de Gateway Lightweight do ATA para garantir que a qualquer hora o controlador de domínio tenha pelo menos 15% de recursos de computação e memória livres.<br><br>
Não importa o que acontece no controlador de domínio, esse processo sempre libera os recursos para fazer com que a funcionalidade principal do controlador de domínio não seja afetada.<br><br>
Se isso faz com que o Gateway Lightweight do ATA fique sem recursos, apenas o tráfego parcial é monitorado e o alerta de monitoramento "Tráfego de rede espelhado na porta descartado" será exibido na página Integridade.

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



## Componentes da sua rede
Para trabalhar com o ATA, verifique o seguinte:

### Espelhamento de porta
Se você estiver usando Gateways do ATA, precisará configurar o espelhamento de porta para os controladores de domínio que serão monitorados e definir o Gateway do ATA como o destino usando os comutadores físicos ou virtuais. Outra opção é usar TAPs de rede. O ATA funcionará se alguns, e não todos, controladores de domínio forem monitorados, mas detecção será menos eficiente.

Enquanto o espelhamento de portas espelha todo o tráfego de rede do controlador de domínio para o Gateway do ATA, apenas uma porcentagem muito pequena desse tráfego é compactada e enviada para o Centro do ATA para análise.

Os controladores de domínio e os Gateways do ATA podem ser físicos ou virtuais, consulte [Configurar o espelhamento de porta](/advanced-threat-analytics/deploy-use/configure-port-mirroring) para obter mais informações.


### Eventos
Para melhorar a detecção de passagem de hash, força bruta e Honey Tokens, o ATA precisa do log de eventos do Windows ID 4776. Isso pode ser encaminhado para o Gateway de ATA usando de uma entre duas maneiras, configurando o Gateway de ATA para escutar eventos SIEM ou usando o encaminhamento de eventos do Windows.

-   Configuração do Gateway de ATA para escutar eventos SIEM <br>Configure o SIEM para encaminhar eventos específicos do Windows para o ATA. O ATA oferece suporte a vários fornecedores SIEM. Para obter mais informações, confira [Configurar coleta de eventos](/advanced-threat-analytics/deploy-use/configure-event-collection).

-   Configuração do encaminhamento de eventos do Windows<br>Outra maneira de o ATA conseguir obter seus eventos é configurando seus controladores de domínio para encaminhar eventos do Windows 4776 para o Gateway de ATA. Isso é especialmente útil se você não tiver um SIEM ou se o SIEM não for atualmente suportado pelo ATA. Para obter mais informações sobre o Encaminhamento de Eventos do Windows no ATA, confira [Configurando o encaminhamento de eventos do Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding).

## Consulte também
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Planejamento da capacidade de ATA](ata-capacity-planning.md)
- [Configurar coleta de eventos](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configuração do encaminhamento de eventos do Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Jun16_HO4-->


