---
# required metadata

title: Solução de problemas do ATA usando os contadores de desempenho | Microsoft Advanced Threat Analytics
description: Descreve como você pode usar os contadores de desempenho para solucionar problemas com o ATA
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: df162a62-f273-4465-9887-94271f5000d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Solução de problemas do ATA usando contadores de desempenho
Os contadores de desempenho do ATA fornecem informações sobre como está o desempenho de cada componente do ATA. Os componentes no ATA processam dados sequencialmente, para que quando haja um problema, ele cause uma reação em cadeia que faz com que o tráfego seja descartado. Para corrigir o problema, você precisa descobrir qual componente está dando problema e corrigi-lo no início da cadeia.
Consulte a [arquitetura do ATA](/advanced-threat-analytics/plan-design/ata-architecture) para entender o fluxo de componentes internos do ATA.

**Processo de componente do ATA**:

1.  Quando um componente atinge seu tamanho máximo, ele impede o componente anterior de lhe enviar mais entidades.

2.  Em seguida, o componente anterior começa a aumentar **seu** próprio tamanho até impedir o componente antes dele de enviar mais entidades.

3.  Isso acontece ao longo de todo o caminho até o componente NetworkListener inicial, que descartará o tráfego quando ele não puder mais encaminhar entidades.

4. Use os dados encontrados nos contadores de desempenho para entender o funcionamento de cada componente.

## Contadores de desempenho do Gateway de ATA

Nesta seção, todas as referências ao Gateway do ATA referem-se também ao Gateway Lightweight do ATA.

Você pode observar o status do desempenho em tempo real do Gateway de ATA adicionando os contadores de desempenho do Gateway de ATA.
Isso é feito abrindo o "Monitor de desempenho" e adicionando todos os contadores ao Gateway de ATA. O nome do objeto do contador de desempenho é: "Microsoft ATA Gateway".

![Adicionar imagem dos contadores de desempenho](media/ATA-performance-counters.png)

Aqui está a lista dos principais contadores do Gateway de ATA a ter em atenção:

|Contador|Descrição|Limite|Solução de problemas|
|-----------|---------------|-------------|-------------------|
|Mensagens do analisador de PEF NetworkListener/s|A quantidade de tráfego processada pelo Gateway de ATA a cada segundo.|Sem limite|Ajuda a entender a quantidade de tráfego que está sendo analisada pelo Gateway de ATA.|
|Eventos descartados por PEF do NetworkListener/s|A quantidade de tráfego descartada pelo Gateway de ATA a cada segundo.|Esse número deve ser sempre zero (intermitência rara e curta de descartes é aceitável).|Verifique se há qualquer componente que atingiu seu tamanho máximo e está bloqueando componentes anteriores até o NetworkListener. Consulte o **Processo de componente do ATA** acima.<br /><br />Verifique se não há nenhum problema com a CPU ou a memória.|
|Eventos descartados por ETW do NetworkListener/s|A quantidade de tráfego descartada pelo Gateway de ATA a cada segundo.|Esse número deve ser sempre zero (intermitência rara e curta de descartes é aceitável).|Verifique se há qualquer componente que atingiu seu tamanho máximo e está bloqueando componentes anteriores até o NetworkListener. Consulte o **Processo de componente do ATA** acima.<br /><br />Verifique se não há nenhum problema com a CPU ou a memória.|
|Número dos dados de mensagem e tamanho do bloco do NetworkActivityTranslator|A quantidade de tráfego na fila de conversão para atividades de rede (NAs).|Deve ser menor que o máximo de 1 (máximo padrão: 100.000)|Verifique se há qualquer componente que atingiu seu tamanho máximo e está bloqueando componentes anteriores até o NetworkListener. Consulte o **Processo de componente do ATA** acima.<br /><br />Verifique se não há nenhum problema com a CPU ou a memória.|
|Tamanho de bloco de atividades do EntityResolver|A quantidade de atividades de rede (NAs) na fila de resolução.|Deve ser menor que o máximo de 1 (máximo padrão: 10.000)|Verifique se há qualquer componente que atingiu seu tamanho máximo e está bloqueando componentes anteriores até o NetworkListener. Consulte o **Processo de componente do ATA** acima.<br /><br />Verifique se não há nenhum problema com a CPU ou a memória.|
|Tamanho do bloco do lote de entidade do EntitySender|A quantidade de atividades de rede (NAs) na fila a ser enviada para o Centro de ATA.|Deve ser menor que o máximo de 1 (máximo padrão: 1.000.000)|Verifique se há qualquer componente que atingiu seu tamanho máximo e está bloqueando componentes anteriores até o NetworkListener. Consulte o **Processo de componente do ATA** acima.<br /><br />Verifique se não há nenhum problema com a CPU ou a memória.|
|Hora de envio em lote do EntitySender|A quantidade de tempo necessária para enviar o último lote.|Deve ser menor que 1.000 milissegundos na maioria das vezes|Verifique se há problemas de rede entre o Gateway de ATA e o Centro de ATA.|

