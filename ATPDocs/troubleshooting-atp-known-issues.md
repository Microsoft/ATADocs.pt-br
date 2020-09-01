---
title: Solução de problemas conhecidos do ATP do Azure
description: Descreve como solucionar problemas de inicialização na ATP do Azure.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 04/28/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 23386e36-2756-4291-923f-fa8607b5518a
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4de688b3ea1c80f8ed0e517baf9da3b469a8d82a
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88956713"
---
# <a name="troubleshooting-azure-atp-known-issues"></a>Solução de problemas conhecidos da ATP do Azure

## <a name="sensor-failure-communication-error"></a>Erro de comunicação de falha no sensor

Se você receber o seguinte erro de falha no sensor:

System.Net.Http.HttpRequestException: ocorreu um erro ao enviar a solicitação. System.Net.WebException: Não é possível se conectar ao servidor remoto ---> System.Net.Sockets.SocketException: falha em uma tentativa de conexão porque a parte conectada não respondeu corretamente após um período ou houve falha na conexão estabelecida devido a uma falha na resposta do host conectado...

**Resolução:**

Verifique se a comunicação não está bloqueada para localhost, porta TCP 444. Para saber mais sobre os pré-requisitos do ATP do Azure, confira [portas](atp-prerequisites.md#ports).

## <a name="deployment-log-location"></a>Local do log de implantação

Os logs de implantação do Azure ATP estão localizados no diretório temp do usuário que instalou o produto. O local de instalação padrão é: C:\Usuários\Administrator\AppData\Local\Temp (ou um diretório acima de %temp%). Para saber mais, veja [Solucionar problemas do ATP usando logs](troubleshooting-atp-using-logs.md)

## <a name="proxy-authentication-problem-presents-as-a-licensing-error"></a>Problema de autenticação de proxy apresentado como erro de licenciamento

Se o seguinte erro surgir durante a instalação do sensor:  **O sensor falhou ao registrar devido a problemas de licenciamento.**

**Entradas de log de implantação:**

[1C60:1AA8][2018-03-24T23:59:13]i000: 2018-03-25 02:59:13.1237 Info  InteractiveDeploymentManager ValidateCreateSensorAsync returned [validateCreateSensorResult=LicenseInvalid]] [1C60:1AA8][2018-03-24T23:59:56]i000: 2018-03-25 02:59:56.4856 Info  InteractiveDeploymentManager ValidateCreateSensorAsync returned [validateCreateSensorResult=LicenseInvalid]] [1C60:1AA8][2018-03-25T00:27:56]i000: 2018-03-25 03:27:56.7399 Debug SensorBootstrapperApplication Engine.Quit [deploymentResultStatus=1602 isRestartRequired=False]] [1C60:15B8][2018-03-25T00:27:56]i500: Desligando, código de saída: 0x642

**Causa:**

em alguns casos, ao se comunicar por meio de um proxy durante a autenticação, ele pode responder para o sensor do Azure ATP com o erro 401 ou 403, em vez do erro 407. O sensor Azure ATP interpretará o erro 401 ou 403 como um problema de licenciamento, não como um problema de autenticação de proxy.

**Resolução:**

o sensor deve poder navegar até *.atp.azure.com por meio do proxy configurado sem autenticação. Saiba mais em [Configurar o proxy para habilitar a comunicação](configure-proxy.md).

## <a name="proxy-authentication-problem-presents-as-a-connection-error"></a>Problema de autenticação de proxy apresentado como um erro de conexão

Se o seguinte erro surgir durante a instalação do sensor: **O sensor não pôde se conectar ao serviço.**

**Causa:**

O problema pode ser causado por um erro de configuração de proxy transparente no Server Core, como certificados raiz exigidos pelo ATP do Azure ausentes ou não atualizados.

**Resolução:**

Execute o cmdlet do PowerShell a seguir para verificar se o certificado raiz confiável do serviço ATP do Azure existe no Server Core. O exemplo a seguir usa o "DigiCert Baltimore Root".

