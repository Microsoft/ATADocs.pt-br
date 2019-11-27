---
title: Alertas de segurança da fase de reconhecimento do ATP do Azure | Microsoft Docs
d|Description: This article explains the Azure ATP alerts issued when attacks typically part of reconnaissance phase efforts are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 05/30/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: e9cf68d2-36bd-4b0d-b36e-7cf7ded2618e
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b19abab8774f79d18b9d82b4048625dd72b3af43
ms.sourcegitcommit: be4525a93601d9356a4e487398262a2ffaf8c202
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2019
ms.locfileid: "74206223"
---
# <a name="tutorial-reconnaissance-alerts"></a>Tutorial: Alertas de reconhecimento  

Normalmente, os ataques cibernéticos são lançados contra alguma entidade acessível, como um usuário com poucos privilégios e, em seguida, se movem lateralmente com rapidez até que o invasor obtenha acesso a ativos valiosos. Os ativos valiosos podem ser contas confidenciais, administradores de domínio ou dados altamente confidenciais. O ATP do Azure identifica essas ameaças avançadas na origem ao longo de toda a cadeia de ataque e classifica-as nas seguintes fases:

1. **Reconhecimento**
2. [Credenciais comprometidas](atp-compromised-credentials-alerts.md)
3. [Movimentos laterais](atp-lateral-movement-alerts.md)
4. [Comprometimento de domínio](atp-domain-dominance-alerts.md)
5. [Exportação](atp-exfiltration-alerts.md) 

Para entender melhor a estrutura e os componentes comuns de todos os alertas de segurança do ATP do Azure, confira [Understanding security alerts](understanding-security-alerts.md) (Entendendo os alertas de segurança).

Os alertas de segurança a seguir ajudam você a identificar e corrigir atividades suspeitas da fase de **Reconhecimento** detectadas pelo ATP do Azure em sua rede.

Neste tutorial, aprenda como entender, classificar, corrigir e impedir os seguintes tipos de ataques:

> [!div class="checklist"]
> * Reconhecimento de enumeração de conta (ID 2003 externa)
> * Reconhecimento de mapeamento de rede (DNS) (ID 2007 externa)
> * Reconhecimento de entidade de segurança (LDAP) (ID 2038 externa)
> * Reconhecimento de endereço IP e de usuário (SMB) (ID 2012 externa)
> * Reconhecimento de usuário e de associação a um grupo (SAMR) (ID 2021 externa)
 

## <a name="account-enumeration-reconnaissance-external-id-2003"></a>Reconhecimento de enumeração de conta (ID 2003 externa) 


*Nome anterior:* Reconhecimento de enumeração de conta

**Descrição**

No reconhecimento de enumeração de conta, um invasor usa um dicionário com milhares de nomes de usuário ou ferramentas como o KrbGuess para tentar adivinhar nomes de usuário no domínio.

**Kerberos**: O invasor faz solicitações Kerberos usando esses nomes para tentar localizar um nome de usuário válido no domínio. Quando uma adivinhação determina um nome de usuário com êxito, o invasor recebe o erro do Kerberos **Pré-autenticação necessária** em vez de **Entidade de segurança desconhecida**.

**NTLM**: O invasor faz solicitações de autenticação NTLM usando o dicionário de nomes para tentar localizar um nome de usuário válido no domínio. Quando uma adivinhação determina com êxito um nome de usuário, o invasor obtém o erro do NTLM **WrongPassword (0xc000006a)** em vez de **NoSuchUser (0xc0000064)** .

Nessa detecção de alerta, o ATP do Azure detecta de onde veio o ataque de enumeração de conta, o número total de tentativas de adivinhação e quantas tentativas foram correspondidas. Se houver muitos usuários desconhecidos, o Azure ATP considerará isso uma atividade suspeita.

**TP, B-TP ou FP**

Alguns aplicativos e servidores consultam controladores de domínio para determinar se as contas existem em cenários de uso legítimo.

Para determinar se essa consulta foi um **TP**, **BTP** ou **FP**, clique no alerta para acessar a página de detalhes:

