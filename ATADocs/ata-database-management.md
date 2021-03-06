---
title: Gerenciamento de banco de dados do Advanced Threat Analytics
description: Procedimentos para ajudá-lo a mover, fazer backup ou restaurar o banco de dados do ATA.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 05e49e23-6e0a-4ec0-9a63-a2093173c8a1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f6f39619aa3ba960384b646f2b4237118cabf725
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94691070"
---
# <a name="ata-database-management"></a>Gerenciamento do Banco de Dados de ATA

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Se você precisar mover, fazer backup ou restaurar o banco de dados do ATA, use estes procedimentos para trabalhar com o MongoDB.

## <a name="backing-up-the-ata-database"></a>Fazendo backup do banco de dados de ATA
Consulte a [documentação relevante do MongoDB](http://docs.mongodb.org/manual/administration/backup/).

## <a name="restoring-the-ata-database"></a>Restaurando o banco de dados do ATA
Consulte a [documentação relevante do MongoDB](http://docs.mongodb.org/manual/administration/backup/).

## <a name="moving-the-ata-database-to-another-drive"></a>Movendo o banco de dados do ATA para outra unidade

1. Pare o serviço **Centro do Microsoft Advanced Threat Analytics**.
   > [!Important] 
   > Verifique se o serviço do Centro do ATA foi interrompido antes de passar para a próxima etapa.

1. Pare o serviço **MongoDB**.

1. Abra o arquivo de configuração Mongo localizado, por padrão, em C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg.

   Localize o parâmetro `storage: dbPath`

1. Mova a pasta listada no parâmetro `dbPath` para o novo local.

1. Altere o parâmetro `dbPath` dentro do arquivo de configuração mongo para o novo caminho de pasta, salve e feche o arquivo.

    ![Imagem ao modificar a configuração do MongoDB](media/ATA-mongoDB-moveDB.png)

1. Inicie o serviço **MongoDB** .

1. Inicie o serviço **Centro do Microsoft Advanced Threat Analytics**.

## <a name="see-also"></a>Consulte Também
- [Arquitetura do ATA](ata-architecture.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

