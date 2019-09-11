---
title: Definição das configurações do Syslog na Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Descreve como fazer com que o Azure ATP notifique você (por email ou pelo encaminhamento de eventos do Azure ATP) quando detectar atividades suspeitas
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: a2d29c9c-7ecb-4804-b74b-fde899b28648
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0d2befa95ca0bc8fd87cb5fa2dc6563646892945
ms.sourcegitcommit: e4f108aec3cbfd88562217e36195b5d1250a1bbd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2019
ms.locfileid: "70803219"
---
# <a name="integrate-with-syslog"></a>Integrar com o Syslog

O ATP do Azure poderá notificar você quando detectar atividades suspeitas e alertas de segurança de problemas, bem como com alertas de integridade, enviando a notificação do sensor selecionado para seu servidor Syslog. Se você habilitar as notificações do Syslog, poderá definir o seguinte:

   |Campo|Descrição|
   |---------|---------------|
   |sensor|Selecione um sensor designado para ser responsável por agregar todos os eventos de Syslog e encaminhá-los para seu servidor de SIEM.|
   |Ponto de extremidade de serviço|FQDN do servidor Syslog e, opcionalmente, altere o número da porta (padrão: 514)|
   |Transport|Pode ser UDP, TCP ou TLS (Syslog protegido)|
   |Formato|Trata-se do formato usado pelo Azure ATP para enviar eventos ao servidor de SIEM – RFC 5424 ou RFC 3164.|

1. Antes de configurar as notificações do Syslog, trabalhe com seu administrador do SIEM para descobrir as seguintes informações:

   -   FQDN ou Endereço IP do servidor SIEM

   -   Porta na qual o servidor SIEM está escutando

   -   Qual transporte usar: UDP, TCP ou TLS (Syslog protegido)

   -   Formato no qual enviar os dados, RFC 3164 ou 5424

1. Abra o portal do ATP do Azure. 
2. Clique em **Configurações**.
3. No submenu **Notificações e Relatórios**, selecione **Notificações**. 
1. Na opção **Serviço Syslog**, clique em **Configurar**.
1. Selecione o **Sensor**. 
1. Insira a URL do **Ponto de extremidade de serviço**.
1. Selecione o protocolo de **Transporte** (TCP ou UDP). 
1. Selecione o formato (RFC 3164 ou RFC 5424). 
1. Selecione **Enviar mensagem de texto do Syslog** e verifique se a mensagem foi recebida na sua solução de infraestrutura de Syslog. 
1. Clique em **Salvar**. 

Para revisar ou modificar suas configurações do Syslog.  

3. Clique em **Notificações**e, em **Notificações do Syslog**, clique em **Configurar** e insira as seguintes informações:

   ![Imagem das configurações do servidor Syslog do Azure ATP](media/atp-syslog.png)

4. Você pode selecionar quais eventos enviar ao servidor do Syslog. Em **Notificações do Syslog**, especifique quais notificações devem ser enviadas ao servidor do Syslog: novos alertas de segurança, alertas de segurança atualizados e novos problemas de integridade.

> [!NOTE]
> Caso planeje criar automação ou scripts para logs de SIEM do ATP do Azure, é recomendável usar o campo **externalId** para identificar o tipo de alerta em vez de usar o nome do alerta para essa finalidade. Nomes de alertas, ocasionalmente, podem ser modificados, enquanto o **externalId** de cada alerta é permanente. Para saber mais, confira [Referência de logs SIEM da Proteção Avançada contra Ameaças do Azure](cef-format-sa.md). 


## <a name="see-also"></a>Consulte Também

- [Trabalhando com contas confidenciais](sensitive-accounts.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
