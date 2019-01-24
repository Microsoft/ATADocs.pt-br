---
title: Referência de log do SIEM do ATA | Microsoft Docs
description: Fornece exemplos de logs de alertas de segurança enviados do ATA para o SIEM.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/20/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 601b48ba-a327-4aff-a1f9-2377a2bb7a42
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: 357f3517a864114c0aaa83a074c0b061d21259c2
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54840923"
---
# <a name="ata-siem-log-reference"></a>Referência de log do SIEM do ATA


*Aplica-se a: Advanced Threat Analytics versão 1.9*

O ATA pode encaminhar eventos de alerta de monitoramento e de segurança para o SIEM. Os alertas são encaminhados no formato CEF. Abaixo, temos um exemplo de cada tipo de log de alerta de segurança a ser enviado para o SIEM.

## <a name="sample-ata-security-alerts-in-cef-format"></a>Alertas de segurança de exemplo do ATA do Azure no formato CEF
Os campos a seguir e seus valores são encaminhados para o SIEM:

-   start – a hora de início do alerta
-   suser – conta (normalmente, a conta de usuário) envolvida no alerta
-   shost – o computador de origem do alerta
-   outcome – alertas com êxito ou falha da atividade definida executada no alerta  
-   msg – descrição do alerta
-   cnt – alertas com uma contagem do número de vezes que o alerta ocorreu (por exemplo, a força bruta tem uma quantidade de senhas adivinhadas)
-   app – protocolo de alerta
-   externalId – a ID do evento que o ATA grava no log de eventos que corresponde ao alerta*
-   cs#label e cs# – cadeias de caracteres do cliente que o CEF permite usar. cs#label é o nome do novo campo e cs# é o valor, por exemplo: cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa

Neste exemplo, cs1 é um campo que tem uma URL para o alerta.

*Se você criar scripts ou com base nos logs de automação, use o externalID permanente de cada log em vez de usar os nomes de log, pois nomes de log estão sujeitos a alterações sem aviso prévio. 

|Nome do alerta|IDs do evento de alerta|
|---------|---------------|
|2001|Suspeita de roubo de identidade com base no comportamento anormal|
|2002|Implementação de protocolo incomum|
|2003|Reconhecimento de enumeração de conta|
|2004|Ataque de força bruta usando associação simples LDAP|
|2006|Replicação mal-intencionada de serviços de diretório|
|2007|Reconhecimento usando DNS|
|2008|Atividade de downgrade de criptografia|
|2009|Atividade de downgrade de criptografia (possível ataque golden ticket)|
|2010|Atividade de downgrade de criptografia (possível ataque overpass-the-hash)|
|2011|Atividade de downgrade de criptografia (possível ataque de skeleton key)|
|2012|Reconhecimento usando a enumeração da sessão SMB|
|2013|Elevação de privilégios usando dados de autorização forjados|
|2014|Atividade de Honeytoken|
|2016|Exclusão de objeto grande|
|2017|Roubo de identidade usando o ataque de passagem de Hash|
|2018|Roubo de identidade usando o ataque Pass-the-Ticket|
|2019|Tentativa de execução remota detectada|
|2020|Solicitação mal-intencionada de informações privadas para proteção de dados|
|2021|Reconhecimento usando consultas de serviços de diretório|
|2022|Atividade Golden Ticket do Kerberos|
|2023|Falhas de autenticação suspeitas|
|2024|Modificação anormal de grupos confidenciais|
|2026|Criação de serviço suspeito|



## <a name="sample-logs"></a>Logs de exemplo

Prioridades: 3=Baixa 5=Média 10=Alta

### <a name="abnormal-modification-of-sensitive-groups"></a>Modificação anormal de grupos confidenciais
1 2018-12-12T16:53:22.925757+00:00 CENTER ATA 4688 AbnormalSensitiveGroupMembership CEF:0|Microsoft|ATA|1.9.0.0|AbnormalSensitiveGroupMembershipChangeSuspiciousActivity|Modificação anormal de grupos confidenciais|5|start=2018-12-12T18:52:58.0000000Z app=GroupMembershipChangeEvent suser=krbtgt msg=krbtgt tem associações a grupos confidenciais modificadas de modo estranho. externalId=2024 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113d028ca1ec1250ca0491

