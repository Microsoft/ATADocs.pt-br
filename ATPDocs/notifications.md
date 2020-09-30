---
title: Definir notificações da Proteção Avançada contra Ameaças do Azure
description: Descreve como definir alertas de segurança do Azure ATP para que você seja notificado quando atividades suspeitas forem detectadas.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/29/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 4308f03e-b2a7-4e38-a750-540ff94faa81
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b60044cbc2ccf05ff1802ecce6e3e11d42543f97
ms.sourcegitcommit: dd8435ba20f76a6fc4590980c040c6fc7ec6c62b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91451747"
---
# <a name="set-azure-atp-notifications"></a>Definir notificações do Azure ATP

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

O Azure ATP pode notificar você quando detectar uma atividade suspeita e emite um alerta de segurança ou um alerta de integridade por email.

Para receber notificações em um endereço de email específico, defina os seguintes parâmetros:

1. No portal do Azure ATP, selecione a opção de configurações na barra de ferramentas e selecione **Configuração**.

    ![Ícone de definições de configuração do Azure ATP](media/atp-config-menu.png)

1. Clique em **Notificações**.
1. Em **Notificações por email**, adicione endereços de email para as notificações que deseja receber. Você poderá receber notificações referentes a novos alertas (atividades suspeitas) e problemas de integridade.

    > [!NOTE]
    >
    > - Os emails são enviados somente para notificações em que há endereços de email definidos.
    > - Alertas de email para atividades suspeitas são enviados somente quando a atividade suspeita é criada.

1. Clique em **Save** (Salvar).

    ![Notificações do Azure ATP](media/atp-notifications.png)

## <a name="see-also"></a>Consulte Também

- [Configurar coleta de eventos](configure-event-collection.md)

- [Definir configurações de Syslog](setting-syslog.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
