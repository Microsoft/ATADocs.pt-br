---
title: Gerenciamento do banco de dados do ATA | Microsoft ATA
description: "Procedimentos para ajudá-lo a mover, fazer backup ou restaurar o banco de dados do ATA."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5cd030f3b952d08c6617a6cda121c344a9c36f51
ms.openlocfilehash: b4e68e9e8dbd94075a34a8e3e8f42d4f534caf50


---

*Aplica-se a: Advanced Threat Analytics versão 1.7*



# Gerenciamento do Banco de Dados de ATA
Se você precisar mover, fazer backup ou restaurar o banco de dados do ATA, use estes procedimentos para trabalhar com o MongoDB.

## Fazendo backup do banco de dados de ATA
Consulte a [documentação relevante do MongoDB](http://docs.mongodb.org/manual/administration/backup/).

## Restaurando o banco de dados do ATA
Consulte a [documentação relevante do MongoDB](http://docs.mongodb.org/manual/administration/backup/).

## Movendo o banco de dados do ATA para outra unidade

1.  Pare o serviço **Centro do Microsoft Advanced Threat Analytics**.

2.  Pare o serviço **MongoDB**.

3.  Abra o arquivo de configuração Mongo localizado, por padrão, em C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg.

    Localize o parâmetro `storage: dbPath`

4.  Mova a pasta listada no parâmetro `dbPath` para o novo local.

5.  Altere o parâmetro `dbPath` dentro do arquivo de configuração mongo para o novo caminho de pasta, salve e feche o arquivo.

    ![Imagem ao modificar a configuração do MongoDB](media/ATA-mongoDB-moveDB.png)

6.  Inicie o serviço **MongoDB**.

7. Inicie o serviço **Centro do Microsoft Advanced Threat Analytics**.

## Arquivo de configuração do ATA
A configuração do ATA é armazenada na coleção "SystemProfile" no banco de dados.
Essa coleção passa por backup a cada hora, realizado pelo serviço da Central do ATA para arquivos chamados: "SystemProfile_*carimbo de data e hora*.json". As 10 versões mais recentes são armazenadas.
Ele está localizado em uma subpasta chamada "Backup". No local de instalação padrão do ATA, ele pode ser encontrado aqui: *C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_*timestamp*.json*. 

**Observação**: é recomendável fazer o backup desse arquivo sempre que você fizer alterações importantes no ATA.

É possível restaurar todas as configurações executando o seguinte comando:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## Consulte Também
- [Arquitetura do ATA](/advanced-threat-analytics/plan-design/ata-architecture)
- [Pré-requisitos do ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Aug16_HO5-->


