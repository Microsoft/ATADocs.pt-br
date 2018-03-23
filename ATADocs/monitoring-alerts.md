---
title: Entendendo os alertas de monitoramento do ATA | Microsoft Docs
description: Descreve como você pode usar os logs do ATA para solucionar problemas
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: b04fb8a4-b366-4b55-9d4c-6f054fa58a90
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 6506ecf445641e9789cb1817916089f5463ba289
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2018
---
*Aplica-se a: Advanced Threat Analytics versão 1.9*


# <a name="understanding-ata-monitoring-alerts"></a>Entendendo os alertas de monitoramento do ATA
O Centro de Integridade do ATA permite saber quando há um problema com a implantação do ATA gerando um alerta de monitoramento.
Este artigo descreve todos os alertas de monitoramento para cada componente, listando a causa e as etapas necessárias para resolver o problema.
## <a name="ata-center-issues"></a>Problemas do Centro do ATA
### <a name="center-running-out-of-disk-space"></a>Centro com pouco espaço em disco
|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O espaço livre na unidade do computador do Centro do ATA usado para armazenar o banco de dados do ATA está acabando.|Isso significa que o disco rígido tem menos de 200 GB de espaço livre ou que há menos de 20% de espaço livre, o que for menor. Quando o ATA reconhece que a unidade está ficando com pouco espaço, ele começa a excluir dados antigos do banco de dados. Se ele não puder excluir dados antigos porque ainda precisa dos dados para o mecanismo de detecção, você receberá esse alerta. Quando você recebe esse alerta, o ATA para de controlar novas atividades.|Aumente o tamanho da unidade ou liberar espaço na unidade.|Alta|
### <a name="failure-sending-mail"></a>Falha ao enviar email
|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O ATA não conseguiu enviar uma notificação por email para o servidor de email especificado.|Nenhum email será enviado do ATA.|Verifique a configuração do servidor SMTP.|Baixo|

### <a name="center-overloaded"></a>Centro sobrecarregado
|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O Centro do ATA não é capaz de lidar com a quantidade de dados sendo transferida dos Gateways do ATA. |O Centro do ATA para a análise de novos eventos e tráfego de rede. Isso significa que a precisão de detecções de perfis é reduzida enquanto esse alerta de monitoramento está ativo.|Certifique-se de que você forneceu recursos suficientes para o Centro do ATA. Veja [Planejamento da capacidade de ATA](ata-capacity-planning.md) para obter mais detalhes sobre como planejar adequadamente a capacidade do Centro do ATA. Investigue o desempenho do Centro do ATA usando [Solução de problemas do ATA usando contadores de desempenho](troubleshooting-ata-using-perf-counters.md).|Alta|

### <a name="failure-connecting-to-the-siem-server-using-syslog"></a>Falha ao conectar ao servidor SIEM usando Syslog
|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O ATA falhou ao enviar eventos para o SIEM especificado.|Isso significa que o Centro do ATA não pode enviar atividades suspeitas e alertas de monitoramento para o SIEM.|Certifique-se de que suas [configurações do servidor Syslog estão definidas corretamente](setting-syslog-email-server-settings.md).|Baixo|
### <a name="center-certificate-is-about-to-expire"></a>O certificado do Centro está prestes a expirar
|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O certificado do Centro do ATA expirará em menos de três semanas.|Após a expiração do certificado: a conectividade de Gateways do ATA com o Centro do ATA falhará. O processo do Centro do ATA falhará e toda a funcionalidade do ATA será interrompida.|[Substitua o certificado do Centro do ATA](modifying-ata-center-configuration.md)|Média|
### <a name="ata-center-certificate-expired"></a>Certificado do Centro de ATA expirado
|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O certificado do Centro de ATA expirou.|Após a expiração do certificado: a conectividade de Gateways do ATA com o Centro do ATA falhará. O processo do Centro do ATA falha e toda a funcionalidade do ATA é interrompida.|[Substitua o certificado do Centro do ATA](modifying-ata-center-configuration.md)|Alta|
## <a name="ata-gateway-issues"></a>Problemas do Gateway do ATA
### <a name="read-only-user-password-to-expire-shortly"></a>Senha de usuário somente leitura a expirar em breve
|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|A senha de usuário somente leitura, usada para executar a resolução de entidades no Active Directory, está prestes a expirar em menos de 30 dias.|Se a senha para este usuário expirar, todos os Gateways do ATA interromperão a execução e nenhum novo dado será coletado.|[Altere a senha de conectividade do domínio](modifying-ata-config-dcpassword.md) e, em seguida, atualize a senha no Console do ATA.|Média|
### <a name="read-only-user-password-expired"></a>A senha de usuário somente leitura expirou
|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|A senha de usuário somente leitura, usada para obter dados de diretório, expirou.|Todos os Gateways do ATA interrompem a execução (ou interrompem a execução em breve) e nenhum novo dado é coletado.|[Altere a senha de conectividade do domínio](modifying-ata-config-dcpassword.md) e, em seguida, atualize a senha no Console do ATA.|Alta|
### <a name="gateway-certificate-about-to-expire"></a>Certificado do Gateway prestes a expirar
|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O certificado do Gateway do ATA expirará em menos de três semanas.|A conectividade do Gateway do ATA específico com o Centro do ATA falha. Nenhum dado desse Gateway do ATA é enviado.|O certificado do Gateway do ATA deveria ter sido renovado automaticamente. Leia os logs do Gateway do ATA e o Centro do ATA para entender porque esse certificado não foi renovado automaticamente.|Média|

