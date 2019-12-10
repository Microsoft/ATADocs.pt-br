---
title: Configurar seu proxy ou firewall para habilitar a comunicação do Azure ATP com o sensor | Microsoft Docs
description: Descreve como configurar o firewall ou proxy para permitir a comunicação entre o serviço de nuvem do Azure ATP e sensores do Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 27630e93db4e103454e6d0fec7756824988ec4a2
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "71185491"
---
# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-azure-atp-sensor"></a>Configurar o proxy do ponto de extremidade e configurações de conectividade de Internet para o Sensor de ATP do Azure

Cada sensor do Azure ATP (Proteção Avançada contra Ameaças) requer conectividade com a Internet para que o serviço de nuvem do Azure ATP funcione com êxito. Em algumas organizações, os controladores de domínio não são diretamente conectados à Internet, mas são conectados por meio de uma conexão de proxy Web. Cada sensor do Azure ATP requer que você use a configuração de proxy do WinINET (Microsoft Windows Internet) para relatar dados do sensor e comunicar-se com o serviço do Azure ATP. Se você usar o WinHTTP para a configuração de proxy, ainda será necessário definir as configurações de proxy do navegador WinINet (Windows Internet) para a comunicação entre o sensor e o serviço de nuvem do Azure ATP.

Ao configurar o proxy, você precisará saber que o serviço de sensor do ATP do Azure interno é executado no contexto do sistema usando a conta **LocalService** e o serviço de Atualizador do Sensor do ATP do Azure é executado no contexto do sistema usando a conta **LocalSystem**. 

> [!NOTE]
> Se estiver usando um proxy Transparente ou WPAD em sua topologia de rede, você não precisará configurar WinINET para o proxy.

## <a name="configure-the-proxy"></a>Configurar o proxy 

Você pode definir as configurações de proxy durante a instalação do sensor, usando os parâmetros definidos em [Instalação silenciosa, configurações de autenticação de proxy](https://docs.microsoft.com/azure-advanced-threat-protection/atp-silent-installation#proxy-authentication).

### <a name="proxy-authentication"></a>Autenticação de proxy

Use os seguintes comandos para concluir a autenticação de proxy:

**Sintaxe**:


> [!div class="mx-tableFixed"]
> 
> |Nome|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
> |-------------|----------|---------|---------|
> |ProxyUrl|ProxyUrl="https\://proxy.contoso.com:8080"|Não|Especifica o ProxyUrl e o número da porta para o sensor do ATP do Azure.|
> |ProxyUserName|ProxyUserName="Contoso\ProxyUser"|Não|Se o seu serviço de proxy exigir autenticação, forneça um nome de usuário no formato DOMÍNIO\usuário.|
> |ProxyUserPassword|ProxyUserPassword="P@ssw0rd"|Não|Especifica a senha para o nome de usuário do proxy. *As credenciais são criptografadas e armazenadas localmente pelo sensor do ATP do Azure.|

Também pode configurar o servidor proxy manualmente usando um proxy estático baseado no Registro, para permitir que o sensor ATP do Azure relate dados de diagnóstico e se comunique com o serviço de nuvem do ATP do Azure quando um computador não tiver permissão para se conectar à Internet.

> [!NOTE]
> As alterações no Registro devem ser aplicadas apenas a LocalService e LocalSystem.

O proxy estático é configurável por meio do Registro. Você deve copiar a configuração de proxy que usa no contexto do usuário para localsystem e localservice. Para copiar as configurações de proxy do contexto de usuário:

1.   Não deixe de fazer backup das chave do Registro antes de modificá-las.

2. No Registro, procure o valor `DefaultConnectionSettings` como REG_BINARY na chave do registro `HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings` e copie-o.
 
2.  Se LocalSystem não tiver as configurações de proxy corretas (se elas não estiverem configuradas ou se forem diferentes de Current_User), copie as configurações de proxy de Current_User para LocalSystem. Na chave do Registro `HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings`.

3.  Cole o valor de Current_user `DefaultConnectionSettings` como REG_BINARY.

4.  Se LocalService não tiver as configurações de proxy corretas, copie a configuração de proxy de Current_User para LocalService. Na chave do Registro `HKU\S-1-5-19\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings`.

5.  Cole o valor de Current_User `DefaultConnectionSettings` como REG_BINARY.

> [!NOTE]
> Isso afetará todos os aplicativos, incluindo os serviços do Windows que usam WinINET com LocalService, contexto LocalSytem.


## <a name="enable-access-to-azure-atp-service-urls-in-the-proxy-server"></a>Habilitar o acesso a URLs de serviço do Azure ATP no servidor proxy

Para habilitar o acesso ao ATP do Azure, permita o tráfego às URLs a seguir:

- \<nome-da-sua-instância>.atp.azure.com – para conectividade do console. Por exemplo, "Contoso-corp.atp.azure.com"

- \<nome-da-sua-instância>sensorapi.atp.azure.com – para conectividade de sensores. Por exemplo, "contoso-corpsensorapi.atp.azure.com"

As URLs anteriores são mapeadas automaticamente para o local do serviço correto da instância do ATP do Azure. Se você precisar de um controle mais granular, considere permitir o tráfego para os pontos de extremidade relevantes da tabela a seguir:

|Local do serviço|Registro DNS *.atp.azure.com|
|----|----|
|EUA |triprd1wcusw1sensorapi.atp.azure.com<br>triprd1wcuswb1sensorapi.atp.azure.com<br>triprd1wcuse1sensorapi.atp.azure.com|
|Ocidental|triprd1wceun1sensorapi.atp.azure.com<br>triprd1wceuw1sensorapi.atp.azure.com|
|Ásia|triprd1wcasse1sensorapi.atp.azure.com|

 
> [!NOTE]
> Para garantir a segurança máxima e a privacidade dos dados, o ATP do Azure usa autenticação mútua baseada em certificado entre cada sensor e o back-end de nuvem do ATP do Azure. Se a inspeção SSL for usada em seu ambiente, verifique se ela está configurada para autenticação mútua, de modo que não interfira no processo de autenticação.



## <a name="see-also"></a>Consulte Também
- [Configurar o encaminhamento de eventos](configure-event-forwarding.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
