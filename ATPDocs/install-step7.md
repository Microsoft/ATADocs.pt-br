---
title: Configurar exclusões de detecção e contas honeytoken da Proteção Avançada contra Ameaças do Azure
description: Configuração de exclusões de detecção e contas de usuário honeytoken.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/22/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1ad5e923-9bbd-4f56-839a-b11a9f387d4b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fa4f487c2b5a60f1bb8900ae36aef2d34a5193f3
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90827989"
---
# <a name="configure-detection-exclusions-and-honeytoken-accounts"></a>Configurar exclusões de detecção e contas de honeytoken

O Azure ATP permite que endereços IP ou usuários específicos sejam excluídos de várias detecções.

Por exemplo, uma **exclusão por Reconhecimento de DNS** poderia ser um verificador de segurança que usa o DNS como um mecanismo de verificação. A exclusão ajuda o Azure ATP a ignorar esses verificadores.

O Azure ATP também permite a configuração de contas de honeytoken, usadas como interceptações de ações mal-intencionadas. Qualquer autenticação associada a essas contas de honeytoken (normalmente inativas) dispara um alerta.

Para configurar, execute estas etapas:

1. No portal do Azure ATP, clique no ícone de configurações e selecione **Configuração**.

    ![Definições de configuração do Azure ATP](media/atp-config-menu.png)

1. Em **Detecção**, clique em **Marcas de entidade**.

1. Em **Contas de honeytoken**, insira o nome da conta de honeytoken e clique no sinal **+** . O campo de contas Honeytoken é pesquisável e exibe automaticamente entidades em sua rede. Clique em **Salvar**.

    ![Honeytoken](media/honeytoken-sensitive.png)

1. Clique em **Exclusões**. Insira uma conta de usuário ou endereço IP a ser excluído da detecção, para cada tipo de ameaça.
1. Clique no sinal *mais*. O campo **Adicionar entidade** (usuário ou computador) é pesquisável e será preenchido automaticamente com entidades na sua rede. Para obter mais informações, confira [Excluindo entidades das detecções](excluding-entities-from-detections.md) e o [Guia de alerta de segurança](suspicious-activity-guide.md).

    ![Excluindo entidades de detecções](media/exclusions.png)

1. Clique em **Salvar**.

Parabéns, você implantou a Proteção Avançada contra Ameaças do Azure!

Verifique a linha do tempo de ataque para visualizar os alertas de segurança gerados das atividades detectadas e procure os usuários ou computadores exibindo os perfis deles.

A verificação do ATP do Azure é iniciada imediatamente. Algumas detecções, como [Adições suspeitas a grupos confidenciais](domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024), requerem um período de aprendizado e não estão disponíveis imediatamente após a implantação do ATP do Azure. Esse período para cada alerta aparece em detalhes no [guia de alerta de segurança](suspicious-activity-guide.md).

## <a name="see-also"></a>Confira Também

- [Ferramenta de dimensionamento do Azure ATP](https://aka.ms/aatpsizingtool)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do Azure ATP](prerequisites.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
