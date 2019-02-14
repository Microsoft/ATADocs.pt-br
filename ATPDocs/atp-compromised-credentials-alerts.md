---
title: Alertas de segurança de fase de credenciais comprometidas do ATP do Azure | Microsoft Docs
d|Description: This article explains the Azure ATP alerts issued when attacks typical of the compromised credentials phase are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 1/15/2019
ms.topic: tutorial
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: e9cf68d2-36bd-4b0d-b36e-7cf7ded2618e
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 3696bf0d19957e95ab66bdc8d7de91184f437f80
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56077874"
---
# <a name="tutorial-compromised-credential-alerts"></a>Tutorial: Alertas de credencial comprometida  

Normalmente, os ataques cibernéticos são iniciados contra qualquer entidade acessível, como um usuário com poucos privilégios e, em seguida, se movem lateralmente com rapidez até que o invasor obtenha acesso a ativos valiosos – como contas confidenciais, administradores de domínio e dados altamente confidenciais. O ATP do Azure identifica essas ameaças avançadas na origem ao longo de toda a cadeia de ataque e classifica-as nas seguintes fases:

1. [Reconhecimento](atp-reconnaissance-alerts.md)
2. **Credencial comprometida**
3. [Movimentos laterais](atp-lateral-movement-alerts.md)
4. [Comprometimento de domínio](atp-domain-dominance-alerts.md)
5. [Exportação](atp-exfiltration-alerts.md) 

Para entender melhor a estrutura e os componentes comuns de todos os alertas de segurança do ATP do Azure, confira [Understanding security alerts](understanding-security-alerts.md) (Entendendo os alertas de segurança).

Os alertas de segurança a seguir ajudam você a identificar e corrigir atividades suspeitas da fase de **Credencial comprometida** detectada pelo ATP do Azure em sua rede. Neste tutorial, você aprenderá como entender, classificar, corrigir e impedir os seguintes tipos de ataques:

> [!div class="checklist"]
> * Atividade de Honeytoken (ID externa 2014)
> * Suspeita de ataque de força bruta (NTLM do Kerberos) (ID externa 2023)
> * Suspeita de ataque de força bruta (LDAP) (ID externa 2004)
> * Suspeita de ataque de força bruta (SMB) (ID externa 2033)
> * Suspeita de ataque do ransomware WannaCry (ID externa 2035)
> * Suspeita de uso da estrutura de hacker Metasploit (ID externa 2034)
> * Conexão VPN suspeita (ID externa 2025)

## <a name="honeytoken-activity-external-id-2014"></a>Atividade de Honeytoken (ID externa 2014) 

*Nome anterior:* Atividade de Honeytoken

**Descrição**

As contas Honeytoken são contas fictícias configuradas para identificar e rastrear atividades mal-intencionadas que envolvem essas contas. Contas de Honeytoken devem ser deixadas como não utilizadas, enquanto têm um nome atraente para atrair invasores (por exemplo, SQL-Admin). Qualquer atividade delas pode indicar comportamento mal-intencionado.

Para obter mais informações sobre contas de honeytoken, confira [Configurar exclusões de detecção e contas de honeytoken](install-atp-step7.md).

**TP, B-TP ou FP**

1. Verifique se o proprietário do computador de origem usou a conta Honeytoken para autenticar, usando o método descrito na página de atividades suspeitas (por exemplo, Kerberos, LDAP, NTLM).

    Se o proprietário do computador de origem usou a conta de honeytoken para autenticar, usando o método exato descrito na página de alertas, *feche* o alerta de segurança, como uma atividade **B-TP**.

**Entender o escopo da violação**

1. Investigue o [usuário de origem](investigate-a-user.md).
2. Investigue o [computador de origem](investigate-a-computer.md).

**Correção sugerida e etapas de prevenção**

1. Contenha o computador de origem.
    - Encontre a ferramenta que realizou o ataque e remova-a.
    - Procure usuários que estavam conectados no mesmo período em que a atividade ocorreu, pois eles também podem estar comprometidos. Redefina as senhas e habilite o MFA.

