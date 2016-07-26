---
title: "Definindo notificações do ATA | Microsoft ATA"
description: "Descreve como definir alertas do ATA para que você seja notificado quando atividades suspeitas forem detectadas."
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
ms.openlocfilehash: 03f6f184e7f34d6985103f503b8d88a3fc820c18


---

# Configurando notificações do ATA
O ATA pode notificar você quando detectar uma atividade suspeita, por email ou usando o encaminhamento de eventos do ATA, e encaminhar o evento para o servidor syslog/SIEM. Antes de selecionar quais notificações quer receber, você precisará [configurar o servidor de email e o servidor Syslog](setting-syslog-email-server-settings.md).

> [!NOTE]
> -   Notificações por email incluem um link que levará o usuário diretamente para a atividade suspeita detectada. A parte do nome do host do link é obtida da configuração da URL do Console do ATA na página do Centro do ATA. Por padrão, a URL do Console do ATA é o endereço IP selecionado durante a instalação do Centro do ATA.  Se você pretende configurar notificações por email, aconselhamos o uso de um FQDN como a URL do Console do ATA.
> -   As notificações são enviadas do Centro do ATA para o servidor SMTP e o servidor Syslog.

Para receber notificações por email, defina o seguinte:


1. No Console do ATA, selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.
![Ícone Definições de configuração do ATA](media/ATA-config-icon.JPG)

2. Selecione **Notificações**.
3. Em **Notificações por email**, use os botões para selecionar quais notificações devem ser enviadas:


    - Nova atividade suspeita foi detectada
    - Novo problema de integridade foi detectado
    - Nova atualização de software está disponível

4. Especifique os destinatários que receberão as notificações por email.

    [!Observação:] alertas de email para atividades suspeitas são enviados somente quando a atividade suspeita é criada.


5. Clique em **Salvar**.

Para receber notificações por Syslog, defina o seguinte:


1. No Console do ATA, selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.
![Ícone Definições de configuração do ATA](media/ATA-config-icon.JPG)

2. Selecione **Notificações**.
3. Em **Notificações do Syslog**, use os botões para selecionar quais notificações devem ser enviadas:


    - Nova atividade suspeita foi detectada
    - Atividade suspeita existente foi atualizada
    - Novo problema de integridade foi detectado
5. Clique em **Salvar**.
![Imagem das configurações de notificação do ATA](media/ATA-notification-settings.png)




## Consulte também
[Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


