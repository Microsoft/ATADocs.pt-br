---
title: Alertas de segurança da fase de comprometimento das credenciais do Microsoft Defender para Identidade
description: Este artigo explica os alertas do Microsoft Defender para Identidade emitidos quando são detectados ataques contra a sua organização, que são típicos da fase de comprometimento das credenciais.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1f0b06f81986eedaac03f58c9c040a0b3348c304
ms.sourcegitcommit: 3c5ca2cb13ebe6c839ede951b238261d1fc73f26
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2020
ms.locfileid: "93343545"
---
# <a name="tutorial-compromised-credential-alerts"></a>Tutorial: Alertas de credencial comprometida

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Normalmente, os ataques cibernéticos são iniciados contra qualquer entidade acessível, como um usuário com poucos privilégios e, em seguida, se movem lateralmente com rapidez até que o invasor obtenha acesso a ativos valiosos – como contas confidenciais, administradores de domínio e dados altamente confidenciais. O [!INCLUDE [Product long](includes/product-long.md)] identifica essas ameaças avançadas na origem ao longo de toda a cadeia de eliminação do ataque e classifica-as nas seguintes fases:

1. [Reconhecimento](reconnaissance-alerts.md)
1. **Credencial comprometida**
1. [Movimentos laterais](lateral-movement-alerts.md)
1. [Comprometimento de domínio](domain-dominance-alerts.md)
1. [Exportação](exfiltration-alerts.md)

