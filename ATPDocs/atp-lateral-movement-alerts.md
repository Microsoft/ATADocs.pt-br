---
title: Alertas de segurança de movimento lateral do ATP do Azure | Microsoft Docs
d|Description: This article explains the Azure ATP alerts issued when attacks typically part of lateral movement phase efforts are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/15/2019
ms.topic: tutorial
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 2257eb00-8614-4577-b6a1-5c65085371f2
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7816dba02c2fea07afc080c7aed5ede073c88fac
ms.sourcegitcommit: e2daa0f93d97d552cfbf1577fbd05a547b63e95b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2019
ms.locfileid: "54314305"
---
# <a name="tutorial-lateral-movement-alerts"></a>Tutorial: Alertas de movimento lateral  

Normalmente, os ataques cibernéticos são lançados contra alguma entidade acessível, como um usuário com poucos privilégios e, em seguida, se movem lateralmente com rapidez até que o invasor obtenha acesso a ativos valiosos. Os ativos valiosos podem ser contas confidenciais, administradores de domínio ou dados altamente confidenciais. O ATP do Azure identifica essas ameaças avançadas na origem ao longo de toda a cadeia de ataque e classifica-as nas seguintes fases:

1. [Reconhecimento](atp-reconnaissance-alerts.md)
2. [Credenciais comprometidas](atp-compromised-credentials-alerts.md)
3. **Movimentos laterais**
4. [Comprometimento de domínio](atp-domain-dominance-alerts.md)
5. [Exportação](atp-exfiltration-alerts.md)

Para entender melhor a estrutura e os componentes comuns de todos os alertas de segurança do ATP do Azure, confira [Understanding security alerts](understanding-security-alerts.md) (Entendendo os alertas de segurança).

Os alertas de segurança a seguir ajudam a identificar e corrigir atividades suspeitas da fase de **Movimento lateral** detectadas pelo ATP do Azure em sua rede. Neste tutorial, você aprenderá como entender, classificar, corrigir e impedir os seguintes tipos de ataques:

> [!div class="checklist"]
> * Suspeita de roubo de identidade (Pass-the-Hash) (ID 2017 externa)
> * Suspeita de roubo de identidade (Pass-the-Ticket) (ID 2018 externa)
> * Suspeita de ataque de Overpass-the-Hash (downgrade de criptografia) (ID 2008 externa)
> * Suspeita de ataque de Overpass-the-Hash (Kerberos) (ID 2002 externa)

## <a name="suspected-identity-theft-pass-the-hash-external-id-2017"></a>Suspeita de roubo de identidade (Pass-the-Hash) (ID 2017 externa)

*Nome anterior:* Roubo de identidade usando o ataque de passagem de Hash

**Descrição**

Passagem de Hash é uma técnica de movimento lateral em que os invasores roubam o hash NTLM de um usuário de um computador e o usa para acessar outro computador.

**TP, B-TP ou FP?**
1. Determine se o hash foi usado dos computadores que o usuário está usando regularmente. 
    - Se o hash foi usado dos computadores usados regularmente, **feche** o alerta como um **FP**.  
 
**Entender o escopo da violação**

1. Investigue os [computadores de origem e destino](investigate-a-computer.md) ainda mais.  
2. Investigue o [usuário comprometido](investigate-a-computer.md).
 
**Correção sugerida e etapas de prevenção**

1. Redefina a senha do usuário de origem e habilite a MFA.
2. Contêm os computadores de origem e de destino.
3. Encontre a ferramenta que realizou o ataque e remova-a.
4. Procure usuários que estavam conectados no mesmo período da atividade, pois eles também podem estar comprometidos. Redefina as senhas e habilite o MFA.

## <a name="suspected-identity-theft-pass-the-ticket-external-id-2018"></a>Suspeita de roubo de identidade (Pass-the-Ticket) (ID 2018 externa)

*Nome anterior:* Roubo de identidade usando o ataque Pass-the-Ticket

**Descrição**

Pass-the-Ticket é uma técnica de movimento lateral em que os invasores roubam um tíquete Kerberos de um computador e o usam para acessar outro computador reutilizando o tíquete roubado. Nessa detecção, um tíquete Kerberos é visto sendo usado em dois (ou mais) computadores diferentes.

**TP, B-TP ou FP?**

