---
title: Definição das configurações de notificação de email no Advanced Threat Analytics | Microsoft Docs
description: Descreve como fazer o ATA notificar você (por email ou por encaminhamento de eventos do ATA) quando ele detectar atividades suspeitas
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: bff20bf7-8b53-49da-81e5-b818a1c3b24e
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f415fabe71512a5f9948a824d04e7bfece086ba4
ms.sourcegitcommit: ca6153d046d8ba225ee5bf92cf55d0bd57cf4765
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2018
ms.locfileid: "39585028"
---
*Aplica-se a: Advanced Threat Analytics versão 1.9*



# <a name="provide-ata-with-your-email-server-settings"></a>Forneça ao ATA suas configurações do servidor de emails
O ATA pode notificar você quando detectar uma atividade suspeita. Para que o ATA possa enviar notificações por email, primeiro é necessário definir as **Configurações do servidor de email**.

1.  No servidor do Centro do ATA, clique no ícone **Microsoft Advanced Threat Analytics Management** na área de trabalho.

2.  Digite seu nome de usuário e senha e clique em **Entrar**.

3.  Selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

    ![Ícone Definições de configuração do ATA](media/ATA-config-icon.png)

4.  Na seção **Notificações**, em **Servidor de email**, insira as seguintes informações:

    |Campo|Descrição|Valor|
    |---------|---------------|---------|
    |Ponto de extremidade do servidor SMTP (obrigatório)|Digite o FQDN do servidor SMTP e, opcionalmente, altere o número da porta (padrão: 25).|Por exemplo:<br />smtp.contoso.com|
    |SSL|Ativar SSL se o servidor SMTP exigir SSL. **Observação:** se você habilitar o SSL, também precisará alterar o número da Porta.|O padrão é desabilitado|
    |Autenticação|Habilite se o seu servidor SMTP exigir autenticação. **Observação:** se você habilitar a autenticação, será necessário fornecer um nome de usuário e senha de uma conta de email que tenha permissão para se conectar ao servidor SMTP.|O padrão é desabilitado|
    |Enviar de (obrigatório)|Digite um endereço de email a partir do qual o email será enviado.|Por exemplo:<br />ATA@contoso.com|
    
    ![Imagem das configurações do servidor de emails do ATA](media/ata-email-server.png)

## <a name="provide-ata-with-your-syslog-server-settings"></a>Forneça ao ATA suas configurações do servidor Syslog
O ATA pode notificar você quando detectar uma atividade suspeita, enviando a notificação para seu servidor Syslog. Se você habilitar as notificações do Syslog, poderá definir os itens a seguir.

1.  Antes de configurar as notificações do Syslog, trabalhe com seu administrador do SIEM para descobrir as seguintes informações:

    -   FQDN ou Endereço IP do servidor SIEM

    -   Porta na qual o servidor SIEM está escutando

    -   O transporte a ser usado: UDP, TCP ou TLS (Syslog protegido)

    -   Formato no qual enviar os dados, RFC 3164 ou 5424

2.  No servidor do Centro do ATA, clique no ícone **Microsoft Advanced Threat Analytics Management** na área de trabalho.

3.  Digite seu nome de usuário e senha e clique em **Entrar**.

4.  Selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

    ![Ícone Definições de configuração do ATA](media/ATA-config-icon.png)

5.  Na seção Notificações, selecione **Servidor Syslog** insira as seguintes informações:

    |Campo|Descrição|
    |---------|---------------|
    |Ponto de extremidade de servidor Syslog|FQDN do servidor Syslog e, opcionalmente, altere o número da porta (padrão: 514)|
    |Transport|Pode ser UDP, TCP ou TLS (Syslog protegido)|
    |Formato|Este é o formato usado pelo ATA para enviar eventos ao servidor SIEM - RFC 5424 ou RFC 3164.|

 ![Imagem das configurações do servidor Syslog do ATA](media/ata-syslog-server-settings.png)



## <a name="see-also"></a>Consulte Também
[Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
