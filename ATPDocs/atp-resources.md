---
title: Lista de recursos úteis da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Este artigo contém uma lista de recursos úteis do Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 7/23/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 34dc152c-6b7f-4128-93fe-aad56c282730
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 498d1b4d14db079583da1999bfb68a5648111362
ms.sourcegitcommit: 63a36cd96aec30e90dd77bee1d0bddb13d2c4c64
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39227131"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*



# <a name="azure-atp-readiness-guide"></a>Guia de preparação do Azure ATP

Este artigo contém um roteiro de preparação que lista os recursos úteis para começar a usar o Azure Advanced Threat Analytics. 

## <a name="understanding-azure-atp"></a>Noções básicas do Azure ATP

O ATP (Proteção Avançada contra Ameaças do Azure) é um serviço de nuvem que ajuda a proteger sua empresa de vários tipos de ameaças internas e ataques cibernéticos direcionados avançados. Use os seguintes recursos para saber mais sobre o Azure ATP: 
- [Visão geral do Azure ATP](what-is-atp.md)
- [Vídeo introdutório do Azure ATP – completo](https://www.youtube.com/watch?v=KX-xpFc0sBw) 

## <a name="deployment-decisions"></a>Decisões de implantação

O Azure ATP é composto de um Serviço de Nuvem que reside no Azure e de sensores que podem ser instalados em um controlador de domínio ou em servidores dedicados. Antes de executar o Azure ATP, é importante escolher o tipo de sensor que se adapta melhor à sua implantação.<br>Se você estiver usando servidores físicos, você deverá planejar a capacidade. Você pode obter ajuda da ferramenta de dimensionamento para alocar espaço para os sensores: 
- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/aatpsizingtool) – a ferramenta de dimensionamento automatiza a coleta da quantidade de tráfego que a Azure ATP monitora. Ela fornece automaticamente o suporte e as recomendações do recurso para sensores. 
- [Diretrizes de planejamento da capacidade do ATA](atp-capacity-planning.md)

## <a name="deploy-azure-atp"></a>Implantar o Azure ATP

Esses recursos ajudarão você a configurar o Azure ATP, conectar ao Active Directory, baixar o pacote do sensor, configurar coleta de eventos e, opcionalmente, integrar com a sua VPN e configurar contas de honeytoken e exclusões. 
- [Teste o Azure ATP (parte do EMS E5)](http://aka.ms/aatptrial) A avaliação é válida por 90 dias.
- [Guia de implantação](install-atp-step1.md) Siga estas etapas para implantar o Azure ATP no seu ambiente.
- [Integrar o Azure ATP ao Windows Defender ATP](integrate-wd-atp.md)

## <a name="azure-atp-settings"></a>Configurações do Azure ATP

As configurações básicas necessárias no Azure ATP são definidas ao criar o espaço de trabalho. No entanto, há várias outras configurações que podem ser definidas para ajustar o Azure ATP que tornam as detecções mais precisas para o seu ambiente, como a integração do SIEM e configurações de auditoria. 

- [Documentação geral do Azure ATP](what-is-atp.md)
- [Configurações de auditoria](https://blogs.technet.microsoft.com/positivesecurity/2017/08/18/ata-auditing-auditpol-advanced-audit-settings-enforcement-lightweight-gateway-service-discovery/) – Audite a integridade do seu controlador de domínio antes e após uma implantação do ATA. 

## <a name="work-with-azure-atp"></a>Trabalhar com o Azure ATP

Depois que o Azure ATP estiver em execução, você poderá exibir as atividades suspeitas detectadas na linha do tempo de atividade. Essa é a página de aterrissagem padrão exibida quando você entra no portal do Azure ATP. Por padrão, todas as atividades suspeitas abertas são mostradas na linha do tempo de ataque. Você também pode ver a severidade atribuída a cada atividade. Investigue cada atividade suspeita, analisando as entidades (computadores, dispositivos, usuários) para abrir suas páginas de perfil que fornecem mais informações. Esses recursos ajudarão você a trabalhar com as atividades suspeitas do Azure ATP: 

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