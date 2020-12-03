---
title: Configurar o espelhamento de porta ao implantar o Microsoft Defender para Identidade
description: Descreve as opções de espelhamento de porta e como configurá-las no Microsoft Defender para Identidade
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 72b453c5e90b46f432bd7eb89572e519d50d9e4a
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96544038"
---
# <a name="configure-port-mirroring"></a>Configurar o espelhamento de porta

Este artigo será relevante apenas se você implantar sensores autônomos do [!INCLUDE [Product long](includes/product-long.md)] em vez de sensores do [!INCLUDE [Product short](includes/product-short.md)].

> [!NOTE]
> Os sensores autônomos do [!INCLUDE [Product short](includes/product-short.md)] não dão suporte à coleção de entradas de log do ETW (Rastreamento de Eventos para Windows) que fornecem dados para várias detecções. Para cobertura completa do seu ambiente, recomendamos implantar o sensor do [!INCLUDE [Product short](includes/product-short.md)].

A fonte de dados principal usada pelo [!INCLUDE [Product short](includes/product-short.md)] é uma inspeção profunda de pacotes do tráfego de rede proveniente dos controladores de domínio e direcionado a eles. Para que o [!INCLUDE [Product short](includes/product-short.md)] veja o tráfego de rede, você deve configurar o espelhamento de porta ou usar um TAP de rede.

Para o espelhamento de porta, configure **espelhamento de porta** para cada controlador de domínio a ser monitorado, como a **origem** do tráfego de rede. Normalmente, você precisa trabalhar com a equipe de virtualização ou de rede para configurar o espelhamento de porta.
Para saber mais, veja a documentação do fornecedor.

Seus controladores de domínio e o sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] podem ser físicos ou virtuais. Veja a seguir métodos comuns de espelhamento de porta e algumas considerações. Para saber mais, veja a documentação de produtos para servidores de virtualização ou comutador. O fabricante do comutador pode usar terminologias distintas.

**Switched Port Analyzer (SPAN)** – Copia o tráfego de rede de uma ou mais portas de comutador para outra porta de comutador no mesmo comutador. Tanto o sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] quanto os controladores de domínio devem estar conectados ao mesmo comutador físico.

**Remote Switch Port Analyzer (RSPAN)**  – Permite que você monitore o tráfego de rede das portas de origem distribuídas em vários comutadores físicos. O RSPAN copia o tráfego de origem em uma VLAN especial configurada com RSPAN. Essa VLAN precisa ser truncada com os outros comutadores envolvidos. RSPAN funciona na Camada 2.

**Encapsulated Remote Switch Port Analyzer (ERSPAN)** – É uma tecnologia da Cisco que funciona na Camada 3. O ERSPAN permite que você monitore o tráfego entre comutadores, sem a necessidade de troncos de VLAN. O ERSPAN usa o recurso GRE (encapsulamento de roteamento genérico) para copiar o tráfego de rede monitorado. Atualmente, o [!INCLUDE [Product short](includes/product-short.md)] não pode receber o tráfego do ERSPAN diretamente. Para que o [!INCLUDE [Product short](includes/product-short.md)] trabalhe com o tráfego do ERSPAN, um comutador ou roteador que possa desencapsular o tráfego deve ser configurado como o destino do ERSPAN em que esse desencapsulamento será feito. Em seguida, configure o comutador ou roteador para encaminhar o tráfego desencapsulado para o sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] usando SPAN ou RSPAN.

> [!NOTE]
> Se o controlador de domínio que está passando por espelhamento de porta estiver conectado por um link de WAN, verifique se o link de WAN pode lidar com a carga adicional do tráfego do ERSPAN.
> O [!INCLUDE [Product short](includes/product-short.md)] dá suporte ao monitoramento de tráfego somente quando o tráfego alcança a NIC e o controlador de domínio da mesma maneira. O [!INCLUDE [Product short](includes/product-short.md)] não dá suporte ao monitoramento de tráfego quando o tráfego é dividido em portas diferentes.

## <a name="supported-port-mirroring-options"></a>Opções de espelhamento de porta com suporte

|Sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)]|Controlador de Domínio|Considerações|
|---------------|---------------------|------------------|
|Máquina|Virtual no mesmo host|O comutador virtual precisa oferecer suporte ao espelhamento de porta.<br /><br />Mover uma das máquinas virtuais para outro host por si só pode quebrar o espelhamento de porta.|
|Máquina|Virtuais em hosts diferentes|Verifique se o comutador virtual oferece suporte a esse cenário.|
|Máquina|Físico|Exige um adaptador de rede dedicado, caso contrário, o [!INCLUDE [Product short](includes/product-short.md)] verá todo o tráfego que chega e sai do host, até mesmo o tráfego que ele envia ao serviço de nuvem do [!INCLUDE [Product short](includes/product-short.md)].|
|Físico|Máquina|Verifique se o comutador virtual oferece suporte a este cenário, e se a configuração de espelhamento de porta em seus comutadores físicos tem base no cenário:<br /><br />Se o host virtual estiver no mesmo comutador físico, você precisará configurar um span no nível do comutador.<br /><br />Se o host virtual estiver em um comutador diferente, você precisará configurar RSPAN ou ERSPAN&#42;.|
|Físico|Físico no mesmo comutador|O comutador físico deve oferecer suporte ao Espelhamento de Porta/SPAN.|
|Físico|Físico em um comutador diferente|Exige que os comutadores físicos ofereçam suporte a RSPAN ou ERSPAN&#42;.|

&#42; O ERSPAN tem suporte apenas quando o desencapsulamento é executado antes que o tráfego seja analisado pelo [!INCLUDE [Product short](includes/product-short.md)].

> [!NOTE]
> Verifique se os controladores de domínio e o sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] ao qual eles se conectam estão com os horários sincronizados com uma diferença de cinco minutos.

**Se você estiver trabalhando com clusters de virtualização:**

- Para cada controlador de domínio em execução no cluster de virtualização em uma máquina virtual com o sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)], configure a afinidade entre o controlador de domínio e o sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)]. Dessa forma, quando o controlador de domínio for para outro host no cluster, o sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] o seguirá. Isso funciona bem quando há alguns controladores de domínio.

  > [!NOTE]
  > Caso seu ambiente dê suporte a RSPAN (virtual para virtual em hosts diferentes), você não precisa se preocupar com afinidade.

- Para garantir que o sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] esteja dimensionado corretamente para lidar com o monitoramento de todos os controladores de domínio por si só, tente a seguinte opção: instale uma máquina virtual em cada host de virtualização e um sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] em cada host. Configure cada sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] para monitorar todos os controladores de domínio executados no cluster. Dessa forma, qualquer host no qual os controladores de domínio são executados será monitorado.

Depois de configurar o espelhamento de porta, verifique se ele está funcionando antes de instalar o sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)].

## <a name="see-also"></a>Consulte Também

- [Configurar o encaminhamento de eventos](configure-event-forwarding.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
