---
title: Entender e usar os caminhos de movimentação lateral com o Microsoft Defender para Identidade
description: Este artigo descreve os possíveis LMPs (caminhos de movimentação lateral) do Microsoft Defender para Identidade
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 3676eb1b7a4528fcbd6d45b4052c5a49f03c4718
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93277693"
---
# <a name="product-long-lateral-movement-paths-lmps"></a>Caminhos de movimentação lateral (LMPs) do [!INCLUDE [Product long](includes/product-long.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

> [!NOTE]
> Os recursos do [!INCLUDE [Product long](includes/product-long.md)] explicados nesta página também podem ser acessados usando o novo [portal](https://portal.cloudappsecurity.com).

O movimento lateral ocorre quando um invasor usa contas não confidenciais para obter acesso a contas confidenciais em toda a rede. O movimento lateral é usado pelos invasores para identificar e obter acesso a contas e computadores confidenciais na rede que compartilham credenciais de logon armazenadas em contas, grupos e computadores. Depois que um invasor faz movimentos laterais bem-sucedidos em busca dos destinos principais, ele também pode aproveitar a oportunidade para obter acesso aos controladores de domínio. Os ataques de movimento lateral são realizados usando muitos dos métodos descritos no [Guia de atividades suspeitas](suspicious-activity-guide.md).

Um componente fundamental para obter insights de segurança do [!INCLUDE [Product long](includes/product-long.md)] são os caminhos de movimentação lateral ou LMPs. Os LMPs do [!INCLUDE [Product short](includes/product-short.md)] são guias visuais que ajudam a compreender e identificar de forma rápida e exata como os invasores podem fazer movimentos laterais dentro de sua rede. A finalidade dos movimentos laterais dentro da cadeia de extermínio do ataque cibernético é que os invasores obtenham e comprometam as contas confidenciais usando contas não confidenciais. O comprometimento das contas confidenciais aproxima-os mais do objetivo final, que é comprometer o domínio. Para impedir o sucesso desses ataques, os LMPs do [!INCLUDE [Product short](includes/product-short.md)] oferecem orientações visuais diretas e fáceis de interpretar em suas contas confidenciais e mais vulneráveis. Os LMPs ajudam a atenuar e impedir esses riscos no futuro e encerram o ataque do invasor antes que ele comprometa a predominância do domínio.

![LMP (caminho de movimentação lateral) do [!INCLUDE [Product short](includes/product-short.md)]](media/lmp.png)

Os ataques de movimento lateral normalmente são realizados usando uma série de técnicas diferentes. Alguns dos métodos mais populares usados pelos invasores são o roubo de credencial e o Pass-the-Ticket. Em ambos os métodos, contas não confidenciais são usadas pelos invasores para realizar movimentos laterais explorando computadores não confidenciais que compartilham credenciais de logon armazenadas em contas, grupos e computadores com contas confidenciais.

## <a name="where-can-i-find-product-short-lmps"></a>Onde posso encontrar LMPs do [!INCLUDE [Product short](includes/product-short.md)]?

Cada perfil de computador ou de usuário descoberto pelo [!INCLUDE [Product short](includes/product-short.md)] em um LMP apresenta uma guia **Caminhos de movimentação lateral**. Os computadores e perfis que não apresentam nenhuma guia nunca foram descobertos em um possível LMP.

![Guia LMP (Caminho de Movimentação Lateral) do [!INCLUDE [Product short](includes/product-short.md)]](media/lateral-movement-path-tab.png)

O LMP de cada entidade fornece informações diferentes dependendo da confidencialidade da entidade:

- Usuários confidenciais – são mostrados os possíveis LMPs que levam a esse usuário.
- Usuários e computadores não confidenciais – são mostrados os possíveis LMPs aos quais a entidade está relacionada.

Cada vez que a guia recebe um clique, o [!INCLUDE [Product short](includes/product-short.md)] exibe o último LMP descoberto. Cada possível LMP é salvo por 48 horas após a descoberta. O histórico do LMP está disponível. Veja os LMPs mais antigos que foram descobertos anteriormente clicando em **Exibir uma data diferente**.

![Exibição LMP (Caminho de Movimentação Lateral) do [!INCLUDE [Product short](includes/product-short.md)]](media/lmp-complete.png)

Descubra quando os possíveis LMPs foram identificados e quais entidades relacionadas possivelmente estão envolvidas.

## <a name="lmp-discovery"></a>Descoberta de LMP

Na guia Atividades, uma indicação é fornecida quando um novo possível LMP é identificado:

- Usuários confidenciais – quando um novo caminho é identificado a um usuário confidencial

![LMP (Caminho de Movimentação Lateral) do [!INCLUDE [Product short](includes/product-short.md)] confidencial identificado](media/lmp-activities.png)

- Usuários e computadores não confidenciais – quando essa entidade é identificada em um possível LMP que leva a um usuário confidencial.

![LMP (Caminho de Movimentação Lateral) do [!INCLUDE [Product short](includes/product-short.md)] não confidencial identificado](media/lateral-non-sensitive.png)

## <a name="lmp-related-entities"></a>Entidades relacionadas ao LMP

O LMP agora pode ajudar diretamente no processo de investigação. As listas de evidências de alerta de segurança do [!INCLUDE [Product short](includes/product-short.md)] fornecem as entidades relacionadas que estão envolvidas em cada possível caminho de movimentação lateral. As listas de evidências ajudam diretamente a equipe de resposta de segurança a aumentar ou reduzir a importância do alerta de segurança e/ou a investigação das entidades relacionadas. Por exemplo, quando uma alerta de Pass-the-Ticket é emitido, o computador de origem, o usuário comprometido e o computador de destino do qual o tíquete roubado foi usado fazem parte do possível caminho de movimento lateral que leva a um usuário confidencial. A existência do LMP detectado aumenta ainda mais a importância da investigação do alerta e da observação do usuário suspeito para evitar que o adversário faça outros movimentos laterais. A evidência rastreável é fornecida nos LMPs para você impedir com rapidez e facilidade que os invasores avancem na rede.

## <a name="lateral-movement-paths-to-sensitive-accounts-report"></a>Relatório de caminhos de movimento lateral para contas confidenciais

Os dados do LMP também estão disponíveis no [Relatório de caminhos de movimento lateral para contas confidenciais](investigate-lateral-movement-path.md). Este relatório lista as contas confidenciais expostas por caminhos de movimento lateral e inclui os caminhos que foram selecionados manualmente em um período de tempo específico ou incluídos no período de tempo dos relatórios agendados.  Personalize o intervalo de datas incluído usando a seleção de calendário.

## <a name="preventative-best-practices"></a>Melhores práticas recomendadas

Os insights de segurança são sempre oportunos para impedir um próximo ataque e corrigir os danos. Por esse motivo, a investigação de um ataque, mesmo durante a fase de comprometimento de domínio, oferece um exemplo diferente, mas importante. Normalmente, durante a investigação de um alerta de segurança, como a execução remota de código, se o alerta é um verdadeiro positivo, o controlador de domínio pode já estar comprometido. Mas os LMPs informam onde o invasor obteve privilégios e qual caminho ele usou em sua rede. Usados dessa forma, os LMPs também podem oferecer insights importantes sobre como corrigir.

- A melhor maneira de evitar a exposição ao movimento lateral em sua organização é garantir que os usuários confidenciais usem apenas suas credenciais de administrador para fazer logon em computadores protegidos. No exemplo, verifique se o administrador no caminho realmente precisa acessar o computador compartilhado. Se ele precisar de acesso, terá que fazer logon no computador compartilhado com um nome de usuário e uma senha diferente das credenciais de administrador.

- Verifique se os usuários não têm permissões administrativas desnecessárias. No exemplo, verifique se todos no grupo compartilhado realmente requerem direitos de administrador no computador exposto.

- Verifique se as pessoas têm acesso apenas aos recursos necessários. No exemplo, Ron Harper amplia significativamente a exposição de Nick Cowley. É necessário que Ron Harper seja incluído no grupo? Há subgrupos que podem ser criados para minimizar a exposição ao movimento lateral?

**Dica** – quando não for detectada nenhuma possível atividade de caminho de movimento lateral para uma entidade nas últimas 48 horas, escolha **Exibir uma data diferente** e verifique se há possíveis caminhos de movimento lateral anteriores. O **Relatório de LMP para usuários confidenciais** está sempre disponível, se os LMPs tiverem sido descobertos, e fornece informações sobre possíveis caminhos de movimento lateral detectados para usuários confidenciais.

**Dica** – para obter instruções sobre como configurar seus servidores e clientes a fim de permitir que o [!INCLUDE [Product short](includes/product-short.md)] execute as operações de SAM-R necessárias para detectar caminhos de movimentação lateral, confira [Configurar SAM-R](install-step8-samr.md).

## <a name="investigating-lmps"></a>Investigando LMPs

Para obter instruções de como identificar e investigar o uso de caminhos de movimentação lateral do [!INCLUDE [Product short](includes/product-short.md)], confira [Investigar caminhos de movimentação lateral](investigate-lateral-movement-path.md).

## <a name="see-also"></a>Consulte Também

- [Investigar LMPs do [!INCLUDE [Product short](includes/product-short.md)]](investigate-lateral-movement-path.md)
- [Configurar o [!INCLUDE [Product short](includes/product-short.md)] para realizar chamadas remotas para SAM](install-step8-samr.md)
- [Trabalhando com alertas de segurança](working-with-suspicious-activities.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
