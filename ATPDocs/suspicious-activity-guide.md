---
title: Guia de alerta de segurança do Azure ATP | Microsoft Docs
d|Description: This article provides a list of the security alerts issued by Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 02/03/2019
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f84e49846a0c144da0674b8a4594eab2ee33efba
ms.sourcegitcommit: 9236d279f5e01424b498ce23e9d84c407ebfcdf3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/04/2019
ms.locfileid: "55689346"
---
# <a name="azure-atp-security-alerts"></a>Alertas de segurança do ATP do Azure

Os alertas de segurança do ATP do Azure explicam as atividades suspeitas detectadas pelo sensores do ATP do Azure em sua rede e os atores e os computadores envolvidos na cada ameaça.   As listas de evidências dos alertas contêm links diretos para os computadores e os usuários envolvidos para ajudar a tornar suas investigações fáceis e diretas.

Os alertas de segurança do ATP do Azure são divididos nas categorias ou fases a seguir, assim como as fases vistas em uma cadeia de eliminação de ataque cibernético típica. Saiba mais sobre cada fase, os alertas projetados para detectar cada ataque e como usar os alertas para ajudar a proteger sua rede usando os links a seguir:
  1. [Alertas de fase de reconhecimento](atp-reconnaissance-alerts.md)
  2. [Alertas de fase de credencial comprometida](atp-compromised-credentials-alerts.md)
  3. [Alertas de fase de movimento lateral](atp-lateral-movement-alerts.md)
  4. [Alertas de fase de comprometimento de domínio](atp-domain-dominance-alerts.md)
  5. [Alertas da fase de exportação](atp-exfiltration-alerts.md)

Para saber mais sobre a estrutura e os componentes comuns de todos os alertas de segurança do ATP do Azure, confira [Entendendo os alertas de segurança](understanding-security-alerts.md).

## <a name="security-alert-name-mapping-and-unique-external-ids"></a>Mapeamento de nome do alerta de segurança e IDs externas exclusivas

Na versão 2.56, todos os alertas de segurança da ATP do Azure existentes foram renomeados para facilitar a compreensão dos nomes. O mapeamento entre os nomes antigos e novos e suas externalIds exclusivas correspondentes estão listados na tabela a seguir. Quando usadas com scripts ou automação, a Microsoft recomenda o uso de IDs externas de alertas em vez de nomes de alertas, já que apenas IDs externas de alertas são permanentes e não estão sujeitas a alterações.

> [!div class="mx-tableFixed"] 

