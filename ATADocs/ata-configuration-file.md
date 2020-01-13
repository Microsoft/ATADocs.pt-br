---
title: Exportação e importação da Configuração do Advanced Threat Analytics | Microsoft Docs
description: Como exportar e importar a configuração de ATA.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 9/04/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 522c4e197a52c6ccbd40d7ab1e8dea1764bce275
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2020
ms.locfileid: "75905416"
---
# <a name="export-and-import-the-ata-configuration"></a>Exportar e importar a configuração do ATA

*Aplica-se a: Advanced Threat Analytics versão 1.9*

A configuração do ATA é armazenada na coleção "SystemProfile" no banco de dados.
A cada hora, o backup dessa coleção é feito a cada quatro horas pelo serviço da Central do ATA para arquivos chamados: **SystemProfile_*carimbo_de_data/hora*.json**. As 300 versões mais recentes estão armazenadas.
Esse arquivo está localizado em uma subpasta chamada **backup**. No local de instalação padrão do ATA, ele pode ser encontrado aqui: <em>C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_</em>timestamp<em>.json</em>. 

**Observação**: é recomendável fazer o backup desse arquivo sempre que você fizer alterações importantes no ATA.

É possível restaurar todas as configurações executando o seguinte comando:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Confira Também
- [Arquitetura do ATA](ata-architecture.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

