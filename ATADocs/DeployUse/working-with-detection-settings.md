---
# required metadata

title: Trabalhando com as configurações de detecção do ATA | Microsoft Advanced Threat Analytics
description: Descreve como configurar uma lista de endereços IP e sub-redes que tem circunstâncias incomuns e que deve ser tratada de forma diferente em relação a outras entidades em sua rede
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: f4f2ae30-4849-4a4f-8f6d-bfe99a32c746

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Trabalhando com as configurações de detecção do ATA
A página de configuração **Detecção** permite que você configure uma lista de endereços IP e sub-redes que tem circunstâncias incomuns e que deve ser tratada de forma ligeiramente diferente em relação a outras entidades em sua rede.

## Configuração da detecção
Na página **Detecção** você pode definir os seguintes itens:

-   **Sub-redes de concessão a curto prazo** – Se a sua organização tiver qualquer sub-rede com endereço IP de prazo muito curto, por exemplo, sub-redes de endereço IP de VPN ou sub-redes de Wi-Fi, é importante inserir esses endereços IP e sub-redes no ATA para que ele saiba armazenar a associação entre um computador e um endereço IP a partir desses intervalos por um período mais curto de tempo do que o de outros endereços IP.

-   **SIDs da conta Honeytoken** – Esta é uma conta de usuário que não deve ter nenhuma atividade de rede. Essa conta será configurada como o usuário Honeytoken do ATA. Se alguém tentar usar esta conta de usuário, o ATA criará uma atividade suspeita e é uma indicação de atividade mal-intencionada. Para configurar o usuário Honeytoken, será necessário a SID da conta de usuário, não o nome de usuário.

Você pode excluir endereços IP das seguintes detecções. Se você inserir um endereço IP em uma dessas listas, o ATA excluirá esse endereço IP deste tipo específico de atividade detectada.

-   Exclusões de endereço IP de reconhecimento de DNS

-   Exclusões de endereço IP de passagem de tíquete

## Consulte também
- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Modificando a configuração do ATA](modifying-ata-configuration.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


