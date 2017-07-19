---
title: "Configuração de notificações do Advanced Threat Analytics | Microsoft Docs"
description: "Descreve como definir alertas do ATA para que você seja notificado quando atividades suspeitas forem detectadas."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/12/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: cc7f5d2e75076b1f684ad76daca9ceb35e0d30e3
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*



# <a name="set-ata-notifications"></a>Definir notificações do ATA
O ATA pode notificar você quando detectar uma atividade suspeita, por email ou usando o encaminhamento de eventos do ATA, e encaminhar o evento para o servidor syslog/SIEM. Antes de selecionar quais notificações quer receber, você precisará [configurar o servidor de email e o servidor Syslog](setting-syslog-email-server-settings.md).

> [!NOTE]
> -   Notificações por email incluem um link que levará o usuário diretamente para a atividade suspeita detectada. A parte do nome do host do link é obtida da configuração da URL do Console do ATA na página do Centro do ATA. Por padrão, a URL do Console do ATA é o endereço IP selecionado durante a instalação do Centro do ATA.  Se você pretende configurar notificações por email, aconselhamos o uso de um FQDN como a URL do Console do ATA.
> -   As notificações são enviadas do Centro do ATA para o servidor SMTP e o servidor Syslog.


Para receber notificações, defina o seguinte:


1. No Console do ATA, selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

![Ícone Definições de configuração do ATA](media/ATA-config-icon.png)

2. Na seção **Notifications & Reports (Notificações e Relatórios)**, selecione **Notificações**.
3. Em **Notificações por Email**, especifique quais notificações devem ser enviadas por email: novas atividades suspeitas e novos problemas de integridade. Você pode definir um endereço de email separado para o qual enviar as atividades suspeitas e para os alertas de integridade para que, por exemplo, notificações de atividades suspeitas possam ser enviadas para o analista de segurança e as notificações de alerta de integridade possam ser enviadas para o administrador de TI.
>   [!NOTE]
>   Alertas de email para atividades suspeitas são enviados somente quando a atividade suspeita é criada.
3. Em **Syslog notifications (Notificações do Syslog)**, especifique quais notificações devem ser enviadas para o servidor Syslog: novas atividades suspeitas, atividades suspeitas atualizadas e novos problemas de integridade.
5. Clique em **Salvar**.

![Imagem das configurações de notificação de email do ATA](media/ata-mail-notification-settings.png)




## <a name="see-also"></a>Consulte também
[Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
