---
title: Configurar exclusões de detecção e contas honeytoken da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Configuração de exclusões de detecção e contas de usuário honeytoken.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 10/22/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1ad5e923-9bbd-4f56-839a-b11a9f387d4b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4035fbbb3a705cff541c5e07d6bbdce72d99d119
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2020
ms.locfileid: "75905188"
---
# <a name="configure-detection-exclusions-and-honeytoken-accounts"></a>Configurar exclusões de detecção e contas de honeytoken

O Azure ATP permite que endereços IP ou usuários específicos sejam excluídos de várias detecções. 

Por exemplo, uma **exclusão por Reconhecimento de DNS** poderia ser um verificador de segurança que usa o DNS como um mecanismo de verificação. A exclusão ajuda o Azure ATP a ignorar esses verificadores.  

O Azure ATP também permite a configuração de contas de honeytoken, usadas como interceptações de ações mal-intencionadas. Qualquer autenticação associada a essas contas de honeytoken (normalmente inativas) dispara um alerta.

Para configurar, execute estas etapas:

1.  No portal do Azure ATP, clique no ícone de configurações e selecione **Configuração**.

    ![Definições de configuração do Azure ATP](media/atp-config-menu.png)

2.  Em **Detecção**, clique em **Marcas de entidade**.

3. Em **Contas de honeytoken**, insira o nome da conta de honeytoken e clique no sinal **+** . O campo de contas Honeytoken é pesquisável e exibe automaticamente entidades em sua rede. Clique em **Salvar**.

   ![Honeytoken](media/honeytoken-sensitive.png)

4. Clique em **Exclusões**. Insira uma conta de usuário ou endereço IP a ser excluído da detecção, para cada tipo de ameaça. 
5. Clique no sinal *mais*. O campo **Adicionar entidade** (usuário ou computador) é pesquisável e será preenchido automaticamente com entidades na sua rede. Para obter mais informações, confira [Excluindo entidades das detecções](excluding-entities-from-detections.md) e o [Guia de alerta de segurança](suspicious-activity-guide.md).

   ![Exclusões](media/exclusions.png)

6.  Clique em **Salvar**.


Parabéns, você implantou a Proteção Avançada contra Ameaças do Azure!

Verifique a linha do tempo de ataque para visualizar os alertas de segurança gerados das atividades detectadas e procure os usuários ou computadores exibindo os perfis deles.

A verificação do ATP do Azure é iniciada imediatamente. Algumas detecções, como [Adições suspeitas a grupos confidenciais](atp-domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024), requerem um período de aprendizado e não estão disponíveis imediatamente após a implantação do ATP do Azure. Esse período para cada alerta aparece em detalhes no [guia de alerta de segurança](suspicious-activity-guide.md). 


## <a name="see-also"></a>Consulte Também
- [Ferramenta de dimensionamento do Azure ATP](https://aka.ms/aatpsizingtool)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
