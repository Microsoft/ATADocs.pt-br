---
title: Entender e usar os Caminhos de Movimentação Lateral com o ATP do Azure
description: Este artigo descreve os possíveis LMPs (caminhos de movimento lateral) da ATP (Proteção Avançada contra Ameaças) do Azure.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/15/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: de15c920-8904-4124-8bdc-03abd9f667cf
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: edb37833ac44e3f04f9daf7ee57a8e1f41ca5d38
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88955609"
---
# <a name="azure-atp-lateral-movement-paths-lmps"></a>LMPs (caminhos de movimento lateral) da ATP do Azure 

> [!NOTE]
> Os recursos do ATP do Azure explicados nesta página também podem ser acessados usando o novo [portal](https://portal.cloudappsecurity.com).

O movimento lateral ocorre quando um invasor usa contas não confidenciais para obter acesso a contas confidenciais em toda a rede. O movimento lateral é usado pelos invasores para identificar e obter acesso a contas e computadores confidenciais na rede que compartilham credenciais de logon armazenadas em contas, grupos e computadores. Depois que um invasor faz movimentos laterais bem-sucedidos em busca dos destinos principais, ele também pode aproveitar a oportunidade para obter acesso aos controladores de domínio. Os ataques de movimento lateral são realizados usando muitos dos métodos descritos no [Guia de atividades suspeitas](suspicious-activity-guide.md).

Um componente fundamental para obter insights de segurança da ATP do Azure são os caminhos de movimento lateral ou LMPs. Os LMPs da ATP do Azure são guias visuais que ajudam a compreender e identificar rapidamente exatamente como os invasores podem fazer movimentos laterais dentro de sua rede. A finalidade dos movimentos laterais dentro da cadeia de extermínio do ataque cibernético é que os invasores obtenham e comprometam as contas confidenciais usando contas não confidenciais. O comprometimento das contas confidenciais aproxima-os mais do objetivo final, que é comprometer o domínio. Para impedir o sucesso desses ataques, os LMPs da ATP do Azure oferecem orientações visuais diretas e fáceis de interpretar em suas contas confidenciais e mais vulneráveis. Os LMPs ajudam a atenuar e impedir esses riscos futuros e encerram o ataque do invasor antes que ele comprometa o domínio.

![LMP (caminho de movimento lateral) da ATP do Azure](media/atp-lmp.png)

Os ataques de movimento lateral normalmente são realizados usando uma série de técnicas diferentes. Alguns dos métodos mais populares usados pelos invasores são o roubo de credencial e o Pass-the-Ticket. Em ambos os métodos, contas não confidenciais são usadas pelos invasores para realizar movimentos laterais explorando computadores não confidenciais que compartilham credenciais de logon armazenadas em contas, grupos e computadores com contas confidenciais.

## <a name="where-can-i-find-azure-atp-lmps"></a>Onde posso encontrar os LMPs da ATP do Azure?

Cada perfil de computador ou de usuário descoberto pela ATP do Azure em um LMP apresenta uma guia **Caminhos de movimento lateral**. Os computadores e perfis que não apresentam nenhuma guia nunca foram descobertos em um possível LMP. 

![Guia do LMP (caminho de movimento lateral) da ATP do Azure](media/lateral-movement-path-tab.png)

O LMP de cada entidade fornece informações diferentes dependendo da confidencialidade da entidade: 
- Usuários confidenciais – são mostrados os possíveis LMPs que levam a esse usuário.
- Usuários e computadores não confidenciais – são mostrados os possíveis LMPs aos quais a entidade está relacionada. <br>

Cada vez que a guia é clicada, a ATP do Azure exibe o último LMP descoberto. Cada possível LMP é salvo por 48 horas após a descoberta. O histórico do LMP está disponível. Veja os LMPs mais antigos que foram descobertos anteriormente clicando em **Exibir uma data diferente**. 

![Exibição do LMP (caminho de movimento lateral) da ATP do Azure](media/atp-lmp-complete.png)

Descubra quando os possíveis LMPs foram identificados e quais entidades relacionadas possivelmente estão envolvidas. 

## <a name="lmp-discovery"></a>Descoberta de LMP

Na guia Atividades, uma indicação é fornecida quando um novo possível LMP é identificado:
- Usuários confidenciais – quando um novo caminho é identificado a um usuário confidencial

![LMP (caminho de movimento lateral) confidencial da ATP do Azure identificado](media/atp-lmp-activities.png)

- Usuários e computadores não confidenciais – quando essa entidade é identificada em um possível LMP que leva a um usuário confidencial.

![LMP (caminho de movimento lateral) não confidencial da ATP do Azure identificado](media/atp-lateral-non-sensitive.png)

## <a name="lmp-related-entities"></a>Entidades relacionadas ao LMP
O LMP agora pode ajudar diretamente no processo de investigação. As listas de evidências de alerta de segurança da ATP do Azure fornecem as entidades relacionadas que estão envolvidas em cada possível caminho de movimento lateral. As listas de evidências ajudam diretamente a equipe de resposta de segurança a aumentar ou reduzir a importância do alerta de segurança e/ou a investigação das entidades relacionadas. Por exemplo, quando uma alerta de Pass-the-Ticket é emitido, o computador de origem, o usuário comprometido e o computador de destino do qual o tíquete roubado foi usado fazem parte do possível caminho de movimento lateral que leva a um usuário confidencial. A existência do LMP detectado aumenta ainda mais a importância da investigação do alerta e da observação do usuário suspeito para evitar que o adversário faça outros movimentos laterais. A evidência rastreável é fornecida nos LMPs para você impedir com rapidez e facilidade que os invasores avancem na rede. 

## <a name="lateral-movement-paths-to-sensitive-accounts-report"></a>Relatório de caminhos de movimento lateral para contas confidenciais 
Os dados do LMP também estão disponíveis no [Relatório de caminhos de movimento lateral para contas confidenciais](investigate-lateral-movement-path.md). Este relatório lista as contas confidenciais expostas por caminhos de movimento lateral e inclui os caminhos que foram selecionados manualmente em um período de tempo específico ou incluídos no período de tempo dos relatórios agendados.  Personalize o intervalo de datas incluído usando a seleção de calendário. 

## <a name="preventative-best-practices"></a>Melhores práticas recomendadas
Os insights de segurança são sempre oportunos para impedir um próximo ataque e corrigir os danos. Por esse motivo, a investigação de um ataque, mesmo durante a fase de comprometimento de domínio, oferece um exemplo diferente, mas importante. Normalmente, durante a investigação de um alerta de segurança, como a execução remota de código, se o alerta é um verdadeiro positivo, o controlador de domínio pode já estar comprometido. Mas os LMPs informam onde o invasor obteve privilégios e qual caminho ele usou em sua rede. Usados dessa forma, os LMPs também podem oferecer insights importantes sobre como corrigir.  

- A melhor maneira de evitar a exposição ao movimento lateral em sua organização é garantir que os usuários confidenciais usem apenas suas credenciais de administrador para fazer logon em computadores protegidos. No exemplo, verifique se o administrador no caminho realmente precisa acessar o computador compartilhado. Se ele precisar acessar, garanta que o acesso ao computador compartilhado seja feito com um nome de usuário e uma senha diferentes das credenciais de administrador ele.

- Verifique se os usuários não têm permissões administrativas desnecessárias. No exemplo, verifique se todos no grupo compartilhado realmente requerem direitos de administrador no computador exposto.

- Verifique se as pessoas têm acesso apenas aos recursos necessários. No exemplo, Ron Harper amplia significativamente a exposição de Nick Cowley. É necessário que Ron Harper seja incluído no grupo? Há subgrupos que podem ser criados para minimizar a exposição ao movimento lateral?

**Dica** – quando não for detectada nenhuma possível atividade de caminho de movimento lateral para uma entidade nas últimas 48 horas, escolha **Exibir uma data diferente** e verifique se há possíveis caminhos de movimento lateral anteriores. O **Relatório de LMP para usuários confidenciais** está sempre disponível, se os LMPs tiverem sido descobertos, e fornece informações sobre possíveis caminhos de movimento lateral detectados para usuários confidenciais. 

**Dica** – para obter instruções sobre como configurar seus servidores e clientes para permitir que o Azure ATP execute as operações de SAM-R necessárias para detectar caminhos de movimento lateral, veja [Configurar SAM-R](install-atp-step8-samr.md).


## <a name="investigating-lmps"></a>Investigando LMPs
Para obter instruções de como identificar e investigar o uso de caminhos de movimento lateral da ATP do Azure, confira [Investigar caminhos de movimento lateral](investigate-lateral-movement-path.md).


## <a name="see-also"></a>Consulte Também
- [Investigando LMPs da ATP do Azure](investigate-lateral-movement-path.md)
- [Configurar o Azure ATP para realizar chamadas remotas para SAM](install-atp-step8-samr.md)
- [Trabalhando com alertas de segurança](working-with-suspicious-activities.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
