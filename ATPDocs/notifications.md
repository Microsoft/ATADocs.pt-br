---
title: Definir notificações da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Descreve como definir alertas de segurança do Azure ATP para que você seja notificado quando atividades suspeitas forem detectadas.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 10/04/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 4308f03e-b2a7-4e38-a750-540ff94faa81
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5aaf4ad892944b81944639c1f401c0ea9e127bf6
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196685"
---
# <a name="set-azure-atp-notifications"></a>Definir notificações do Azure ATP

O Azure ATP pode notificar você quando detectar uma atividade suspeita e emite um alerta de segurança ou um alerta de integridade por email. 

Para receber notificações em um endereço de email específico, defina os seguintes parâmetros:


1. No portal do Azure ATP, selecione a opção de configurações na barra de ferramentas e selecione **Configuração**.

   ![Ícone de definições de configuração do Azure ATP](media/atp-config-menu.png)

2. Clique em **Notificações**.
3. Em **Notificações por email**, especifique quais notificações devem ser enviadas por email – é possível enviar notificações de novos alertas (atividades suspeitas) e novos problemas de integridade. 
 
   > [!NOTE]
   > Alertas de email para atividades suspeitas são enviados somente quando a atividade suspeita é criada.
 
4. Clique em **Salvar**.

   ![Notificações do Azure ATP](media/atp-notifications.png)



## <a name="see-also"></a>Consulte Também

- [Configurar coleta de eventos](configure-event-collection.md)

- [Definir configurações de Syslog](setting-syslog.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
