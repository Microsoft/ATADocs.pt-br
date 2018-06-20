---
title: O que é o Azure ATP (Proteção Avançada contra Ameaças)? | Microsoft Docs
description: Explica o que é o Azure ATP (Proteção Avançada contra Ameaças) e os tipos de atividades suspeitas que ele pode detectar
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 2d14d0e9-1b03-4bcc-ae97-8fd41526ffc5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5ccac90a171c895ee8b4d5336a125ccd7fa66239
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2018
ms.locfileid: "29445072"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*


# <a name="what-is-azure-advanced-threat-protection"></a>O que é a Proteção Avançada contra Ameaças do Azure?
O Azure ATP (Proteção Avançada contra Ameaças) é um serviço de nuvem que ajuda a proteger seus ambientes híbridos corporativos de vários tipos de ameaças internas e ataques cibernéticos direcionados avançados.

## <a name="how-azure-atp-works"></a>Como o Azure ATP funciona

O Azure ATP aproveita um mecanismo de análise de rede proprietário para capturar e analisar o tráfego de rede de vários protocolos (como Kerberos, DNS, RPC, NTLM entre outros) para autenticação, autorização e coleta de informações. Essas informações são coletadas pelo Azure ATP por meio do(a):

-   Implantação de sensores do Azure ATP diretamente em seus controladores de domínio
-   Espelhamento de porta de controladores de domínio e servidores DNS para o sensor autônomo do Azure ATP

O Azure ATP obtém informações de várias fontes de dados, como eventos e logs em sua rede, a fim de aprender o comportamento dos usuários e de outras entidades na organização e criar um perfil comportamental sobre eles.
O Azure ATP pode receber eventos e logs de:

-   Integração do SIEM
-   WEF (Encaminhamento de Eventos do Windows)
-   Diretamente do Coletor de Eventos do Windows (para o sensor)
-   Contabilidade do RADIUS para VPNs


Para obter mais informações sobre a arquitetura do Azure ATP, consulte [Arquitetura do Azure ATP](atp-architecture.md).

## <a name="what-does-azure-atp-do"></a>O que o Azure ATP faz?

A tecnologia do Azure ATP detecta várias atividades suspeitas, concentrando-se em várias fases da cadeia do ataque cibernético, incluindo:

-   Reconhecimento, durante o qual os invasores coletam informações sobre como o ambiente foi compilado criado, o que são os ativos diferentes e quais entidades existem. Geralmente, eles criam o plano para as próximas fases do ataque.
-   Ciclo de movimentação lateral, durante o qual um invasor investe tempo e esforço na propagação da superfície de seu ataque dentro de sua rede.
-   Controle do domínio (persistência), durante o qual um invasor captura as informações permitindo que retome sua campanha usando vários conjuntos de pontos de entrada, credenciais e técnicas. 

Essas fases de um ataque cibernético são semelhantes e previsíveis, independentemente do tipo de empresa que está sob ataque ou do tipo de informação visado.
O Azure ATP procura três tipos de ataques principais: ataques mal-intencionados, comportamento anormal e riscos e problemas de segurança.

**Ataques mal-intencionados** são detectadas de forma determinística, bem como por meio de análise de comportamento anormal. A lista completa de tipos de ataques conhecidos inclui:

-   Pass-the-Ticket (PtT)
-   Pass-the-Hash (PtH)
-   Overpass-the-Hash
-   PAC Forjado (MS14-068)
-   Golden Ticket
-   Replicação mal-intencionada
-   Enumeração do serviço de diretório
-   Enumeração da Sessão SMB
-   Reconhecimento de DNS
-   Força bruta horizontal 
-   Força bruta vertical
-   Skeleton Key
-   Protocolo incomum
-   Downgrade de criptografia
-   Execução remota
-   Criação de serviço mal-intencionado


O Azure ATP detecta essas atividades suspeitas e revela as informações no portal de espaço de trabalho do Azure ATP, incluindo uma visão clara de Quem, O que, Quando e Como. Como você pode ver, monitorando este painel simples e fácil de usar, você será alertado de que o Azure ATP suspeita de uma tentativa de ataque Pass-the-Ticket nos computadores Cliente 1 e Cliente 2 em sua rede.

 ![tela de exemplo do Azure ATP de pass-the-ticket](media/pass-the-ticket-sa.png)


O Azure ATP também detecta **riscos e problemas de segurança**, incluindo:

-   Protocolos fracos
-   Vulnerabilidades de protocolo conhecidas
-   [Caminho de movimento lateral para contas confidenciais](use-case-lateral-movement-path.md)

# <a name="what-threats-does-azure-atp-look-for"></a>Que tipos de ameaças o Azure ATP procura?

O Azure ATP fornece detecção para as seguintes várias fases de um ataque avançado: reconhecimento, comprometimento de credenciais, movimento lateral, elevação de privilégios, predominância de domínio e outros. Essas detecções visam detectar ataques avançados e ameaças internas antes que eles possam causar danos à sua organização.

A detecção de cada fase resulta em várias atividades suspeitas relevantes para a fase em questão, em que cada atividade suspeita se correlaciona com diferentes tipos de ataques possíveis.
Essas fases na cadeia de ataques em que o Azure ATP atualmente fornece as detecções estão realçadas na imagem a seguir:

![O Azure ATP se concentra na atividade lateral da cadeia de ataque](media/attack-kill-chain-small.jpg)


Para obter mais informações, consulte [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md) e o [Guia de atividades suspeitas do Azure ATP](suspicious-activity-guide.md).

## <a name="whats-next"></a>Novidades

-   Para obter mais informações sobre como o Azure ATP se encaixa em sua rede: [Arquitetura do Azure ATP](atp-architecture.md)

-   Para começar a implantar o ATP: [Instalar o ATP](install-atp-step1.md)


## <a name="see-also"></a>Consulte Também
- [Perguntas frequentes sobre o Azure ATP](atp-technical-faq.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)