### <a name="gateway-certificate-expired"></a>Certificado do Gateway expirou
|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O certificado do Gateway do ATA expirou.|Não há conectividade desse Gateway do ATA com o Centro do ATA. Nenhum dado desse Gateway do ATA é enviado.|[Desinstale e reinstale o Gateway do ATA](install-ata-step3.md).|Alta|
### <a name="domain-synchronizer-not-assigned"></a>Sincronizador de domínio não atribuído
|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|Não há nenhum sincronizador de domínio atribuído a qualquer Gateway do ATA. Isso pode ocorrer se não houver nenhum Gateway do ATA configurado como um candidato a sincronizador de domínio.|Quando o domínio não está sincronizado, alterações em entidades podem fazer com que as informações de entidade no ATA fiquem desatualizadas ou ausentes, mas não afetam nenhuma detecção.|Certifique-se de que pelo menos um Gateway do ATA esteja definido como um [Sincronizador de domínio](install-ata-step5.md).|Baixo|
### <a name="allsome-of-the-capture-network-adapters-on-a-gateway-are-not-available"></a>Todos ou alguns dos adaptadores de rede de captura em um Gateway não estão disponíveis
|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|Todos ou alguns dos adaptadores de rede de captura selecionados no Gateway do ATA estão desabilitados ou desconectados.|O tráfego de rede para alguns ou todos os controladores de domínio não é capturado pelo Gateway do ATA. Isso afeta a capacidade de detectar atividades suspeitas, relacionadas aos controladores de domínio.|Certifique-se de que esses adaptadores de rede de captura selecionados no Gateway do ATA estejam habilitados e conectados.|Média|
### <a name="some-domain-controllers-are-unreachable-by-a-gateway"></a>Alguns controladores de domínio estão inacessíveis por um Gateway
|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|Um Gateway do ATA limitaram a funcionalidade devido a problemas de conectividade com alguns dos controladores de domínio configurados.|A passagem de detecção de Hash pode ser menos precisa quando alguns controladores de domínio não podem ser consultados pelo Gateway do ATA.|Certifique-se de que os controladores de domínio estejam em funcionamento e que esse Gateway do ATA possa abrir conexões LDAP para eles.|Média|
### <a name="all-domain-controllers-are-unreachable-by-a-gateway"></a>Todos os controladores de domínio estão inacessíveis por um Gateway
|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O Gateway do ATA está offline no momento devido a problemas de conectividade a todos os controladores de domínio configurados.|Isso afeta a capacidade do ATA de detectar atividades suspeitas relacionadas aos controladores de domínio monitorados por esse Gateway do ATA.| Certifique-se de que os controladores de domínio estejam em funcionamento e que esse Gateway do ATA possa abrir conexões LDAP para eles.|Média|
### <a name="gateway-stopped-communicating"></a>O Gateway parou de se comunicar
|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|Não houve nenhuma comunicação do Gateway do ATA. O período padrão para este alerta é de cinco minutos.|O tráfego de rede não é mais capturado pelo adaptador de rede no Gateway do ATA. Isso afeta a capacidade do ATA para detectar atividades suspeitas, já que o tráfego de rede não será capaz de alcançar o Centro do ATA.|Verifique se a porta usada para a comunicação entre o Gateway do ATA e o serviço do Centro do ATA não está bloqueada por firewalls ou roteadores.|Média|
### <a name="no-traffic-received-from-domain-controller"></a>Nenhum tráfego recebido do controlador de domínio
|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|Nenhum tráfego foi recebido do controlador de domínio por meio desse Gateway do ATA.|Isso pode indicar que o espelhamento de porta dos controladores de domínio com o Gateway do ATA ainda não está configurado ou não está funcionando.|Verifique se o [espelhamento de porta está configurado corretamente em seus dispositivos de rede](configure-port-mirroring.md).<br></br>Na NIC de captura no Gateway do ATA, desabilite esses recursos em Configurações Avançadas:<br></br>União de Segmentos de Recebimento (IPv4)<br></br>União de Segmentos de Recebimento (IPv6)|Média|
### <a name="some-forwarded-events-are-not-being-analyzed"></a>Alguns eventos encaminhados não estão sendo analisados
|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O Gateway do ATA está recebendo mais eventos do que ele possa processar.|Alguns eventos encaminhados não estão sendo analisados, o que pode afetar a capacidade de detectar atividades suspeitas provenientes dos controladores de domínio sendo monitorados por este Gateway do ATA.|Verifique se apenas os eventos necessários são encaminhados ao Gateway do ATA ou tente encaminhar alguns dos eventos para outro Gateway do ATA.|Média|
### <a name="some-network-traffic-is-not-being-analyzed"></a>Parte do tráfego de rede não está sendo analisado
|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O Gateway do ATA está recebendo mais tráfego de rede do que pode processar.|Parte do tráfego de rede não está sendo analisada, o que pode afetar a capacidade de detectar atividades suspeitas provenientes dos controladores de domínio sendo monitorados por este Gateway do ATA.|Considere [adicionar mais processadores e memória](ata-capacity-planning.md) conforme necessário. Se esse for um Gateway do ATA independente, reduza o número de controladores de domínio sendo monitorado.<br></br>Isso também pode ocorrer se você estiver usando controladores de domínio em máquinas virtuais VMware. Para evitar esses alertas, verifique se as configurações a seguir estão definidas como 0 ou Desabilitado na máquina virtual:<br></br>– TsoEnable<br></br>– LargeSendOffload(IPv4)<br></br>– Descarregamento de TSO do IPv4<br></br>Além disso, considere desabilitar o Descarregamento TSO gigante do IPv4. Para saber mais, confira a documentação do VMware.|Média|

