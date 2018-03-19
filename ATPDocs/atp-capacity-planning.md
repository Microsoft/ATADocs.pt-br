---
title: "Planejamento da implantação da Proteção Avançada contra Ameaças do Azure | Microsoft Docs"
description: "Ajuda você a planejar a implantação e a decidir quantos servidores do Azure ATP serão necessários para dar suporte à sua rede"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/11/2018
ms.topic: get-started-article
ms.service: azure-advanced-threat-protection
ms.prod: 
ms.assetid: da0ee438-35f8-4097-b3a1-1354ad59eb32
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 577b7a5105e8de773f57b1e00bc1c9cb51096799
ms.sourcegitcommit: 912e453753156902618ae6ebb8489c2320c06fc6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/12/2018
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*



# <a name="azure-atp-capacity-planning"></a>Planejamento de capacidade do Azure ATP
Este artigo ajuda você a determinar quantos sensores e quantos sensores autônomos do Azure ATP são necessários.

> [!NOTE] 
> A ferramenta de dimensionamento tem duas folhas – uma para o ATA e outra para o Azure ATP. Verifique se você está na folha correta.

## <a name="using-the-sizing-tool"></a>Usando a ferramenta de dimensionamento
A maneira recomendada e mais simples de determinar a capacidade de sua implantação do Azure ATP é usar o [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/aatpsizingtool). Execute a Ferramenta de dimensionamento do Azure ATP e, nos resultados do arquivo do Excel, use os campos a seguir para determinar a memória e a CPU usadas pelo sensor:

