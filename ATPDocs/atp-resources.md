---
title: Lista de recursos úteis da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Este artigo contém uma lista de recursos úteis do Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/15/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 34dc152c-6b7f-4128-93fe-aad56c282730
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 56b74b2e02fcab2b7584afbabd5d4384f066261c
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166366"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*



# <a name="azure-atp-readiness-guide"></a>Guia de preparação do Azure ATP

Este artigo contém um roteiro de preparação que lista os recursos úteis para começar a usar a Proteção Avançada contra Ameaças. 

## <a name="understanding-azure-atp"></a>Noções básicas do Azure ATP

O ATP (Proteção Avançada contra Ameaças) é um serviço de nuvem que ajuda a identificar e a proteger a empresa de vários tipos de ameaças internas e ataques cibernéticos direcionados avançados. Use os seguintes recursos para saber mais sobre o Azure ATP: 
- [Visão geral do Azure ATP](what-is-atp.md)
- [Vídeo introdutório do Azure ATP – completo](https://www.youtube.com/watch?v=KX-xpFc0sBw) 

## <a name="deployment-decisions"></a>Decisões de implantação

O Azure ATP é composto por um Serviço de Nuvem que reside no Azure e por sensores integrados que podem ser instalados em um controlador de domínio ou em sensores autônomos em servidores dedicados. Antes de executar o Azure ATP, é importante escolher o tipo de sensor que se adapta melhor à sua implantação e às suas necessidades. Os sensores integrados do Azure ATP oferecem segurança aprimorada, custos operacionais mais baixos e implantação facilitada. Os sensores autônomos do Azure ATP requerem um hardware físico, etapas de configuração adicionais e maiores custos operacionais. <br>Se você estiver usando servidores físicos, o planejamento de capacidade é fundamental. Você pode obter ajuda da ferramenta de dimensionamento para alocar espaço para os sensores: 
- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/aatpsizingtool) – a ferramenta de dimensionamento automatiza a coleta da quantidade de tráfego que a Azure ATP monitora. Ela fornece automaticamente o suporte e as recomendações do recurso para sensores. 
- [Diretrizes de planejamento da capacidade do ATA](atp-capacity-planning.md)

## <a name="deploy-azure-atp"></a>Implantar o Azure ATP

Esses recursos ajudarão você a configurar o Azure ATP, conectar ao Active Directory, baixar o pacote do sensor, configurar coleta de eventos e, opcionalmente, integrar com a sua VPN e configurar contas de honeytoken e exclusões. 
- [Teste o Azure ATP (parte do EMS E5)](http://aka.ms/aatptrial) A avaliação é válida por 90 dias.
- [Guia de implantação](install-atp-step1.md) Siga estas etapas para implantar o Azure ATP no seu ambiente.
- [Integrar o Azure ATP ao Windows Defender ATP](integrate-wd-atp.md)

## <a name="azure-atp-settings"></a>Configurações do Azure ATP

As configurações básicas necessárias no Azure ATP são definidas ao criar o espaço de trabalho. No entanto, há várias outras configurações que podem ser definidas para ajustar o Azure ATP que tornam as detecções mais precisas para o ambiente, como a integração do SIEM e configurações de auditoria. 

- [Documentação geral do Azure ATP](what-is-atp.md)
- [Configurações de auditoria](https://blogs.technet.microsoft.com/positivesecurity/2017/08/18/ata-auditing-auditpol-advanced-audit-settings-enforcement-lightweight-gateway-service-discovery/) – Audite a integridade do controlador de domínio antes e após uma implantação do ATP. 

## <a name="work-with-azure-atp"></a>Trabalhar com o Azure ATP

Depois que o Azure ATP estiver em execução, visualize as atividades suspeitas detectadas na linha do tempo de atividades do portal do Azure ATP. A linha do tempo de atividade é a página de aterrissagem padrão depois do login no portal do Azure ATP. Por padrão, todas as atividades suspeitas abertas são mostradas na linha do tempo de ataque. Você também pode ver a severidade atribuída a cada atividade. Investigue cada atividade suspeita, analisando as entidades (computadores, dispositivos, usuários) para abrir as páginas de perfil com mais informações. Esses recursos ajudam você a trabalhar com as atividades suspeitas do Azure ATP: 

- [Guia de atividades suspeitas do Azure ATP](suspicious-activity-guide.md) Saiba como fazer triagens e siga os próximos passos com as detecções do Azure ATP.
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
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)