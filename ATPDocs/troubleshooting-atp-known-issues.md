---
title: Solução de problemas conhecidos da ATP do Azure | Microsoft Docs
description: Descreve como solucionar problemas de inicialização na ATP do Azure.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 08/28/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 23386e36-2756-4291-923f-fa8607b5518a
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b5709955763015870067490ab458c1e94cdf567b
ms.sourcegitcommit: bb33e24591acf11688955318b5938bc3d662a398
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70076657"
---
# <a name="troubleshooting-azure-atp-known-issues"></a>Solução de problemas conhecidos da ATP do Azure 


## <a name="deployment-log-location"></a>Local do log de implantação
 
Os logs de implantação do Azure ATP estão localizados no diretório temp do usuário que instalou o produto. O local de instalação padrão é: C:\Usuários\Administrator\AppData\Local\Temp (ou um diretório acima de %temp%). Para saber mais, veja [Solucionar problemas do ATP usando logs](troubleshooting-atp-using-logs.md)

## <a name="proxy-authentication-problem-presents-as-a-licensing-error"></a>Problema de autenticação de proxy apresentado como erro de licenciamento

Se o seguinte erro surgir durante a instalação do sensor:  **O sensor falhou ao registrar devido a problemas de licenciamento.**

Entradas de log de implantação: [1C60:1AA8][2018-03-24T23:59:13]i000: 2018-03-25 02:59:13.1237 Informações  InteractiveDeploymentManager ValidateCreateSensorAsync retornaram [\[]validateCreateSensorResult=LicenseInvalid[\]] [1C60:1AA8][2018-03-24T23:59:56]i000: 2018-03-25 02:59:56.4856 Informações  InteractiveDeploymentManager ValidateCreateSensorAsync retornaram [\[]validateCreateSensorResult=LicenseInvalid[\]] [1C60:1AA8][2018-03-25T00:27:56]i000: 2018-03-25 03:27:56.7399 Depurar SensorBootstrapperApplication Engine.Quit [\[]deploymentResultStatus=1602 isRestartRequired=False[\]] [1C60:15B8][2018-03-25T00:27:56]i500: Desligando, código de saída: 0x642


**Causa:**

em alguns casos, ao se comunicar por meio de um proxy durante a autenticação, ele pode responder para o sensor do Azure ATP com o erro 401 ou 403, em vez do erro 407. O sensor Azure ATP interpretará o erro 401 ou 403 como um problema de licenciamento, não como um problema de autenticação de proxy. 

**Resolução:**

o sensor deve poder navegar até *.atp.azure.com por meio do proxy configurado sem autenticação. Saiba mais em [Configurar o proxy para habilitar a comunicação](configure-proxy.md).

## <a name="silent-installation-error-when-attempting-to-use-powershell"></a>Erro de instalação silenciosa ao tentar usar o PowerShell  

Se durante a instalação do sensor silenciosa você tentar usar o PowerShell e receber o seguinte erro: 


    "Azure ATP sensor Setup.exe" "/quiet" NetFrameworkCommandLineArguments="/q" Acce ...           Unexpected token '"/quiet"' in expression or statement."

**Causa:** ao usar o PowerShell há falha ao incluir o prefixo ./ obrigatório na instalação. 

**Resolução:** use o comando completo para instalar com êxito. 

    ./"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"

## Problema de agrupamento NIC do sensor da ATP do Azure <a name="nic-teaming"></a>

Se tentar instalar o sensor do ATP em um computador configurado com um adaptador de agrupamento NIC, você receberá um erro de instalação. Se desejar instalar o sensor da ATP em um computador configurado com Agrupamento NIC, siga estas instruções:

Se você ainda não tiver instalado o sensor:

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

## <a name="multi-processor-group-mode"></a>Modo Grupo de multiprocessadores 
Para os sistemas operacionais Windows 2008R2 e 2012, o sensor do ATP do Azure não tem suporte em um modo Grupo de multiprocessadores.

Soluções alternativas possíveis sugeridas:
- Se o Hyper Threading estiver ativado, desative-o. Isso pode reduzir o número de núcleos lógicos o suficiente para evitar a necessidade de execução no modo **Grupo de multiprocessadores**. 

- Se seu computador tiver menos de 64 núcleos lógicos e estiver em execução em um host HP, você poderá alterar a configuração do BIOS de **Otimização do Tamanho do Grupo NUMA** do padrão **Clusterizado** para **Simples**. 

## <a name="windows-defender-atp-integration-issue"></a>Problemas de integração do Windows Defender ATP

A Proteção Avançada contra Ameaças do Azure permite integrar esse recurso ao Windows Defender ATP. Confira [Integrar o Azure ATP ao Windows Defender ATP](integrate-wd-atp.md) para obter mais informações. 

## <a name="vmware-virtual-machine-sensor-issue"></a>Problema de sensor da Máquina Virtual VMware

Caso tenha um sensor da ATP do Azure em Máquinas Virtuais VMware, talvez você receba o alerta de monitoramento **Parte do tráfego de rede não está sendo analisado**. Isso ocorre devido a uma incompatibilidade de configuração no VMware.

Para resolver esse problema:

Defina as configurações a seguir como **0** ou **Desabilitado** na configuração de NIC da máquina virtual: TsoEnable, LargeSendOffload, Descarregamento do TSO Offload, Descarregamento Gigante do TSO.
> [!NOTE]
> No caso dos sensores da ATP do Azure, é necessário desabilitar apenas o **Descarregamento TSO IPv4** na configuração NIC.

 ![Problema de sensor VMware](./media/vm-sensor-issue.png)

## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
