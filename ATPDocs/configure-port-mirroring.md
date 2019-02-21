---
title: Configurar o espelhamento de porta ao implantar a Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Descreve as opções de espelhamento de porta e como configurá-las para o Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 10/4/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 9ec7eb4c-3cad-4543-bbf0-b951d8fc8ffe
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e8ae465094c6b3413b266b26cf4790339362ebac
ms.sourcegitcommit: c48db18274edb2284e281960c6262d97f96e01d2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56263906"
---
# <a name="configure-port-mirroring"></a>Configurar o espelhamento de porta
> [!NOTE] 
> Este artigo será relevante apenas se você implantar sensores autônomos do Azure ATP, em vez de sensores do Azure ATP. Para determinar se você precisa usar sensores autônomos do Azure ATP, confira [Choosing the right sensors for your deployment](atp-capacity-planning.md#choosing-the-right-sensor-type-for-your-deployment) (Escolhendo os sensores certos para sua implantação).
 
A fonte de dados principal usada pelo Azure ATP é uma inspeção profunda de pacotes do tráfego de rede para e dos controladores de domínio. Para que o Azure ATP veja o tráfego de rede, você deve configurar o espelhamento de porta ou usar uma TAP de Rede.

Para o espelhamento de porta, configure **espelhamento de porta** para cada controlador de domínio a ser monitorado, como a **origem** do tráfego de rede. Normalmente, você precisa trabalhar com a equipe de virtualização ou de rede para configurar o espelhamento de porta.
Para saber mais, veja a documentação do fornecedor.

Seus controladores de domínio e o sensor autônomo do Azure ATP podem ser físicos ou virtuais. Veja a seguir métodos comuns de espelhamento de porta e algumas considerações. Para saber mais, veja a documentação de produtos para servidores de virtualização ou comutador. O fabricante do comutador pode usar terminologias distintas.

**Switched Port Analyzer (SPAN)** – Copia o tráfego de rede de uma ou mais portas de comutador para outra porta de comutador no mesmo comutador. Tanto o sensor autônomo do Azure ATP quanto os controladores de domínio devem estar conectados ao mesmo comutador físico.

**Remote Switch Port Analyzer (RSPAN)**  – Permite que você monitore o tráfego de rede das portas de origem distribuídas em vários comutadores físicos. O RSPAN copia o tráfego de origem em uma VLAN especial configurada com RSPAN. Essa VLAN precisa ser truncada com os outros comutadores envolvidos. RSPAN funciona na Camada 2.

**Encapsulated Remote Switch Port Analyzer (ERSPAN)** – É uma tecnologia da Cisco que funciona na Camada 3. O ERSPAN permite que você monitore o tráfego entre comutadores, sem a necessidade de troncos de VLAN. O ERSPAN usa o recurso GRE (encapsulamento de roteamento genérico) para copiar o tráfego de rede monitorado. Atualmente, o Azure ATP não pode receber o tráfego do ERSPAN diretamente. Para que o Azure ATP trabalhe com o tráfego do ERSPAN, um comutador ou roteador que pode desencapsular o tráfego deve ser configurado como o destino do ERSPAN em que o tráfego é desencapsulado. Em seguida, configure o comutador ou roteador para encaminhar o tráfego desencapsulado para o sensor autônomo do ATP do Azure usando SPAN ou RSPAN.

> [!NOTE]
> Se o controlador de domínio que está passando por espelhamento de porta estiver conectado por um link de WAN, verifique se o link de WAN pode lidar com a carga adicional do tráfego do ERSPAN.
> O Azure ATP dá suporte ao monitoramento de tráfego somente quando o tráfego alcança a NIC e o controlador de domínio da mesma maneira. O Azure ATP não dá suporte ao monitoramento de tráfego quando o tráfego é dividido em portas diferentes.

## <a name="supported-port-mirroring-options"></a>Opções de espelhamento de porta com suporte

|Sensor autônomo do Azure ATP|Controlador de Domínio|Considerações|
|---------------|---------------------|------------------|
|Máquina|Virtual no mesmo host|O comutador virtual precisa oferecer suporte ao espelhamento de porta.<br /><br />Mover uma das máquinas virtuais para outro host por si só pode quebrar o espelhamento de porta.|
|Máquina|Virtuais em hosts diferentes|Verifique se o comutador virtual oferece suporte a esse cenário.|
|Máquina|Físico|Exige um adaptador de rede dedicado. Caso contrário, o Azure ATP verá todo o tráfego que chega e sai do host, até mesmo o tráfego que ele envia ao serviço de nuvem do Azure ATP.|
|Físico|Máquina|Verifique se o comutador virtual oferece suporte a este cenário, e se a configuração de espelhamento de porta em seus comutadores físicos tem base no cenário:<br /><br />Se o host virtual estiver no mesmo comutador físico, você precisará configurar um span no nível do comutador.<br /><br />Se o host virtual estiver em um comutador diferente, você precisará configurar RSPAN ou ERSPAN&#42;.|
|Físico|Físico no mesmo comutador|O comutador físico deve oferecer suporte ao Espelhamento de Porta/SPAN.|
|Físico|Físico em um comutador diferente|Exige que os comutadores físicos ofereçam suporte a RSPAN ou ERSPAN&#42;.|

&#42; O ERSPAN tem suporte apenas quando o desencapsulamento é executado antes de o tráfego ser analisado pelo ATP.

> [!NOTE]
> Certifique-se de que os controladores de domínio e o sensor autônomo do Azure ATP ao qual eles se conectam tenham os horários sincronizados com uma diferença de cinco minutos.

**Se você estiver trabalhando com clusters de virtualização:**

- Para cada controlador de domínio em execução no cluster de virtualização em uma máquina virtual com o sensor autônomo do Azure ATP, configure a afinidade entre o controlador de domínio e o sensor autônomo do Azure ATP. Dessa forma, quando o controlador de domínio for para outro host no cluster, o sensor autônomo do Azure ATP o seguirá. Isso funciona bem quando há alguns controladores de domínio.

  > [!NOTE]
  > Caso seu ambiente dê suporte a RSPAN (virtual para virtual em hosts diferentes), você não precisa se preocupar com afinidade.
 
- Para garantir que o sensor autônomo do ATP do Azure esteja dimensionado corretamente para lidar com o monitoramento de todos os controladores de domínio por si só, tente esta opção: instale uma máquina virtual em cada host de virtualização e um sensor autônomo do ATP do Azure em cada host. Configure cada sensor autônomo do Azure ATP para monitorar todos os controladores de domínio executados no cluster. Dessa forma, qualquer host no qual os controladores de domínio são executados será monitorado.

Depois de configurar o espelhamento de porta, verifique se ele está funcionando antes de instalar o sensor autônomo do Azure ATP.

## <a name="see-also"></a>Consulte Também
- [Configurar o encaminhamento de eventos](configure-event-forwarding.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
