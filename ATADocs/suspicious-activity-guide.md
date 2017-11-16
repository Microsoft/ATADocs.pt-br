---
title: Guia de atividades suspeitas do ATA | Microsoft Docs
d|Description: This article provides a list of the suspicious activities ATA can detect and steps for remediation.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1fe5fd6f-1b79-4a25-8051-2f94ff6c71c1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: bff477a66b837d82bb10a43a0dad7d36c6542d9f
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*


# <a name="advanced-threat-analytics-suspicious-activity-guide"></a>Guia de atividades suspeitas Advanced Threat Analytics

Após investigação adequada, qualquer atividade suspeita pode ser classificada como:

-   **Verdadeiro positivo**: uma ação mal intencionada detectada pelo ATA.

-   **Verdadeiro positivo benigno**: uma ação detectada pelo ATA que é real, mas não é mal intencionada, como um teste de penetração.

-   **Falso positivo**: um alarme falso, indicando que a atividade não ocorreu.

Para saber mais sobre como trabalhar com alertas ATA, confira [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md).

Para fazer perguntas ou comentários, entre em contato com a equipe do ATA em [ATAEval@microsoft.com](mailto:ATAEval@microsoft.com).

## <a name="abnormal-sensitive-group-modification"></a>Modificação anormal de grupo confidencial


**Descrição**

Os invasores adicionam usuários a grupos altamente privilegiados. Eles fazem isso para obter acesso a mais recursos e obter persistência. A detecção conta com a criação de perfil de atividades de modificação do grupo de usuários e com o alerta para quando uma adição anormal a um grupo confidencial é vista. A criação de perfil é executada continuamente pelo ATA. O período mínimo antes do acionamento de um alerta é de um mês por cada controlador de domínio.