> [!NOTE]
> -   Os contadores de tempo estão em milissegundos.
> -   Às vezes, é mais conveniente monitorar a lista completa de contadores usando o tipo de gráfico "Relatório" (exemplo: monitoramento em tempo real de todos os contadores)

## Contadores de desempenho do Centro de ATA
Você pode observar o status de desempenho em tempo real do Centro de ATA adicionando os contadores de desempenho do Centro de ATA.

Isso é feito abrindo o "Monitor de desempenho" e adicionando todos os contadores ao Centro de ATA. O nome do objeto do contador de desempenho é: "Microsoft ATA Center".

![Centro de ATA adiciona contadores de desempenho](media/ATA-Gateway-perf-counters.png)

Aqui está a lista dos principais contadores do Centro de ATA a ter em atenção:

|Contador|Descrição|Limite|Solução de problemas|
|-----------|---------------|-------------|-------------------|
|Tamanho do bloco do lote de entidade do EntityReceiver|O número de lotes de entidade colocados em fila pelo Centro de ATA.|Deve ser menor que o máximo de 1 (máximo padrão: 10.000)|Verifique se há qualquer componente que atingiu seu tamanho máximo e está bloqueando componentes anteriores até o NetworkListener.  Consulte o **Processo de componente do ATA** acima.<br /><br />Verifique se não há nenhum problema com a CPU ou a memória.|
|Tamanho do bloco de atividade de rede do NetworkActivityProcessor|O número de atividades de rede (NAs) na fila de processamento.|Deve ser menor que o máximo de 1 (máximo padrão: 50.000)|Verifique se há qualquer componente que atingiu seu tamanho máximo e está bloqueando componentes anteriores até o NetworkListener. Consulte o **Processo de componente do ATA** acima.<br /><br />Verifique se não há nenhum problema com a CPU ou a memória.|
|Tamanho do bloco de atividade de rede do EntityProfiler|O número de atividades de rede (NAs) na fila de criação de perfil.|Deve ser menor que o máximo de 1 (máximo padrão: 10.000)|Verifique se há qualquer componente que atingiu seu tamanho máximo e está bloqueando componentes anteriores até o NetworkListener. Consulte o **Processo de componente do ATA** acima.<br /><br />Verifique se não há nenhum problema com a CPU ou a memória.|
|CenterDatabase &#42; Tamanho do Bloco|O número de atividades de rede, de um tipo específico, colocadas em fila para serem gravadas no banco de dados.|Deve ser menor que o máximo de 1 (máximo padrão: 50.000)|Verifique se há qualquer componente que atingiu seu tamanho máximo e está bloqueando componentes anteriores até o NetworkListener. Consulte o **Processo de componente do ATA** acima.<br /><br />Verifique se não há nenhum problema com a CPU ou a memória.|


> [!NOTE]
> -   Os contadores de tempo estão em milissegundos
> -   Às vezes, é mais conveniente monitorar a lista completa de contadores usando o tipo de gráfico de Relatório (exemplo: monitoramento em tempo real de todos os contadores).

## Contadores do sistema operacional
Abaixo temos a lista dos principais contadores do sistema operacional a ter em atenção:

