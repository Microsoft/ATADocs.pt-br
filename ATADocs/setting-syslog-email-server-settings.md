---
title: Definindo as configurações de notificação de email no Advanced Threat Analytics
description: Descreve como fazer o ATA notificar você (por email ou por encaminhamento de eventos do ATA) quando ele detectar atividades suspeitas
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: bff20bf7-8b53-49da-81e5-b818a1c3b24e
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: d56f485a89ee468940ac68ba8e5fad4219753a55
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88955761"
---
# <a name="provide-ata-with-your-email-server-settings"></a>Forneça ao ATA suas configurações do servidor de emails

*Aplica-se a: Advanced Threat Analytics versão 1.9*

O ATA pode notificar você quando detectar uma atividade suspeita. Para que o ATA possa enviar notificações por email, primeiro é necessário definir as **Configurações do servidor de email**.

1. No servidor do Centro do ATA, clique no ícone **Microsoft Advanced Threat Analytics Management** na área de trabalho.

1. Digite seu nome de usuário e senha e clique em **Entrar**.

1. Selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

    ![Ícone Definições de configuração do ATA](media/ATA-config-icon.png)

1. Na seção **Notificações**, em **Servidor de email**, insira as seguintes informações:


   |              Campo              |                                                                                                 Descrição                                                                                                  |               Valor                |
   |---------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------|
   | Ponto de extremidade do servidor SMTP (obrigatório) |                                                            Digite o FQDN do servidor SMTP e, opcionalmente, altere o número da porta (padrão: 25).                                                            | Por exemplo:<br />smtp.contoso.com |
   |               SSL               |                                              Ativar SSL se o servidor SMTP exigir SSL. **Observação:** se você habilitar o SSL, também precisará alterar o número da Porta.                                               |        O padrão é desabilitado         |
   |         Autenticação          | Habilite se o seu servidor SMTP exigir autenticação. **Observação:** Se você habilitar a autenticação, deverá fornecer um nome de usuário e senha de uma conta de email que tenha permissão para se conectar ao servidor SMTP. |        O padrão é desabilitado         |
   |      Enviar de (obrigatório)       |                                                                        Digite um endereço de email a partir do qual o email será enviado.                                                                         | Por exemplo:<br />ATA@contoso.com  |

    ![Imagem das configurações do servidor de emails do ATA](media/ata-email-server.png)

## <a name="provide-ata-with-your-syslog-server-settings"></a>Forneça ao ATA suas configurações do servidor Syslog
O ATA pode notificar você quando detectar uma atividade suspeita, enviando a notificação para seu servidor Syslog. Se você habilitar as notificações do Syslog, poderá definir os itens a seguir.

1. Antes de configurar as notificações do Syslog, trabalhe com seu administrador do SIEM para descobrir as seguintes informações:

   - FQDN ou Endereço IP do servidor SIEM

   - Porta na qual o servidor SIEM está escutando

   - Qual transporte usar: UDP, TCP ou TLS (Syslog protegido)

   - Formato no qual enviar os dados, RFC 3164 ou 5424

1. No servidor do Centro do ATA, clique no ícone **Microsoft Advanced Threat Analytics Management** na área de trabalho.

1. Digite seu nome de usuário e senha e clique em **Entrar**.

1. Selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

    ![Ícone Definições de configuração do ATA](media/ATA-config-icon.png)

1. Na seção Notificações, selecione **Servidor Syslog** insira as seguintes informações:

   |Campo|Descrição|
   |---------|---------------|
   |Ponto de extremidade de servidor Syslog|FQDN do servidor Syslog e, opcionalmente, altere o número da porta (padrão: 514)|
   |Transport|Pode ser UDP, TCP ou TLS (Syslog protegido)|
   |Formato|Este é o formato usado pelo ATA para enviar eventos ao servidor SIEM - RFC 5424 ou RFC 3164.|

    ![Imagem das configurações do servidor Syslog do ATA](media/ata-syslog-server-settings.png)



## <a name="see-also"></a>Consulte Também
[Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
