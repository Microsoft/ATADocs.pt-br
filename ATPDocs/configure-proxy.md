---
title: Configurar seu proxy ou firewall para habilitar a comunicação do ATP do Azure com o sensor
description: Descreve como configurar o firewall ou proxy para permitir a comunicação entre o serviço de nuvem do Azure ATP e sensores do Azure ATP
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 07/29/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 24fab947687183f40d5043678b24e12792d98233
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88956832"
---
# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-azure-atp-sensor"></a>Configurar o proxy do ponto de extremidade e configurações de conectividade de Internet para o Sensor de ATP do Azure

Cada sensor da Proteção Avançada contra Ameaças do Azure precisa de conectividade com a Internet para que o serviço de nuvem do ATP do Azure relate dados de sensor e funcione com êxito. Em algumas organizações, os controladores de domínio não estão diretamente conectados à Internet, mas por meio de uma conexão de proxy Web.

É recomendável usar a linha de comando para configurar o servidor proxy, pois isso garante que apenas os serviços do sensor do ATP do Azure se comuniquem por meio do proxy.

## <a name="configure-proxy-server-using-the-command-line"></a>Configurar o servidor proxy usando a linha de comando

É possível configurar o servidor proxy durante a instalação do sensor usando as opções de linha de comando a seguir.

### <a name="syntax"></a>Sintaxe

"Azure ATP sensor Setup.exe" [/quiet] [/Help] [ProxyUrl="https://proxy.internal.com"] [ProxyUserName="domain\proxyuser"] [ProxyUserPassword="ProxyPassword"]

### <a name="switch-descriptions"></a>Descrições de comutador

> [!div class="mx-tableFixed"]
>
> |Name|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
> |-------------|----------|---------|---------|
> |ProxyUrl|ProxyUrl="http\://proxy.contoso.com:8080"|Não|Especifica o ProxyUrl e o número da porta para o sensor do ATP do Azure.|
> |ProxyUserName|ProxyUserName="Contoso\ProxyUser"|Não|Se o seu serviço de proxy exigir autenticação, forneça um nome de usuário no formato DOMÍNIO\usuário.|
> |ProxyUserPassword|ProxyUserPassword="P@ssw0rd"|Não|Especifica a senha para o nome de usuário do proxy. *As credenciais são criptografadas e armazenadas localmente pelo sensor do ATP do Azure.|

## <a name="alternative-methods-to-configure-your-proxy-server"></a>Métodos alternativos para configurar o servidor proxy

Use um dos métodos alternativos a seguir para configurar o servidor proxy. Ao definir as configurações de proxy com esses métodos, outros serviços em execução no contexto, como Sistema Local ou Serviço Local, também direcionarão o tráfego pelo proxy.

