---
title: "Gerenciar configurações de telemetria | Microsoft ATA"
description: Descreve os dados coletados pelo ATA e fornece etapas para desativar a coleta de dados.
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 3a7e375da4acd5546347310c5965394b2addfe63
ms.openlocfilehash: 0c6b8589fffe24298d0caf2cf2eb5e7e817e4da2


---

*Aplica-se a: Advanced Threat Analytics versão 1.7*



# Gerenciamento das configurações de telemetria
O ATA (Advanced Threat Analytics) coleta dados de telemetria anônimos sobre o ATA e os transmite por uma conexão HTTPS para os servidores Microsoft.  Esses dados são usados pela Microsoft para ajudar a melhorar as versões futuras do ATA.

## Dados coletados
Os dados anônimos coletados incluem o seguinte:

-   Contadores de desempenho do Centro do ATA e do Gateway do ATA

-   ID do produto de cópias licenciadas do ATA

-   Data da implantação do Centro do ATA

-   Número de Gateways do ATA implantados

-   As seguintes informações anônimas do Active Directory:

    -   ID de Domínio do domínio cujo nome seria o primeiro domínio quando classificado em ordem alfabética

    -   Número de controladores de domínio

    -   Número de controladores de domínio monitorados pelo ATA por meio do espelhamento de porta

    -   Número de sites

    -   Número de computadores

    -   Número de grupos

    -   Número de usuários

-   Atividades suspeitas – os dados anônimos a seguir são coletados para cada atividade suspeita:

    (Os nomes de computador, nomes de usuário e endereços IP **não** são coletados)

    -   Tipo de atividade suspeita

    -   ID da atividade suspeita

    -   Status

    -   Horas de início e de término

    -   Entrada fornecida

- Problemas de integridade – Os seguintes dados anônimos são coletados para cada problema de integridade:

    (Os nomes de computador, nomes de usuário e endereços IP não são coletados)

    -   Tipo de problema de integridade

    -   ID do problema de integridade

    -   Status

    -   Horas de início e de término

- Endereços de URL do Console do ATA - Endereços de URL ao usar o Console do ATA, ou seja, quais páginas no Console do ATA foram visitadas.


### Desabilitar coleta de dados
Execute as etapas a seguir para interromper a coleta e o envio de dados de telemetria à Microsoft:

1.  Faça logon no Console do ATA, clique nos três pontos na barra de ferramentas e escolha **Sobre**.

2.  Desmarque a caixa para **Envie informações de uso para ajudar a melhorar a experiência do cliente no futuro**.

## Consulte Também
- [Novidades na versão 1.6](/advanced-threat-analytics/understand-explore/whats-new-version-1.6)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->


