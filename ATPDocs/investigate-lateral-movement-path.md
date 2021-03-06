---
title: Como investigar caminhos de movimentação lateral com o Microsoft Defender para Identidade
description: Este artigo descreve como detectar e investigar possíveis ataques de caminho de movimentação lateral com o Microsoft Defender para Identidade.
ms.date: 10/26/2020
ms.topic: tutorial
ms.openlocfilehash: 45b4f0e7af69c0404b00e5f317f986bad84e644a
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96542984"
---
# <a name="tutorial-use-lateral-movement-paths-lmps"></a>Tutorial: Usar LMPs (caminhos de movimento lateral)

> [!NOTE]
> Os recursos do [!INCLUDE [Product long](includes/product-long.md)] explicados nesta página também podem ser acessados usando o novo [portal](https://portal.cloudappsecurity.com).

Os ataques de movimento lateral normalmente são realizados usando uma série de técnicas diferentes. Alguns dos métodos mais populares usados pelos invasores são o [roubo de credencial](suspicious-activity-guide.md#) e os ataques de [Pass-the-Ticket](suspicious-activity-guide.md). Em ambos os métodos, as contas não confidenciais são usadas pelos invasores para realizar movimentos laterais explorando computadores não confidenciais que compartilham credenciais de logon armazenadas em contas, grupos e computadores com contas confidenciais.

Neste tutorial, você aprenderá a usar os LMPs do [!INCLUDE [Product long](includes/product-long.md)] para [investigar](#investigate) possíveis caminhos de movimentação lateral e, junto com os alertas de segurança do [!INCLUDE [Product short](includes/product-short.md)], compreender melhor o que ocorreu na sua rede e como isso aconteceu. Além disso, você aprenderá a usar o [LMP para relatório de conta confidencial](#discover-your-at-risk-sensitive-accounts) para descobrir todas as contas confidenciais com possíveis caminhos de movimento lateral descobertos na sua rede por período de tempo.

> [!div class="checklist"]
>
> - Investigar LMPs
> - Descobrir suas contas confidenciais que estão em risco
> - Acessar o relatório de **Caminhos de movimento lateral para contas confidenciais**

## <a name="investigate"></a>Investigar

Há várias maneiras de usar e investigar LMPs. No portal do [!INCLUDE [Product short](includes/product-short.md)], faça a pesquisa por entidade e explore-a por caminho ou atividade.

1. No portal, pesquise um usuário ou computador. Observe se uma notificação de movimento lateral foi adicionada a um perfil de entidade. As notificações serão exibidas apenas quando uma entidade for descoberta em um possível LMP nas últimas 48 horas.

    ![ícone lateral](media/lateral-movement-icon.png) ou ![ícone do caminho](media/paths-icon.png).

1. Na página de perfil do usuário que é aberta, clique na guia **Caminhos de movimento lateral**.

    ![Guia LMP (Caminho de Movimentação Lateral) do [!INCLUDE [Product short](includes/product-short.md)]](media/lateral-movement-path-tab.png)

1. O gráfico exibido fornece um mapa dos possíveis caminhos até o usuário confidencial durante a período de tempo de 48 horas. Se não foi detectada nenhuma atividade nos últimos dois dias, o gráfico não será exibido. Use a opção **Exibir uma data diferente** para exibir o gráfico de detecções anteriores de caminho de movimento lateral da entidade.

    ![LMP – exibir uma data diferente](media/view-different-date.png)

1. Examine o gráfico para ver o que você pode aprender sobre a exposição das credenciais de seus usuários confidenciais. Por exemplo, no caminho, siga as setas cinzas **Conectado por** para saber onde Nick se conectou com suas credenciais privilegiadas. Nesse caso, as credenciais confidenciais de Nick foram salvas no computador SHAREPOINT-SRV. Agora, observe quais outros usuários se conectaram em quais computadores e criaram mais exposição e vulnerabilidade. Você pode ver isso examinando as setas pretas **Administrador em** para ver quem tem privilégios de administrador no recurso. Neste exemplo, todos no grupo HelpDesk têm a capacidade de acessar as credenciais do usuário desse recurso.

    ![LMP (caminho de movimentação lateral) do [!INCLUDE [Product short](includes/product-short.md)]](media/lmp.png)

## <a name="discover-your-at-risk-sensitive-accounts"></a>Descobrir suas contas confidenciais que estão em risco

Para descobrir todas as contas confidenciais em sua rede que estão expostas por causa da conexão com contas, grupos e computadores não confidenciais em caminhos de movimento lateral, siga estas etapas.

1. No menu do portal do [!INCLUDE [Product short](includes/product-short.md)], clique no ícone de relatórios ![ícone de relatórios](media/report-icon.png).

1. Em **Caminhos de movimento lateral para contas confidenciais**, se não forem encontrados caminhos potenciais de movimento lateral, o relatório ficará indisponível. Se houver o potencial para caminhos de movimento lateral, o relatório pré-selecionará automaticamente a primeira data em que há dados relevantes. O relatório de caminho de movimento lateral fornece dados de até 60 dias.

    ![Captura de tela mostrando a seleção de data do relatório](media/reports.png)

1. Clique em **Baixar**.

1. É criado um arquivo do Excel que fornece detalhes sobre os possíveis caminhos de movimento lateral e exposição de conta confidencial para as datas selecionadas. A guia **Resumo** fornece gráficos que detalham o número de contas confidenciais, computadores e as médias do acesso em risco. A guia **Detalhes** fornece uma lista das contas confidenciais que você deve investigar mais.

## <a name="schedule-report"></a>Agendar relatório

O relatório Movimento lateral para conta confidencial também pode ser agendado usando o recurso de definição de relatórios agendados.

Observe que os LMPs reais detalhados no relatório baixável podem não estar mais disponíveis porque foram detectados anteriormente e podem ter sido alterados, modificados ou corrigidos desde a detecção.

Para examinar os LMPs históricos, selecione datas disponíveis diferentes na seleção de calendário ao criar um relatório.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu a usar LMPs para investigar atividades suspeitas. Para saber mais sobre as entidades envolvidas na LMPs, continue para o tutorial Investigar entidades.

> [!div class="nextstepaction"]
> [Investigar entidades](investigate-entity.md)

## <a name="see-also"></a>Consulte Também

- [Noções básicas sobre os caminhos de movimentação lateral do [!INCLUDE [Product short](includes/product-short.md)]](use-case-lateral-movement-path.md)
- [Configurar o [!INCLUDE [Product short](includes/product-short.md)] para realizar chamadas remotas para SAM](install-step8-samr.md)
- [Trabalhando com alertas de segurança](working-with-suspicious-activities.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
