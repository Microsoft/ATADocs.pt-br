---
# required metadata

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

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Arquitetura do ATA
A arquitetura da Advanced Threat Analytics é detalhada neste diagrama:

![Diagrama de topologia da arquitetura de ATA](media/ATA-architecture-topology.jpg)

O ATA é formada por dois componentes: o Gateway de ATA e o Centro de ATA.

Eles se conectam à sua rede existente espelhando o tráfego de rede de e para os controladores de domínio e examinando os eventos do Windows (encaminhados diretamente dos controladores de domínio ou de um servidor SIEM) e analisando os dados de ataques e ameaças.

Esta seção descreve o fluxo de rede e de captura de evento, fazendo uma busca detalhada nos principais componentes do Gateway de ATA, do Centro de ATA e de suas funcionalidades.

![Diagrama de fluxo de tráfego de ATA](media/ATA-traffic-flow.jpg)

## Componentes de ATA
O ATA consiste no seguinte:

-   Um ou mais Gateways de ATA

-   Um Centro de ATA:

## Gateway de ATA
O **Gateway de ATA** executa as seguintes funções:

-   Captura e inspeciona o tráfego de rede do controlador de domínio por meio de espelhamento de porta

-   Recebe eventos do Windows a partir de servidores SIEM ou Syslog ou de controladores de domínio usando o encaminhamento de eventos do Windows

-   Recupera dados sobre usuários e computadores do domínio do Active Directory

-   Executa a resolução de entidades de rede (usuários, grupos e computadores)

-   Transfere os dados relevantes para o Centro de ATA

-   Monitora vários controladores de domínio de um único Gateway de ATA

O Gateway de ATA recebe o tráfego de rede espelhado e os eventos do Windows da sua rede e processa-os nos seguintes componentes principais:

|||
|-|-|
|Ouvinte de Rede|O Ouvinte de Rede é responsável por capturar o tráfego de rede e analisar o tráfego. Essa é uma tarefa de CPU intensa, portanto, é muito importante verificar os [Pré-requisitos de ATA](/advanced-threat-analytics/PlanDesign/ata-prerequisites) ao planejar seu Gateway de ATA.|
|Ouvinte de Evento|O Ouvinte de Eventos é responsável por capturar e analisar eventos do Windows encaminhados de um servidor SIEM na sua rede.|
|Leitor de Log de Eventos do Windows|O Leitor de Log de Eventos do Windows é responsável por ler e analisar eventos do Windows encaminhados ao log de eventos do Windows do Gateway de ATA a partir dos controladores de domínio.|
|Conversor de Atividade de Rede | Converte o tráfego analisado na representação lógica do tráfego de ATA (NetworkActivity).
|Resolvedor de Entidade|O Resolvedor de Entidade utiliza os dados analisados (tráfego de rede e eventos) e resolve os dados com o Active Directory para localizar informações de conta e identidade, criando uma correspondência com os endereços IP encontrados nos dados analisados.  Além disso, o Resolvedor de Entidade inspeciona os cabeçalhos de pacote com eficiência, permite analisar pacotes de autenticação para nomes, propriedades e identidades de computadores e combina tudo isso com os dados no pacote real.|
|Remetente de Entidade|O Remetente de Entidade é responsável por enviar os dados analisados e correspondentes para o Centro de ATA.|
Considere o seguinte ao decidir quantos Gateways de ATA você quer implantar em sua rede:

-   Florestas e domínios do Active Directory

    Os Gateways de ATA podem monitorar o tráfego de vários domínios de uma única floresta do Active Directory.   O monitoramento de várias florestas do Active Directory requer implantações de ATA separadas. Os Gateways de ATA não devem ser configurados para monitorar o tráfego de rede de controladores de domínio em florestas diferentes.

-   Espelhamento de porta

    Considerações sobre o espelhamento de porta provavelmente exigirão que você implante pelo menos um Gateway de ATA por data center / área geográfica

-   Capacidade

    Cada Gateway de ATA pode analisar e enviar uma determinada quantidade de tráfego por segundo. Se os controladores de domínio que você está monitorando estão enviando e recebendo mais tráfego do que o Gateway de ATA consegue suportar, você precisará adicionar Gateways de ATA adicionais de acordo com o volume de tráfego. Para mais informações, confira [Planejamento de capacidade do ATA](/advanced-threat-analytics/PlanDesign/ata-capacity-planning).

## Centro de ATA
O **Centro de ATA** executa as seguintes funções:

-   Gerencia as definições de configuração do Gateway de ATA

-   Recebe dados de Gateways de ATA

-   Detecta atividades suspeitas

-   Executa diversos mecanismos de aprendizado de máquina comportamentais

-   Executa o Console do ATA.

-   Opcional: o Centro de ATA pode ser configurado para enviar emails e eventos quando uma atividade suspeita é detectada.

O Centro de ATA recebe tráfego analisado do Gateway de ATA, realiza a criação de perfil, executa detecção determinística e executa algoritmos comportamentais e de aprendizado de máquina para conhecer sua rede, permitindo a detecção de anomalias e avisando sobre atividades suspeitas.

