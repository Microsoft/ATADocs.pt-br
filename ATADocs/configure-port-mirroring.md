---
title: Configurar o espelhamento de porta ao implantar a análise avançada de ameaças
description: Descreve as opções de espelhamento de porta e como configurá-las para o ATA
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: cdaddca3-e26e-4137-b553-8ed3f389c460
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: d6d63077d0e8c102d9237fce21677608335e8c60
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88954690"
---
# <a name="configure-port-mirroring"></a>Configurar o espelhamento de porta

*Aplica-se a: Advanced Threat Analytics versão 1.9*

> [!NOTE] 
> Este artigo somente é relevante se você implanta Gateways do ATA em vez de Gateways Lightweight do ATA. Para determinar se você precisa usar gateways do ATA, consulte [escolhendo os gateways corretos para sua implantação](ata-capacity-planning.md#choosing-the-right-gateway-type-for-your-deployment).

A fonte de dados principal usada pelo ATA é uma inspeção profunda de pacotes do tráfego de rede para e dos controladores de domínio. Para que o ATA veja o tráfego de rede, você deve configurar o espelhamento de porta ou usar uma TAP de Rede.

Para o espelhamento de porta, configure **espelhamento de porta** para cada controlador de domínio a ser monitorado, como a **origem** do tráfego de rede. Normalmente, você precisa trabalhar com a equipe de virtualização ou de rede para configurar o espelhamento de porta.
Para saber mais, veja a documentação do fornecedor.

Seus controladores de domínio e Gateways do ATA podem ser físicos ou virtuais. Veja a seguir métodos comuns de espelhamento de porta e algumas considerações. Para saber mais, veja a documentação de produtos para servidores de virtualização ou comutador. O fabricante do comutador pode usar terminologias distintas.

**Switched Port Analyzer (SPAN)** – Copia o tráfego de rede de uma ou mais portas de comutador para outra porta de comutador no mesmo comutador. Tanto o Gateway do ATA quanto os controladores de domínio devem estar conectados ao mesmo comutador físico.

**Remote Switch Port Analyzer (RSPAN)**  – Permite que você monitore o tráfego de rede das portas de origem distribuídas em vários comutadores físicos. O RSPAN copia o tráfego de origem em uma VLAN especial configurada com RSPAN. Essa VLAN precisa ser truncada com os outros comutadores envolvidos. RSPAN funciona na Camada 2.

**Encapsulated Remote Switch Port Analyzer (ERSPAN)** – É uma tecnologia da Cisco que funciona na Camada 3. O ERSPAN permite que você monitore o tráfego entre comutadores, sem a necessidade de troncos de VLAN. O ERSPAN usa o recurso GRE (encapsulamento de roteamento genérico) para copiar o tráfego de rede monitorado. Atualmente, o ATA não pode receber o tráfego do ERSPAN diretamente. Para que o ATA trabalhe com o tráfego do ERSPAN, um comutador ou roteador que pode desencapsular o tráfego deve ser configurado como o destino do ERSPAN onde o tráfego é desencapsulado. Em seguida, configure o comutador ou roteador para encaminhar o tráfego desencapsulado para o Gateway do ATA usando SPAN ou RSPAN.

> [!NOTE]
> Se o controlador de domínio que está passando por espelhamento de porta estiver conectado por um link de WAN, verifique se o link de WAN pode lidar com a carga adicional do tráfego do ERSPAN.
> A ATA dá suporte ao monitoramento de tráfego somente quando o tráfego alcança a NIC e o controlador de domínio da mesma maneira. ATA não dá suporte ao monitoramento de tráfego quando o tráfego é dividido em portas diferentes.

## <a name="supported-port-mirroring-options"></a>Opções de espelhamento de porta com suporte

|Gateway de ATA|Controlador de Domínio|Considerações|
|---------------|---------------------|------------------|
|Máquina|Virtual no mesmo host|O comutador virtual precisa oferecer suporte ao espelhamento de porta.<br /><br />Mover uma das máquinas virtuais para outro host por si só pode quebrar o espelhamento de porta.|
|Máquina|Virtuais em hosts diferentes|Verifique se o comutador virtual oferece suporte a esse cenário.|
|Máquina|Físico|Exige um adaptador de rede dedicado, caso contrário o ATA verá todo o tráfego que chega e sai do host, até mesmo o tráfego que ele envia ao Centro do ATA.|
|Físico|Máquina|Verifique se o comutador virtual oferece suporte a este cenário, e se a configuração de espelhamento de porta em seus comutadores físicos tem base no cenário:<br /><br />Se o host virtual estiver no mesmo comutador físico, você precisará configurar um span no nível do comutador.<br /><br />Se o host virtual estiver em um comutador diferente, você precisará configurar RSPAN ou ERSPAN&#42;.|
|Físico|Físico no mesmo comutador|O comutador físico deve oferecer suporte ao Espelhamento de Porta/SPAN.|
|Físico|Físico em um comutador diferente|Exige que os comutadores físicos ofereçam suporte a RSPAN ou ERSPAN&#42;.|

&#42; O ERSPAN recebe suporte apenas quando o desencapsulamento é executado antes de o tráfego ser analisado pelo ATA.

> [!NOTE]
> Verifique se os controladores de domínio e os Gateways do ATA aos quais eles se conectam estão com seus horários sincronizados com uma diferença de cinco minutos.

**Se você estiver trabalhando com clusters de virtualização:**

- Para cada controlador de domínio em execução no cluster de virtualização em uma máquina virtual com o Gateway do ATA, configure a afinidade entre o controlador de domínio e o Gateway do ATA. Dessa forma, quando o controlador de domínio for para outro host no cluster, o Gateway do ATA o seguirá. Isso funciona bem quando há alguns controladores de domínio.

> [!NOTE]
> Caso seu ambiente dê suporte a RSPAN (virtual para virtual em hosts diferentes), você não precisa se preocupar com afinidade.

- Para verificar se os Gateways do ATA estão com um tamanho correto que os permita lidar com o monitoramento de todos os controladores de domínio, tente esta opção: instalar uma máquina virtual em cada host de virtualização e instalar um Gateway do ATA em cada host. Configure cada Gateway do ATA para monitorar todos os controladores de domínio executados no cluster. Dessa forma, qualquer host no qual os controladores de domínio são executados será monitorado.

Depois de configurar o espelhamento de porta, verifique se está funcionando antes de instalar o Gateway do ATA.

## <a name="see-also"></a>Consulte Também
- [Validação do espelhamento de porta](validate-port-mirroring.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
