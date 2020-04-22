---
title: Guia de alertas de segurança do ATP do Azure
d|Description: This article provides a list of the security alerts issued by Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 01/22/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 39fbd3f42cfccd60a007b8640421a8af1c178243
ms.sourcegitcommit: 63be53de5b84eabdeb8c006438dab45bd35a4ab7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2020
ms.locfileid: "79318765"
---
# <a name="azure-atp-security-alerts"></a>Alertas de segurança do ATP do Azure

> [!NOTE]
> Os recursos do ATP do Azure explicados nesta página também podem ser acessados usando o novo [portal](https://portal.cloudappsecurity.com).

Os alertas de segurança do ATP do Azure explicam as atividades suspeitas detectadas pelo sensores do ATP do Azure em sua rede e os atores e os computadores envolvidos na cada ameaça. As listas de evidências dos alertas contêm links diretos para os computadores e os usuários envolvidos para ajudar a tornar suas investigações fáceis e diretas.

Os alertas de segurança do ATP do Azure são divididos nas categorias ou fases a seguir, assim como as fases vistas em uma cadeia de eliminação de ataque cibernético típica. Saiba mais sobre cada fase, os alertas projetados para detectar cada ataque e como usar os alertas para ajudar a proteger sua rede usando os links a seguir:

  1. [Alertas de fase de reconhecimento](atp-reconnaissance-alerts.md)
  2. [Alertas de fase de credencial comprometida](atp-compromised-credentials-alerts.md)
  3. [Alertas de fase de movimento lateral](atp-lateral-movement-alerts.md)
  4. [Alertas de fase de comprometimento de domínio](atp-domain-dominance-alerts.md)
  5. [Alertas da fase de exportação](atp-exfiltration-alerts.md)

Para saber mais sobre a estrutura e os componentes comuns de todos os alertas de segurança do ATP do Azure, confira [Entendendo os alertas de segurança](understanding-security-alerts.md).

## <a name="security-alert-name-mapping-and-unique-external-ids"></a>Mapeamento de nome do alerta de segurança e IDs externas exclusivas

A tabela a seguir lista o mapeamento entre nomes de alerta, suas IDs externas exclusivas correspondentes e suas IDs de alerta do Microsoft Cloud App Security. Quando usadas com scripts ou automação, a Microsoft recomenda o uso de IDs externas de alertas em vez de nomes de alertas, já que apenas IDs externas de alertas são permanentes e não estão sujeitas a alterações.

# <a name="external-ids"></a>[IDs externas](#tab/external)

> [!div class="mx-tdBreakAll"]
> |Novo nome do alerta de segurança|ID externa exclusiva|Severidade|MITRE ATT&CK Matrix™|
> |---|---|---|---|
> |[Reconhecimento de enumeração de conta](atp-reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)|2003|Médio|Descoberta|
> |[Exportação de dados por SMB](atp-exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030)|2030|Alta|Exportação,<br>Movimentação lateral,<br>Comando e controle|
> |[Atividade de Honeytoken](atp-compromised-credentials-alerts.md#honeytoken-activity-external-id-2014)|2014|Médio|Acesso com credenciais,<br>Descoberta|
> |[Solicitação mal-intencionada de chave mestra da API de Proteção de Dados](atp-domain-dominance-alerts.md#malicious-request-of-data-protection-api-master-key-external-id-2020)|2020|Alta|Acesso com credenciais|
> |[Reconhecimento de mapeamento de rede (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)|2007|Médio|Descoberta|
> |[Tentativa de execução remota de código](atp-domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)|2019|Médio|Execução,<br>Persistência,<br>Elevação de privilégios,<br>Evasão de defesa,<br>Movimentação lateral|
> |[Execução remota de código no DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)|2036|Médio|Elevação de privilégios,<br>Movimentação lateral|
> |[Reconhecimento de entidade de segurança (LDAP)](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)|2038|Médio|Acesso com credenciais|
> |[Suspeita de ataque de força bruta (Kerberos e NTLM)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)|2023|Médio|Acesso com credenciais|
> |[Suspeita de ataque de força bruta (LDAP)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004)|2004|Médio|Acesso com credenciais|
> |[Suspeita de ataque de força bruta (SMB)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)|2033|Médio|Movimentação lateral|
> |[Suspeita de ataque DCShadow (promoção do controlador de domínio)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-promotion-external-id-2028)|2028|Alta|Evasão de defesa|
> |[Suspeito de ataque DCShadow (solicitação de replicação do controlador de domínio)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029)|2029|Alta|Evasão de defesa|
> |[Suspeita de ataque DCSync (replicação dos serviços de diretório)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)|2006|Alta|Persistência,<br>Acesso com credenciais|
> |[Suspeita de uso de Golden Ticket (downgrade de criptografia)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)|2009|Médio|Elevação de privilégios,<br>Movimentação lateral,<br>Persistência|
> |[Suspeita de uso de Golden Ticket (dados de autorização forjados)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013)|2013|Alta|Elevação de privilégios,<br>Movimentação lateral,<br>Persistência|
> |[Suspeita de uso de Golden Ticket (conta inexistente)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)|2027|Alta|Elevação de privilégios,<br>Movimentação lateral,<br>Persistência|
> |[Suspeita de uso de Golden Ticket (anomalia de tíquete)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)|2032|Alta|Elevação de privilégios,<br>Movimentação lateral,<br>Persistência|
> |[Suspeita de uso de Golden Ticket (anomalia de tempo)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)|2022|Alta|Elevação de privilégios,<br>Movimentação lateral,<br>Persistência|
> |[Suspeita de roubo de identidade (Pass-the-Hash)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017)|2017|Alta|Movimentação lateral|
> |[Suspeita de roubo de identidade (Pass-the-Ticket)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)|2018|Alta ou média|Movimentação lateral|
> |[Suspeita de violação da autenticação NTLM](atp-lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039)|2039|Médio|Elevação de privilégios, <br>Movimentação lateral|
> |[Suspeita de ataque de retransmissão de NTLM](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)|2037|Média ou baixa se observado usando o protocolo NTLM v2 assinado|Elevação de privilégios, <br>Movimentação lateral|
> |[Suspeita de ataque Overpass-the-Hash (downgrade de criptografia)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008)|2008|Médio|Movimentação lateral|
> |[Suspeita de ataque Overpass-the-Hash (Kerberos)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)|2002|Médio|Movimentação lateral|
> |[Suspeita de ataque com chave de esqueleto (downgrade de criptografia)](atp-domain-dominance-alerts.md#suspected-skeleton-key-attack-encryption-downgrade-external-id-2010)|2010|Médio|Movimentação lateral,<br>Persistência|
> |[Uso suspeito da estrutura de hacker Metasploit](atp-compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)|2034|Médio|Movimentação lateral|
> |[Suspeita de ataque do ransomware WannaCry](atp-compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)|2035|Médio|Movimentação lateral|
> |[Adições suspeitas a grupos confidenciais](atp-domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024)|2024|Médio|Acesso com credenciais,<br>Persistência|
> |[Comunicação suspeita por DNS](atp-exfiltration-alerts.md#suspicious-communication-over-dns-external-id-2031)|2031|Médio|Exfiltração|
> |[Criação de serviço suspeito](atp-domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)|2026|Médio|Execução,<br>Persistência,<br>Elevação de privilégios,<br>Evasão de defesa,<br>Movimentação lateral|
> |[Conexão de VPN suspeita](atp-compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)|2025|Médio|Persistência,<br>Evasão de defesa|
> |[Reconhecimento de usuário e de associação a um grupo (SAMR)](atp-reconnaissance-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)|2021|Médio|Descoberta|
> |[Reconhecimento de endereço IP e de usuário (SMB)](atp-reconnaissance-alerts.md#user-and-ip-address-reconnaissance-smb-external-id-2012)|2012|Médio|Descoberta|

# <a name="cloud-app-security-ids"></a>[IDs do Cloud App Security](#tab/cloud-app-security)

> [!div class="mx-tdBreakAll"]
> |Novo nome do alerta de segurança|ID do alerta do Cloud App Security|
> |---|---|
> |[Reconhecimento de enumeração de conta](atp-reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)|ALERT_EXTERNAL_AATP_ACCOUNT_ENUMERATION_SECURITY_ALERT|
> |[Exportação de dados por SMB](atp-exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030)|ALERT_EXTERNAL_AATP_SMB_DATA_EXFILTRATION_SECURITY_ALERT|
> |[Atividade de Honeytoken](atp-compromised-credentials-alerts.md#honeytoken-activity-external-id-2014)|ALERT_EXTERNAL_AATP_HONEYTOKEN_ACTIVITY_SECURITY_ALERT|
> |[Solicitação mal-intencionada de chave mestra da API de Proteção de Dados](atp-domain-dominance-alerts.md#malicious-request-of-data-protection-api-master-key-external-id-2020)|ALERT_EXTERNAL_AATP_RETRIEVE_DATA_PROTECTION_BACKUP_KEY_SECURITY_ALERT|
> |[Reconhecimento de mapeamento de rede (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)|ALERT_EXTERNAL_AATP_DNS_RECONNAISSANCE_SECURITY_ALERT|
> |[Tentativa de execução remota de código](atp-domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)|ALERT_EXTERNAL_AATP_REMOTE_EXECUTION_SECURITY_ALERT|
> |[Execução remota de código no DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)|ALERT_EXTERNAL_AATP_DNS_REMOTE_CODE_EXECUTION_SECURITY_ALERT|
> |[Reconhecimento de entidade de segurança (LDAP)](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)|ALERT_EXTERNAL_AATP_LDAP_SEARCH_RECONNAISSANCE_SECURITY_ALERT|
> |[Suspeita de ataque de força bruta (Kerberos e NTLM)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)|ALERT_EXTERNAL_AATP_BRUTE_FORCE_SECURITY_ALERT|
> |[Suspeita de ataque de força bruta (LDAP)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004)|ALERT_EXTERNAL_AATP_LDAP_BRUTE_FORCE_SECURITY_ALERT|
> |[Suspeita de ataque de força bruta (SMB)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)|ALERT_EXTERNAL_AATP_ABNORMAL_SMB_BRUTE_FORCE_SECURITY_ALERT|
> |[Suspeita de ataque DCShadow (promoção do controlador de domínio)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-promotion-external-id-2028)|ALERT_EXTERNAL_AATP_DIRECTORY_SERVICES_ROGUE_PROMOTION_SECURITY_ALERT|
> |[Suspeito de ataque DCShadow (solicitação de replicação do controlador de domínio)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029)|ALERT_EXTERNAL_AATP_DIRECTORY_SERVICES_ROGUE_REPLICATION_SECURITY_ALERT|
> |[Suspeita de ataque DCSync (replicação dos serviços de diretório)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)|ALERT_EXTERNAL_AATP_DIRECTORY_SERVICES_REPLICATION_SECURITY_ALERT|
> |[Suspeita de uso de Golden Ticket (downgrade de criptografia)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)|ALERT_EXTERNAL_AATP_GOLDEN_TICKET_ENCRYPTION_DOWNGRADE_SECURITY_ALERT|
> |[Suspeita de uso de Golden Ticket (dados de autorização forjados)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013)|ALERT_EXTERNAL_AATP_FORGED_PAC_SECURITY_ALERT|
> |[Suspeita de uso de Golden Ticket (conta inexistente)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)|ALERT_EXTERNAL_AATP_FORGED_PRINCIPAL_SECURITY_ALERT|
> |[Suspeita de uso de Golden Ticket (anomalia de tíquete)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)|ALERT_EXTERNAL_AATP_GOLDEN_TICKET_SIZE_ANOMALY_SECURITY_ALERT|
> |[Suspeita de uso de Golden Ticket (anomalia de tempo)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)|ALERT_EXTERNAL_AATP_GOLDEN_TICKET_SECURITY_ALERT|
> |[Suspeita de roubo de identidade (Pass-the-Hash)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017)|ALERT_EXTERNAL_AATP_PASS_THE_HASH_SECURITY_ALERT|
> |[Suspeita de roubo de identidade (Pass-the-Ticket)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)|ALERT_EXTERNAL_AATP_PASS_THE_TICKET_SECURITY_ALERT|
> |[Suspeita de violação da autenticação NTLM](atp-lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039)|ALERT_EXTERNAL_AATP_ABNORMAL_NTLM_SIGNING_SECURITY_ALERT|
> |[Suspeita de ataque de retransmissão de NTLM](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)|ALERT_EXTERNAL_AATP_NTLM_RELAY_SECURITY_ALERT|
> |[Suspeita de ataque Overpass-the-Hash (downgrade de criptografia)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008)|ALERT_EXTERNAL_AATP_OVERPASS_THE_HASH_ENCRYPTION_DOWNGRADE_SECURITY_ALERT|
> |[Suspeita de ataque Overpass-the-Hash (Kerberos)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)|ALERT_EXTERNAL_AATP_ABNORMAL_KERBEROS_OVERPASS_THE_HASH_SECURITY_ALERT|
> |[Suspeita de ataque com chave de esqueleto (downgrade de criptografia)](atp-domain-dominance-alerts.md#suspected-skeleton-key-attack-encryption-downgrade-external-id-2010)|ALERT_EXTERNAL_AATP_SKELETON_KEY_ENCRYPTION_DOWNGRADE_SECURITY_ALERT|
> |[Uso suspeito da estrutura de hacker Metasploit](atp-compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)|ALERT_EXTERNAL_AATP_ABNORMAL_SMB_METASPLOIT_SECURITY_ALERT|
> |[Suspeita de ataque do ransomware WannaCry](atp-compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)|ALERT_EXTERNAL_AATP_ABNORMAL_SMB_WANNA_CRY_SECURITY_ALERT|
> |[Adições suspeitas a grupos confidenciais](atp-domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024)|ALERT_EXTERNAL_AATP_ABNORMAL_SENSITIVE_GROUP_MEMBERSHIP_CHANGE_SECURITY_ALERT|
> |[Comunicação suspeita por DNS](atp-exfiltration-alerts.md#suspicious-communication-over-dns-external-id-2031)|ALERT_EXTERNAL_AATP_DNS_SUSPICIOUS_COMMUNICATION_SECURITY_ALERT|
> |[Criação de serviço suspeito](atp-domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)|ALERT_EXTERNAL_AATP_MALICIOUS_SERVICE_CREATION_SECURITY_ALERT|
> |[Conexão de VPN suspeita](atp-compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)|ALERT_EXTERNAL_AATP_ABNORMAL_VPN_SECURITY_ALERT|
> |[Reconhecimento de usuário e de associação a um grupo (SAMR)](atp-reconnaissance-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)|ALERT_EXTERNAL_AATP_SAMR_RECONNAISSANCE_SECURITY_ALERT|
> |[Reconhecimento de endereço IP e de usuário (SMB)](atp-reconnaissance-alerts.md#user-and-ip-address-reconnaissance-smb-external-id-2012)|ALERT_EXTERNAL_AATP_ENUMERATE_SESSIONS_SECURITY_ALERT|

> [!NOTE]
> Para desabilitar um alerta de segurança, contate o suporte.

## <a name="see-also"></a>Confira Também

- [Trabalhando com alertas de segurança](working-with-suspicious-activities.md)
- [Entender os alertas de segurança](understanding-security-alerts.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
