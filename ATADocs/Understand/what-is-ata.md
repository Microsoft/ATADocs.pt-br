---
title: "O que é o Microsoft Advanced Threat Analytics (ATA)? | Microsoft Docs"
description: "Explica o que é o Microsoft Advanced Threat Analytics (ATA) e os tipos de atividades suspeitas que ele pode detectar"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 22d08a20291b1651a36247e9ffbeff8c881aefc5
ms.openlocfilehash: 0941d7695f51eb5662626e02b5fc8a9997dea975


---

*Aplica-se a: Advanced Threat Analytics versão 1.7*


# <a name="what-is-advanced-threat-analytics"></a>O que é o Advanced Threat Analytics?
O ATA (Advanced Threat Analytics) é uma plataforma local que ajuda a proteger sua empresa contra vários tipos de ataques cibernéticos avançados e ameaças internas.

## <a name="how-ata-works"></a>Como o ATA funciona
O ATA obtém informações de várias fontes de dados, desde eventos e logs em sua rede, a fim de aprender o comportamento dos usuários e de outras entidades na organização e criar um perfil comportamental sobre eles.
O ATA pode receber eventos e logs de:

-   Integração do SIEM
-   WEF (Encaminhamento de Eventos do Windows)

Além disso, o ATA aproveita um mecanismo de análise de rede proprietário para capturar e analisar o tráfego de rede de vários protocolos (como Kerberos, DNS, RPC, NTLM entre outros) para autenticação, autorização e coleta de informações. Essas informações são coletadas pelo ATA por meio de:

-   Espelhamento de porta de seus controladores de domínio e servidores DNS para o Gateway do ATA
-   Implantação de um LGW (Gateway Lightweight do ATA) diretamente nos Controladores de domínio

Para saber mais sobre a arquitetura do ATA, confira [Arquitetura do ATA](/advanced-threat-analytics/plan-design/ata-architecture).

## <a name="what-does-ata-do"></a>O que o ATA faz?

A tecnologia do ATA detecta várias atividades suspeitas, concentrando-se em várias fases da cadeia do ataque cibernético, incluindo:

-   Reconhecimento, durante o qual os invasores coletam informações sobre como o ambiente foi criado, quais são os diferentes ativos e entidades que existem, e geralmente criam seu plano para as próximas fases do ataque.
-   Ciclo de movimentação lateral, durante o qual um invasor investe tempo e esforço na propagação da superfície de seu ataque dentro de sua rede.
-   Controle do domínio (persistência), durante o qual um invasor captura as informações permitindo que retome sua campanha usando vários conjunto de pontos de entrada, credenciais e técnicas. 

Essas fases de um ataque cibernético são semelhantes e previsíveis, independentemente do tipo de empresa que está sob ataque ou do tipo de informação visado.
O ATA procura três tipos de ataques principais: ataques mal-intencionados, comportamento anormal e riscos e problemas de segurança.

Os **ataques mal-intencionados** são detectados de forma determinista, olhando a lista completa de tipos de ataques conhecidos, incluindo:

-   Pass-the-Ticket (PtT)
-   Pass-the-Hash (PtH)
-   Overpass-the-Hash
-   PAC Forjado (MS14-068)
-   Golden Ticket
-   Replicações mal-intencionadas
-   Reconhecimento
-   Força Bruta
-   Execução remota

Para obter uma lista completa de detecções e suas descrições, consulte [Quais atividades suspeitas o ATA pode detectar?](ata-threats.md)
O ATA detecta essas atividades suspeitas e revela as informações no Console do ATA, incluindo uma visão clara de Quem, O que, Quando e Como. Como você pode ver, monitorando este painel simples e fácil de usar, você será alertado de que o ATA suspeita de uma tentativa de ataque Pass-the-Hash nos computadores Cliente 1 e Cliente 2 em sua rede.

 ![tela de exemplo do ATA de pass-the-hash](media/sample screen pth.png)

**Comportamento anormal** é detectado pelo ATA usando análise comportamental e aproveitando o Machine Learning para descobrir atividades questionáveis e comportamentos anormais em usuários e dispositivos de sua rede, incluindo:

-   Logons anormais
-   Ameaças desconhecidas
-   Compartilhamento de senha
-   Movimentação lateral


Você pode exibir as atividades suspeitas desse tipo no Painel do ATA. No exemplo a seguir, o ATA alerta você quando um usuário acessa quatro computadores que não são normalmente acessados por esse usuário, o que pode ser uma causa de alarme.

 ![comportamento anormal da tela de exemplo do ATA](media/sample screen abnormal behavior.png) 

O ATA também detecta **riscos e problemas de segurança**, incluindo:

-   Confiança quebrada
-   Protocolos fracos
-   Vulnerabilidades de protocolo conhecidas

Você pode exibir as atividades suspeitas desse tipo no Painel do ATA. No exemplo a seguir, o ATA está informando que há uma relação de confiança quebrada entre um computador em sua rede e o domínio.

  ![tela de exemplo de ATA de confiança quebrada](media/sample screen broken trust.png)


## <a name="whats-next"></a>Novidades

-   Para saber mais sobre como o ATA se adapta à sua rede: [Arquitetura do ATA](/advanced-threat-analytics/plan-design/ata-architecture)

-   Para começar a implantar o ATA: [Instalar o ATA](/advanced-threat-analytics/deploy-use/install-ata-step1)

## <a name="see-also"></a>Consulte também
[Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Feb17_HO1-->


