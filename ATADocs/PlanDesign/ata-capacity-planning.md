---
# required metadata

title: Planejando a implantação do ATA | Microsoft Advanced Threat Analytics
description: Ajuda você a planejar a implantação e decidir quantos servidores ATA serão necessários para oferecer suporte à sua rede
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 279d79f2-962c-4c6f-9702-29744a5d50e2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Planejamento da capacidade de ATA
Este tópico ajuda a determinar quantos servidores ATA serão necessários para oferecer suporte à sua rede, inclusive a entender quantos Gateways do ATA e Gateways Lightweight do ATA você precisa, bem como a capacidade do servidor para suo Centro do ATA e Gateways do ATA.

## Dimensionamento da Central de ATA
A Central de ATA requer um mínimo recomendado de 30 dias de dados para a análise de comportamento do usuário. O espaço em disco necessário para o banco de dados do ATA, um por controlador de domínio, é definido abaixo. Se você tiver vários controladores de domínio, some o espaço em disco necessário por controlador para calcular a quantidade total de espaço necessário para o banco de dados do ATA.

|Pacotes por segundo&#42;|CPU (núcleos&#42;&#42;)|Memória (GB)|Armazenamento de bancos de dados por dia (GB)|Armazenamento de bancos de dados por mês (GB)|IOPS&#42;&#42;&#42;|
|---------------------------|-------------------------|-------------------|---------------------------------|-----------------------------------|-----------------------------------|
|1,000|2|32|0.3|9|30 (100)
|10.000|4|48|3|90|200 (300)
|40.000|8|64|12|360|500 (1.000)
|100,000|12|96|30|900|1.000 (1.500)
|400.000|40|128|120|1.800|2.000 (2.500)
&#42;Número médio diário total de pacotes por segundo de todos os controladores de domínio sendo monitorados por todos os Gateways de ATA.

&#42;&#42;Isto inclui os núcleos físicos, não os núcleos com hyper-threading.

&#42;&#42;&#42;Média dos números (Números de pico)
> [!NOTE]
> -   A Central do ATA pode lidar com um máximo agregado de 400.000 FPS (quadros por segundo) de todos os controladores de domínio monitorados.
> -   O volume de armazenamento ditado aqui são os valores net que você sempre deve levar em consideração para o crescimento futuro e verificar se o disco no qual o banco de dados reside tem, pelo menos, 20% de espaço livre.
> -   Se o espaço livre chegar a um mínimo de 20% ou 100 GB, o conjunto mais antigo de dados será excluído. Isso continuará a ocorrer até que somente dois dias de dados, 5% ou 50 GB de espaço livre permaneça no ponto em que a coleta de dados irá parar de funcionar.
> -  A latência de armazenamento para a leitura e a gravação das atividades deve estar abaixo de 10 ms.
> -  A taxa entre as atividades de leitura e gravação é de, aproximadamente, 1:3 abaixo de 100.000 pacotes por segundo e 1:6 acima de 100.000 pacotes por segundo.

