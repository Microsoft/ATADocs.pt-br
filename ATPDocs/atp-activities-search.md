---
title: Filtro e Pesquisa de Atividades Monitoradas da Proteção Avançada contra Ameaças do Azure
description: Este artigo fornece uma visão geral de como filtrar e pesquisar atividades monitoradas usando o ATP do Azure.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/15/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: a546703b-d5a9-404d-9e87-125523bb8421
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c6766319861a766ba970ef0ed3d23d1f20c0f34d
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2020
ms.locfileid: "84774461"
---
# <a name="azure-atp-monitored-activities-search-and-filter"></a>Pesquisa e filtragem de atividades monitoradas do ATP do Azure 

> [!NOTE]
> Os recursos do ATP do Azure explicados nesta página também podem ser acessados usando o novo [portal](https://portal.cloudappsecurity.com).

Atividades detectadas pelo ATP do Azure em sua rede podem ser pesquisadas e filtradas para busca detalhada e organização fáceis durante sua pesquisa e investigação de alertas de segurança.  

Na linha do tempo do ATP do Azure, selecione qualquer entidade em sua rede (controlador de domínio, computador ou usuário) como o ponto de acesso do filtro. Em seguida, escolha filtrar pelo **Alerta de segurança**, tipo de **Atividade** ou qualquer combinação. Depois que o filtro é aplicado, a linha do tempo da ameaça da entidade é atualizada com as informações filtradas. Seu alertas e atividades filtrados também podem ser baixados para continuar sua investigação ou acompanhamento em outras ferramentas. 

![Filtrar alertas e atividades](./media/activities-filter.png)

Para filtrar alertas e atividades:
 1. Selecione a entidade a investigar da linha do tempo do ATP do Azure. 
 2. Clique em **Filtrar por** e, em seguida, selecione as atividades e/ou alertas a filtrar. 
 3. Clique em **Aplicar**. A linha do tempo de entidade é atualizada de acordo com os filtros que você selecionou. 
 4. Para baixar as atividades filtradas, clique em **Baixar atividades** e selecione o intervalo de datas para o relatório de download. 
 5. Para redefinir a linha do tempo de entidade para exibir todas as atividades e alertas, clique em **Redefinir** ou feche o filtro. 


## <a name="see-also"></a>Confira Também
- [Investigar entidades](investigate-entity.md)
- [Alertas de integridade](health-alerts.md)
- [Trabalhar com alertas de segurança](working-with-suspicious-activities.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)