A resolução bem-sucedida de IPs nos computadores da organização é fundamental para identificar ataques Pass-the-Ticket de um computador para outro. 

1. Verifique se o endereço IP de um ou ambos os computadores pertence a uma sub-rede alocada de um pool de DHCP subdimensionado, por exemplo, VPN, WiFi ou VDI. 
2. O endereço IP é compartilhado (por exemplo, por um dispositivo NAT)?  
3. O sensor não está resolvendo um ou mais dos endereços IP de destino? Se um endereço IP de destino não for resolvido, isso poderá indicar que as portas certas entre os dispositivos e o sensor não estão abertas corretamente. 

    Se a resposta a uma das perguntas anteriores for **sim**, verifique se os computadores de origem e de destinos são os mesmos. Se eles forem o mesmo, esse será um **FP** e indicando que não houve nenhuma tentativa real de **Pass-the-Ticket**. 

Há aplicativos personalizados que encaminham tíquetes em nome de usuários. Esses aplicativos têm direitos de delegação para tíquetes de usuário.

1. No momento, há um tipo de aplicativo personalizado, como aquele descrito anteriormente, nos computadores de destino? Quais serviços o aplicativo está executando? Os serviços estão atuando em nome de usuários, por exemplo, acessando bancos de dados?
    - Se a resposta for sim, **feche** o alerta de segurança como uma atividade **T-BP**.
2. O computador de destino é um servidor de delegação?
    - Se a resposta for sim, **feche** o alerta de segurança e exclua esse computador como uma atividade **T-BP**.
 
**Entender o escopo da violação**

1. Investigue os [computadores de origem e de destino](investigate-a-computer.md).  
2. Investigue o [usuário comprometido](investigate-a-computer.md). 

**Correção sugerida e etapas de prevenção**

1. Redefina a senha do usuário de origem e habilite a MFA.
2. Contêm os computadores de origem e de destino.
3. Encontre a ferramenta que realizou o ataque e remova-a.
4. Procure por usuários que estavam conectados em horário próximo àquele da atividade, pois eles também podem estar comprometidos. Redefina as senhas e habilite o MFA.
5. Se o Windows Defender ATP estiver instalado – use **klist.exe purge** para excluir todos os tíquetes da sessão de logon especificada e evitar o uso dos tíquetes no futuro.

## <a name="suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008"></a>Suspeita de ataque de Overpass-the-Hash (downgrade de criptografia) (ID 2008 externa) 

*Nome anterior:* Atividade de downgrade de criptografia

**Descrição**

O downgrade de criptografia é um método para enfraquecer o Kerberos usando um downgrade de criptografia de diferentes campos do protocolo que normalmente são criptografados usando o nível mais elevado de criptografia. Um campo criptografado enfraquecido pode ser um alvo mais fácil para tentativas de força bruta offline. Vários métodos de ataque utilizam criptografias Kerberos fracas. Nessa detecção, o ATP do Azure aprende os tipos de criptografia Kerberos usados por computadores e usuários e alerta você quando é usada uma criptografia mais fraca e que seja incomum para o computador de origem e/ou o usuário e que corresponda a técnicas de ataque conhecidas. 

Em um ataque de Overpass-the-Hash, um invasor pode usar um hash roubado fraco para criar um tíquete forte, com uma solicitação de AS Kerberos. Nessa detecção, são detectadas as instâncias em que o tipo de criptografia de mensagem AS_REQ do computador de origem sofreu downgrade, em comparação com o comportamento aprendido anteriormente (o AES usado pelo computador).

**TP, B-TP ou FP?**
1. Determine se a configuração do cartão inteligente foi alterada recentemente. 
    - As contas envolvidas recentemente sofreram alterações de configurações de cartão inteligente?  
    
    Se a resposta for sim, **feche** o alerta de segurança como uma atividade **T-BP**. 

Alguns recursos legítimos não permitem codificações de criptografia forte e podem disparar o alerta. 

