---
title: Solução de problemas conhecidos da ATP do Azure | Microsoft Docs
description: Descreve como solucionar problemas de inicialização na ATP do Azure.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/10/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 23386e36-2756-4291-923f-fa8607b5518a
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2112e9fea1f316ff12d87b3a477b78bff4457a5f
ms.sourcegitcommit: e0209c6db649a1ced8303bb1692596b9a19db60d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*


# <a name="troubleshooting-azure-atp-known-issues"></a>Solução de problemas conhecidos da ATP do Azure 


## <a name="deployment-log-location"></a>Local do log de implantação
 
Os logs de implantação do Azure ATP estão localizados no diretório temp do usuário que instalou o produto. No local de instalação padrão, ele pode ser encontrado em: C:\Users\Administrator\AppData\Local\Temp (ou um diretório acima de %temp%).

## <a name="azure-atp-sensor-nic-teaming-issue"></a>Problemas do Agrupamento NIC do sensor da ATP do Azure

Se tentar instalar o sensor do ATP em um computador configurado com um adaptador de agrupamento NIC, você receberá um erro de instalação. Se quiser instalar o sensor da ATP em um computador configurado com Agrupamento NIC, siga essas instruções:

Se ainda não instalou o sensor:

1.  Baixar Npcap de [https://nmap.org/npcap/](https://nmap.org/npcap/).
2.  Desinstale o WinPcap, caso esteja instalado.
3.  Instale o Npcap com as seguintes opções: loopback_support=no & winpcap_mode=yes
4.  Instale o pacote do sensor.

Após instalar o sensor:

1.  Baixar Npcap de [https://nmap.org/npcap/](https://nmap.org/npcap/).
2.  Desinstale o sensor.
3.  Desinstale o WinPcap.
4.  Instale o Npcap com as seguintes opções: loopback_support=no & winpcap_mode=yes
5.  Reinstale o pacote do sensor.

## <a name="windows-defender-atp-integration-issue"></a>Problemas de integração do Windows Defender ATP

A Proteção Avançada contra Ameaças do Azure permite integrar esse recurso ao Windows Defender ATP. Atualmente, a integração está habilitada somente se você for um cliente de visualização privada do Windows Defender ATP. 

## <a name="vmware-virtual-machine-sensor-issue"></a>Problema de sensor da Máquina Virtual VMware

Caso tenha um sensor da ATP do Azure em Máquinas Virtuais VMware, talvez você receba o alerta de monitoramento **Parte do tráfego de rede não está sendo analisado**. Isso ocorre devido a uma incompatibilidade de configuração no VMware.

Para resolver esse problema:

Defina as configurações a seguir como **0** ou **Desabilitado** na configuração NIC da máquina virtual: TsoEnable, LargeSendOffload, Descarregamento TSO, Descarregamento TSO gigante.
> [!NOTE]
> No caso dos sensores da ATP do Azure, é necessário desabilitar apenas o **Descarregamento TSO IPv4** na configuração NIC.

 ![Problema de sensor VMware](./media/vm-sensor-issue.png)

## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)