## <a name="suspected-brute-force-attack-kerberos-ntlm-external-id-2023"></a>Suspeita de ataque de força bruta (NTLM do Kerberos) (ID externa 2023)

*Nome anterior:* Falhas de autenticação suspeitas

**Descrição**

Em um ataque de força bruta, o invasor tenta a autenticação usando várias senhas em diferentes contas até que uma senha correta seja encontrada ou usando uma senha em uma pulverização de senhas de grande escala que funcione para pelo menos uma conta. Uma vez descoberta, o invasor entra usando a conta autenticada.

Nessa detecção, um alerta é disparado quando ocorrem diversas falhas de autenticação usando Kerberos ou NTLM ou ainda quando o uso de uma pulverização de senhas é detectada. Por meio do Kerberos ou NTLM, esse tipo de ataque geralmente é realizado em esquema *horizontal*, usando um pequeno conjunto de senhas com vários usuários, ou *vertical*, com um grande conjunto de senhas com poucos usuários ou uma combinação dos dois.

Em uma pulverização de senhas, depois de enumerar com êxito uma lista de usuários válidos do controlador de domínio, os invasores tentam UMA senha cuidadosamente concebida em TODAS as contas de usuário conhecidas (uma senha para várias contas). Se a pulverização de senhas inicial falhar, eles tentam novamente utilizando uma senha diferente cuidadosamente concebida, normalmente após aguardar 30 minutos entre as tentativas. Esse tempo de espera permite que os invasores evitem disparar a maioria dos limites de bloqueio de conta que se baseiam no tempo. A pulverização de senhas tornou-se rapidamente uma técnica de preferência entre os invasores e testadores de intrusão. Os ataques de pulverização de senhas se mostraram eficazes na conquista de uma entrada na organização e por fazer movimentos laterais posteriores, tentando aumentar os privilégios. O período mínimo antes que um alerta possa ser disparado é de uma semana.

**Período de aprendizado**
 <br>Uma semana

**TP, B-TP ou FP**

É importante verificar se alguma tentativa de logon terminou com uma autenticação bem-sucedida.

1. Se quaisquer tentativas de logon terminaram com êxito, verifique se qualquer uma das  **contas adivinhadas** normalmente são usadas desse computador de origem.
   - Há alguma chance dessas contas falharem porque uma senha incorreta foi usada?  
   - Verifique com os usuários se eles geraram a atividade (falha ao fazer logon algumas vezes e, em seguida, êxito). 

     Se a resposta às perguntas acima for **sim**, **feche** o alerta de segurança como uma atividade B-TP.

2. Se não houver nenhuma **Conta adivinhada**, verifique se alguma das **Contas atacadas** é normalmente usada no computador de origem.
    - Verifique se há um script em execução no computador de origem com credenciais erradas/antigas?
    - Se a resposta à pergunta anterior for **Sim**, interrompa e edite o script ou exclua-o. **Feche** o alerta de segurança como uma atividade B-TP.

**Entender o escopo da violação**

1. Investigue o computador de origem.  
2. Na página de alerta, verifique quais usuários, se houver, foram adivinhados com êxito.
    - Para cada usuário adivinhado com êxito, [verifique seu perfil](investigate-a-user.md) para investigar mais.
3. Se um alerta ocorrer muitas vezes e a autenticação tiver sido executada usando NTLM, às vezes, não haverá informações suficientes disponíveis sobre o servidor que o computador de origem tentou acessar.
    1. Para obter essas informações, certifique-se de habilitar auditoria NTLM nos controladores de domínio envolvidos.  
    2. Para habilitar auditoria NTLM, ative o evento 8004 (o evento de autenticação de NTLM que inclui informações sobre o computador de origem, a conta de usuário e o servidor que o computador de origem tentou acessar).
    3. Depois de saber qual servidor enviou a validação de autenticação, investigue-o verificando eventos como o 4624 para compreender melhor o processo de autenticação.

**Correção sugerida e etapas de prevenção**

1. Redefina as senhas dos usuários adivinhados e habilite o MFA.
2. Contenha o computador de origem.
    - Encontre a ferramenta que realizou o ataque e remova-a.
    - Procure usuários que estavam conectados no mesmo período em que a atividade ocorreu, pois eles também podem estar comprometidos. Redefina as senhas e habilite o MFA.
