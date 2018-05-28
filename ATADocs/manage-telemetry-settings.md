---
title: Gerenciar logs gerados pelo sistema do Advanced Threat Analytics | Microsoft Docs
description: Descreve os dados coletados pelo ATA e fornece etapas para desativar a coleta de dados.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7f1a0cb9a7e237259a9b77b96e16c6680336c2b0
ms.sourcegitcommit: 324dc941282f2948366afa5a919bda0b029bd59d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2018
---
*Aplica-se a: Advanced Threat Analytics versão 1.9*



# <a name="manage-system-generated-logs-note"></a>Gerenciar logs gerados pelo sistema[!NOTE]
> Se você tiver interesse em visualizar ou excluir dados pessoais, consulte as diretrizes da Microsoft no [Gerente de Conformidade da Microsoft](https://servicetrust.microsoft.com/ComplianceManager) e na [seção RGPD do site de Conformidade Corporativa do Microsoft 365 Enterprise](https://docs.microsoft.com/en-us/microsoft-365/compliance/gdpr). Se você estiver procurando informações gerais sobre o RGPD, confira a seção [RGPD do Portal de Confiança do Serviço](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).


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
