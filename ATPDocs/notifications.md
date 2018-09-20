---
title: Definir notificações da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Descreve como definir alertas do Azure ATP para que você seja notificado quando atividades suspeitas forem detectadas.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4308f03e-b2a7-4e38-a750-540ff94faa81
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c3fc5adbb700c4b8df66c243a655cf98aacc79af
ms.sourcegitcommit: 9f02f0f6669b25f39b616bb0885bb55b8c4f050b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/19/2018
ms.locfileid: "46362418"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*


# <a name="set-azure-atp-notifications"></a>Definir notificações do Azure ATP

O Azure ATP pode notificar você quando detectar uma atividade suspeita ou um alerta de integridade por email. 

Para receber notificações em um endereço de email específico, defina os seguintes parâmetros:


1. No portal do espaço de trabalho do Azure ATP, selecione a opção de configurações na barra de ferramentas e selecione **Configuração**.

![Ícone de definições de configuração do Azure ATP](media/atp-config-menu.png)

2. Clique em **Notificações**.
3. Em **Notificações por email**, especifique quais notificações devem ser enviadas por email – é possível enviar notificações de novos alertas (atividades suspeitas) e novos problemas de integridade. 
 
 >  [!NOTE]
 >   Alertas de email para atividades suspeitas são enviados somente quando a atividade suspeita é criada.
 
4. Clique em **Salvar**.

 ![Notificações do Azure ATP](media/atp-notifications.png)



## <a name="see-also"></a>Consulte Também

- [Configurar coleta de eventos](configure-event-collection.md)

- [Definir configurações de Syslog](setting-syslog.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)