2. Todos os usuários do código-fonte compartilham algo? 
    1. Por exemplo, todos os membros da equipe de marketing estão acessando um recurso específico que pode fazer com que o alerta seja disparado?
    2. Verifique os recursos acessados por esses tíquetes. 
        - Confira isso no Active Directory verificando o atributo *msDS-SupportedEncryptionTypes*, da conta de serviço do recurso.
    3. Se houver apenas um recurso acessado, verifique se é um recurso válido para o acesso desses usuários.   

    Se a resposta a uma das perguntas anteriores for **sim**, provavelmente essa será uma atividade **T-BP**. Verifique se o recurso pode dar suporte a uma codificação de criptografia forte, implemente uma codificação de criptografia mais forte sempre que possível e **feche** o alerta de segurança.

**Entender o escopo da violação**

1. Investigue o [computador de origem](investigate-a-computer.md).  
2. Investigue o [usuário comprometido](investigate-a-computer.md). 

**Correção sugerida e etapas de prevenção** 

**Remediação**
1. Redefina a senha do usuário de origem e habilite a MFA. 
2. Contenha o computador de origem. 
3. Encontre a ferramenta que realizou o ataque e remova-a. 
4. Procure usuários que estavam conectados no horário da atividade, pois eles também podem estar comprometidos. Redefina as senhas e habilite a MFA  

**Prevenção**
 
1. Configure seu domínio para dar suporte à codificação de criptografia forte e remova *Usar tipos de criptografia Kerberos DES*. Saiba mais sobre [tipos de criptografia e Kerberos](https://blogs.msdn.microsoft.com/openspecification/2011/05/30/windows-configurations-for-kerberos-supported-encryption-type/). 
2. Verifique se o nível funcional do domínio está definido para dar suporte à codificação de criptografia forte.  
3. Dê preferência ao uso de aplicativos compatíveis com a codificação de criptografia forte.

## <a name="suspected-overpass-the-hash-attack-kerberos-external-id-2002"></a>Suspeita de ataque de Overpass-the-Hash (Kerberos) (ID 2002 externa) 

*Nome anterior:* Implementação incomum de protocolo Kerberos (possível ataque de overpass-the-hash)

**Descrição**

Os invasores usam ferramentas que implementam vários protocolos como SMB e Kerberos de maneiras não padrão. Embora o Microsoft Windows aceite esse tipo de tráfego de rede sem avisos, o ATP do Azure é capaz de reconhecer possíveis casos mal-intencionados. O comportamento é uma indicação do uso de técnicas como Overpass-the-Hash, força bruta e explorações avançadas de ransomware, como o WannaCry.

**TP, B-TP ou FP?**

Às vezes, os aplicativos implementam sua própria pilha de Kerberos, não de acordo com o RFC Kerberos. 

1. Verifique se o computador de origem está executando um aplicativo com sua própria pilha Kerberos, que não esteja de acordo com o Kerberos RFC.  
2. Se o computador de origem estiver executando um aplicativo desse tipo e **não** precisasse estar, corrija a configuração do aplicativo. **Feche** o alerta de segurança como uma atividade **T-BP**.  
3. Se o computador de origem estiver executando esse aplicativo e deva continuar, **feche** o alerta de segurança como uma atividade **T-BP** e exclua o computador. 

**Entender o escopo da violação**

1. Investigue o [computador de origem](investigate-a-computer.md).  
2. Se houver um [usuário de origem](investigate-a-user.md), investigue. 

**Correção sugerida e etapas de prevenção** 

1. Redefina as senhas dos usuários comprometidos e habilite a MFA.
2. Contenha o computador de origem.
3. Encontre a ferramenta que realizou o ataque e remova-a.
4. Procure usuários que estavam conectados no mesmo período da atividade suspeita, pois eles também podem estar comprometidos. Redefina as senhas e habilite o MFA.  
5. Redefina as senhas do usuário de origem e habilite a MFA.

> [!div class="nextstepaction"]
> [Tutorial de alerta de comprometimento de domínio](atp-domain-dominance-alerts.md)

## <a name="see-also"></a>Consulte Também

- [Investigar um computador](investigate-a-computer.md)
- [Trabalhando com alertas de segurança](working-with-suspicious-activities.md)
- [Trabalhando com caminhos de movimento lateral](use-case-lateral-movement-path.md)
- [Alertas de reconhecimento](atp-reconnaissance-alerts.md)
- [Alertas de credencial comprometida](atp-compromised-credentials-alerts.md)
- [Alertas de predominância de domínio](atp-domain-dominance-alerts.md)
- [Alertas de exfiltração](atp-exfiltration-alerts.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)