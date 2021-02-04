---
title: Solução de problemas conhecidos do Microsoft defender para identidade
description: Descreve como você pode solucionar problemas no Microsoft defender para identidade.
ms.date: 02/04/2021
ms.topic: how-to
ms.openlocfilehash: 933d4442d88f2d03ddcd2fa4c90d59d98e229340
ms.sourcegitcommit: 50e6f5511329e56545fa5ab4c9f5ab69046d1e10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/04/2021
ms.locfileid: "99551600"
---
# <a name="troubleshooting-product-long-known-issues"></a>Solucionando [!INCLUDE [Product long](includes/product-long.md)] problemas conhecidos

## <a name="sensor-failure-communication-error"></a>Erro de comunicação de falha no sensor

Se você receber o seguinte erro de falha no sensor:

System.Net.Http.HttpRequestException: ocorreu um erro ao enviar a solicitação. System.Net.WebException: Não é possível se conectar ao servidor remoto ---> System.Net.Sockets.SocketException: falha em uma tentativa de conexão porque a parte conectada não respondeu corretamente após um período ou houve falha na conexão estabelecida devido a uma falha na resposta do host conectado...

**Resolução:**

Verifique se a comunicação não está bloqueada para localhost, porta TCP 444. Para saber mais sobre os [!INCLUDE [Product long](includes/product-long.md)] pré-requisitos, consulte [portas](prerequisites.md#ports).

## <a name="deployment-log-location"></a>Local do log de implantação

Os [!INCLUDE [Product short](includes/product-short.md)] logs de implantação estão localizados no diretório Temp do usuário que instalou o produto. O local de instalação padrão é: C:\Usuários\Administrator\AppData\Local\Temp (ou um diretório acima de %temp%). Para obter mais informações, consulte [Solucionando problemas [!INCLUDE [Product short](includes/product-short.md)] usando logs](troubleshooting-using-logs.md)

## <a name="proxy-authentication-problem-presents-as-a-licensing-error"></a>Problema de autenticação de proxy apresentado como erro de licenciamento

Se o seguinte erro surgir durante a instalação do sensor:  **O sensor falhou ao registrar devido a problemas de licenciamento.**

**Entradas de log de implantação:**

[1C60:1AA8][2018-03-24T23:59:13]i000: 2018-03-25 02:59:13.1237 Info  InteractiveDeploymentManager ValidateCreateSensorAsync returned [validateCreateSensorResult=LicenseInvalid]] [1C60:1AA8][2018-03-24T23:59:56]i000: 2018-03-25 02:59:56.4856 Info  InteractiveDeploymentManager ValidateCreateSensorAsync returned [validateCreateSensorResult=LicenseInvalid]] [1C60:1AA8][2018-03-25T00:27:56]i000: 2018-03-25 03:27:56.7399 Debug SensorBootstrapperApplication Engine.Quit [deploymentResultStatus=1602 isRestartRequired=False]] [1C60:15B8][2018-03-25T00:27:56]i500: Desligando, código de saída: 0x642

**Causa:**

Em alguns casos, ao se comunicar por meio de um proxy, durante a autenticação, ele pode responder ao [!INCLUDE [Product short](includes/product-short.md)] sensor com o erro 401 ou 403 em vez do erro 407. O [!INCLUDE [Product short](includes/product-short.md)] sensor irá interpretar o erro 401 ou 403 como um problema de licenciamento e não como um problema de autenticação de proxy.

**Resolução:**

o sensor deve poder navegar até *.atp.azure.com por meio do proxy configurado sem autenticação. Saiba mais em [Configurar o proxy para habilitar a comunicação](configure-proxy.md).

## <a name="proxy-authentication-problem-presents-as-a-connection-error"></a>Problema de autenticação de proxy apresentado como um erro de conexão

Se o seguinte erro surgir durante a instalação do sensor: **O sensor não pôde se conectar ao serviço.**

**Causa:**

O problema pode ser causado por um erro de configuração de proxy transparente no Server Core, como os certificados raiz exigidos pelo [!INCLUDE [Product short](includes/product-short.md)] não são atuais ou ausentes.

**Resolução:**

Execute o seguinte cmdlet do PowerShell para verificar se o [!INCLUDE [Product short](includes/product-short.md)] certificado raiz confiável do serviço existe no Server Core. O exemplo a seguir usa o "DigiCert Baltimore Root" e o "DigiCert Global Root".

```powershell
Get-ChildItem -Path "Cert:\LocalMachine\Root" | where { $_.Thumbprint -eq "D4DE20D05E66FC53FE1A50882C78DB2852CAE474"} | fl
Get-ChildItem -Path "Cert:\LocalMachine\Root" | where { $_.Thumbprint -eq "df3c24f9bfd666761b268073fe06d1cc8d4f82a4"} | fl
```

