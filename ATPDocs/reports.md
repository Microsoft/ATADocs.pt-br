---
title: Trabalhando com relatórios do Azure ATP | Microsoft Docs
description: Descreve como você pode gerar relatórios no Azure ATP para monitorar sua rede.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/26/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2c2d6b1a-fc8c-4ff7-b07d-64ce6159f84d
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d51447eafcd6e267fef65798ff25e2f75fb71ec2
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196490"
---
# <a name="azure-atp-reports"></a>Relatórios do Azure ATP

A seção de relatórios da ATP do Azure no portal da ATP do Azure permite que você agende ou imediatamente gere e baixe relatórios que fornecem informações de status do sistema e da entidade. Com o recurso de relatórios, você pode criar relatórios sobre a integridade do sistema, alertas de segurança e possíveis caminhos de movimento lateral detectados em seu ambiente.


Para acessar a página relatórios, clique no ícone de relatório na barra de menus: ![ícone de relatório](./media/atp-report-icon.png).
Os relatórios disponíveis são: 

- **Relatório de resumo**: o relatório de resumo apresenta um painel do status no sistema. Você pode exibir três guias – uma para um **Resumo** do que foi detectado na rede, **Atividades suspeitas em aberto** que lista as atividades suspeitas das quais você deve cuidar e **Problemas de integridade em aberto** que lista os problemas de integridade do sistema do Azure ATP dos quais você deve cuidar. As atividades suspeitas listadas são divididas por tipo, assim como os problemas de integridade. 

- **Modificação de grupos confidenciais**: este relatório lista toda vez que uma modificação é feita em grupos confidenciais (como administradores ou contas ou grupos marcadas manualmente). Se você estiver usando sensores autônomos da ATP do Azure, para receber um relatório completo sobre seus grupos confidenciais, verifique se os [eventos são encaminhados de seus controladores de domínio para os sensores autônomos](configure-event-forwarding.md). 

- **Senhas expostas em texto não criptografado**: alguns serviços usam o protocolo não seguro do LDAP para enviar credenciais de conta em texto sem formatação. Isso pode ocorrer até mesmo para contas confidenciais. Os invasores que monitoram o tráfego de rede podem capturar e reutilizar essas credenciais para fins mal-intencionados. Este relatório lista todos os computadores de origem e as senhas de conta detectados pela ATP do Azure como enviados em texto não criptografado. 

- **Caminhos de movimento lateral para contas confidenciais**: este relatório lista as contas confidenciais que estão expostas por meio de caminhos de movimentação lateral. Para obter mais informações, consulte [Caminhos de movimento lateral](use-case-lateral-movement-path.md). Este relatório coleta os possíveis caminhos de movimento lateral que foram detectados no período de relatório selecionado. 

Há duas maneiras de gerar um relatório: sob demanda ou agendando um relatório para ser enviado para seu email periodicamente.

Para gerar um relatório sob demanda:

1. Na barra de menus do Azure ATP, clique no ícone de relatório na barra de menus: ![ícone de relatório](./media/atp-report-icon.png).

2. Em seu tipo de relatório selecionado, defina as datas **De** e **Para** e clique em **Baixar**. 
 ![relatórios](./media/reports.png)

Para definir um relatório agendado:
 
1. Na página **Relatórios**, clique em **Definir relatórios agendados** ou, na página de configuração do portal da ATP do Azure, em Notificações e Relatórios, clique em **Relatórios agendados**.

   ![Agendar relatórios](./media/atp-sched-reports.png)
 
   > [!NOTE]
   > Por padrão, os relatórios diários foram criados para serem enviados logo após a meia-noite (UTC). Escolha seu próprio horário usando a opção de seleção de horário. 

2. Clique em **Agendar** ao lado do tipo de relatório selecionado para definir a frequência e o endereço de email para entrega dos relatórios. A frequência do relatório que você selecionar determinará as informações incluídas nele. Para adicionar emails, clique no sinal de adição ao lado do campo de endereço de email, insira o endereço e clique em **Salvar**.

   ![Frequência e email do relatório agendado](./media/sched-report1.png)


## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
