---
title: "Solução de problemas do Advanced Threat Analytics usando os contadores de desempenho | Microsoft Docs"
description: "Descreve como você pode usar os contadores de desempenho para solucionar problemas com o ATA"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: df162a62-f273-4465-9887-94271f5000d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 5c4662cd2d83135227cf86e339d5e30f9713f022
ms.sourcegitcommit: 998e8aed5835b228e907aab78845723a02521741
translationtype: HT
---
*Aplica-se a: Advanced Threat Analytics versão 1.7*



# <a name="troubleshooting-ata-using-the-performance-counters"></a>Solução de problemas do ATA usando contadores de desempenho
Os contadores de desempenho do ATA fornecem informações sobre como está o desempenho de cada componente do ATA. Os componentes no ATA processam dados sequencialmente, para que quando houver um problema, ele possa causar um descarte de tráfego parcial em algum ponto da cadeia de componentes. Para corrigir o problema, você precisa descobrir qual componente está dando problema e corrigi-lo no início da cadeia. Use os dados encontrados nos contadores de desempenho para entender o funcionamento de cada componente.
Consulte a [arquitetura do ATA](/advanced-threat-analytics/plan-design/ata-architecture) para entender o fluxo de componentes internos do ATA.

**Processo de componente do ATA**:

1.  Quando um componente atinge seu tamanho máximo, ele impede o componente anterior de lhe enviar mais entidades.

2.  Em seguida, o componente anterior começa a aumentar **seu** próprio tamanho até impedir o componente antes dele de enviar mais entidades.

3.  Isso acontece ao longo de todo o caminho até o componente NetworkListener, que descartará o tráfego quando ele não puder mais encaminhar entidades.


## <a name="retrieving-performance-monitor-files-for-troubleshooting"></a>Recuperando arquivos do monitor de desempenho para solução de problemas