### <a name="gateway-version-outdated"></a>Versão do Gateway desatualizada
|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O Centro do ATA é mais recente do que a versão instalada no Gateway do ATA. Isso está fazendo o Gateway do ATA parar de funcionar conforme o esperado.|Isso pode afetar a capacidade de detectar atividades suspeitas provenientes dos controladores de domínio sendo monitorados por este Gateway do ATA.|Atualize o Gateway do ATA para a versão mais recente automaticamente permitindo a [atualização automática](install-ata-step1.md) no Console do ATA ou baixando o pacote do Gateway do ATA mais recente disponível no Console do ATA.|Alta|
### <a name="gateway-service-failed-to-start"></a>Falha ao iniciar o serviço de Gateway
|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O serviço de Gateway do ATA não conseguiu iniciar por pelo menos 30 minutos.|Isso pode afetar a capacidade de detectar atividades suspeitas provenientes dos controladores de domínio sendo monitorados por este Gateway do ATA.|Monitore os logs do Gateway do ATA para [entender a causa raiz da falha do serviço de Gateway do ATA](troubleshooting-ata-using-logs.md).|Alta|
## <a name="lightweight-gateway"></a>Gateway Lightweight
### <a name="lightweight--gateway-reached-a-memory-resource-limit"></a>O Gateway Lightweight atingiu o limite de um recurso de memória
|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O Gateway Lightweight do ATA interrompeu seu funcionamento e reiniciará automaticamente para proteger o controlador de domínio de uma condição de memória insuficiente.|O Gateway Lightweight do ATA impõe limitações de memória em si mesmo para impedir que o controlador de domínio tenha limitações de recursos. Isso ocorre quando o uso de memória no controlador de domínio é alto. Os dados do controlador de domínio são apenas parcialmente monitorados.|Aumente a quantidade de memória (RAM) no controlador de domínio ou adicione mais controladores de domínio a esse site para melhor distribuir o carregamento deste controlador de domínio.|Média|


## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Planejamento da capacidade do ATA](ata-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
