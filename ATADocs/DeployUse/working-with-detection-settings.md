---
title: "Definição das configurações de telemetria do Advanced Threat Analytics | Microsoft Docs"
description: "Descreve como configurar uma lista de endereços IP e sub-redes que tem circunstâncias incomuns e que deve ser tratada de forma diferente em relação a outras entidades em sua rede"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: f4f2ae30-4849-4a4f-8f6d-bfe99a32c746
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 831bafd08e0eea821fda94bd4f519d92ffec3397
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*Aplica-se a: Advanced Threat Analytics versão 1.7*



# <a name="working-with-ata-detection-settings"></a>Trabalhando com as configurações de detecção do ATA
A página de configuração **Detecção** permite que você configure uma lista de endereços IP e sub-redes que tem circunstâncias incomuns e que deve ser tratada de forma ligeiramente diferente em relação a outras entidades em sua rede.

## <a name="setting-up-detection"></a>Configuração da detecção
Na seção **Detecção**, defina os itens a seguir:

-   **SIDs da conta Honeytoken** – Esta é uma conta de usuário que não deve ter nenhuma atividade de rede. Essa conta será configurada como o usuário Honeytoken do ATA. Se alguém tentar usar esta conta de usuário, o ATA criará uma atividade suspeita e é uma indicação de atividade mal-intencionada. Para configurar o usuário Honeytoken, será necessário a SID da conta de usuário, não o nome de usuário.

>[!NOTE]
> Você pode encontrar o SID do usuário na guia *Informações da Conta* do perfil de usuário no Console do ATA.


![Honeytoken de configurações de detecção do ATA](media/ata-detection-settings-honeytoken-1.7.png)


**Exclusões de detecção** - Você pode excluir endereços IP das seguintes detecções. Se você inserir um endereço IP em uma dessas listas, o ATA excluirá esse endereço IP deste tipo específico de atividade detectada.

-   Exclusões de endereço IP de reconhecimento de DNS

-   Exclusões de endereço IP de passagem de tíquete

![Exclusões de configurações de detecção do ATA](media/ata-detection-settings-exclusions-1.7.png)


## <a name="see-also"></a>Consulte Também
- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Modificando a configuração do ATA](modifying-ata-configuration.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