### <a name="brute-force-attack-using-ldap-simple-bind"></a>Ataque de força bruta usando associação simples LDAP
12-12-2018  19:52:18    Auth.Warning    192.168.0.222   1 2018-12-12T17:52:18.899690+00:00 CENTER ATA 4688 LdapBruteForceSuspiciousActivity ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|LdapBruteForceSuspiciousActivity|Ataque de força bruta usando associação simples LDAP|5|start=2018-12-12T17:52:10.2350665Z app=Ldap msg=10000 tentativas de adivinhação de senha foram feitas em 100 contas de W2012R2-000000-Server. Uma senha da conta foi adivinhada com êxito. externalId=2004 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114acb8ca1ec1250cacdcb

### <a name="encryption-downgrade-activity-golden-ticket"></a>Atividade de downgrade de criptografia (Golden Ticket)
12-12-2018  20:12:35    Auth.Warning    192.168.0.222   1 2018-12-12T18:12:35.105942+00:00 CENTER ATA 4688 EncryptionDowngradeSuspiciousAct ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|EncryptionDowngradeSuspiciousActivity|Atividade de downgrade de criptografia|5|start=2018-12-12T18:10:35.0334169Z app=Kerberos msg=O método de criptografia do campo TGT da mensagem TGS_REQ do W2012R2-000000-Server sofreu downgrade com base em comportamento previamente aprendido. Isso pode ser resultado de um Golden Ticket em uso em W2012R2-000000-Server. externalId=2009 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114f938ca1ec1250cafcfa

### <a name="encryption-downgrade-activity-overpass-the-hash"></a>Atividade de downgrade de criptografia (overpass-the-hash)
12-12-2018          19:00:31               Auth.Warning    192.168.0.222     1 2018-12-12T17:00:31.963485+00:00 CENTER ATA 4688 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.9.0.0|EncryptionDowngradeSuspiciousActivity|Atividade de downgrade de criptografia|5|start=2018-12-12T17:00:31.2975188Z app=Kerberos msg=O método de criptografia do campo Encrypted_Timestamp da mensagem AS_REQ do W2012R2-000000-Server passou por downgrade com base no comportamento aprendido anteriormente. Isso pode ser resultado de um roubo de credencial usando o Overpass-the-Hash do W2012R2-000000-Server. externalId=2010 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113eaf8ca1ec1250ca0883

###  <a name="encryption-downgrade-activity-skeleton-key"></a>Atividade de downgrade de criptografia (Skeleton Key)
12-12-2018  20:07:24    Auth.Warning    192.168.0.222   1 2018-12-12T18:07:24.065140+00:00 CENTER ATA 4688 EncryptionDowngradeSuspiciousAct ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|EncryptionDowngradeSuspiciousActivity|Atividade de downgrade de criptografia|5|start=2018-12-12T18:07:24.0222746Z app=Kerberos msg=O método de criptografia do campo ETYPE_INFO2 da mensagem KRB_ERR do W2012R2-000000-Server sofreu downgrade com base em comportamento previamente aprendido. Isso pode ser resultado de uma Skeleton Key no DC1. externalId=2011 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114e5c8ca1ec1250cafafe

### <a name="honeytoken-activity"></a>Atividade de Honeytoken
12-12-2018  19:51:52    Auth.Warning    192.168.0.222   1 2018-12-12T17:51:52.659618+00:00 CENTER ATA 4688 HoneytokenActivitySuspiciousActi ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|HoneytokenActivitySuspiciousActivity|Atividade de honeytoken|5|start=2018-12-12T17:51:52.5855994Z app=Kerberos suser=USR78982 msg=As seguintes atividades foram realizadas por USR78982 LAST78982:\r\nAutenticado de CLIENT1 usando NTLM ao acessar domain1.test.local\cifs em DC1. externalId=2014 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114ab88ca1ec1250ca7f76