Para entender melhor a estrutura e os componentes comuns de todos os alertas de segurança do [!INCLUDE [Product short](includes/product-short.md)], confira [Noções básicas sobre os alertas de segurança](understanding-security-alerts.md). Para obter informações sobre **TP (verdadeiro positivo)** , **B-TP (verdadeiro positivo benigno)** e **FP (falso positivo)** , confira as [classificações de alertas de segurança](understanding-security-alerts.md#security-alert-classifications).

Os alertas de segurança a seguir ajudam você a identificar e corrigir as atividades suspeitas da fase de **Comprometimento das credenciais** detectada pelo [!INCLUDE [Product short](includes/product-short.md)] na sua rede. Neste tutorial, você aprenderá como entender, classificar, corrigir e impedir os seguintes tipos de ataques:

> [!div class="checklist"]
>
> - [Atividade de Honeytoken (ID externa 2014)](#honeytoken-activity-external-id-2014)
> - [Suspeita de ataque de força bruta (NTLM do Kerberos) (ID externa 2023)](#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)
> - [Suspeita de ataque de força bruta (LDAP) (ID externa 2004)](#suspected-brute-force-attack-ldap-external-id-2004)
> - [Suspeita de ataque de força bruta (SMB) (ID externa 2033)](#suspected-brute-force-attack-smb-external-id-2033)
> - [Suspeita de tentativa de elevação de privilégio do Netlogon (exploração CVE-2020-1472) (ID externa 2411)](#suspected-netlogon-priv-elev-2411)
> - [Suspeita de ataque do ransomware WannaCry (ID externa 2035)](#suspected-wannacry-ransomware-attack-external-id-2035)
> - [Suspeita de uso da estrutura de hacker Metasploit (ID externa 2034)](#suspected-use-of-metasploit-hacking-framework-external-id-2034)
> - [Conexão VPN suspeita (ID externa 2025)](#suspicious-vpn-connection-external-id-2025)

<!--
> - [Suspected Kerberos SPN exposure (external ID 2410)](#suspected-kerberos-spn-exposure-external-id-2410)
-->

## <a name="honeytoken-activity-external-id-2014"></a>Atividade de Honeytoken (ID externa 2014)

*Antigo nome:* atividade de Honeytoken

**Descrição**

As contas Honeytoken são contas fictícias configuradas para identificar e rastrear atividades mal-intencionadas que envolvem essas contas. As contas Honeytoken devem ser mantidas inutilizadas, mas com um nome atraente para atrair os invasores (por exemplo, SQL-Admin). Qualquer atividade delas pode indicar comportamento mal-intencionado.

Para obter mais informações sobre contas de honeytoken, confira [Configurar exclusões de detecção e contas de honeytoken](install-step7.md).

**TP, B-TP ou FP**

1. Verifique se o proprietário do computador de origem usou a conta Honeytoken para autenticar, usando o método descrito na página de atividades suspeitas (por exemplo, Kerberos, LDAP, NTLM).

    Se o proprietário do computador de origem usou a conta de honeytoken para autenticar, usando o método exato descrito na página de alertas, *feche* o alerta de segurança, como uma atividade **B-TP**.

**Entender o escopo da violação**

1. Investigue o [usuário de origem](investigate-a-user.md).
1. Investigue o [computador de origem](investigate-a-computer.md).

    > [!NOTE]
    > Se a autenticação tiver sido feita usando o NTLM, poderá não haver informações suficientes disponíveis sobre o servidor que o computador de origem tentou acessar em alguns cenários. O [!INCLUDE [Product short](includes/product-short.md)] captura os dados do computador de origem com base no Evento 4776 do Windows, que contém o nome do computador de origem definido pelo computador.
    > Ao usar o Evento 4776 do Windows para capturar essas informações, o campo de origem dessa informação, ocasionalmente, é substituído pelo dispositivo ou software para exibir apenas Estação de trabalho ou MSTSC. Se você tiver com frequência dispositivos que são exibidos como Estação de trabalho ou MSTSC, certifique-se de habilitar a auditoria de NTLM nos controladores de domínio relevantes para obter o nome do computador de origem real.
    > Para habilitar a auditoria NTLM, ative o Evento do Windows 8004 (o evento de autenticação NTLM que inclui informações sobre o computador de origem, a conta de usuário e o servidor que o computador de origem tentou acessar).

**Correção sugerida e etapas de prevenção**

1. Contenha o computador de origem.
    - Encontre a ferramenta que realizou o ataque e remova-a.
    - Procure usuários que estavam conectados no mesmo período em que a atividade ocorreu, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.

## <a name="suspected-brute-force-attack-kerberos-ntlm-external-id-2023"></a>Suspeita de ataque de força bruta (NTLM do Kerberos) (ID externa 2023)

*Antigo nome:* falhas de autenticação suspeitas

**Descrição**

Em um ataque de força bruta, o invasor tenta a autenticação usando várias senhas em diferentes contas até que uma senha correta seja encontrada ou usando uma senha em uma pulverização de senhas de grande escala que funcione para pelo menos uma conta. Uma vez descoberta, o invasor entra usando a conta autenticada.

Nessa detecção, um alerta é disparado quando ocorrem diversas falhas de autenticação usando Kerberos ou NTLM ou ainda quando o uso de uma pulverização de senhas é detectada. Por meio do Kerberos ou NTLM, esse tipo de ataque geralmente é realizado em esquema *horizontal* , usando um pequeno conjunto de senhas com vários usuários, ou *vertical* , com um grande conjunto de senhas com poucos usuários ou uma combinação dos dois.

Em uma pulverização de senhas, depois de enumerar com êxito uma lista de usuários válidos do controlador de domínio, os invasores tentam UMA senha cuidadosamente concebida em TODAS as contas de usuário conhecidas (uma senha para várias contas). Se a pulverização de senhas inicial falhar, eles tentam novamente utilizando uma senha diferente cuidadosamente concebida, normalmente após aguardar 30 minutos entre as tentativas. Esse tempo de espera permite que os invasores evitem disparar a maioria dos limites de bloqueio de conta que se baseiam no tempo. A pulverização de senhas tornou-se rapidamente uma técnica de preferência entre os invasores e testadores de intrusão. Os ataques de pulverização de senhas se mostraram eficazes na conquista de uma entrada na organização e por fazer movimentos laterais posteriores, tentando aumentar os privilégios. O período mínimo antes que um alerta possa ser disparado é de uma semana.

**Período de aprendizado**

Uma semana

**TP, B-TP ou FP**

É importante verificar se alguma tentativa de logon terminou com uma autenticação bem-sucedida.

1. Se alguma tentativa de logon terminar com êxito, verifique se alguma das **Contas adivinhadas** é usada normalmente nesse computador de origem.
    - Há alguma chance dessas contas falharem porque uma senha incorreta foi usada?
    - Verifique com os usuários se eles geraram a atividade (falha ao fazer logon algumas vezes e, em seguida, êxito).

      Se a resposta às perguntas acima for **sim** , **feche** o alerta de segurança como uma atividade B-TP.

1. Se não houver nenhuma **Conta adivinhada** , verifique se alguma das **Contas atacadas** é normalmente usada no computador de origem.
    - Verifique se há um script em execução no computador de origem com credenciais erradas/antigas?
    - Se a resposta à pergunta anterior for **Sim** , interrompa e edite o script ou exclua-o. **Feche** o alerta de segurança como uma atividade B-TP.

**Entender o escopo da violação**

1. Investigue o computador de origem.
1. Na página de alerta, verifique quais usuários, se houver, foram adivinhados com êxito.
    - Para cada usuário adivinhado com êxito, [verifique seu perfil](investigate-a-user.md) para investigar mais.

    > [!NOTE]
    > Examine a evidência para conhecer o protocolo de autenticação usado. Se a autenticação NTLM tiver sido usada, habilite a auditoria NTLM do evento 8004 do Windows no controlador de domínio para determinar o servidor de recursos que os usuários tentaram acessar. O evento 8004 do Windows é o evento de autenticação NTLM que inclui informações sobre o computador de origem, a conta de usuário e o servidor que a conta de usuário de origem tentou acessar.
    > O [!INCLUDE [Product short](includes/product-short.md)] captura os dados do computador de origem com base no Evento 4776 do Windows, que contém o nome do computador de origem definido pelo computador. Usando o evento 4776 do Windows para capturar essas informações, o campo de origem de informações é ocasionalmente substituído pelo dispositivo ou software e só exibe a Estação de trabalho ou o MSTSC como a fonte de informações. Além disso, o computador de origem pode não existir de fato em sua rede. Isso é possível porque os adversários geralmente se destinam a servidores abertos, acessíveis pela Internet de fora da rede, depois o utilizam para enumerar os usuários. Se você tiver com frequência dispositivos que são exibidos como Estação de trabalho ou MSTSC, habilite a auditoria NTLM nos controladores de domínio para obter o nome do servidor do recurso acessado. Você também deve investigar esse servidor, verificar se está aberto na Internet e, se possível, fechá-lo.

1. Depois de saber qual servidor enviou a validação de autenticação, investigue-o verificando eventos como o Evento 4624 do Windows para compreender melhor o processo de autenticação.
1. Verifique se esse servidor está exposto à Internet usando quaisquer portas abertas.
    Por exemplo, o servidor aberto está usando o RDP para a Internet?

**Correção sugerida e etapas de prevenção**

1. Redefina as senhas dos usuários adivinhados e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Contenha o computador de origem.
    - Encontre a ferramenta que realizou o ataque e remova-a.
    - Procure usuários que estavam conectados no mesmo período em que a atividade ocorreu, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Redefina as senhas dos usuários de origem e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Imponha o uso de [senhas complexas e longas](/windows/device-security/security-policy-settings/password-policy) na organização, isso fornecerá o primeiro nível necessário de segurança contra ataques de força bruta futuros.

## <a name="suspected-brute-force-attack-ldap-external-id-2004"></a>Suspeita de ataque de força bruta (LDAP) (ID externa 2004)

*Antigo nome:* ataque de força bruta usando associação simples de LDAP

**Descrição**

Em um ataque de força bruta, o invasor tenta autenticar com muitas senhas diferentes para diferentes contas até que uma senha correta seja encontrada para pelo menos uma conta. Uma vez encontrada, um invasor pode fazer logon usando essa conta.

Nessa detecção, um alerta é disparado quando o [!INCLUDE [Product short](includes/product-short.md)] detecta um grande número de autenticações de associação simples. Esse alerta detecta ataques de força bruta realizados, seja *horizontalmente* , com um pequeno conjunto de senhas entre vários usuários, *verticalmente* , com um grande conjunto de senhas em apenas alguns usuários ou com qualquer combinação dessas duas opções.

**TP, B-TP ou FP**

É importante verificar se alguma tentativa de logon terminou com uma autenticação bem-sucedida.

1. Se quaisquer tentativas de logon terminaram com êxito, alguma das **Contas adivinhadas** serão normalmente usadas desse computador de origem?
    - Há alguma chance dessas contas falharem porque uma senha incorreta foi usada?
    - Verifique com os usuários se eles geraram a atividade (falha ao fazer logon algumas vezes e, em seguida, êxito).

        Se a resposta às perguntas anteriores for **sim** , **feche** o alerta de segurança como uma atividade B-TP.

1. Se não houver nenhuma **Conta adivinhada** , verifique se alguma das **Contas atacadas** é normalmente usada no computador de origem.
    - Verifique se há um script em execução no computador de origem com credenciais erradas/antigas?

        Se a resposta à pergunta anterior for **Sim** , interrompa e edite o script ou exclua-o. **Feche** o alerta de segurança como uma atividade B-TP.

**Entender o escopo da violação**

1. Investigue o [computador de origem](investigate-a-computer.md).
1. Na página de alerta, verifique quais usuários, se houver, foram adivinhados com êxito. Para cada usuário adivinhado com êxito, [verifique seu perfil](investigate-a-user.md) para investigar mais.

**Correção sugerida e etapas de prevenção**

1. Redefina as senhas dos usuários adivinhados e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Contenha o computador de origem.
    - Encontre a ferramenta que realizou o ataque e remova-a.
    - Procure usuários que estavam conectados no mesmo período em que a atividade ocorreu, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Redefina as senhas dos usuários de origem e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Imponha o uso de [senhas complexas e longas](/windows/device-security/security-policy-settings/password-policy) na organização, isso fornecerá o primeiro nível necessário de segurança contra ataques de força bruta futuros.
1. Evite o uso futuro do protocolo de texto não criptografado de LDAP em sua organização.

## <a name="suspected-brute-force-attack-smb-external-id-2033"></a>Suspeita de ataque de força bruta (SMB) (ID externa 2033)

*Nome anterior:* Implementação de protocolo incomum (possível uso de ferramentas mal-intencionadas, como a Hydra)

**Descrição**

Os invasores usam ferramentas que implementam vários protocolos como SMB, Kerberos e NTLM de maneiras não padrão. Embora esse tipo de tráfego de rede seja aceito pelo Windows sem avisos, o [!INCLUDE [Product short](includes/product-short.md)] tem a capacidade de reconhecer possíveis casos mal-intencionados. O comportamento é uma indicação de técnicas de força bruta.

**TP, B-TP ou FP**

1. Verifique se o computador de origem está executando uma ferramenta de ataque como Hydra.
    1. Se o computador de origem está executando uma ferramenta de ataque, esse alerta é um **TP**. Siga as instruções descritas em **Entender o escopo da violação**.

Ocasionalmente, os aplicativos implementam sua própria pilha NTLM ou SMB.

1. Verifique se o computador de origem está executando um aplicativo que implementa sua própria pilha NTLM ou SMB.
    1. Se o computador de origem encontra-se executando esse tipo de aplicativo e ele não deve continuar em execução, corrija a configuração do aplicativo conforme necessário. **Feche** o alerta de segurança como uma atividade **T-BP**.
    1. Se o computador de origem estiver executando esse aplicativo e precisar continuar, **feche** o alerta de segurança como uma atividade **B-TP** e exclua o computador.

**Entender o escopo da violação**

1. Investigue o [computador de origem](investigate-a-computer.md).
1. Investigue o [usuário de origem](investigate-a-user.md) (se houver um).

**Correção sugerida e etapas de prevenção**

1. Redefina as senhas dos usuários adivinhados e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Conter o computador de origem
    1. Encontre a ferramenta que realizou o ataque e remova-a.
    1. Pesquise usuários que estavam conectados no horário da atividade, pois eles também podem estar comprometidos.
    1. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Imponha [senhas complexas e longas](/windows/security/threat-protection/security-policy-settings/password-policy) na organização. As senhas complexas e longas fornecem o primeiro nível necessário de segurança contra ataques de força bruta futuros.
1. [Desabilitar SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

<!--
## Suspected Kerberos SPN exposure (external ID 2410)

**Description**

Attackers use tools to enumerate service accounts and their respective SPNs (Service principal names), request a Kerberos service ticket for the services, capture the Ticket Granting Service (TGS) tickets from memory and extract their hashes, and save them for later use in an offline brute force attack.

**Learning period**

None

**TP, B-TP, or FP**

1. Check if the source computer is running an attack tool, such as PowerSploit or Rubeus.
    1. If yes, it is a true positive. Follow the instructions in **Understand the scope of the breach**.
    1. If the source computer is found running that type of application, and it should continue doing so, Close the security alert as a T-BP activity, and exclude that computer.

**Understand the scope of the breach**

1. Investigate the [exposed accounts](investigate-a-user.md). Check for malicious activity or suspicious behavior for these accounts.
1. Investigate the [source computer](investigate-a-computer.md).

**Remediation:**

1. Contain the source computer.
    - Find the tool that performed the attack and remove it.
    - Look for users who were logged on around the same time as the activity occurred, as these users may also be compromised. Reset their passwords and enable MFA or, if you have configured the relevant high-risk user policies in Azure Active Directory Identity Protection, you can use the [**Confirm user compromised**](/cloud-app-security/accounts#governance-actions) action in the Cloud App Security portal.
1. Reset the passwords of the exposed users and enable MFA or, if you have configured the relevant high-risk user policies in Azure Active Directory Identity Protection, you can use the [**Confirm user compromised**](/cloud-app-security/accounts#governance-actions) action in the Cloud App Security portal.
-->

<a name="suspected-netlogon-priv-elev-2411"></a>

## <a name="suspected-netlogon-privilege-elevation-attempt-cve-2020-1472-exploitation-external-id-2411"></a>Suspeita de tentativa de elevação de privilégio do Netlogon (exploração CVE-2020-1472) (ID externa 2411)

A Microsoft publicou o [CVE-2020-1472](https://portal.msrc.microsoft.com/security-guidance/advisory/CVE-2020-1472) anunciando a existência de uma nova vulnerabilidade que permite a elevação de privilégios ao controlador de domínio.

Existe uma vulnerabilidade de elevação de privilégio quando um invasor estabelece uma conexão vulnerável de canal seguro do Netlogon com um controlador de domínio, usando o Protocolo Remoto Netlogon ( [MS-NRPC](/openspecs/windows_protocols/ms-nrpc/ff8f970f-3e37-40f7-bd4b-af7336e4792f)), também conhecido como *Vulnerabilidade de Elevação de Privilégio do Netlogon*.

**Período de aprendizado**

Nenhum

**TP, B-TP ou FP**

Se o computador de origem for um DC (controlador de domínio), uma resolução com falha ou de baixa certeza poderá impedir que o [!INCLUDE [Product short](includes/product-short.md)] consiga confirmar a identificação.

1. Se o computador de origem for um controlador de domínio, **Fechar** o alerta como uma atividade  **B-TP** .

1. Se este computador de origem deve gerar esse tipo de atividade e espera-se que continue gerando esse tipo de atividade no futuro, **Fechar** o alerta de segurança como uma atividade **B-TP** e excluir o computador para evitar alertas benignos adicionais.

Caso contrário, considere esse alerta um  **TP**  e siga as instruções em  **Entender o escopo da violação**.

**Entender o escopo da violação**

1. Investigue o [computador de origem](investigate-a-computer.md), verifique se há scripts ou ferramentas mal-intencionados que fizeram a conexão com o DC.

1. Investigue o DC de destino para ver se ocorreram atividades suspeitas depois que a vulnerabilidade foi usada.

**Correção:**

1. Corrija todos os computadores, lembrando-se de aplicar atualizações de segurança.
1. Examine [nossas diretrizes](https://support.microsoft.com/help/4557222/how-to-manage-the-changes-in-netlogon-secure-channel-connections-assoc) sobre o gerenciamento de alterações na conexão de canal seguro do Netlogon que se relacionam e podem evitar essa vulnerabilidade.
1. Contenha o computador de origem.
    - Encontre a ferramenta que realizou o ataque e remova-a.

## <a name="suspected-wannacry-ransomware-attack-external-id-2035"></a>Suspeita de ataque do ransomware WannaCry (ID externa 2035)

*Nome anterior:* Implementação de protocolo incomum (possível ataque do ransomware WannaCry)

**Descrição**

Os invasores usam ferramentas que implementam vários protocolos de maneiras não padrão. Embora esse tipo de tráfego de rede seja aceito pelo Windows sem avisos, o [!INCLUDE [Product short](includes/product-short.md)] tem a capacidade de reconhecer possíveis casos mal-intencionados. O comportamento é uma indicação de técnicas usadas por ransomware avançado, como WannaCry.

**TP, B-TP ou FP**

1. Verifique se o WannaCry está em execução no computador de origem.

    - Se o WannaCry estiver em execução, esse alerta será um **TP**. Siga as instruções acima, em **Entender o escopo da violação**.

Ocasionalmente, os aplicativos implementam sua própria pilha NTLM ou SMB.

1. Verifique se o computador de origem está executando um aplicativo que implementa sua própria pilha NTLM ou SMB.
    1. Se o computador de origem encontra-se executando esse tipo de aplicativo e ele não deve continuar em execução, corrija a configuração do aplicativo conforme necessário. **Feche** o alerta de segurança como uma atividade **T-BP**.
    1. Se o computador de origem estiver executando esse aplicativo e precisar continuar, **feche** o alerta de segurança como uma atividade **T-BP** e exclua o computador.

**Entender o escopo da violação**

1. Investigue o [computador de origem](investigate-a-computer.md).
1. Investigue o [usuário comprometido](investigate-a-user.md).

**Correção sugerida e etapas de prevenção**

1. Contenha o computador de origem.
    - [Remover WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo)
    - O WanaKiwi poderá descriptografar os dados nas mãos de algum ransoware, mas apenas se o usuário não tiver reiniciado ou desligado o computador. Para obter mais informações, confira [Ransomware WannaCry](https://answers.microsoft.com/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1)
    - Pesquise usuários que estavam conectados no horário da atividade, pois é provável que eles também possam estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Corrija todos os computadores, lembrando-se de aplicar atualizações de segurança.
    - [Desabilitar SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

## <a name="suspected-use-of-metasploit-hacking-framework-external-id-2034"></a>Suspeita de uso da estrutura de hacker Metasploit (ID externa 2034)

*Nome anterior:* Implementação de protocolo incomum (possível uso das ferramentas de invasão Metasploit)

**Descrição**

Os invasores usam ferramentas que implementam vários protocolos (SMB, Kerberos, NTLM) de maneiras não padrão. Embora esse tipo de tráfego de rede seja aceito pelo Windows sem avisos, o [!INCLUDE [Product short](includes/product-short.md)] tem a capacidade de reconhecer possíveis casos mal-intencionados. O comportamento é uma indicação de técnicas como o uso da estrutura Metasploit dos hackers.

**TP, B-TP ou FP**

1. Verifique se o computador de origem está executando uma ferramenta de ataque como Metasploit ou Medusa.

1. Em caso afirmativo, é um verdadeiro positivo. Siga as instruções acima, em **Entender o escopo da violação**.

Ocasionalmente, os aplicativos implementam sua própria pilha NTLM ou SMB.

 1. Verifique se o computador de origem está executando um aplicativo que implementa sua própria pilha NTLM ou SMB.
    1. Se o computador de origem encontra-se executando esse tipo de aplicativo e ele não deve continuar em execução, corrija a configuração do aplicativo conforme necessário. **Feche** o alerta de segurança como uma atividade **T-BP**.
    1. Se o computador de origem estiver executando esse aplicativo e precisar continuar, **feche** o alerta de segurança como uma atividade **T-BP** e exclua o computador.

**Entender o escopo da violação**

1. Investigue o [computador de origem](investigate-a-computer.md).
1. Se houver um usuário de origem, [investigue-o](investigate-a-user.md).

**Correção sugerida e etapas de prevenção**

1. Redefina as senhas dos usuários adivinhados e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Contenha o computador de origem.
    1. Encontre a ferramenta que realizou o ataque e remova-a.
    1. Pesquise usuários que estavam conectados no horário da atividade, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Redefina as senhas dos usuários de origem e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. [Desabilitar SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

## <a name="suspicious-vpn-connection-external-id-2025"></a>Conexão VPN suspeita (ID externa 2025)

*Antigo nome:* conexão VPN suspeita

**Descrição**

O [!INCLUDE [Product short](includes/product-short.md)] aprende o comportamento da entidade de conexões VPN dos usuários em um período corrido de um mês.

O modelo de comportamento de VPN é baseado nos computadores nos quais os usuários fazem logon e nas localizações de onde eles se conectam.

Um alerta é aberto quando há um desvio no comportamento do usuário com base em um algoritmo de machine learning.

**Período de aprendizado**

30 dias a partir a primeira conexão de VPN e pelo menos 5 conexões de VPN nos últimos 30 dias, por usuário.

**TP, B-TP ou FP**

1. O usuário sob suspeita deveria estar executando essas operações?
    1. O usuário alterou sua localização recentemente?
    1. O usuário está viajando e se conectando de um novo dispositivo?

Se a resposta às perguntas acima for sim, **feche** o alerta de segurança como uma atividade **B-TP**.

**Entender o escopo da violação**

1. Investigue o [computador de origem](investigate-a-computer.md).
1. Se houver um usuário de origem, [investigue-o](investigate-a-user.md).

**Correção sugerida e etapas de prevenção**

1. Redefina a senha do usuário e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Considere a possibilidade de impedir que esse usuário se conecte usando VPN.
1. Considere a possibilidade de impedir que esse computador se conecte usando VPN.
1. Verifique se há outros usuários conectados por meio de VPN desses locais e também se eles foram comprometidos.

> [!div class="nextstepaction"]
> [Tutorial de alertas de movimento lateral](lateral-movement-alerts.md)

## <a name="see-also"></a>Consulte Também

- [Investigar um computador](investigate-a-computer.md)
- [Investigar um usuário](investigate-a-user.md)
- [Trabalhando com alertas de segurança](working-with-suspicious-activities.md)
- [Trabalhando com caminhos de movimento lateral](use-case-lateral-movement-path.md)
- [Alertas de reconhecimento](reconnaissance-alerts.md)
- [Alertas de movimento lateral](lateral-movement-alerts.md)
- [Alertas de predominância de domínio](domain-dominance-alerts.md)
- [Alertas de exfiltração](exfiltration-alerts.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
