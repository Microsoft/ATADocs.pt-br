---
title: "Configurar seu proxy ou firewall para habilitar a comunicação do Azure ATP com o sensor | Microsoft Docs"
description: "Descreve como configurar o firewall ou proxy para permitir a comunicação entre o serviço de nuvem do Azure ATP e sensores do Azure ATP"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 47fa5ad5d6fb7800c7df4b878d16ec335e2b70e5
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2018
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*



# <a name="configure-your-proxy-to-allow-communication-between-azure-atp-sensors-and-the-azure-atp-cloud-service"></a>Configure seu proxy para permitir a comunicação entre os sensores do Azure ATP e o serviço de nuvem do Azure ATP

Para seus Controladores de domínio se comunicarem com o serviço de nuvem, você deve abrir: *. atp.azure.com porta 443 em seu firewall ou proxy. A configuração precisa ser feita no nível do computador (= conta do computador) e não no nível de conta do usuário. Você pode testar a configuração usando as seguintes etapas:
 
1.  Confirme se o **usuário atual** tem acesso ao ponto de extremidade do processador usando o Internet Explorer, navegando até a seguinte URL do CD: https://triprd1wcuse1sensorapi.eastus.cloudapp.azure.com (nos EUA), você deve receber o erro 503:

 ![serviço indisponível](/media/service-unavailable.png)
 
2.  Se não receber um erro 503, examine a configuração de proxy e tente novamente.

3.  Se a configuração de proxy funcionar para **CURRENT_USER** (ou seja, se você vir o erro 503), verifique se as configurações de proxy de WinInet estão habilitadas para a conta **LOCAL_SYSTEM** (usada pelo serviço de atualizador do sensor) executando o seguinte comando no prompt de comandos com privilégios elevados:
 
    reg compare "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" "HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" /v DefaultConnectionSettings

Se você receber o erro "ERRO: O sistema não pôde localizar a chave do registro ou valor especificado." isso significa que nenhum proxy foi definido no nível do **LOCAL_SYSTEM**
 
 ![erro de sistema local do proxy](/media/proxy-local-system-error.png)

Se o resultado for "Resultado comparado: diferente ", isso significa que o proxy foi definido para **LOCAL_SYSTEM**, mas não é o mesmo que o **CURRENT_USER**:
 
  ![resultado de proxy comparado](/media/proxy-result-compared.png)

5.  Se **LOCAL_SYSTEM** não tiver as configurações de proxy corretas (não configuradas ou diferentes de **CURRENT_USER**), talvez seja necessário copiar as configurações de proxy de **CURRENT_ USER** para **LOCAL_SYSTEM**. Não deixe de fazer backup da chave do registro antes de modificá-la:

 Chave do usuário atual: HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings” Chave do sistema local: HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings”

 
6.  Conclua as etapas 4 e 5 para a conta **Local_Service** (é a mesma que **Local_System**, mas deve ser S-1-5-19 em vez de S-1-5-18.



## <a name="see-also"></a>Consulte Também
- [Configurar o encaminhamento de eventos](configure-event-forwarding.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)