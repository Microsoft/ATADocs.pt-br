---
title: Entendendo os alertas de monitoramento do Azure ATP | Microsoft Docs
description: Descreve como você pode usar os logs do Azure ATP para solucionar problemas
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/15/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: d0551e91-3b21-47d5-ad9d-3362df6d47c0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7cffaef77a80b5c1c9bb33694ef2c7a73ef80ee0
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166911"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*

# <a name="understanding-azure-atp-sensor-and-standalone-sensor-monitoring-alerts"></a>Entendendo os alertas de monitoramento do sensor autônomo e do sensor do Azure ATP

O Centro de Integridade do Azure ATP informa quando há um problema algum em seus espaços de trabalho do Azure ATP gerando um alerta de monitoramento. Este artigo descreve todos os alertas de monitoramento para cada componente, listando a causa e as etapas necessárias para resolver o problema.

## <a name="read-only-user-password-to-expire-shortly"></a>Senha de usuário somente leitura a expirar em breve

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|A senha de usuário somente leitura, usada para executar a resolução de entidades no Active Directory, está prestes a expirar em menos de 30 dias.|Se a senha do usuário expirar, todos os sensores do Azure ATP deixarão de ser executados e nenhum novo dado será coletado.|[Altere a senha de conectividade do domínio](modifying-atp-config-dcpassword.md) e, em seguida, atualize a senha no Console do Azure ATP.|Média|

## <a name="read-only-user-password-expired"></a>A senha de usuário somente leitura expirou

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|A senha de usuário somente leitura, usada para obter dados de diretório, expirou.|Todos os sensores do Azure ATP deixam de ser executados (ou deixarão de ser executados em breve) e nenhum novo dado é coletado.|[Altere a senha de conectividade do domínio](modifying-atp-config-dcpassword.md) e, em seguida, atualize a senha no Console do Azure ATP.|Alta|

## <a name="domain-synchronizer-not-assigned"></a>Sincronizador de domínio não atribuído

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|Não há nenhum sincronizador de domínio atribuído a um sensor do Azure ATP. Isso pode ocorrer se não houver nenhum sensor do Azure ATP configurado como um candidato a sincronizador de domínio.|Quando o domínio não está sincronizado, alterações em entidades podem fazer com que as informações da entidade no Azure ATP fiquem desatualizadas ou ausentes, mas isso não afeta nenhuma detecção.|Certifique-se de que pelo menos um sensor do Azure ATP esteja definido como [Sincronizador de domínio](install-atp-step5.md).|Baixo|

## <a name="allsome-of-the-capture-network-adapters-on-a-sensor-are-not-available"></a>Todos ou alguns dos adaptadores de rede de captura em um sensor não estão disponíveis

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|Todos ou alguns dos adaptadores de rede de captura selecionados no sensor do Azure ATP estão desabilitados ou desconectados.|O tráfego de rede para alguns ou todos os controladores de domínio não é capturado pelo sensor do Azure ATP. Isso afeta a capacidade de detectar atividades suspeitas, relacionadas aos controladores de domínio.|Certifique-se de que esses adaptadores de rede de captura selecionados no sensor do Azure ATP estejam habilitados e conectados.|Média|

## <a name="some-domain-controllers-are-unreachable-by-a-sensor"></a>Alguns controladores de domínio ficam inacessíveis por um sensor

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|Um sensor do Azure ATP tem funcionalidade limitada devido a problemas de conectividade com alguns dos controladores de domínio configurados.|A detecção de Passagem de hash pode ser menos precisa quando alguns controladores de domínio não podem ser consultados pelo sensor do Azure ATP.|Certifique-se de que os controladores de domínio estejam em funcionamento e de que esse sensor do Azure ATP possa abrir conexões LDAP para eles.|Média|

## <a name="all-domain-controllers-are-unreachable-by-a-sensor"></a>Todos os controladores de domínio ficam inacessíveis por um sensor

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O sensor do Azure ATP está offline no momento devido a problemas de conectividade com todos os controladores de domínio configurados.|Isso afeta a capacidade do Azure ATP de detectar atividades suspeitas relacionadas aos controladores de domínio monitorados por esse sensor do Azure ATP.| Certifique-se de que os controladores de domínio estejam em funcionamento e de que esse sensor do Azure ATP possa abrir conexões LDAP para eles.|Média|

