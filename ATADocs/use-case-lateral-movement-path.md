---
title: Investigando ataques de caminho de movimento lateral com o ATA | Microsoft Docs
description: Este artigo descreve como detectar ataques de caminho de movimento lateral com o ATA (Advanced Threat Analytics).
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 710f01bd-c878-4406-a7b2-ce13f98736ea
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: dc03cfe1719541dac0f8509c0f8f22987ecb96bb
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2018
---
*Aplica-se a: Advanced Threat Analytics versão 1.9*

# <a name="investigating-lateral-movement-paths-with-ata"></a>Investigando caminhos de movimento lateral com o ATA

Mesmo que você faça o melhor para proteger os usuários confidenciais e seus administradores tenham senhas complexas alteradas com frequência, computadores protegidos e dados armazenados com segurança, os invasores ainda podem usar caminhos de movimento lateral para acessar contas confidenciais. Em ataques de movimento lateral, o invasor tira proveito de situações em que os usuários confidenciais fazem logon em um computador no qual um usuário não confidencial tem direitos locais. Os invasores podem mover-se lateralmente acessando o usuário menos confidencial e, em seguida, movendo-se pelo computador para obter credenciais de usuários confidenciais. 

## <a name="what-is-a-lateral-movement-path"></a>O que é um caminho de movimento lateral?

O movimento lateral ocorre quando um invasor usa proativamente contas não confidenciais para acessar contas confidenciais. Eles podem usar qualquer um dos métodos descritos no [Guia de atividades suspeitas](suspicious-activity-guide.md) para obter a senha não confidencial inicial e, em seguida, usar uma ferramenta, como o Bloodhound, para entender quem são os administradores em sua rede e quais computadores eles acessaram. Em seguida, eles podem acessar os dados em seus controladores de domínio para saber quem tem quais contas e acesso a quais recursos e arquivos. Assim, eles podem roubar as credenciais de outros usuários (às vezes, de usuários confidenciais) armazenadas nos computadores que já acessaram e mover-se lateralmente pelos usuários e recursos até obter privilégios de administrador em sua rede. 

O ATA permite que você adote medidas preventivas em sua rede para impedir que invasores tenham êxito no movimento lateral.

## <a name="discovery-your-at-risk-sensitive-accounts"></a>Descura suas contas confidenciais que estão em risco

Para descobrir quais contas confidenciais de sua rede estão vulneráveis devido à sua conexão a contas ou recursos não confidenciais, siga estas etapas. Para proteger sua rede contra ataques de movimento lateral, o ATA trabalha do final ao começo, o que significa que o ATA oferece um mapa que começa por suas contas privilegiadas e mostra quais usuários e dispositivos estão no caminho lateral desses usuários e de suas credenciais.

1. No menu do console do ATA, clique no ícone de relatórios ![ícone de relatórios](./media/ata-report-icon.png).

2. Em **Caminhos de movimento lateral para contas confidenciais**, se não forem encontrados caminhos de movimento lateral, o relatório ficará indisponível. Se houver caminhos de movimento lateral, as datas do relatório selecionarão automaticamente a primeira data em que há dados relevantes. 

 ![relatórios](./media/reports.png)

3. Clique em **Baixar**.

3. O arquivo do Excel que é criado fornece detalhes sobre suas contas confidenciais que estão em risco. A guia **Resumo** fornece gráficos que detalham o número de contas confidenciais, computadores e médias de recursos em risco. A guia **Detalhes** fornece uma lista das contas confidenciais com que você deve se preocupar.


## <a name="investigate"></a>Investigar

Agora que você sabe quais contas confidenciais estão em risco, aprofunde-se no ATA para saber mais e tomar medidas preventivas.

1. No console do ATA, examine o usuário cuja conta está listada como vulnerável no relatório de **Caminhos de movimento lateral para contas confidenciais**, por exemplo, Samira Abbasi. Você também pode pesquisar a notificação de Movimento lateral que é adicionada ao perfil da entidade quando ela está em um caminho de movimento lateral ![ícone lateral](./media/lateral-movement-icon.png) ou ![ícone do caminho](./media/paths-icon.png).

2. Na página de perfil do usuário que é aberta, clique na guia **Caminhos de movimento lateral**.

3. O diagrama exibido fornece um mapa dos caminhos possíveis para seu usuário confidencial. O gráfico mostra conexões que foram feitas nos últimos dois dias, portanto, a exposição está atualizada.

4. Examine o gráfico para ver o que você pode aprender sobre a exposição das credenciais de seus usuários confidenciais. Por exemplo, neste mapa de Samira Abbasi, você pode seguir as setas cinza **Conectado por** para ver onde Samira fez logon com suas credenciais privilegiadas. Nesse caso, as credenciais confidenciais de Samira foram salvas no computador REDMOND-WA-DEV. Em seguida, veja quais outros usuários se conectaram em quais computadores e criaram mais exposição e vulnerabilidade. Você pode ver isso examinando as setas pretas **Administrador em** para ver quem tem privilégios de administrador no recurso. Neste exemplo, todos no grupo Contoso All podem acessar as credenciais do usuário desse recurso.  

 ![caminhos de movimento lateral do perfil do usuário](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Melhores práticas recomendadas

- A melhor maneira de impedir o movimento lateral é verificar se os usuários confidenciais usam suas credenciais de administrador somente ao fazer logon em computadores protegidos que nenhum usuário não confidencial tenha direitos de administrador no mesmo computador. No exemplo, verifique se Samira precisa de acesso a REDMOND-WA-DEV, se ela faz logon com nome de usuário e senha diferentes de suas credenciais de administrador ou remova o grupo Contoso All do grupo de administradores locais em REDMOND-WA-DEV.

- Também é recomendável que você assegure que ninguém tenha permissões administrativas desnecessárias. No exemplo, você deve verificar se todos no grupo Contoso All realmente precisam de direitos de administrador em REDMOND-WA-DEV.

- É sempre uma boa ideia certificar-se de que as pessoas tenham acesso somente a recursos necessários. Como você pode ver no exemplo, Oscar Posada amplia significativamente a exposição de Samira. Ele precisa estar incluído em Contoso All? Há subgrupos que você poderia criar para minimizar a exposição?


## <a name="see-also"></a>Consulte Também
- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
