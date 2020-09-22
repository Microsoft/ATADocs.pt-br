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
ms.openlocfilehash: 4b0fd3c0ff5702d382a2232a896a82495cce16be
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912636"
---
# <a name="set-azure-atp-notifications"></a>Definir notificações do Azure ATP

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

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
