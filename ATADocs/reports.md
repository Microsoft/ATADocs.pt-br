---
title: Trabalhando com relatórios do ATA | Microsoft Docs
description: Descreve como você pode gerar relatórios no ATA para monitorar sua rede.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 3/27/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 38ea49b5-cd5e-43e5-bc39-5071f759633b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 279c8cc8f44e0c2803966709511d3089bce5d3a8
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65197086"
---
# <a name="ata-reports"></a>Relatórios do ATA


*Aplica-se a: Advanced Threat Analytics versão 1.9*

A seção de relatórios do ATA no console permite gerar relatórios que fornecem informações do status do sistema, a integridade do sistema e um relatório de atividades suspeitas detectadas em seu ambiente.

Para acessar a página relatórios, clique no ícone de relatório na barra de menus: ![ícone de relatório](./media/ata-report-icon.png).
Os relatórios disponíveis são: 

- **Relatório de resumo**: o relatório de resumo apresenta um painel do status no sistema. Você pode exibir três guias, uma para um **Resumo** do que foi detectado na rede, **Open suspicious activities (Atividades suspeitas em aberto)** que lista as atividades suspeitas das quais você deve cuidar e **Open health issues (Problemas de integridade em aberto)** que lista os problemas de integridade do sistema do ATA dos quais você deve cuidar. As atividades suspeitas listadas são divididas por tipo, assim como os problemas de integridade. 

- **Modificação de grupos confidenciais**: esse relatório lista todas as vezes que uma modificação é feita em grupos confidenciais (como no grupo de administradores).

- **Senhas expostas em texto não criptografado**: alguns serviços usam o protocolo não seguro do LDAP para enviar credenciais de conta em texto sem formatação. Isso pode ocorrer até mesmo para contas confidenciais. Os invasores que monitoram o tráfego de rede podem capturar e reutilizar essas credenciais para fins mal-intencionados. Esse relatório lista todos os computadores de origem e as senhas de contas do ATA detectadas como tendo sido enviadas em texto não criptografado. 

- **Caminhos de movimento lateral para contas confidenciais**: este relatório lista as contas confidenciais que estão expostas por meio de caminhos de movimentação lateral. Para obter mais informações, veja [Caminhos de movimento lateral](use-case-lateral-movement-path.md)

Há duas maneiras de gerar um relatório: sob demanda ou agendando um relatório para ser enviado para seu email periodicamente.

Para gerar um relatório sob demanda:

1. Na barra de menus do console do ATA, clique no ícone de relatório na barra de menus: ![ícone de relatório](./media/ata-report-icon.png).

2. Em seu tipo de relatório selecionado, defina as datas **De** e **Até** e clique em **Baixar**. 
 ![relatórios](./media/reports.png)

Para definir um relatório agendado:
 
1. Na página **Relatórios**, clique em **Set scheduled reports (Definir relatórios agendados)** ou, na página de configuração do Console do ATA, em Notifications e Reports (Notificações e Relatórios), clique em **Relatórios agendados**.

   ![Agendar relatórios](./media/ata-sched-reports.png)

   > [!NOTE]
   > Os relatórios diários foram criados para serem enviados logo após a meia-noite (UTC).

2. Clique em **Agendar** ao lado do tipo de relatório selecionado para definir a frequência e o endereço de email para a entrega dos relatórios, clique no sinal de adição ao lado dos endereços de email para adicioná-los e clique em **Salvar**.

   ![Frequência e email do relatório agendado](./media/sched-report1.png)


> [!NOTE]
> Os relatórios agendados são entregues por email e poderão ser enviados apenas se você já tiver configurado um servidor de email em **Configuração** e, em seguida, em **Notificações e Relatórios**, selecione **Servidor de email**.


## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Planejamento da capacidade do ATA](ata-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-collection.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
