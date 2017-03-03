---
title: "Gerenciamento das configurações de telemetria do Advanced Threat Analytics | Microsoft Docs"
description: Descreve os dados coletados pelo ATA e fornece etapas para desativar a coleta de dados.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: 1b6da432e81bc42b772b2146213d2f24bee6231a


---

*Aplica-se a: Advanced Threat Analytics versão 1.7*



# <a name="manage-telemetry-settings"></a>Gerenciamento das configurações de telemetria
O ATA (Advanced Threat Analytics) coleta dados de telemetria anônimos sobre o ATA e os transmite por uma conexão HTTPS para os servidores Microsoft.  Esses dados são usados pela Microsoft para ajudar a melhorar as versões futuras do ATA.

## <a name="data-collected"></a>Dados coletados
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


### <a name="disable-data-collection"></a>Desabilitar coleta de dados
Execute as etapas a seguir para interromper a coleta e o envio de dados de telemetria à Microsoft:

1.  Faça logon no Console do ATA, clique nos três pontos na barra de ferramentas e escolha **Sobre**.

2.  Desmarque a caixa para **Envie informações de uso para ajudar a melhorar a experiência do cliente no futuro**.

## <a name="see-also"></a>Consulte também
- [Novidades na versão 1.6](/advanced-threat-analytics/understand-explore/whats-new-version-1.6)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Feb17_HO1-->


