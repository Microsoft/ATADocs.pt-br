---
title: "Definição de configurações de notificação por email na Proteção Avançada contra Ameaças do Azure | Microsoft Docs"
description: "Descreve como fazer com que o Azure ATP notifique você (por email ou pelo encaminhamento de eventos do Azure ATP) quando detectar atividades suspeitas"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: a2d29c9c-7ecb-4804-b74b-fde899b28648
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 74fe9976df769ae01c58a5d66ca491c3fa8958d9
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2018
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*



# <a name="integrate-with-syslog"></a>Integrar com o Syslog

O Azure ATP pode notificar você quando detectar atividades suspeitas e alertas de integridade, enviando a notificação para seu servidor Syslog. Se você habilitar as notificações do Syslog, poderá definir os itens a seguir.

1.  Antes de configurar as notificações do Syslog, trabalhe com seu administrador do SIEM para descobrir as seguintes informações:

    -   FQDN ou Endereço IP do servidor SIEM

    -   Porta na qual o servidor SIEM está escutando

    -   O transporte a ser usado: UDP, TCP ou TLS (Syslog protegido)

    -   Formato no qual enviar os dados, RFC 3164 ou 5424

2.  Entre na URL do portal do espaço de trabalho.

3.  Digite seu nome de usuário e senha do Azure Active Directory e clique em **Entrar**.

4.  Selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

    ![Ícone de definições de configuração do Azure ATP](media/ATP-config-menu.png)

5.  Clique em **Notificações**e, em **Notificações do Syslog**, clique em **Configurar** e insira as seguintes informações:

    |Campo|Descrição|
    |---------|---------------|
    |sensor|Selecione um sensor designado para ser responsável por agregar todos os eventos de Syslog e encaminhá-los para seu servidor de SIEM.|
    |Ponto de extremidade de serviço|FQDN do servidor Syslog e, opcionalmente, altere o número da porta (padrão: 514)|
    |Transport|Pode ser UDP, TCP ou TLS (Syslog protegido)|
    |Formato|Trata-se do formato usado pelo Azure ATP para enviar eventos ao servidor de SIEM – RFC 5424 ou RFC 3164.|

 ![Imagem das configurações do servidor Syslog do Azure ATP](media/atp-syslog.png)

6. Você pode selecionar quais eventos enviar ao servidor do Syslog. Em **Notificações do Syslog**, especifique quais notificações devem ser enviadas ao servidor do Syslog: novos alertas de segurança, alertas de segurança atualizados e novos problemas de integridade.


## <a name="see-also"></a>Consulte Também

- [Trabalhando com contas confidenciais](sensitive-accounts.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)