|||
|-|-|
|Receptor de Entidade|Recebe lotes de entidades de todos os Gateways de ATA.|
|Processador de atividade de rede|Processa todas as atividades de rede em cada lote recebido. Por exemplo, a correspondência entre as diversas etapas do Kerberos executadas em computadores potencialmente diferentes|
|Criador de perfil de entidade|Cria o perfil de todas as entidades exclusivas de acordo com o tráfego e os eventos. Por exemplo, este é o local onde o ATA atualiza a lista de computadores logados para cada perfil de usuário.|
|Cliente de banco de dados do Centro de ATA |Gerencia o processo de gravação de atividades de rede e os eventos no banco de dados. |
|Banco de dados|O ATA utiliza o MongoDB para armazenar todos os dados no sistema:<br /><br />-   Atividade de rede<br />-   Eventos<br />-   Entidades exclusivas<br />-   Atividades suspeitas<br />-   Configuração do ATA|
|Mecanismos de detecção|Os mecanismos de detecção de usam algoritmos de aprendizado de máquina e regras determinísticas para localizar atividades suspeitas e comportamento anormal do usuário em sua rede.|
|Console do ATA|O Console do ATA é para configurar o ATA e monitorar atividades suspeitas detectadas pelo ATA em sua rede. O Console do ATA não é dependente do serviço do Centro de ATA e será executado mesmo quando o serviço for interrompido, desde que ele possa se comunicar com o banco de dados.|
Considere o seguinte ao decidir quantos Centros de ATA você quer implantar em sua rede:

-   Um Centro de ATA pode monitorar uma única floresta do Active Directory. Se você tiver mais de uma floresta do Active Directory, será necessário pelo menos um Centro de ATA por floresta do Active Directory.

    Em grandes implantações do Active Directory, um único Centro de ATA pode não ser capaz de lidar com todo o tráfego de todos os controladores de domínio. Neste caso, serão necessários vários Centros de ATA e as detecções de ATA serão menos eficientes. O número de Centros de ATA devem ser determinados pelo [planejamento de capacidade de ATA](/advanced-threat-analytics/PlanDesign/ata-capacity-planning).

## Componentes da sua rede
Para trabalhar com ATA, você não precisará fazer praticamente nenhuma alteração na rede existente, mas você precisará fazer o seguinte.

### Espelhamento de porta
Para que o ATA funcione, você precisa habilitar o espelhamento de porta para todos os controladores de domínio na floresta do Active Directory que estão sendo monitorados. O ATA funcionará se alguns, mas não todos os controladores de domínio tiverem espelhamento de porta habilitado para ATA, mas detecção será menos eficiente.

Configure o espelhamento de porta de seus controladores de domínio para o Gateway de ATA. Enquanto isto espelha todo o tráfego de rede do controlador de domínio para o Gateway ATA, apenas uma porcentagem muito pequena desse tráfego é compactada e enviada para o Centro de ATA para análise.

Os controladores de domínio e os Gateways de ATA podem ser físicos ou virtuais, consulte [Configurar o espelhamento de porta](/advanced-threat-analytics/PlanDesign/configure-port-mirroring) para obter mais informações.

### Eventos
Para aumentar a detecção do ATA de passagem de Hash, o ATA precisa da ID de log de eventos do Windows 4776. Isso pode ser encaminhado para o Gateway de ATA usando de uma entre duas maneiras, configurando o Gateway de ATA para escutar eventos SIEM ou usando o encaminhamento de eventos do Windows.

-   Configuração do Gateway de ATA para escutar eventos SIEM

    Configure o SIEM para encaminhar eventos específicos do Windows para o ATA. O ATA oferece suporte a vários fornecedores SIEM. Para saber mais, confira [Configurar coleta de eventos](/advanced-threat-analytics/PlanDesign/configure-event-collection).

-   Configuração do encaminhamento de eventos do Windows

    Outra maneira de o ATA conseguir obter seus eventos é configurando seus controladores de domínio para encaminhar eventos do Windows 4776 para o Gateway de ATA. Isso é especialmente útil se você não tiver um SIEM ou se o SIEM não for atualmente suportado pelo ATA. Para obter mais informações sobre o encaminhamento de eventos do Windows no ATA, consulte [Configuração do encaminhamento de eventos do Windows](/advanced-threat-analytics/PlanDesign/configure-event-collection#ATA_event_WEF).

## Consulte também
- [Pré-requisitos do ATA](/advanced-threat-analytics/PlanDesign/ata-prerequisites)
- [Planejamento da capacidade de ATA](/advanced-threat-analytics/PlanDesign/ata-capacity-planning)
- [Configurar coleta de eventos](/advanced-threat-analytics/PlanDesign/configure-event-collection)
- [Configuração do encaminhamento de eventos do Windows](/advanced-threat-analytics/PlanDesign/configure-event-collection#ATA_event_WEF)
- [Para obter suporte, confira nosso fórum!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