## <a name="sensor-stopped-communicating"></a>O sensor parou de se comunicar

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|Não houve nenhuma comunicação do sensor do Azure ATP. O período padrão para este alerta é de cinco minutos.|O tráfego de rede não é mais capturado pelo adaptador de rede no sensor do Azure ATP. Isso afeta a capacidade do ATA de detectar atividades suspeitas, uma vez que o tráfego de rede não será capaz de alcançar o serviço de nuvem do Azure ATP.|Verifique se a porta usada para comunicação entre o sensor do Azure ATP e o serviço de nuvem do Azure ATP não está bloqueada por firewalls ou roteadores.|Média|

## <a name="no-traffic-received-from-domain-controller"></a>Nenhum tráfego recebido do controlador de domínio

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|Nenhum tráfego foi recebido do controlador de domínio por meio desse sensor do Azure ATP.|Isso pode indicar que o espelhamento de porta dos controladores de domínio com o sensor do Azure ATP ainda não está configurado ou não está funcionando.|Verifique se o [espelhamento de porta está configurado corretamente em seus dispositivos de rede](configure-port-mirroring.md).<br></br>Na NIC de captura do sensor do Azure ATP, desabilite esses recursos em Configurações Avançadas:<br></br>União de Segmentos de Recebimento (IPv4)<br></br>União de Segmentos de Recebimento (IPv6)|Média|

## <a name="some-forwarded-events-are-not-being-analyzed"></a>Alguns eventos encaminhados não estão sendo analisados

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O sensor do Azure ATP está recebendo mais eventos do que pode processar.|Alguns eventos encaminhados não estão sendo analisados, o que pode afetar a capacidade de detectar atividades suspeitas provenientes dos controladores de domínio monitorados por este sensor do Azure ATP.|Verifique se apenas os eventos necessários são encaminhados ao sensor do Azure ATP ou tente encaminhar alguns dos eventos para outro sensor do ATP.|Média|

## <a name="some-network-traffic-is-not-being-analyzed"></a>Parte do tráfego de rede não está sendo analisado

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O sensor do Azure ATP está recebendo mais tráfego de rede do que pode processar.|Parte do tráfego de rede não está sendo analisado, o que pode afetar a capacidade de detectar atividades suspeitas provenientes dos controladores de domínio monitorados por este sensor do Azure ATP.|Considere [adicionar mais processadores e memória](atp-capacity-planning.md) conforme necessário. Se esse for um sensor autônomo do Azure ATP, reduza o número de controladores de domínio monitorados.<br></br>Isso também pode ocorrer se você estiver usando controladores de domínio em máquinas virtuais VMware. Para evitar esses alertas, verifique se as configurações a seguir estão definidas como 0 ou Desabilitado na máquina virtual:<br></br>– TsoEnable<br></br>– LargeSendOffload(IPv4)<br></br>– Descarregamento de TSO do IPv4<br></br>Além disso, considere desabilitar o Descarregamento TSO gigante do IPv4. Para obter mais informações, consulte a documentação do VMware.|Média|

## <a name="sensor-service-failed-to-start"></a>O serviço do sensor falhou ao iniciar

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O sensor do Azure ATP não conseguiu iniciar por pelo menos 30 minutos.|Isso pode afetar a capacidade de detectar atividades suspeitas provenientes dos controladores de domínio monitorados por este sensor do Azure ATP.|Monitore os logs do sensor do Azure ATP para entender a causa raiz da falha do serviço do sensor do Azure ATP.|Alta|

## <a name="sensor-reached-a-memory-resource-limit"></a>O sensor atingiu o limite de um recurso de memória

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O sensor do Azure ATP interrompeu seu funcionamento e reiniciará automaticamente para proteger o controlador de domínio de uma condição de memória insuficiente.|O sensor do Azure ATP impõe limitações de memória a si mesmo para impedir que o controlador de domínio tenha limitações de recursos. Isso ocorre quando o uso de memória no controlador de domínio é alto. Os dados do controlador de domínio são apenas parcialmente monitorados.|Aumente a quantidade de memória (RAM) no controlador de domínio ou adicione mais controladores de domínio a esse site para melhor distribuir o carregamento deste controlador de domínio.|Média|

## <a name="sensor-outdated"></a>Sensor desatualizado

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|Um sensor do Azure ATP está desatualizado.|Um sensor do Azure ATP está executando uma versão desatualizada há três ou mais versões.|Atualize manualmente o sensor e verifique por que ele não está sendo atualizado automaticamente. Se isso não funcionar, baixe o pacote de instalação mais recente do sensor e desinstale e reinstale o sensor. Para obter mais informações, consulte [Instalando o sensor do Azure ATP](install-atp-step4.md).|Média|

## <a name="see-also"></a>Consulte Também

- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)