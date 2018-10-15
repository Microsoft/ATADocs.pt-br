---
title: Lista de recursos úteis da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Este artigo contém uma lista de recursos úteis do Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 34dc152c-6b7f-4128-93fe-aad56c282730
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 029077455f9b2800984065a10c3e221e62d7c606
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783144"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*



# <a name="azure-atp-readiness-guide"></a>Guia de preparação do Azure ATP

Este artigo contém um roteiro de preparação que lista os recursos úteis para começar a usar a Proteção Avançada contra Ameaças. 

## <a name="understanding-azure-atp"></a>Noções básicas do Azure ATP

O ATP (Proteção Avançada contra Ameaças) é um serviço de nuvem que ajuda a identificar e a proteger a empresa de vários tipos de ameaças internas e ataques cibernéticos direcionados avançados. Para saber mais sobre o Azure ATP: 
- [Visão geral do Azure ATP](what-is-atp.md)
- [Vídeo introdutório do Azure ATP (25 minutos) – completo](https://www.youtube.com/watch?v=EGY2m8yU_KE)
- [Vídeo aprofundado do Azure ATP (75 minutos) – completo](https://www.youtube.com/watch?v=QXZIfH0wP3Q)

## <a name="deployment-decisions"></a>Decisões de implantação

O Azure ATP é composto por um Serviço de Nuvem que reside no Azure e por sensores integrados que podem ser instalados em um controlador de domínio ou em sensores autônomos em servidores dedicados. Antes de executar o Azure ATP, é importante escolher o tipo de sensor que se adapta melhor à sua implantação e às suas necessidades. Os sensores integrados do Azure ATP (sensores do Azure ATP) fornecem segurança aprimorada, custos operacionais mais baixos e implantação mais fácil do que os sensores autônomos do Azure ATP. Os sensores autônomos do Azure ATP requerem um hardware físico, etapas de configuração adicionais e maiores custos operacionais. <br>Se você estiver usando servidores físicos, o planejamento de capacidade é fundamental. Você pode obter ajuda da ferramenta de dimensionamento para alocar espaço para os sensores: 
- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/aatpsizingtool) – a ferramenta de dimensionamento automatiza a coleta da quantidade de tráfego que a Azure ATP monitora. Ela fornece automaticamente o suporte e as recomendações do recurso para sensores. 
- [Diretrizes de planejamento da capacidade do ATP](atp-capacity-planning.md)

## <a name="deploy-azure-atp"></a>Implantar o Azure ATP

Esses recursos ajudarão você a configurar o Azure ATP, conectar ao Active Directory, baixar o pacote do sensor, configurar coleta de eventos e, opcionalmente, integrar com a sua VPN e configurar contas de honeytoken e exclusões. 
- [Teste o Azure ATP (parte do EMS E5)](http://aka.ms/aatptrial) A avaliação é válida por 90 dias.
- [Configuração do Azure ATP](install-atp-step1.md) Implante o Azure ATP em seu ambiente seguindo estas etapas.
- [Integrar o Azure ATP ao Windows Defender ATP](integrate-wd-atp.md)

## <a name="azure-atp-settings"></a>Configurações do Azure ATP

As configurações básicas necessárias no Azure ATP são configuradas ao criar seu workspace. No entanto, há várias configurações adicionais que podem ser definidas no Azure ATP que tornam as detecções mais precisas para seu ambiente, como integração de VPN, permissões exigidas por SAM e configurações avançadas da política de auditoria. 

- [Integração de VPN](install-atp-step6-vpn.md)
- [Permissões exigidas pelo SAM-R](install-atp-step8-samr.md)
- [Configurações da política de auditoria](atp-advanced-audit-policy.md) – audite a integridade do controlador de domínio antes e após uma implantação do ATP. 

## <a name="work-with-azure-atp"></a>Trabalhar com o Azure ATP

Depois que o Azure ATP estiver em execução, exiba os alertas de segurança na linha de tempo da atividade do portal do Azure ATP. A linha do tempo de atividade é a página de aterrissagem padrão depois do login no portal do Azure ATP. Por padrão, todos os alertas de segurança abertos são mostradas na linha do tempo de ataque. Também é possível ver a gravidade atribuída a cada alerta. Investigue cada alerta, analisando detalhadamente as entidades (computadores, dispositivos, usuários) para abrir as páginas de perfil com mais informações. Estes recursos ajudam a trabalhar com os alertas de segurança do Azure ATP: 

- [Guia de alerta de segurança do Azure ATP](suspicious-activity-guide.md) Saiba como fazer triagens e siga os próximos passos com as detecções do Azure ATP.
- [Marque grupos como confidenciais](sensitive-accounts.md) Aumente a visibilidade da exposição de credenciais em grupos de segurança confidenciais.

## <a name="security-best-practices"></a>Práticas recomendadas de segurança

- [Perguntas frequentes do Azure ATP](atp-technical-faq.md) – este artigo fornece uma lista de perguntas frequentes sobre o Azure ATP, bem como informações e respostas. 

## <a name="community-resources"></a>Recursos da comunidade

Blog: [Blog do Azure ATP](https://aka.ms/aatpblog)

Comunidade pública: [Comunidade Tecnológica do Azure ATP](https://aka.ms/AatpCom)

Comunidade privada: [Grupo do Azure ATP no Yammer](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893&view=all)

Channel 9: [Página do Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)



## <a name="see-also"></a>Consulte Também

- [Trabalhando com contas confidenciais](sensitive-accounts.md)
- [Confira o fórum do Azure ATP!](https://aka.ms/azureatpcommunity)