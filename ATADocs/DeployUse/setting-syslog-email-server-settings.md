---
title: "Definindo notificações do ATA | Microsoft ATA"
description: "Descreve como fazer o ATA notificar você (por email ou por encaminhamento de eventos do ATA) quando ele detectar atividades suspeitas"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 5864070fe3ad5aedf1ff79d8386caba4b6a79adc


---

## Forneça ao ATA suas configurações do servidor de emails
O ATA pode notificar você quando detectar uma atividade suspeita. Para que o ATA possa enviar notificações por email, primeiro é necessário definir as **Configurações do servidor de email**.

1.  No servidor do Centro do ATA, clique no ícone **Microsoft Advanced Threat Analytics Management** na área de trabalho.

2.  Digite seu nome de usuário e senha e clique em **Entrar**.

3.  Selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

    ![Ícone Definições de configuração do ATA](media/ATA-config-icon.JPG)

4.  Na guia **Geral**, em **Servidor de emails**, insira as seguintes informações:

    |Campo|Descrição|Valor|
    |---------|---------------|---------|
    |Ponto de extremidade do servidor SMTP (obrigatório)|Digite o FQDN do servidor SMTP.|Por exemplo:<br />smtp.contoso.com|
    |SSL|Ativar SSL se o servidor SMTP exigir SSL. **Observação:** se você habilitar o SSL, também precisará alterar o número da Porta.|O padrão é desabilitado|
    |Autenticação|Habilite se o seu servidor SMTP exigir autenticação. **Observação:** se você habilitar a autenticação, será necessário fornecer um nome de usuário e senha de uma conta de email que tenha permissão para se conectar ao servidor SMTP.|O padrão é desabilitado|
    |Enviar de (obrigatório)|Digite um endereço de email a partir do qual o email será enviado.|Por exemplo:<br />ATA@contoso.com|
    ![Imagem das configurações do servidor de emails do ATA](media/ATA-email-server.png)

## Forneça ao ATA suas configurações do servidor Syslog
O ATA pode notificar você quando detectar uma atividade suspeita, enviando a notificação para seu servidor Syslog. Se você habilitar as notificações do Syslog, poderá definir os itens a seguir.

1.  Antes de configurar as notificações do Syslog, trabalhe com seu administrador do SIEM para descobrir as seguintes informações:

    -   FQDN ou Endereço IP do servidor SIEM

    -   Porta na qual o servidor SIEM está escutando

    -   O transporte a ser usado: UDP, TCP ou TLS (Syslog protegido)

    -   Formato no qual enviar os dados, RFC 3164 ou 5424

2.  No servidor do Centro do ATA, clique no ícone **Microsoft Advanced Threat Analytics Management** na área de trabalho.

3.  Digite seu nome de usuário e senha e clique em **Entrar**.

4.  Selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

    ![Ícone Definições de configuração do ATA](media/ATA-config-icon.JPG)

5.  Selecione **Servidor Syslog** e insira as seguintes informações:

    |Campo|Descrição|
    |---------|---------------|
    |Ponto de extremidade de servidor Syslog|FQDN do servidor Syslog|
    |Transport|Pode ser UDC, TCP ou TLS (Syslog protegido)|
    |Formato|Este é o formato usado pelo ATA para enviar eventos ao servidor SIEM - RFC 5424 ou RFC 3164.|





## Consulte também
[Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


