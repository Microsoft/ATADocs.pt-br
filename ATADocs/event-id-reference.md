---
title: Referência de ID de evento ATA | Microsoft Docs
description: Fornece uma lista de IDs de eventos ATA e as respectivas descrições.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 5d639e84-2e37-43a9-9667-49be6c4fa8b7
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 38610c6b8f94dbe1a31e218e064750bf2bde2c49
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133133"
---
*Aplica-se a: Advanced Threat Analytics versão 1.9*


# <a name="ata-event-id-reference"></a>Referência de ID do evento ATA

O visualizador de eventos da Central do ATA registra eventos para o ATA. Este artigo fornece uma lista de IDs de eventos e fornece uma descrição de cada um deles.

Os eventos podem ser encontrados aqui:

![local da ID do evento](./media/event-id-location.png)

## <a name="ata-health-events"></a>Eventos de integridade do ATA

1001 – Alerta de integridade de espaço livre da unidade de dados de banco de dados da Central do ATA 

1003 – Alerta de integridade de Central do ATA sobrecarregada 

1004 – Alerta de integridade de expiração do certificado 

1005 – Alerta de integridade de banco de dados da Central desconectado 

1006 – Alerta de integridade de expiração de senha da conta de cliente dos serviços de diretório do Gateway do ATA 

1007 – Alerta de integridade de sincronizador de domínio do Gateway do ATA não atribuído 

1008 – Alerta de integridade de adaptador de rede de captura do Gateway do ATA com falha 

1009 – Alerta de integridade de adaptador de rede de captura do Gateway do ATA ausente 

1010 – Alerta de integridade de conectividade de cliente dos serviços de diretório do Gateway do ATA 

1011 – Alerta de integridade de Gateway do ATA desconectado 

1012 – Alerta de integridade de atividades de evento do Gateway do ATA sobrecarregadas 

1013 – Alerta de integridade de atividades de rede do Gateway do ATA sobrecarregadas 

1014 – Alerta de integridade de email da Central 

1015 – Alerta de integridade de Syslog da Central 

1016 – Alerta de integridade de Gateways do ATA desatualizados 

1017 – Alerta de integridade de Central não recebendo tráfego 

1018 – Alerta de integridade de falha ao iniciar o Gateway do ATA 

1019 – Alerta de integridade de memória insuficiente no Gateway do ATA 

1020 – alerta de integridade de ouvinte de evento de RADIUS do Gateway do ATA 

1021 – Alerta de integridade de ouvinte de evento de Syslog do Gateway do ATA 

1022 – Alerta de integridade de falha na resolução de endereço IP externo da Central do ATA 
 
## <a name="ata-suspicious-activity-events"></a>Eventos de atividade suspeita do ATA

2001 – Atividade suspeita de comportamento anormal 

2002 – Atividade suspeita de protocolo anormal 

2003 – Atividade suspeita de enumeração de conta 

2004 – Atividade suspeita de força bruta de LDAP 

2006 – Atividade suspeita de replicação de serviços de diretório 

2007 – Atividade suspeita de reconhecimento de DNS 

2008 – Atividade suspeita de downgrade de criptografia 

2012 – Atividade suspeita na enumeração de sessões 

2013 – Atividade suspeita de PAC forjado 

2014 – Atividade suspeita de atividade de Honeytoken 

2016 – Atividade suspeita de exclusão de objeto grande 

2017 – Atividade suspeita de passagem de hash 

2018 – Atividade suspeita de passagem de tíquete 

2019 – Atividade suspeita de execução remota 

2020 – Atividade suspeita de recuperação de chave de backup de proteção de dados 

2021 – Atividade suspeita de reconhecimento de SAMR 

2022 – Atividade suspeita de golden ticket 

2023 – Atividade suspeita de força bruta 

2024 – Atividade suspeita de alteração de associação de grupo confidencial anormal  

## <a name="ata-auditing-events"></a>Eventos de auditoria de ATA

3001 – Alteração à configuração do ATA 

3002 – Gateway do ATA adicionado

3003 – Gateway do ATA excluído

3004 – Licença ATA ativada

3005 – Fazer logon no console do ATA

3006 – Alteração manual ao status da atividade de integridade 

3007 – Alteração manual ao status da atividade suspeita 


## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Planejamento da capacidade do ATA](ata-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