### <a name="identity-theft-using-pass-the-hash-attack"></a>Roubo de identidade usando o ataque de passagem de Hash
12-12-2018  19:56:02    Auth.Error  192.168.0.222   1 2018-12-12T17:56:02.047236+00:00 CENTER ATA 4688 PassTheHashSuspiciousActivity ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|PassTheHashSuspiciousActivity|Roubo de identidade usando o ataque Pass-the-Hash|10|start=2018-12-12T17:54:01.9582400Z app=Ntlm suser=USR46829 LAST46829 msg=O hash de USR46829 LAST46829 foi roubado de um dos computadores nos quais USR46829 LAST46829 fez logon anteriormente e que foram usados de W2012R2-000000-Server. externalId=2017 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114bb28ca1ec1250caf673

### <a name="identity-theft-using-pass-the-ticket-attack"></a>Roubo de identidade usando o ataque Pass-the-Ticket
12-12-2018  22:03:51    Auth.Error  192.168.0.222   1 2018-12-12T20:03:51.643633+00:00 CENTER ATA 4688 PassTheTicketSuspiciousActivity ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|PassTheTicketSuspiciousActivity|Roubo de identidade usando o ataque Pass-the-Ticket|10|start=2018-12-12T17:54:12.9960662Z app=Kerberos suser=Birdie Lamb msg=Os tíquetes de Birdie Lamb (engenheira de Software) foram roubados de W2012R2-000106-Server para W2012R2-000051-Server e usados para acessar domain1.test.local\host. externalId=2018 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114b458ca1ec1250caf5b7

### <a name="kerberos-golden-ticket-activity"></a>Atividade Golden Ticket do Kerberos
12-12-2018  19:53:26    Auth.Error  192.168.0.222   1 2018-12-12T17:53:26.869091+00:00 CENTER ATA 4688 GoldenTicketSuspiciousActivity ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|GoldenTicketSuspiciousActivity|Atividade Golden Ticket do Kerberos|10|start=2018-12-13T06:51:26.7290524Z app=Kerberos suser=Sonja Chadsey msg=Foi detectado uso suspeito do tíquete do Kerberos de Sonja Chadsey (engenheira de software), indicando um potencial ataque de Golden Ticket. externalId=2022 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114b168ca1ec1250caf556

### <a name="malicious-data-protection-private-information-request"></a>Solicitação mal-intencionada de informações privadas para proteção de dados
12-12-2018  20:03:49    Auth.Error  192.168.0.222   1 2018-12-12T18:03:49.814620+00:00 CENTER ATA 4688 RetrieveDataProtectionBackupKeyS ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|RetrieveDataProtectionBackupKeySuspiciousActivity|Solicitação maliciosa de informações particulares de proteção de dados|10|start=2018-12-12T17:58:56.3537533Z app=LsaRpc shost=W2012R2-000000-Server msg=Um usuário desconhecido realizou uma tentativa bem-sucedida, originada de W2012R2-000000-Server, de recuperar a chave de backup do domínio DPAPI de DC1. externalId=2020 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114d858ca1ec1250caf983

### <a name="malicious-replication-of-directory-services"></a>Replicação mal-intencionada de serviços de diretório
12-12-2018  19:56:49    Auth.Error  192.168.0.222   1 2018-12-12T17:56:49.312648+00:00 CENTER ATA 4688 DirectoryServicesReplicationSusp ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|DirectoryServicesReplicationSuspiciousActivity|Replicação mal-intencionada de serviços de diretório|10|start=2018-12-12T17:52:34.3287329Z app=Drsr shost=W2012R2-000000-Server msg=Solicitações mal-intencionadas de replicação foram realizadas com êxito de W2012R2-000000-Server para DC1. outcome=Success externalId=2006 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114be18ca1ec1250caf6b8

### <a name="privilege-escalation-using-forged-authorization-data"></a>Elevação de privilégios usando dados de autorização forjados
12-12-2018  19:51:15    Auth.Error  192.168.0.222   1 2018-12-12T17:51:15.658608+00:00 CENTER ATA 4688 ForgedPacSuspiciousActivity ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|ForgedPacSuspiciousActivity|Elevação de privilégios usando dados de autorização forjados|10|start=2018-12-12T17:51:15.0261128Z app=Kerberos suser=triservice msg=O triservice tentou elevar os privilégios no DC1 do W2012R2-000000-Server usando dados de autorização forjados. externalId=2013 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114a938ca1ec1250ca7f48

