---
title: Referência de ID de evento ATA | Microsoft Docs
description: Fornece uma lista de IDs de eventos ATA e as respectivas descrições.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 12/20/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 5d639e84-2e37-43a9-9667-49be6c4fa8b7
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: c89b37f3fda698af907cb4e74886e0b65e6df7e9
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90909415"
---
# <a name="ata-event-id-reference"></a>Referência de ID do evento ATA


[!INCLUDE [Banner for top of topics](includes/banner.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

O visualizador de eventos da Central do ATA registra eventos para o ATA. Este artigo fornece uma lista de IDs de eventos e fornece uma descrição de cada um deles.

Os eventos podem ser encontrados aqui:

![local da ID do evento](media/event-id-location.png)

## <a name="ata-health-events"></a>Eventos de integridade do ATA

|ID do evento|Nome do alerta|
|---------|---------------|
|1001|Centro com pouco espaço em disco|
|1003|Centro sobrecarregado|
|1004|Certificado do centro prestes a expirar/Certificado do centro expirado|
|1005|O MongoDB está inativo|
|1006|A senha de usuário somente leitura expirará em breve/A senha de usuário somente leitura expirou|
|1007|Sincronizador de domínio não atribuído|
|1008|Todos ou alguns dos adaptadores de rede de captura em um Gateway não estão disponíveis|
|1009|Um adaptador de rede de captura em um Gateway não existe mais|
|1010|Alguns controladores de domínio estão inacessíveis por um Gateway/Todos os controladores de domínio estão inacessíveis por um Gateway|
|1011|O Gateway parou de se comunicar|
|1012|Alguns eventos encaminhados não estão sendo analisados|
|1013|Parte do tráfego de rede não está sendo analisado|
|1014|Falha ao enviar email|
|1015|Falha ao conectar ao servidor SIEM usando Syslog|
|1016|Versão do Gateway desatualizada|
|1017|Nenhum tráfego recebido do controlador de domínio|
|1018|Falha ao iniciar o serviço de Gateway|
|1019|O Gateway Lightweight atingiu o limite de um recurso de memória|
|1020|O Gateway não está processando eventos do Radius|
|1021|O Gateway não está processando eventos do Syslog|
|1022|O serviço de geolocalização não está disponível|
 
## <a name="ata-security-alert-events"></a>Eventos do alerta de segurança ATA

|ID do evento|Nome do alerta|
|---------|---------------|
|2001|Suspeita de roubo de identidade com base no comportamento anormal|
|2002|Implementação de protocolo incomum|
|2003|Reconhecimento de enumeração de conta|
|2004|Ataque de força bruta usando associação simples LDAP|
|2006|Replicação mal-intencionada de serviços de diretório|
|2007|Reconhecimento usando DNS|
|2008|Atividade de downgrade de criptografia|
|2009|Atividade de downgrade de criptografia (possível ataque golden ticket)|
|2010|Atividade de downgrade de criptografia (possível ataque overpass-the-hash)|
|2011|Atividade de downgrade de criptografia (possível ataque de skeleton key)|
|2012|Reconhecimento usando a enumeração da sessão SMB|
|2013|Elevação de privilégios usando dados de autorização forjados|
|2014|Atividade de Honeytoken|
|2016|Exclusão de objeto grande|
|2017|Roubo de identidade usando o ataque de passagem de Hash|
|2018|Roubo de identidade usando o ataque Pass-the-Ticket|
|2019|Tentativa de execução remota detectada|
|2020|Solicitação mal-intencionada de informações privadas para proteção de dados|
|2021|Reconhecimento usando consultas de serviços de diretório|
|2022|Atividade Golden Ticket do Kerberos|
|2023|Falhas de autenticação suspeitas|
|2024|Modificação anormal de grupos confidenciais|
|2026|Criação de serviço suspeito|

## <a name="ata-auditing-events"></a>Eventos de auditoria de ATA

|ID do evento|Nome do alerta|
|---------|---------------|
|3001|Alteração à configuração do ATA|
|3002|Gateway do ATA adicionado|
|3003|Gateway do ATA excluído|
|3004|Licença ATA ativada|
|3005|Fazer logon no console do ATA|
|3006|Alteração manual ao status da atividade de integridade|
|3007|Alteração manual ao status da atividade suspeita|

## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Planejamento da capacidade do ATA](ata-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-collection.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
