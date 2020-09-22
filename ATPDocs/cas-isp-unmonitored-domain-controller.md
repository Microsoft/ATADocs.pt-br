---
title: Avaliações de controladores de domínio não monitorados da Proteção Avançada contra Ameaças do Azure
description: Este artigo apresenta uma visão geral do relatório de avaliação da situação da segurança de identidade de controladores de domínio não monitorados do ATP do Azure.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f3dfe585bb9b8bfd334d6481a830d9d1c2621fdb
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912776"
---
# <a name="security-assessment-unmonitored-domain-controllers"></a>Avaliação de segurança: Controladores de domínio não monitorados

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="what-are-unmonitored-domain-controllers"></a>O que são os controladores de domínio não monitorados?

Uma parte essencial da solução do ATP do Azure exige que os sensores sejam implantados em todos os controladores de domínio da organização, proporcionando uma visão abrangente de todas as atividades de usuários em cada dispositivo.

O ATP do Azure monitora continuamente seu ambiente para identificar os controladores de domínio sem um sensor instalado do ATP do Azure e relata esses servidores não monitorados para ajudar a gerenciar a cobertura completa do ambiente.

## <a name="what-risk-do-unmonitored-domain-controllers-pose-to-an-organization"></a>Que riscos os controladores de domínio não monitorados representam para uma organização?

Para operar com o máximo de eficiência, todos os controladores de domínio devem ser monitorados com sensores do ATP do Azure. Organizações que não consigam corrigir controladores de domínio não monitorados têm uma visibilidade reduzida de seu ambiente, com o potencial de expor seus ativos a agentes mal-intencionados.

## <a name="how-do-i-use-this-security-assessment"></a>Como usar a avaliação de segurança?

1. Use a tabela do relatório para descobrir quais controladores de domínio não estão monitorados.
    ![Corrigir controladores de domínio não monitorados](media/atp-cas-isp-unmonitored-domain-controller-1.png)
1. Realize a ação apropriada nesses controladores de domínio ao [instalar e configurar sensores de monitoramento](sensor-monitoring.md#domain-controller-status).

> [!NOTE]
> Essa avaliação é atualizada quase em tempo real.

## <a name="see-also"></a>Consulte Também

- [Monitorando a cobertura do controlador de domínio](sensor-monitoring.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
