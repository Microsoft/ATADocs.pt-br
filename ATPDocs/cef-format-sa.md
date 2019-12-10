---
title: Referência de log de SIEM do Azure ATP | Microsoft Docs
description: Fornece exemplos de logs de atividades suspeitas enviados do Azure ATP para o SIEM.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/25/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 3261155c-3c72-4327-ba29-c113c63a4e6d
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 3b2df6ec2beddd276e1e4acdb0a38feb4a3511a3
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "68781884"
---
# <a name="azure-atp-siem-log-reference"></a>Referência de logs de SIEM do Azure ATP

A Proteção Avançada contra Ameaças do Azure pode encaminhar eventos de alerta de monitoramento e de segurança para o SIEM. Os alertas e eventos estão no formato CEF. Este artigo de referência fornece exemplos dos logs enviados ao SIEM.

## <a name="sample-azure-atp-security-alerts-in-cef-format"></a>Alertas de segurança de exemplo da Proteção Avançada contra Ameaças do Azure no formato CEF
Os campos a seguir e seus valores são encaminhados para o SIEM:

|Detalhes|Explicação|
|---------|---------------|
|iniciar|hora de início do alerta|
|suser|conta (normalmente a do usuário) envolvida no alerta|
|conta do computador|conta (normalmente a do usuário) envolvida no alerta|
|resultado|quando relevante, êxito ou falha da atividade suspeita no alerta|
|msg|descrição do alerta|
|cnt|para alertas com uma contagem do número de vezes que a atividade ocorreu (por exemplo, a força bruta tem uma quantidade de senhas adivinhadas)|
|app |protocolo usado neste alerta|
|externalId|a ID do tipo de evento que a Proteção Avançada contra Ameaças do Azure grava no log de eventos correspondente a cada tipo de alerta|
|cs#label|cadeias de caracteres do cliente permitidas pelo CEF, em que cs#label é o nome do novo campo |
|cs#|cadeias de caracteres do cliente permitidas pelo CEF, em que cs# é o valor.|
|
- Por exemplo: cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa
<br> O campo cs1 é a URL de alerta. 

- Por exemplo: cs2Label=trigger cs2=new
<br> O campo cs2 identifica se o alerta é novo ou atualizado.


> [!NOTE]
> Caso planeje criar automação ou scripts para logs de SIEM do ATP do Azure, é recomendável usar o campo **externalId** para identificar o tipo de alerta em vez de usar o nome do alerta para essa finalidade. Nomes de alertas, ocasionalmente, podem ser modificados, enquanto o **externalId** de cada alerta é permanente.  

## <a name="azure-atp-security-alert-unique-external-ids"></a>IDs externas exclusivas de alerta de segurança do ATP do Azure

> [!div class="mx-tableFixed"] 

