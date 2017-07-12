---
title: "Exportação e importação da Configuração do Advanced Threat Analytics | Microsoft Docs"
description: "Como exportar e importar a configuração de ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/13/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: a04378838fab20c43df159ef3259530b8a599ed4
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*



<a id="export-and-import-the-ata-configuration" class="xliff"></a>

# Exportar e importar a configuração do ATA
A configuração do ATA é armazenada na coleção "SystemProfile" no banco de dados.
Essa coleção passa por backup a cada hora, realizado pelo serviço da Central do ATA para arquivos chamados: "SystemProfile_*carimbo de data e hora*.json". As 10 versões mais recentes são armazenadas.
Ele está localizado em uma subpasta chamada "Backup". No local de instalação padrão do ATA, ele pode ser encontrado aqui: *C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_*timestamp*.json*. 

**Observação**: é recomendável fazer o backup desse arquivo sempre que você fizer alterações importantes no ATA.

É possível restaurar todas as configurações executando o seguinte comando:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

<a id="see-also" class="xliff"></a>

## Consulte também
- [Arquitetura do ATA](ata-architecture.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

