---
title: Guia de alertas de segurança do ATP do Azure
description: Este artigo fornece uma lista de alertas de segurança emitidos pelo ATP do Azure.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 04/23/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f0c39f6ec4d47136324ba25c5c9bd29e0409854c
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90909976"
---
# <a name="azure-atp-security-alerts"></a>Alertas de segurança do ATP do Azure

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

> [!NOTE]
> Os recursos do ATP do Azure explicados nesta página também podem ser acessados usando o novo [portal](https://portal.cloudappsecurity.com).

Os alertas de segurança do ATP do Azure explicam as atividades suspeitas detectadas pelo sensores do ATP do Azure em sua rede e os atores e os computadores envolvidos na cada ameaça. As listas de evidências dos alertas contêm links diretos para os computadores e os usuários envolvidos para ajudar a tornar suas investigações fáceis e diretas.

Os alertas de segurança do ATP do Azure são divididos nas categorias ou fases a seguir, assim como as fases vistas em uma cadeia de eliminação de ataque cibernético típica. Saiba mais sobre cada fase, os alertas projetados para detectar cada ataque e como usar os alertas para ajudar a proteger sua rede usando os links a seguir:

  1. [Alertas de fase de reconhecimento](reconnaissance-alerts.md)
  2. [Alertas de fase de credencial comprometida](compromised-credentials-alerts.md)
  3. [Alertas de fase de movimento lateral](lateral-movement-alerts.md)
  4. [Alertas de fase de comprometimento de domínio](domain-dominance-alerts.md)
  5. [Alertas da fase de exportação](exfiltration-alerts.md)

Para saber mais sobre a estrutura e os componentes comuns de todos os alertas de segurança do ATP do Azure, confira [Entendendo os alertas de segurança](understanding-security-alerts.md).

## <a name="security-alert-name-mapping-and-unique-external-ids"></a>Mapeamento de nome do alerta de segurança e IDs externas exclusivas

A tabela a seguir lista o mapeamento entre nomes de alerta, suas IDs externas exclusivas correspondentes e suas IDs de alerta do Microsoft Cloud App Security. Quando usadas com scripts ou automação, a Microsoft recomenda o uso de IDs externas de alertas em vez de nomes de alertas, já que apenas IDs externas de alertas são permanentes e não estão sujeitas a alterações.

# <a name="external-ids"></a>[IDs externas](#tab/external)

> [!div class="mx-tdBreakAll"]
> |Nome do alerta de segurança|ID externa exclusiva|Severidade|MITRE ATT&CK Matrix&trade;|
> |---|---|---|---|
> |[Reconhecimento de enumeração de conta](reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)|2003|Média|Descoberta|
> |[Exportação de dados por SMB](exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030)|2030|Alta|Exportação,<br>Movimentação lateral,<br>Comando e controle|
> |[Atividade de Honeytoken](compromised-credentials-alerts.md#honeytoken-activity-external-id-2014)|2014|Média|Credencial de acesso,<br>Descoberta|
> |[Solicitação mal-intencionada de chave mestra da API de Proteção de Dados](domain-dominance-alerts.md#malicious-request-of-data-protection-api-master-key-external-id-2020)|2020|Alta|Credencial de acesso|
> |[Reconhecimento de mapeamento de rede (DNS)](reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)|2007|Média|Descoberta|
> |[Tentativa de execução remota de código](domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)|2019|Média|Execução,<br>Persistência,<br>Elevação de privilégios,<br>Evasão de defesa,<br>Movimento lateral|
> |[Execução remota de código no DNS](lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)|2036|Média|Elevação de privilégios,<br>Movimento lateral|
> |[Reconhecimento de entidade de segurança (LDAP)](reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)|2038|Média|Credencial de acesso|
> |[Suspeita de ataque de força bruta (Kerberos e NTLM)](compromised-credentials-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)|2023|Média|Credencial de acesso|
> |[Suspeita de ataque de força bruta (LDAP)](compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004)|2004|Média|Credencial de acesso|
> |[Suspeita de ataque de força bruta (SMB)](compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)|2033|Média|Movimento lateral|
> |[Suspeita de ataque DCShadow (promoção do controlador de domínio)](domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-promotion-external-id-2028)|2028|Alta|Evasão de defesa|
> |[Suspeito de ataque DCShadow (solicitação de replicação do controlador de domínio)](domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029)|2029|Alta|Evasão de defesa|
> |[Suspeita de ataque de DCSync (replicação de serviços de diretório)](domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)|2006|Alta|Persistência,<br>Credencial de acesso|
> |[Suspeita de uso de Golden Ticket (downgrade de criptografia)](domain-dominance-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)|2009|Média|Elevação de privilégios,<br>Movimentação lateral,<br>Persistência|
> |[Suspeita de uso de Golden Ticket (dados de autorização forjados)](domain-dominance-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013)|2013|Alta|Elevação de privilégios,<br>Movimentação lateral,<br>Persistência|
> |[Suspeita de uso de Golden Ticket (conta inexistente)](domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)|2027|Alta|Elevação de privilégios,<br>Movimentação lateral,<br>Persistência|
> |[Suspeita de uso de Golden Ticket (anomalia de tíquete)](domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)|2032|Alta|Elevação de privilégios,<br>Movimentação lateral,<br>Persistência|
> |[Suspeita de uso de Golden Ticket (anomalia de tempo)](domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)|2022|Alta|Elevação de privilégios,<br>Movimentação lateral,<br>Persistência|
> |[Suspeita de roubo de identidade (Pass-the-Hash)](lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017)|2017|Alta|Movimentação lateral|
> |[Suspeita de roubo de identidade (Pass-the-Ticket)](lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)|2018|Alto ou médio|Movimento lateral|
> |[Suspeita de violação da autenticação NTLM](lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039)|2039|Média|Elevação de privilégios, <br>Movimento lateral|
> |[Suspeita de ataque de retransmissão de NTLM](lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)|2037|Médio ou baixo se observado usando o protocolo NTLM v2 assinado|Elevação de privilégios, <br>Movimento lateral|
> |[Suspeita de ataque de Overpass-the-Hash (Kerberos)](lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)|2002|Média|Movimento lateral|
> |[Suspeita de ataque com chave de esqueleto (downgrade de criptografia)](domain-dominance-alerts.md#suspected-skeleton-key-attack-encryption-downgrade-external-id-2010)|2010|Média|Movimentação lateral,<br>Persistência|
> |[Suspeita de manipulação de pacote SMB (exploração de CVE-2020-0796) – (versão prévia)](lateral-movement-alerts.md#suspected-smb-packet-manipulation-cve-2020-0796-exploitation-external-id-2406)|2406|Alta|Movimentação lateral|
> |[Suspeita de uso da estrutura de hacker Metasploit](compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)|2034|Média|Movimentação lateral|
> |[Suspeita de ataque do ransomware WannaCry](compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)|2035|Média|Movimento lateral|
> |[Adições suspeitas a grupos confidenciais](domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024)|2024|Média|Credencial de acesso,<br>Persistência|
> |[Comunicação suspeita por DNS](exfiltration-alerts.md#suspicious-communication-over-dns-external-id-2031)|2031|Média|Exfiltração|
> |[Criação de serviço suspeito](domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)|2026|Média|Execução,<br>Persistência,<br>Elevação de privilégios,<br>Evasão de defesa,<br>Movimento lateral|
> |[Conexão de VPN suspeita](compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)|2025|Média|Persistência,<br>Evasão de defesa|
> |[Reconhecimento de usuário e de associação a um grupo (SAMR)](reconnaissance-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)|2021|Média|Descoberta|
> |[Reconhecimento de endereço IP e de usuário (SMB)](reconnaissance-alerts.md#user-and-ip-address-reconnaissance-smb-external-id-2012)|2012|Média|Descoberta|


# <a name="cloud-app-security-ids"></a>[IDs do Cloud App Security](#tab/cloud-app-security)

> [!div class="mx-tdBreakAll"]
> |Nome do alerta de segurança|ID do alerta do Cloud App Security|
> |---|---|
> |[Reconhecimento de enumeração de conta](reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)|ALERT_EXTERNAL_AATP_ACCOUNT_ENUMERATION_SECURITY_ALERT|
> |[Exportação de dados por SMB](exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030)|ALERT_EXTERNAL_AATP_SMB_DATA_EXFILTRATION_SECURITY_ALERT|
> |[Atividade de Honeytoken](compromised-credentials-alerts.md#honeytoken-activity-external-id-2014)|ALERT_EXTERNAL_AATP_HONEYTOKEN_ACTIVITY_SECURITY_ALERT|
> |[Solicitação mal-intencionada de chave mestra da API de Proteção de Dados](domain-dominance-alerts.md#malicious-request-of-data-protection-api-master-key-external-id-2020)|ALERT_EXTERNAL_AATP_RETRIEVE_DATA_PROTECTION_BACKUP_KEY_SECURITY_ALERT|
> |[Reconhecimento de mapeamento de rede (DNS)](reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)|ALERT_EXTERNAL_AATP_DNS_RECONNAISSANCE_SECURITY_ALERT|
> |[Tentativa de execução remota de código](domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)|ALERT_EXTERNAL_AATP_REMOTE_EXECUTION_SECURITY_ALERT|
> |[Execução remota de código no DNS](lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)|ALERT_EXTERNAL_AATP_DNS_REMOTE_CODE_EXECUTION_SECURITY_ALERT|
> |[Reconhecimento de entidade de segurança (LDAP)](reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)|ALERT_EXTERNAL_AATP_LDAP_SEARCH_RECONNAISSANCE_SECURITY_ALERT|
> |[Suspeita de ataque de força bruta (Kerberos e NTLM)](compromised-credentials-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)|ALERT_EXTERNAL_AATP_BRUTE_FORCE_SECURITY_ALERT|
> |[Suspeita de ataque de força bruta (LDAP)](compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004)|ALERT_EXTERNAL_AATP_LDAP_BRUTE_FORCE_SECURITY_ALERT|
> |[Suspeita de ataque de força bruta (SMB)](compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)|ALERT_EXTERNAL_AATP_ABNORMAL_SMB_BRUTE_FORCE_SECURITY_ALERT|
> |[Suspeita de ataque DCShadow (promoção do controlador de domínio)](domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-promotion-external-id-2028)|ALERT_EXTERNAL_AATP_DIRECTORY_SERVICES_ROGUE_PROMOTION_SECURITY_ALERT|
> |[Suspeito de ataque DCShadow (solicitação de replicação do controlador de domínio)](domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029)|ALERT_EXTERNAL_AATP_DIRECTORY_SERVICES_ROGUE_REPLICATION_SECURITY_ALERT|
> |[Suspeita de ataque de DCSync (replicação de serviços de diretório)](domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)|ALERT_EXTERNAL_AATP_DIRECTORY_SERVICES_REPLICATION_SECURITY_ALERT|
> |[Suspeita de uso de Golden Ticket (downgrade de criptografia)](domain-dominance-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)|ALERT_EXTERNAL_AATP_GOLDEN_TICKET_ENCRYPTION_DOWNGRADE_SECURITY_ALERT|
> |[Suspeita de uso de Golden Ticket (dados de autorização forjados)](domain-dominance-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013)|ALERT_EXTERNAL_AATP_FORGED_PAC_SECURITY_ALERT|
> |[Suspeita de uso de Golden Ticket (conta inexistente)](domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)|ALERT_EXTERNAL_AATP_FORGED_PRINCIPAL_SECURITY_ALERT|
> |[Suspeita de uso de Golden Ticket (anomalia de tíquete)](domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)|ALERT_EXTERNAL_AATP_GOLDEN_TICKET_SIZE_ANOMALY_SECURITY_ALERT|
> |[Suspeita de uso de Golden Ticket (anomalia de tempo)](domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)|ALERT_EXTERNAL_AATP_GOLDEN_TICKET_SECURITY_ALERT|
> |[Suspeita de roubo de identidade (Pass-the-Hash)](lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017)|ALERT_EXTERNAL_AATP_PASS_THE_HASH_SECURITY_ALERT|
> |[Suspeita de roubo de identidade (Pass-the-Ticket)](lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)|ALERT_EXTERNAL_AATP_PASS_THE_TICKET_SECURITY_ALERT|
> |[Suspeita de violação da autenticação NTLM](lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039)|ALERT_EXTERNAL_AATP_ABNORMAL_NTLM_SIGNING_SECURITY_ALERT|
> |[Suspeita de ataque de retransmissão de NTLM](lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)|ALERT_EXTERNAL_AATP_NTLM_RELAY_SECURITY_ALERT|
> |[Suspeita de ataque de Overpass-the-Hash (Kerberos)](lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)|ALERT_EXTERNAL_AATP_ABNORMAL_KERBEROS_OVERPASS_THE_HASH_SECURITY_ALERT|
> |[Suspeita de ataque com chave de esqueleto (downgrade de criptografia)](domain-dominance-alerts.md#suspected-skeleton-key-attack-encryption-downgrade-external-id-2010)|ALERT_EXTERNAL_AATP_SKELETON_KEY_ENCRYPTION_DOWNGRADE_SECURITY_ALERT|
> |[Suspeita de manipulação de pacote SMB (exploração de CVE-2020-0796) – (versão prévia)](lateral-movement-alerts.md#suspected-smb-packet-manipulation-cve-2020-0796-exploitation-external-id-2406)|ALERT_EXTERNAL_AATP_SMB_GHOST_SECURITY_ALERT|
> |[Suspeita de uso da estrutura de hacker Metasploit](compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)|ALERT_EXTERNAL_AATP_ABNORMAL_SMB_METASPLOIT_SECURITY_ALERT|
> |[Suspeita de ataque do ransomware WannaCry](compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)|ALERT_EXTERNAL_AATP_ABNORMAL_SMB_WANNA_CRY_SECURITY_ALERT|
> |[Adições suspeitas a grupos confidenciais](domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024)|ALERT_EXTERNAL_AATP_ABNORMAL_SENSITIVE_GROUP_MEMBERSHIP_CHANGE_SECURITY_ALERT|
> |[Comunicação suspeita por DNS](exfiltration-alerts.md#suspicious-communication-over-dns-external-id-2031)|ALERT_EXTERNAL_AATP_DNS_SUSPICIOUS_COMMUNICATION_SECURITY_ALERT|
> |[Criação de serviço suspeito](domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)|ALERT_EXTERNAL_AATP_MALICIOUS_SERVICE_CREATION_SECURITY_ALERT|
> |[Conexão de VPN suspeita](compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)|ALERT_EXTERNAL_AATP_ABNORMAL_VPN_SECURITY_ALERT|
> |[Reconhecimento de usuário e de associação a um grupo (SAMR)](reconnaissance-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)|ALERT_EXTERNAL_AATP_SAMR_RECONNAISSANCE_SECURITY_ALERT|
> |[Reconhecimento de endereço IP e de usuário (SMB)](reconnaissance-alerts.md#user-and-ip-address-reconnaissance-smb-external-id-2012)|ALERT_EXTERNAL_AATP_ENUMERATE_SESSIONS_SECURITY_ALERT|

<!-- FROM TOP TABLE |[Suspected over-pass-the-hash attack (encryption downgrade)](lateral-movement-alerts.md#suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008)|2008|Medium|Lateral movement|-->
<!-- FROM BOTTOM TABLE |[Suspected over-pass-the-hash attack (encryption downgrade)](lateral-movement-alerts.md#suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008)|ALERT_EXTERNAL_AATP_OVERPASS_THE_HASH_ENCRYPTION_DOWNGRADE_SECURITY_ALERT|-->

> [!NOTE]
> Para desabilitar um alerta de segurança, contate o suporte.

## <a name="see-also"></a>Consulte Também

- [Trabalhando com alertas de segurança](working-with-suspicious-activities.md)
- [Entender os alertas de segurança](understanding-security-alerts.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
