---
title: Gerenciamento do banco de dados do ATA | Microsoft ATA
description: "Procedimentos para ajudá-lo a mover, fazer backup ou restaurar o banco de dados do ATA."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 115ec28877665c79e5cbcd557528da156c8d7149
ms.openlocfilehash: fd00623f9be396b3a2c384cce436996b5093cc3f


---

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

7.  Abra um prompt de comando e execute o shell Mongo executando `mongo.exe ATA`.

    Por padrão, o mongo.exe está localizado em C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\MongoDB\bin

8.  Execute o seguinte comando: `db.SystemProfiles.update( {_t: "CenterSystemProfile"} , {$set:{"Configuration.CenterDatabaseClientConfiguration.DataPath" : "<New DB Location>"}})`

   Em vez de <New DB Location>, em que `&lt;New DB Location&gt;` é o novo caminho da pasta.

9.  Atualize HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center\DatabaseDataPath com o novo caminho de pasta.

9. Inicie o serviço **Centro do Microsoft Advanced Threat Analytics**.

## Consulte também
- [Arquitetura do ATA](/advanced-threat-analytics/plan-design/ata-architecture)
- [Pré-requisitos do ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Jul16_HO3-->


