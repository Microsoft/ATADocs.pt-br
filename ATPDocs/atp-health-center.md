---
title: Monitorar eventos e a integridade do sistema da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Use o centro de integridade do espaço de trabalho do Azure ATP para verificar como o serviço do Azure ATP está funcionando, ser alertado sobre possíveis problemas e exibir eventos de sistema no Visualizador de Eventos.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 1b7e72c3-a538-443f-981c-398ffafa5ab8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8fdaa7311d39680ed8e9389f5dc9b7cdeca73197
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48782889"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*


# <a name="working-with-azure-atp-workspace-health-and-events"></a>Trabalhando com a integridade e eventos do espaço de trabalho do Azure ATP

## <a name="azure-atp-workspace-health-center"></a>Centro de integridade do espaço de trabalho do Azure ATP 

O centro de integridade do espaço de trabalho do Azure ATP informa sobre o desempenho de seu espaço de trabalho do Azure ATP e alerta quando há problemas.

## <a name="working-with-the-azure-atp-workspace-health-center"></a>Trabalhando com o centro de integridade do espaço de trabalho do Azure ATP

O centro de integridade do espaço de trabalho do Azure ATP permite que você saiba que há um problema gerando um alerta (um ponto vermelho) acima do ícone de Centro de Integridade na barra de menus.

![Barra de ferramentas com ponto vermelho no centro de integridade do espaço de trabalho do Azure ATP](media/atp-health-bar.png)

### <a name="managing-azure-atp-workspace-health"></a>Gerenciando a integridade do espaço de trabalho do Azure ATP
Para verificar a integridade geral de seu espaço de trabalho, clique no ícone do Centro de Integridade na barra de menus ![Ícone do centro de integridade do espaço de trabalho do Azure ATP](media/atp-red-dot.png)

-   Todos os problemas abertos podem ser gerenciados configurando-os para **Fechar** ou **Suprimir** clicando nos três pontos no canto do alerta e fazendo sua escolha.

-   **Abrir**: todas as novas atividades suspeitas aparecem nesta lista.

-   **Fechar**: é usado para rastrear atividades suspeitas que você identificou, pesquisou e corrigiu como mitigado.

    > [!NOTE]
    > O Azure ATP poderá reabrir uma atividade fechada se a mesma atividade for detectada novamente em um curto período.
    
-   **Suprimir**: suprimir uma atividade significa que você deseja ignorá-la por enquanto e apenas ser alertado novamente se houver uma nova instância. Se houver um alerta semelhante, o Azure ATP não o reabrirá. Mas, se o alerta parar por sete dias e for observado novamente, você será alertado novamente.

-   **Reabrir**: você pode reabrir um problema fechado ou suprimido para que ele seja novamente exibido como Aberto na linha do tempo.

-   **Excluir**: dentro da linha do tempo de atividades suspeitas, você também tem a opção de excluir um problema de integridade. Se você excluir um alerta, ele será excluído do espaço de trabalho e você NÃO poderá restaurá-lo. Depois de clicar em Excluir, você poderá excluir todas as atividades suspeitas do mesmo tipo.



![Imagem dos problemas da central de integridade do Azure ATP](media/atp-health-issue.png)






## <a name="see-also"></a>Consulte Também

- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do Azure ATP!](https://aka.ms/azureatpcommunity)
