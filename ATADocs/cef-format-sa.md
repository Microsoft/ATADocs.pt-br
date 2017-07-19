---
title: "Referência de log do SIEM do ATA | Microsoft Docs"
description: Fornece exemplos de logs de atividades suspeitas enviados do ATA para o SIEM.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/21/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 601b48ba-a327-4aff-a1f9-2377a2bb7a42
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: ca460647fbed07820e8d19083d5aca19a05bc0a8
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*


# <a name="ata-siem-log-reference"></a>Referência de log do SIEM do ATA

O ATA pode encaminhar eventos de alerta de monitoramento e atividade suspeita para seu SIEM. Eventos de atividade suspeita estão no formato CEF. Este artigo de referência fornece exemplos dos logs de atividades suspeitas enviados para o SIEM.

## <a name="sample-ata-suspicious-activities-in-cef-format"></a>Atividades suspeitas do ATA de exemplo em formato CEF
Os campos a seguir e seus valores são encaminhados para o SIEM:

-   start – a hora de início do alerta
-   suser – a conta (geralmente deve ser a conta de usuário) que está envolvida neste alerta
-   shost – o computador de origem para este alerta
-   outcome – para alertas para os quais há um êxito/falha da atividade executada nesse alerta  
-   msg – a descrição do alerta
-   cnt – para alertas que têm uma contagem de vezes que o alerta ocorreu (por exemplo, força bruta que tem uma quantidade de senhas adivinhada)
-   app – o protocolo usado neste alerta
-   externalId – a ID do evento que o ATA grava no log de eventos que corresponde a esse alerta
-   cs#label e cs# – essas são as cadeias de caracteres do cliente que o CEF permite usar. cs#label é o nome do novo campo e cs# é o valor, por exemplo: cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa

Neste exemplo, cs1 é um campo que tem uma URL para o alerta.

## <a name="sample-logs"></a>Logs de exemplo

Prioridades: 3 = baixa 5 = média 10 = alta

### <a name="bruteforce--ldap"></a>BruteForce – LDAP
05-03-2017          13:35:01               Auth.Warning    192.168.0.220     May  3 10:35:01 CENTER ATA:CEF:0|Microsoft|ATA|.5942.64854|BruteForceSuspiciousActivity|Brute force attack using LDAP simple bind|5|start=2017-05-03T10:34:57.2785534Z app=Ldap suser=Darris Woods shost=CLIENT1 msg=Ocorreu uma tentativa de ataque de força bruta usando o protocolo LDAP no Darris Woods (Engenheiro de Software) do CLIENT1 (76 tentativas de adivinhação). cnt=76 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70

05-03-2017          13:35:05               Auth.Warning    192.168.0.220     May  3 10:35:05 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|BruteForceSuspiciousActivity|Brute force attack using LDAP simple bind|5|start=2017-05-03T10:34:58.7004159Z app=Ldap suser=Dino Hopkins shost=CLIENT1 msg=Ocorreu uma tentativa de ataque de força bruta usando o protocolo LDAP no Dino Hopkins (Engenheiro de Software) do CLIENT1 (3 tentativas de adivinhação). cnt=3 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70

