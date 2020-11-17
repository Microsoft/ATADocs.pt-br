---
title: Exportar e importar a configuração do Advanced Threat Analytics
description: Como exportar e importar a configuração de ATA.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 9/04/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3d596b1833db7221027295014e114a07b45f2f6f
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94691087"
---
# <a name="export-and-import-the-ata-configuration"></a>Exportar e importar a configuração do ATA

[!INCLUDE [Banner for top of topics](includes/banner.md)]

A configuração do ATA é armazenada na coleção "SystemProfile" no banco de dados.
A cada hora, o backup dessa coleção é feito a cada quatro horas pelo serviço da Central do ATA para arquivos chamados: **SystemProfile_ *carimbo_de_data/hora*.json**. As 300 versões mais recentes estão armazenadas.
Esse arquivo está localizado em uma subpasta chamada **Backup**. No local de instalação padrão do ATA, ele pode ser encontrado aqui: <em>C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_</em>timestamp<em>.json</em>. 

**Observação**: é recomendável fazer o backup desse arquivo sempre que você fizer alterações importantes no ATA.

É possível restaurar todas as configurações executando o seguinte comando:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Consulte Também
- [Arquitetura do ATA](ata-architecture.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