## Escolhendo o tipo certo de gateway para sua implantação
É recomendável usar um Gateway Lightweight do ATA em vez de um Gateway do ATA sempre que possível, desde que os controladores de domínio cumpram a tabela de dimensionamento listada abaixo.
A maioria dos controladores de domínio pode e deve ser coberta com o Gateway Lightweight do ATA, a menos que eles não atendam aos requisitos na [tabela de dimensionamento do Gateway Lightweight do ATA](#ata-lightweight-gateway-sizing).
Veja a seguir os exemplos de cenários nos quais todos os controladores de domínio devem ser cobertos pelos Gateways Lightweight do ATA:

-   Sites da filial
-   Controladores de domínio virtuais de qualquer fornecedor IaaS


## Dimensionamento do Gateway Lightweight do ATA
É recomendável usar um Gateway Lightweight do ATA em vez de um Gateway do ATA sempre que possível, desde que os controladores de domínio cumpram a tabela de dimensionamento listada aqui.

Um Gateway Lightweight do ATA pode oferecer suporte ao monitoramento de um controlador de domínio com base na quantidade de tráfego de rede gerado pelo controlador de domínio. 

|Pacotes por segundo&#42;|CPU (núcleos&#42;&#42;)|Memória (GB)&#42;&#42;&#42;|
|---------------------------|-------------------------|---------------|
|1,000|2|6|
|5,000|6|16|
    |10.000|10|24|

&#42;Número total de pacotes por segundo no controlador de domínio sendo monitorado pelo Gateway Lightweight do ATA específico.

&#42;&#42;Quantidade total de núcleos não hyper-threaded que esse controlador de domínio tem instalada.<br>Embora o hyper-threading seja aceitável para o Gateway Lightweight do ATA, ao planejar a capacidade, você deve contar os núcleos reais, e não os núcleos hyper-threaded.

&#42;&#42;&#42;Quantidade total de memória que esse controlador de domínio tem instalada.
> [!NOTE]   Se o controlador de domínio não tiver a quantidade necessária de recursos exigida pelo Gateway Lightweight do ATA, o desempenho do controlador de domínio não será afetado, mas o Gateway Lightweight do ATA pode não operar conforme o esperado.


## Dimensionamento do Gateway de ATA

Considere o seguinte ao decidir quantos Gateways do ATA implantar.

A maioria dos controladores de domínio pode ser coberta por um Gateway Lightweight do ATA, o que deve ser planejado de acordo com a tabela de dimensionamento do Gateway Lightweight do ATA, acima.

Se os Gateways do ATA ainda forem necessários, veja a seguir as considerações da quantidade exigida:<br>

-   **Florestas e domínios do Active Directory**<br>
    O ATA pode monitorar o tráfego de vários domínios de uma única floresta do Active Directory. Monitorar várias florestas do Active Directory exige implantações separadas do ATA. Uma única implantação do ATA não deve ser configurada para monitorar o tráfego de rede dos controladores de domínio de diferentes florestas.

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



## Estimativa de tráfego do controlador de domínio
Há várias ferramentas que você pode usar para descobrir a média de pacotes por segundo dos controladores de domínio. Se você não tiver as ferramentas que acompanham este contador, poderá usar o Monitor de Desempenho para coletar as informações necessárias.

Para determinar os pacotes por segundo, execute o seguinte em cada controlador de domínio:

1.  Abra o Monitor de Desempenho.

    ![Imagem do monitor de desempenho](media/ATA-traffic-estimation-1.png)

2.  Expanda **Conjuntos de Coletores de Dados**.

    ![Imagem dos conjuntos de coletores de dados](media/ATA-traffic-estimation-2.png)

3.  Clique com botão direito do mouse em **Definido pelo Usuário** e selecione **Novo** &gt; **Conjunto de Coletores de Dados**.

    ![Imagem do novo conjunto de coletores de dados](media/ATA-traffic-estimation-3.png)

4.  Insira um nome para o conjunto de coletores e selecione **Criar Manualmente (Avançado)**.

5.  Em **Qual tipo de dados você deseja incluir?**, selecione  **Criar logs de dados e Contador de desempenho**.

    ![Imagem do tipo de dados do novo conjunto de coletores de dados](media/ATA-traffic-estimation-5.png)

6.  Em **Quais contadores de desempenho você gostaria de registrar**, clique em **Adicionar**.

7.  Expanda **Adaptador de Rede**, selecione **Pacotes/s** e escolha a instância apropriada. Se não tiver certeza, você poderá selecionar **&lt;Todas as instâncias&gt;** e clicar em **Adicionar** e **OK**.

    > [!NOTE] Para fazer isso, em uma linha de comando, execute `ipconfig /all` para ver o nome do adaptador e a configuração.

    ![Adicionar imagem dos contadores de desempenho](media/ATA-traffic-estimation-7.png)

8.  Altere o **Intervalo de amostragem** para **1 segundo**.

9. Defina o local onde você deseja que os dados sejam salvos.

10. Em **Criar conjunto de coletores de dados**,  selecione **Iniciar conjunto de coletores de dados agora** e clique em **Concluir**.

    Agora, você deverá ver o conjunto de coletores de dados que acabou de criar com um triângulo verde, indicando que ele está funcionando.

11. Após 24 horas, pare o conjunto de coletores de dados clicando com o botão direito do mouse no conjunto de coletores de dados e selecionando **Parar**.

    ![Imagem ao parar o conjunto de coletores de dados](media/ATA-traffic-estimation-12.png)

12. No Explorador de Arquivos, navegue até a pasta onde o arquivo. blg foi salvo e clique duas vezes nele para abri-lo no Monitor de Desempenho.

13. Selecione o contador Pacotes/s e registre os valores médio e máximo.

    ![Imagem do contador de pacotes por segundo](media/ATA-traffic-estimation-14.png)

## Consulte também
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Arquitetura do ATA](ata-architecture.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