05-03-2017          13:35:05               Auth.Warning    192.168.0.220     May  3 10:35:05 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|BruteForceSuspiciousActivity|Brute force attack using LDAP simple bind|5|start=2017-05-03T10:34:59.7269332Z app=Ldap suser=Dino Hopkins shost=CLIENT1 msg=Ocorreu uma tentativa com êxito de ataque de força bruta usando o protocolo LDAP no Dino Hopkins (Engenheiro de Software) do CLIENT1 (77 tentativas de adivinhação). cnt=77 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70
### <a name="bruteforce"></a>BruteForce
05-14-2017          13:27:05               Auth.Warning    192.168.0.220     1 2017-05- ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|BruteForceSuspiciousActivity|Suspicious authentication failures|5|start=2017-05-14T10:27:04.3904739Z app=Kerberos shost=CLIENT1 msg=Foram detectadas falhas de autenticação suspeitas indicando um possível ataque de força bruta do CLIENT1. externalId=2023 cs1Label=url cs1=https://center/suspiciousActivity/591830f98ca1ec11d0c0d7f5
### <a name="privilege-escalation"></a>Elevação de privilégios
#### <a name="silver"></a>Prata
05-10-2017          17:14:15               Auth.Error           192.168.0.220     1 2017-05-10T14:14:15.589415+00:00 CENTER ATA 596 ForgedPacSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|ForgedPacSuspiciousActivity|Privilege escalation using forged authorization data|10|start=2017-05-10T14:11:51.8053059Z app=Kerberos suser=user1 msg=O user1 tentou elevar os privilégios para o HOST/client1 do CLIENT2 usando dados de autenticação forjados. externalId=2013 cs1Label=url cs1=https://center/suspiciousActivity/591320378ca1ec02543e4747
#### <a name="gold"></a>Ouro
05-10-2017          17:13:30               Auth.Error           192.168.0.220     1 2017-05-10T14:13:30.244377+00:00 CENTER ATA 596 ForgedPacSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|ForgedPacSuspiciousActivity|Privilege escalation using forged authorization data|10|start=2017-05-10T14:11:27.6455273Z app=Kerberos suser=user1 msg=O user1 tentou elevar os privilégios no DC4 do CLIENT1 usando dados de autorização forjados. externalId=2013 cs1Label=url cs1=https://center/suspiciousActivity/5913200a8ca1ec02543e3ea8
### <a name="golden-ticket"></a>Golden Ticket
05-14-2017          15:57:10               Auth.Warning    192.168.0.220     1 2017-05-14T12:57:10.392730+00:00 CENTER ATA 4732 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|Encryption downgrade activity|5|start=2017-05-14T12:55:08.6913033Z app=Kerberos msg=O método de criptografia do campo TGT da mensagem TGS_REQ do CLIENT1 passou por downgrade com base no comportamento aprendido anteriormente. Isso pode ser resultado de um Golden Ticket em uso no CLIENT1. externalId=2009 cs1Label=url cs1=https://center/suspiciousActivity/591854268ca1ec127ceec396
### <a name="honey-token-activity"></a>Atividade de Honey Token
05-11-2017          16:49:10               Auth.Warning    192.168.0.220     1 2017-05-11T13:49:10.725605+00:00 CENTER ATA 876 HoneytokenActivitySuspiciousActi ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|HoneytokenActivitySuspiciousActivity|Honeytoken activity|5|start=2017-05-11T13:49:09.6455794Z app=Kerberos suser=privtriservice msg=As seguintes atividades foram executadas por privtriservice:\r\nAutenticado do DC1 usando NTLM em recursos corporativos via DC1. externalId=2014 cs1Label=url cs1=https://center/suspiciousActivity/59146bd68ca1ec036ce57d29
### <a name="suspicious-replication-of-directory-services"></a>Replicação suspeita de serviços de diretório
May  3 11:02:28 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DirectoryServicesReplicationSuspiciousActivity|Malicious replication of directory services|10|start=2017-05-03T11:00:13.6560919Z suser=user1 shost=CLIENT1 outcome=Failure msg=Ocorreram tentativas de solicitações de replicação mal-intencionada pelo user1, do CLIENT1 no DC1. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b8c48ca1ec04d05ed28d
### <a name="malicious-data-protection-private-information-request"></a>Solicitação de informações privadas para proteção contra dados mal-intencionados
May  3 13:39:18 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|RetrieveDataProtectionBackupKeySuspiciousActivity|Malicious Data Protection Private Information Request|10|start=2017-05-03T13:37:06.4039886Z app=LsaRpc shost=CLIENT1 suser= outcome=Success msg=Um usuário desconhecido executou 4 tentativas com êxito do CLIENT1 para recuperar a chave de backup do domínio DPAPI do DC1. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909dd868ca1ec04d05fb01d
### <a name="massive-object-deletion"></a>Exclusão de Objeto Grande
05-14-2017          14:38:34               Auth.Warning    192.168.0.220     1 2017-05-14T11:38:34.898810+00:00 CENTER ATA 3748 MassiveObjectDeletionSuspiciousA ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|MassiveObjectDeletionSuspiciousActivity|Massive object deletion|5|start=2017-05-14T11:33:32.0000000Z msg=496 objetos (9,75% do total de objetos AD) foram excluídos em um período de nenhum tempo do domínio domain1.test.local. cnt=496 externalId=2016 cs1Label=url cs1=https://center/suspiciousActivity/591841ba8ca1ec0ea4ad587a
### <a name="over-pass-the-hash"></a>Over-pass-the-hash
05-14-2017          12:07:46               Auth.Warning    192.168.0.220     1 2017-05-14T09:07:46.652319+00:00 CENTER ATA 1116 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|Encryption downgrade activity|5|start=2017-05-14T09:07:44.9933773Z app=Kerberos msg=O método de criptografia do campo Encrypted_Timestamp da mensagem AS_REQ do CLIENT1 passou por downgrade com base no comportamento aprendido anteriormente. Isso pode ser resultado de um roubo de credencial usando o Overpass-the-Hash do CLIENT1. externalId=2010 cs1Label=url cs1=https://center/suspiciousActivity/59181e628ca1ec045cdfa929
### <a name="pass-the-hash"></a>Pass-the-hash
05-10-2017          17:48:51               Auth.Error           192.168.0.220     1 2017-05-10T14:48:51.998620+00:00 CENTER ATA 596 PassTheHashSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|PassTheHashSuspiciousActivity|Identity theft using Pass-the-Hash attack|10|start=2017-05-10T14:46:50.9463800Z app=Ntlm suser=user2 msg=O hash do user2 foi roubado de um dos computadores conectados anteriormente pelo user2 e usados do CLIENT1. externalId=2017 cs1Label=url cs1=https://center/suspiciousActivity/591328538ca1ec02543f9a1a
### <a name="account-enumeration"></a>Enumeração de conta
05-10-2017          16:44:22               Auth.Warning    192.168.0.220     1 2017-05-10T13:44:22.706381+00:00 CENTER ATA 596 AccountEnumerationSuspiciousActi ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|AccountEnumerationSuspiciousActivity|Reconnaissance using account enumeration|5|start=2017-05-10T13:44:20.9930644Z app=Kerberos shost=CLIENT3 msg=A atividade de enumeração de conta suspeita usando o protocolo Kerberos, originado do CLIENT3, foi detectada. O invasor realizou um total de 72 tentativas de adivinhação para nomes de conta, 2 tentativas de adivinhação corresponderam a nomes de conta existentes no Active Directory. externalId=2003 cs1Label=url cs1=https://center/suspiciousActivity/591319368ca1ec02543c56ee
### <a name="dns-recon"></a>Reconhecimento de DNS
05-03-2017          13:16:57               Auth.Warning    192.168.0.220     May  3 10:16:57 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DnsReconnaissanceSuspiciousActivity|Reconnaissance using DNS|5|start=2017-05-03T10:16:41.8297467Z app=Dns shost=CLIENT1 msg=Foi observada uma atividade DNS suspeita, originada do CLIENT1 (que não é um servidor DNS) no DC1. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa 05-03-2017          13:24:21               Auth.Warning    192.168.0.220     May  3 10:24:21 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DnsReconnaissanceSuspiciousActivity|Reconnaissance using DNS|5|start=2017-05-03T10:24:08.0950753Z app=Dns shost=CLIENT1 request=contoso.com requestMethod=Axfr reason=NameError outcome=Failure msg=Foi observada uma atividade DNS suspeita, originada do CLIENT1 (que não é um servidor DNS). A consulta foi para contoso.com (tipo Axfr). A resposta foi NameError. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa
### <a name="smb-session-enumeration"></a>Enumeração da sessão SMB
May  3 11:55:43 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|EnumerateSessionsSuspiciousActivity|Reconnaissance using SMB Session Enumeration|5|start=2017-05-03T11:52:02.4360718Z app=SrvSvc shost=CLIENT1 msg=As tentativas de enumeração de sessão SMB foram realizadas com êxito do CLIENT1 no DC1, expondo o user1 (daf::1). cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909c53f8ca1ec04d05f1cf1
### <a name="samr-enumeration"></a>Enumeração SAMR
May  3 11:44:48 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|SamrReconnaissanceSuspiciousActivity|Reconnaissance using directory services enumeration|5|start=2017-05-03T11:42:46.5911225Z app=Samr shost=CLIENT1 suser=user1 outcome=Success msg=Ocorreram tentativas de realizar as seguintes enumerações de serviços de diretório usando o protocolo SAMR no DC1 do CLIENT1:\r\nEnumeração com êxito de todos os grupos em domain1.test.local pelo user1 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909c2b08ca1ec04d05f0e19
### <a name="remote-execution"></a>Execução Remota
May  3 12:36:47 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|RemoteExecutionSuspiciousActivity|Remote execution attempt detected|3|start=2017-05-03T12:34:32.3714348Z app=ServiceControl shost=CLIENT1 suser=Administrator outcome=Success msg=As tentativas de execução remota a seguir foram realizadas no DC1 do CLIENT1:\r\nCriação remota com êxito de PSEXESVC pelo Administrador. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909cedf8ca1ec04d05f5692
### <a name="skeleton-key"></a>Skeleton Key
05-14-2017          12:13:12               Auth.Warning    192.168.0.220     1 2017-05-14T09:13:12.102468+00:00 CENTER ATA 1116 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|Encryption downgrade activity|5|start=2017-05-14T09:13:03.3509467Z app=Kerberos msg=O método de criptografia do campo ETYPE_INFO2 da mensagem KRB_ERR do CLIENT2 passou por downgrade com base no comportamento aprendido anteriormente. Isso pode ser resultado de uma Skeleton Key no DC3. externalId=2011 cs1Label=url cs1=https://center/suspiciousActivity/59181fa88ca1ec045cdfe630
### <a name="unusual-protocol-implementation"></a>Implementação de protocolo incomum
May  3 12:28:19 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|AbnormalProtocolSuspiciousActivity|Unusual protocol implementation|5|start=2017-05-03T12:28:05.3561302Z app=Ntlm shost=CLIENT1 suser=Administrator outcome=Success msg=Administrador autenticado com êxito do CLIENT1 no DC1 usando uma implementação de protocolo incomum. Isso pode ser resultado de ferramentas mal-intencionadas usadas para executar ataques como Pass-the-Hash e força bruta. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909cce38ca1ec04d05f4ab4
### <a name="sensitive-account-credentials-exposed"></a>Credenciais de conta confidenciais expostas
May  3 13:23:18 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|LdapSimpleBindCleartextPasswordSuspiciousActivity|Sensitive account credentials exposed|3|start=2017-05-03T13:23:09.7798589Z app=Ldap shost=CLIENT1 suser=Administrator msg=As credenciais do administrador foram expostas em texto não criptografado usando a associação LDAP simples de CLIENT1. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909d9c68ca1ec04d05f9918
### <a name="services-exposing-account-credentials"></a>Serviços expondo credenciais de conta
May  3 13:34:23 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|LdapSimpleBindCleartextPasswordSuspiciousActivity|Services exposing account credentials|3|start=2017-05-03T13:28:36.5159194Z app=Ldap shost=daf::220 msg=Os serviços em execução em daf::220 (daf::220) expõem as credenciais da conta em texto não criptografado usando a associação LDAP simples. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909dc5f8ca1ec04d05fa8b1
### <a name="pass-the-ticket"></a>Passagem de tíquete (Pass the ticket)
May  4 13:15:41 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|PassTheTicketSuspiciousActivity|Identity theft using Pass-the-Ticket attack|10|start=2017-05-04T13:13:44.5160000Z app=Kerberos shost=CLIENT1 suser=Administrator request=krbtgt/DOMAIN1.TEST.LOCAL msg=Os tíquetes do Kerberos do Administrador foram roubados do CLIENT2 para o CLIENT1 e usados para acessar krbtgt/DOMAIN1.TEST.LOCAL. cs2Label=ticketSourceComputer cs2=CLIENT2 cs3Label=ticketSourceComputerIpAddress cs3= cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/590b29168ca1ec0ba438acf6

## <a name="see-also"></a>Consulte também
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Planejamento da capacidade do ATA](ata-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
