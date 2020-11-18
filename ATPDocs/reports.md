---
title: Trabalhar com relatórios do Microsoft Defender para Identidade
description: Descreve como você pode gerar relatórios no Microsoft Defender para Identidade para monitorar sua rede.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2c2d6b1a-fc8c-4ff7-b07d-64ce6159f84d
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 68c129e0c92c369bb666483dc17013c54a84e282
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94849036"
---
# <a name="product-long-reports"></a>Relatórios do [!INCLUDE [Product long](includes/product-long.md)]

A seção de relatórios do [!INCLUDE [Product long](includes/product-long.md)] no portal do [!INCLUDE [Product short](includes/product-short.md)] permite que você agende ou gere e baixe imediatamente relatórios que fornecem informações de status do sistema e da entidade. Com o recurso de relatórios, você pode criar relatórios sobre a integridade do sistema, alertas de segurança e possíveis caminhos de movimento lateral detectados em seu ambiente.

Para acessar a página relatórios, clique no ícone de relatório na barra de menus: ![ícone de relatório](media/report-icon.png).
Os relatórios disponíveis são:

- **Relatório de resumo**: o relatório de resumo apresenta um painel do status no sistema. Você pode exibir três guias – uma para um **Resumo** do que foi detectado na rede, outra para **Atividades suspeitas em aberto**, listando as atividades suspeitas sobre as quais você deve tomar uma medida, e outra para **Problemas de integridade em aberto**, listando os problemas de integridade do sistema do [!INCLUDE [Product short](includes/product-short.md)] suspeitas sobre as quais deve adotar uma ação. As atividades suspeitas listadas são divididas por tipo, assim como os problemas de integridade.

- **Modificação de grupos confidenciais**: este relatório lista toda vez que uma modificação é feita em grupos confidenciais (como administradores ou contas ou grupos marcadas manualmente). Se você está usando sensores autônomos do [!INCLUDE [Product short](includes/product-short.md)], para receber um relatório completo sobre seus grupos confidenciais, verifique se os [eventos são encaminhados de seus controladores de domínio para os sensores autônomos](configure-event-forwarding.md).

- **Senhas expostas em texto não criptografado**: alguns serviços usam o protocolo não seguro do LDAP para enviar credenciais de conta em texto sem formatação. Isso pode ocorrer até mesmo para contas confidenciais. Os invasores que monitoram o tráfego de rede podem capturar e reutilizar essas credenciais para fins mal-intencionados. Esse relatório lista todos os computadores de origem e as senhas de conta detectados pelo [!INCLUDE [Product short](includes/product-short.md)] como enviados em texto não criptografado.

- **Caminhos de movimento lateral para contas confidenciais**: este relatório lista as contas confidenciais que estão expostas por meio de caminhos de movimentação lateral. Para obter mais informações, consulte [Caminhos de movimento lateral](use-case-lateral-movement-path.md). Este relatório coleta os possíveis caminhos de movimento lateral que foram detectados no período de relatório selecionado.

Há duas maneiras de gerar um relatório: sob demanda ou agendando um relatório para ser enviado para seu email periodicamente.

Para gerar um relatório sob demanda:

1. Na barra de menus do portal do [!INCLUDE [Product short](includes/product-short.md)], clique no ícone de relatório na barra de menus: ![ícone de relatório](media/report-icon.png).

1. Em seu tipo de relatório selecionado, defina as datas **De** e **Para** e clique em **Baixar**.
 ![Captura de tela mostrando o download do relatório](media/reports.png)

Para definir um relatório agendado:

1. Na página **Relatórios**, clique em **Definir relatórios agendados** ou, na página de configuração do portal do [!INCLUDE [Product short](includes/product-short.md)], em Notificações e Relatórios, clique em **Relatórios agendados**.

    ![Agendar relatórios](media/sched-reports.png)

    > [!NOTE]
    > Por padrão, os relatórios diários foram criados para serem enviados logo após a meia-noite (UTC). Escolha seu próprio horário usando a opção de seleção de horário.

1. Clique em **Agendar** ao lado do tipo de relatório selecionado para definir a frequência e o endereço de email para entrega dos relatórios. A frequência do relatório que você selecionar determinará as informações incluídas nele. Para adicionar emails, clique no sinal de adição ao lado do campo de endereço de email, insira o endereço e clique em **Salvar**.

    ![Frequência e email do relatório agendado](media/sched-report1.png)

## <a name="see-also"></a>Consulte Também

- [Pré-requisitos do [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Planejamento de capacidade do [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