```powershell
Get-ChildItem -Path "Cert:\LocalMachine\Root" | where { $_.Thumbprint -eq "D4DE20D05E66FC53FE1A50882C78DB2852CAE474"}
```

```Output
Subject      : CN=Baltimore CyberTrust Root, OU=CyberTrust, O=Baltimore, C=IE
Issuer       : CN=Baltimore CyberTrust Root, OU=CyberTrust, O=Baltimore, C=IE
Thumbprint   : D4DE20D05E66FC53FE1A50882C78DB2852CAE474
FriendlyName : DigiCert Baltimore Root
NotBefore    : 5/12/2000 11:46:00 AM
NotAfter     : 5/12/2025 4:59:00 PM
Extensions   : {System.Security.Cryptography.Oid, System.Security.Cryptography.Oid, System.Security.Cryptography.Oid}
```

Se você não vir a saída esperada, use as seguintes etapas:

1. Baixe o [certificado raiz Baltimore CyberTrust](https://cacert.omniroot.com/bc2025.crt) no computador do Server Core.
1. Execute o cmdlet do PowerShell a seguir para instalar o certificado.

    ```powershell
    Import-Certificate -FilePath "<PATH_TO_CERTIFICATE_FILE>\bc2025.crt" -CertStoreLocation Cert:\LocalMachine\Root
    ```

## <a name="silent-installation-error-when-attempting-to-use-powershell"></a>Erro de instalação silenciosa ao tentar usar o PowerShell

Se durante a instalação do sensor silenciosa você tentar usar o PowerShell e receber o seguinte erro:

```powershell
"Azure ATP sensor Setup.exe" "/quiet" NetFrameworkCommandLineArguments="/q" Acce ... Unexpected token '"/quiet"' in expression or statement."
```

**Causa:**

ao usar o PowerShell há falha ao incluir o prefixo ./ obrigatório na instalação.

**Resolução:**

use o comando completo para instalar com êxito.

```powershell
./"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"
```

## <a name="azure-atp-sensor-nic-teaming-issue"></a>Problema de agrupamento NIC do sensor da ATP do Azure <a name="nic-teaming"></a>

Se tentar instalar o sensor do ATP em um computador configurado com um adaptador de agrupamento NIC, você receberá um erro de instalação. Se desejar instalar o sensor da ATP em um computador configurado com Agrupamento NIC, siga estas instruções:

1. Baixe o instalador do Npcap versão 0.9984 do [https://nmap.org/npcap/](https://nmap.org/npcap/dist/npcap-0.9984.exe).
    - Como alternativa, solicite a versão OEM do driver Npcap (que dá suporte à instalação silenciosa) com a equipe de suporte.
    - As cópias do Npcap não contarão para a limitação de cinco cópias, cinco computadores ou cinco licenças de usuário se estiverem instaladas e forem usadas exclusivamente em conjunto com o ATP do Azure. Para obter mais informações, confira [Licenciamento do NPCAP](https://github.com/nmap/npcap/blob/master/LICENSE).

Se você ainda não tiver instalado o sensor:

1. Desinstale o WinPcap, caso esteja instalado.
1. Instale o Npcap com as seguintes opções: loopback_support=no & winpcap_mode=yes.
    - Se estiver usando o instalador de GUI, desmarque **suporte de loopback** e marque o modo **WinPcap**.
1. Instale o pacote do sensor.

Após instalar o sensor:

1. Desinstale o sensor.
1. Desinstale o WinPcap.
1. Instale o Npcap com as seguintes opções: loopback_support=no & winpcap_mode=yes
    - Se estiver usando o instalador de GUI, desmarque **suporte de loopback** e marque o modo **WinPcap**.
1. Reinstale o pacote do sensor.

## <a name="multi-processor-group-mode"></a>Modo Grupo de multiprocessadores

Para os sistemas operacionais Windows 2008R2 e 2012, o sensor do ATP do Azure não tem suporte em um modo Grupo de multiprocessadores.

Soluções alternativas possíveis sugeridas:

- Se o Hyper Threading estiver ativado, desative-o. Isso pode reduzir o número de núcleos lógicos o suficiente para evitar a necessidade de execução no modo **Grupo de multiprocessadores**.

- Se seu computador tiver menos de 64 núcleos lógicos e estiver em execução em um host HP, você poderá alterar a configuração do BIOS de **Otimização do Tamanho do Grupo NUMA** do padrão **Clusterizado** para **Simples**.

## <a name="microsoft-defender-atp-integration-issue"></a>Problema de integração do Microsoft Defender ATP

A Proteção Avançada contra Ameaças do Azure permite integrar esse recurso ao Microsoft Defender ATP. Confira [Integração do ATP do Azure com o Microsoft Defender ATP](integrate-wd-atp.md) para saber mais.

## <a name="vmware-virtual-machine-sensor-issue"></a>Problema de sensor da Máquina Virtual VMware

Caso tenha um sensor do ATP do Azure em Máquinas Virtuais VMware, talvez você receba o alerta de integridade **Parte do tráfego de rede não está sendo analisado**. Isso pode ocorrer devido a uma incompatibilidade de configuração no VMware.

Para resolver o problema:

Defina as configurações a seguir como **Desabilitado** na configuração de NIC da máquina virtual: **Descarregamento de TSO do IPv4**.

 ![Problema de sensor VMware](media/vm-sensor-issue.png)

Use o seguinte comando para verificar se o LSO (Descarregamento de Envio Grande) está habilitado ou desabilitado:

`Get-NetAdapterAdvancedProperty | Where-Object DisplayName -Match "^Large*"`

![Verificar o status do LSO](media/missing-network-traffic-health-alert.png)

Se o LSO estiver habilitado, use o seguinte comando para desabilitá-lo:

`Disable-NetAdapterLso -Name {name of adapter}`

![Desabilitar o status do LSO](media/disable-lso-vmware.png)

## <a name="sensor-failed-to-retrieve-group-managed-service-account-gmsa-credentials"></a>Falha do sensor ao tentar recuperar as credenciais da gMSA (conta de serviço gerenciado do grupo)

Se você receber o seguinte alerta de integridade: **As credenciais de usuário dos serviços de diretório estão incorretas**

**Entradas de log do sensor:**

2020-02-17 14:01:36.5315 Info ImpersonationManager CreateImpersonatorAsync started [UserName=account_name Domain=domain1.test.local IsGroupManagedServiceAccount=True] 2020-02-17 14:01:36.5750 Info ImpersonationManager CreateImpersonatorAsync finished [UserName=account_name Domain=domain1.test.local IsSuccess=False]

**Entradas de log do Atualizador do Sensor:**

2020-02-17 14:02:19.6258 Warn GroupManagedServiceAccountImpersonationHelper GetGroupManagedServiceAccountAccessTokenAsync failed GMSA password could not be retrieved [errorCode=AccessDenied AccountName=account_name DomainDnsName=domain1.test.local]

**Causa:**

O sensor falhou ao tentar recuperar a gMSA designada no portal do ATP do Azure.

**Resolução:**

Verifique se as credenciais da conta gMSA estão corretas e se o sensor recebeu as permissões para recuperar as credenciais da conta. Na política aplicada, talvez seja necessário adicionar a conta gMSA às atribuições do direito de usuário de **Fazer logon como um serviço**.

## <a name="report-downloads-cannot-contain-more-than-300000-entries"></a>Downloads de relatório não podem conter mais de 300.000 entradas

O ATP do Azure não dá suporte a downloads de relatório que contêm mais de 300.000 entradas por relatório. Os relatórios serão renderizados como incompletos se mais de 300.000 entradas forem incluídas.

**Causa:**

essa é uma limitação de engenharia.

**Resolução:**

Não há solução conhecida.

## <a name="see-also"></a>Consulte Também

- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
