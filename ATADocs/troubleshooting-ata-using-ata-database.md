---
title: Solução de problemas da análise avançada de ameaças usando o banco de dados
description: Descreve como você pode usar o banco de dados do ATA para solucionar problemas
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 377a3c81-5c1d-486f-8942-85249aacf560
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1efc5aee15527212a6f2eb53c147fe8fa1d62ea3
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2020
ms.locfileid: "79414209"
---
# <a name="troubleshooting-ata-using-the-ata-database"></a>Solução de problemas do ATA usando o banco de dados do ATA

*Aplica-se a: Advanced Threat Analytics versão 1.9*

O ATA usa o MongoDB como seu banco de dados.
Você pode interagir com o banco de dados usando a linha de comando padrão ou usando uma ferramenta de interface de usuário para executar tarefas avançadas e solucionar problemas.

## <a name="interacting-with-the-database"></a>Interação com o banco de dados
O modo padrão, e mais básico, de consultar o banco de dados é usando o shell Mongo:

1.  Abra uma janela de linha de comando e altere o caminho até a pasta bin do MongoDB. O caminho padrão é: **C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**.

2.  Execute: `mongo.exe ATA`. Digite ATA com letras maiúsculas.

> [!div class="mx-tableFixed"]
> 
> |Como...|Sintaxe|Anotações|
> |-------------|----------|---------|
> |Verifique se há coleções no banco de dados.|`show collections`|É útil como um teste completo para verificar se o tráfego está sendo gravado no banco de dados, e se o evento 4776 está sendo recebido pelo ATA.|
> |Obter detalhes de um usuário/computador/grupo (UniqueEntity), como ID do usuário.|`db.UniqueEntity.find({CompleteSearchNames: "<name of entity in lower case>"})`||
> |Encontre o tráfego de autenticação Kerberos proveniente de um computador específico em um dia específico.|`db.KerberosAs_<datetime>.find({SourceComputerId: "<Id of the source computer>"})`|Para obter a &lt;ID do computador de origem&gt;, consulte as coleções UniqueEntity, conforme mostrado no exemplo.<br /><br />Cada tipo de atividade de rede, por exemplo, autenticações Kerberos, possui sua própria coleção de acordo com a data UTC.|
> |Faça alterações de configuração avançadas. Neste exemplo, altere o tamanho da fila de envio de todos os Gateways do ATA para 10.000.|`db.SystemProfile.update( {_t: "GatewaySystemProfile"} ,`<br>`{$set:{"Configuration.EntitySenderConfiguration.EntityBatchBlockMaxSize" : "10000"}})`|`|

O exemplo a seguir fornece um código de exemplo usando a sintaxe fornecida anteriormente. Se você estiver investigando uma atividade suspeita que ocorreu em 20/10/2015 e quiser saber mais sobre as atividades de NTLM que "John Doe" realizou nesse dia:<br /><br />Primeiro, encontre a ID de "John Doe"

`db.UniqueEntity.find({Name: "John Doe"})`<br>Anote a ID conforme indicado pelo valor de `_id` Por exemplo, digamos que a ID seja `123bdd24-b269-h6e1-9c72-7737as875351`<br>Depois, pesquise pela coleção com a data mais próxima e anterior à data que você está procurando, no exemplo, 20/10/2015.<br>Em seguida, procure por atividades de NTLM na conta de John Doe: 

`db.Ntlms_<closest date>.find({SourceAccountId: "123bdd24-b269-h6e1-9c72-7737as875351"})`

## <a name="see-also"></a>Confira Também
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Planejamento da capacidade do ATA](ata-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-collection.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
