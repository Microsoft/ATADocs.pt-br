---
title: Monitorar eventos e a integridade do sistema da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Use o centro de integridade do workspace do Azure ATP para verificar como o serviço do Azure ATP está funcionando, ser alertado sobre possíveis problemas e exibir eventos de sistema no Visualizador de Eventos.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 11/28/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 1b7e72c3-a538-443f-981c-398ffafa5ab8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 100964d904c7cda48e75cb5401fbba8a3ec0718e
ms.sourcegitcommit: f4f2a1b2c674c4dba7a46ece0624f5ea10c4865e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2018
ms.locfileid: "52744652"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*


# <a name="working-with-azure-atp-workspace-health-and-events"></a>Trabalhando com a integridade e eventos do workspace do Azure ATP

## <a name="azure-atp-workspace-health-center"></a>Centro de integridade do workspace do Azure ATP 

O centro de integridade do workspace do Azure ATP informa sobre o desempenho de seu workspace do Azure ATP e alerta quando há problemas.

## <a name="working-with-the-azure-atp-workspace-health-center"></a>Trabalhando com o centro de integridade do workspace do Azure ATP

O centro de integridade do workspace do Azure ATP permite que você saiba que há um problema gerando um alerta (um ponto vermelho) acima do ícone de Centro de Integridade na barra de menus.

![Barra de ferramentas com ponto vermelho no centro de integridade do workspace do Azure ATP](media/atp-health-bar.png)

### <a name="managing-azure-atp-workspace-health"></a>Gerenciando a integridade do workspace do Azure ATP
Para verificar a integridade geral de seu workspace, clique no ícone do Centro de Integridade na barra de menus ![Ícone do centro de integridade do workspace do Azure ATP](media/atp-red-dot.png)

-   Todos os problemas abertos podem ser gerenciados configurando-os para **Fechar** ou **Suprimir** clicando nos três pontos no canto do alerta e fazendo sua escolha.

-   **Abrir**: todas as novas atividades suspeitas aparecem nesta lista.

-   **Fechar**: é usado para rastrear atividades suspeitas que você identificou, pesquisou e corrigiu como mitigado.

    > [!NOTE]
    > O Azure ATP poderá reabrir uma atividade fechada se a mesma atividade for detectada novamente em um curto período.
    
-   **Suprimir**: suprimir uma atividade significa que você deseja ignorá-la por enquanto e apenas ser alertado novamente se houver uma nova instância. Se houver um alerta semelhante, o Azure ATP não o reabrirá. Mas, se o alerta parar por sete dias e, depois, for observado novamente, você será alertado novamente.

-   **Reabrir**: você pode reabrir um alerta fechado ou suprimido para que ele seja exibido novamente como **Aberto** na linha do tempo.

-   **Excluir**: na linha do tempo de alerta de segurança, você também tem a opção de excluir um problema de integridade. Se você excluir um alerta, ele será excluído da instância e você NÃO poderá restaurá-lo. Após clicar em Excluir, será possível excluir todos os alertas de segurança do mesmo tipo.



![Imagem dos problemas da central de integridade do Azure ATP](media/atp-health-issue.png)






## <a name="see-also"></a>Consulte Também

- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
