---
title: "Planejamento da implantação do Advanced Threat Analytics | Microsoft Docs"
description: "Ajuda você a planejar a implantação e decidir quantos servidores ATA serão necessários para oferecer suporte à sua rede"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/9/2017
ms.topic: get-started-article
ms.service: advanced-threat-analytics
ms.prod: 
ms.assetid: 279d79f2-962c-4c6f-9702-29744a5d50e2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: af88c02c6e2e5f679aca75b17a288c72ab300069
ms.sourcegitcommit: be6bdfa24a9b25a3375a4768d513b93900b3a498
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*



# Planejamento da capacidade de ATA
<a id="ata-capacity-planning" class="xliff"></a>
Este tópico ajuda a determinar quantos servidores do ATA são necessários para monitorar a rede. Ele também ajudará você a descobrir quantos Gateways do ATA e/ou Gateways Lightweight do ATA são necessários e a capacidade do servidor para o Centro do ATA e para os Gateways do ATA.

> [!NOTE] 
> O ATA Center pode ser implantado em qualquer fornecedor de IaaS, desde que os requisitos de desempenho descritos neste artigo sejam atendidos.

##Usando a ferramenta de dimensionamento
<a id="using-the-sizing-tool" class="xliff"></a>
A maneira recomendada e mais simples para determinar a capacidade para sua implantação ATA é usar o [Ferramenta de Dimensionamento de ATA](http://aka.ms/atasizingtool). Execute a Ferramenta de Dimensionamento ATA e resultados de arquivo do Excel, use os campos a seguir para determinar a capacidade ATA que você precisa:

- CPU e Memória do Centro do ATA: corresponda o campo **Pacotes Ocupado/s** na tabela do Centro do ATA no arquivo de resultados ao campo **PACOTES POR SEGUNDO** na [tabela do Centro do ATA](#ata-center-sizing).

- Armazenamento do Centro do ATA: corresponda o campo **Média de Pacotes/s** na tabela do Centro do ATA no arquivo de resultados para o campo **PACOTES POR SEGUNDO** na [tabela do Centro do ATA](#ata-center-sizing).
- Gateway do ATA: corresponder o campo **Pacotes Ocupados/s** na tabela do Gateway do ATA no arquivo de resultados ao campo **PACOTES POR SEGUNDO** na [tabela do Gateway do ATA](#ata-gateway-sizing) ou na [tabela do Lightweight Gateway do ATA](#ata-lightweight-gateway-sizing), dependendo do [tipo de gateway que você escolher](#choosing-the-right-gateway-type-for-your-deployment).


![Ferramenta de planejamento de capacidade de amostra](media/capacity tool.png)



Se, por alguma razão, você não puder usar a Ferramenta de Dimensionamento ATA, reúna manualmente as informações do contador de pacotes/segundos de todos os Controladores de Domínio por um período de 24 horas com um intervalo de coleta baixo (aproximadamente 5 segundos). Em seguida, para cada Controlador de Domínio, você deve calcular a média diária e a média do período mais ocupado (15 minutos).
As seções a seguir apresentam instruções sobre como coletar o contador de pacotes/segundo de um Controlador de Domínio.



### Dimensionamento da Central de ATA
<a id="ata-center-sizing" class="xliff"></a>
A Central de ATA requer um mínimo recomendado de 30 dias de dados para a análise de comportamento do usuário.
 

|Pacotes por segundo de todos os controladores de domínio|CPU (núcleos&#42;)|Memória (GB)|Armazenamento de bancos de dados por dia (GB)|Armazenamento de bancos de dados por mês (GB)|IOPS&#42;&#42;|
|---------------------------|-------------------------|-------------------|---------------------------------|-----------------------------------|-----------------------------------|
|1,000|2|32|0.3|9|30 (100)
|40.000|4|48|12|360|500 (750)
|200.000|8|64|60|1.800|1.000 (1.500)
|400.000|12|96|120|3.600|2.000 (2.500)
|750.000|24|112|225|6.750|2.500 (3.000)
|1.000.000|40|128|300|9.000|4.000 (5.000)

&#42;Isso inclui os núcleos físicos, não os núcleos com hyper-threading.

&#42;&#42;Média dos números (Números de pico)
> [!NOTE]
> -   O Centro do ATA pode lidar com um máximo agregado de 1 milhão de pacotes por segundo de todos os controladores de domínio monitorados. Em alguns ambientes, o mesmo Centro do ATA pode lidar com o tráfego geral superior a 400.000. Entre em contato com askcesec@microsoft.com para obter assistência para esses ambientes.
> -   A quantidade de armazenamento determinada aqui refere-se a valores líquidos. Você sempre deve levar em consideração o crescimento futuro e verificar se o disco no qual o banco de dados reside tem, pelo menos, 20% de espaço livre.
> -   Se o espaço livre chegar a um mínimo de 20% ou 100 GB, o conjunto mais antigo de dados será excluído. A exclusão continuará a ocorrer até 5% ou 50 GB de espaço livre permaneça no ponto em que a coleta de dados deixará de funcionar.
> - O ATA Center pode ser implantado em qualquer fornecedor de IaaS, desde que os requisitos de desempenho descritos neste artigo sejam atendidos.
> -   A latência de armazenamento para a leitura e a gravação das atividades deve estar abaixo de 10 ms.
> -   A taxa entre as atividades de leitura e gravação é de, aproximadamente, 1:3 abaixo de 100.000 pacotes por segundo e 1:6 acima de 100.000 pacotes por segundo.
> -   Durante a execução como uma memória dinâmica da máquina virtual ou qualquer outra memória, não há suporte para o recurso de inchamento.
> -   Para ter um melhor desempenho, defina a **Opção de Energia** do Centro do ATA como **Alto Desempenho**.<br>
> -   Ao trabalhar em um servidor físico, o banco de dados do ATA precisa que você **desabilite** o NUMA (acesso não uniforme à memória) no BIOS. O sistema pode referir-se ao NUMA como Intercalação de Nó, caso em que você precisará **habilitar** a Intercalação de Nó para desabilitar o NUMA. Para obter mais informações, consulte a documentação do BIOS. Isso não é pertinente quando o Centro do ATA está em execução em um servidor virtual.


## Escolhendo o tipo certo de gateway para sua implantação
<a id="choosing-the-right-gateway-type-for-your-deployment" class="xliff"></a>
Em uma implantação do ATA, há suporte para qualquer combinação dos tipos de Gateway do ATA:

- Somente Gateways do ATA
- Somente Gateways Lightweight do ATA
- Uma combinação de ambas

Ao decidir sobre o tipo de implantação do Gateway, considere os seguintes benefícios:

|Tipo de gateway|Vantagens|Custo|Topologia de implantação|Uso do controlador de domínio|
|----|----|----|----|-----|
|Gateway do ATA|A implantação Fora de banda dificulta o trabalho dos invasores em descobrir se o ATA está presente|Mais alto|Instalado junto com o controlador de domínio (fora de banda)|Dá suporte a até 50.000 pacotes por segundo|
|Gateway Lightweight do ATA|Não exige uma configuração de espelhamento de porta e servidor dedicado|Inferior|Instalado em um controlador de domínio|Dá suporte a até 10.000 pacotes por segundo|

Veja a seguir exemplos de cenários nos quais os controladores de domínio devem ser cobertos pelo Gateway Lightweight do ATA:


- Sites da filial

- Controladores de domínio virtual implantados na nuvem (IaaS)


Veja a seguir exemplos de cenários nos quais os controladores de domínio devem ser cobertos pelo Gateway do ATA:


- Matriz dos datacenters (com controladores de domínio com mais de 10.000 pacotes por segundo)


### Dimensionamento do Gateway Lightweight do ATA
<a id="ata-lightweight-gateway-sizing" class="xliff"></a>

Um Gateway Lightweight do ATA pode oferecer suporte ao monitoramento de um controlador de domínio com base na quantidade de tráfego de rede gerado pelo controlador de domínio. 


|Pacotes por segundo&#42;|CPU (núcleos&#42;&#42;)|Memória (GB)&#42;&#42;&#42;|
|---------------------------|-------------------------|---------------|
|1,000|2|6|
|5,000|6|16|
    |10.000|10|24|

&#42;Número total de pacotes por segundo no controlador de domínio sendo monitorado pelo Gateway Lightweight do ATA específico.

&#42;&#42;Número total de núcleos não hyper-threaded que esse controlador de domínio tem instalada.<br>Embora o hyper-threading seja aceitável para o Gateway Lightweight do ATA, ao planejar a capacidade, você deve contar os núcleos reais, e não os núcleos hyper-threaded.

&#42;&#42;&#42;Quantidade total de memória que esse controlador de domínio tem instalada.

> [!NOTE]   
> -   Se o controlador de domínio não tiver os recursos exigidos pelo Gateway Lightweight do ATA, o desempenho do controlador de domínio não será afetado, mas o Gateway Lightweight do ATA poderá não operar conforme o esperado.
> -   Durante a execução como uma memória dinâmica da máquina virtual ou qualquer outra memória, não há suporte para o recurso de inchamento.
> -   Para ter um melhor desempenho, defina a **Opção de Energia** do Gateway Lightweight do ATA como **Alto Desempenho**.
> -   É necessário um mínimo de 5 GB de espaço e é recomendável 10 GB de espaço, incluindo o espaço necessário para os binários do ATA, [logs do ATA](troubleshooting-ata-using-logs.md) e [logs de desempenho](troubleshooting-ata-using-perf-counters.md).


### Dimensionamento do Gateway de ATA
<a id="ata-gateway-sizing" class="xliff"></a>

Considere as seguintes questões ao decidir quantos Gateways do ATA implantar.

-   **Florestas e domínios do Active Directory**<br>
    O ATA pode monitorar o tráfego de vários domínios de uma única floresta do Active Directory. Monitorar várias florestas do Active Directory exige implantações separadas do ATA. Não configure uma única implantação do ATA para monitorar o tráfego de rede dos controladores de domínio de diferentes florestas.

-   **Espelhamento de porta**<br>
As considerações de espelhamento de porta podem exigir que você implante vários Gateways do ATA por data center ou site de filial.

-   **Capacidade**<br>
    Um Gateway do ATA pode oferecer suporte ao monitoramento de vários controladores de domínio, dependendo da quantidade de tráfego de rede dos controladores de domínio sendo monitorados. 
<br>



|Pacotes por segundo&#42;|CPU (núcleos&#42;&#42;)|Memória (GB)|
|---------------------------|-------------------------|---------------|
|1,000|1|6|
|5,000|2|10|
|10.000|3|12|
|20.000|6|24|
|50.000|16|48|
&#42;Número médio total de pacotes por segundo de todos os controladores de domínio que estão sendo monitorados pelo Gateway do ATA específico durante a respectiva hora do dia mais ocupada.

&#42;A quantidade total de tráfego espelhado pela porta do controlador de domínio não pode exceder a capacidade do NIC de captura no Gateway de ATA.

&#42;&#42;O hyper-threading deve ser desabilitado.

> [!NOTE] 
> -   Não há suporte para memória dinâmica.
> -   Para ter um melhor desempenho, defina a **Opção de Energia** do Gateway de ATA para **Alto Desempenho**.
> -   É necessário um mínimo de 5 GB de espaço e é recomendável 10 GB de espaço, incluindo o espaço necessário para os binários do ATA, [logs do ATA](troubleshooting-ata-using-logs.md) e [logs de desempenho](troubleshooting-ata-using-perf-counters.md).


## Estimativa de tráfego do controlador de domínio
<a id="domain-controller-traffic-estimation" class="xliff"></a>
Há várias ferramentas que você pode usar para descobrir a média de pacotes por segundo dos controladores de domínio. Se você não tiver as ferramentas que acompanham este contador, poderá usar o Monitor de Desempenho para coletar as informações necessárias.

Para determinar os pacotes por segundo, execute as etapas a seguir em cada controlador de domínio:

1.  Abra o Monitor de Desempenho.

    ![Imagem do monitor de desempenho](media/ATA-traffic-estimation-1.png)

2.  Expanda **Conjuntos de Coletores de Dados**.

    ![Imagem dos conjuntos de coletores de dados](media/ATA-traffic-estimation-2.png)

3.  Clique com botão direito do mouse em **Definido pelo Usuário** e selecione **Novo** &gt; **Conjunto de Coletores de Dados**.

    ![Imagem do novo conjunto de coletores de dados](media/ATA-traffic-estimation-3.png)

4.  Insira um nome para o conjunto de coletores e selecione **Criar Manualmente (Avançado)**.

5.  Em **Que tipo de dados deseja incluir?**, selecione **Criar logs de dados e Contador de desempenho**.

    ![Imagem do tipo de dados do novo conjunto de coletores de dados](media/ATA-traffic-estimation-5.png)

6.  Em **Que contadores de desempenho deseja registrar em log?**, clique em **Adicionar**.

7.  Expanda **Adaptador de Rede**, selecione **Pacotes/s** e escolha a instância apropriada. Se não tiver certeza, você poderá selecionar **&lt;Todas as instâncias&gt;** e clicar em **Adicionar** e **OK**.

    > [!NOTE]
    > Para executar essa operação em uma linha de comando, execute `ipconfig /all` para ver o nome do adaptador e a configuração.

    ![Adicionar imagem dos contadores de desempenho](media/ATA-traffic-estimation-7.png)

8.  Altere o **Intervalo de amostragem** para **1 segundo**.

9. Defina o local onde você deseja que os dados sejam salvos.

10. Em **Criar conjunto de coletores de dados**, selecione **Iniciar conjunto de coletores de dados agora** e clique em **Concluir**.

    Agora, você deverá ver o conjunto de coletores de dados que criou com um triângulo verde, indicando que ele está funcionando.

11. Após 24 horas, pare o conjunto de coletores de dados clicando com o botão direito do mouse no conjunto de coletores de dados e selecionando **Parar**.

    ![Imagem ao parar o conjunto de coletores de dados](media/ATA-traffic-estimation-12.png)

12. No Explorador de Arquivos, navegue até a pasta em que o arquivo .blg foi salvo e clique duas vezes nele para abri-lo no Monitor de Desempenho.

13. Selecione o contador Pacotes/s e registre os valores médio e máximo.

    ![Imagem do contador de pacotes por segundo](media/ATA-traffic-estimation-14.png)

## Consulte também
<a id="see-also" class="xliff"></a>
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Arquitetura do ATA](ata-architecture.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)