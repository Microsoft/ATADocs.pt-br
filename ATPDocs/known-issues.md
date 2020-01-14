---
title: Problemas conhecidos do ATP do Azure | Microsoft Docs
description: Descreve os problemas atuais conhecidos no ATP do Azure
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 02/25/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: feea1982-ba23-48be-a468-98d2586cf840
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e74d9330735e88eecbdd382f65dd8ac504502da7
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2020
ms.locfileid: "75906094"
---
# <a name="azure-atp-known-issues"></a>Problemas conhecidos do ATP do Azure

Ocasionalmente, o ATP do Azure tem limitações de engenharia ou recurso que podem limitar ou alterar a maneira como sua organização usa os serviços do ATP do Azure. Limitações conhecidas do problema que não têm nenhuma solução alternativa ou um status de trabalho em andamento sem uma linha do tempo de atualização específica são descritos aqui. 

Para problemas conhecidos do ATP do Azure com soluções alternativas conhecidas, veja [Solução de problemas conhecidos do ATP do Azure](troubleshooting-atp-known-issues.md). Para verificar o status do seu locatário do ATP do Azure, visite o [Centro de integridade do ATP do Azure](atp-health-center.md). 

## <a name="dns-reconnaissance-alert"></a>Alerta de reconhecimento de DNS
> [!div class="mx-tableFixed"] 

|Problema|Status|
|----|----|
O problema do alerta de segurança de *reconhecimento de DNS* afeta os clientes emitindo **alertas de reconhecimento DNS** falsos positivos repetitivos de um único computador. Se um pico de **alertas de reconhecimento DNS** for gerado a partir de um único computador, feche ou exclua esses alertas até que a atualização 2.67 seja implantada e resolva esse problema. | A atualização 2.67 resolve esse problema.|

## <a name="suspected-brute-force-attack-ldap-security-alert-display"></a>Exibição de alerta de segurança de suspeita de LDAP (ataque de força bruta)
> [!div class="mx-tableFixed"] 

|Problema|Status|
|----|----|
O alerta de segurança de *Suspeita de LDAP (ataque de força bruta)* não é sempre exibido como esperado. Em determinados cenários, a descrição do alerta é exibida fora de ordem.| A engenharia está trabalhando atualmente em resolver esse problema e solucionar esse problema.| 

## <a name="ad-groups-with-more-than-1000-members-have-limited-detail-sync"></a>Grupos do AD com mais de 1.000 membros têm sincronização de detalhes limitada
> [!div class="mx-tableFixed"]  
> 
> |Problema|Status|
> |----|----|
> |O ATP do Azure não dá suporte à sincronização de detalhes da entidade em grupos do AD com mais de 1.000 membros por grupo. Ao investigar entidades em grupos com mais de 1000 membros, algumas entidades poderão não conseguir sincronizar ou exibir detalhes.|Limitação de engenharia. Não há solução conhecida.|

## <a name="report-downloads-cannot-contain-more-than-100000-entries"></a>Downloads de relatório não podem conter mais de 100.000 entradas
> [!div class="mx-tableFixed"]  
> 
> |Problema|Status|
> |----|----|
> |O ATP do Azure não dá suporte a downloads de relatório que contêm mais de 100.000 entradas por relatório. Os relatórios serão renderizados como incompletos se mais de 100.000 entradas forem incluídas.|Limitação de engenharia. Não há solução conhecida.|

## <a name="closed-issues"></a>Problemas corrigidos

Esse grupo de problemas conhecidos agora está fechado. Verifique o número de versão da correção para referência.   
### <a name="remote-code-execution-attempts-using-remote-powershell-commands-or-scripts-are-not-detected-when-using-windows-server-2016---v257-december-2-2018"></a>As tentativas de Execução Remota de Código por meio de comandos ou scripts remotos do PowerShell não são detectadas quando o Windows Server 2016 – v.2.57 (2 de dezembro de 2018) é usado
> [!div class="mx-tableFixed"]  
> 
> |Problema|Status|
> |----|----|
> |No momento, as tentativas de Execução de Código Remoto por meio dos comandos do PowerShell Remoto não são detectadas em computadores Sensor que executam o Windows Server 2016. As detecções relacionadas e os alertas resultantes não estão disponíveis.|A engenharia está trabalhando atualmente em resolver esse problema e adicionar suporte ao Windows Server 2016.|

## <a name="see-also"></a>Consulte Também

- [Solução de problemas conhecidos do ATP do Azure](troubleshooting-atp-known-issues.md)
- [Solução de problemas do ATP do Azure usando logs](troubleshooting-atp-using-logs.md)
- [Novidades sobre o Azure ATP](atp-whats-new.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
