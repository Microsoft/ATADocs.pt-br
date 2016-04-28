---
# required metadata

title: Gerenciamento das configurações de telemetria | Microsoft Advanced Threat Analytics
description: Descreve os dados coletados pelo ATA e fornece etapas para desativar a coleta de dados.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Gerenciamento das configurações de telemetria
O ATA (Advanced Threat Analytics) coleta dados de telemetria anônimas sobre o ATA e os transmite por uma conexão HTTPS para os servidores Microsoft.  Esses dados são usados pela Microsoft para ajudar a melhorar as versões futuras do ATA.

## Dados coletados
Entre os dados coletados estão os seguintes:

-   Contadores de desempenho do Centro do ATA... e do Gateway do ATA

-   ID do produto após o licenciamento do ATA

-   Data da implantação do Centro do ATA

-   Número de Gateways do ATA implantados

-   As seguintes informações do Active Directory:

    -   ID de Domínio do domínio cujo nome seria o primeiro domínio quando classificado em ordem alfabética

    -   Número de controladores de domínio

    -   Número de controladores de domínio monitorados pelo ATA por meio do espelhamento de porta

    -   Número de sites

    -   Número de computadores

    -   Número de grupos

    -   Número de usuários

-   Atividades suspeitas – os dados a seguir são coletados para cada atividade suspeita:

    (Os nomes de computador, nomes de usuário e endereços IP **não** são coletados)

    -   Tipo de atividade suspeita

    -   ID da atividade suspeita

    -   Status

    -   Horas de início e de término

    -   Entrada fornecida

### Desabilitar coleta de dados
Para deixar de coletar e enviar dados de telemetria à Microsoft, execute estas etapas.

1.  Faça logon no Console do ATA, clique nos três pontos na barra de ferramentas e escolha **Sobre**.

2.  Desmarque a caixa para **Envie informações de uso para ajudar a melhorar a experiência do cliente no futuro**.

## Consulte também
- [Novidades na versão 1.5](whats-new-version-1.5.md)
- [Novidades na versão 1.4](whats-new-version-1.4.md)
- [Para obter suporte, confira nosso fórum!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


