---
title: Configurar seu proxy ou firewall para habilitar a comunicação do Azure ATP com o sensor | Microsoft Docs
description: Descreve como configurar o firewall ou proxy para permitir a comunicação entre o serviço de nuvem do Azure ATP e sensores do Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/29/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2f39c0d3628c3a3cc9e034fa1da8bb5a66bc704b
ms.sourcegitcommit: 3eade64779002d2c8ae005565bc69e1b3f89fb7d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34560234"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*



# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-azure-atp-sensor"></a>Configurar o proxy do ponto de extremidade e configurações de conectividade de Internet para o Sensor de ATP do Azure

Cada sensor do Azure ATP (Proteção Avançada contra Ameaças) requer conectividade com a Internet para que o serviço de nuvem do Azure ATP funcione com êxito. Em algumas organizações, os controladores de domínio não são diretamente conectados à Internet, mas são conectados por meio de uma conexão de proxy da Web. Cada sensor do Azure ATP requer que você use a configuração de proxy do WinINET (Microsoft Windows Internet) para relatar dados do sensor e comunicar-se com o serviço do Azure ATP. Se você usar o WinHTTP para a configuração de proxy, ainda será necessário definir as configurações de proxy do navegador WinINet (Windows Internet) para a comunicação entre o sensor e o serviço de nuvem do Azure ATP.


Ao configurar o proxy, você precisará saber o que o serviço de sensor do Azure ATP interno é executado no contexto do sistema usando a conta **LocalService**, e o serviço de Atualizador do Sensor do Azure ATP é executado no contexto do sistema usando a conta **LocalSystem**. 

> [!NOTE]
> Se estiver usando um proxy Transparente ou WPAD em sua topologia de rede, você não precisará configurar WinINET para o proxy.

## <a name="configure-the-proxy"></a>Configurar o proxy 

Configure o servidor proxy manualmente usando um proxy estático baseado no Registro, para permitir que o sensor ATP do Azure relate dados de diagnóstico e se comunique com o serviço de nuvem do Azure ATP quando um computador não tiver permissão para se conectar à Internet.

> [!NOTE]
> As alterações no Registro devem ser aplicadas apenas a LocalService e LocalSystem.

O proxy estático é configurável por meio do Registro. Você deve copiar a configuração de proxy que usa no contexto do usuário para localsystem e localservice. Para copiar as configurações de proxy do contexto de usuário:

1.   Não deixe de fazer backup das chave do Registro antes de modificá-las.

2. No Registro, procure o valor `DefaultConnectionSetting` como REG_BINARY na chave do registro `HKCU\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting` e copie-o.
 
2.  Se LocalSystem não tiver as configurações de proxy corretas (se elas não estiverem configuradas ou se forem diferentes de Current_User), copie as configurações de proxy de Current_User para LocalSystem. Na chave do Registro `HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting`.

3.  Cole o valor de Current_user `DefaultConnectionSetting` como REG_BINARY.

4.  Se LocalService não tiver as configurações de proxy corretas, copie a configuração de proxy de Current_User para LocalService. Na chave do Registro `HKU\S-1-5-19\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting`.

5.  Cole o valor de Current_User `DefaultConnectionSetting` como REG_BINARY.

> [!NOTE]
> Isso afetará todos os aplicativos, incluindo os serviços do Windows que usam WinINET com LocalService, contexto LocalSytem.


## <a name="enable-access-to-azure-atp-service-urls-in-the-proxy-server"></a>Habilitar o acesso a URLs de serviço do Azure ATP no servidor proxy

Se um proxy ou firewall estiver bloqueando todo o tráfego por padrão e permitindo somente domínios específicos ou se a verificação de HTTPS (inspeção de SSL) estiver habilitada, verifique se as seguintes URLs estão na lista de permissão para permitir a comunicação com o serviço do Azure ATP na porta 443:

|Local do serviço|Registro DNS .Atp.Azure.com|
|----|----|
|EUA |triprd1wcusw1sensorapi.atp.azure.com<br>triprd1wcuswb1sensorapi.atp.azure.com<br>triprd1wcuse1sensorapi.atp.azure.com|
|Ocidental|triprd1wceun1sensorapi.atp.azure.com<br>triprd1wceuw1sensorapi.atp.azure.com|
|Ásia|triprd1wcasse1sensorapi.atp.azure.com|


Também é possível fortalecer as regras de firewall ou de proxy para um espaço de trabalho específico criado por você, definindo uma regra para os seguintes registros DNS:
- <Workspace-Name>.atp.azure.com – para conectividade do console. Por exemplo, contosoATP.atp.azure.com
- <Workspace-Name>sensorapi.atp.azure.com – para conectividade de sensores. Por exemplo, contosoATPsensorapi.atp.azure.com

 
> [!NOTE]
> Ao executar a inspeção de SSL no tráfego de rede do Azure ATP (entre o sensor e o serviço do Azure ATP), a inspeção de SSL deve dar suporte à inspeção mútua.


## <a name="see-also"></a>Consulte Também
- [Configurar o encaminhamento de eventos](configure-event-forwarding.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)