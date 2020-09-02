---
title: Investigando caminhos de movimento lateral com o Azure ATP
description: Este artigo descreve como detectar e investigar possíveis ataques de caminho de movimento lateral com a ATP (Proteção Avançada contra Ameaças) do Azure.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/15/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 9295dc09-ecdb-44c0-906b-cba4c5c8f17c
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4d27ca218eceb42f379680e9f2fae1b5e17e237f
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88956611"
---
# <a name="tutorial-use-lateral-movement-paths-lmps"></a>Tutorial: Usar LMPs (caminhos de movimento lateral)

> [!NOTE]
> Os recursos do ATP do Azure explicados nesta página também podem ser acessados usando o novo [portal](https://portal.cloudappsecurity.com).

Os ataques de movimento lateral normalmente são realizados usando uma série de técnicas diferentes. Alguns dos métodos mais populares usados pelos invasores são o [roubo de credencial](suspicious-activity-guide.md#) e os ataques de [Pass-the-Ticket](suspicious-activity-guide.md). Em ambos os métodos, as contas não confidenciais são usadas pelos invasores para realizar movimentos laterais explorando computadores não confidenciais que compartilham credenciais de logon armazenadas em contas, grupos e computadores com contas confidenciais.

Neste tutorial, você aprenderá a usar os LMPs da ATP do Azure para [investigar](#investigate) possíveis caminhos de movimento lateral e, junto com os alertas de segurança da ATP do Azure, compreender melhor o que aconteceu em sua rede e como. Além disso, você aprenderá a usar o [LMP para relatório de conta confidencial](#discover-your-at-risk-sensitive-accounts) para descobrir todas as contas confidenciais com possíveis caminhos de movimento lateral descobertos na sua rede por período de tempo.

> [!div class="checklist"]
>
> - Investigar LMPs
> - Descobrir suas contas confidenciais que estão em risco
> - Acessar o relatório de **Caminhos de movimento lateral para contas confidenciais**

## <a name="investigate"></a>Investigar

Há várias maneiras de usar e investigar LMPs. No portal da ATP do Azure, pesquise por entidade e, em seguida, explore por caminho ou atividade.

1. No portal, pesquise um usuário ou computador. Observe se uma notificação de movimento lateral foi adicionada a um perfil de entidade. As notificações serão exibidas apenas quando uma entidade for descoberta em um possível LMP nas últimas 48 horas.

    ![ícone lateral](media/lateral-movement-icon.png) ou ![ícone do caminho](media/paths-icon.png).

1. Na página de perfil do usuário que é aberta, clique na guia **Caminhos de movimento lateral**.

    ![Guia do LMP (caminho de movimento lateral) da ATP do Azure](media/lateral-movement-path-tab.png)

1. O gráfico exibido fornece um mapa dos possíveis caminhos até o usuário confidencial durante a período de tempo de 48 horas. Se não foi detectada nenhuma atividade nos últimos dois dias, o gráfico não será exibido. Use a opção **Exibir uma data diferente** para exibir o gráfico de detecções anteriores de caminho de movimento lateral da entidade.

    ![LMP – exibir uma data diferente](media/atp-view-different-date.png)

1. Examine o gráfico para ver o que você pode aprender sobre a exposição das credenciais de seus usuários confidenciais. Por exemplo, no caminho, siga as setas cinzas **Conectado por** para saber onde Nick se conectou com suas credenciais privilegiadas. Nesse caso, as credenciais confidenciais de Nick foram salvas no computador SHAREPOINT-SRV. Agora, observe quais outros usuários se conectaram em quais computadores e criaram mais exposição e vulnerabilidade. Você pode ver isso examinando as setas pretas **Administrador em** para ver quem tem privilégios de administrador no recurso. Neste exemplo, todos no grupo HelpDesk têm a capacidade de acessar as credenciais do usuário desse recurso.

    ![LMP (caminho de movimento lateral) da ATP do Azure](media/atp-lmp.png)

## <a name="discover-your-at-risk-sensitive-accounts"></a>Descobrir suas contas confidenciais que estão em risco

Para descobrir todas as contas confidenciais em sua rede que estão expostas por causa da conexão com contas, grupos e computadores não confidenciais em caminhos de movimento lateral, siga estas etapas.

1. No menu do portal do Azure ATP, clique no ícone de relatórios ![ícone de relatórios](media/atp-report-icon.png).

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

- [Investigando caminhos de movimento lateral com o ATP do Azure](use-case-lateral-movement-path.md)
- [Configurar o Azure ATP para realizar chamadas remotas para SAM](install-atp-step8-samr.md)
- [Trabalhando com alertas de segurança](working-with-suspicious-activities.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
