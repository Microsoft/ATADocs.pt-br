---
title: "Gerenciamento das configurações de telemetria do Advanced Threat Analytics | Microsoft Docs"
description: Descreve os dados coletados pelo ATA e fornece etapas para desativar a coleta de dados.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/3/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b0e94ca7d817d6d5735921fefd7c9f4cf2cbd866
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*



<a id="manage-telemetry-settings" class="xliff"></a>

# Gerenciamento das configurações de telemetria
O ATA (Advanced Threat Analytics) coleta dados de telemetria anônimos sobre o ATA e os transmite por uma conexão HTTPS para os servidores Microsoft.  Esses dados são usados pela Microsoft para ajudar a melhorar as versões futuras do ATA.

<a id="data-collected" class="xliff"></a>

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


<a id="disable-data-collection" class="xliff"></a>

### Desabilitar coleta de dados
Execute as etapas a seguir para interromper a coleta e o envio de dados de telemetria à Microsoft:

1.  Faça logon no Console do ATA, clique nos três pontos na barra de ferramentas e escolha **Sobre**.

2.  Desmarque a caixa para **Envie informações de uso para ajudar a melhorar a experiência do cliente no futuro**.

<a id="see-also" class="xliff"></a>

## Consulte Também
- [Troubleshooting ATA using the event log](troubleshooting-ata-using-logs.md) (Solução de problemas do ATA usando o log de eventos)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
