---
# required metadata

title: Solução de problemas do ATA utilizando os logs do ATA | Microsoft Advanced Threat Analytics
description: Descreve como você pode usar os logs do ATA para solucionar problemas
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b8ad5511-8893-4d1d-81ee-b9a86e378347

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Solução de problemas do ATA usando os logs do ATA
Os logs do ATA fornecem informações sobre o que cada componente do ATA está fazendo a qualquer momento determinado

## Logs do Gateway do ATA
Os logs do Gateway do ATA estão localizados em uma subpasta chamada **Logs** . No local de instalação padrão, ela pode ser encontrada em: **C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Gateway\Logs**.

O Gateway do ATA tem os seguintes logs:

-   **Microsoft.Tri.Gateway.log** – Esse log contém tudo o que acontece no Gateway do ATA (inclusive resolução e erros).

    Uso principal: obter o status geral de todas as operações, em ordem cronológica de ocorrência.

-   **Microsoft.Tri.Gateway Resolution.log** – Esse log contém os detalhes da resolução das entidades vistas no tráfego pelo Gateway do ATA.

    Uso principal: investigar problemas de resolução de entidades.

-   **Microsoft.Tri.Gateway-Errors.log** – Esse log contém apenas os erros que são detectados pelo Gateway do ATA.

    Uso principal: executar verificações de integridade e investigar problemas que precisam estar correlacionados a horários específicos.

-   **Microsoft.Tri.Gateway-ExceptionStatistics.log** – Esse log agrupa todos os erros e exceções semelhantes e mede sua contagem.
    Esse arquivo começa vazio sempre que o serviço do Gateway do ATA é iniciado, e é atualizado a cada minuto.

    Uso principal: entender se há erros ou problemas com o Gateway do ATA, pois é mais fácil ler os erros agrupados e verificar se há um novo tipo de problema ou erro.

> [!NOTE]
> Os três primeiros arquivos de log têm um tamanho máximo de até 50 MB. Quando esse tamanho é atingido, um novo arquivo de log é aberto e o anterior é renomeada para "&lt;nome do arquivo&gt;- Arquivado- 00000" em que o número é incrementado a cada renomeação.

### Logs do Centro do ATA
Os logs do Centro do ATA estão localizados em uma subpasta chamada **Logs** . No local de instalação padrão, ela pode ser encontrada em: **C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\Logs**.

O Centro do ATA tem os seguintes logs:

-   **Microsoft.Tri.Center.log** – Esse log contém tudo o que acontece no Centro do ATA, inclusive detecções e erros.

    Uso principal: obter o status geral de todas as operações, em ordem cronológica de ocorrência.

-   **Microsoft.Tri.Center-Detection.log** – esse log contém apenas os detalhes de detecção do Centro do ATA.

    Uso principal: investigar problemas de detecção.

-   **Microsoft.Tri.Center-Errors.log** – Esse log contém apenas os erros que são detectados pelo Centro do ATA.

    Uso principal: executar verificações de integridade e investigar problemas que precisam estar correlacionados a horários específicos.

-   **Microsoft.Tri.Center-ExceptionStatistics.log** – Esse log agrupa todos os erros e exceções semelhantes e mede sua contagem.
    Esse arquivo começa vazio sempre que o serviço do Centro do ATA é iniciado, e é atualizado a cada minuto.

    Uso principal: entender se há erros ou problemas com o Centro do ATA, pois é mais fácil ler os erros agrupados e verificar se há um novo tipo de problema ou erro.

> [!NOTE]
> Os três primeiros arquivos de log têm um tamanho máximo de até 50 MB. Quando esse tamanho é atingido, um novo arquivo de log é aberto e o anterior é renomeada para "&lt;nome do arquivo&gt;- Arquivado- 00000" em que o número é incrementado a cada renomeação.

### Logs do Console do ATA
Os logs do Console ATA (os logs da API de gerenciamento) estão localizados em uma subpasta chamada **Logs** . No local de instalação padrão, ela pode ser encontrada em: **C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\Management\Logs**.

O Console do ATA tem os seguintes logs:

-   **w3wp.log** – Esse log contém tudo o que acontece no processo de gerenciamento (IIS).


-   **w3wp-Errors.log** – Esse log contém apenas os erros que são detectados pelo processo de gerenciamento (IIS).


-   **8e75f9f1-ExceptionStatistics.log** – Esse log contém todos os erros e exceções semelhantes, além de medir a contagem.
    Esse arquivo começa vazio sempre que o serviço do gateway é iniciado, e é atualizado a cada minuto.

    Uso principal: entender se há erros ou problemas com o Centro do ATA, pois é mais fácil ler os erros agrupados e verificar se há um novo tipo de problema ou erro.

> [!NOTE]
> Os dois primeiros arquivos de log tem um tamanho máximo de 50 MB. Quando esse tamanho é atingido, um novo arquivo de log é aberto e o anterior é renomeada para "&lt;nome do arquivo&gt;- Arquivado- 00000" em que o número é incrementado a cada renomeação.

### Logs de implantação do ATA
Os logs de implantação do ATA (instalação) estão localizados no diretório temp do usuário que instalou o produto. No local de instalação padrão, ele pode ser encontrado em: **C:\Usuários\Administrator\AppData\Local\Temp** (ou um diretório acima de %temp%).

Logs de implantação do Centro do Ata

-   **Microsoft Advanced Threat Analytics Center_20150601104213.log** - Esse log lista as etapas no processo de implantação do Centro do ATA.
Uso principal: acompanhar o processo de implantação do Centro do ATA.

-   **Microsoft Advanced Threat Analytics Center_20150601104213_0_MongoDBPackage.log** - Esse log lista as etapas no processo de implantação do MongoDB no Centro do ATA.
Uso principal: acompanhar o processo de implantação do MongoDB.

-   **Microsoft Advanced Threat Analytics Center_20150601104213_1_MsiPackage.log** - Esse log lista as etapas no processo de implantação dos binários do Centro do ATA.
Uso principal: acompanhar a implantação dos binários do Centro do ATA.

Logs de implantação do Gateway do ATA:

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801.log** - Esse log lista as etapas no processo de implantação do Gateway do ATA.
Uso principal: acompanhar o processo de implantação do Gateway do ATA.

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801_001_MsiPackage.log** - Esse log lista as etapas no processo de implantação dos binários do Gateway do ATA.
Uso principal: acompanhar a implantação dos binários do Gateway do ATA.


<!--HONumber=Apr16_HO2-->