3. Redefina as senhas do usuário de origem e habilite a MFA.
4. Imponha o uso de [senhas complexas e longas](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) na organização, isso fornecerá o primeiro nível necessário de segurança contra ataques de força bruta futuros.

## <a name="suspected-brute-force-attack-ldap-external-id-2004"></a>Suspeita de ataque de força bruta (LDAP) (ID externa 2004) 

*Nome anterior:* Ataque de força bruta usando associação simples LDAP

**Descrição**

Em um ataque de força bruta, o invasor tenta autenticar com muitas senhas diferentes para diferentes contas até que uma senha correta seja encontrada para pelo menos uma conta. Uma vez encontrada, um invasor pode fazer logon usando essa conta.  
Nesta detecção, um alerta é disparado quando o Azure ATP detecta um grande número de autenticações de associação simples. Esse alerta detecta ataques de força bruta realizados, seja *horizontalmente*, com um pequeno conjunto de senhas entre vários usuários, *verticalmente*, com um grande conjunto de senhas em apenas alguns usuários ou com qualquer combinação dessas duas opções.

**TP, B-TP ou FP**

É importante verificar se alguma tentativa de logon terminou com uma autenticação bem-sucedida.

1. Se quaisquer tentativas de logon terminaram com êxito, alguma das  **contas adivinhadas** são normalmente usadas desse computador de origem?
   - Há alguma chance dessas contas falharem porque uma senha incorreta foi usada?  
   - Verifique com os usuários se eles geraram a atividade (falha ao fazer logon algumas vezes e, em seguida, êxito).

     Se a resposta às perguntas anteriores for **sim**, **feche** o alerta de segurança como uma atividade B-TP.

2. Se não houver nenhuma **Conta adivinhada**, verifique se alguma das **Contas atacadas** é normalmente usada no computador de origem.
   - Verifique se há um script em execução no computador de origem com credenciais erradas/antigas?

     Se a resposta à pergunta anterior for **Sim**, interrompa e edite o script ou exclua-o. **Feche** o alerta de segurança como uma atividade B-TP.

**Entender o escopo da violação**

1. Investigue o [computador de origem](investigate-a-computer.md).  
2. Na página de alerta, verifique quais usuários, se houver, foram adivinhados com êxito. Para cada usuário adivinhado com êxito, [verifique seu perfil](investigate-a-user.md) para investigar mais.

**Correção sugerida e etapas de prevenção**

1. Redefina as senhas dos usuários adivinhados e habilite o MFA.
2. Contenha o computador de origem.
    - Encontre a ferramenta que realizou o ataque e remova-a.
    - Procure usuários que estavam conectados no mesmo período em que a atividade ocorreu, pois eles também podem estar comprometidos. Redefina as senhas e habilite o MFA.
3. Redefina as senhas do usuário de origem e habilite a MFA.
4. Imponha o uso de [senhas complexas e longas](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) na organização, isso fornecerá o primeiro nível necessário de segurança contra ataques de força bruta futuros.
5. Evite o uso futuro do protocolo de texto não criptografado de LDAP em sua organização.

## <a name="suspected-brute-force-attack-smb-external-id-2033"></a>Suspeita de ataque de força bruta (SMB) (ID externa 2033) 

*Nome anterior:* Implementação de protocolo incomum (possível uso de ferramentas mal-intencionadas, como a Hydra)

**Descrição**

Os invasores usam ferramentas que implementam vários protocolos como SMB, Kerberos e NTLM de maneiras não padrão. Embora esse tipo de tráfego de rede seja aceito pelo Windows sem avisos, o Azure ATP é capaz de reconhecer possíveis casos mal-intencionados. O comportamento é uma indicação de técnicas de força bruta.

**TP, B-TP ou FP**

