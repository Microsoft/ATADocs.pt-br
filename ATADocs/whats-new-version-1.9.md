---
title: Novidades da versão 1.9 do ATA
description: Lista as novidades da nova versão 1.9 do ATA e os problemas conhecidos
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/25/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 51de491c-49ba-4aff-aded-cc133a8ccf0b
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: 261d6c5253dc697ae50523c24ccb34feba75a4e6
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2020
ms.locfileid: "84774665"
---
# <a name="whats-new-in-ata-version-19"></a>Novidades da versão 1.9 do ATA

A versão mais recente da atualização do ATA pode ser [baixada do Centro de Download](https://www.microsoft.com/download/details.aspx?id=56725) ou a versão completa pode ser baixada do [centro Eval](https://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).

Essas notas de versão fornecem informações sobre atualizações, novos recursos, correções de bug e problemas conhecidos nesta versão do Advanced Threat Analytics.

## <a name="new--updated-detections"></a>Detecções novas e atualizadas

-  **Criação de serviços suspeitos**: invasores tentam executar serviços suspeitos na sua rede. Agora, o ATA emite um alerta quando identifica que alguém executa um novo serviço, que parece suspeito, em um controlador de domínio. Essa detecção é baseada em eventos (e não em tráfego de rede). Para obter mais informações, veja o [Guia de atividades suspeitas](suspicious-activity-guide.md#suspicious-service-creation).


## <a name="new-reports-to-help-you-investigate"></a>Novos relatórios para ajudá-lo a investigar 

-   O recurso [**Senhas expostas em texto não criptografado**](reports.md) habilita a detecção de quando as contas confidenciais e não confidenciais enviam as credenciais de conta em texto sem formatação. Isso permite a investigação e a mitigação do uso da associação simples ao LDAP no seu ambiente, o que melhora o nível de segurança da rede. Esse relatório substitui os alertas de atividades suspeitas em texto não criptografado de contas confidenciais e de serviços.

- A opção [**Caminhos de movimento lateral para contas confidenciais**](reports.md) lista as contas confidenciais expostas por meio de caminhos de movimento lateral. Dessa forma, é possível reduzir esses caminhos e fortalecer sua rede a fim de minimizar o risco de superfície de ataque. Assim, você pode impedir a movimentação lateral, para que os invasores não se movimentem entre usuários e computadores ao longo da rede até encontrarem o prêmio máximo da segurança virtual: suas credenciais de conta do administrador.

## <a name="improved-investigation"></a>Investigação aprimorada

-  O ATA 1.9 inclui um novo e aprimorado [perfil de entidade](entity-profiles.md). O perfil de entidade fornece um painel projetado para fazer investigações completas e aprofundadas de usuários, dos recursos que eles acessaram e do histórico deles. O perfil de entidade também permite identificar usuários confidenciais que podem ser acessados por meio de caminhos de movimento lateral. 

-   O ATA 1.9 permite [marcar manualmente grupos](tag-sensitive-accounts.md) ou contas como confidenciais para aprimorar as detecções. Essa marcação afeta muitas detecções do ATA, como a detecção de modificação de grupos confidenciais e o caminho de movimento lateral, dependendo de quais grupos e contas são considerados confidenciais.

## <a name="performance-improvements"></a>Melhorias de desempenho

- O desempenho da infraestrutura da Central do ATA foi aprimorado: a exibição agregada do tráfego permite otimizar a CPU e o pipeline de pacotes, além de reutilizar soquetes para os controladores de domínio minimizarem as sessões de SSL para o controlador de domínio.



## <a name="additional-changes"></a>Alterações adicionais

- Depois de instalar uma nova versão do ATA, o ícone [**Novidades**](working-with-ata-console.md) será exibido na barra de ferramentas para que você saiba o que foi alterado na versão mais recente. Ele também fornece um link para o log de mudanças detalhado da versão.


## <a name="removed-and-deprecated-features"></a>Recursos removidos e preteridos

- O alerta **Atividade suspeita de confiança quebrada** foi removido.
- O recurso Senhas expostas em atividade suspeita em texto não criptografado foi removido. Ele foi substituído pelo [**Relatório de senhas expostas em texto não criptografado**](reports.md).



## <a name="see-also"></a>Consulte Também
[Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Atualizar o ATA para a versão 1.9 — guia de migração](ata-update-1.9-migration-guide.md)

