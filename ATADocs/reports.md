---
title: "Trabalhando com relatórios do ATA | Microsoft Docs"
description: "Descreve como você pode gerar relatórios no ATA para monitorar sua rede."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/12/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 38ea49b5-cd5e-43e5-bc39-5071f759633b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4f29dfcc8b18ff755f6c0dcdaa08eaa807b08072
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*


# <a name="ata-reports"></a>Relatórios do ATA

A seção de relatórios do ATA no console permite gerar relatórios que fornecem informações do status do sistema, a integridade do sistema e um relatório de atividades suspeitas detectadas em seu ambiente.

Para acessar a página relatórios, clique no ícone de relatório na barra de menus: ![ícone de relatório](./media/ata-report-icon.png).
Os relatórios disponíveis são: 
- Relatório de resumo: o relatório de resumo apresenta um painel do status no sistema. Você pode exibir três guias, uma para um **Resumo** do que foi detectado na rede, **Open suspicious activities (Atividades suspeitas em aberto)** que lista as atividades suspeitas das quais você deve cuidar e **Open health issues (Problemas de integridade em aberto)** que lista os problemas de integridade do sistema do ATA dos quais você deve cuidar. As atividades suspeitas listadas são divididas por tipo, assim como os problemas de integridade. 
- Modification to sensitive groups (Modificação para grupos confidenciais): este relatório lista toda vez que uma modificação é feita para grupos confidenciais (como administradores).

Há duas maneiras de gerar um relatório: sob demanda ou agendando um relatório para ser enviado para seu email periodicamente.

Para gerar um relatório sob demanda:

1. Na barra de menus do console do ATA, clique no ícone de relatório na barra de menus: ![ícone de relatório](./media/ata-report-icon.png).
2. Em **Resumo** ou **Modifications to sensitive groups (Modificações para grupos confidenciais)**, defina as datas **De** e **Até** e clique em **Baixar**. 
![relatórios](./media/reports.png)

Para definir um relatório agendado:
 
1. Na página **Relatórios**, clique em **Set scheduled reports (Definir relatórios agendados)** ou, na página de configuração do Console do ATA, em Notifications e Reports (Notificações e Relatórios), clique em **Relatórios agendados**.

   ![Agendar relatórios](./media/ata-sched-reports.png)

2. Clique em **Agendar** ao lado de **Resumo** ou **Modification to sensitive groups (Modificação para grupos confidenciais)** para definir a frequência e o endereço de email para a entrega dos relatórios, clique no sinal de adição ao lado dos endereços de email e adicione-os e clique em **Salvar**.

   ![Frequência e email do relatório agendado](./media/sched-report1.png)


> [!NOTE]
> Os relatórios agendados são entregues por email e podem ser enviados apenas se você já tiver configurado um servidor de email em **Configuração** e, em seguida, em Notifications e Reports (Notificações e Relatórios), selecione **Servidor de email**.


## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Planejamento da capacidade do ATA](ata-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
