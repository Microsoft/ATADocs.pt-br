---
title: Investigando ataques de caminho de movimento lateral com o ATA | Microsoft Docs
description: Este artigo descreve como detectar ataques de caminho de movimento lateral com o ATA (Advanced Threat Analytics).
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 6/14/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 710f01bd-c878-4406-a7b2-ce13f98736ea
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 28661912916dfc4838584c00758244f15eda0b89
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2019
ms.locfileid: "58674768"
---
# <a name="investigating-lateral-movement-paths-with-ata"></a>Investigando caminhos de movimento lateral com o ATA


*Aplica-se a: Advanced Threat Analytics versão 1.9*

Mesmo que você faça o melhor para proteger os usuários confidenciais e seus administradores tenham senhas complexas alteradas com frequência, computadores protegidos e dados armazenados com segurança, os invasores ainda podem usar caminhos de movimento lateral para acessar contas confidenciais. Em ataques de movimento lateral, o invasor tira proveito de situações em que os usuários confidenciais fazem logon em um computador no qual um usuário não confidencial tem direitos locais. Os invasores podem mover-se lateralmente acessando o usuário menos confidencial e, em seguida, movendo-se pelo computador para obter credenciais de usuários confidenciais. 

## <a name="what-is-a-lateral-movement-path"></a>O que é um caminho de movimento lateral?

O movimento lateral ocorre quando um invasor usa contas não confidenciais para acessar contas confidenciais. Isso pode ser feito usando os métodos descritos no [Guia de atividades suspeitas](suspicious-activity-guide.md). Para entender quem são os administradores na sua rede e quais computadores o invasor pode acessar, ele pode tirar proveito dos dados em seus controladores de domínio. 

O ATA permite que você adote medidas preventivas em sua rede para impedir que invasores tenham êxito na movimentação lateral.

## <a name="discovery-your-at-risk-sensitive-accounts"></a>Descura suas contas confidenciais que estão em risco

Para descobrir quais contas confidenciais na sua rede estavam vulneráveis devido à conexão a contas ou recursos não confidenciais em um período específico, siga estas etapas. 

1. No menu do console do ATA, clique no ícone de relatórios ![ícone de relatórios](./media/ata-report-icon.png).

2. Em **Caminhos de movimento lateral para contas confidenciais**, se não forem encontrados caminhos de movimento lateral, o relatório ficará indisponível. Se houver caminhos de movimento lateral, as datas do relatório selecionarão automaticamente a primeira data em que há dados relevantes. 

   ![relatórios](./media/reports.png)

3. Clique em **Baixar**.

4. O arquivo do Excel que é criado fornece detalhes sobre suas contas confidenciais que estão em risco. A guia **Resumo** fornece gráficos que detalham o número de contas confidenciais, computadores e médias de recursos em risco. A guia **Detalhes** fornece uma lista das contas confidenciais com que você deve se preocupar. Observe que os caminhos são caminhos que existiam anteriormente e podem não estar disponível atualmente.


## <a name="investigate"></a>Investigar

Agora que você sabe quais contas confidenciais estão em risco, aprofunde-se no ATA para saber mais e tomar medidas preventivas.

1. No console do ATA, pesquise a notificação de Movimentação lateral que foi adicionada ao perfil da entidade quando ela está em um caminho de movimentação lateral ![ícone lateral](./media/lateral-movement-icon.png) ou ![ícone do caminho](./media/paths-icon.png). Isso estará disponível se tiver ocorrido um caminho de movimentação lateral nos últimos dois dias.

2. Na página de perfil do usuário que é aberta, clique na guia **Caminhos de movimento lateral**.

3. O gráfico exibido fornece um mapa dos caminhos possíveis para o usuário confidencial. O grafo mostra conexões que foram feitas nos últimos dois dias.

4. Examine o gráfico para ver o que você pode aprender sobre a exposição das credenciais de seus usuários confidenciais. Por exemplo, neste mapa, é possível seguir as setas cinzas **Conectado por** para ver onde Samira se conectou com suas credenciais privilegiadas. Nesse caso, as credenciais confidenciais de Samira foram salvas no computador REDMOND-WA-DEV. Em seguida, veja quais outros usuários se conectaram em quais computadores e criaram mais exposição e vulnerabilidade. Você pode ver isso examinando as setas pretas **Administrador em** para ver quem tem privilégios de administrador no recurso. Neste exemplo, todos no grupo **Contoso All** podem acessar as credenciais do usuário desse recurso.  

   ![caminhos de movimento lateral do perfil do usuário](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>Melhores práticas recomendadas

- A melhor maneira de impedir o movimento lateral é verificar se os usuários confidenciais usam suas credenciais de administrador somente ao fazer logon em computadores protegidos que nenhum usuário não confidencial tenha direitos de administrador no mesmo computador. No exemplo, verifique se Samira precisa de acesso a REDMOND-WA-DEV, se ela faz logon com nome de usuário e senha diferentes de suas credenciais de administrador ou remova o grupo Contoso All do grupo de administradores locais em REDMOND-WA-DEV.

- Também é recomendável que você assegure que ninguém tenha permissões administrativas desnecessárias. No exemplo, você deve verificar se todos no grupo Contoso All realmente precisam de direitos de administrador em REDMOND-WA-DEV.

- Verifique se as pessoas têm acesso apenas aos recursos necessários. No exemplo, Oscar Posada amplia significativamente a exposição de Samira. É necessário que ele seja incluído no grupo **Contoso All**? Há subgrupos que você poderia criar para minimizar a exposição?

**Dica** – Se não tiver sido detectada nenhuma atividade nos últimos dois dias, o grafo deixará de aparecer, mas o relatório de caminho de movimentação lateral ainda estará disponível para fornecer informações sobre caminhos de movimentação lateral dos últimos 60 dias.

**Dica** – Para ver instruções de como configurar seus servidores para permitir que o ATA execute as operações de SAM-R necessárias para detectar caminhos de movimentação lateral, [configure o SAM-R](install-ata-step9-samr.md).




## <a name="see-also"></a>Consulte Também
- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
