---
title: Problemas conhecidos do ATP do Azure | Microsoft Docs
description: Descreve os problemas atuais conhecidos no ATP do Azure
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 11/12/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: feea1982-ba23-48be-a468-98d2586cf840
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c1c5aa0359ac0d24d2bf3fc3033986657c3fc897
ms.sourcegitcommit: 2afc1486b40431f442d51a53df06e289796de87e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51561420"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*

# <a name="azure-atp-known-issues"></a>Problemas conhecidos do ATP do Azure

Ocasionalmente, o ATP do Azure tem limitações de engenharia ou recurso que podem limitar ou alterar a maneira como sua organização usa os serviços do ATP do Azure. Limitações conhecidas do problema que não têm nenhuma solução alternativa ou um status de trabalho em andamento sem uma linha do tempo de atualização específica são descritos aqui. 

Para problemas conhecidos do ATP do Azure com soluções alternativas conhecidas, veja [Solução de problemas conhecidos do ATP do Azure](troubleshooting-atp-known-issues.md). Para verificar o status do seu locatário do ATP do Azure, visite o [Centro de integridade do ATP do Azure](atp-health-center.md). 

## <a name="winrm-not-supported-using-windows-server-2016"></a>O WinRM não é compatível com o Windows Server 2016
> [!div class="mx-tableFixed"]  
|Problema|Status|
|----|----|
|No momento, o WinRM não dá suporte ao Windows Server 2016. A detecção relacionada e os alertas resultantes (tentativas de execução de código remoto) não estão disponíveis para computadores que executam o Windows Server 2016.|A engenharia está trabalhando atualmente em resolver esse problema e adicionar suporte ao Windows Server 2016.|

## <a name="ad-groups-with-more-than-1000-members-have-limited-detail-sync"></a>Grupos do AD com mais de 1.000 membros têm sincronização de detalhes limitada
> [!div class="mx-tableFixed"]  
|Problema|Status|
|----|----|
|O ATP do Azure não dá suporte à sincronização de detalhes da entidade em grupos do AD com mais de 1.000 membros por grupo. Ao investigar entidades em grupos com mais de 1000 membros, algumas entidades poderão não conseguir sincronizar ou exibir detalhes.|Limitação de engenharia. Não há solução conhecida.|

## <a name="report-downloads-cannot-contain-more-than-100000-entries"></a>Downloads de relatório não podem conter mais de 100.000 entradas
> [!div class="mx-tableFixed"]  
|Problema|Status|
|----|----|
|O ATP do Azure não dá suporte a downloads de relatório que contêm mais de 100.000 entradas por relatório. Os relatórios serão renderizados como incompletos se mais de 100.000 entradas forem incluídas.|Limitação de engenharia. Não há solução conhecida.|

## <a name="see-also"></a>Consulte Também

- [Solução de problemas conhecidos do ATP do Azure](troubleshooting-atp-known-issues.md)
- [Solução de problemas do ATP do Azure usando logs](troubleshooting-atp-using-logs.md)
- [Novidades sobre o Azure ATP](atp-whats-new.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)