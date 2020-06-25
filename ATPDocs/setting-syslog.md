---
title: Definir configurações do Syslog na Proteção Avançada contra Ameaças do Azure
description: Descreve como fazer com que o Azure ATP notifique você (por email ou pelo encaminhamento de eventos do Azure ATP) quando detectar atividades suspeitas
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: a2d29c9c-7ecb-4804-b74b-fde899b28648
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5a7d5fbaf2313b6876c2fbdcc6bde84aaa89cbd5
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2020
ms.locfileid: "84775872"
---
# <a name="integrate-with-syslog"></a>Integrar com o Syslog

> [!NOTE]
> Os recursos do ATP do Azure explicados nesta página também podem ser acessados usando o novo [portal](https://portal.cloudappsecurity.com).

O ATP do Azure poderá notificar você quando detectar atividades suspeitas enviando alertas de segurança e de integridade para seu servidor Syslog por meio de um sensor indicado.

Após habilitar as notificações do Syslog, você poderá definir o seguinte:

   |Campo|Descrição|
   |---------|---------------|
   |sensor|Selecione um sensor designado para ser responsável por agregar todos os eventos de Syslog e encaminhá-los para seu servidor de SIEM.|
   |Ponto de extremidade de serviço|FQDN do servidor Syslog e, opcionalmente, altere o número da porta (padrão: 514)|
   |Transport|Pode ser UDP, TCP ou TLS (Syslog protegido)|
   |Formato|Trata-se do formato usado pelo Azure ATP para enviar eventos ao servidor de SIEM – RFC 5424 ou RFC 3164.|

1. Antes de configurar as notificações do Syslog, trabalhe com seu administrador do SIEM para descobrir as seguintes informações:

    - FQDN ou Endereço IP do servidor SIEM
    - Porta na qual o servidor SIEM está escutando
    - Qual transporte usar: UDP, TCP ou TLS (Syslog protegido)
    - Formato no qual enviar os dados, RFC 3164 ou 5424

1. Abra o portal do ATP do Azure.
1. Clique em **Configurações**.
1. No submenu **Notificações e Relatórios**, selecione **Notificações**.
1. Na opção **Serviço Syslog**, clique em **Configurar**.
1. Selecione o **Sensor**.
1. Insira a URL do **Ponto de extremidade de serviço**.
1. Selecione o protocolo de **Transporte** (TCP ou UDP).
1. Selecione o formato (RFC 3164 ou RFC 5424).
1. Selecione **Enviar mensagem de texto do Syslog** e verifique se a mensagem foi recebida na sua solução de infraestrutura de Syslog.
1. Clique em **Salvar**.

Para revisar ou modificar suas configurações do Syslog.

1. Clique em **Notificações**e, em **Notificações do Syslog**, clique em **Configurar** e insira as seguintes informações:

   ![Imagem das configurações do servidor Syslog do Azure ATP](media/atp-syslog.png)

1. Você pode selecionar quais eventos enviar ao servidor do Syslog. Em **Notificações do Syslog**, especifique quais notificações devem ser enviadas ao servidor do Syslog: novos alertas de segurança, alertas de segurança atualizados e novos problemas de integridade.

> [!NOTE]
> Caso planeje criar automação ou scripts para logs de SIEM do ATP do Azure, é recomendável usar o campo **externalId** para identificar o tipo de alerta em vez de usar o nome do alerta para essa finalidade. Nomes de alertas, ocasionalmente, podem ser modificados, enquanto o **externalId** de cada alerta é permanente. Para saber mais, confira [Referência de logs SIEM da Proteção Avançada contra Ameaças do Azure](cef-format-sa.md).

## <a name="see-also"></a>Consulte Também

- [Trabalhando com contas confidenciais](sensitive-accounts.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