|Novo nome do alerta de segurança|Antigo nome do alerta de segurança|ID externa exclusiva|Severidade|MITRE ATT&CK Matrix™ |
|---------|----------|---------|---------|---------|
|[Reconhecimento de enumeração de conta](atp-reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)|Reconhecimento de enumeração de conta|2003|Média|Descoberta|
|[Exportação de dados por SMB](atp-exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030)| NA| 2030|Alta|Exportação,<br>Movimentação lateral,<br>Comando e controle|
|[Atividade de Honeytoken](atp-compromised-credentials-alerts.md#honeytoken-activity-external-id-2014)|Atividade de Honeytoken|2014|Média|Credencial de acesso,<br> Descoberta|
|[Solicitação mal-intencionada de chave mestra da API de Proteção de Dados](atp-domain-dominance-alerts.md#malicious-request-of-data-protection-api-master-key-external-id-2020)|Solicitação de informações privadas para proteção contra dados mal-intencionados|2020|Alta|Credencial de acesso|
|[Reconhecimento de mapeamento de rede (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)|Reconhecimento usando DNS|2007|Média|Descoberta|
|[Tentativa de execução remota de código](atp-domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)|Tentativa de execução remota de código|2019|Média|Execução,<br> Persistência,<br> Elevação de privilégios,<br> Evasão de defesa,<br> Movimentação lateral|
|[Execução remota de código sobre DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)|NA|2036|Média|Elevação de privilégios,<br> Movimentação lateral|
|[Reconhecimento de entidade de segurança (LDAP)](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)|NA|2038|Média|Credencial de acesso|
|[Suspeita de ataque de força bruta (NTLM do Kerberos)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)|Falhas de autenticação suspeitas|2023|Média|Credencial de acesso|
|[Suspeita de LDAP (ataque de força bruta)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004)|Ataque de força bruta usando associação simples LDAP|2004|Média|Credencial de acesso|
|[Suspeita de ataque de força bruta (SMB)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)|Implementação de protocolo incomum (possível uso de ferramentas mal-intencionadas, como a Hydra)|2033|Média|Movimentação lateral|
|[Suspeita de ataque de DCShadow (promoção do controlador de domínio)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-promotion-external-id-2028)|Promoção do controlador de domínio suspeito (possível ataque DCShadow)|2028|Alta|Evasão de defesa|
|[Suspeita de ataque de DCShadow (solicitação de replicação do controlador de domínio)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029)|Solicitação de replicação de controlador de domínio suspeita (possível ataque DCShadow)|2029|Alta|Evasão de defesa|
|[Suspeita de ataque de DCSync (replicação de serviços de diretório)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)|Replicação mal-intencionada de serviços de diretório|2006|Alta|Persistência,<br> Credencial de acesso|
|[Suspeita de uso de Golden Ticket (downgrade de criptografia)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)|Atividade de downgrade de criptografia (possível ataque golden ticket)|2009|Média|Elevação de privilégios,<br> Movimentação lateral,<br>Persistência|
|[Suspeita de uso de Golden Ticket (dados de autorização forjados)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013)|Elevação de privilégios usando dados de autorização forjados|2013|Alta|Elevação de privilégios,<br>Movimentação lateral,<br>Persistência|
|[Suspeita de uso de Golden Ticket (conta inexistente)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)|Golden Ticket do Kerberos – conta não existente|2027|Alta|Elevação de privilégios,<br> Movimentação lateral,<br>Persistência|
|[Suspeita de uso de Golden Ticket (anomalia de tíquete)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)|NA|2032|Alta|Elevação de privilégios,<br> Movimentação lateral,<br>Persistência|
|[Suspeita de uso de Golden Ticket (anomalia de tempo)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)|Golden Ticket do Kerberos – anomalia de tempo|2022|Alta|Elevação de privilégios,<br> Movimentação lateral,<br>Persistência|
|[Suspeita de roubo de identidade (Pass-the-Hash)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017)|Roubo de identidade usando o ataque de passagem de Hash|2017|Alta|Movimentação lateral|
|[Suspeita de roubo de identidade (Pass-the-Ticket)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)|Roubo de identidade usando o ataque Pass-the-Ticket|2018|Alto ou médio|Movimentação lateral|
|[Suspeita de violação da autenticação NTLM](atp-lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039)|NA|2039|Média|Elevação de privilégios,<br> Movimentação lateral|
|[Suspeita de ataque de retransmissão de NTLM](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)|NA|2037|Médio ou baixo se observado usando o protocolo NTLM v2 assinado|Elevação de privilégios, <br> Movimentação lateral|
|[Suspeita de ataque de Overpass-the-Hash (downgrade de criptografia)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008)|Atividade de downgrade de criptografia (possível ataque overpass-the-hash)|2008|Média|Movimentação lateral|
|[Suspeita de ataque de Overpass-the-Hash (Kerberos)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)|Implementação incomum de protocolo Kerberos (possível ataque de overpass-the-hash)|2002|Média|Movimentação lateral|
|[Suspeita de ataque de Skeleton Key (downgrade de criptografia)](atp-domain-dominance-alerts.md#suspected-skeleton-key-attack-encryption-downgrade-external-id-2010)|Atividade de downgrade de criptografia (possível ataque de skeleton key)|2010|Média|Movimentação lateral,<br> Persistência|
|[Suspeita de uso da estrutura de hacker Metasploit](atp-compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)|Implementação de protocolo incomum (possível uso das ferramentas de invasão Metasploit)|2034|Média|Movimentação lateral|
|[Suspeita de ataque do ransomware WannaCry](atp-compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)|Implementação de protocolo incomum (possível ataque do ransomware WannaCry)|2035|Média|Movimentação lateral|
|[Comunicação suspeita por DNS](atp-exfiltration-alerts.md#suspicious-communication-over-dns-external-id-2031)|Comunicação suspeita por DNS|2031|Média|Exfiltração|
|[Adições suspeitas a grupos confidenciais](atp-domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024)|Adições suspeitas a grupos confidenciais|2024|Média|Credencial de acesso,<br>Persistência|
|[Criação de serviço suspeito](atp-domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)|Criação de serviço suspeito|2026|Média|Execução,<br> Persistência,<br> Elevação de privilégios,<br> Evasão de defesa,<br>Movimentação lateral|
|[Conexão de VPN suspeita](atp-compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)|Conexão de VPN suspeita|2025|Média|Persistência,<br>Evasão de defesa|
|[Reconhecimento de usuário e de associação a um grupo (SAMR)](atp-reconnaissance-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)|Reconhecimento usando consultas de serviços de diretório|2021|Média|Descoberta|
|[Reconhecimento de endereço IP e de usuário (SMB)](atp-reconnaissance-alerts.md#user-and-ip-address-reconnaissance-smb-external-id-2012)|Reconhecimento usando a enumeração da sessão SMB|2012|Média|Descoberta|
|

## <a name="sample-logs"></a>Logs de exemplo

Os exemplos de logs estão em conformidade com o RFC 5242, mas o ATP do Azure também dá suporte ao RFC 3164.

Prioridades:

- 3 = Baixa
- 5 = Média
- 10 = Alta

### <a name="account-enumeration-reconnaissance"></a>Reconhecimento de enumeração de conta 
02-21-2018  16:19:35    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:27.540731+00:00 CENTER CEF 6076 AccountEnumerationSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AccountEnumerationSecurityAlert|Reconnaissance using account enumeration|5|start=2018-02-21T14:19:02.6045416Z app=Kerberos shost=CLIENT1 suser=LMaldonado msg=Suspicious account enumeration activity using the Kerberos protocol, originating from CLIENT1, was observed and successfully guessed Lamon Maldonado (Software Engineer). externalId=2003 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/eb6a35da-ff7f-4ab5-a1b5-a07529a89e6d cs2Label=trigger cs2=new

### <a name="data-exfiltration-over-smb"></a>Exportação de dados por SMB
19-12-2018 14:17:46    Auth.Error     127.0.0.1      1 2018-12-19T12:17:34.645993+00:00 DC1 CEF 3288 SmbDataExfiltrationSecurityAlert ï»¿0|Microsoft|Azure ATP|2.60.0.0|SmbDataExfiltrationSecurityAlert|[PREVIEW] Exportação de dados por SMB|10|start=2018-12-19T12:14:12.4932821Z app=Smb shost=CLIENT1 msg=Eugene Jenkins (Engenheiro de Software) em DC2 copiou arquivos suspeitos para CLIENT1. externalId=2030 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/3ca2ec9d-2c67-44cc-a2d6-391716611bb6 cs2Label=trigger cs2=new

### <a name="honeytoken-activity"></a>Atividade de Honeytoken
02-21-2018  16:20:36    Auth.Warning  192.168.0.220 1 2018-02-21T14:20:34.106162+00:00 CENTER CEF 6076 HoneytokenActivitySecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|HoneytokenActivitySecurityAlert|Honeytoken activity|5|start=2018-02-21T14:20:26.6705617Z app=Kerberos suser=honey msg=The following activities were performed by honey:\r\nLogged in to CLIENT2 via DC1. externalId=2014 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/9249fe9a-c883-46dd-a4da-2a1fca5f211c cs2Label=trigger cs2=new

### <a name="malicious-request-of-data-protection-api-master-key"></a>Solicitação mal-intencionada de chave mestra da API de Proteção de Dados 
10-29-2018  11:22:04    Auth.Error  192.168.0.202   1 2018-10-29T09:22:00.350864+00:00 DC3 CEF 3908 RetrieveDataProtectionBackupKeyS ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|RetrieveDataProtectionBackupKeySecurityAlert|Malicious Data Protection Private Information Request|10|start=2018-10-29T09:19:45.6307993Z app=LsaRpc shost=CLIENT1 msg=user1 performed 1 successful attempts from CLIENT1 to retrieve DPAPI domain backup key from DC1. externalId=2020 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/2f5717cb-2434-4d54-8af4-b2c6d14bc15c cs2Label=trigger cs2=new

### <a name="network-mapping-reconnaissance-dns"></a>Reconhecimento de mapeamento de rede (DNS)
10-29-2018  11:20:02    Auth.Warning    192.168.0.202   1 2018-10-29T09:19:59.056894+00:00 DC3 CEF 3908 DnsReconnaissanceSecurityAlert ï»¿0|Microsoft|ATP do Azure|2.52.5704.46184|DnsReconnaissanceSecurityAlert|Reconhecimento de uso de DNS|5|start=2018-10-29T09:19:43.5033765Z app=Dns shost=CLIENT1 msg=Foi observada atividade de DNS suspeita, originada do CLIENT1 (que não é um servidor DNS) em DC1. externalId=2007 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/23937d33-ff71-484d-be0a-3c417fe573ce cs2Label=trigger cs2=new

### <a name="reconnaissance-using-directory-services-queries"></a>Reconhecimento usando consultas de serviços de diretório 
02-21-2018  16:22:08    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:54.267658+00:00 CENTER CEF 6076 SamrReconnaissanceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|SamrReconnaissanceSecurityAlert| Reconnaissance using directory services enumeration |5|start=2018-02-21T14:19:41.9912772Z app= Samr shost=CLIENT1 suser=user1 outcome=Success msg= The following directory services enumerations using SAMR protocol were attempted against DC1 from CLIENT1:\r\nSuccessful enumeration of all groups in domain1.test.local by user1. externalId=2019 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0 cs2Label=trigger cs2=new

### <a name="remote-code-execution-attempt"></a>Tentativa de execução remota de código
10-29-2018  11:22:04    Auth.Warning    192.168.0.202   1 2018-10-29T09:22:00.100856+00:00 DC3 CEF 3908 RemoteExecutionSecurityAlert ï»¿0|Microsoft|ATP do Azure|2.52.5704.46184|RemoteExecutionSecurityAlert|Tentativa de execução remota de código|5|start=2018-10-29T09:19:45.0552367Z shost=CLIENT1 msg=As seguintes tentativas de execução remota de código foram realizadas em DC1 por meio do CLIENT1:\r\nÊxito no agendamento remoto de uma ou mais tarefas por user1.\r\nFalha no agendamento remoto de uma ou mais tarefas por user1.\r\nÊxito na execução remota de um ou mais métodos de WMI por user1. externalId=2019 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/f063c778-830c-4e9f-98d1-bc6c11c94e11 cs2Label=trigger cs2=new

### <a name="remote-code-execution-over-dns"></a>Execução remota de código sobre DNS
1-17-2019   08:24:54    Auth.Warning    192.168.0.202   1 2019-01-17T08:24:54.100856+00:00 DC3 CEF 3908 DnsRemoteCodeExecutionSecurityAlert ï»¿0|Microsoft|Azure ATP|2.63.0.0|DnsRemoteCodeExecutionSecurityAlert|[PREVIEW] Execução remota de código sobre DNS|5|start=2019-01-17T08:24:54.5293800Z app=Dns shost=CLIENT1 msg=Um agente tentou executar remotamente comandos em CLIENT1 a partir de DC1 sobre o protocolo DNS. externalId=2036 cs1Label=url cs1=https\:////contoso-corp.atp.azure.com:13000/securityAlert/591f9769-d904-40b1-89fa-c307c2ca814f cs2Label=trigger cs2=new

### <a name="security-principal-reconnaissance-ldap"></a>Reconhecimento de entidade de segurança (LDAP)
02-18-2019  16:48:08 Auth.Warning  127.0.0.1  1 2019-02-18T14:48:02.912264+00:00 DC1 CEF 4656 LdapSearchReconnaissanceSecurity ï»¿0|Microsoft|Azure ATP|2.66.0.0|LdapSearchReconnaissanceSecurityAlert|[PREVIEW] Reconhecimento usando consultas LDAP Queries|5|start=2019-02-18T14:46:29.4644276Z app=LdapSearch shost=CLIENT1 msg=um ator em CLIENT1 enviou consultas LDAP suspeitas para DC1, procurando por 4 tipos de enumerações e Operadores de Servidor (os membros podem administrar servidores do domínio) em 2 domínios externId=2038 cs1Label=url cs1=https\://contoso-corp.atp.azure..com:13000/securityAlert/81ea99c4-ce1f-4581-ac8f-7440fbed7cd0 cs2Label=trigger cs2=new

### <a name="suspected-brute-force-attack-ldap"></a>Suspeita de LDAP (ataque de força bruta)
02-21-2018  16:20:21    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:06.156238+00:00 CENTER CEF 6076 LdapBruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|LdapBruteForceSecurityAlert|Brute force attack using LDAP simple bind|5|start=2018-02-21T14:19:41.7422810Z app=Ldap suser=Wofford Thurston shost=CLIENT1 msg=A brute force attack using the Ldap protocol was attempted on Wofford Thurston (Software Engineer) from CLIENT1 (100 guess attempts). cnt=100 externalId=2004 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/57b8ac96-7907-4971-9b27-ec77ad8c029a cs2Label=trigger cs2=update

### <a name="suspected-brute-force-attack-kerberos-ntlm"></a>Suspeita de ataque de força bruta (NTLM do Kerberos)
10-29-2018  11:20:47    Auth.Warning    192.168.0.202   1 2018-10-29T09:20:44.478827+00:00 DC3 CEF 3908 BruteForceSecurityAlert ï»¿0|Microsoft|ATP do Azure|2.52.5704.46184|BruteForceSecurityAlert|Falhas de autenticação suspeitas|5|start=2018-10-29T09:19:44.9512286Z app=Kerberos shost=CLIENT1 msg=Falhas de autenticação suspeitas indicando um potencial ataque de força bruta foram detectadas do CLIENT1. externalId=2023 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/85042c8e-27fa-49b3-8667-dabc1aa31580 cs2Label=trigger cs2=new

### <a name="suspected-dcsync-attack-replication-of-directory-services"></a>Suspeita de ataque de DCSync (replicação de serviços de diretório)
02-21-2018  16:20:06    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:54.254930+00:00 CENTER CEF 6076 MaliciousServiceCreationSecurity ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|MaliciousServiceCreationSecurityAlert|Suspicious service creation|5|start=2018-02-21T14:19:41.7897808Z app=ServiceInstalledEvent shost=CLIENT1 msg=user1 created MaliciousService in order to execute potentially malicious commands on CLIENT1. externalId=2026 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/179229b6-b791-4895-b5aa-fdf3747a325c cs2Label=trigger cs2=update

### <a name="suspected-golden-ticket-usage-encryption-downgrade"></a>Suspeita de uso de Golden Ticket (downgrade de criptografia)
10-29-2018  11:25:07    Auth.Warning    192.168.0.202   1 2018-10-29T09:25:01.007701+00:00 DC3 CEF 3908 GoldenTicketEncryptionDowngradeS ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|GoldenTicketEncryptionDowngradeSecurityAlert|Encryption downgrade activity (potential golden ticket attack)|5|start=2018-10-29T09:37:49.0849130Z app=Kerberos msg=W10-000007-Lap used a weaker encryption method (RC4),Â in the Kerberos service request (TGS_REQ),Â from W10-000007-Lap, to access host/domain1.test.local. externalId=2009 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/f01f8403-88b2-437e-b4ad-d72485fe05ac cs2Label=trigger cs2=new

### <a name="suspected-golden-ticket-usage-non-existent-account"></a>Suspeita de uso de Golden Ticket (conta inexistente)
07-01-2018  14:28:49    Auth.Error  192.168.0.100   1 2018-07-01T11:28:35.546638+00:00 CENTER CEF 38768 ForgedPrincipalSecurityAlert ï»¿0|Microsoft|Azure ATP|2.39.0.0|ForgedPrincipalSecurityAlert|Kerberos Golden Ticket - non-existing account|10|start=2018-07-01T09:48:31.2567987Z app=Kerberos suser=domain1.test.local\fake msg=domain1.test.local\fake, which does not exist in Active Directory, used a Kerberos ticket. O tíquete foi detectado em dois computadores para acessar três recursos. Isso pode indicar um possível ataque de Golden Ticket. externalId=2027 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/98f050d4-9134-429c-8e54-d8eeb19849c4 cs2Label=trigger cs2=update

### <a name="suspected-golden-ticket-usage-ticket-anomaly"></a>Suspeita de uso de Golden Ticket (anomalia de tíquete) 
1 2018-11-18T10:46:23.346946+00:00 MAXIMG-7050 CEF 24284 GoldenTicketSizeAnomalySecurityA 0|Microsoft|ATP do Azure|2.56.0.0|GoldenTicketSizeAnomalySecurityAlert|[PREVIEW] Suspeita de uso de Golden Ticket (anomalia de tíquete)|10|start=2018-11-18T10:44:12.9317797Z app=Kerberos shost=CLIENT2 suser=RFosdyke msg=Renzo Fosdyke (Engenheiro de Software) usou um tíquete Kerberos suspeito do CLIENT2 para acessar ldap/domain1.test.local. externalId=2032 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/63600e03-f423-49bf-a92d-4010e1d52b9f cs2Label=trigger cs2=update

### <a name="suspected-golden-ticket-usage-time-anomaly"></a>Suspeita de uso de Golden Ticket (anomalia de tempo) 
02-21-2018  16:22:39    Auth.Error  192.168.0.220   1 2018-02-21T14:22:34.274054+00:00 CENTER CEF 6076 GoldenTicketSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|GoldenTicketSecurityAlert|Kerberos Golden Ticket activity|10|start=2018-02-21T14:19:03.2416152Z app=Kerberos suser=Lanell Campos msg=Suspicious usage of Lanell Campos (Software Engineer)'s Kerberos ticket, indicating a potential Golden Ticket attack, was detected. externalId=2022 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/702c836e-6f49-4479-9892-80e8bccbfac0 cs2Label=trigger cs2=update

### <a name="suspected-golden-ticket-usage-forged-authorization-data"></a>Suspeita de uso de Golden Ticket (dados de autorização forjados) 
10-29-2018  11:22:04    Auth.Error  192.168.0.202   1 2018-10-29T09:21:59.288337+00:00 DC3 CEF 3908 ForgedPacSecurityAlert ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|ForgedPacSecurityAlert|Privilege escalation using forged authorization data|10|start=2018-10-29T09:19:43.6403358Z app=Kerberos suser=user1 msg=user1 failed to escalate privileges against DC1 to host/domain1.test.local from CLIENT1 by using forged authorization data. externalId=2013 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/b698d438-5013-4bca-be0b-f219f8b69108 cs2Label=trigger cs2=new

### <a name="suspected-identity-theft-pass-the-hash"></a>Suspeita de roubo de identidade (Pass-the-Hash)
02-21-2018  17:04:47    Auth.Error  192.168.0.220   1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheHashSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheHashSecurityAlert|Identity theft using Pass-the-Hash attack|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Eugene Jenkins (Software Engineer)'s hash was stolen from one of the computers previously logged into by Eugene Jenkins (Software Engineer) and used from CLIENT1. externalId=2017 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd cs2Label=trigger cs2=update

### <a name="suspected-identity-theft-pass-the-ticket"></a>Suspeita de roubo de identidade (Pass-the-Ticket) 
02-21-2018  17:04:47    Auth.Error  192.168.0.220   1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheTicketSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheTicketSecurityAlert|Identity theft using Pass-the-Ticket attack|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Eugene Jenkins (Software Engineer)'s Kerberos tickets were stolen from Admin-PC to Victim-PC and used to access krbtgt/DOMAIN1.TEST.LOCAL. externalId=2018 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd cs2Label=trigger cs2=new

### <a name="suspected-ntlm-authentication-tampering"></a>Suspeita de violação da autenticação NTLM
07-17-2019  18:18:44    Auth.Warning   192.168.0.77       1 2019-07-09T15:18:30.967118+00:00 CENTER CEF 7144 AbnormalNtlmSigningSecurityAlert ï»¿0|Microsoft|ATP do Azure|2.86.0.0|AbnormalNtlmSigningSecurityAlert|[PREVIEW] Suspeita de violação da autenticação NTLM|5|start=2019-07-09T15:14:57.5280720Z app=Ntlm shost=CLIENT1 msg=2 contas no CLIENT1 estão tentando se autenticar com 2 computadores por NTLM de modo suspeito. externalId=2039 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/d4ce6252-2c0f-47f6-a534-47ee8ad983be cs2Label=trigger cs2=new

### <a name="suspected-over-pass-the-hash-attack-encryption-downgrade"></a>Suspeita de ataque de Overpass-the-Hash (downgrade de criptografia) 
02-21-2018  16:21:07    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:54.145833+00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EncryptionDowngradeSecurityAlert|Encryption downgrade activity|5|start=2018-02-21T14:19:41.8737870Z app=Kerberos msg= The encryption method of the Encrypted_Timestamp field of AS_REQ message from CLIENT1 has been downgraded based on previously learned behavior. Isso pode ser resultado de um roubo de credencial usando o Overpass-the-Hash do CLIENT1. externalId=2008 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2 cs2Label=trigger cs2=update

### <a name="suspected-skeleton-key-attack-encryption-downgrade"></a>Suspeita de ataque de Skeleton Key (downgrade de criptografia) 
02-21-2018  16:21:07    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:54.145833+00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|EncryptionDowngradeSecurityAlert|Encryption downgrade activity|5|start=2018-02-21T14:19:41.8737870Z app=Kerberos msg=The encryption method of the ETYPE_INFO2 field of KRB_ERR message from CLIENT1 has been downgraded based on previously learned behavior. Isso pode ser resultado de uma Skeleton Key no DC1. externalId=2010 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2 cs2Label=trigger cs2=new

### <a name="suspicious-authentication-failures"></a>Falhas de autenticação suspeitas
02-21-2018  16:19:20    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:15.397995+00:00 CENTER CEF 6076 BruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|BruteForceSecurityAlert|Suspicious authentication failures|5|start=2018-02-21T14:19:03.3831122Z app=Kerberos shost=CLIENT1 msg=Suspicious authentication failures indicating a potential brute-force attack were detected from CLIENT1. externalId=2023 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/fea88fc7-4110-454d-816d-349032474fd6 cs2Label=trigger cs2=new

### <a name="suspicious-communication-over-dns"></a>Comunicação suspeita por DNS
10-04-2018  14:49:38    Auth.Warning    192.168.0.202   1 2018-10-04T11:49:25.954059+00:00 DC3 CEF 3604 DnsSuspiciousCommunicationSecuri ï»¿0|Microsoft|ATP do Azure|2.49.5589.58606|DnsSuspiciousCommunicationSecurityAlert|Comunicação suspeita por meio de DNS|5|start=2018-10-04T11:49:11.0822077Z app=DnsEvent dhost= suspiciousdomainname msg=O CLIENT1 enviou consultas DNS suspeitas resolvendo suspiciousdomainname externalId=2031 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/0fc77777-49ca-40b3-a7ba-7644f355539e cs2Label=trigger cs2=new

### <a name="suspicious-domain-controller-promotion-potential-dcshadow-attack"></a>Promoção do controlador de domínio suspeito (possível ataque DCShadow)
07-12-2018  11:18:07    Auth.Error  192.168.0.200    1 2018-07-12T08:18:06.883880+00:00 DC1 CEF 3868 DirectoryServicesRoguePromotionS ï»¿0|Microsoft|Azure ATP|2.40.0.0|DirectoryServicesRoguePromotionSecurityAlert| **Promoção do controlador de domínio suspeito (possível ataque DcShadow)** |10|start=2018-07-12T08:17:55.4067092Z app=Ldap shost=CLIENT1 msg=CLIENT1, que é um computador em domain1.test.local, registrado como um controlador de domínio em DC1. externalId=2028 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/97c59b43-dc18-44ee-9826-8fd5d03bd53 cs2Label=trigger cs2=update

### <a name="suspicious-additions-to-sensitive-groups"></a>Adições suspeitas a grupos confidenciais
10-29-2018  11:21:03    Auth.Warning    192.168.0.202   1 2018-10-29T09:20:49.667014+00:00 DC3 CEF 3908 AbnormalSensitiveGroupMembership ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|AbnormalSensitiveGroupMembershipChangeSecurityAlert|Suspicious modification of sensitive groups|5|start=2018-10-29T09:19:43.3013729Z app=GroupMembershipChangeEvent suser=user1 msg=user1 has uncharacteristically modified sensitive group memberships. externalId=2024 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/6f7e677e-f068-41e5-bada-708cd5a322b9 cs2Label=trigger cs2=new

### <a name="suspicious-replication-of-directory-services"></a>Replicação suspeita de serviços de diretório
02-21-2018  16:21:22    Auth.Error  192.168.0.220   1 2018-02-21T14:21:13.978554+00:00 CENTER CEF 6076 DirectoryServicesReplicationSecu ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|DirectoryServicesReplicationSecurityAlert|Malicious replication of directory services|10|start=2018-02-21T14:19:03.9975656Z app=Drsr shost=CLIENT1 msg=Malicious replication requests were successfully performed by user1, from CLIENT1 against DC1. outcome=Success externalId=2006 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/cb95648e-1b6f-4d3b-81b9-7605532787d7 cs2Label=trigger cs2=new

### <a name="suspicious-replication-request-potential-dcshadow-attack"></a>Solicitação de replicação suspeita (possível ataque DCShadow)
07-12-2018  11:18:37    Auth.Error  192.168.0.200    1 2018-07-12T08:18:32.265989+00:00 DC1 CEF 3868 DirectoryServicesRogueReplicatio ï»¿0|Microsoft|Azure ATP|2.40.0.0|DirectoryServicesRogueReplicationSecurityAlert| **Solicitação de replicação suspeita (possível ataque DcShadow)** |10|start=2018-07-12T08:17:55.3816102Z **app=Replication Activity** shost=CLIENT1 msg=CLIENT1, que não é um controlador de domínio válido em domain1.test.local, alterações enviadas para objeto do diretório em DC1. externalId=2029 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/1d5d1444-12cf-4db9-be48-39ebc2f51515 cs2Label=trigger cs2=new

### <a name="suspicious-service-creation"></a>Criação de serviço suspeito 
10-29-2018  11:20:02    Auth.Warning    192.168.0.202   1 2018-10-29T09:19:59.164874+00:00 DC3 CEF 3908 MaliciousServiceCreationSecurity ï»¿0|Microsoft|Azure ATP|2.52.5704.46184|MaliciousServiceCreationSecurityAlert|Suspicious service creation|5|start=2018-10-29T09:19:44.9471965Z app=ServiceInstalledEvent shost=CLIENT1 msg=user1 created MaliciousService in order to execute potentially malicious commands on CLIENT1. externalId=2026 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/118bbe3d-fe72-40de-80d0-2678b68aa027 cs2Label=trigger cs2=new

### <a name="suspicious-vpn-connection"></a>Conexão VPN suspeita
07-03-2018  13:13:12    Auth.Warning  192.168.0.200   1 2018-07-03T10:13:06.187834+00:00 DC1 CEF 2520 AbnormalVpnSecurityAlert ï»¿0|Microsoft|Azure ATP|2.39.0.0|AbnormalVpnSecurityAlert|Conexão VPN suspeita|5|start=2018-06-30T15:34:05.3887333Z app=VpnConnection suser=user1 msg=user1 conectado a uma VPN usando 3 computadores de 3 locais.     externalId=2025 cs1Label=url cs1=https\://contoso-corp.eng.atp.azure.com:13000/securityAlert/88c46b0e-372f-4c06-9935-67bd512c4f68 cs2Label=trigger cs2=new

### <a name="suspected-wannacry-ransomware-attack"></a>Suspeita de ataque do ransomware WannaCry
02-21-2018  16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|SuspectedWannaCryRansomwareAttack|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=Houve tentativas de autenticação do CLIENT2 em DC1 usando uma implementação de protocolo incomum. Pode ser um resultado de ferramentas mal-intencionadas usadas para executar ataques como o WannaCry. externalId=2035 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

### <a name="suspected-brute-force-attack-smb"></a>Suspeita de ataque de força bruta (SMB)
002-21-2018 16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|SuspectedBrutForceAttack|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Êxito msg=Houve tentativas de autenticação do CLIENT2 em DC1 usando uma implementação de protocolo incomum. Pode ser um resultado de ferramentas mal-intencionadas usadas para executar ataques como o Hydra. externalId=2033 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

### <a name="suspected-use-of-metasploit-hacking-framework"></a>Suspeita de uso da estrutura de hacker Metasploit
002-21-2018 16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|SuspectedAttackUsingMetasploit|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Êxito msg=Houve tentativas de autenticação do CLIENT2 em DC1 usando uma implementação de protocolo incomum. Pode ser um resultado de ferramentas mal-intencionadas usadas para executar ataques como o Metasploit. externalId=2034 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

### <a name="suspected-overpass-the-hash-attack-kerberos"></a>Suspeita de ataque de Overpass-the-Hash (Kerberos)
002-21-2018 16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|SuspectedOverPassTheHashAttack|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Êxito msg=Houve tentativas de autenticação do CLIENT2 em DC1 usando uma implementação de protocolo incomum. Pode ser o resultado de ações mal-intencionadas que usam o protocolo Kerberos. externalId=2002 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

### <a name="user-and-ip-address-reconnaissance-smb"></a>Reconhecimento de endereço IP e de usuário (SMB) 
002-21-2018 16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|ReconnaissanceusingSMBSessionEnumeration|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Êxito msg=Houve tentativas de autenticação do CLIENT2 em DC1 usando uma implementação de protocolo incomum. Pode ser um resultado de ferramentas mal-intencionadas usadas para executar ataques como o Metasploit. externalId=2034 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label=trigger cs2=new

## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
