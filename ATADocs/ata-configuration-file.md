---
title: Exportação e importação da Configuração do Advanced Threat Analytics | Microsoft Docs
description: Como exportar e importar a configuração de ATA.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 9/04/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: cc62b556cc27e363a0d37260d80fda4a7bfdd105
ms.sourcegitcommit: 62b631f64a639f5df04bf805755f26c69b40e8e4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638789"
---
# <a name="export-and-import-the-ata-configuration"></a>Exportar e importar a configuração do ATA

*Aplica-se a: Advanced Threat Analytics versão 1.9*

A configuração do ATA é armazenada na coleção "SystemProfile" no banco de dados.
o backup dessa coleta é feito a cada quatro horas pelo serviço do ATA Center para arquivos chamados: **SystemProfile_*timestamp*.json**. As 300 versões mais recentes estão armazenadas.
Esse arquivo está localizado em uma subpasta chamada **Backup**. O local de instalação padrão do ATA está em:  <em>C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_</em>timestamp<em>.json</em>. 

**Observação**: Recomendamos o backup deste arquivo sempre que você fizer alterações importantes no ATA.

É possível restaurar todas as configurações executando o seguinte comando:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Consulte Também
- [Arquitetura do ATA](ata-architecture.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