```Output
Subject      : CN=Baltimore CyberTrust Root, OU=CyberTrust, O=Baltimore, C=IE
Issuer       : CN=Baltimore CyberTrust Root, OU=CyberTrust, O=Baltimore, C=IE
Thumbprint   : D4DE20D05E66FC53FE1A50882C78DB2852CAE474
FriendlyName : DigiCert Baltimore Root
NotBefore    : 5/12/2000 11:46:00 AM
NotAfter     : 5/12/2025 4:59:00 PM
Extensions   : {System.Security.Cryptography.Oid, System.Security.Cryptography.Oid, System.Security.Cryptography.Oid}

Subject      : CN=DigiCert Global Root G2, OU=www.digicert.com, O=DigiCert Inc, C=US
Issuer       : CN=DigiCert Global Root G2, OU=www.digicert.com, O=DigiCert Inc, C=US
Thumbprint   : DF3C24F9BFD666761B268073FE06D1CC8D4F82A4
FriendlyName : DigiCert Global Root G2
NotBefore    : 01/08/2013 15:00:00
NotAfter     : 15/01/2038 14:00:00
Extensions   : {System.Security.Cryptography.Oid, System.Security.Cryptography.Oid, System.Security.Cryptography.Oid}
```

Se você não vir a saída esperada, use as seguintes etapas:

