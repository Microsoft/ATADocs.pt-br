---
title: Central de Integridade do ATA | Microsoft Docs
description: "Use a Central de Integridade de ATA para verificar como o serviço do ATA está funcionando e seja alertado sobre possíveis problemas."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 85e285c5d88e5916e0bf0eb7dd327cb4cb45b4cb
ms.openlocfilehash: bff593f07d70cd559a1ee75d3b75c61b6534432d


---

*Aplica-se a: Advanced Threat Analytics versão 1.7*



# <a name="ata-health-center"></a>Centro de Integridade de ATA
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

## <a name="see-also"></a>Consulte Também
- [Trabalhando com as configurações de detecção do ATA](working-with-detection-settings.md)
- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jan17_HO1-->


