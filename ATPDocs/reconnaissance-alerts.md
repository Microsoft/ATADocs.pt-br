---
title: Alertas de segurança da fase de reconhecimento do Microsoft Defender para Identidade
description: Este artigo explica os alertas do Microsoft Defender para Identidade emitidos quando são detectados ataques contra a sua organização, que normalmente fazem parte dos esforços da fase de reconhecimento.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1a21762351400d298154e7dbf7503fd7d820e0a2
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93275363"
---
# <a name="tutorial-reconnaissance-alerts"></a>Tutorial: Alertas de reconhecimento

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Normalmente, os ataques cibernéticos são lançados contra alguma entidade acessível, como um usuário com poucos privilégios e, em seguida, se movem lateralmente com rapidez até que o invasor obtenha acesso a ativos valiosos. Os ativos valiosos podem ser contas confidenciais, administradores de domínio ou dados altamente confidenciais. O [!INCLUDE [Product long](includes/product-long.md)] identifica essas ameaças avançadas na origem ao longo de toda a cadeia de eliminação do ataque e classifica-as nas seguintes fases:

1. **Reconhecimento**
1. [Credenciais comprometidas](compromised-credentials-alerts.md)
1. [Movimentos laterais](lateral-movement-alerts.md)
1. [Comprometimento de domínio](domain-dominance-alerts.md)
1. [Exportação](exfiltration-alerts.md)

