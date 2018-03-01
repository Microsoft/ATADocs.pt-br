---
title: "Trabalhando com relatórios do Azure ATP | Microsoft Docs"
description: "Descreve como você pode gerar relatórios no Azure ATP para monitorar sua rede."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 2c2d6b1a-fc8c-4ff7-b07d-64ce6159f84d
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2ebc0d9bb860bd93f14c4c511b034c740b59dffb
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2018
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*


# <a name="azure-atp-reports"></a>Relatórios do Azure ATP

A seção de relatórios do Azure ATP no portal de espaço de trabalho permite gerar relatórios que fornecem informações do status do sistema, a integridade do sistema e um relatório de atividades suspeitas detectadas em seu ambiente.

Para acessar a página relatórios, clique no ícone de relatório na barra de menus: ![ícone de relatório](./media/atp-report-icon.png).
Os relatórios disponíveis são: 

- **Relatório de resumo**: o relatório de resumo apresenta um painel do status no sistema. Você pode exibir três guias – uma para um **Resumo** do que foi detectado na rede, **Atividades suspeitas em aberto** que lista as atividades suspeitas das quais você deve cuidar e **Problemas de integridade em aberto** que lista os problemas de integridade do sistema do Azure ATP dos quais você deve cuidar. As atividades suspeitas listadas são divididas por tipo, assim como os problemas de integridade. 

- **Modificação de grupos confidenciais**: este relatório lista toda vez que uma modificação é feita em grupos confidenciais (como administradores ou contas ou grupos marcadas manualmente). Se você estiver usando sensores autônomos do Azure ATP, para receber um relatório completo sobre seus grupos confidenciais, é necessário garantir que os [eventos sejam encaminhados de seus controladores de domínio para os sensores autônomos](configure-event-forwarding.md). 

- **Senhas expostas em texto não criptografado**: alguns serviços usam o protocolo não seguro do LDAP para enviar credenciais de conta em texto sem formatação. Isso pode ocorrer até mesmo para contas confidenciais. Os invasores que monitoram o tráfego de rede podem capturar e reutilizar essas credenciais para fins mal-intencionados. Este relatório lista todos os computadores de origem e as senhas de conta do Azure ATP detectadas como tendo sido enviadas em texto não criptografado. 

- **Caminhos de movimento lateral para contas confidenciais**: este relatório lista as contas confidenciais que estão expostas por meio de caminhos de movimentação lateral. Para obter mais informações, consulte [Caminhos de movimento lateral](use-case-lateral-movement-path.md). Este relatório coleta caminhos que foram criados nos últimos 60 dias, em vez das informações exibidas no portal de espaço de trabalho, que representam somente dois dias.

Há duas maneiras de gerar um relatório: sob demanda ou agendando um relatório para ser enviado para seu email periodicamente.

Para gerar um relatório sob demanda:

1. Na barra de menus do portal de espaço de trabalho do Azure ATP, clique no ícone de relatório na barra de menus: ![ícone de relatório](./media/atp-report-icon.png).

2. Em seu tipo de relatório selecionado, defina as datas **De** e **Até** e clique em **Baixar**. 
 ![relatórios](./media/reports.png)

Para definir um relatório agendado:
 
1. Na página **Relatórios**, clique em **Definir relatórios agendados** ou, na página de configuração do portal de espaço de trabalho do Azure ATP, em Notificações e Relatórios, clique em **Relatórios agendados**.

   ![Agendar relatórios](./media/atp-sched-reports.png)

2. Clique em **Agendar** ao lado do tipo de relatório selecionado para definir a frequência e o endereço de email para a entrega dos relatórios, clique no sinal de adição ao lado dos endereços de email para adicioná-los e clique em **Salvar**.

   ![Frequência e email do relatório agendado](./media/sched-report1.png)


## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)