|Contador|Descrição|Limite|Solução de problemas|
|-----------|---------------|-------------|-------------------|
|Processador(_Total)\% Tempo do Processador|Percentual de tempo decorrido que o processador gasta para executar um thread não ocioso.|Menos de 80% em média|Verifique se há um processo específico que está levando muito mais tempo de processamento do que deveria.<br /><br />Adicione mais processadores.<br /><br />Reduza a quantidade de tráfego por servidor.<br /><br />O contador "Processador(_Total)\% Tempo do Processador" pode ser menos preciso em servidores virtuais. Nesse caso, a maneira mais precisa de medir a falta de energia do processador é por meio do contador "Sistema\Comprimento da Fila do Processador".|
|System\Context Switches/sec|A taxa combinada na qual todos os processadores alternam de um thread para outro.|Menos de 5.000&#42;núcleos (núcleos físicos)|Verifique se há um processo específico que está levando muito mais tempo de processamento do que deveria.<br /><br />Adicione mais processadores.<br /><br />Reduza a quantidade de tráfego por servidor.<br /><br />O contador "Processador(_Total)\% Tempo do Processador" pode ser menos preciso em servidores virtuais. Nesse caso, a maneira mais precisa de medir a falta de energia do processador é por meio do contador "Sistema\Comprimento da Fila do Processador".|
|Sistema por Comprimento da Fila do Processador|O número de threads que estão prontos para executar e estão aguardando para ser agendados.|Menos que 5&#42;núcleos (núcleos físicos)|Verifique se há um processo específico que está levando muito mais tempo de processamento do que deveria.<br /><br />Adicione mais processadores.<br /><br />Reduza a quantidade de tráfego por servidor.<br /><br />O contador "Processador(_Total)\% Tempo do Processador" pode ser menos preciso em servidores virtuais. Nesse caso, a maneira mais precisa de medir a falta de energia do processador é por meio do contador "Sistema\Comprimento da Fila do Processador".|
|Memory\Available MBytes|A quantidade de memória física (RAM) disponível para alocação.|Deve ser a mais que 512|Verifique se há um processo específico que está consumindo muito mais memória física do que deveria.<br /><br />Aumento da quantidade de memória física.<br /><br />Reduza a quantidade de tráfego por servidor.|
|LogicalDisk(&#42;)\Média Segundos de Disco/Leitura|A latência média de leitura dos dados do disco (você deve escolher a unidade de banco de dados como a instância).|Deve ser menor que 10 milissegundos|Verifique se há um processo específico que está utilizando a unidade de banco de dados mais do que deveria.<br /><br />Consulte o fornecedor ou a equipe de armazenamento se esta unidade pode fornecer a carga de trabalho atual enquanto tem menos de 10 ms de latência. A carga de trabalho atual pode ser determinada usando os contadores de utilização do disco.|
|LogicalDisk(&#42;)\Média Média de Gravações/Disco s|A latência média de gravação dos dados para o disco (você deve escolher a unidade de banco de dados como a instância).|Deve ser menor que 10 milissegundos|Verifique se há um processo específico que está utilizando a unidade de banco de dados mais do que deveria.<br /><br />Consulte o fornecedor ou a equipe de armazenamento se esta unidade pode fornecer a carga de trabalho atual enquanto tem menos de 10 ms de latência. A carga de trabalho atual pode ser determinada usando os contadores de utilização do disco.|
|\LogicalDisk(&#42;)\Leituras de Disco/seg|A taxa de execução de operações de leitura para o disco.|Sem limite|Os contadores de utilização de disco podem adicionar informações ao solucionar problemas de latência de armazenamento.|
|\LogicalDisk(&#42;)\Bytes de Leitura de Disco/seg|O número de bytes por segundo que estão sendo lidos no disco.|Sem limite|Os contadores de utilização de disco podem adicionar informações ao solucionar problemas de latência de armazenamento.|
|\LogicalDisk(&#42;)\Escritas de Disco/seg|A taxa de execução de operações de gravação no disco.|Sem limite|Os contadores de utilização de disco (pode adicionar informações ao solucionar problemas de latência de armazenamento)|
|\LogicalDisk(&#42;)\Bytes de Escrita de Disco/seg|O número de bytes por segundo que estão sendo gravados no disco.|Sem limite|Os contadores de utilização de disco podem adicionar informações ao solucionar problemas de latência de armazenamento.|

## Consulte também
- [Pré-requisitos do ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planejamento da capacidade de ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurar coleta de eventos](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configuração do encaminhamento de eventos do Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