Para entender melhor a estrutura e os componentes comuns de todos os alertas de segurança do [!INCLUDE [Product short](includes/product-short.md)], confira [Noções básicas sobre os alertas de segurança](understanding-security-alerts.md). Para obter informações sobre **TP (verdadeiro positivo)** , **B-TP (verdadeiro positivo benigno)** e **FP (falso positivo)** , confira as [classificações de alertas de segurança](understanding-security-alerts.md#security-alert-classifications).

Os alertas de segurança a seguir ajudam você a identificar e corrigir as atividades suspeitas da fase de **Reconhecimento** detectadas pelo [!INCLUDE [Product short](includes/product-short.md)] na sua rede.

Neste tutorial, aprenda como entender, classificar, corrigir e impedir os seguintes tipos de ataques:

> [!div class="checklist"]
>
> - Reconhecimento de enumeração de conta (ID 2003 externa)
> - Reconhecimento de atributos do Active Directory (LDAP) (ID externa 2210)
> - Reconhecimento de mapeamento de rede (DNS) (ID 2007 externa)
> - Reconhecimento de entidade de segurança (LDAP) (ID 2038 externa)
> - Reconhecimento de usuário e de associação a um grupo (SAMR) (ID 2021 externa)
> - Reconhecimento de endereço IP e de usuário (SMB) (ID 2012 externa)

## <a name="account-enumeration-reconnaissance-external-id-2003"></a>Reconhecimento de enumeração de conta (ID 2003 externa)

*Nome anterior:* Reconhecimento de enumeração de conta

**Descrição**

No reconhecimento de enumeração de conta, um invasor usa um dicionário com milhares de nomes de usuário ou ferramentas como o KrbGuess para tentar adivinhar nomes de usuário no domínio.

**Kerberos** : O invasor faz solicitações Kerberos usando esses nomes para tentar localizar um nome de usuário válido no domínio. Quando uma adivinhação determina um nome de usuário com êxito, o invasor recebe o erro do Kerberos **Pré-autenticação necessária** em vez de **Entidade de segurança desconhecida**.

**NTLM** : O invasor faz solicitações de autenticação NTLM usando o dicionário de nomes para tentar localizar um nome de usuário válido no domínio. Quando uma adivinhação determina com êxito um nome de usuário, o invasor obtém o erro do NTLM **WrongPassword (0xc000006a)** em vez de **NoSuchUser (0xc0000064)** .

Nessa detecção de alerta, o [!INCLUDE [Product short](includes/product-short.md)] detecta a origem do ataque de enumeração de conta, o número total de tentativas de adivinhação e quantas tentativas foram correspondidas. Se houver muitos usuários desconhecidos, o [!INCLUDE [Product short](includes/product-short.md)] detectará isso como uma atividade suspeita.

**Período de aprendizado**

Não se aplica

**TP, B-TP ou FP**

Alguns aplicativos e servidores consultam controladores de domínio para determinar se as contas existem em cenários de uso legítimo.

Para determinar se essa consulta foi um **TP** , **BTP** ou **FP** , clique no alerta para acessar a página de detalhes:

1. Verifique se o computador de origem deveria ter realizado esse tipo de consulta. Exemplos de um **B-TP** , nesse caso, podem ser servidores Microsoft Exchange ou sistemas de recursos humanos.

1. Verifique os domínios de conta.
    - Há usuários adicionais que pertencem a um domínio diferente?  
     Um erro de configuração do servidor, como Exchange, Skype ou ADSF, pode causar a presença de usuários adicionais que pertençam a domínios diferentes.
    - Examine a configuração do serviço com problema para corrigir o erro de configuração.

    Se você respondeu **sim** às perguntas acima, essa é uma atividade **B-TP**. *Feche* o alerta de segurança.

Como próxima etapa, examine o computador de origem:

1. Há algum script ou aplicativo em execução no computador de origem que possa estar gerando esse comportamento?
    - Trata-se de um script antigo em execução com credenciais antigas?  
    Em caso afirmativo, interrompa e edite ou exclua o script.
    - O aplicativo é um script ou um aplicativo administrativo ou de segurança que deve ser executado no ambiente?

      Se você respondeu **sim** à pergunta anterior, *feche* o alerta de segurança e exclua esse computador. Provavelmente, essa é uma atividade **B-TP**.

Agora, examine as contas:

Os invasores são conhecidos por usar um dicionário de nomes de conta aleatórios para localizar nomes de conta existentes em uma organização.

1. As contas inexistentes são familiares?
    - Se as contas inexistentes forem familiares, talvez sejam contas desabilitadas ou pertencentes a funcionários que saíram da empresa.
    - Verifique se há um aplicativo ou script que possa determinar quais contas ainda existem no Active Directory.

      Se você respondeu **Sim** a uma das perguntas anteriores, *feche* o alerta de segurança. Provavelmente, essa é uma atividade **B-TP**.

1. Se qualquer uma das tentativas de suposição corresponder nomes de contas existentes, o invasor sabe da existência de contas em seu ambiente e pode tentar usar força bruta para acessar seu domínio usando os nomes de usuário descobertos.
    - Verifique os nomes de conta que foram adivinhados para ver se há atividades suspeitas adicionais.
    - Verifique se todas as contas correspondentes são contas confidenciais.

**Entender o escopo da violação**

1. Investigue o computador de origem
1. Se uma das tentativas de adivinhação corresponder a nomes de contas existentes, o invasor saberá da existência das contas em seu ambiente e poderá usar a força bruta para tentar acessar seu domínio usando os nomes de usuário descobertos. Investigue as contas existentes usando o [guia de investigação do usuário](investigate-a-user.md).
    > [!NOTE]
    > Examine a evidência para conhecer o protocolo de autenticação usado. Se a autenticação NTLM tiver sido usada, habilite a auditoria NTLM do evento 8004 do Windows no controlador de domínio para determinar o servidor de recursos que os usuários tentaram acessar.  
    > O evento 8004 do Windows é o evento de autenticação NTLM que inclui informações sobre o computador de origem, a conta de usuário e o servidor que a conta de usuário de origem tentou acessar.  
    > O [!INCLUDE [Product short](includes/product-short.md)] captura os dados do computador de origem com base no Evento 4776 do Windows, que contém o nome do computador de origem definido pelo computador. Usando o evento 4776 do Windows para capturar essas informações, o campo de origem de informações é ocasionalmente substituído pelo dispositivo ou software e só exibe a Estação de trabalho ou o MSTSC como a fonte de informações. Além disso, o computador de origem pode não existir de fato em sua rede. Isso é possível porque os adversários geralmente se destinam a servidores abertos, acessíveis pela Internet de fora da rede, depois o utilizam para enumerar os usuários. Se você tiver com frequência dispositivos que são exibidos como Estação de trabalho ou MSTSC, habilite a auditoria NTLM nos controladores de domínio para obter o nome do servidor do recurso acessado. Você também deve investigar esse servidor, verificar se está aberto na Internet e, se possível, fechá-lo.

1. Depois de saber qual servidor enviou a validação de autenticação, investigue-o verificando eventos como o Evento 4624 do Windows para compreender melhor o processo de autenticação.

1. Verifique se esse servidor está exposto à Internet usando quaisquer portas abertas. Por exemplo, o servidor aberto está usando o RDP para a Internet?

**Correção sugerida e etapas de prevenção**

1. Contém o [computador](investigate-a-computer.md) de origem.
    1. Encontre a ferramenta que realizou o ataque e remova-a.
    1. Procure usuários que estavam conectados no mesmo período em que a atividade ocorreu, pois eles também podem estar comprometidos.
    1. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Imponha [senhas complexas e longas](/windows/device-security/security-policy-settings/password-policy) na organização. As senhas complexas e longas fornecem o primeiro nível de segurança necessário contra ataques de força bruta. Os ataques de força bruta geralmente são a próxima etapa na cadeia de ataque cibernético após a enumeração.

## <a name="active-directory-attributes-reconnaissance-ldap-external-id-2210"></a>Reconhecimento de atributos do Active Directory (LDAP) (ID externa 2210)

**Descrição**

O reconhecimento do Active Directory usando LDAP é empregado pelos invasores para obter informações críticas sobre o ambiente do domínio em questão. Estas informações podem ajudar os invasores a mapear a estrutura de domínio, bem como identificar contas privilegiadas para uso em etapas posteriores na cadeia de eliminação do ataque. O protocolo LDAP é um dos métodos mais populares usados para fins legítimos e mal-intencionados para consultar o Active Directory.

**Período de aprendizado**

Não se aplica

**TP, B-TP ou FP**

1. Clique no alerta para exibir as consultas que foram executadas.
    - Verifique se o computador de origem deve efetuar essas consultas
        - Em caso afirmativo, feche o alerta de segurança como um **FP**. Se for uma atividade contínua, exclua a atividade suspeita.
1. Clique no computador de origem e acesse a página de perfil.
    - Procure qualquer atividade incomum que tenha ocorrido no momento das consultas, como os seguintes tipos de pesquisa: usuários conectados, recursos acessados e outras consultas de sondagem.
    - Se a integração do Microsoft Defender para Ponto de Extremidade estiver habilitada, clique no ícone dele para investigar o computador mais detalhadamente.
        - Procurar processos e alertas incomuns que tenham ocorrido no momento das consultas
1. Verifique as contas expostas.
    - Procure atividades incomuns.

Se você respondeu sim para as perguntas 2 ou 3, considere este alerta um **TP** e siga as instruções em **Entender o escopo da violação**.

**Entender o escopo da violação**

1. Investigue o [computador de origem](investigate-a-computer.md).
1. O computador está executando uma ferramenta de verificação que realiza várias consultas LDAP?
    - Investigue se os usuários e grupos específicos consultados no ataque são contas com privilégios ou de alto valor (ou seja, CEO, CFO, gerenciamento de TI etc.). Nesse caso, examine outras atividades no ponto de extremidade e monitore os computadores em que as contas consultadas são registradas, como eles são provavelmente destinos para a movimentação lateral.
1. Verifique as consultas e os respectivos atributos e determine se foram bem-sucedidos. Investigue cada grupo exposto, procure atividades suspeitas realizadas no grupo ou por usuários membros do grupo.
1. Você observou comportamentos de reconhecimento de SAM-R, DNS ou SMB no computador de origem?

**Correção sugerida e etapas de prevenção**

1. Conter o computador de origem
    1. Encontre a ferramenta que realizou o ataque e remova-a.
    1. Se o computador estiver executando uma ferramenta de verificação que executa uma série de consultas LDAP, procure os usuários que fizeram logon ao mesmo tempo em que a atividade ocorreu, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Redefina a senha se o acesso aos recursos do SPN foi feito e executado sob uma conta de usuário (não na conta do computador).

## <a name="network-mapping-reconnaissance-dns-external-id-2007"></a>Reconhecimento de mapeamento de rede (DNS) (ID 2007 externa)

*Nome anterior:* Reconhecimento usando DNS

**Descrição**

O servidor DNS contém um mapa de todos os computadores, endereços IP e serviços em sua rede. Essas informações são usadas pelos invasores para mapear sua estrutura de rede e visar computadores interessantes para etapas posteriores no ataque.

Há vários tipos de consulta no protocolo DNS. Esse alerta de segurança do [!INCLUDE [Product short](includes/product-short.md)] detecta solicitações suspeitas, seja em solicitações que usam uma AXFR (transferência) proveniente de servidores não DNS ou naquelas que usam uma quantidade excessiva de solicitações.

**Período de aprendizado**

Esse alerta tem um período de aprendizado de oito dias, a partir do momento em que o controlador de domínio inicia o monitoramento.

**TP, B-TP ou FP**

1. Verifique se o computador de origem é um servidor DNS.

    - Se o computador de origem **for** um servidor DNS, feche o alerta de segurança como um **FP**.
    - Para evitar futuros **FPs** , verifique se a porta UDP 53 está **aberta** entre o sensor do [!INCLUDE [Product short](includes/product-short.md)] e o computador de origem.

Verificadores de segurança e aplicativos legítimos podem gerar consultas DNS.

1. Verifique se o computador de origem deve gerar esse tipo de atividade.

    - Se o computador de origem precisar gerar esse tipo de atividade, **feche** o alerta de segurança e exclua o computador como uma atividade **B-TP**.

**Entender o escopo da violação**

1. Investigue o [computador de origem](investigate-a-computer.md).

**Correção sugerida e etapas de prevenção**

**Correção:**

- Contenha o computador de origem.
  - Encontre a ferramenta que realizou o ataque e remova-a.
  - Procure usuários que estavam conectados no mesmo período em que a atividade ocorreu, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.

**Prevenção:**

é importante evitar ataques futuros que usem consultas AXFR protegendo seu servidor DNS interno.

- Proteja seu servidor DNS interno para impedir o reconhecimento usando DNS desabilitando a transferências de zona ou [restringindo as transferências de zona](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649273(v=ws.10)) apenas a endereços IP especificados. A modificação de transferências de zona é uma tarefa entre uma lista de verificação que deve ser resolvida para [proteger seus servidores DNS contra ataques internos e externos](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649273(v=ws.10)).

## <a name="security-principal-reconnaissance-ldap-external-id-2038"></a>Reconhecimento de entidade de segurança (LDAP) (ID 2038 externa)

**Descrição**

O reconhecimento de entidade de segurança é usado pelos invasores para obter informações críticas sobre o ambiente de domínio. As informações que ajudam os invasores a mapear a estrutura de domínio, bem como identificar contas privilegiadas para uso em etapas posteriores em sua cadeia de encerramento do ataque. O protocolo LDAP (Lightweight Directory Access Protocol) é um dos métodos mais populares usados para fins legítimos e mal-intencionados para consultar o Active Directory Domain Services. O reconhecimento de entidade de segurança focada no LDAP é normalmente usado como a primeira fase de um ataque Kerberoasting. Os ataques de Kerberoasting são usados para obter uma lista de destino de SPNs (nome da entidade de serviço), que os invasores tentam, então, obter tíquetes do TGS (servidor de concessão de tíquete).

Para permitir que o [!INCLUDE [Product short](includes/product-short.md)] analise com precisão e reconheça os usuários legítimos, nenhum alerta desse tipo é disparado nos primeiros dez dias após a implantação do [!INCLUDE [Product short](includes/product-short.md)]. Depois que a fase de aprendizado inicial do [!INCLUDE [Product short](includes/product-short.md)] é concluída, os alertas são gerados nos computadores que executam consultas de enumeração de LDAP suspeitas ou consultas destinadas a grupos confidenciais que usam métodos não observados anteriormente.

**Período de aprendizado**

15 dias por computador, desde o dia do primeiro evento observado pelo computador.

**TP, B-TP ou FP**

1. Clique no computador de origem e acesse a página de perfil.
    1. Este computador de origem deve gerar essa atividade?
    1. Se o computador e a atividade forem esperados, **Feche** o alerta de segurança e exclua esse computador como uma atividade **B-TP**.

**Entender o escopo da violação**

1. Verifique as consultas que foram executadas (como administradores de domínio ou todos os usuários em um domínio) e determine se as consultas foram bem-sucedidas. Investigue cada pesquisa de grupo exposto por atividades suspeitas realizadas no grupo ou por usuários membros do grupo.
1. Investigue o [computador de origem](investigate-a-computer.md).
    - Usando as consultas LDAP, verifique se todas as atividades de acesso ao recurso ocorreram em qualquer um dos SPNs expostos.

**Correção sugerida e etapas de prevenção**

1. Conter o computador de origem
    1. Encontre a ferramenta que realizou o ataque e remova-a.
    1. O computador está executando uma ferramenta de verificação que realiza várias consultas LDAP?
    1. Procure por usuários que estavam conectados em horário próximo ao que a atividade ocorreu, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Redefina a senha se o acesso aos recursos do SPN foi feito e executado sob uma conta de usuário (não na conta do computador).

**Etapas sugeridas específicas de Kerberoasting para prevenção e correção**

1. Redefina as senhas dos usuários comprometidos e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Exija o uso de [senhas longas e complexas para usuários com contas de entidade de serviço](/windows/security/threat-protection/security-policy-settings/minimum-password-length).
1. [Substitua a conta de usuário pela gMSA (conta de serviço gerenciado de grupo)](/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview).

> [!NOTE]
> Só há suporte para os alertas de reconhecimento de entidade de segurança (LDAP) nos sensores do [!INCLUDE [Product short](includes/product-short.md)].

## <a name="user-and-group-membership-reconnaissance-samr-external-id-2021"></a>Reconhecimento de usuário e de associação a um grupo (SAMR) (ID 2021 externa)

*Nome anterior:* Reconhecimento usando consultas de serviços de diretório

**Descrição**

O reconhecimento de usuário e de associação a um grupo é usado pelos invasores para mapear a estrutura de diretório e visar contas com privilégios para as próximas etapas do ataque. O protocolo SAM-R (Remoto do Gerenciador de Contas de Segurança) é um dos métodos usados para consultar o diretório para realizar esse tipo de mapeamento.
Nessa detecção, nenhum alerta é disparado no primeiro mês após a implantação do [!INCLUDE [Product short](includes/product-short.md)] (período de aprendizado). Durante o período de aprendizado, o [!INCLUDE [Product short](includes/product-short.md)] analisa quais consultas SAM-R são feitas de quais computadores, tanto consultas de enumeração quanto individuais de contas confidenciais.

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
1. Investigue cada usuário exposto usando o guia de investigação de usuário.
1. Investigue o computador de origem.

**Correção sugerida e etapas de prevenção**

1. Contenha o computador de origem.
1. Localize e remova a ferramenta que executou o ataque.
1. Procure por usuários que estavam conectados em horário próximo àquele da atividade, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Redefina a senha do usuário de origem e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Aplique o acesso à rede e restrinja os clientes com permissão para fazer chamadas remotas à política de grupo SAM.

## <a name="user-and-ip-address-reconnaissance-smb-external-id-2012"></a>Reconhecimento de endereço IP e de usuário (SMB) (ID 2012 externa)

*Nome anterior:* Reconhecimento usando a enumeração da sessão SMB

### <a name="description"></a>Descrição

A enumeração usando o protocolo SMB permite que invasores obtenham informações sobre onde os usuários se conectaram recentemente. Depois que os invasores tiverem essas informações, eles podem mover lateralmente na rede para obter uma determinada conta confidencial.

Nessa detecção, um alerta é acionado quando uma enumeração de sessão SMB é executada em um controlador de domínio.

**TP, B-TP ou FP**

Aplicativos e verificadores de segurança podem consultar legitimamente os controladores de domínio para verificar se há sessões SMB abertas.

1. Esse computador de origem deve gerar atividades desse tipo?
1. Há algum tipo de verificador de segurança em execução no computador de origem?
    Se a resposta for sim, provavelmente essa será uma atividade B-TP. *Feche* o alerta de segurança e exclua esse computador.
1. Verifique os usuários que realizaram a operação.
    Esses usuários devem executar essas ações?
    Se a resposta for sim, *feche* o alerta de segurança como uma atividade B-TP.

**Entender o escopo da violação**

1. Investigue o computador de origem.
1. Na página do alerta, verifique se há algum usuário exposto. Para investigar mais detalhadamente cada usuário exposto, verifique o perfil deles. Recomendamos que você comece a investigação com os usuários confidenciais e de alta prioridade de investigação.

**Correção sugerida e etapas de prevenção**

Use a [ferramenta Net Cease](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b) para proteger seu ambiente contra esse ataque.

> [!NOTE]
> Para desabilitar um alerta de segurança do [!INCLUDE [Product short](includes/product-short.md)], entre em contato com o suporte.

> [!div class="nextstepaction"]
> [Tutorial do alerta de credencial comprometida](compromised-credentials-alerts.md)

## <a name="see-also"></a>Consulte Também

- [Investigar um computador](investigate-a-computer.md)
- [Investigar um usuário](investigate-a-user.md)
- [Trabalhando com alertas de segurança](working-with-suspicious-activities.md)
- [Alertas de credencial comprometida](compromised-credentials-alerts.md)
- [Alertas de movimento lateral](lateral-movement-alerts.md)
- [Alertas de predominância de domínio](domain-dominance-alerts.md)
- [Alertas de exfiltração](exfiltration-alerts.md)
- [Referência de log de SIEM do [!INCLUDE [Product short](includes/product-short.md)]](cef-format-sa.md)
- [Trabalhando com caminhos de movimento lateral](use-case-lateral-movement-path.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
