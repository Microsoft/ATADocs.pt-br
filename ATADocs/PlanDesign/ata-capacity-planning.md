---
# required metadata

title: Planejamento da Capacidade do ATA | Microsoft Advanced Threat Analytics
description: Ajuda a determinar quantos servidores do ATA serão necessários para dar suporte à rede
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
Este tópico ajuda a determinar quantos servidores do ATA serão necessários para dar suporte à rede.

## Dimensionamento da Central de ATA
A Central de ATA requer um mínimo recomendado de 30 dias de dados para a análise de comportamento do usuário. O espaço em disco necessário para o banco de dados do ATA, um por controlador de domínio, é definido abaixo. Se você tiver vários controladores de domínio, some o espaço em disco necessário por controlador para calcular a quantidade total de espaço necessário para o banco de dados do ATA.

|Pacotes por segundo&#42;|CPU (núcleos&#42;&#42;)|Memória (GB)|Armazenamento do SO (GB)|Armazenamento de bancos de dados por dia (GB)|Armazenamento de bancos de dados por mês (GB)|IOPS&#42;&#42;&#42;|
|---------------------------|-------------------------|---------------|-------------------|---------------------------------|-----------------------------------|-----------------------------------|
|1,000|4|48|200|1.5|45|30 (100)
|10.000|4|48|200|15|450|200 (300)
|40.000|8|64|200|60|1.800|500 (1.000)
|100,000|12|96|200|150|4.500|1.000 (1.500)
|200.000|16|128|200|300|9.000|2.000 (2.500)
&#42;Número médio diário total de pacotes por segundo de todos os controladores de domínio sendo monitorados por todos os Gateways de ATA.

&#42;&#42;Isto inclui os núcleos físicos, não os núcleos com hyper-threading.

&#42;&#42;&#42;Média dos números (Números de pico)
> [!NOTE]
> -   A Central de ATA pode lidar com um máximo agregado de 200.000 quadros por segundo (FPS) a partir de todos os controladores de domínio monitorados.
> -   Para as grandes implantações (começando em cerca de 100.000 pacotes por segundo), é necessário que o diário do banco de dados esteja localizado em um disco diferente do banco de dados.
> -   O volume de armazenamento ditado aqui são os valores net que você sempre deve levar em consideração para o crescimento futuro e verificar se o disco no qual o banco de dados reside tem, pelo menos, 20% de espaço livre.
> -   Se o espaço livre atingir um mínimo de 20% ou 100 GB, as 24 horas mais antigas dos dados serão excluídas. Isso continuará a ocorrer até que somente dois dias de dados, 5% ou 50 GB de espaço livre permaneça no ponto em que a coleta de dados irá parar de funcionar.
> -  A latência de armazenamento para a leitura e a gravação das atividades deve estar abaixo de 10 ms.
> -  A taxa entre as atividades de leitura e gravação é de, aproximadamente, 1:3 abaixo de 100.000 pacotes por segundo e 1:6 acima de 100.000 pacotes por segundo.

## Dimensionamento do Gateway de ATA
Um Gateway de ATA pode dar suporte ao monitoramento de vários controladores de domínio, dependendo da quantidade de tráfego de rede dos controladores de domínio sendo monitorados.

|Pacotes por segundo&#42;|CPU (núcleos&#42;&#42;)|Memória (GB)|Armazenamento do SO (GB)|
|---------------------------|-------------------------|---------------|-------------------|
|10.000|4|12|80|
|20.000|8|24|100|
|40.000|16|64|200|
&#42;Número total de pacotes por segundo a partir de todos os controladores de domínio sendo monitorados pelo Gateway do ATA específico.

&#42;A quantidade total de tráfego espelhado pela porta do controlador de domínio não pode exceder a capacidade do NIC de captura no Gateway de ATA.

&#42;&#42;O hyper-threading deve ser desabilitado.

## Estimativa de tráfego do controlador de domínio
Há várias ferramentas que você pode usar para descobrir a média de pacotes por segundo dos controladores de domínio. Se você não tiver as ferramentas que acompanham este contador, poderá usar o Monitor de Desempenho para coletar as informações necessárias.

Para determinar os pacotes por segundo, execute o seguinte em cada controlador de domínio:

1.  Abra o Monitor de Desempenho.

    ![Imagem do monitor de desempenho](media/ATA-traffic-estimation-1.png)

2.  Expanda **Conjuntos de Coletores de Dados**.

    ![Imagem dos conjuntos de coletores de dados](media/ATA-traffic-estimation-2.png)

3.  Clique com botão direito do mouse em **Usuário Definido** e selecione **Novo** &gt; **Conjunto de Coletores de Dados**.

    ![Imagem do novo conjunto de coletores de dados](media/ATA-traffic-estimation-3.png)

4.  Insira um nome para o conjunto de coletores e selecione **Criar Manualmente (Avançado)**.

5.  Em **Qual tipo de dados você deseja incluir?**, selecione  **Criar logs de dados e Contador de desempenho**.

    ![Imagem do tipo de dados do novo conjunto de coletores de dados](media/ATA-traffic-estimation-5.png)

6.  Em **Quais contadores de desempenho você gostaria de registrar**, clique em **Adicionar**.

7.  Expanda **Adaptador de Rede**, selecione **Pacotes/s** e escolha a instância apropriada. Se você não tiver certeza, poderá selecionar **&lt;Todas as instâncias&gt;** e clicar em **Adicionar** e **OK**.

    > [!NOTE]
    > Para fazer isso, em uma linha de comando, execute `ipconfig /all` para ver o nome do adaptador e a configuração.

    ![Adicionar imagem dos contadores de desempenho](media/ATA-traffic-estimation-7.png)

8.  Altere o **Intervalo de amostragem** para **1 segundo**.

9. Defina o local onde você deseja que os dados sejam salvos.

10. Em **Criar conjunto de coletores de dados**,  selecione **Iniciar conjunto de coletores de dados agora** e clique em **Concluir**.

    Agora, você deverá ver o conjunto de coletores de dados que acabou de criar com um triângulo verde, indicando que ele está funcionando.

11. Após 24 horas, pare o conjunto de coletores de dados clicando com o botão direito do mouse no conjunto de coletores de dados e selecionando **Parar**

    ![Imagem ao parar o conjunto de coletores de dados](media/ATA-traffic-estimation-12.png)

12. No Explorador de Arquivos, navegue até a pasta onde o arquivo. blg foi salvo e clique duas vezes nele para abri-lo no Monitor de Desempenho.

13. Selecione o contador Pacotes/s e registre os valores médio e máximo.

    ![Imagem do contador de pacotes por segundo](media/ATA-traffic-estimation-14.png)

## Consulte também
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Arquitetura do ATA](/advanced-threat-analytics/Understand/ata-architecture)
- [Para obter suporte, confira nosso fórum!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


