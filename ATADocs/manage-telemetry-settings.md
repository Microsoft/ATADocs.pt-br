---
title: Gerenciar logs gerados pelo sistema do Advanced Threat Analytics | Microsoft Docs
description: Descreve os dados coletados pelo ATA e fornece etapas para desativar a coleta de dados.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/26/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 602dcac31c5fe7e6b0dfb8761d86abfab0f454eb
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166163"
---
*Aplica-se a: Advanced Threat Analytics versão 1.9*



# <a name="manage-system-generated-logs-note"></a>Gerenciar logs gerados pelo sistema[!NOTE]

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

O ATA (Advanced Threat Analytics) coleta dados de log anônimos gerados pelo sistema sobre o ATA e transmite os dados por uma conexão HTTPS para os servidores da Microsoft.  Esses dados são usados pela Microsoft para ajudar a melhorar as versões futuras do ATA.

## <a name="data-collected"></a>Dados coletados
Os dados anônimos coletados incluem os seguintes parâmetros:

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


### <a name="disable-data-collection"></a>Desabilitar coleta de dados
Execute as etapas a seguir para interromper a coleta e o envio de dados de telemetria à Microsoft:

1.  Faça logon no Console do ATA, clique nos três pontos na barra de ferramentas e escolha **Sobre**.

2.  Desmarque a caixa para **Envie informações de uso para ajudar a melhorar a experiência do cliente no futuro**.

## <a name="see-also"></a>Consulte Também
- [Troubleshooting ATA using the event log](troubleshooting-ata-using-logs.md) (Solução de problemas do ATA usando o log de eventos)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