Para recuperar os arquivos do monitor de desempenho (BLG) de vários componentes do ATA:
1.  Abra o perfmon.
2.  Parar o conjunto de coletores de dados nomeado: "Microsoft ATA Gateway" ou "Microsoft ATA Center".
3.  Vá para a pasta de conjunto de coletores de dados (por padrão, isso é "C:\Program Files\Microsoft Advanced Threat Analytics\Gateway\Logs\DataCollectorSets" ou “C:\Program Files\Microsoft Advanced Threatts").
4.  Copie o arquivo BLG que foi modificado mais recentemente.
5.  Reinicie o conjunto de coletores de dados nomeado: "Microsoft ATA Gateway" ou "Microsoft ATA Center".


## <a name="ata-gateway-performance-counters"></a>Contadores de desempenho do Gateway de ATA

Nesta seção, todas as referências ao Gateway do ATA referem-se também ao Gateway Lightweight do ATA.

Você pode observar o status do desempenho em tempo real do Gateway de ATA adicionando os contadores de desempenho do Gateway de ATA.
Isso é feito abrindo o "Monitor de desempenho" e adicionando todos os contadores ao Gateway de ATA. O nome do objeto do contador de desempenho é: "Microsoft ATA Gateway".

Aqui está a lista dos principais contadores do Gateway de ATA a ter em atenção:

|Contador|Descrição|Limite|Solução de problemas|
|-----------|---------------|-------------|-------------------|
|Mensagens\s do PEF analisado do NetworkListener\Gateway de ATA da Microsoft|A quantidade de tráfego processada pelo Gateway de ATA a cada segundo.|Sem limite|Ajuda a entender a quantidade de tráfego que está sendo analisada pelo Gateway de ATA.|
|Eventos descartados por PEF do NetworkListener\s|A quantidade de tráfego descartada pelo Gateway de ATA a cada segundo.|Esse número deve ser sempre zero (intermitência rara e curta de descartes é aceitável).|Verifique se há qualquer componente que atingiu seu tamanho máximo e está bloqueando componentes anteriores até o NetworkListener. Consulte o **Processo de componente do ATA** acima.<br /><br />Verifique se não há nenhum problema com a CPU ou a memória.|
|Eventos descartados\s do Analisador de ETW NetworkListener/Gateway do ATA da Microsoft|A quantidade de tráfego descartada pelo Gateway de ATA a cada segundo.|Esse número deve ser sempre zero (intermitência rara e curta de descartes é aceitável).|Verifique se há qualquer componente que atingiu seu tamanho máximo e está bloqueando componentes anteriores até o NetworkListener. Consulte o **Processo de componente do ATA** acima.<br /><br />Verifique se não há nenhum problema com a CPU ou a memória.|
|Nº do Tamanho do Bloco e dos Dados de Mensagem do NetworkActivityTranslator/Gateway ATA da Microsoft|A quantidade de tráfego na fila de conversão para atividades de rede (NAs).|Deve ser menor que o máximo de 1 (máximo padrão: 100.000)|Verifique se há qualquer componente que atingiu seu tamanho máximo e está bloqueando componentes anteriores até o NetworkListener. Consulte o **Processo de componente do ATA** acima.<br /><br />Verifique se não há nenhum problema com a CPU ou a memória.|
|Tamanho de Bloco de Atividades do EntityResolver/Gateway do ATA da Microsoft|A quantidade de atividades de rede (NAs) na fila de resolução.|Deve ser menor que o máximo de 1 (máximo padrão: 10.000)|Verifique se há qualquer componente que atingiu seu tamanho máximo e está bloqueando componentes anteriores até o NetworkListener. Consulte o **Processo de componente do ATA** acima.<br /><br />Verifique se não há nenhum problema com a CPU ou a memória.|
|Tamanho de Bloco do Lote de Entidade do EntitySender/Gateway do ATA da Microsoft|A quantidade de atividades de rede (NAs) na fila a ser enviada para o Centro de ATA.|Deve ser menor que o máximo de 1 (máximo padrão: 1.000.000)|Verifique se há qualquer componente que atingiu seu tamanho máximo e está bloqueando componentes anteriores até o NetworkListener. Consulte o **Processo de componente do ATA** acima.<br /><br />Verifique se não há nenhum problema com a CPU ou a memória.|
|Tempo de Envio de Lote do EntitySender/Gateway do ATA da Microsoft|A quantidade de tempo necessária para enviar o último lote.|Deve ser menor que 1.000 milissegundos na maioria das vezes|Verifique se há problemas de rede entre o Gateway de ATA e o Centro de ATA.|

> [!NOTE]
> -   Os contadores de tempo estão em milissegundos.
> -   Às vezes, é mais conveniente monitorar a lista completa de contadores usando o tipo de gráfico "Relatório" (exemplo: monitoramento em tempo real de todos os contadores)

## <a name="ata-lightweight-gateway-performance-counters"></a>Contadores de desempenho do Gateway Lightweight do ATA
Os contadores de desempenho podem ser usados para gerenciamento de cotas no Gateway Lightweight, a fim de certificar-se de que o ATA não use muitos recursos de muitos dos controladores de domínio no qual ele está instalado.
Para medir as limitações de recursos que o ATA impõe sobre o Gateway Lightweight, adicione os contadores a seguir.

Para fazer isso, abra o "Monitor de desempenho" e adicione todos os contadores ao Lightweight Gateway do ATA. O nome dos objetos de contador de desempenho são: "Microsoft ATA Gateway" e "Microsoft ATA Gateway Updater".


|Contador|Descrição|Limite|Solução de problemas|
|-----------|---------------|-------------|-------------------|
|% Máxima de Tempo de CPU do Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager|A quantidade máxima de tempo da CPU (em porcentagem) que o processo do Gateway Lightweight pode consumir. |Sem limite. | Esta é a limitação que impede que os recursos do controlador de domínio sejam usados pelo Gateway Lightweight do ATA. Se você perceber que o processo atinge frequentemente o limite máximo durante um período (o processo atinge o limite e, em seguida, começa a descartar tráfego), significa que você precisa adicionar mais recursos ao servidor que está executando o controlador de domínio.|
|Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager Commit Memory Max Size|A quantidade máxima de memória confirmada (em bytes) que o processo do Gateway Lightweight pode consumir.|Sem limite. | Esta é a limitação que impede que os recursos do controlador de domínio sejam usados pelo Gateway Lightweight do ATA. Se você perceber que o processo atinge frequentemente o limite máximo durante um período (o processo atinge o limite e, em seguida, começa a descartar tráfego), significa que você precisa adicionar mais recursos ao servidor que está executando o controlador de domínio.| 
|Tamanho Limite do Conjunto de Trabalho do Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager|A quantidade máxima de memória física (em bytes) que o processo do Gateway Lightweight pode consumir.|Sem limite. | Esta é a limitação que impede que os recursos do controlador de domínio sejam usados pelo Gateway Lightweight do ATA. Se você perceber que o processo atinge frequentemente o limite máximo durante um período (o processo atinge o limite e, em seguida, começa a descartar tráfego), significa que você precisa adicionar mais recursos ao servidor que está executando o controlador de domínio.|



Para ver seu consumo real, consulte os seguintes contadores:



|Contador|Descrição|Limite|Solução de problemas|
|-----------|---------------|-------------|-------------------|
|Process(Microsoft.Tri.Gateway)\%Tempo do Processador|A quantidade de tempo da CPU (em porcentagem) que o processo do Gateway Lightweight está consumindo. |Sem limite. | Compare os resultados desse contador com o limite encontrado em GatewayUpdaterResourceManager CPU Time Max %. Se você perceber que o processo atinge frequentemente o limite máximo durante um período (o processo atinge o limite e, em seguida, começa a descartar tráfego), significa que você precisa dedicar mais recursos ao Gateway Lightweight.|
|Process(Microsoft.Tri.Gateway)Bytes Privados|A quantidade de memória confirmada (em bytes) que o processo do Gateway Lightweight está consumindo.|Sem limite. | Compare os resultados desse contador com o limite encontrado em Tamanho Máximo de Memória de Confirmação do GatewayUpdaterResourceManager. Se você perceber que o processo atinge frequentemente o limite máximo durante um período (o processo atinge o limite e, em seguida, começa a descartar tráfego), significa que você precisa dedicar mais recursos ao Gateway Lightweight.| 
|Process(Microsoft.Tri.Gateway)\Conjunto de Trabalho|A quantidade de memória física (em bytes) que o processo do Gateway Lightweight está consumindo.|Sem limite. |Compare os resultados desse contador com o limite encontrado em GatewayUpdaterResourceManager Working Set Limit Size. Se você perceber que o processo atinge frequentemente o limite máximo durante um período (o processo atinge o limite e, em seguida, começa a descartar tráfego), significa que você precisa dedicar mais recursos ao Gateway Lightweight.|

## <a name="ata-center-performance-counters"></a>Contadores de desempenho do Centro de ATA
Você pode observar o status de desempenho em tempo real da Central do ATA adicionando os contadores de desempenho da Central do ATA.

Isso é feito abrindo o "Monitor de desempenho" e adicionando todos os contadores ao Centro de ATA. O nome do objeto do contador de desempenho é: "Microsoft ATA Center".

Aqui está a lista dos principais contadores do Centro de ATA a ter em atenção:

|Contador|Descrição|Limite|Solução de problemas|
|-----------|---------------|-------------|-------------------|
|Tamanho do Bloco do Lote de Entidade do Centro do Microsoft ATA/EntityReceiver|O número de lotes de entidade colocados em fila pelo Centro de ATA.|Deve ser menor que o máximo de 1 (máximo padrão: 10.000)|Verifique se há qualquer componente que atingiu seu tamanho máximo e está bloqueando componentes anteriores até o NetworkListener.  Consulte o **Processo de componente do ATA** acima.<br /><br />Verifique se não há nenhum problema com a CPU ou a memória.|
|Tamanho do Bloco de Atividade de Rede do Centro do Microsoft ATA\NetworkActivityProcessor|O número de atividades de rede (NAs) na fila de processamento.|Deve ser menor que o máximo de 1 (máximo padrão: 50.000)|Verifique se há qualquer componente que atingiu seu tamanho máximo e está bloqueando componentes anteriores até o NetworkListener. Consulte o **Processo de componente do ATA** acima.<br /><br />Verifique se não há nenhum problema com a CPU ou a memória.|
|Tamanho do Bloco de Atividade de Rede do Centro do Microsoft ATA\EntityProfiler|O número de atividades de rede (NAs) na fila de criação de perfil.|Deve ser menor que o máximo de 1 (máximo padrão: 10.000)|Verifique se há qualquer componente que atingiu seu tamanho máximo e está bloqueando componentes anteriores até o NetworkListener. Consulte o **Processo de componente do ATA** acima.<br /><br />Verifique se não há nenhum problema com a CPU ou a memória.|
|Tamanho do Bloco &#42; do Centro\Banco de dados do ATA da Microsoft|O número de atividades de rede, de um tipo específico, colocadas em fila para serem gravadas no banco de dados.|Deve ser menor que o máximo de 1 (máximo padrão: 50.000)|Verifique se há qualquer componente que atingiu seu tamanho máximo e está bloqueando componentes anteriores até o NetworkListener. Consulte o **Processo de componente do ATA** acima.<br /><br />Verifique se não há nenhum problema com a CPU ou a memória.|


> [!NOTE]
> -   Os contadores de tempo estão em milissegundos
> -   Às vezes, é mais conveniente monitorar a lista completa de contadores usando o tipo de gráfico de Relatório (exemplo: monitoramento em tempo real de todos os contadores).

## <a name="operating-system-counters"></a>Contadores do sistema operacional
Abaixo temos a lista dos principais contadores do sistema operacional a ter em atenção:

|Contador|Descrição|Limite|Solução de problemas|
|-----------|---------------|-------------|-------------------|
|Processador(_Total)\% Tempo do Processador|Percentual de tempo decorrido que o processador gasta para executar um thread não ocioso.|Menos de 80% em média|Verifique se há um processo específico que está levando muito mais tempo de processamento do que deveria.<br /><br />Adicione mais processadores.<br /><br />Reduza a quantidade de tráfego por servidor.<br /><br />O contador "Processador(_Total)\% Tempo do Processador" pode ser menos preciso em servidores virtuais. Nesse caso, a maneira mais precisa de medir a falta de energia do processador é por meio do contador "Sistema\Comprimento da Fila do Processador".|
|Sistema\Comutações de contexto\s|A taxa combinada na qual todos os processadores alternam de um thread para outro.|Menos de 5.000&#42;núcleos (núcleos físicos)|Verifique se há um processo específico que está levando muito mais tempo de processamento do que deveria.<br /><br />Adicione mais processadores.<br /><br />Reduza a quantidade de tráfego por servidor.<br /><br />O contador "Processador(_Total)\% Tempo do Processador" pode ser menos preciso em servidores virtuais. Nesse caso, a maneira mais precisa de medir a falta de energia do processador é por meio do contador "Sistema\Comprimento da Fila do Processador".|
|Sistema por Comprimento da Fila do Processador|O número de threads que estão prontos para executar e estão aguardando para ser agendados.|Menos que 5&#42;núcleos (núcleos físicos)|Verifique se há um processo específico que está levando muito mais tempo de processamento do que deveria.<br /><br />Adicione mais processadores.<br /><br />Reduza a quantidade de tráfego por servidor.<br /><br />O contador "Processador(_Total)\% Tempo do Processador" pode ser menos preciso em servidores virtuais. Nesse caso, a maneira mais precisa de medir a falta de energia do processador é por meio do contador "Sistema\Comprimento da Fila do Processador".|
|Memory\Available MBytes|A quantidade de memória física (RAM) disponível para alocação.|Deve ser a mais que 512|Verifique se há um processo específico que está consumindo muito mais memória física do que deveria.<br /><br />Aumento da quantidade de memória física.<br /><br />Reduza a quantidade de tráfego por servidor.|
|LogicalDisk(&#42;)\Média Segundos de Disco\Leitura|A latência média de leitura dos dados do disco (você deve escolher a unidade de banco de dados como a instância).|Deve ser menor que 10 milissegundos|Verifique se há um processo específico que está utilizando a unidade de banco de dados mais do que deveria.<br /><br />Consulte o fornecedor ou a equipe de armazenamento se esta unidade pode fornecer a carga de trabalho atual enquanto tem menos de 10 ms de latência. A carga de trabalho atual pode ser determinada usando os contadores de utilização do disco.|
|LogicalDisk(&#42;)\Média Média de Gravações\Disco s|A latência média de gravação dos dados para o disco (você deve escolher a unidade de banco de dados como a instância).|Deve ser menor que 10 milissegundos|Verifique se há um processo específico que está utilizando a unidade de banco de dados mais do que deveria.<br /><br />Consulte o fornecedor ou a equipe de armazenamento se esta unidade pode fornecer a carga de trabalho atual enquanto tem menos de 10 ms de latência. A carga de trabalho atual pode ser determinada usando os contadores de utilização do disco.|
|\LogicalDisk(&#42;)\Leituras de Disco\s|A taxa de execução de operações de leitura para o disco.|Sem limite|Os contadores de utilização de disco podem adicionar informações ao solucionar problemas de latência de armazenamento.|
|\LogicalDisk(&#42;)\Bytes de Leitura de Disco\s|O número de bytes por segundo que estão sendo lidos no disco.|Sem limite|Os contadores de utilização de disco podem adicionar informações ao solucionar problemas de latência de armazenamento.|
|\LogicalDisk&#42;\Gravações em Disco\s|A taxa de execução de operações de gravação no disco.|Sem limite|Os contadores de utilização de disco (pode adicionar informações ao solucionar problemas de latência de armazenamento)|
|\LogicalDisk(&#42;)\Bytes de Gravação em Disco\s|O número de bytes por segundo que estão sendo gravados no disco.|Sem limite|Os contadores de utilização de disco podem adicionar informações ao solucionar problemas de latência de armazenamento.|

## <a name="see-also"></a>Consulte também
- [Pré-requisitos do ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planejamento da capacidade do ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurar coleta de eventos](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configuração do encaminhamento de eventos do Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