1. Verifique se o computador de origem está executando uma ferramenta de ataque como Hydra.
   1. Se o computador de origem está executando uma ferramenta de ataque, esse alerta é um **TP**. Siga as instruções em [Entender o escopo da violação](#understand-the-scope-of-the-breach).

Ocasionalmente, os aplicativos implementam sua própria pilha NTLM ou SMB.

1. Verifique se o computador de origem está executando um aplicativo que implementa sua própria pilha NTLM ou SMB.
    1. Se o computador de origem encontra-se executando esse tipo de aplicativo e ele não deve continuar em execução, corrija a configuração do aplicativo conforme necessário. **Feche** o alerta de segurança como uma atividade **T-BP**.
    2. Se o computador de origem estiver executando esse aplicativo e precisar continuar, **feche** o alerta de segurança como uma atividade **T-BP** e exclua o computador.

**Entender o escopo da violação**

1. Investigue o [computador de origem](investigate-a-computer.md).
2. Investigue o [usuário de origem](investigate-a-user.md) (se houver um).

**Correção sugerida e etapas de prevenção**

1. Redefina as senhas dos usuários adivinhados e habilite a autenticação multifator.
2. Conter o computador de origem
   1. Encontre a ferramenta que realizou o ataque e remova-a.
   2. Pesquise usuários que estavam conectados no horário da atividade, pois eles também podem estar comprometidos.
   3. Redefina suas senhas e habilite a autenticação multifator.
3. Imponha [senhas complexas e longas](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/password-policy) na organização. As senhas complexas e longas fornecem o primeiro nível necessário de segurança contra ataques de força bruta futuros.
4. [Desabilitar SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

## <a name="suspected-wannacry-ransomware-attack-external-id-2035"></a>Suspeita de ataque do ransomware WannaCry (ID externa 2035)

*Nome anterior:* Implementação de protocolo incomum (possível ataque do ransomware WannaCry)

**Descrição**

Os invasores usam ferramentas que implementam vários protocolos de maneiras não padrão. Embora esse tipo de tráfego de rede seja aceito pelo Windows sem avisos, o Azure ATP é capaz de reconhecer possíveis casos mal-intencionados. O comportamento é uma indicação de técnicas usadas por ransomware avançado, como WannaCry.

**TP, B-TP ou FP**

1. Verifique se o WannaCry está em execução no computador de origem. 

    - Se o WannaCry estiver em execução, esse alerta será um **TP**. Siga as instruções em [Entender o escopo da violação](#understand-the-scope-of-the-breach).

Ocasionalmente, os aplicativos implementam sua própria pilha NTLM ou SMB.

1. Verifique se o computador de origem está executando um aplicativo que implementa sua própria pilha NTLM ou SMB. 
    1. Se o computador de origem encontra-se executando esse tipo de aplicativo e ele não deve continuar em execução, corrija a configuração do aplicativo conforme necessário. **Feche** o alerta de segurança como uma atividade **T-BP**.
    2. Se o computador de origem estiver executando esse aplicativo e precisar continuar, **feche** o alerta de segurança como uma atividade **T-BP** e exclua o computador.

**Entender o escopo da violação**

1. Investigue o [computador de origem](investigate-a-computer.md).
2. Investigue o [usuário comprometido](investigate-a-user.md).

**Correção sugerida e etapas de prevenção**

1. Contenha o computador de origem.
      - [Remover WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo)
      - O WanaKiwi poderá descriptografar os dados nas mãos de algum ransomware, mas apenas se o usuário não tiver reiniciado ou desligado o computador. Para obter mais informações, confira [Ransomware WannaCry](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1)
      - Pesquise usuários que estavam conectados no horário da atividade, pois é provável que eles também possam estar comprometidos. Redefina as senhas e habilite o MFA.
2. Corrija todos os computadores, lembrando-se de aplicar atualizações de segurança. 
      - [Desabilitar SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

## <a name="suspected-use-of-metasploit-hacking-framework-external-id-2034"></a>Suspeita de uso da estrutura de hacker Metasploit (ID externa 2034)

*Nome anterior:* Implementação de protocolo incomum (possível uso das ferramentas de invasão Metasploit)

**Descrição**

Os invasores usam ferramentas que implementam vários protocolos (SMB, Kerberos, NTLM) de maneiras não padrão. Embora esse tipo de tráfego de rede seja aceito pelo Windows sem avisos, o Azure ATP é capaz de reconhecer possíveis casos mal-intencionados. O comportamento é uma indicação de técnicas como o uso da estrutura Metasploit dos hackers. 

**TP, B-TP ou FP**

1. Verifique se o computador de origem está executando uma ferramenta de ataque como Metasploit ou Medusa.

2. Em caso afirmativo, é um verdadeiro positivo. Siga as instruções em [Entender o escopo da violação](#understand-the-scope-of-the-breach).

Ocasionalmente, os aplicativos implementam sua própria pilha NTLM ou SMB.

 1. Verifique se o computador de origem está executando um aplicativo que implementa sua própria pilha NTLM ou SMB. 
    1. Se o computador de origem encontra-se executando esse tipo de aplicativo e ele não deve continuar em execução, corrija a configuração do aplicativo conforme necessário. **Feche** o alerta de segurança como uma atividade **T-BP**.
    2. Se o computador de origem estiver executando esse aplicativo e precisar continuar, **feche** o alerta de segurança como uma atividade **T-BP** e exclua o computador.

**Entender o escopo da violação**

1. Investigue o [computador de origem](investigate-a-computer.md).
2. Se houver um usuário de origem, [investigue-o](investigate-a-user.md).

**Correção sugerida e etapas de prevenção**

1. Redefina as senhas dos usuários adivinhados e habilite o MFA.
2. Contenha o computador de origem.
   1. Encontre a ferramenta que realizou o ataque e remova-a.
   2. Pesquise usuários que estavam conectados no horário da atividade, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a autenticação multifator.
3. Redefina as senhas do usuário de origem e habilite a MFA. 
4. [Desabilitar SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/) 

## <a name="suspicious-vpn-connection-external-id-2025"></a>Conexão VPN suspeita (ID externa 2025) 

*Nome anterior:* Conexão de VPN suspeita 

**Descrição**

A Azure ATP aprende o comportamento da entidade dos usuários de conexões VPN em um período corrido de um mês. 

O modelo de comportamento de VPN é baseado nos computadores nos quais os usuários fazem logon e nas localizações de onde eles se conectam. 

Um alerta é aberto quando há um desvio no comportamento do usuário com base em um algoritmo de aprendizado de máquina.

**Período de aprendizado**

30 dias a partir a primeira conexão de VPN e pelo menos 5 conexões de VPN nos últimos 30 dias, por usuário.

**TP, B-TP ou FP**

1. O usuário sob suspeita deveria estar executando essas operações?
    1. O usuário alterou sua localização recentemente?
    2. O usuário está viajando e se conectando de um novo dispositivo?

Se a resposta às perguntas acima for sim, **feche** o alerta de segurança como uma atividade **B-TP**.

**Entender o escopo da violação**

1. Investigue o [computador de origem](investigate-a-computer.md).
2. Se houver um usuário de origem, [investigue-o](investigate-a-user.md).

**Correção sugerida e etapas de prevenção**

1. Redefina a senha do usuário e habilite o MFA.
2. Considere a possibilidade de impedir que esse usuário se conecte usando VPN.
3. Considere a possibilidade de impedir que esse computador se conecte usando VPN.
4. Verifique se há outros usuários conectados por meio de VPN desses locais e também se eles foram comprometidos.

> [!div class="nextstepaction"]
> [Tutorial de alertas de movimento lateral](atp-lateral-movement-alerts.md)

## <a name="see-also"></a>Consulte Também

- [Investigar um computador](investigate-a-computer.md)
- [Investigar um usuário](investigate-a-user.md)
- [Trabalhando com alertas de segurança](working-with-suspicious-activities.md)
- [Trabalhando com caminhos de movimento lateral](use-case-lateral-movement-path.md)
- [Alertas de reconhecimento](atp-reconnaissance-alerts.md)
- [Alertas de movimento lateral](atp-lateral-movement-alerts.md)
- [Alertas de predominância de domínio](atp-domain-dominance-alerts.md)
- [Alertas de exfiltração](atp-exfiltration-alerts.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
