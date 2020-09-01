---
title: Lista de recursos úteis da Proteção Avançada contra Ameaças do Azure
description: Este artigo contém uma lista de recursos úteis do Azure ATP
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 02/19/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 34dc152c-6b7f-4128-93fe-aad56c282730
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fbd5b1c3b641559f8d5555d65f4424ab34acd80d
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88956594"
---
# <a name="azure-atp-readiness-guide"></a>Guia de preparação do Azure ATP

Este artigo oferece uma lista de recursos do roteiro de preparação que ajuda a começar a usar a Proteção Avançada contra Ameaças do Azure.

## <a name="understanding-azure-atp"></a>Noções básicas do Azure ATP

O ATP (Proteção Avançada contra Ameaças) é um serviço de nuvem que ajuda a identificar e a proteger a empresa de vários tipos de ameaças internas e ataques cibernéticos direcionados avançados.

Para saber mais sobre o Azure ATP:

- [Visão geral do Azure ATP](what-is-atp.md)
- [Vídeo introdutório do Azure ATP (25 minutos) – completo](https://www.youtube.com/watch?v=EGY2m8yU_KE)
- [Vídeo aprofundado do Azure ATP (75 minutos) – completo](https://www.youtube.com/watch?v=QXZIfH0wP3Q)

## <a name="deployment-decisions"></a>Decisões de implantação

O ATP do Azure é composto por um serviço de nuvem que reside no Azure e por sensores integrados que podem ser instalados em controladores de domínio. Se você estiver usando servidores físicos, o planejamento de capacidade é fundamental. Obtenha ajuda da ferramenta de dimensionamento para alocar espaço para os sensores:

- [Ferramenta de dimensionamento do Azure ATP](https://aka.ms/aatpsizingtool) – a ferramenta de dimensionamento automatiza a coleta da quantidade de tráfego que a Azure ATP monitora. Ela fornece automaticamente o suporte e as recomendações do recurso para sensores.
- [Diretrizes de planejamento da capacidade do ATP](atp-capacity-planning.md)

## <a name="deploy-azure-atp"></a>Implantar o Azure ATP

Use esses recursos para configurar o ATP do Azure, conectar ao Active Directory, baixar o pacote do sensor, configurar a coleta de eventos e, opcionalmente, integrar à sua VPN e configurar contas e exclusões de honeytoken.

- [Teste o Azure ATP (parte do EMS E5)](https://aka.ms/aatptrial) A avaliação é válida por 90 dias.
- [Configuração do ATP do Azure](install-atp-step1.md) Siga essas etapas para implantar o ATP do Azure em seu ambiente.
- [Integração do ATP do Azure com o Microsoft Defender ATP](integrate-wd-atp.md)

## <a name="azure-atp-settings"></a>Configurações do Azure ATP

Durante a criação da instância do ATP do Azure, as configurações básicas necessárias são definidas automaticamente. Há várias definições configuráveis adicionais no ATP do Azure para melhorar a detecção e a precisão do alerta para seu ambiente, como a integração de VPN, as permissões necessárias para SAM e as configurações de política de auditoria avançadas.

- [Integração de VPN](install-atp-step6-vpn.md)
- [Permissões exigidas pelo SAM-R](install-atp-step8-samr.md)
- [Configurações da política de auditoria](configure-windows-event-collection.md) – audite a integridade do controlador de domínio antes e após uma implantação do ATP.

## <a name="work-with-azure-atp"></a>Trabalhar com o Azure ATP

Depois que o ATP do Azure estiver em funcionamento, exiba os alertas de segurança na linha do tempo da atividade do portal do ATP do Azure. A linha do tempo de atividade é a página de aterrissagem padrão após o logon no portal do ATP do Azure. Por padrão, todos os alertas de segurança abertos são mostrados na linha do tempo de atividade. Também é possível ver a gravidade atribuída a cada alerta. Investigue cada alerta, analisando detalhadamente as entidades (computadores, dispositivos, usuários) para abrir as páginas de perfil com mais informações. Os caminhos de movimento lateral mostram os possíveis movimentos que podem ser feitos em sua rede e os usuários confidenciais em risco. Investigue e corrija a exposição usando os grafos de detecção de caminho de movimento lateral. Estes recursos ajudam a trabalhar com os alertas de segurança do Azure ATP:

- [Guia de alerta de segurança do Azure ATP](suspicious-activity-guide.md) Saiba como fazer triagens e siga os próximos passos com as detecções do Azure ATP.
- [Caminhos de movimento lateral do ATP do Azure](use-case-lateral-movement-path.md)
- [Marque grupos como confidenciais](sensitive-accounts.md) Aumente a visibilidade da exposição de credenciais em grupos de segurança confidenciais.

## <a name="security-best-practices"></a>Práticas recomendadas de segurança

- [Perguntas frequentes do Azure ATP](atp-technical-faq.md) – este artigo fornece uma lista de perguntas frequentes sobre o Azure ATP, bem como informações e respostas.

## <a name="community-resources"></a>Recursos da comunidade

Blog: [Blog do Azure ATP](https://aka.ms/aatpblog)

Comunidade pública: [Comunidade Tecnológica do Azure ATP](https://aka.ms/AatpCom)

Comunidade privada: [Grupo do Azure ATP no Yammer](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893&view=all)

Channel 9: [Página do Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)

## <a name="see-also"></a>Confira Também

- [Como trabalhar com contas confidenciais](sensitive-accounts.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)