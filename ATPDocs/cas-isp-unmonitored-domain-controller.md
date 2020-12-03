---
title: Avaliações de controladores de domínio não monitorados do Microsoft defender para identidade
description: Este artigo fornece uma visão geral do relatório de avaliação de postura de segurança de identidade de controladores de domínio não monitorados do Microsoft defender para identidade.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 86a1e02b84cf874f23fbf7b69d50c482cd15713b
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96544140"
---
# <a name="security-assessment-unmonitored-domain-controllers"></a>Avaliação de segurança: Controladores de domínio não monitorados

## <a name="what-are-unmonitored-domain-controllers"></a>O que são os controladores de domínio não monitorados?

Uma parte essencial da [!INCLUDE [Product long](includes/product-long.md)] solução requer que seus sensores sejam implantados em todos os controladores de domínio organizacionais, fornecendo uma visão abrangente para todas as atividades do usuário de cada dispositivo.

Por esse motivo, [!INCLUDE [Product short](includes/product-short.md)] o monitora continuamente o seu ambiente para identificar os controladores de domínio sem um [!INCLUDE [Product short](includes/product-short.md)] sensor instalado e emite relatórios sobre esses servidores não monitorados para ajudá-lo a gerenciar a cobertura completa do seu ambiente.

## <a name="what-risk-do-unmonitored-domain-controllers-pose-to-an-organization"></a>Que riscos os controladores de domínio não monitorados representam para uma organização?

Para operar com eficiência máxima, todos os controladores de domínio devem ser monitorados com [!INCLUDE [Product short](includes/product-short.md)] sensores. Organizações que não consigam corrigir controladores de domínio não monitorados têm uma visibilidade reduzida de seu ambiente, com o potencial de expor seus ativos a agentes mal-intencionados.

## <a name="how-do-i-use-this-security-assessment"></a>Como usar a avaliação de segurança?

1. Use a tabela do relatório para descobrir quais controladores de domínio não estão monitorados.
    ![Corrigir controladores de domínio não monitorados](media/cas-isp-unmonitored-domain-controller-1.png)
1. Realize a ação apropriada nesses controladores de domínio ao [instalar e configurar sensores de monitoramento](sensor-monitoring.md#domain-controller-status).

> [!NOTE]
> Essa avaliação é atualizada quase em tempo real.

## <a name="see-also"></a>Consulte Também

- [Monitorando a cobertura do controlador de domínio](sensor-monitoring.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
