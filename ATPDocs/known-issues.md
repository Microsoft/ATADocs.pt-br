---
title: Problemas conhecidos do ATP do Azure | Microsoft Docs
description: Descreve os problemas atuais conhecidos no ATP do Azure
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 11/15/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: feea1982-ba23-48be-a468-98d2586cf840
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1d478957b33e65e0016600826718ae6efd4e0e43
ms.sourcegitcommit: f4e1d3e28037afc7b9a22355808a04a8dc8b9605
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2018
ms.locfileid: "52831435"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*

# <a name="azure-atp-known-issues"></a>Problemas conhecidos do ATP do Azure

Ocasionalmente, o ATP do Azure tem limitações de engenharia ou recurso que podem limitar ou alterar a maneira como sua organização usa os serviços do ATP do Azure. Limitações conhecidas do problema que não têm nenhuma solução alternativa ou um status de trabalho em andamento sem uma linha do tempo de atualização específica são descritos aqui. 

Para problemas conhecidos do ATP do Azure com soluções alternativas conhecidas, veja [Solução de problemas conhecidos do ATP do Azure](troubleshooting-atp-known-issues.md). Para verificar o status do seu locatário do ATP do Azure, visite o [Centro de integridade do ATP do Azure](atp-health-center.md). 

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

# <a name="closed"></a>Fechado 

Esse grupo de problemas conhecidos agora está fechado. Verifique o número de versão da correção para referência.   
## <a name="remote-code-execution-attempts-using-remote-powershell-commands-or-scripts-are-not-detected-when-using-windows-server-2016---v257-december-2-2018"></a>As tentativas de Execução Remota de Código por meio de comandos ou scripts remotos do PowerShell não são detectadas quando o Windows Server 2016 – v.2.57 (2 de dezembro de 2018) é usado
> [!div class="mx-tableFixed"]  
|Problema|Status|
|----|----|
|No momento, as tentativas de Execução de Código Remoto por meio dos comandos do PowerShell Remoto não são detectadas em computadores Sensor que executam o Windows Server 2016. As detecções relacionadas e os alertas resultantes não estão disponíveis.|A engenharia está trabalhando atualmente em resolver esse problema e adicionar suporte ao Windows Server 2016.|

## <a name="see-also"></a>Consulte Também

- [Solução de problemas conhecidos do ATP do Azure](troubleshooting-atp-known-issues.md)
- [Solução de problemas do ATP do Azure usando logs](troubleshooting-atp-using-logs.md)
- [Novidades sobre o Azure ATP](atp-whats-new.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)