- Sensor do Azure ATP: faça a correspondência entre o campo **Pacotes Ocupados/s** na tabela do sensor do Azure ATP no arquivo de resultados com o campo **PACOTES POR SEGUNDO** na [Tabela do sensor autônomo do Azure ATP](#azure-atp-sensor-sizing) ou na [Tabela do sensor do Azure ATP](#azure-atp-standalone-sensor-sizing), dependendo do [tipo de sensor que você escolher](#choosing-the-right-sensor-type-for-your-deployment).


![Ferramenta de planejamento de capacidade de amostra](media/capacity-tool.png)


Se, por alguma razão, você não puder usar a Ferramenta de dimensionamento do Azure ATP, reúna manualmente as informações do contador de pacotes/s de todos os Controladores de domínio por 24 horas com um intervalo de coleta baixo (aproximadamente 5 segundos). Em seguida, para cada Controlador de Domínio, você deve calcular a média diária e a média do período mais ocupado (15 minutos).
As seções a seguir apresentam instruções sobre como coletar o contador de pacotes/segundo de um Controlador de Domínio.

## Escolher o tipo certo de sensor para a implantação<a name="choosing-the right-sensor-type-for-your-deployment"></a>
Em uma implantação do Azure ATP, qualquer combinação dos tipos de sensor autônomo do Azure ATP tem suporte:

- Somente sensores autônomos do Azure ATP
- Somente sensor do Azure ATP
- Uma combinação de ambas

Ao decidir o tipo de implantação do sensor, considere os seguintes benefícios:

|tipo de sensor|Vantagens|Custo|Topologia de implantação|Uso do controlador de domínio|
|----|----|----|----|-----|
|Sensor autônomo do Azure ATP|A implantação Fora de banda dificulta o trabalho dos invasores de descobrir se o Azure ATP está presente|Mais alto|Instalado junto com o controlador de domínio (fora de banda)|Dá suporte a até 100.000 pacotes por segundo|
|Sensor do Azure ATP|Não exige uma configuração de espelhamento de porta e servidor dedicado|Inferior|Instalado em um controlador de domínio|Dá suporte a até 100.000 pacotes por segundo|

Considere as seguintes questões ao decidir quantos sensores autônomos do Azure ATP implantar.

-   **Florestas e domínios do Active Directory**<br>
    O Azure ATP pode monitorar o tráfego de vários domínios em uma única floresta do Active Directory para cada espaço de trabalho que você criar. Para monitorar várias florestas, você precisa criar vários espaços de trabalho. 

-   **Espelhamento de porta**<br>
Considerações de espelhamento de porta podem exigir que você implante vários sensores autônomos do Azure ATP por data center ou site de filial.

-   **Capacidade**<br>
    Um sensor autônomo do Azure ATP pode dar suporte ao monitoramento de vários controladores de domínio, dependendo da quantidade de tráfego de rede dos controladores de domínio sendo monitorados. 


## Sensor do Azure ATP e dimensionamento de sensor autônomo <a name="sizing"></a>

Um sensor do Azure ATA pode dar suporte ao monitoramento de um controlador de domínio com base na quantidade de tráfego de rede gerado pelo controlador de domínio. A tabela a seguir é uma estimativa, o valor final que o sensor analisa depende da quantidade de tráfego que você tem e da distribuição desse tráfego. 
> [!NOTE]
> A capacidade de CPU e memória a seguir se refere ao consumo do próprio sensor – e não à capacidade do controlador de domínio.

|Pacotes por segundo*|CPU (núcleos)|Memória (GB)|
|----|----|-----|
|0 - 1k|0.25|2.50|
|1k - 5k|0.75|6.00|
|5k - 10k|1.00|6.50|
|10k - 20k|2.00|9.00|
|20k - 50k|3.50|9.50|
|50k - 75k |3.50|9.50|
|75k - 100k|3.50 |9.50|

> [!NOTE]
> - Número total de núcleos a serem usados pelo serviço de sensor.<br>Recomendamos não trabalhar com núcleos hyper-threaded.
> - Número total de memória a ser usada pelo serviço de sensor.
> -   Se o controlador de domínio não tiver os recursos exigidos pelo sensor do Azure ATP, o desempenho do controlador de domínio não será afetado, mas o sensor do Azure ATP poderá não operar conforme o esperado.
> -   Durante a execução como uma memória dinâmica da máquina virtual ou qualquer outra memória, não há suporte para o recurso de inchamento.
> -   Para ter um melhor desempenho, defina a **Opção de Energia** do sensor do Azure ATP como **Alto Desempenho**.
> -   É necessário um mínimo de dois núcleos e 6 GB de espaço, e 10 GB são recomendados, incluindo o espaço necessário para os binários e logs do Azure ATP.


## <a name="domain-controller-traffic-estimation"></a>Estimativa de tráfego do controlador de domínio

Há várias ferramentas que você pode usar para descobrir a média de pacotes por segundo dos controladores de domínio. Se você não tiver as ferramentas que acompanham este contador, poderá usar o Monitor de Desempenho para coletar as informações necessárias.

Para determinar os pacotes por segundo, execute as etapas a seguir em cada controlador de domínio:

1.  Abra o Monitor de Desempenho.

    ![Imagem do monitor de desempenho](media/atp-traffic-estimation-1.png)

2.  Expanda **Conjuntos de Coletores de Dados**.

    ![Imagem dos conjuntos de coletores de dados](media/atp-traffic-estimation-2.png)

3.  Clique com botão direito do mouse em **Definido pelo Usuário** e selecione **Novo** &gt; **Conjunto de Coletores de Dados**.

    ![Imagem do novo conjunto de coletores de dados](media/atp-traffic-estimation-3.png)

4.  Insira um nome para o conjunto de coletores e selecione **Criar Manualmente (Avançado)**.

5.  Em **Que tipo de dados deseja incluir?**, selecione **Criar logs de dados e Contador de desempenho**.

    ![Imagem do tipo de dados do novo conjunto de coletores de dados](media/atp-traffic-estimation-5.png)

6.  Em **Que contadores de desempenho deseja registrar em log?**, clique em **Adicionar**.

7.  Expanda **Adaptador de Rede**, selecione **Pacotes/s** e escolha a instância apropriada. Se não tiver certeza, você poderá selecionar **&lt;Todas as instâncias&gt;** e clicar em **Adicionar** e **OK**.

    > [!NOTE]
    > Para executar essa operação em uma linha de comando, execute `ipconfig /all` para ver o nome do adaptador e a configuração.

    ![Adicionar imagem dos contadores de desempenho](media/atp-traffic-estimation-7.png)

8.  Altere o **Intervalo de amostragem** para **cinco segundos**.

9. Defina o local onde você deseja que os dados sejam salvos.

10. Em **Criar conjunto de coletores de dados**, selecione **Iniciar conjunto de coletores de dados agora** e clique em **Concluir**.

    Agora, você deverá ver o conjunto de coletores de dados que criou com um triângulo verde, indicando que ele está funcionando.

11. Após 24 horas, pare o conjunto de coletores de dados clicando com o botão direito do mouse no conjunto de coletores de dados e selecionando **Parar**.

    ![Imagem ao parar o conjunto de coletores de dados](media/atp-traffic-estimation-12.png)

12. No Explorador de Arquivos, navegue até a pasta em que o arquivo .blg foi salvo e clique duas vezes nele para abri-lo no Monitor de Desempenho.

13. Selecione o contador Pacotes/s e registre os valores médio e máximo.

    ![Imagem do contador de pacotes por segundo](media/atp-traffic-estimation-14.png)



## <a name="see-also"></a>Consulte Também
- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/aatpsizingtool)
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Arquitetura do Azure ATP](atp-architecture.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)
