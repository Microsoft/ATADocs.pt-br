---
title: Exportação e importação da Configuração do Advanced Threat Analytics | Microsoft Docs
description: Como exportar e importar a configuração de ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: edbf553bf48d984f4864264643d197362c3d6042
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2018
---
*Aplica-se a: Advanced Threat Analytics versão 1.9*



# <a name="export-and-import-the-ata-configuration"></a>Exportar e importar a configuração do ATA
A configuração do ATA é armazenada na coleção "SystemProfile" no banco de dados.
A cada hora, é feito o backup dessa coleção pelo serviço da Central do ATA para arquivos chamados: **SystemProfile_*timestamp*.json**. As 10 versões mais recentes são armazenadas.
Esse arquivo está localizado em uma subpasta chamada **Backup**. No local de instalação padrão do ATA, ele pode ser encontrado aqui: *C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_*timestamp*.json*. 

**Observação**: é recomendável fazer o backup desse arquivo sempre que você fizer alterações importantes no ATA.

É possível restaurar todas as configurações executando o seguinte comando:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Consulte Também
- [Arquitetura do ATA](ata-architecture.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

