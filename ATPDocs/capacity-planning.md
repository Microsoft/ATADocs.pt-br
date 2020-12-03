---
title: Planejando sua implantação do Microsoft defender para identidade
description: Ajuda a planejar sua implantação e a decidir quantos Microsoft defender for Identity Servers serão necessários para dar suporte à sua rede
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: a5db3865b75e79a7b5f69dd5223e27497cc7ae18
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96544225"
---
# <a name="plan-capacity-for-product-long"></a>Planejar capacidade para [!INCLUDE [Product long](includes/product-long.md)]

Neste guia, você determina a quantidade de [!INCLUDE [Product long](includes/product-long.md)] sensores de que precisa.

## <a name="prerequisites"></a>Pré-requisitos

- Baixe a [ [!INCLUDE [Product short](includes/product-short.md)] ferramenta de dimensionamento](https://aka.ms/aatpsizingtool).
- Examine o artigo [Arquitetura do [!INCLUDE [Product short](includes/product-short.md)]](architecture.md).
- Examine o artigo [Pré-requisitos do [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md).

## <a name="use-the-sizing-tool"></a>Usar a ferramenta de dimensionamento

A maneira recomendada e mais simples de determinar a capacidade para sua [!INCLUDE [Product short](includes/product-short.md)] implantação é usar a [!INCLUDE [Product short](includes/product-short.md)] ferramenta de dimensionamento. Caso isso não seja possível, colete informações sobre o tráfego manualmente. Para saber mais sobre o método manual, confira a seção [Estimador de tráfego do controlador de domínio](#manual-sizing), no final deste artigo.

1. Execute a [!INCLUDE [Product short](includes/product-short.md)] ferramenta de dimensionamento, **TriSizingTool.exe**, no arquivo zip que você baixou.
1. Quando concluir a execução da ferramenta, abra os resultados de arquivo do Excel.
1. No arquivo do Excel, localize e clique na planilha **Resumo do ATP do Azure**. A outra planilha não é necessária, pois ela se destina ao planejamento do ATA.
    ![Ferramenta de planejamento de capacidade de amostra](media/capacity-tool.png)

1. Localize o campo **Pacotes ocupados/s**, na tabela do sensor do ATP do Azure, no arquivo de resultados do Excel, e anote isso.
1. Corresponda o campo **pacotes ocupados/s** ao campo **pacotes por segundo** na seção [ [!INCLUDE [Product short](includes/product-short.md)] tabela do sensor](#sizing) deste artigo. Use os campos para determinar a capacidade de memória e CPU que será usada pelo sensor.

## <a name="product-short-sensor-sizing"></a><a name="sizing"></a>[!INCLUDE [Product short](includes/product-short.md)]dimensionamento do sensor

Um [!INCLUDE [Product short](includes/product-short.md)] sensor pode dar suporte ao monitoramento de um controlador de domínio com base na quantidade de tráfego de rede que o controlador de domínio gera. A tabela a seguir representa uma estimativa. O valor final que o sensor analisa depende da quantidade de tráfego e da distribuição desse tráfego.

A capacidade da CPU e da memória RAM a seguir se refere ao **consumo do próprio sensor**, e não à capacidade do controlador de domínio.

|Pacotes por segundo|CPU (núcleos)\*|Memória\*\* (GB)|
|----|----|-----|
|0 - 1k|0.25|2.50|
|1k - 5k|0.75|6.00|
|5k - 10k|1.00|6.50|
|10k - 20k|2.00|9.00|
|20k - 50k|3.50|9.50|
|50k - 75k |3.50|9.50|
|75k - 100k|3.50|9.50|

\* Isso inclui os núcleos físicos, não os núcleos com hyper-threading.  
\*\* Memória RAM

Quando determinar o dimensionamento, observe os seguintes itens:

- Número total de núcleos a serem usados pelo serviço de sensor.  
Recomendamos não trabalhar com núcleos hyper-threaded. Trabalhar com núcleos de Hyper-thread pode resultar em [!INCLUDE [Product short](includes/product-short.md)] problemas de integridade do sensor.
- Número total de memória a ser usada pelo serviço de sensor.
- Se o controlador de domínio não tiver os recursos exigidos pelo [!INCLUDE [Product short](includes/product-short.md)] sensor, o desempenho do controlador de domínio não será afetado. No entanto, o [!INCLUDE [Product short](includes/product-short.md)] sensor pode não funcionar conforme o esperado.
- Na execução como uma máquina virtual, toda a memória precisa ser alocada para a máquina virtual em todos os momentos.
- Para obter um desempenho ideal, defina a **opção de energia** do [!INCLUDE [Product short](includes/product-short.md)] sensor para **alto desempenho**.
- São necessários no mínimo dois núcleos e
- Um mínimo de 6 GB de espaço no disco rígido é necessário, 10 GB é recomendado, incluindo o espaço necessário para os [!INCLUDE [Product short](includes/product-short.md)] binários e logs.

### <a name="dynamic-memory"></a>Memória dinâmica

> [!NOTE]
> Na execução como uma VM (máquina virtual), toda a memória precisa ser alocada para a VM em todos os momentos.

|VM em execução em|Descrição|
|------------|-------------|
|Hyper-V|Garanta que a opção **Habilitar Memória Dinâmica** não esteja habilitada para a VM.|
|VMWare|Verifique se a quantidade de memória configurada e a memória reservada são iguais ou selecione a seguinte opção na configuração da VM – **Reservar toda a memória de convidado (Tudo bloqueado)** .|
|Outro host de virtualização|Confira a documentação fornecida pelo fornecedor sobre como garantir que a memória seja totalmente alocada para a VM em todos os momentos. |

## <a name="domain-controller-traffic-estimation"></a><a name="manual-sizing"></a> Estimativa de tráfego do controlador de domínio

Se, por alguma razão, você não puder usar a [!INCLUDE [Product short](includes/product-short.md)] ferramenta de dimensionamento, reúna manualmente as informações do contador de pacotes/s de todos os controladores de domínio. Reúna as informações durante 24 horas com um pequeno intervalo de coleta de aproximadamente cinco segundos. Em seguida, calcule a média diária e a média mais ocupada do período (15 minutos) de cada controlador de domínio. As seções a seguir apresentam instruções de como coletar o contador de pacotes/s de um controlador de domínio.

Há várias ferramentas que você pode usar para descobrir a média de pacotes por segundo dos controladores de domínio. Caso não tenha as ferramentas que controlam este contador, use o monitor de desempenho para coletar as informações necessárias.

Para determinar os pacotes por segundo, faça os seguintes procedimentos em cada controlador de domínio:

1. Abra o Monitor de Desempenho.

    ![Imagem do monitor de desempenho](media/traffic-estimation-1.png)

1. Expanda **Conjuntos de Coletores de Dados**.

    ![Imagem dos conjuntos de coletores de dados](media/traffic-estimation-2.png)

1. Clique com botão direito do mouse em **Usuário Definido** e selecione **Novo** &gt; **Conjunto de Coletores de Dados**.

    ![Imagem do novo conjunto de coletores de dados](media/traffic-estimation-3.png)

1. Insira um nome para o conjunto de coletores e selecione **Criar Manualmente (Avançado)** .

1. Em **Que tipo de dados deseja incluir?** , selecione **Criar logs de dados e Contador de desempenho**.

    ![Imagem do tipo de dados do novo conjunto de coletores de dados](media/traffic-estimation-5.png)

1. Em **Que contadores de desempenho deseja registrar em log?** , clique em **Adicionar**.

1. Expanda **Adaptador de Rede**, selecione **Pacotes/s** e escolha a instância apropriada. Se não tiver certeza, selecione **&lt;Todas as instâncias&gt;** , clique em **Adicionar** e em **OK**.

    > [!NOTE]
    > Para executar essa operação em uma linha de comando, execute `ipconfig /all` para ver o nome do adaptador e a configuração.

    ![Adicionar imagem dos contadores de desempenho](media/traffic-estimation-7.png)

1. Altere o **Intervalo de amostragem** para **cinco segundos**.

1. Defina o local onde você deseja que os dados sejam salvos.

1. Em **Criar conjunto de coletores de dados**, selecione **Iniciar conjunto de coletores de dados agora** e clique em **Concluir**.

    Agora, você deverá ver o conjunto de coletores de dados criado com um triângulo verde, indicando que ele está funcionando.

1. Após 24 horas, pare o conjunto de coletores de dados clicando com o botão direito do mouse no conjunto de coletores de dados e selecionando **Parar**.

    ![Imagem ao parar o conjunto de coletores de dados](media/traffic-estimation-12.png)

1. No Explorador de Arquivos, navegue até a pasta em que o arquivo .blg foi salvo e clique duas vezes nele para abri-lo no Monitor de Desempenho.

1. Selecione o contador Pacotes/s e registre os valores médio e máximo.

    ![Imagem do contador de pacotes por segundo](media/traffic-estimation-14.png)

## <a name="next-steps"></a>Próximas etapas

Neste guia, você determinou quantos [!INCLUDE [Product short](includes/product-short.md)] sensores precisa. Determinou também o dimensionamento dos sensores. Continue para o guia de [!INCLUDE [Product short](includes/product-short.md)] início rápido criar uma instância.

> [!div class="nextstepaction"]
> [Criar sua [!INCLUDE [Product short](includes/product-short.md)] instância](install-step1.md)

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o [!INCLUDE [Product short](includes/product-short.md)] e a segurança relacionada com outras pessoas? Participe da Comunidade [[!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity) hoje mesmo!