Para obter uma definição de grupos confidenciais no ATA, consulte [Trabalhando com o console do ATA](working-with-ata-console.md#sensitive-groups).


A detecção depende de [eventos auditados em controladores de domínio](https://docs.microsoft.com/advanced-threat-analytics/configure-event-collection).
Para verificar se seus controladores de domínio realizam a auditoria de eventos necessários, use a ferramenta referenciada em [Auditoria do ATA (AuditPol, Aplicação de configurações de auditoria avançadas, descoberta de serviço do Gateway Lightweight)](https://aka.ms/ataauditingblog).

**Investigação**

1. A modificação do grupo é legítima? </br>Modificações de grupo legítimas que raramente ocorrem e não foram conhecidas como "normais" podem causar um alerta que seria considerado como um positivo verdadeiro benigno.

2. Se o objeto adicionado for uma conta de usuário, verifique quais ações a conta de usuário realizou após ser adicionada ao grupo de administrador. Vá para a página do usuário no ATA para obter mais contexto. Houve alguma outra atividade suspeita associada à conta antes ou após a adição ocorrer? Baixe o relatório **Modificação de grupos confidenciais** para ver quais outras modificações foram feitas e por quem durante o mesmo período de tempo.

**Remediação**

Minimize a quantidade de pessoas que estão autorizadas a modificar grupos confidenciais.

Configure o [Privileged Access Management para Active Directory](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) se aplicável.

## <a name="broken-trust-between-computers-and-domain"></a>Confiança quebrada entre domínio e computadores

**Descrição**

Confiança quebrada significa que os requisitos de segurança do Active Directory podem não estar em vigor para os computadores em questão. Isso é geralmente considerado uma falha de conformidade e segurança de linha de base e um alvo fácil para os invasores. Nessa detecção, um alerta será acionado se mais de 5 falhas de autenticação Kerberos forem vistas de uma conta de computador em 24 horas.

**Investigação**

O computador em questão está permitindo que os usuários de domínio façam logon? 
- Se sim, é possível ignorar esse computador nas etapas remediação.

**Remediação**

Ingresse novamente o computador no domínio se necessário ou redefina a senha do computador.

## <a name="brute-force-attack-using-ldap-simple-bind"></a>Ataque de força bruta usando associação simples LDAP

**Descrição**

>[!NOTE]
> A principal diferença entre **Falhas de autenticação suspeitas** e esta detecção é que, nessa detecção, o ATA pode determinar se senhas diferentes foram usadas.

Em um ataque de força bruta, o invasor tenta autenticar com muitas senhas diferentes para diferentes contas até que uma senha correta seja encontrada para pelo menos uma conta. Uma vez encontrada, um invasor pode fazer logon usando essa conta.

Nessa detecção, um alerta é disparado quando o ATA detecta que muitas senhas diferentes estão sendo usadas. Isso pode ser *horizontalmente* com um pequeno conjunto de senhas entre vários usuários; ou *verticalmente "* com um grande conjunto de senhas em apenas alguns usuários; ou qualquer combinação dessas duas opções.

**Investigação**

1. Se houver muitas contas envolvidas, clique em **Baixar detalhes** para exibir a lista em uma planilha do Excel.

2. Clique no alerta para ir até a página dedicada. Verifique se alguma tentativa de logon terminou com uma autenticação bem-sucedida. As tentativas aparecerem como **Contas adivinhadas** no lado direito do infográfico. Se sim, alguma das **Contas adivinhadas** é normalmente usada pelo computador de origem? Se sim, **Omita** a atividade suspeita.

3. Se não houver nenhuma **Conta adivinhada**, alguma das **Contas atacadas** é normalmente usada no computador de origem? Se sim, **Omita** a atividade suspeita.

**Remediação**

[Senhas complexas e longas](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) fornecem o primeiro nível necessário de segurança contra ataques de força bruta.

## <a name="encryption-downgrade-activity"></a>Atividade de downgrade de criptografia

**Descrição**

Vários métodos de ataque utilizam criptografias Kerberos fracas. Nessa detecção, o ATA aprende os tipos de criptografia Kerberos usados por computadores e usuários e alerta você quando uma criptografia mais fraca é usada que: (1) seja incomum para o computador de origem e/ou o usuário; e (2) corresponda a técnicas de ataque conhecidas.

Há três tipos de detecção:

1.  Skeleton Key – é um malware que é executado nos controladores de domínio e permite a autenticação no domínio com qualquer conta sem saber sua senha. Este malware geralmente usa algoritmos de criptografia mais fracos para codificação de senhas do usuário no controlador de domínio. Nesta detecção, o método de criptografia da mensagem KRB_ERR do computador de origem foi desatualizado em comparação com o comportamento aprendido anteriormente.

2.  Golden Ticket – em um alerta [Golden Ticket](#golden-ticket), o método de criptografia do campo TGT da mensagem TGS_REQ (solicitação de serviço) do computador de origem foi desatualizado em comparação com o comportamento aprendido anteriormente. Isso não tem base em uma anomalia de tempo (como na outra detecção Golden Ticket). Além disso, não houve nenhuma solicitação de autenticação Kerberos associada à solicitação de serviço anterior detectada pelo ATA.

3.  Overpass-the-Hash – o tipo de criptografia de mensagem AS_REQ do computador de origem foi desatualizado em comparação com o comportamento aprendido anteriormente (ou seja, o computador estava usando AES).

**Investigação**

Primeiro, verifique a descrição do alerta para ver com qual dos três tipos de detecção acima você está lidando.

1.  Skeleton Key – Você pode verificar se a Skeleton Key afetou os controladores de domínio usando [o analisador gravado pela equipe do ATA](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73).
    Se o analisador encontrar malware em 1 ou mais controladores de domínio, é um verdadeiro positivo.

2.  Golden Ticket – há casos em que um aplicativo personalizado que é raramente usado está se autenticando usando uma codificação de criptografia inferior. Verifique se há algum desses aplicativos personalizados no computador de origem. Nesse caso, ele é provavelmente um positivo verdadeiro benigno e pode ser suprimido.

3.  Overpass-the-Hash – há casos em que esse alerta pode ser disparado quando usuários configurados com cartões inteligentes forem necessários para logon interativo e essa configuração é desabilitada e, em seguida, habilitada. Verifique se ocorreram alterações como essa para a(s) conta(s) envolvida(s). Nesse caso, ele é provavelmente um positivo verdadeiro benigno e pode ser suprimido.

**Remediação**

1.  Skeleton Key – Remova malware. Para obter mais informações, consulte [Análise do malware Skeleton Key](https://www.secureworks.com/research/skeleton-key-malware-analysis) da SecureWorks.

2.  Golden Ticket – Siga as instruções das atividades suspeitas do [Golden Ticket](#golden-ticket).   
    Além disso, como criar um tíquete de ouro requer direitos de administrador de domínio, implemente [Passar as recomendações de hash](http://aka.ms/PtH).

3.  Overpass-the-Hash – Se a conta envolvida não for confidencial, então, redefina a senha dessa conta. Isso impede que o invasor crie novos tíquetes Kerberos do hash de senha, embora os tíquetes existentes ainda possam ser usados até expirarem. Se for uma conta confidencial, você deverá considerar redefinir a conta KRBTGT duas vezes como na atividade suspeita do Golden Ticket. Redefinir o KRBTGT duas vezes invalida todos os tíquetes Kerberos nesse domínio, portanto, planeje antes de fazer isso. Consulte as diretrizes em [Scripts de redefinição de senha da conta KRBTGT disponíveis agora para os clientes](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/). Consulte também como usar a [ferramenta Redefinir as chaves/senha da conta KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Como essa é uma técnica de movimentação lateral, siga as práticas recomendadas das [recomendações de Passagem de hash](http://aka.ms/PtH).

## Golden Ticket<a name="golden-ticket"></a>

**Descrição**

Os invasores com direitos de administrador de domínio podem comprometer a [conta KRBTGT](https://technet.microsoft.com/library/dn745899(v=ws.11).aspx#Sec_KRBTGT). Ao usar a conta KRBTGT, eles podem criar um tíquete de concessão de tíquete Kerberos (TGT) que fornece autorização para qualquer recurso e define a expiração do tíquete para qualquer momento arbitrário. Esse TGT falso é chamado de "Golden Ticket" e permite que os invasores obtenham persistência na rede.

Nessa detecção, um alerta é acionado quando um tíquete de concessão de tíquete Kerberos for usado por mais tempo do que o permitido conforme especificado na política de segurança [Tempo de vida máximo para tíquete de usuário](https://technet.microsoft.com/library/jj852169(v=ws.11).aspx).

**Investigação**

1. Houve alguma alteração recente (dentro das últimas horas) feita na configuração **Tempo de vida máximo para tíquete de usuário** na política de grupo? Se Sim, então, **Feche** o alerta (era um falso positivo).

2. O Gateway do ATA envolvido nesse alerta é uma máquina virtual? Se Sim, ele retomou recentemente de um estado salvo? Se Sim, então, **Feche** este alerta.

3. Se a resposta para as perguntas acima for não, suponha que ele seja mal-intencionado.

**Remediação**

Altere o Tíquete de concessão de tíquete Kerberos (KRBTGT) duas vezes de acordo com as diretrizes em [Scripts de redefinição de senha da conta KRBTGT disponíveis agora para clientes](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) usando a [ferramenta Redefinir chaves/senha da conta KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Redefinir o KRBTGT duas vezes invalida todos os tíquetes Kerberos nesse domínio, portanto, planeje antes de fazer isso.  
Além disso, como criar um tíquete de ouro requer direitos de administrador de domínio, implemente [Passar as recomendações de hash](http://aka.ms/PtH).

## <a name="honeytoken-activity"></a>Atividade de Honeytoken


**Descrição**

As contas Honeytoken são contas fictícias configuradas para identificar e rastrear atividades mal-intencionadas que envolvem essas contas. Contas de Honeytoken devem ser deixadas como não utilizadas, enquanto têm um nome atraente para atrair invasores (por exemplo, SQL-Admin). Qualquer atividade delas pode indicar comportamento mal-intencionado.

Para obter mais informações sobre contas do honeytoken, consulte [Instalar o ATA – etapa 7](install-ata-step7.md).

**Investigação**

1.  Verifique se o proprietário do computador de origem usou a conta Honeytoken para autenticar, usando o método descrito na página de atividades suspeitas (por exemplo, Kerberos, LDAP, NTLM).

2.  Navegue até as páginas de perfil de computador(es) de origem e verifique quais outras contas se autenticaram por meio delas. Verifique com os proprietários dessas contas se eles usaram a conta Honeytoken.

3.  Isso pode ser um logon não interativo, portanto, certifique-se de verificar se há aplicativos ou scripts que são executados no computador de origem.

Se, depois de executar as etapas 1 a 3, não houver nenhuma evidência de uso benigno, suponha que isso é mal-intencionado.

**Remediação**

Certifique-se de que as contas Honeytoken sejam usadas apenas para sua finalidade pretendida, caso contrário, elas podem gerar muitos alertas.

## <a name="identity-theft-using-pass-the-hash-attack"></a>Roubo de identidade usando o ataque de passagem de Hash

**Descrição**

Passagem de Hash é uma técnica de movimento lateral em que os invasores roubam o hash NTLM de um usuário de um computador e o usa para acessar outro computador. 

**Investigação**

O hash foi usado em um computador que o usuário destinado possui ou usa regularmente? Se sim, esse é um falso positivo. Caso contrário, provavelmente é um verdadeiro positivo.

**Remediação**

1. Se a conta envolvida não for confidencial, então, redefina a senha dessa conta. Isso impede que o invasor crie novos tíquetes Kerberos do hash de senha, embora os tíquetes existentes ainda possam ser usados até expirarem. 

2. Se for uma conta confidencial, você deverá considerar redefinir a conta KRBTGT duas vezes como na atividade suspeita do Golden Ticket. Redefinir o KRBTGT duas vezes invalida todos os tíquetes Kerberos nesse domínio, portanto, planeje antes de fazer isso. Consulte as diretrizes em [Scripts de redefinição de senha da conta KRBTGT disponíveis agora para clientes](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), consulte também como usar a [ferramenta Redefinir chaves/senha da conta KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Como essa é uma técnica de movimentação lateral, siga as práticas recomendadas das [recomendações de Passagem de hash](http://aka.ms/PtH).

## <a name="identity-theft-using-pass-the-ticket-attack"></a>Roubo de identidade usando o ataque Pass-the-Ticket

**Descrição**

Pass-the-Ticket é uma técnica de movimento lateral em que os invasores roubam um tíquete Kerberos de um computador e o usam para acessar outro computador reutilizando o tíquete roubado. Nessa detecção, um tíquete Kerberos é visto sendo usado em dois (ou mais) computadores diferentes.

**Investigação**

1. Clique no botão **Baixar detalhes** para exibir a lista completa de endereços IP envolvidos. O endereço IP de um ou ambos os computadores pertence a uma sub-rede que é alocada de um pool de DHCP subdimensionado, por exemplo, Wi-Fi ou VPN? O endereço IP é compartilhado? Por exemplo, por um dispositivo NAT? Se a resposta para qualquer uma dessas perguntas for sim, isso será um falso positivo.

2. Há um aplicativo personalizado que encaminha os tíquetes em nome dos usuários? Nesse caso, é um positivo verdadeiro benigno.

**Remediação**

1. Se a conta envolvida não for confidencial, então, redefina a senha dessa conta. Isso impede que o invasor crie novos tíquetes Kerberos do hash de senha, embora os tíquetes existentes ainda possam ser usados até expirarem.  

2. Se for uma conta confidencial, você deverá considerar redefinir a conta KRBTGT duas vezes como na atividade suspeita do Golden Ticket. Redefinir o KRBTGT duas vezes invalida todos os tíquetes Kerberos nesse domínio, portanto, planeje antes de fazer isso. Consulte as diretrizes em [Scripts de redefinição de senha da conta KRBTGT disponíveis agora para clientes](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), consulte também como usar a [ferramenta Redefinir chaves/senha da conta KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).  Como essa é uma técnica de movimentação lateral, siga as práticas recomendadas nas [recomendações de Passagem de hash](http://aka.ms/PtH).

## <a name="malicious-data-protection-private-information-request"></a>Solicitação de informações privadas para proteção contra dados mal-intencionados

**Descrição**

A DPAPI (API de Proteção de Dados) é usada pelo Windows para proteger senhas com segurança salvas por navegadores, arquivos criptografados e outros dados confidencias. Os controladores de domínio têm uma chave mestra de backup que pode ser usada para descriptografar todos os segredos criptografados com DPAPI em computadores Windows ingressados no domínio. Os invasores podem usar essa chave mestra para descriptografar informações secretas protegidas por DPAPI em todos os computadores que ingressaram no domínio.
Nessa detecção, um alerta é acionado quando o DPAPI é usado para recuperar a chave mestra do backup.

**Investigação**

1. O computador de origem está executando uma verificação de segurança avançada aprovada pela organização em relação ao Active Directory?

2. Se sim e sempre precisar fazer isso, **Feche e exclua** a atividade suspeita.

3. Se sim e não precisar fazer isso, **Feche** a atividade suspeita.

**Remediação**

Para usar DPAPI, um invasor precisa de direitos de administrador de domínio. Implemente as [recomendações de Pass the hash](http://aka.ms/PtH).

## <a name="malicious-replication-requests"></a>Solicitações de replicação mal-intencionada


**Descrição**

A replicação do Active Directory é o processo pelo qual as alterações feitas em um controlador de domínio são sincronizadas com todos os outros controladores de domínio. Com as permissões necessárias, os invasores podem iniciar uma solicitação de replicação, permitindo que eles possam recuperar os dados armazenados no Active Directory, incluindo hashes de senha.

Nessa detecção, um alerta é disparado quando uma solicitação de replicação for iniciada em um computador que não seja um controlador de domínio.

**Investigação**

1. O computador em questão é um controlador de domínio? Por exemplo, um controlador de domínio recém-promovido que teve problemas de replicação. Se sim, **Feche e exclua** a atividade suspeita.  

2. O computador em questão deveria estar replicando dados do Active Directory? Por exemplo, o Azure AD Connect. Se sim, **Feche e exclua** a atividade suspeita.

**Remediação**

Valide as seguintes permissões: 

- Replicar alterações de diretório   

- Replicar todas as alterações de diretório  

Para obter mais informações, consulte [Conceder permissões do Active Directory Domain Services para sincronização de perfil no SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).
Você pode utilizar o [Scanner ACL do AD](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) ou criar um script do Windows PowerShell para determinar quem no domínio tem essas permissões.

## <a name="massive-object-deletion"></a>Exclusão de objeto grande

**Descrição**

Em alguns cenários, os invasores executam uma negação de serviço (DoS) em vez de apenas roubar informações. Excluir um grande número de contas é uma técnica DoS.

Nessa detecção, um alerta é disparado quando mais de 5% de todas as contas for excluído. A detecção requer o acesso de leitura ao contêiner do objeto excluído.  
Para obter informações sobre como configurar permissões de somente leitura no contêiner Objetos excluídos, confira a seção **Alterar permissões em um contêiner de objetos excluídos** no tópico [Exibir ou definir permissões em um objeto de diretório](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

**Investigação**

Examine a lista de contas excluídas e verifique se há um padrão ou um motivo comercial que possa justificar essa exclusão em massa.

**Remediação**

Remova as permissões para usuários que podem excluir contas no Active Directory. Para obter mais informações, consulte [Exibir ou definir permissões em um objeto de diretório](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

## <a name="privilege-escalation-using-forged-authorization-data"></a>Elevação de privilégios usando dados de autorização forjados

**Descrição**

As vulnerabilidades conhecidas em versões mais antigas do Windows Server permitem que os invasores manipulem o PAC (Certificado de Atributo Privilegiado), um campo no tíquete Kerberos que contém os dados de autorização do usuário (no Active Directory essa é a associação de grupo), concedendo ao invasor privilégios adicionais.

**Investigação**

1. Clique no alerta para ver sua página de detalhes.

2. O computador de destino (sob a coluna **ACESSADO**) tem patch MS14-068 (controlador de domínio) ou MS11-013 (servidor)? Se sim, **Feche** a atividade suspeita (é um falso positivo).

3. Se não, o computador de origem for executado (sob a coluna **DE**) tem um sistema operacional/aplicativo conhecido para modificar o PAC? Em caso afirmativo, **Suprima** a atividade suspeita (é um positivo verdadeiro benigno).

4. Se a resposta para as duas perguntas acima for não, suponha que ele seja mal-intencionado.

**Remediação**

Verifique se todos os controladores de domínio com sistemas operacionais até o Windows Server 2012 R2 estão instalados com o [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege) e todos os servidores membros e controladores de domínio até 2012 R2 estão atualizados com o KB2496930. Para obter mais informações, consulte [PAC Prata](https://technet.microsoft.com/library/security/ms11-013.aspx) e [PAC Forjado](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="reconnaissance-using-directory-services-queries"></a>Reconhecimento usando consultas de serviços de diretório

**Descrição**

O reconhecimento de serviços de diretório é usado pelos invasores para mapear a estrutura de diretório e visar contas com privilégios para as etapas posteriores em um ataque. O protocolo SAM-R (Remoto do Gerenciador de Conta de Segurança) é um dos métodos usados para consultar o diretório para realizar esse mapeamento.

Nessa detecção, nenhum alerta será disparado no primeiro mês após a implantação do ATA. Durante o período de aprendizado, o ATA cria perfis de quais consultas SAM-R são feitas de quais computadores, de consultas de enumeração e individuais de contas confidenciais.

**Investigação**

1. Clique no alerta para ver sua página de detalhes. Verifique quais consultas foram executadas (por exemplo, administradores corporativos ou administrador) e se elas foram bem-sucedidas.

2. Essas consultas devem ser feitas do computador de origem em questão?

3. Se sim e se o alerta for atualizado, **Suprima** a atividade suspeita.

4. Se sim e se não precisar fazer mais isso, **Feche** a atividade suspeita.

5. Se não houver informações sobre a conta envolvida: essas consultas devem ser feitas por essa conta ou essa conta normalmente faz logon no computador de origem?

 - Se sim e se o alerta for atualizado, **Suprima** a atividade suspeita.

 - Se sim e se não precisar fazer mais isso, **Feche** a atividade suspeita.

 - Se a resposta para todas as perguntas acima for não, suponha que ele seja mal-intencionado.

**Remediação**

Use a [ferramenta SAMRi10](https://gallery.technet.microsoft.com/SAMRi10-Hardening-Remote-48d94b5b) para proteger seu ambiente contra essa técnica.

## <a name="reconnaissance-using-dns"></a>Reconhecimento usando DNS

**Descrição**

O servidor DNS contém um mapa de todos os computadores, endereços IP e serviços em sua rede. Essas informações são usadas pelos invasores para mapear sua estrutura de rede e visar computadores interessantes para etapas posteriores no ataque.

Há vários tipos de consulta no protocolo DNS. O ATA detecta a solicitação AXFR (transferência) proveniente de servidores não DNS.

**Investigação**

1. O computador de origem (**Proveniente de...** ) é um servidor DNS? Se sim, então, provavelmente é um falso positivo. Para validar, clique no alerta para ver sua página de detalhes. Na tabela, em **Consulta**, verifique quais domínios foram consultados. Esses domínios são existentes? Se sim, então, **Feche** a atividade suspeita (é um falso positivo). Além disso, certifique-se de que a porta 53 do UDP esteja aberta entre os Gateways do ATA e o computador de origem para evitar futuros falsos positivos.

2. O computador de origem está executando um verificador de segurança? Em caso afirmativo, **Exclua as entidades** no ATA, seja diretamente com **Fechar e excluir** ou por meio da página **Exclusão** (em **Configuração** – disponível para administradores do ATA).

3. Se a resposta para todas as perguntas acima for não, suponha que ele seja mal-intencionado.

**Remediação**

A proteção de um servidor DNS interno para impedir que o reconhecimento usando DNS ocorra pode ser obtida desabilitando ou restringindo as transferências de zona apenas para endereços IP específicos. Para obter mais informações sobre como restringir transferências de zona, consulte [Restringir transferências de zona](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx).
A modificação de transferências de zona é uma tarefa entre uma lista de verificação que deve ser resolvida para [proteger seus servidores DNS contra ataques internos e externos](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx).

## <a name="reconnaissance-using-smb-session-enumeration"></a>Reconhecimento usando a enumeração da sessão SMB


**Descrição**

A enumeração do protocolo SMB (Bloco de mensagens de servidor) permite que invasores obtenham informações sobre onde os usuários se conectaram recentemente. Depois que os invasores tiverem essas informações, eles podem mover lateralmente na rede para obter uma determinada conta confidencial.

Nessa detecção, um alerta é acionado quando uma enumeração de sessão SMB é executada em um controlador de domínio, pois isso não deve ocorrer.

**Investigação**

1. Clique no alerta para ver sua página de detalhes. Verifique qual conta realizou a operação e quais contas foram expostas, se houver.

 - Há algum tipo de verificador de segurança em execução no computador de origem? Se sim, **Feche e exclua** a atividade suspeita.

2. Verifique quais usuários envolvidos realizaram a operação. Eles normalmente se registram no computador de origem ou eles são administradores que deveriam realizar essas ações?  

3. Se sim e se o alerta for atualizado, **Suprima** a atividade suspeita.  

4. Se sim e se não precisar fazer mais isso, **Feche** a atividade suspeita.

5. Se a resposta para todas as perguntas acima for não, suponha que ele seja mal-intencionado.

**Remediação**

Use a [ferramenta Net Cease](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b) para proteger seu ambiente contra esse ataque.

## <a name="remote-execution-attempt-detected"></a>Tentativa de execução remota detectada

**Descrição**

Os invasores que comprometem credenciais de administrador ou que usam uma exploração de dia zero podem executar comandos remotos no controlador de domínio. Isso pode ser usado para obter a persistência, coletar informações, ataques DOS (negação de serviço) ou qualquer outro motivo. O ATA detecta conexões PSexec e WMI remoto.

**Investigação**

1. Isso é comum para membros da equipe de TI e de estações de trabalho administrativas ou contas de serviço que executam tarefas administrativas nos controladores de domínio. Se for esse o caso e se o alerta for atualizado desde que o mesmo administrador e/ou computador esteja executando a tarefa, então, **Suprima** o alerta.

2. O **computador** em questão tem permissão para realizar essa execução remota em seu controlador de domínio?

 - A **conta** em questão tem permissão para realizar essa execução remota em seu controlador de domínio?

 - Se a resposta a ambas as perguntas for *Sim*, então, **Feche** o alerta.

3. Se a resposta a uma das perguntas for *não*, então, isso deverá ser considerado um positivo verdadeiro.

**Remediação**

1. Restrinja o acesso remoto aos controladores de domínio de computadores que não são da camada 0.

2. Implemente [acesso privilegiado](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access) para permitir que apenas computadores protegidos se conectem aos controladores de domínio para administração.

## <a name="sensitive-account-credentials-exposed--services-exposing-account-credentials"></a>Credenciais de contas confidenciais expostas e serviços que expõem credenciais da conta

**Descrição**

Alguns serviços enviam as credenciais de conta em texto sem formatação. Isso pode ocorrer até mesmo para contas confidenciais. Os invasores que monitoram o tráfego de rede podem capturar e reutilizar essas credenciais para fins mal-intencionados. Qualquer senha de texto não criptografada para uma conta confidencial dispara o alerta, enquanto para contas não confidenciais o alerta é disparado se cinco ou mais contas diferentes enviarem senhas em texto não criptografado no mesmo computador de origem. 

**Investigação**

Clique no alerta para ver sua página de detalhes. Veja quais contas foram expostas. Se houver muitas contas assim, clique em **Baixar detalhes** para exibir a lista em uma planilha do Excel.

Geralmente, há um aplicativo herdado ou script nos computadores de origem que usa a associação simples LDAP.

**Remediação**

Verifique a configuração nos computadores de origem e certifique-se de não usar a associação LDAP simples. Em vez de usar as ligações LDAP simples, use LDAP SALS ou LDAPS.

## <a name="suspicious-authentication-failures"></a>Falhas de autenticação suspeitas

**Descrição**

Em um ataque de força bruta, o invasor tenta autenticar com muitas senhas diferentes para diferentes contas até que uma senha correta seja encontrada para pelo menos uma conta. Uma vez encontrada, um invasor pode fazer logon usando essa conta.

Nessa detecção, um alerta é disparado quando diversas falhas de autenticação ocorrerem, isso pode ser horizontalmente com um pequeno conjunto de senhas entre vários usuários; ou verticalmente com um grande conjunto de senhas em apenas alguns usuários; ou qualquer combinação dessas duas opções.

**Investigação**

1. Se houver muitas contas envolvidas, clique em **Baixar detalhes** para exibir a lista em uma planilha do Excel.

2. Clique no alerta para ir até sua página de detalhes. Verifique se alguma tentativa de logon terminou com uma autenticação bem-sucedida, elas aparecem como **Contas adivinhadas** no lado direito do infográfico. Se sim, alguma das **Contas adivinhadas** é normalmente usada pelo computador de origem? Se sim, **Omita** a atividade suspeita.

3. Se não houver nenhuma **Conta adivinhada**, alguma das **Contas atacadas** é normalmente usada no computador de origem? Se sim, **Omita** a atividade suspeita.

**Remediação**

[Senhas complexas e longas](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) fornecem o primeiro nível necessário de segurança contra ataques de força bruta.

## <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>Suspeita de roubo de identidade com base no comportamento anormal

**Descrição**

O ATA aprende o comportamento de entidade para usuários, computadores e recursos em um período de três semanas corridas. O modelo de comportamento é baseado nas seguintes atividades: os computadores nos quais as entidades se registram, os recursos para os quais a entidade solicitou acesso e a hora em que essas operações foram realizadas. O ATA envia um alerta quando houver um desvio do comportamento da entidade com base em algoritmos de aprendizado do computador. 

**Investigação**

1. O usuário em questão deveria executar essas operações?

2. Considere os seguintes casos como possíveis falsos positivos: um usuário que retornou de férias, a equipe de TI que realiza o acesso em excesso como parte de seu serviço (por exemplo um aumento no suporte de help desk em um determinado dia ou semana), aplicativos de área de trabalho remota. + Se você **Fechar e excluir** o alerta, o usuário não será mais parte da detecção


**Remediação**

Dependendo do que fez com que esse comportamento ocorresse, diferentes ações devem ser tomadas. Por exemplo, se isso for devido à verificação da rede, o computador do qual isso ocorreu deverá ser bloqueado da rede (a menos que ela seja aprovado).

## <a name="unusual-protocol-implementation"></a>Implementação de protocolo incomum


**Descrição**

Os invasores usam ferramentas que implementam vários protocolos (SMB, Kerberos, NTLM) de maneiras não padrão. Embora esse tipo de tráfego de rede seja aceito pelo Windows sem avisos, o ATA é capaz de reconhecer possíveis mal-intencionados. O comportamento é uma indicação de técnicas como força bruta e de Over-Pass-the-Hash, bem como explorações usadas pelo ransomware avançado, por exemplo, WannaCry.

**Investigação**

Identifique o protocolo que seja incomum – na linha do tempo de atividade Suspeita, clique na atividade suspeita para ir para a página de detalhes; o protocolo é exibido acima da seta: Kerberos ou NTLM.

- **Kerberos**: isso geralmente será disparado se uma ferramenta de invasão como Mimikatz tiver sido usada, potencialmente executando um ataque de Overpass-the-Hash. Verifique se o computador de origem está executando um aplicativo que implementa a sua própria pilha de Kerberos, não de acordo com o RFC Kerberos. Se esse for o caso, é um positivo verdadeiro benigno e você poderá **Fechar** o alerta. Se o alerta continuar sendo disparado e esse ainda for o caso, você poderá **Suprimir** o alerta.

- **NTLM**: pode ser WannaCry ou ferramentas como Metasploit, Medusa e Hydra.  

Para determinar se este é um ataque WannaCry, realize as seguintes etapas:

1. Verifique se o computador de origem está executando uma ferramenta de ataque como Metasploit, Medusa ou Hydra.

2. Se nenhuma ferramenta de ataque for encontrada, verifique se o computador de origem está executando um aplicativo que implementa a sua própria pilha NTLM ou SMB.

3. Caso contrário, então, verifique se isso é causado pelo WannaCry executando um script de verificação de WannaCry, por exemplo [este analisador](https://github.com/apkjet/TrustlookWannaCryToolkit/tree/master/scanner) no computador de origem envolvido na atividade suspeita. Se o analisador descobrir que o computador está infectado ou vulnerável, aplique patches no computador, remova o malware e bloqueie-o da rede.

4. Se o script não considerar que o computador está infectado ou vulnerável, então, ele ainda poderá estar infectado, mas o SMBv1 pode ter sido desabilitado ou o computador foi corrigido, o que afetaria a ferramenta de verificação.

**Remediação**

Corrija todos os seus computadores, especialmente aplicando as atualizações de segurança.

1. [Desabilitar SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

2. [Remover WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo)

3. O WanaKiwi poderá descriptografar os dados nas mãos de algum ransoware, mas apenas se o usuário não tiver reiniciado ou desligado o computador. Para obter mais informações, consulte [Ransomware Wanna Cry](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1)

## <a name="related-videos"></a>Vídeos Relacionados
- [Participar da comunidade de segurança](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community)


## <a name="see-also"></a>Consulte também
- [Manual da atividade suspeita do ATA](http://aka.ms/ataplaybook)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