### <a name="reconnaissance-using-directory-services-queries"></a>Reconhecimento usando consultas de serviços de diretório
12-12-2018  20:23:52    Auth.Warning    192.168.0.222   1 2018-12-12T18:23:52.155531+00:00 CENTER ATA 4688 SamrReconnaissanceSuspiciousActi ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|SamrReconnaissanceSuspiciousActivity|Reconhecimento usando consultas de serviços de diretório|5|start=2018-12-12T18:04:12.9868815Z app=Samr shost=W2012R2-000000-Server msg=Houve tentativas de realizar as seguintes consultas de serviços de diretório a DC1, usando protocolo SAMR, de W2012R2-000000-Server:\r\nConsulta bem-sucedida sobre Criadores de confiança de floresta de entrada (membros desse grupo podem criar relações de confiança unidirecionais de entrada para esta floresta) in domain1.test.local externalId=2021 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114e758ca1ec1250cafb2e

### <a name="reconnaissance-using-account-enumeration"></a>Reconhecimento de enumeração de conta
1 2018-12-12T16:57:09.661680+00:00 CENTER ATA 4688 AccountEnumerationSuspiciousActi CEF:0|Microsoft|ATA|1.9.0.0|AccountEnumerationSuspiciousActivity|Reconhecimento usando enumeração de conta|5|start=2018-12-12T16:57:09.1706828Z app=Kerberos shost=W2012R2-000000-Server msg=A atividade de enumeração de conta suspeita usando o protocolo Kerberos, originada do W2012R2-000000-Server, foi detectada. O invasor realizou um total de 100 tentativas de adivinhação para nomes de conta, uma tentativa de adivinhação correspondeu a um nome de conta existente no Active Directory. externalId=2003 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113de58ca1ec1250ca06d8

### <a name="reconnaissance-using-dns"></a>Reconhecimento usando DNS
1 2018-12-12T16:57:20.743634+00:00 CENTER ATA 4688 DnsReconnaissanceSuspiciousActiv CEF:0|Microsoft|ATA|1.9.0.0|DnsReconnaissanceSuspiciousActivity|Reconhecimento usando DNS|5|start=2018-12-12T16:57:20.2556472Z app=Dns shost=W2012R2-000000-Server msg=Foi observada uma atividade DNS suspeita, originada do W2012R2-000000-Server (que não é um servidor DNS) direcionada a DC1. externalId=2007 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113df08ca1ec1250ca074c

### <a name="reconnaissance-using-smb-session-enumeration"></a>Reconhecimento usando a enumeração da sessão SMB
12-12-2018  19:50:51    Auth.Warning    192.168.0.222   1 2018-12-12T17:50:51.090247+00:00 CENTER ATA 4688 EnumerateSessionsSuspiciousActiv ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|EnumerateSessionsSuspiciousActivity|Reconhecimento usando enumeração de sessão SMB|5|start=2018-12-12T17:00:42.7234229Z app=SrvSvc shost=W2012R2-000000-Server msg=Falha nas tentativas de enumeração de sessão SMB de W2012R2-000000-Server para DC1. Nenhuma conta foi exposta. externalId=2012 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114a788ca1ec1250ca7735

### <a name="remote-execution-attempt-detected"></a>Tentativa de execução remota detectada
12-12-2018  19:58:45    Auth.Warning    192.168.0.222   1 2018-12-12T17:58:45.082799+00:00 CENTER ATA 4688 RemoteExecutionSuspiciousActivit ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|RemoteExecutionSuspiciousActivity|Tentativa de execução remota detectada|5|start=2018-12-12T17:54:23.9523766Z shost=W2012R2-000000-Server msg=As seguintes tentativas de execução remota foram realizadas no DC1 por W2012R2-000000-Server:\r\nFalha no agendamento remoto de uma ou mais tarefas. externalId=2019 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114c548ca1ec1250caf783