- [Configurar o servidor proxy com o WinINet](#configure-proxy-server-using-wininet)
- [Configurar o servidor proxy com o Registro](#configure-proxy-server-using-the-registry)

### <a name="configure-proxy-server-using-wininet"></a>Configurar o servidor proxy com o WinINet

É possível configurar o servidor proxy com o WinINet (Microsoft Windows Internet) para permitir que o sensor do ATP do Azure relate dados de diagnóstico e se comunique com o serviço de nuvem do ATP do Azure quando um computador não tiver permissão para se conectar à Internet. Se você usar o WinHTTP para a configuração de proxy, ainda será necessário definir as configurações de proxy do navegador WinINet (Windows Internet) para a comunicação entre o sensor e o serviço de nuvem do Azure ATP.

Ao configurar o proxy, lembre-se de que o serviço de sensor do ATP do Azure incorporado é executado no contexto do sistema usando a conta **LocalService** e que o serviço de Atualizador do Sensor do ATP do Azure é executado no contexto do sistema usando a conta **LocalSystem**.

> [!NOTE]
> Se estiver usando um proxy Transparente ou WPAD na topologia de rede, você não precisará configurar o WinINet para o proxy.

### <a name="configure-proxy-server-using-the-registry"></a>Configurar o servidor proxy com o Registro

Também pode configurar o servidor proxy manualmente usando um proxy estático baseado no Registro, para permitir que o sensor ATP do Azure relate dados de diagnóstico e se comunique com o serviço de nuvem do ATP do Azure quando um computador não tiver permissão para se conectar à Internet.

> [!NOTE]
> As alterações no Registro devem ser aplicadas apenas a LocalService e LocalSystem.

O proxy estático é configurável por meio do Registro. Você deve copiar a configuração de proxy que usa no contexto do usuário para localsystem e localservice. Para copiar as configurações de proxy do contexto de usuário:

1. Não deixe de fazer backup das chave do Registro antes de modificá-las.

1. No Registro, procure o valor `DefaultConnectionSettings` como REG_BINARY na chave do registro `HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings` e copie-o.

1. Se LocalSystem não tiver as configurações de proxy corretas (se elas não estiverem configuradas ou se forem diferentes de Current_User), copie as configurações de proxy de Current_User para LocalSystem. Na chave do Registro `HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings`.

1. Cole o valor de Current_user `DefaultConnectionSettings` como REG_BINARY.

1. Se LocalService não tiver as configurações de proxy corretas, copie a configuração de proxy de Current_User para LocalService. Na chave do Registro `HKU\S-1-5-19\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings`.

1. Cole o valor de Current_User `DefaultConnectionSettings` como REG_BINARY.

> [!NOTE]
> Isso afetará todos os aplicativos, incluindo os serviços do Windows que usam WinINET com LocalService, contexto LocalSytem.

## <a name="enable-access-to-azure-atp-service-urls-in-the-proxy-server"></a>Habilitar o acesso a URLs de serviço do Azure ATP no servidor proxy

Para habilitar o acesso ao ATP do Azure, é recomendável permitir o tráfego para as URLs a seguir. As URLs são mapeadas automaticamente para o local do serviço correto da instância do ATP do Azure.

- `<your-instance-name>.atp.azure.com` – para conectividade com o console. Por exemplo, `contoso-corp.atp.azure.com`

- `<your-instance-name>sensorapi.atp.azure.com` – para conectividade com os sensores. Por exemplo, `contoso-corpsensorapi.atp.azure.com`

Também é possível usar os intervalos de endereço IP na marca de serviço do Azure (**AzureAdvancedThreatProtection**) para habilitar o acesso ao ATP do Azure. Para obter mais informações sobre marcas de serviço, confira [Marcas de serviço de rede virtual](/azure/virtual-network/service-tags-overview) ou [baixe o arquivo de marcas de serviço](https://www.microsoft.com/download/details.aspx?id=56519).

Como alternativa, se você precisar de um controle mais granular, considere permitir o tráfego para os pontos de extremidade relevantes da seguinte tabela:

|Local do serviço|Registro DNS *.atp.azure.com|
|----|----|
|EUA |`triprd1wcusw2sensorapi.atp.azure.com`<br>`triprd1wcuswb3sensorapi.atp.azure.com`<br>`triprd1wcuse3sensorapi.atp.azure.com`|
|GCC High dos EUA|`https://triff1wcva2sensorapi.atp.azure.us`|
|Europa|`triprd1wceun2sensorapi.atp.azure.com`<br>`triprd1wceuw3sensorapi.atp.azure.com`|
|Ásia|`triprd1wcasse2sensorapi.atp.azure.com`|
|Reino Unido|`triprd1wcuks2sensorapi.atp.azure.com`|

> [!NOTE]
>
> - Para garantir a segurança máxima e a privacidade dos dados, o ATP do Azure usa autenticação mútua baseada em certificado entre cada sensor e o back-end de nuvem do ATP do Azure. Se a inspeção SSL for usada em seu ambiente, verifique se ela está configurada para autenticação mútua, de modo que não interfira no processo de autenticação.
> - Ocasionalmente, os endereços IP do serviço do ATP do Azure podem mudar. Portanto, se você configurar manualmente os endereços IP ou se o proxy resolver automaticamente os nomes DNS para cada endereço IP e usá-los, será necessário verificar periodicamente se os endereços IP configurados ainda estão atualizados.

## <a name="see-also"></a>Consulte Também

- [Configurar o encaminhamento de eventos](configure-event-forwarding.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)