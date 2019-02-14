---
title: Roteiro de preparação e recursos do Advanced Threat Analytics | Microsoft Docs
description: Fornece uma lista de recursos do ATA, vídeos, introdução, implantação e links do roteiro de preparação.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 7/15/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 42a1a34f-ed6b-4538-befb-452168a30e8c
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b8fdc8fd65c2ada0f116ff67150939a06ab46fd2
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56076684"
---
# <a name="ata-readiness-roadmap"></a>Roteiro de preparação do ATA 

*Aplica-se a: Advanced Threat Analytics versão 1.9*

Este artigo fornece um roteiro de preparação que ajudará você a se familiarizar com o Advanced Threat Analytics.

## <a name="understanding-ata"></a>Compreendendo o ATA

O ATA (Advanced Threat Analytics) é uma plataforma local que ajuda a proteger sua empresa contra vários tipos de ataques cibernéticos avançados e ameaças internas. Use os seguintes recursos para saber mais sobre o ATA:

- [Visão geral do ATA](what-is-ata.md)

- [Vídeo de introdução do ATA – curto](https://aka.ms/ATAShort)

- [Vídeo introdutório do ATA – completo](https://aka.ms/ATAVideo) 


## <a name="deployment-decisions"></a>Decisões de implantação

O ATA é composto pelo Centro do ATA, que pode ser instalado em um servidor, e pelos Gateways do ATA, que podem ser instalados em computadores separados ou ao usar o Gateway Lightweight diretamente em seus controladores de domínio. Antes de você colocar em funcionamento, é importante tomar as decisões de implantação a seguir:

|Configuração | Decisão |
|----|----|
|Tipo de hardware|VM do Azure, físico, virtual|
|Grupo de Trabalho ou Domínio|Grupo de trabalho, domínio|
|Dimensionamento do Gateway|Gateway completo, Gateway Lightweight|
|Certificados|PKI, autoassinado|

Se você estiver usando servidores físicos, você deverá planejar a capacidade. Você pode obter ajuda da ferramenta de dimensionamento para alocar espaço para o ATA:

[Ferramenta de dimensionamento do ATA](ata-capacity-planning.md) – A ferramenta de dimensionamento automatiza a coleta da quantidade de tráfego que a ATA precisa. Ele fornece automaticamente o suporte e as recomendações do recurso para o centro do ATA e Gateways Lightweight do ATA.


[Planejamento da capacidade do ATA](ata-capacity-planning.md)


## <a name="deploy-ata"></a>Implantar o ATA

Esses recursos ajudarão você a baixar e instalar o Centro do ATA, a se conectar ao Active Directory, a baixar o pacote de Gateway do ATA, a configurar a coleta de eventos e, opcionalmente, integrar com a sua VPN e configurar contas de honeytoken e exclusões.

[Baixar o ATA](http://aka.ms/ataeval) – Antes de implantar o ATA, se você ainda não fez a decisão de compra do ATA, você poderá baixar a versão de avaliação. 

[Guia estratégico de POC do ATA](http://aka.ms/atapoc) – Guia para todas as etapas necessárias para fazer uma implantação de POC bem-sucedida do ATA.

[Vídeo de implantação do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes) – Este vídeo oferece uma visão geral das etapas de implantação do ATA em menos de 10 minutos.

## <a name="ata-settings"></a>Configurações do LAN

As configurações básicas necessárias no ATA são configuradas como parte do assistente de instalação. No entanto, há várias outras configurações que podem ser definidas para ajustar o ATA que torna as detecções mais precisas para o seu ambiente, como a integração do SIEM e configurações de auditoria.

[Configurações de auditoria](https://aka.ms/ataauditingblog) – Audite a integridade do seu controlador de domínio antes e após uma implantação do ATA.

[Documentação geral do ATA](https://docs.microsoft.com/advanced-threat-analytics/)

## <a name="work-with-ata"></a>Trabalhar com o ATA

Depois que o ATA estiver em execução, você poderá exibir as atividades suspeitas detectadas na linha do tempo do Ataque. Essa é a página de aterrissagem exibida quando você entra no Console do ATA. Por padrão, todas as atividades suspeitas abertas são mostradas na linha do tempo de ataque. Você também pode ver a severidade atribuída a cada atividade. Investigue cada atividade suspeita, analisando as entidades (computadores, dispositivos, usuários) para abrir suas páginas de perfil que fornecem mais informações. Esses recursos ajudarão você a trabalhar com as atividades suspeitas do ATA:

[Guia estratégico de atividades suspeitas do ATA](http://aka.ms/ataplaybook) – Este artigo o orienta por meio de técnicas de ataque de roubo de credenciais usando as ferramentas de pesquisa prontamente disponíveis na Internet. Em cada ponto de ataque, você pode ver como o ATA ajuda você a obter visibilidade nessas ameaças.

[Guia de atividade suspeita do ATA](suspicious-activity-guide.md)



## <a name="security-best-practices"></a>Práticas recomendadas de segurança

[Práticas recomendadas do ATA](https://aka.ms/atasecbestpractices) – Práticas recomendadas para proteger o ATA.

[Perguntas frequentes do ATA](ata-technical-faq.md) – Este artigo fornece uma lista de perguntas frequentes sobre o ATA e também fornece informações e respostas.

## <a name="additional-resources"></a>Recursos adicionais

[Página do Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)

## <a name="community-resources"></a>Recursos da comunidade

[Blog do ATA](https://aka.ms/ATABlog)
[comunidade do ATA](https://aka.ms/ATACommunity)
[Fornecer comentários sobre o ATA](https://aka.ms/ATAUserVoice)
