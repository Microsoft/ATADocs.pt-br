---
title: Monitorar os eventos e a integridade do sistema do Advanced Threat Analytics | Microsoft Docs
description: Use a Central de Integridade de ATA para verificar como o serviço do ATA está funcionando e seja alertado sobre possíveis problemas e exibir eventos de sistema no Visualizador de Eventos.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7bf91f258d1eaf9c83cc610fc43dfa52a2da3e6b
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166894"
---
*Aplica-se a: Advanced Threat Analytics versão 1.9*


# <a name="working-with-ata-system-health-and-events"></a>Trabalhando com eventos e a integridade do sistema ATA

## <a name="ata-health-center"></a>Centro de Integridade de ATA
A Central de Integridade de ATA permite saber como seu serviço ATA está sendo executado e alerta-o para os problemas.

## <a name="working-with-the-ata-health-center"></a>Trabalhando com a Central de Integridade de ATA
A Central de Integridade de ATA permite que você saiba se há um problema gerando um alerta (um ponto vermelho) acima do ícone Central de Integridade na barra de menus.

![Barra de ferramentas do ponto vermelho da Central de Integridade do ATA](media/ATA-Health-Center-Alert-red-dot.png)

### <a name="managing-ata-health"></a>Gerenciando a Integridade de ATA
Para verificar a integridade geral do sistema, clique no ícone Central de Integridade na barra de menus ![Ícone Central de Integridade de ATA](media/ATA-red-dot.png)

-   Todos os alertas abertos podem ser gerenciados configurando-os para **Fechar**, **Suprimir** ou **Excluir** clicando nos três pontos no canto do alerta e fazendo sua escolha.

-   **Abrir**: todas as novas atividades suspeitas aparecem nesta lista.

-   **Fechar**: é usado para rastrear atividades suspeitas que você identificou, pesquisou e corrigiu como mitigado.

    > [!NOTE]
    > O ATA pode reabrir uma atividade fechada se a mesma atividade for novamente detectada em um curto período de tempo.

-   **Suprimir**: suprimir uma atividade significa que você deseja ignorá-la por enquanto e apenas ser alertado novamente se houver uma nova instância. Se houver um alerta semelhante, o ATA não reabrirá. Mas, se o alerta parar por sete dias e for observado novamente, você será alertado novamente.

- **Excluir**: se você excluir um alerta, ele será excluído do sistema, do banco de dados e você NÃO poderá restaurá-lo. Depois de clicar em Excluir, você poderá excluir todas as atividades suspeitas do mesmo tipo.



![Imagem dos problemas da Central de Integridade de ATA](media/ATA-Health-Issue.JPG)






## <a name="see-also"></a>Consulte Também

- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
