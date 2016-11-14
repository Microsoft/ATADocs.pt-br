---
title: "Arquivo de configuração do ATA | Microsoft ATA"
description: "Fazendo backup da configuração do ATA."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 10/31/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f334f9c8440e4bb0202579de220f6530d0aabad8
ms.openlocfilehash: 542bdf983e26fa98c036de55860b482d0b1d734d


---

*Aplica-se a: Advanced Threat Analytics versão 1.7*



# <a name="ata-configuration-file"></a>Arquivo de configuração do ATA
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




<!--HONumber=Oct16_HO5-->


