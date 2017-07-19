---
title: Monitorar os eventos e a integridade do sistema do Advanced Threat Analytics | Microsoft Docs
description: "Use a Central de Integridade de ATA para verificar como o serviço do ATA está funcionando e seja alertado sobre possíveis problemas e exibir eventos de sistema no Visualizador de Eventos."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 59e5cafcff7b84ffb9dc161cd0b50cd3014e455a
ms.sourcegitcommit: 3177d5894413fbd363b9aca8130f3f7a369223b8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*


# <a name="working-with-ata-system-health-and-events"></a>Trabalhando com eventos e a integridade do sistema ATA

## <a name="ata-health-center"></a>Centro de Integridade de ATA
A Central de Integridade de ATA permite saber como seu serviço ATA está sendo executado e alerta-o para os problemas.

## <a name="working-with-the-ata-health-center"></a>Trabalhando com a Central de Integridade de ATA
A Central de Integridade de ATA permite que você saiba se há um problema gerando um alerta (um ponto vermelho) acima do ícone Central de Integridade na barra de menus.

![Barra de ferramentas do ponto vermelho da Central de Integridade do ATA](media/ATA-Health-Center-Alert-red-dot.png)

### <a name="managing-ata-health"></a>Gerenciando a Integridade de ATA
Para verificar a integridade geral do sistema, clique no ícone Central de Integridade na barra de menus ![Ícone Central de Integridade de ATA](media/ATA-red-dot.png)

-   Todos os alertas abertos podem ser gerenciados definindo-os como **Resolvido** ou **Ignorado**. No Alerta, clique em **Abrir** e role para baixo até **Resolvido** ou **Ignorado**.

-   Se você resolver um problema e o ATA detectar que ele persiste, o problema será automaticamente retornado para a lista de problemas **Abrir**. Se o ATA detectar que um problema aberto está resolvido, ele será automaticamente movido para a lista de problemas **Resolvido**.

-   Os problemas em **Ignorado** são aqueles que você não deseja que o ATA continue a verificar - por exemplo, se você for alertado para um problema que sabe que existe e não planeja resolvê-lo, mas não deseja continuar recebendo notificações sobre ele e não deseja vê-lo em sua lista de problemas **Abrir**, poderá defini-lo para **Ignorado**.

![Imagem dos problemas da Central de Integridade de ATA](media/ATA-Health-Issue.JPG)






## <a name="see-also"></a>Consulte também

- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
