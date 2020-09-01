---
title: Definir notificações da Proteção Avançada contra Ameaças do Azure
description: Descreve como definir alertas de segurança do Azure ATP para que você seja notificado quando atividades suspeitas forem detectadas.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/04/2018
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 4308f03e-b2a7-4e38-a750-540ff94faa81
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b54f609074c7e2a17eec51629682bade14e40cfa
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88953398"
---
# <a name="set-azure-atp-notifications"></a>Definir notificações do Azure ATP

O Azure ATP pode notificar você quando detectar uma atividade suspeita e emite um alerta de segurança ou um alerta de integridade por email. 

Para receber notificações em um endereço de email específico, defina os seguintes parâmetros:


1. No portal do Azure ATP, selecione a opção de configurações na barra de ferramentas e selecione **Configuração**.

    ![Ícone de definições de configuração do Azure ATP](media/atp-config-menu.png)

1. Clique em **Notificações**.
1. Em **Notificações por email**, especifique quais notificações devem ser enviadas por email – é possível enviar notificações de novos alertas (atividades suspeitas) e novos problemas de integridade. 
 
   > [!NOTE]
   > Alertas de email para atividades suspeitas são enviados somente quando a atividade suspeita é criada.
 
1. Clique em **Salvar**.

    ![Notificações do Azure ATP](media/atp-notifications.png)



## <a name="see-also"></a>Confira Também

- [Configurar coleta de eventos](configure-event-collection.md)

- [Definir configurações de Syslog](setting-syslog.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
