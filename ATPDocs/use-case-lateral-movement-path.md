---
title: Investigando ataques de caminho de movimento lateral com o Azure ATP | Microsoft Docs
description: Este artigo descreve como detectar ataques de caminho de movimento lateral com o Azure ATP (Proteção Avançada contra Ameaças).
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 7/29/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: de15c920-8904-4124-8bdc-03abd9f667cf
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b89cc6e7933c4f75e69cd045551518b2806b3cf0
ms.sourcegitcommit: 759e99f670c42c2dd60d07b2200d3de01ddf6055
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2018
ms.locfileid: "39336108"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*

# <a name="investigating-lateral-movement-paths-with-azure-atp"></a>Investigando caminhos de movimento lateral com o Azure ATP


O movimento lateral ocorre quando um invasor usa contas não confidenciais para acessar contas confidenciais. Isso pode ser feito usando os métodos descritos no [Guia de atividades suspeitas](suspicious-activity-guide.md). O movimento lateral é usado pelos invasores para identificar e obter acesso às contas confidenciais e máquinas em sua rede usando contas não confidenciais que compartilham credenciais de logon armazenadas em contas, grupos e computadores. Depois que um invasor obtém acesso, ele também pode aproveitar os dados em seus controladores de domínio.


## <a name="discovery-your-at-risk-sensitive-accounts"></a>Descura suas contas confidenciais que estão em risco

Para descobrir quais contas confidenciais de sua rede estão expostas devido à sua conexão a contas, grupos e computadores não confidenciais, siga estas etapas. 

1. No menu do portal de espaço de trabalho do Azure ATP, clique no ícone de relatórios ![ícone de relatórios](./media/atp-report-icon.png).

2. Em **Caminhos de movimento lateral para contas confidenciais**, se não forem encontrados caminhos potenciais de movimento lateral, o relatório ficará indisponível. Se houver o potencial para caminhos de movimento lateral, o relatório pré-selecionará automaticamente a primeira data em que há dados relevantes. O relatório de caminho de movimento lateral fornece dados de até 60 dias.

 ![relatórios](./media/reports.png)

3. Clique em **Baixar**.

4. É criado um arquivo do Excel que fornece detalhes sobre os possíveis caminhos de movimento lateral e exposição de conta confidencial para as datas selecionadas. A guia **Resumo** fornece gráficos que detalham o número de contas confidenciais, computadores e as médias do acesso em risco. A guia **Detalhes** fornece uma lista das contas confidenciais que você deve investigar mais. Observe que os caminhos detalhados no relatório baixado podem não estar mais disponíveis porque foram detectados nos últimos 60 dias e podem ter sido alterados ou modificados.


## <a name="investigate"></a>Investigar



1. No portal do espaço de trabalho do Azure ATP, pesquise a notificação de Movimento lateral que foi adicionada ao perfil da entidade quando ela está em um caminho de movimento lateral ![ícone lateral](./media/lateral-movement-icon.png) ou ![ícone do caminho](./media/paths-icon.png). Observe que as notificações só aparecerão se houver movimento lateral nas últimas 48 horas. 

2. Na página de perfil do usuário que é aberta, clique na guia **Caminhos de movimento lateral**. 

3. O gráfico exibido fornece um mapa dos caminhos possíveis para o usuário confidencial. O gráfico mostra as possíveis conexões observadas nas últimas 48 horas. Se não foi detectada nenhuma atividade nos últimos dois dias, o gráfico não será exibido. 

4. Examine o gráfico para ver o que você pode aprender sobre a exposição das credenciais de seus usuários confidenciais. Por exemplo, neste mapa, você pode seguir as setas cinzas **Conectado por** para ver onde Samira se conectou com suas credenciais privilegiadas. Nesse caso, as credenciais confidenciais de Samira foram salvas no computador REDMOND-WA-DEV. Agora, observe quais outros usuários se conectaram em quais computadores e criaram mais exposição e vulnerabilidade. Você pode ver isso examinando as setas pretas **Administrador em** para ver quem tem privilégios de administrador no recurso. Neste exemplo, todos no grupo Contoso All podem acessar as credenciais do usuário desse recurso.  

 ![caminhos de movimento lateral do perfil do usuário](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Melhores práticas recomendadas

- A melhor maneira de impedir movimentos laterais é certificar-se de que os usuários confidenciais usem suas credenciais de administrador somente ao fazer logon em computadores protegidos. No exemplo, certifique-se de que, se a administradora Samira precisar de acesso a REDMOND-WA-DEV, ela faça logon com um nome de usuário e senha diferentes de suas credenciais de administrador.

- Também é recomendável que você certifique-se de que ninguém tenha permissões administrativas desnecessárias. No exemplo, você deve verificar se todos no grupo Contoso All realmente precisam de direitos de administrador em REDMOND-WA-DEV.

- Verifique se as pessoas têm acesso apenas aos recursos necessários. No exemplo, Oscar Posada amplia significativamente a exposição de Samira. É necessário que esse usuário seja incluído no grupo **Contoso All**? Existem subgrupos que podem ser criados para minimizar a exposição?

**Dica** – quando não for detectada nenhuma atividade nas últimas 48 horas e o gráfico não estiver disponível, o relatório de caminho de movimento lateral ainda estará disponível e fornecerá informações sobre os possíveis caminhos de movimento lateral detectados nos últimos 60 dias. 

**Dica** – para obter instruções sobre como configurar seus servidores e clientes para permitir que o Azure ATP execute as operações de SAM-R necessárias para detectar caminhos de movimento lateral, veja [Configurar SAM-R](install-atp-step8-samr.md).


## <a name="see-also"></a>Consulte Também

- [Configurar permissões necessárias do SAM-R](install-atp-step8-samr.md)
- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)