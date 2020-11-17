---
title: Investigar ataques de caminho de movimento lateral com o ATA
description: Este artigo descreve como detectar ataques de caminho de movimento lateral com o ATA (Advanced Threat Analytics).
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 06/14/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 710f01bd-c878-4406-a7b2-ce13f98736ea
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4c240ff131442f5cee0dc3602a2e3309cd04e63d
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94689880"
---
# <a name="investigate-lateral-movement-paths-with-ata"></a>Investigar caminhos de movimento lateral com o ATA

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Mesmo que você faça o melhor para proteger os usuários confidenciais e seus administradores tenham senhas complexas alteradas com frequência, computadores protegidos e dados armazenados com segurança, os invasores ainda podem usar caminhos de movimento lateral para acessar contas confidenciais. Em ataques de movimento lateral, o invasor aproveita as instâncias quando usuários confidenciais entram em um computador em que um usuário não confidencial tem direitos locais. Os invasores podem mover-se lateralmente acessando o usuário menos confidencial e, em seguida, movendo-se pelo computador para obter credenciais de usuários confidenciais.

## <a name="what-is-a-lateral-movement-path"></a>O que é um caminho de movimento lateral?

O movimento lateral ocorre quando um invasor usa contas não confidenciais para acessar contas confidenciais. Isso pode ser feito usando os métodos descritos no [Guia de atividades suspeitas](suspicious-activity-guide.md). Os invasores usam o movimento lateral para identificar os administradores em sua rede e saber quais computadores eles podem acessar. Com essas informações e outras movimentações, o invasor pode tirar proveito dos dados em seus controladores de domínio.

O ATA permite que você adote medidas preventivas em sua rede para impedir que invasores tenham êxito na movimentação lateral.

## <a name="discovery-your-at-risk-sensitive-accounts"></a>Descura suas contas confidenciais que estão em risco

Para descobrir quais contas confidenciais em sua rede estão vulneráveis devido à sua conexão com contas ou recursos não confidenciais, em um período de tempo específico, siga estas etapas:

1. No menu do console do ATA, clique no ícone de relatórios ![ícone de relatórios](media/ata-report-icon.png).

1. Em **caminhos de movimentos laterais para contas confidenciais**, se não houver nenhum caminho de movimento lateral encontrado, o relatório ficará esmaecido. Se houver caminhos de movimento lateral, as datas do relatório selecionarão automaticamente a primeira data em que há dados relevantes.

    ![Captura de tela mostrando a seleção de data do relatório](media/reports.png)

1. Clique em **Baixar**.

1. O arquivo do Excel criado fornece detalhes sobre suas contas confidenciais em risco. A guia **Resumo** fornece gráficos que detalham o número de contas confidenciais, computadores e médias de recursos em risco. A guia **Detalhes** fornece uma lista das contas confidenciais com que você deve se preocupar. Observe que os caminhos são caminhos que existiam anteriormente e podem não estar disponível atualmente.

## <a name="investigate"></a>Investigar

Agora que você sabe quais contas confidenciais estão em risco, aprofunde-se no ATA para saber mais e tomar medidas preventivas.

1. No console do ATA, pesquise a notificação de Movimentação lateral que foi adicionada ao perfil da entidade quando ela está em um caminho de movimentação lateral ![ícone lateral](media/lateral-movement-icon.png) ou ![ícone do caminho](media/paths-icon.png). Isso estará disponível se tiver ocorrido um caminho de movimentação lateral nos últimos dois dias.

1. Na página de perfil do usuário que é aberta, clique na guia **Caminhos de movimento lateral**.

1. O gráfico exibido fornece um mapa dos caminhos possíveis para o usuário confidencial. O grafo mostra conexões que foram feitas nos últimos dois dias.

1. Examine o gráfico para ver o que você pode aprender sobre a exposição das credenciais de seus usuários confidenciais. Por exemplo, neste mapa, você pode seguir as setas de **logon em** cinza para ver onde Samira entrou com suas credenciais privilegiadas. Nesse caso, as credenciais confidenciais de Samira foram salvas no computador REDMOND-WA-DEV. Em seguida, veja quais outros usuários entraram em quais computadores criaram mais exposição e vulnerabilidade. Você pode ver isso examinando as setas pretas **Administrador em** para ver quem tem privilégios de administrador no recurso. Neste exemplo, todos no grupo **contoso All** têm a capacidade de acessar as credenciais do usuário a partir desse recurso.

    ![Caminhos de movimento lateral do perfil do usuário](media/user-profile-lateral-movement-paths.png)

## <a name="preventative-best-practices"></a>Melhores práticas recomendadas

- A melhor maneira de evitar o movimento lateral é garantir que os usuários confidenciais usem suas credenciais de administrador somente quando entrarem em computadores protegidos em que não haja nenhum usuário não confidencial que tenha direitos de administrador no mesmo computador. No exemplo, certifique-se de que se Samira precisar de acesso a REDMOND-WA-DEV, eles entrarão com um nome de usuário e senha diferentes de suas credenciais de administrador ou removerão o grupo contoso All do grupo de administradores locais em REDMOND-WA-DEV.

- Também é recomendável que você assegure que ninguém tenha permissões administrativas desnecessárias. No exemplo, verifique para ver se todos na contoso realmente precisam de direitos de administrador em REDMOND-WA-DEV.

- Verifique se as pessoas têm acesso apenas aos recursos necessários. No exemplo, Oscar Posada amplia significativamente a exposição de Samira. É necessário que eles sejam incluídos no grupo **contoso All**? Há subgrupos que você poderia criar para minimizar a exposição?

> [!TIP]
> Se a atividade não for detectada durante os últimos dois dias, o grafo não aparecerá, mas o relatório de caminho de movimento lateral ainda estará disponível para fornecer informações sobre caminhos de movimento lateral nos últimos 60 dias.

> [!TIP]
> Para obter instruções sobre como definir seus servidores para permitir que o ATA execute as operações SAM-R necessárias para detecção de caminho de movimento lateral, [Configure Sam-r](install-ata-step9-samr.md).

## <a name="see-also"></a>Veja também

- [Trabalhar com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