### <a name="unusual-protocol-implementation"></a>Implementação de protocolo incomum
1 2018-12-12T16:50:46.930234+00:00 CENTER ATA 4688 AbnormalProtocolSuspiciousActivi CEF:0|Microsoft|ATA|1.9.0.0|AbnormalProtocolSuspiciousActivity|Implementação de protocolo incomum|5|start=2018-12-12T16:48:46.6480337Z app=Ntlm shost=W2012R2-000000-Server outcome=Success msg=O triservice autenticou com êxito de W2012R2-000000-Server em DC1 usando uma implementação de protocolo incomum. Isso pode ser resultado de ferramentas mal-intencionadas usadas para executar ataques como Pass-the-Hash e força bruta. externalId=2002 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113c668ca1ec1250ca0397

### <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>Suspeita de roubo de identidade com base no comportamento anormal
1 2018-12-12T16:50:35.746877+00:00 CENTER ATA 4688 AbnormalBehaviorSuspiciousActivi CEF:0|Microsoft|ATA|1.9.0.0|AbnormalBehaviorSuspiciousActivity|Suspeita de roubo de identidade com base em comportamento anormal|5|start=2018-12-12T16:48:35.5501183Z app=Kerberos suser=USR45964 msg=USR45964 LAST45964 apresentou comportamento anormal ao realizar atividades que não foram vistas durante o último mês e que também não estão de acordo com as atividades de outras contas na organização. O comportamento anormal baseia-se a seguintes atividades:\r\nLogon interativo realizado de 30 estações de trabalho.\r\nAcesso solicitado para 30 recursos anormais. externalId=2001 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113c5b8ca1ec1250ca0355

### <a name="suspicious-authentication-failures"></a>Falhas de autenticação suspeitas
12-12-2018  19:50:34    Auth.Warning    192.168.0.222   1 2018-12-12T17:04:25.214067+00:00 CENTER ATA 4688 BruteForceSuspiciousActivity ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|BruteForceSuspiciousActivity|Falhas de autenticação suspeitas|5|start=2018-12-12T17:03:58.5892462Z app=Kerberos shost=W2012R2-000106-Server msg=Falhas de autenticação suspeitas indicando um possível ataque de força bruta foram detectadas no W2012R2-000106-Server. externalId=2023 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113f988ca1ec1250ca5810

### <a name="suspicious-service-creation"></a>Criação de serviço suspeito
12-12-2018  19:53:49    Auth.Warning    192.168.0.222   1 2018-12-12T17:53:49.913034+00:00 CENTER ATA 4688 MaliciousServiceCreationSuspicio ‹¯¨CEF:0|Microsoft|ATA|1.9.0.0|MaliciousServiceCreationSuspiciousActivity|Criação de serviços suspeita|5|start=2018-12-12T19:53:49.0000000Z app=ServiceInstalledEvent shost=W2012R2-000000-Server msg=O triservice criou FakeService para executar comandos potencialmente mal-intencionados no W2012R2-000000-Server. externalId=2026 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114b2d8ca1ec1250caf577

## <a name="monitoring-alerts"></a>Monitoramento de alertas

### <a name="gatewaydisconnectedmonitoringalert"></a>GatewayDisconnectedMonitoringAlert
1 2018-12-12T16:52:41.520759+00:00 CENTER ATA 4688 GatewayDisconnectedMonitoringAle CEF:0|Microsoft|ATA|1.9.0.0|GatewayDisconnectedMonitoringAlert|GatewayDisconnectedMonitoringAlert|5|externalId=1011 cs1Label=url cs1=https\://192.168.0.220/monitoring msg=Não houve comunicação do Gateway CENTER por 5 minutos. A última comunicação foi em 12/12/2018 às 16:47:03 UTC.

### <a name="gatewaystartfailuremonitoringalert"></a>GatewayStartFailureMonitoringAlert
1 2018-12-12T15:36:59.701097+00:00 CENTER ATA 1372 GatewayStartFailureMonitoringAle CEF:0|Microsoft|ATA|1.9.0.0|GatewayStartFailureMonitoringAlert|GatewayStartFailureMonitoringAlert|5|externalId=1018 cs1Label=url cs1=https\://192.168.0.220/monitoring msg=O serviço de Gateway em DC1 falhou ao iniciar. Ele foi visto pela última vez em execução em 12/12/2018 15:04:12 UTC.

> [!NOTE]
> Todos os alertas de monitoramentos são enviados com o mesmo modelo acima.


## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Planejamento da capacidade do ATA](ata-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-collection.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
