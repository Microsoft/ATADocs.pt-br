---
title: Avaliações de controladores de domínio não monitorados da Proteção Avançada contra Ameaças do Azure
description: Este artigo apresenta uma visão geral do relatório de avaliação da situação da segurança de identidade de controladores de domínio não monitorados do ATP do Azure.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 02/17/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b82aa4af317b1eb913794f164449716180842c3c
ms.sourcegitcommit: 63be53de5b84eabdeb8c006438dab45bd35a4ab7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2020
ms.locfileid: "77478812"
---
# <a name="security-assessment-unmonitored-domain-controllers"></a>Avaliação de segurança: Controladores de domínio não monitorados

## <a name="what-are-unmonitored-domain-controllers"></a>O que são os controladores de domínio não monitorados?

Uma parte essencial da solução do ATP do Azure exige que os sensores sejam implantados em todos os controladores de domínio da organização, proporcionando uma visão abrangente de todas as atividades de usuários em cada dispositivo.

O ATP do Azure monitora continuamente seu ambiente para identificar os controladores de domínio sem um sensor instalado do ATP do Azure e relata esses servidores não monitorados para ajudar a gerenciar a cobertura completa do ambiente.

## <a name="what-risk-do-unmonitored-domain-controllers-pose-to-an-organization"></a>Que riscos os controladores de domínio não monitorados representam para uma organização?

Para operar com o máximo de eficiência, todos os controladores de domínio devem ser monitorados com sensores do ATP do Azure. Organizações que não consigam corrigir controladores de domínio não monitorados têm uma visibilidade reduzida de seu ambiente, com o potencial de expor seus ativos a agentes mal-intencionados.

## <a name="how-do-i-use-this-security-assessment"></a>Como usar a avaliação de segurança?

1. Use a tabela do relatório para descobrir quais controladores de domínio não estão monitorados.
    ![Corrigir controladores de domínio não monitorados](media/atp-cas-isp-unmonitored-domain-controller-1.png)
1. Realize a ação apropriada nesses controladores de domínio ao [instalar e configurar sensores de monitoramento](atp-sensor-monitoring.md#domain-controller-status).

## <a name="see-also"></a>Consulte Também

- [Monitorar a cobertura do controlador de domínio](atp-sensor-monitoring.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