1. Verifique se o computador de origem deveria ter realizado esse tipo de consulta. Exemplos de um **B-TP**, nesse caso, podem ser servidores Microsoft Exchange ou sistemas de recursos humanos.

2. Verifique os domínios de conta.
   - Há usuários adicionais que pertencem a um domínio diferente? 
     <br>Um erro de configuração do servidor, como Exchange, Skype ou ADSF, pode causar a presença de usuários adicionais que pertençam a domínios diferentes.
   - Examine a configuração do serviço com problema para corrigir o erro de configuração.

     Se você respondeu **sim** às perguntas acima, essa é uma atividade **B-TP**. *Feche* o alerta de segurança.<br>

Como próxima etapa, examine o computador de origem: 

1. Há algum script ou aplicativo em execução no computador de origem que possa estar gerando esse comportamento?  
   - Trata-se de um script antigo em execução com credenciais antigas? <br>Em caso afirmativo, interrompa e edite ou exclua o script. 
   - O aplicativo é um script ou um aplicativo administrativo ou de segurança que deve ser executado no ambiente?
 
     Se você respondeu **sim** à pergunta anterior, *feche* o alerta de segurança e exclua esse computador. Provavelmente, essa é uma atividade **B-TP**.

Agora, examine as contas:<br>
<br>Os invasores são conhecidos por usar um dicionário de nomes de conta aleatórios para localizar nomes de conta existentes em uma organização.

1. As contas inexistentes são familiares?  
   - Se as contas inexistentes forem familiares, talvez sejam contas desabilitadas ou pertencentes a funcionários que saíram da empresa.
   - Verifique se há um aplicativo ou script que possa determinar quais contas ainda existem no Active Directory.

     Se você respondeu **Sim** a uma das perguntas anteriores, *feche* o alerta de segurança. Provavelmente, essa é uma atividade **B-TP**.

2. Se qualquer uma das tentativas de suposição corresponder nomes de contas existentes, o invasor sabe da existência de contas em seu ambiente e pode tentar usar força bruta para acessar seu domínio usando os nomes de usuário descobertos. 
    - Verifique os nomes de conta que foram adivinhados para ver se há atividades suspeitas adicionais. 
    - Verifique se todas as contas correspondentes são contas confidenciais.

### <a name="understand-the-scope-of-the-breach"></a>Entender o escopo da violação

1. Investigue o computador de origem
1. Se uma das tentativas de adivinhação corresponder a nomes de contas existentes, o invasor saberá da existência das contas em seu ambiente e poderá usar a força bruta para tentar acessar seu domínio usando os nomes de usuário descobertos. Investigue as contas existentes usando o [guia de investigação do usuário](investigate-a-user.md).
    > [!NOTE]
    > Examine a evidência para conhecer o protocolo de autenticação usado. Se a autenticação NTLM tiver sido usada, habilite a auditoria NTLM do evento 8004 do Windows no controlador de domínio para determinar o servidor de recursos que os usuários tentaram acessar.<br>
    > O evento 8004 do Windows é o evento de autenticação NTLM que inclui informações sobre o computador de origem, a conta de usuário e o servidor que a conta de usuário de origem tentou acessar. <br>
    > A ATP do Azure captura os dados do computador de origem com base no Evento 4776 do Windows, que contém o nome do computador de origem definido pelo computador. Usando o evento 4776 do Windows para capturar essas informações, o campo de origem de informações é ocasionalmente substituído pelo dispositivo ou software e só exibe a Estação de trabalho ou o MSTSC como a fonte de informações. Além disso, o computador de origem pode não existir de fato em sua rede. Isso é possível porque os adversários geralmente se destinam a servidores abertos, acessíveis pela Internet de fora da rede, depois o utilizam para enumerar os usuários. Se você tiver com frequência dispositivos que são exibidos como Estação de trabalho ou MSTSC, habilite a auditoria NTLM nos controladores de domínio para obter o nome do servidor do recurso acessado. Você também deve investigar esse servidor, verificar se está aberto na Internet e, se possível, fechá-lo.

