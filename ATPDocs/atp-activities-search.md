---
title: Filtro e Pesquisa de Atividades Monitoradas da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Este artigo fornece uma visão geral de como filtrar e pesquisar atividades monitoradas usando o ATP do Azure.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/28/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: a546703b-d5a9-404d-9e87-125523bb8421
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fb3839d5348f11b13176375be84ecd46d44fa365
ms.sourcegitcommit: 3ab48f180aa0276f4e19cf7cd567581c7b4324cc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50202466"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*


# <a name="azure-atp-monitored-activities-search-and-filter"></a>Pesquisa e filtragem de atividades monitoradas do ATP do Azure 

Atividades detectadas pelo ATP do Azure em sua rede podem ser pesquisadas e filtradas para busca detalhada e organização fáceis durante sua pesquisa e investigação de alertas de segurança.  

Na linha do tempo do ATP do Azure, selecione qualquer entidade em sua rede (controlador de domínio, computador ou usuário) como o ponto de acesso do filtro. Em seguida, escolha filtrar pelo **Alerta de segurança**, tipo de **Atividade** ou qualquer combinação. Depois que o filtro é aplicado, a linha do tempo da ameaça da entidade é atualizada com as informações filtradas. Seu alertas e atividades filtrados também podem ser baixados para continuar sua investigação ou acompanhamento em outras ferramentas. 

![Filtrar alertas e atividades](./media/activities-filter.png)

Para filtrar alertas e atividades:
 1. Selecione a entidade a investigar da linha do tempo do ATP do Azure. 
 2. Clique em **Filtrar por** e, em seguida, selecione as atividades e/ou alertas a filtrar. 
 3. Clique em **Aplicar**. A linha do tempo de entidade é atualizada de acordo com os filtros que você selecionou. 
 4. Para baixar as atividades filtradas, clique em **Baixar atividades** e selecione o intervalo de datas para o relatório de download. 
 5. Para redefinir a linha do tempo de entidade para exibir todas as atividades e alertas, clique em **Redefinir** ou feche o filtro. 


## <a name="see-also"></a>Consulte Também
- [Investigar entidades](investigate-entity.md)
- [Monitorar alertas](monitoring-alerts.md)
- [Trabalhar com alertas de segurança](working-with-suspicious-activities.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)
