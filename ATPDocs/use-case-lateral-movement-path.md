---
title: Investigando ataques de caminho de movimento lateral com o Azure ATP | Microsoft Docs
description: "Este artigo descreve como detectar ataques de caminho de movimento lateral com o Azure ATP (Proteção Avançada contra Ameaças)."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: de15c920-8904-4124-8bdc-03abd9f667cf
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7deeec2c2ee2c2d964b6495921eba0fa378bd8ee
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2018
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure versão 1.9*

# <a name="investigating-lateral-movement-paths-with-azure-atp"></a>Investigando caminhos de movimento lateral com o Azure ATP

O Azure ATP pode ajudar você a impedir ataques que usam caminhos de movimento lateral. Mesmo quando você fazer o melhor para proteger os usuários confidenciais, seus administradores têm senhas complexas que alteram com frequência, seus computadores são protegidos e seus dados são armazenados com segurança, invasores ainda poderão usar caminhos de movimento lateral, movendo-se em sua rede entre usuários e computadores até que chegarem ao grande prêmio da segurança virtual: suas credenciais confidenciais da conta do administrador.

## <a name="what-is-a-lateral-movement-path"></a>O que é um caminho de movimento lateral?

O movimento lateral ocorre quando um invasor usa proativamente contas não confidenciais para acessar contas confidenciais. Eles podem usar qualquer um dos métodos descritos no [Guia de atividades suspeitas](suspicious-activity-guide.md) para obter a senha não confidencial inicial e, em seguida, usar uma ferramenta, como o Bloodhound, para entender quem são os administradores em sua rede e quais computadores eles acessaram. Em seguida, eles podem tirar proveito dos dados disponíveis para os invasores em seus controladores de domínio para saber quem tem quais contas e tem acesso a quais recursos e arquivos. Assim, eles podem roubar as credenciais de outros usuários (às vezes, usuários confidenciais) armazenadas nos computadores que já acessaram e, em seguida, mover-se lateralmente para mais usuários e recursos até obter privilégios de administrador em sua rede. 

O Azure ATP permite que você adote medidas preventivas em sua rede para impedir que invasores tenham êxito no movimento lateral.

## <a name="discovery-your-at-risk-sensitive-accounts"></a>Descura suas contas confidenciais que estão em risco

Para descobrir quais contas confidenciais de sua rede estão vulneráveis devido à sua conexão a contas ou recursos não confidenciais, siga estas etapas. Para proteger sua rede contra ataques de movimento lateral, o Azure ATP trabalha a partir do final, o que significa que o Azure ATP oferece um mapa que começa por suas contas privilegiadas e mostra quais usuários e dispositivos estão no caminho lateral desses usuários e suas credenciais.

1. No menu do portal de espaço de trabalho do Azure ATP, clique no ícone de relatórios ![ícone de relatórios](./media/atp-report-icon.png).

2. Em **Caminhos de movimento lateral para contas confidenciais**, se não forem encontrados caminhos de movimento lateral, o relatório ficará indisponível. Se houver caminhos de movimento lateral, as datas do relatório selecionarão automaticamente a primeira data em que há dados relevantes. O relatório de caminho de movimento lateral fornece dados dos últimos 60 dias.

 ![relatórios](./media/reports.png)

3. Clique em **Baixar**.

3. O arquivo do Excel que é criado fornece detalhes sobre suas contas confidenciais que estão em risco. A guia **Resumo** fornece gráficos que detalham o número de contas confidenciais, computadores e médias de recursos em risco. A guia **Detalhes** fornece uma lista das contas confidenciais com que você deve se preocupar.

4. Para obter instruções de como configurar seus servidores para permitir que o Azure ATP execute as operações de SAM-R necessárias para detectar caminhos de movimento lateral, consulte [Configurar SAM-R](install-atp-step8-samr.md).

## <a name="investigate"></a>Investigar

Agora que sabe quais contas confidenciais estão em risco, você pode se aprofundar no Azure ATP para saber mais e tomar medidas preventivas.

1. No portal de espaço de trabalho do Azure ATP, examine o usuário cuja conta está listada como vulnerável no relatório de **Caminhos de movimento lateral para contas confidenciais**, por exemplo, Samira Abbasi. Você também pode pesquisar pela notificação de Movimento lateral que é adicionada ao perfil da entidade quando ela está em um caminho de movimento lateral. ![ícone lateral](./media/lateral-movement-icon.png) ou ![ícone do caminho](./media/paths-icon.png). Isso estará disponível se tiver ocorrido um movimento lateral nos últimos dois dias. 

2. Na página de perfil do usuário que é aberta, clique na guia **Caminhos de movimento lateral**. 

3. O diagrama exibido fornece um mapa dos caminhos possíveis para seu usuário confidencial. O gráfico mostra conexões que foram feitas nos últimos dois dias, portanto, a exposição está atualizada. Se não tiver sido detectada nenhuma atividade nos últimos dois dias, o gráfico deixará de aparecer, mas o [relatório de caminho de movimento lateral](reports.md) ainda estará disponível para fornecer informações sobre caminhos de movimento lateral dos últimos 60 dias.

4. Examine o gráfico para ver o que você pode aprender sobre a exposição das credenciais de seus usuários confidenciais. Por exemplo, neste mapa de Samira Abbasi, você pode seguir as setas cinza **Conectado por** para ver onde Samira se conectou com suas credenciais privilegiadas. Nesse caso, as credenciais confidenciais de Samira foram salvas no computador REDMOND-WA-DEV. Em seguida, veja quais outros usuários se conectaram em quais computadores e criaram mais exposição e vulnerabilidade. Você pode ver isso examinando as setas pretas **Administrador em** para ver quem tem privilégios de administrador no recurso. Neste exemplo, todos no grupo Contoso All podem acessar as credenciais do usuário desse recurso.  

 ![caminhos de movimento lateral do perfil do usuário](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Melhores práticas recomendadas

- A melhor maneira de impedir movimentos laterais é certificar-se de que os usuários confidenciais usem suas credenciais de administrador somente ao fazer logon em computadores protegidos. No exemplo, certifique-se de que, se a administradora Samira precisar de acesso a REDMOND-WA-DEV, ela faça logon com um nome de usuário e senha diferentes de suas credenciais de administrador.

- Também é recomendável que você certifique-se de que ninguém tenha permissões administrativas desnecessárias. No exemplo, você deve verificar se todos no grupo Contoso All realmente precisam de direitos de administrador em REDMOND-WA-DEV.

- É sempre uma boa ideia certificar-se de que as pessoas tenham acesso somente a recursos necessários. Como você pode ver no exemplo, Oscar Posada amplia significativamente a exposição de Samira. É necessário que o usuário esteja incluído em Contoso All? Há subgrupos que você poderia criar para minimizar a exposição?


## <a name="see-also"></a>Consulte Também

- [Configurar permissões necessárias do SAM-R](install-atp-step8-samr.md)
- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)