1. Depois de saber qual servidor enviou a validação de autenticação, investigue-o verificando eventos como o Evento 4624 do Windows para compreender melhor o processo de autenticação. 

1. Verifique se esse servidor está exposto à Internet usando quaisquer portas abertas. Por exemplo, o servidor aberto está usando o RDP para a Internet? 

### <a name="suggested-remediation-and-steps-for-prevention"></a>Correção sugerida e etapas de prevenção

1. Contém o [computador](investigate-a-computer.md) de origem. 
    1. Encontre a ferramenta que realizou o ataque e remova-a.
    1. Procure usuários que estavam conectados no mesmo período em que a atividade ocorreu, pois eles também podem estar comprometidos. 
    1. Redefina as senhas e habilite o MFA.
1. Imponha [senhas complexas e longas](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) na organização. As senhas complexas e longas fornecem o primeiro nível de segurança necessário contra ataques de força bruta. Os ataques de força bruta geralmente são a próxima etapa na cadeia de ataque cibernético após a enumeração. 

## <a name="network-mapping-reconnaissance-dns-external-id-2007"></a>Reconhecimento de mapeamento de rede (DNS) (ID 2007 externa) 

*Nome anterior:* Reconhecimento usando DNS

**Descrição**

O servidor DNS contém um mapa de todos os computadores, endereços IP e serviços em sua rede. Essas informações são usadas pelos invasores para mapear sua estrutura de rede e visar computadores interessantes para etapas posteriores no ataque. 
 
Há vários tipos de consulta no protocolo DNS. Esse alerta de segurança do ATP do Azure detecta solicitações suspeitas, seja em solicitações que usam uma AXFR (transferência) proveniente de servidores não DNS ou naquelas que usam uma quantidade excessiva de solicitações.

**Período de aprendizado**

Esse alerta tem um período de aprendizado de oito dias, a partir do momento em que o controlador de domínio inicia o monitoramento. 

**TP, B-TP ou FP**

1. Verifique se o computador de origem é um servidor DNS.

    - Se o computador de origem **for** um servidor DNS, feche o alerta de segurança como um **FP**. 
    - Para evitar futuros **FPs**, verifique se a porta UDP 53 está **aberta** entre o sensor do ATP do Azure e o computador de origem.

Verificadores de segurança e aplicativos legítimos podem gerar consultas DNS. 

1. Verifique se o computador de origem deve gerar esse tipo de atividade.

    - Se o computador de origem precisar gerar esse tipo de atividade, **feche** o alerta de segurança e exclua o computador como uma atividade **B-TP**.

**Entender o escopo da violação**

1. Investigue o [computador de origem](investigate-a-computer.md). 

**Correção sugerida e etapas de prevenção**

**Correção:**

- Contenha o computador de origem. 
    - Encontre a ferramenta que realizou o ataque e remova-a.
    - Procure usuários que estavam conectados no mesmo período em que a atividade ocorreu, pois eles também podem estar comprometidos. Redefina as senhas e habilite o MFA.

**Prevenção:**<br>

é importante evitar ataques futuros que usem consultas AXFR protegendo seu servidor DNS interno.

- Proteja seu servidor DNS interno para impedir o reconhecimento usando DNS desabilitando a transferências de zona ou [restringindo as transferências de zona](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649273(v=ws.10)) apenas a endereços IP especificados. A modificação de transferências de zona é uma tarefa entre uma lista de verificação que deve ser resolvida para [proteger seus servidores DNS contra ataques internos e externos](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649273(v=ws.10)).

## <a name="security-principal-reconnaissance-ldap-external-id-2038"></a>Reconhecimento de entidade de segurança (LDAP) (ID 2038 externa)

**Descrição**

