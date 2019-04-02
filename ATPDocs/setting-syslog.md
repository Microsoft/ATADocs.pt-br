---
title: Definição de configurações do syslog na Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Descreve como fazer com que o Azure ATP notifique você (por email ou pelo encaminhamento de eventos do Azure ATP) quando detectar atividades suspeitas
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 12/02/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: a2d29c9c-7ecb-4804-b74b-fde899b28648
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b3df102272b045f34eb64b11d97077b9ce1951ad
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2019
ms.locfileid: "58674224"
---
# <a name="integrate-with-syslog"></a>Integrar com o Syslog

O Azure ATP poderá notificar você quando detectar atividades suspeitas e alertas de segurança de problemas, assim como alertas de integridade enviando a notificação para seu servidor Syslog. Se você habilitar as notificações do Syslog, poderá definir o seguinte:

1. Antes de configurar as notificações do Syslog, trabalhe com seu administrador do SIEM para descobrir as seguintes informações:

   -   FQDN ou Endereço IP do servidor SIEM

   -   Porta na qual o servidor SIEM está escutando

   -   Qual transporte usar: UDP, TCP ou TLS (Syslog protegido)

   -   Formato no qual enviar os dados, RFC 3164 ou 5424

2. Insira a URL da instância.

3. Digite seu nome de usuário e senha do Azure Active Directory e clique em **Entrar**.

4. Selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

   ![Ícone de definições de configuração do Azure ATP](media/ATP-config-menu.png)

5. Clique em **Notificações**e, em **Notificações do Syslog**, clique em **Configurar** e insira as seguintes informações:

   |Campo|Descrição|
   |---------|---------------|
   |sensor|Selecione um sensor designado para ser responsável por agregar todos os eventos de Syslog e encaminhá-los para seu servidor de SIEM.|
   |Ponto de extremidade de serviço|FQDN do servidor Syslog e, opcionalmente, altere o número da porta (padrão: 514)|
   |Transport|Pode ser UDP, TCP ou TLS (Syslog protegido)|
   |Formato|Trata-se do formato usado pelo Azure ATP para enviar eventos ao servidor de SIEM – RFC 5424 ou RFC 3164.|

   ![Imagem das configurações do servidor Syslog do Azure ATP](media/atp-syslog.png)

6. Você pode selecionar quais eventos enviar ao servidor do Syslog. Em **Notificações do Syslog**, especifique quais notificações devem ser enviadas ao servidor do Syslog: novos alertas de segurança, alertas de segurança atualizados e novos problemas de integridade.

> [!NOTE]
> Caso planeje criar automação ou scripts para logs de SIEM do ATP do Azure, é recomendável usar o campo **externalId** para identificar o tipo de alerta em vez de usar o nome do alerta para essa finalidade. Nomes de alertas, ocasionalmente, podem ser modificados, enquanto o **externalId** de cada alerta é permanente. Para saber mais, confira [Referência de logs SIEM da Proteção Avançada contra Ameaças do Azure](cef-format-sa.md). 


## <a name="see-also"></a>Consulte Também

- [Trabalhando com contas confidenciais](sensitive-accounts.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
