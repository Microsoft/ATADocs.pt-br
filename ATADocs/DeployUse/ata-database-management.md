---
title: Gerenciamento do Banco de Dados do Advanced Threat Analytics | Microsoft Docs
description: "Procedimentos para ajudá-lo a mover, fazer backup ou restaurar o banco de dados do ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 05e49e23-6e0a-4ec0-9a63-a2093173c8a1
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: 95ac5a45fb69e8b23c60ec95e285a8f8d361853c


---

*Aplica-se a: Advanced Threat Analytics versão 1.7*



# <a name="ata-database-management"></a>Gerenciamento do Banco de Dados de ATA
Se você precisar mover, fazer backup ou restaurar o banco de dados do ATA, use estes procedimentos para trabalhar com o MongoDB.

## <a name="backing-up-the-ata-database"></a>Fazendo backup do banco de dados de ATA
Consulte a [documentação relevante do MongoDB](http://docs.mongodb.org/manual/administration/backup/).

## <a name="restoring-the-ata-database"></a>Restaurando o banco de dados do ATA
Consulte a [documentação relevante do MongoDB](http://docs.mongodb.org/manual/administration/backup/).

## <a name="moving-the-ata-database-to-another-drive"></a>Movendo o banco de dados do ATA para outra unidade

1.  Pare o serviço **Centro do Microsoft Advanced Threat Analytics**.
> [!Important] 
> Verifique se o serviço do Centro do ATA foi interrompido antes de passar para a próxima etapa.

2.  Pare o serviço **MongoDB**.

3.  Abra o arquivo de configuração Mongo localizado, por padrão, em C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg.

    Localize o parâmetro `storage: dbPath`

4.  Mova a pasta listada no parâmetro `dbPath` para o novo local.

5.  Altere o parâmetro `dbPath` dentro do arquivo de configuração mongo para o novo caminho de pasta, salve e feche o arquivo.

    ![Imagem ao modificar a configuração do MongoDB](media/ATA-mongoDB-moveDB.png)

6.  Inicie o serviço **MongoDB**.

7. Inicie o serviço **Centro do Microsoft Advanced Threat Analytics**.

## <a name="see-also"></a>Consulte Também
- [Arquitetura do ATA](/advanced-threat-analytics/plan-design/ata-architecture)
- [Pré-requisitos do ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Feb17_HO1-->