|Novo nome do alerta de segurança|Antigo nome do alerta de segurança|ID externa exclusiva|
|---------|----------|---------|
|[Reconhecimento de enumeração de conta](atp-reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)|Reconhecimento de enumeração de conta|2003|
|[Exportação de dados por SMB](atp-exfiltration-alerts.md#data-exfiltration-over-smb---preview-external-id-2030)| NA| 2030|
|[Atividade de Honeytoken](atp-compromised-credentials-alerts.md#honeytoken-activity-external-id-2014)|Atividade de Honeytoken|2014|
|[Solicitação mal-intencionada de chave mestra da API de Proteção de Dados](atp-domain-dominance-alerts.md#malicious-request-of-data-protection-api-master-key-external-id-2020)|Solicitação de informações privadas para proteção contra dados mal-intencionados|2020|
|[Reconhecimento de mapeamento de rede (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)|Reconhecimento usando DNS|2007|
|[Tentativa de execução remota de código](atp-domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)|Tentativa de execução remota de código|2019|
|[Execução remota de código sobre DNS – versão prévia](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036---preview)|NA|2036|
|[Suspeita de LDAP (ataque de força bruta)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004)|Ataque de força bruta usando associação simples LDAP|2004|
|[Suspeita de ataque de força bruta (NTLM do Kerberos)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)|Falhas de autenticação suspeitas|2023|
|[Suspeita de ataque de força bruta (SMB)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)|Implementação de protocolo incomum (possível uso de ferramentas mal-intencionadas, como a Hydra)|2033|
|[Suspeita de ataque de DCShadow (promoção do controlador de domínio)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-promotion-external-id-2028)|Promoção do controlador de domínio suspeito (possível ataque DCShadow)|2028|
|[Suspeita de ataque de DCShadow (solicitação de replicação do controlador de domínio)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029)|Solicitação de replicação de controlador de domínio suspeita (possível ataque DCShadow)|2029|
|[Suspeita de ataque de DCSync (replicação de serviços de diretório)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)|Replicação mal-intencionada de serviços de diretório|2006|
|[Suspeita de uso de Golden Ticket (downgrade de criptografia)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)|Atividade de downgrade de criptografia (possível ataque golden ticket)|2009|
|[Suspeita de uso de Golden Ticket (dados de autorização forjados)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013) |Elevação de privilégios usando dados de autorização forjados|2013|
|[Suspeita de uso de Golden Ticket (conta inexistente)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)|Golden Ticket do Kerberos – conta não existente|2027|
|[Suspeita de uso de Golden Ticket (anomalia de tíquete)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)|NA|2032|
|[Suspeita de uso de Golden Ticket (anomalia de tempo)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)|Golden Ticket do Kerberos – anomalia de tempo|2022|
|[Suspeita de roubo de identidade (Pass-the-Hash)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017)|Roubo de identidade usando o ataque de passagem de Hash|2017|
|[Suspeita de roubo de identidade (Pass-the-Ticket)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)|Roubo de identidade usando o ataque Pass-the-Ticket|2018|
|[Suspeita de ataque de Overpass-the-Hash (downgrade de criptografia)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008)|Atividade de downgrade de criptografia (possível ataque overpass-the-hash)|2008|
|[Suspeita de ataque de Overpass-the-Hash (Kerberos)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)|Implementação incomum de protocolo Kerberos (possível ataque de overpass-the-hash)|2002|
|[Suspeita de uso da estrutura de hacker Metasploit](atp-compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)|Implementação de protocolo incomum (possível uso das ferramentas de invasão Metasploit)|2034|
|[Suspeita de ataque de Skeleton Key (downgrade de criptografia)](atp-domain-dominance-alerts.md#suspected-skeleton-key-attack-encryption-downgrade-external-id-2010)|Atividade de downgrade de criptografia (possível ataque de skeleton key)|2010|
|[Suspeita de ataque do ransomware WannaCry](atp-compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)|Implementação de protocolo incomum (possível ataque do ransomware WannaCry)|2035|
|[Comunicação suspeita por DNS](atp-exfiltration-alerts.md#suspicious-communication-over-dns-external-id-2031)|Comunicação suspeita por DNS|2031|
|[Modificação suspeita de grupos confidenciais](atp-domain-dominance-alerts.md#suspicious-modification-of-sensitive-groups-external-id-2024)|Modificação suspeita de grupos confidenciais|2024|
|[Criação de serviço suspeito](atp-domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)|Criação de serviço suspeito|2026|
|[Conexão de VPN suspeita](atp-compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)|Conexão de VPN suspeita|2025|
|[Reconhecimento de usuário e de associação a um grupo (SAMR)](atp-reconnaissance-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)|Reconhecimento usando consultas de serviços de diretório|2021|
|[Reconhecimento de endereço IP e de usuário (SMB)](atp-reconnaissance-alerts.md#user-and-ip-address-reconnaissance-smb-external-id-2012)|Reconhecimento usando a enumeração da sessão SMB|2012|

> [!NOTE]
> Para desabilitar um alerta de segurança, contate o suporte.


## <a name="see-also"></a>Consulte Também
- [Trabalhando com alertas de segurança](working-with-suspicious-activities.md)
- [Entender os alertas de segurança](understanding-security-alerts.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