1. Baixe o [certificado raiz Baltimore CyberTrust](https://cacert.omniroot.com/bc2025.crt) e o [DigiCert Global Root G2](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt) no computador Server Core.
1. Execute o cmdlet do PowerShell a seguir para instalar o certificado.

    ```powershell
    Import-Certificate -FilePath "<PATH_TO_CERTIFICATE_FILE>\bc2025.crt" -CertStoreLocation Cert:\LocalMachine\Root
    Import-Certificate -FilePath "<PATH_TO_CERTIFICATE_FILE>\DigiCertGlobalRootG2.crt" -CertStoreLocation Cert:\LocalMachine\Root
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

## <a name="product-short-sensor-nic-teaming-issue"></a>[!INCLUDE [Product short](includes/product-short.md)] problema de agrupamento da NIC do sensor <a name="nic-teaming"></a>

Se você tentar instalar o [!INCLUDE [Product short](includes/product-short.md)] sensor em um computador configurado com um adaptador de agrupamento NIC, receberá um erro de instalação. Se você quiser instalar o [!INCLUDE [Product short](includes/product-short.md)] sensor em um computador configurado com o agrupamento NIC, siga estas instruções:

1. Baixe o instalador do Npcap versão 1,0 do  [https://nmap.org/npcap/](https://nmap.org/npcap/dist/npcap-1.00.exe) .
    - Como alternativa, solicite a versão OEM do driver Npcap (que dá suporte à instalação silenciosa) com a equipe de suporte.
    - As cópias de Npcap não contam para a limitação de cinco, cinco computadores ou cinco licenças de licenciamento de usuário, se estiverem instalados e usados exclusivamente em conjunto com o [!INCLUDE [Product short](includes/product-short.md)] . Para obter mais informações, confira [Licenciamento do NPCAP](https://github.com/nmap/npcap/blob/master/LICENSE).

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

Nos sistemas operacionais Windows 2008 R2 e 2012, não há suporte para o sensor do [!INCLUDE [Product short](includes/product-short.md)] em um modo Grupo de multiprocessadores.

Soluções alternativas possíveis sugeridas:

- Se o Hyper Threading estiver ativado, desative-o. Isso pode reduzir o número de núcleos lógicos o suficiente para evitar a necessidade de execução no modo **Grupo de multiprocessadores**.

- Se seu computador tiver menos de 64 núcleos lógicos e estiver em execução em um host HP, você poderá alterar a configuração do BIOS de **Otimização do Tamanho do Grupo NUMA** do padrão **Clusterizado** para **Simples**.

## <a name="microsoft-defender-for-endpoint-integration-issue"></a>Problema de integração do Microsoft defender para ponto de extremidade

[!INCLUDE [Product short](includes/product-short.md)] permite a integração [!INCLUDE [Product short](includes/product-short.md)] com o Microsoft defender para ponto de extremidade. Consulte [integrar [!INCLUDE [Product short](includes/product-short.md)] com o Microsoft defender para ponto de extremidade](integrate-mde.md) para obter mais informações.

## <a name="vmware-virtual-machine-sensor-issue"></a>Problema de sensor da Máquina Virtual VMware

Se você tiver um [!INCLUDE [Product short](includes/product-short.md)] sensor em máquinas virtuais VMware, você poderá receber o alerta de integridade **parte do tráfego de rede não está sendo analisado**. Isso pode ocorrer devido a uma incompatibilidade de configuração no VMware.

Para resolver o problema:

No SO convidado, defina o seguinte como **desabilitado** na configuração de NIC da máquina virtual: **descarregamento de Tso IPv4**.

![Problema de sensor VMware](media/vm-sensor-issue.png)

Use o seguinte comando para verificar se o LSO (Descarregamento de Envio Grande) está habilitado ou desabilitado:

`Get-NetAdapterAdvancedProperty | Where-Object DisplayName -Match "^Large*"`

![Verificar o status do LSO](media/missing-network-traffic-health-alert.png)

Se o LSO estiver habilitado, use o seguinte comando para desabilitá-lo:

`Disable-NetAdapterLso -Name {name of adapter}`

![Desabilitar o status do LSO](media/disable-lso-vmware.png)

> [!NOTE]
>
> - Talvez seja necessário reiniciar o computador para que essas alterações entrem em vigor.
> - Essas etapas podem variar dependendo da sua versão do VMWare. Consulte a documentação do VMWare para obter informações sobre como desabilitar o LSO/TSO para sua versão do VMWare.

## <a name="sensor-failed-to-retrieve-group-managed-service-account-gmsa-credentials"></a>Falha do sensor ao tentar recuperar as credenciais da gMSA (conta de serviço gerenciado do grupo)

Se você receber o seguinte alerta de integridade: **As credenciais de usuário dos serviços de diretório estão incorretas**

**Entradas de log do sensor:**

2020-02-17 14:01:36.5315 Info ImpersonationManager CreateImpersonatorAsync started [UserName=account_name Domain=domain1.test.local IsGroupManagedServiceAccount=True] 2020-02-17 14:01:36.5750 Info ImpersonationManager CreateImpersonatorAsync finished [UserName=account_name Domain=domain1.test.local IsSuccess=False]

**Entradas de log do Atualizador do Sensor:**

2020-02-17 14:02:19.6258 Warn GroupManagedServiceAccountImpersonationHelper GetGroupManagedServiceAccountAccessTokenAsync failed GMSA password could not be retrieved [errorCode=AccessDenied AccountName=account_name DomainDnsName=domain1.test.local]

**Causa:**

O sensor não pôde recuperar a conta de gMSA designada do [!INCLUDE [Product short](includes/product-short.md)] Portal.

**Resolução:**

Verifique se as credenciais da conta gMSA estão corretas e se o sensor recebeu as permissões para recuperar as credenciais da conta. Embora [!INCLUDE [Product short](includes/product-short.md)]  o não exija a permissão **fazer logon como um serviço** para contas do gMSA, esse problema é geralmente resolvido com a adição da permissão à conta.

## <a name="report-downloads-cannot-contain-more-than-300000-entries"></a>Downloads de relatório não podem conter mais de 300.000 entradas

[!INCLUDE [Product short](includes/product-short.md)] o não oferece suporte a downloads de relatório que contenham mais de 300.000 entradas por relatório. Os relatórios serão renderizados como incompletos se mais de 300.000 entradas forem incluídas.

**Causa:**

essa é uma limitação de engenharia.

**Resolução:**

Não há solução conhecida.

## <a name="sensor-fails-to-enumerate-event-logs"></a>O sensor falha ao enumerar logs de eventos

Se você observar um número limitado ou falta de alertas de eventos de segurança ou atividades lógicas no [!INCLUDE [Product short](includes/product-short.md)] console, mas nenhum alerta de integridade será disparado. 

**Entradas de log do sensor:**

Erro EventLogException System. Diagnostics.. Reader. EventLogException: o identificador é inválido em void System. Diagnostics.. Reader. EventLogException. throw (int ErrorCode) em Object System. Diagnostics. Eventing. Reader. NativeWrapper. EvtGetEventInfo (identificador EventLogHandle, EvtEventPropertyId EnumType) na cadeia de caracteres System.Diagnostics.Eventing.Reader.EventLogRecord.get_ContainerLog ()

**Causa:**

Uma lista de controle de acesso discricionário está limitando o acesso aos logs de eventos necessários pela conta de serviço local.

**Resolução:**

Verifique se a lista de controle de acesso discricionário inclui a seguinte entrada:

`(A;;0x1;;;S-1-5-80-818380073-2995186456-1411405591-3990468014-3617507088)`

## <a name="see-also"></a>Consulte Também

- [Pré-requisitos do [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Planejamento de capacidade do [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
