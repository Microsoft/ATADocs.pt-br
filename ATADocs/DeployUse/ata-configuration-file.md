---
title: "Exportação e importação da Configuração do Advanced Threat Analytics | Microsoft Docs"
description: "Como exportar e importar a configuração de ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: 5ea29a5b64fd1f786200d3bbb62cd3964f8802e2


---

*Aplica-se a: Advanced Threat Analytics versão 1.7*



# <a name="export-and-import-the-ata-configuration"></a>Exportar e importar a configuração do ATA
A configuração do ATA é armazenada na coleção "SystemProfile" no banco de dados.
Essa coleção passa por backup a cada hora, realizado pelo serviço da Central do ATA para arquivos chamados: "SystemProfile_*carimbo de data e hora*.json". As 10 versões mais recentes são armazenadas.
Ele está localizado em uma subpasta chamada "Backup". No local de instalação padrão do ATA, ele pode ser encontrado aqui: *C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_*timestamp*.json*. 

**Observação**: é recomendável fazer o backup desse arquivo sempre que você fizer alterações importantes no ATA.

É possível restaurar todas as configurações executando o seguinte comando:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Consulte também
- [Arquitetura do ATA](/advanced-threat-analytics/plan-design/ata-architecture)
- [Pré-requisitos do ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Feb17_HO1-->


