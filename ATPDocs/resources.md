---
title: Lista de recursos úteis para o Microsoft defender para identidade
description: Este artigo fornece uma lista de recursos úteis para o Microsoft defender para identidade
ms.date: 10/27/2020
ms.topic: conceptual
ms.openlocfilehash: e534baf48d472b9bada6366e9b0e2ccec5ef6c4c
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96542202"
---
# <a name="product-long-readiness-guide"></a>[!INCLUDE [Product long](includes/product-long.md)] Guia de preparação

Este artigo fornece uma lista de roteiros de preparação de recursos que ajudam você a começar a usar o [!INCLUDE [Product long](includes/product-long.md)] .

## <a name="understanding-product-long"></a>Básicas [!INCLUDE [Product long](includes/product-long.md)]

[!INCLUDE [Product long](includes/product-long.md)] o é um serviço de nuvem que ajuda a identificar e proteger sua empresa de vários tipos de ataques de invasores e ameaças internas avançadas.

Para saber mais sobre o [!INCLUDE [Product short](includes/product-short.md)]:

- [[!INCLUDE [Product short](includes/product-short.md)] sobre](what-is.md)
- [[!INCLUDE [Product short](includes/product-short.md)] vídeo introdutório (25 minutos)-completo](https://www.youtube.com/watch?v=EGY2m8yU_KE)
- [[!INCLUDE [Product short](includes/product-short.md)] vídeo aprofundado (75 minutos)-completo](https://www.youtube.com/watch?v=QXZIfH0wP3Q)

## <a name="deployment-decisions"></a>Decisões de implantação

[!INCLUDE [Product short](includes/product-short.md)] é composto de um serviço de nuvem que reside no Azure e de sensores integrados que podem ser instalados em controladores de domínio. Se você estiver usando servidores físicos, o planejamento de capacidade é fundamental. Obtenha ajuda da ferramenta de dimensionamento para alocar espaço para os sensores:

- [ [!INCLUDE [Product short](includes/product-short.md)] ferramenta de dimensionamento](https://aka.ms/aatpsizingtool) – a ferramenta de dimensionamento automatiza a coleta da quantidade de monitores de tráfego [!INCLUDE [Product short](includes/product-short.md)] . Ela fornece automaticamente o suporte e as recomendações do recurso para sensores.
- [[!INCLUDE [Product short](includes/product-short.md)] Diretrizes de planejamento de capacidade](capacity-planning.md)

## <a name="deploy-product-short"></a>Implantar o [!INCLUDE [Product short](includes/product-short.md)]

Use esses recursos para ajudá-lo a configurar [!INCLUDE [Product short](includes/product-short.md)] o, conectar-se a Active Directory, baixar o pacote do sensor, configurar a coleta de eventos e, opcionalmente, integrar com sua VPN e configurar contas e exclusões do honeytoken.

- [Experimente [!INCLUDE [Product short](includes/product-short.md)] (parte do EMS E5)](https://aka.ms/aatptrial)  a avaliação é válida por 90 dias.
- [ [!INCLUDE [Product short](includes/product-short.md)] Configurar](install-step1.md) siga estas etapas para implantar [!INCLUDE [Product short](includes/product-short.md)] em seu ambiente.
- [Integre [!INCLUDE [Product short](includes/product-short.md)] com o Microsoft defender para ponto de extremidade](integrate-mde.md)

## <a name="product-short-settings"></a>Configurações do[!INCLUDE [Product short](includes/product-short.md)]

Ao criar sua [!INCLUDE [Product short](includes/product-short.md)] instância, as configurações básicas necessárias são configuradas automaticamente. Há várias configurações adicionais configuráveis no [!INCLUDE [Product short](includes/product-short.md)] para melhorar a precisão de detecção e alerta para seu ambiente, como integração de VPN, permissões necessárias de Sam e configurações de política de auditoria avançadas.

- [Integração de VPN](install-step6-vpn.md)
- [Permissões exigidas pelo SAM-R](install-step8-samr.md)
- [Configurações de política de auditoria](configure-windows-event-collection.md) – auditar a integridade do controlador de domínio antes e depois de uma [!INCLUDE [Product short](includes/product-short.md)] implantação.

## <a name="work-with-product-short"></a>Trabalhar com [!INCLUDE [Product short](includes/product-short.md)]

Depois [!INCLUDE [Product short](includes/product-short.md)] que o estiver em execução, exiba alertas de segurança na [!INCLUDE [Product short](includes/product-short.md)] linha do tempo de atividade do Portal. A linha do tempo de atividade é a página de aterrissagem padrão depois de fazer logon no [!INCLUDE [Product short](includes/product-short.md)] Portal. Por padrão, todos os alertas de segurança abertos são mostrados na linha do tempo de atividade. Também é possível ver a gravidade atribuída a cada alerta. Investigue cada alerta, analisando detalhadamente as entidades (computadores, dispositivos, usuários) para abrir as páginas de perfil com mais informações. Os caminhos de movimento lateral mostram os possíveis movimentos que podem ser feitos em sua rede e os usuários confidenciais em risco. Investigue e corrija a exposição usando os grafos de detecção de caminho de movimento lateral. Esses recursos ajudam você a trabalhar com os [!INCLUDE [Product short](includes/product-short.md)] alertas de segurança do:

- [ [!INCLUDE [Product short](includes/product-short.md)] Guia de alerta de segurança](suspicious-activity-guide.md) Aprenda a fazer a triagem e executar as próximas etapas com suas [!INCLUDE [Product short](includes/product-short.md)] detecções.
- [[!INCLUDE [Product short](includes/product-short.md)] caminhos de movimento lateral](use-case-lateral-movement-path.md)
- [Marque grupos como confidenciais](sensitive-accounts.md) Aumente a visibilidade da exposição de credenciais em grupos de segurança confidenciais.

## <a name="security-best-practices"></a>Melhores práticas de segurança

- [ [!INCLUDE [Product short](includes/product-short.md)] Perguntas](technical-faq.md) frequentes – Este artigo fornece uma lista de perguntas frequentes sobre o [!INCLUDE [Product short](includes/product-short.md)] e fornece informações e respostas.

## <a name="community-resources"></a>Recursos da comunidade

Blog: [ [!INCLUDE [Product short](includes/product-short.md)] blog](https://aka.ms/aatpblog)

Comunidade pública: [ [!INCLUDE [Product short](includes/product-short.md)] comunidade de tecnologia](https://aka.ms/AatpCom)

Comunidade privada: [ [!INCLUDE [Product short](includes/product-short.md)] grupo do Yammer](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893&view=all&preserve-view=true)

Channel 9: [Página do Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)

## <a name="see-also"></a>Consulte Também

- [Trabalhando com contas confidenciais](sensitive-accounts.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
