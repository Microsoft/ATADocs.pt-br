---
# required metadata

title: Configuração de alertas do ATA | Microsoft Advanced Threat Analytics
description: Descreve como fazer o ATA alertar você (por email ou por encaminhamento de eventos do ATA) quando ele detectar atividades suspeitas 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configurando os alertas do ATA
O ATA pode alertar você quando detectar uma atividade suspeita, por email ou usando o encaminhamento de eventos do ATA, e encaminhando o evento para o servidor syslog/SIEM. Se você habilitar um ou os dois tipos de alertas, você poderá definir o seguinte sobre eles.

> [!NOTE]
> -   Notificações por email incluem um link que levará o usuário diretamente para a atividade suspeita detectada. A parte do nome do host do link é obtida da configuração da URL do Console do ATA na página do Centro do ATA. Por padrão, a URL do Console do ATA é o endereço IP selecionado durante a instalação do Centro do ATA.  Se você pretende configurar alertas de email, recomendamos o uso de um FQDN como a URL do Console do ATA.
> -   Alertas do Alerta de Integridade do Sistema são enviados apenas por email.
> -   Alertas são enviados do Centro do ATA para o servidor SMTP e o servidor Syslog.
> -   Alertas de email para atividades suspeitas são enviados somente quando a atividade suspeita é criada.

## Configuração de idioma e frequência
A configuração **Idioma** aplica-se às notificações enviadas por email e notificações enviadas ao servidor Syslog.

A configuração **Frequência** se aplica somente a notificações enviadas ao servidor Syslog.

1.  Abra o Console do ATA.

2.  Selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

    ![Ícone Definições de configuração do ATA](media/ATA-config-icon.JPG)

3.  Escolha **Alertas**.

4.  Em **Idioma**, escolha o idioma de sua escolha.

5.  Em **Frequência**, escolha **Baixa frequência** se você quiser receber uma breve notificação apenas quando um novo alerta for gerado. Selecione **Alta frequência** se você quiser receber uma notificação detalhada quando um novo alerta for gerado, bem como quando os alertas existentes forem modificados.

    ![Imagem de Configuração de detalhamento do alerta](media/ATA-alerts-verbosity-language.png)

6.  Clique em **Salvar**.

## Configuração de alertas de email
O ATA para alertar você quando detectar uma atividade suspeita. Se você habilitar os alertas de email, poderá definir o seguinte sobre eles.

1.  No servidor do Centro do ATA, clique no ícone **Microsoft Advanced Threat Analytics Management** na área de trabalho.

2.  Digite seu nome de usuário e senha e clique em **Entrar**.

3.  Selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

    ![Ícone Definições de configuração do ATA](media/ATA-config-icon.JPG)

4.  Escolha **Alertas**.

5.  Ative **Email** para habilitar os alertas por email e digite as seguintes informações:

    |Campo|Descrição|Valor|
    |---------|---------------|---------|
    |Ponto de extremidade do servidor SMTP (obrigatório)|Digite o FQDN do servidor SMTP.|Por exemplo:<br />smtp.contoso.com|
    |SSL|Ativar SSL se o servidor SMTP exigir SSL. **Observação:** se você habilitar o SSL, também precisará alterar o número da Porta.|O padrão é desabilitado|
    |Autenticação|Habilite se o seu servidor SMTP exigir autenticação. **Observação:** se você habilitar a autenticação, será necessário fornecer um nome de usuário e senha de uma conta de email que tenha permissão para se conectar ao servidor SMTP.|O padrão é desabilitado|
    |Enviar de (obrigatório)|Digite um endereço de email a partir do qual o email será enviado.|Por exemplo:<br />ATA@contoso.com|
    |Enviar para (obrigatório)|Digite os endereços de email dos usuários ou grupos de email que devem receber emails quando o ATA detectar uma atividade suspeita. **Observação:** digite um endereço de email por vez e clique no sinal de adição para acrescentá-lo.|Por exemplo:<br />securityteam@contoso.com|

## Configuração do encaminhamento de evento do ATA para o SIEM
O ATA pode alertar você quando detectar uma atividade suspeita, enviando o alerta para seu servidor Syslog. Se você habilitar os alertas do Syslog, poderá definir o seguinte sobre eles.

1.  Antes de configurar os alertas do Syslog, trabalhe com seu administrador do SIEM para descobrir as seguintes informações:

    -   FQDN ou Endereço IP do servidor SIEM

    -   Porta na qual o servidor SIEM está escutando

    -   Qual transporte usar UDP ou TCP ou TCP Protegido

    -   Formato no qual enviar os dados, RFC 3164 ou 5424

2.  No servidor do Centro do ATA, clique no ícone **Microsoft Advanced Threat Analytics Management** na área de trabalho.

3.  Digite seu nome de usuário e senha e clique em **Entrar**.

4.  Selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

    ![Ícone Definições de configuração do ATA](media/ATA-config-icon.JPG)

5.  Escolha **Alertas**.

6.  Ative o **Syslog** para permitir que os alertas sobre atividades suspeitas sejam enviados ao servidor Syslog e insira as seguintes informações:

    |Campo|Descrição|
    |---------|---------------|
    |Ponto de extremidade de servidor Syslog|FQDN do servidor Syslog|
    |Transport|Pode ser UDC, TCP ou TCP Protegido|
    |Formato|Este é o formato usado pelo ATA para enviar eventos ao servidor SIEM - RFC 5424 ou RFC 3164.|

## Consulte também
[Para obter suporte, confira nosso fórum!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


