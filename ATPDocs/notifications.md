---
title: Definir notificações do Microsoft Defender para Identidade
description: Descreve como definir os alertas de segurança do Microsoft Defender para Identidade para que você seja notificado quando atividades suspeitas forem detectadas.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 3eb687b716ce69bb4be0aabc2b128b1cf46242ff
ms.sourcegitcommit: 07a855b87931875bdeca14b152b13a36db79bfa8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "94847132"
---
# <a name="set-product-long-notifications"></a>Definir notificações do [!INCLUDE [Product long](includes/product-long.md)]

O [!INCLUDE [Product long](includes/product-long.md)] pode notificar você quando detectar uma atividade suspeita e emitir um alerta de segurança ou um alerta de integridade por email.

Para receber notificações em um endereço de email específico, defina os seguintes parâmetros:

1. No portal do [!INCLUDE [Product short](includes/product-short.md)], selecione o ícone de engrenagem na barra de ferramentas e clique em **Configuração**.

    ![Ícone de definições de configuração do [!INCLUDE [Product short](includes/product-short.md)]](media/config-menu.png)

1. Clique em **Notificações**.
1. Em **Notificações por email**, adicione endereços de email para as notificações que deseja receber. Você poderá receber notificações referentes a novos alertas (atividades suspeitas) e problemas de integridade.

    > [!NOTE]
    >
    > - Os emails são enviados somente para notificações em que há endereços de email definidos.
    > - Alertas de email para atividades suspeitas são enviados somente quando a atividade suspeita é criada.

1. Clique em **Save** (Salvar).

    ![Notificações do [!INCLUDE [Product short](includes/product-short.md)]](media/notifications.png)

## <a name="see-also"></a>Consulte Também

- [Configurar coleta de eventos](configure-event-collection.md)

- [Definir configurações de Syslog](setting-syslog.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