O reconhecimento de entidade de segurança é usado pelos invasores para obter informações críticas sobre o ambiente de domínio. As informações que ajudam os invasores a mapear a estrutura de domínio, bem como identificar contas privilegiadas para uso em etapas posteriores em sua cadeia de encerramento do ataque. O protocolo LDAP (Lightweight Directory Access Protocol) é um dos métodos mais populares usados para fins legítimos e mal-intencionados para consultar o Active Directory Domain Services.  O reconhecimento de entidade de segurança focada no LDAP é normalmente usado como a primeira fase de um ataque Kerberoasting. Os ataques de Kerberoasting são usados para obter uma lista de destino de SPNs (nome da entidade de serviço), que os invasores tentam, então, obter tíquetes do TGS (servidor de concessão de tíquete).

Para permitir que o ATP do Azure crie o perfil com precisão e aprenda os usuários legítimos, nenhum alerta desse tipo é acionado nos primeiros 10 dias após a implantação do ATP do Azure. Depois que a fase de aprendizado inicial do ATP do Azure é concluída, os alertas são gerados em computadores que executam consultas de enumeração de LDAP suspeitas ou consultas destinadas a grupos confidenciais usando métodos não observados anteriormente.  

**Período de aprendizado**

15 dias por computador, desde o dia do primeiro evento observado pelo computador. 

**TP, B-TP ou FP**

1.  Clique no computador de origem e acesse a página de perfil. 
    1. Este computador de origem deve gerar essa atividade? 
    2. Se o computador e a atividade forem esperados, **Feche** o alerta de segurança e exclua esse computador como uma atividade **B-TP**. 

**Entender o escopo da violação**

1.  Verifique as consultas que foram executadas (como administradores de domínio ou todos os usuários em um domínio) e determine se as consultas foram bem-sucedidas. Investigue cada pesquisa de grupo exposto por atividades suspeitas realizadas no grupo ou por usuários membros do grupo.
2. Investigue o [computador de origem](investigate-a-computer.md). 
    - Usando as consultas LDAP, verifique se todas as atividades de acesso ao recurso ocorreram em qualquer um dos SPNs expostos.

**Correção sugerida e etapas de prevenção**

1. Conter o computador de origem
    1. Encontre a ferramenta que realizou o ataque e remova-a.
    2. O computador está executando uma ferramenta de verificação que realiza várias consultas LDAP?
    3. Procure por usuários que estavam conectados em horário próximo ao que a atividade ocorreu, pois eles também podem estar comprometidos. Redefina as senhas e habilite o MFA.
2. Redefina a senha se o acesso aos recursos do SPN foi feito e executado sob uma conta de usuário (não na conta do computador).

**Etapas sugeridas específicas de Kerberoasting para prevenção e correção**

1. Forçar redefinição de senha na conta comprometida  
2. Exija o uso de [senhas longas e complexas para usuários com contas de entidade de serviço](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/minimum-password-length).  
3. [Substitua a conta de usuário pela gMSA (conta de serviço gerenciado de grupo)](https://docs.microsoft.com/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview). 

> [!NOTE]
> Os alertas LDAP (reconhecimento de entidade de segurança) são compatíveis somente com os sensores do ATP.

## <a name="user-and-ip-address-reconnaissance-smb-external-id-2012"></a>Reconhecimento de endereço IP e de usuário (SMB) (ID 2012 externa) 

*Nome anterior:* Reconhecimento usando a enumeração da sessão SMB

### <a name="description"></a>Descrição

A enumeração usando o protocolo SMB permite que invasores obtenham informações sobre onde os usuários se conectaram recentemente. Depois que os invasores tiverem essas informações, eles podem mover lateralmente na rede para obter uma determinada conta confidencial.

Nessa detecção, um alerta é acionado quando uma enumeração de sessão SMB é executada em um controlador de domínio. 

**TP, B-TP ou FP**

Aplicativos e verificadores de segurança podem consultar legitimamente os controladores de domínio para verificar se há sessões SMB abertas.

1. Esse computador de origem deve gerar atividades desse tipo?
2. Há algum tipo de verificador de segurança em execução no computador de origem?  
    Se a resposta for sim, provavelmente essa será uma atividade B-TP. *Feche* o alerta de segurança e exclua esse computador.
3. Verifique os usuários que realizaram a operação.
   Esses usuários devem executar essas ações?  
    Se a resposta for sim, *feche* o alerta de segurança como uma atividade B-TP.

**Entender o escopo da violação**

1. Investigue o computador de origem.  
2. Na página do alerta, verifique se há algum usuário exposto. Para investigar mais detalhadamente cada usuário exposto, verifique o perfil deles. Recomendamos que você comece a investigação com os usuários confidenciais e de alta prioridade de investigação.

**Correção sugerida e etapas de prevenção**

Use a [ferramenta Net Cease](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b) para proteger seu ambiente contra esse ataque.

## <a name="user-and-group-membership-reconnaissance-samr-external-id-2021"></a>Reconhecimento de usuário e de associação a um grupo (SAMR) (ID 2021 externa) 


*Nome anterior:* Reconhecimento usando consultas de serviços de diretório 

**Descrição**
 
O reconhecimento de usuário e de associação a um grupo é usado pelos invasores para mapear a estrutura de diretório e visar contas com privilégios para as próximas etapas do ataque. O protocolo SAM-R (Remoto do Gerenciador de Contas de Segurança) é um dos métodos usados para consultar o diretório para realizar esse tipo de mapeamento.  
Nessa detecção, nenhum alerta é disparado no primeiro mês após a implantação do ATP do Azure (período de aprendizado). Durante o período de aprendizado, o Azure ATP cria perfis de quais consultas SAM-R são feitas de quais computadores, de consultas de enumeração e individuais de contas confidenciais. 

**Período de aprendizado**

Quatro semanas por controlador de domínio, começando com a primeira atividade de rede de SAMR no controlador de domínio específico.

**TP, B-TP ou FP** 

1. Clique no computador de origem para acessar sua página de perfil.        
   - O computador de origem deve gerar atividades desse tipo?
     - Se sim, *feche* o alerta de segurança e exclua esse computador como uma atividade **B-TP**. 
   - Verifique os usuários que realizaram a operação.
     - Esses usuários normalmente se registram nesse computador de origem ou eles são administradores que deveriam estar realizando essas ações específicas?   
     - Verifique o perfil do usuário e suas atividades de usuário relacionadas. Entenda o comportamento normal do usuário e pesquise outras atividades suspeitas usando o [guia de investigação de usuário](investigate-a-user.md). 
    
     Se você respondeu **sim** às perguntas acima, *feche* o alerta como uma atividade **B-TP**. 
  
**Entender o escopo da violação**

1. Verifique as consultas que foram executadas (por exemplo, administradores empresariais ou administrador) e determine se elas foram bem-sucedidas.
2. Investigue cada usuário exposto usando o guia de investigação de usuário.
3. Investigue o computador de origem.  
  
**Correção sugerida e etapas de prevenção**

1. Contenha o computador de origem.
2. Localize e remova a ferramenta que executou o ataque.
3. Procure por usuários que estavam conectados em horário próximo àquele da atividade, pois eles também podem estar comprometidos. Redefina as senhas e habilite o MFA.
4. Redefina a senha do usuário de origem e habilite o MFA.
5. Aplique o acesso à rede e restrinja os clientes com permissão para fazer chamadas remotas à política de grupo SAM.

> [!NOTE]
> Para desabilitar algum alerta de segurança do ATP do Azure, entre em contato com o suporte.

> [!div class="nextstepaction"]
> [Tutorial do alerta de credencial comprometida](atp-compromised-credentials-alerts.md)

## <a name="see-also"></a>Consulte Também

- [Investigar um computador](investigate-a-computer.md)
- [Investigar um usuário](investigate-a-user.md)
- [Trabalhando com alertas de segurança](working-with-suspicious-activities.md)
- [Alertas de credencial comprometida](atp-compromised-credentials-alerts.md)
- [Alertas de movimento lateral](atp-lateral-movement-alerts.md)
- [Alertas de predominância de domínio](atp-domain-dominance-alerts.md)
- [Alertas de exfiltração](atp-exfiltration-alerts.md)
- [Referência de logs de SIEM do Azure ATP](cef-format-sa.md)
- [Trabalhando com caminhos de movimento lateral](use-case-lateral-movement-path.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
