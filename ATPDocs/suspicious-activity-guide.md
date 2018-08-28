---
title: Guia de atividades suspeitas do Azure ATP | Microsoft Docs
d|Description: This article provides a list of the suspicious activities Azure ATP can detect and steps for remediation.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/20/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4aa58228ea23f58ea37b10f941467e9dc076992f
ms.sourcegitcommit: f534a318be71b840aecb6a84744d8cd1f251a7aa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/22/2018
ms.locfileid: "41734831"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*


# <a name="azure-advanced-threat-protection-suspicious-activity-guide"></a>Guia de atividades suspeitas da Proteção Avançada contra Ameaças do Azure

Após investigação adequada, qualquer atividade suspeita pode ser classificada como:

-   **Verdadeiro positivo**: uma ação mal intencionada detectada pelo Azure ATP.

-   **Verdadeiro positivo benigno**: uma ação detectada pelo Azure ATP que é real, mas não é mal intencionada, como um teste de penetração.

-   **Falso positivo**: um alarme falso, indicando que a atividade não ocorreu.

Para saber mais sobre como trabalhar com alertas do Azure ATP, consulte [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md).


## <a name="abnormal-sensitive-group-modification"></a>Modificação anormal de grupo confidencial


**Descrição**

Os invasores adicionam usuários a grupos altamente privilegiados. Eles fazem isso para obter acesso a mais recursos e obter persistência. A detecção conta com a criação de perfil de atividades de modificação do grupo de usuários e com o alerta para quando uma adição anormal a um grupo confidencial é vista. A criação de perfil é executada continuamente pelo ATP. O período mínimo antes do acionamento de um alerta é de um mês por cada controlador de domínio.

Para ver uma definição de grupos confidenciais no Azure ATP, consulte [Trabalhando com contas confidenciais](sensitive-accounts.md).


A detecção depende de [eventos auditados em controladores de domínio](configure-event-collection.md).
Para garantir que seus controladores de domínio auditem os eventos necessários.

**Investigação**

1. A modificação do grupo é legítima? </br>Modificações de grupo legítimas que raramente ocorrem e não foram conhecidas como "normais" podem causar um alerta que seria considerado como um positivo verdadeiro benigno.

2. Se o objeto adicionado for uma conta de usuário, verifique quais ações a conta de usuário realizou após ser adicionada ao grupo de administrador. Vá até a página do usuário no Azure ATP para obter mais contexto. Houve alguma outra atividade suspeita associada à conta antes ou após a adição ocorrer? Baixe o relatório **Modificação de grupos confidenciais** para ver quais outras modificações foram feitas e por quem durante o mesmo período de tempo.

**Remediação**

Minimize a quantidade de pessoas que estão autorizadas a modificar grupos confidenciais.

Configure o [Privileged Access Management para Active Directory](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) se aplicável.


## <a name="brute-force-attack-using-ldap-simple-bind"></a>Ataque de força bruta usando associação simples LDAP

**Descrição**

>[!NOTE]
> A principal diferença entre **Falhas de autenticação suspeitas** e esta detecção é que, nesta detecção, o Azure ATP pode determinar se senhas diferentes foram usadas.

Em um ataque de força bruta, o invasor tenta autenticar com muitas senhas diferentes para diferentes contas até que uma senha correta seja encontrada para pelo menos uma conta. Uma vez encontrada, um invasor pode fazer logon usando essa conta.

Nesta detecção, um alerta é disparado quando o Azure ATP detecta um grande número de autenticações de associação simples. Isso pode ser *horizontalmente* com um pequeno conjunto de senhas entre vários usuários; ou *verticalmente "* com um grande conjunto de senhas em apenas alguns usuários; ou qualquer combinação dessas duas opções.

**Investigação**

1. Se houver muitas contas envolvidas, clique em **Baixar detalhes** para exibir a lista em uma planilha do Excel.

2. Clique no alerta para ir até a página dedicada. Verifique se alguma tentativa de logon terminou com uma autenticação bem-sucedida. As tentativas aparecerem como **Contas adivinhadas** no lado direito do infográfico. Se sim, alguma das **Contas adivinhadas** é normalmente usada pelo computador de origem? Se sim, **Omita** a atividade suspeita.

3. Se não houver nenhuma **Conta adivinhada**, alguma das **Contas atacadas** é normalmente usada no computador de origem? Se sim, **Omita** a atividade suspeita.

**Remediação**

[Senhas complexas e longas](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) fornecem o primeiro nível necessário de segurança contra ataques de força bruta.

## <a name="encryption-downgrade-activity"></a>Atividade de downgrade de criptografia

**Descrição**

O downgrade de criptografia é um método para enfraquecer o Kerberos fazendo um downgrade do nível de criptografia de diferentes campos do protocolo que geralmente são criptografados usando o nível mais elevado de criptografia. Um campo criptografado enfraquecido pode ser um alvo mais fácil para tentativas de força bruta offline. Vários métodos de ataque utilizam criptografias Kerberos fracas. Nessa detecção, o Azure ATP aprende os tipos de criptografia Kerberos usados por computadores e usuários e alerta você quando é usada uma criptografia mais fraca que: (1) seja incomum para o computador de origem e/ou o usuário; e (2) corresponda a técnicas de ataque conhecidas.

Há três tipos de detecção:

1.  Skeleton Key – é um malware que é executado nos controladores de domínio e permite a autenticação no domínio com qualquer conta sem saber sua senha. Este malware geralmente usa algoritmos de criptografia mais fracos para fazer o hash das senhas do usuário no controlador de domínio. Nesta detecção, o método de criptografia da mensagem KRB_ERR do controlador de domínio para a conta, solicitando um tíquete, passou por um downgrade em comparação com o comportamento aprendido anteriormente.

2.  Golden Ticket – em um alerta [Golden Ticket](#golden-ticket), o método de criptografia do campo TGT da mensagem TGS_REQ (solicitação de serviço) do computador de origem foi desatualizado em comparação com o comportamento aprendido anteriormente. Isso não tem base em uma anomalia de tempo (como na outra detecção Golden Ticket). Além disso, não houve nenhuma solicitação de autenticação Kerberos associada à solicitação de serviço anterior detectada pelo ATP.

3.  Overpass-the-Hash – um invasor pode usar um hash roubado fraco para criar um tíquete forte com uma solicitação do Kerberos AS. Nesta detecção, o tipo de criptografia de mensagem AS_REQ do computador de origem passou por downgrade em comparação com o comportamento aprendido anteriormente (ou seja, o computador estava usando AES).

**Investigação**

Primeiro, verifique a descrição do alerta para ver com qual dos três tipos de detecção acima você está lidando. Para saber mais, baixe a planilha do Excel.

1.  Skeleton Key – você pode verificar se a Skeleton Key afetou os controladores de domínio usando [o verificador escrito pela equipe do ATP do Azure](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73). Se o analisador encontrar malware em 1 ou mais controladores de domínio, é um verdadeiro positivo.

2.  Golden Ticket – na planilha do Excel, vá para a guia de atividade de rede. Você verá que o campo de downgrade relevante é **Solicitar Tipo de Criptografia de Tíquete** e **Tipos de Criptografia com Suporte no Computador de Origem** contém métodos de criptografia mais fortes.

  1. Verifique o recurso acessado por essas permissões. Se houver um recurso que todas elas estão acessando, valide-o e verifique se é um recurso válido que elas precisam acessar. Além disso, verifique se o recurso de destino dá suporte a métodos de criptografia forte. Você pode verificar isso no Active Directory verificando o atributo msDS-SupportedEncryptionTypes, da conta de serviço do recurso.
  
  2. Verifique a conta e o computador de origem ou, se houver várias contas e computadores de origem, verifique se eles têm algo em comum. Por exemplo, todos de sua equipe de marketing usam um aplicativo específico que pode causar o acionamento do alerta. Há casos em que um aplicativo personalizado que é raramente usado está se autenticando usando uma codificação de criptografia inferior. Verifique se há algum desses aplicativos personalizados no computador de origem. Nesse caso, ele é provavelmente um positivo verdadeiro benigno e pode ser suprimido.
  


3.  Overpass-the-Hash – na planilha do Excel, vá para a guia de atividade de rede. Você verá que o campo de downgrade relevante é **Tipo de Criptografia de Carimbo de Data/Hora Criptografado** e **Tipos de Criptografia com Suporte no Computador de Origem** contém métodos de criptografia mais fortes.

  1. Há casos em que esse alerta pode ser disparado quando os usuários fazem logon usando cartões inteligentes, se a configuração do cartão inteligente foi alterada recentemente. Verifique se ocorreram alterações como essa para a(s) conta(s) envolvida(s). Nesse caso, ele é provavelmente um positivo verdadeiro benigno e pode ser suprimido.
  2. Verifique o recurso acessado por essas permissões. Se houver um recurso que todas elas estão acessando, valide-o e verifique se é um recurso válido que elas precisam acessar. Além disso, verifique se o recurso de destino dá suporte a métodos de criptografia forte. Você pode verificar isso no Active Directory verificando o atributo msDS-SupportedEncryptionTypes, da conta de serviço do recurso.

**Remediação**

1.  Skeleton Key – Remova malware. Para saber mais, veja [Análise do malware Skeleton Key](https://www.virusbulletin.com/virusbulletin/2016/01/paper-digital-bian-lian-face-changing-skeleton-key-malware).

2.  Golden Ticket – Siga as instruções das atividades suspeitas do [Golden Ticket](#golden-ticket).   
    Além disso, como criar um tíquete de ouro requer direitos de administrador de domínio, implemente [Passar as recomendações de hash](http://aka.ms/PtH).

3.  Overpass-the-Hash – Se a conta envolvida não for confidencial, então, redefina a senha dessa conta. Isso impede que o invasor crie novos tíquetes Kerberos do hash de senha, embora os tíquetes existentes ainda possam ser usados até expirarem. Se for uma conta confidencial, você deverá considerar redefinir a conta KRBTGT duas vezes como na atividade suspeita do Golden Ticket. Redefinir o KRBTGT duas vezes invalida todos os tíquetes Kerberos nesse domínio, portanto, planeje antes de fazer isso. Consulte as diretrizes em [Scripts de redefinição de senha da conta KRBTGT disponíveis agora para os clientes](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/). Consulte também como usar a [ferramenta Redefinir as chaves/senha da conta KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Como essa é uma técnica de movimentação lateral, siga as práticas recomendadas das [recomendações de Passagem de hash](http://aka.ms/PtH).

## <a name="honeytoken-activity"></a>Atividade de Honeytoken


**Descrição**

As contas Honeytoken são contas fictícias configuradas para identificar e rastrear atividades mal-intencionadas que envolvem essas contas. Contas de Honeytoken devem ser deixadas como não utilizadas, enquanto têm um nome atraente para atrair invasores (por exemplo, SQL-Admin). Qualquer atividade delas pode indicar comportamento mal-intencionado.

Para obter mais informações sobre contas honeytoken, consulte [Instalar o Azure ATP – etapa 7](install-atp-step7.md).

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

1. Clique no botão **Baixar detalhes** para exibir a lista completa de endereços IP envolvidos. O endereço IP de um ou ambos os computadores pertence a uma sub-rede que é alocada de um pool de DHCP subdimensionado, por exemplo, Wi-Fi ou VPN? O endereço IP é compartilhado? Por exemplo, por um dispositivo NAT? Um ou mais dos endereços IP de origem não estão sendo resolvidos pelo sensor? (isso pode indicar que as portas adequadas do sensor para os dispositivos não estão abertas corretamente.) Se a resposta para qualquer uma dessas perguntas for sim, isso será um falso positivo.

2. Há um aplicativo personalizado que encaminha os tíquetes em nome dos usuários? Nesse caso, é um positivo verdadeiro benigno.

**Remediação**

1. Se a conta envolvida não for confidencial, então, redefina a senha dessa conta. Isso impede que o invasor crie novos tíquetes Kerberos do hash de senha, embora os tíquetes existentes ainda possam ser usados até expirarem.  

2. Se for uma conta confidencial, você deverá considerar redefinir a conta KRBTGT duas vezes como na atividade suspeita do Golden Ticket. Redefinir o KRBTGT duas vezes invalida todos os tíquetes Kerberos nesse domínio, portanto, planeje antes de fazer isso. Consulte as diretrizes em [Scripts de redefinição de senha da conta KRBTGT disponíveis agora para clientes](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), consulte também como usar a [ferramenta Redefinir chaves/senha da conta KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).  Como essa é uma técnica de movimentação lateral, siga as práticas recomendadas nas [recomendações de Passagem de hash](http://aka.ms/PtH).

## Golden ticket do Kerberos<a name="golden-ticket"></a>

**Descrição**

Os invasores com direitos de administrador de domínio podem comprometer a [conta KRBTGT](https://technet.microsoft.com/library/dn745899(v=ws.11).aspx#Sec_KRBTGT). Ao usar a conta KRBTGT, eles podem criar um tíquete de concessão de tíquete Kerberos (TGT) que fornece autorização para qualquer recurso e define a expiração do tíquete para qualquer momento arbitrário. Esse TGT falso é chamado de "goldenTicket" e permite que os invasores obtenham persistência na rede.

Nessa detecção, um alerta é acionado quando um tíquete de concessão de tíquete Kerberos é usado por mais tempo do que o permitido, como especificado no [Tempo de vida máximo para tíquete de usuário](https://technet.microsoft.com/library/jj852169(v=ws.11).aspx). Esse é um ataque de golden ticket por **anomalia de tempo** ou por uma conta não existente. Esse é um ataque de golden ticket por **conta não existente**.


**Investigação**

- **Anomalia de tempo**
   1.   Houve alguma alteração recente (dentro das últimas horas) feita na configuração "Tempo de vida máximo para tíquete de usuário" na política de grupo? Verifique o valor específico e veja se ele é menor do que o tempo de uso do tíquete. Se sim, então feche o alerta (era um falso positivo).
   2.   O sensor do Azure ATP envolvido neste alerta é uma máquina virtual? Se Sim, ele retomou recentemente de um estado salvo? Se sim, então feche este alerta.
   3.   Se a resposta para as perguntas acima for não, suponha que ele seja mal-intencionado.

- **Conta não existente**
   1.   Faça as seguintes perguntas:
         - O usuário é um usuário de domínio válido e conhecido? Se sim, então feche o alerta (era um falso positivo).
         - O usuário foi adicionado recentemente? Se sim, então feche o alerta, a alteração pode não ter sido ainda sincronizada.
         - O usuário foi excluído recentemente do AD? Se sim, então feche este alerta.
   2.   Se a resposta para as perguntas acima for não, suponha que ele seja mal-intencionado.

1. Para ambos os tipos de ataques de golden ticket, clique no computador de origem para acessar a página **Perfil**. Verifique o que aconteceu no momento da atividade e procure por atividades incomuns, como quem estava conectado e quais recursos foram acessados. 

2.  Todos os usuários que estavam conectados no computador deveriam estar conectados? Quais são os privilégios deles? 

3.  Estes usuários devem ter acesso a esses recursos?<br>
Se você tiver habilitado a integração do Windows Defender ATP, clique no ![selo WD](./media/wd-badge.png) do selo do Windows Defender ATP.
 
 4. Para continuar a investigar o computador, no Windows Defender ATP, verifique quais processos e alertas ocorreram no momento do alerta.

**Remediação**


Altere o Tíquete de concessão de tíquete Kerberos (KRBTGT) duas vezes de acordo com as diretrizes em [Scripts de redefinição de senha da conta KRBTGT disponíveis agora para clientes](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) usando a [ferramenta Redefinir chaves/senha da conta KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Redefinir o KRBTGT duas vezes invalida todos os tíquetes Kerberos nesse domínio, portanto, planeje antes de fazer isso. Além disso, como criar um tíquete de ouro requer direitos de administrador de domínio, implemente [Passar as recomendações de hash](http://aka.ms/PtH).




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

## <a name="malicious-replication-of-directory-services"></a>Replicação mal-intencionada de serviços de diretório


**Descrição**

A replicação do Active Directory é o processo pelo qual as alterações feitas em um controlador de domínio são sincronizadas com todos os outros controladores de domínio. Com as permissões necessárias, os invasores podem iniciar uma solicitação de replicação, permitindo que eles possam recuperar os dados armazenados no Active Directory, incluindo hashes de senha.

Nessa detecção, um alerta é disparado quando uma solicitação de replicação for iniciada em um computador que não seja um controlador de domínio.

**Investigação**

> [!NOTE]
> Se você tem controladores de domínio nos quais os sensores do Azure ATP não estejam instalados, estes controladores de domínio não estão cobertos pelo Azure ATP. Nesse caso, se você implantar um novo controlador de domínio em um controlador de domínio não registrado ou desprotegido, ele poderá não ser identificado inicialmente pelo Azure ATP como um controlador de domínio. É altamente recomendável instalar o sensor do Azure ATP em todos os controladores de domínio para obter uma cobertura completa.

1. O computador em questão é um controlador de domínio? Por exemplo, um controlador de domínio recém-promovido que teve problemas de replicação. Em caso afirmativo, **Fechar** a atividade suspeita. 
2.  O computador em questão deveria estar replicando dados do Active Directory? Por exemplo, o Azure AD Connect ou dispositivos de monitoramento de desempenho de rede. Se sim, **Feche e exclua** a atividade suspeita.
3. O IP que enviou a solicitação de replicação é um NAT ou um proxy? Se sim, verifique se há um novo controlador de domínio atrás do dispositivo ou se outras atividades suspeitas ocorreram a partir dele. 

4. Clique no computador de origem ou na conta para acessar a página de perfil. Verifique o que aconteceu no momento da replicação, pesquisando atividades incomuns, como: quem estava conectado e quais recursos foram acessados. Se você tiver habilitado a integração do Windows Defender ATP, clique no selo do Windows Defender ATP ![Selo do Windows Defender ATP](./media/wd-badge.png) para continuar a investigar o computador. No Windows Defender ATP, você pode ver quais processos e alertas ocorreram no momento do alerta. 


**Remediação**

Valide as seguintes permissões: 

- Replicar alterações de diretório   

- Replicar todas as alterações de diretório  

Para obter mais informações, consulte [Conceder permissões do Active Directory Domain Services para sincronização de perfil no SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).
Você pode utilizar o [Scanner ACL do AD](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) ou criar um script do Windows PowerShell para determinar quem no domínio tem essas permissões.


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

## <a name="reconnaissance-using-account-enumeration"></a>Reconhecimento de enumeração de conta

**Descrição**

No reconhecimento de enumeração de conta, um invasor usa um dicionário com milhares de nomes de usuário ou ferramentas como KrbGuess para tentar adivinhar nomes de usuário em seu domínio. O invasor faz solicitações Kerberos usando esses nomes para tentar localizar um nome de usuário válido no domínio. Se uma estimativa determinar com êxito um nome de usuário, o invasor receberá o erro de Kerberos **Pré-autenticação necessária** em vez de **Entidade de segurança desconhecida**. 

Nesta detecção, o Azure ATP pode detectar de onde veio o ataque, o número total de tentativas de previsão e quantas foram correspondidas. Se houver muitos usuários desconhecidos, o Azure ATP considerará isso uma atividade suspeita. 

**Investigação**

1. Clique no alerta para ver sua página de detalhes. 

2. Este computador host deve consultar o controlador de domínio quanto à existência de contas (por exemplo, os servidores Exchange)? <br></br>
Há um script ou aplicativo em execução no host que pode gerar esse comportamento? <br></br>
Se a resposta para qualquer uma dessas perguntas for sim, **feche** as atividades suspeitas (é um positivo verdadeiro benigno) e exclua o host da atividade suspeita.

3. Baixe os detalhes do alerta em uma planilha do Excel para convenientemente ver a lista de tentativas de conta, dividido em contas existentes e não existentes. Se você observar a folha de contas não existentes na planilha e as contas parecerem familiares, elas poderão ser contas desabilitadas ou funcionários que saíram da empresa. Nesse caso, é improvável que a tentativa é proveniente de um dicionário. Provavelmente, é um aplicativo ou um script que está verificando quais contas que ainda existem no Active Directory, significando que é um positivo verdadeiro benigno.

3. Se os nomes forem muito desconhecidos, alguma das tentativas de estimativa corresponderá aos nomes de conta existentes no Active Directory? Se não houver nenhuma correspondência, a tentativa foi inútil, mas você deve prestar atenção ao alerta para ver se ele é atualizado ao longo do tempo.

4. Se qualquer uma das tentativas de suposição corresponder nomes de contas existentes, o invasor sabe da existência de contas em seu ambiente e pode tentar usar força bruta para acessar seu domínio usando os nomes de usuário descobertos. Verifique os nomes de conta que foram adivinhados para ver se há atividades suspeitas adicionais. Verifique se todas as contas correspondentes são contas confidenciais.


**Remediação**

[Senhas complexas e longas](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) fornecem o primeiro nível necessário de segurança contra ataques de força bruta.


## <a name="reconnaissance-using-directory-services-queries"></a>Reconhecimento usando consultas de serviços de diretório

**Descrição**

O reconhecimento de serviços de diretório é usado pelos invasores para mapear a estrutura de diretório e visar contas com privilégios para as etapas posteriores em um ataque. O protocolo SAM-R (Remoto do Gerenciador de Conta de Segurança) é um dos métodos usados para consultar o diretório para realizar esse mapeamento.

Nessa detecção, nenhum alerta é disparado no primeiro mês após a implantação do Azure ATP. Durante o período de aprendizado, o Azure ATP cria perfis de quais consultas SAM-R são feitas de quais computadores, de consultas de enumeração e individuais de contas confidenciais.

**Investigação**

1. Clique no alerta para ver sua página de detalhes. Verifique quais consultas foram executadas (por exemplo, administradores corporativos ou administrador) e se elas foram bem-sucedidas.

2. Essas consultas devem ser feitas do computador de origem em questão?

3. Se sim e se o alerta for atualizado, **Suprima** a atividade suspeita.

4. Se sim e se não precisar fazer mais isso, **Feche** a atividade suspeita.

5. Se não houver informações sobre a conta envolvida: essas consultas devem ser feitas por essa conta ou essa conta normalmente faz logon no computador de origem?

 - Se sim e se o alerta for atualizado, **Suprima** a atividade suspeita.

 - Se sim e se não precisar fazer mais isso, **Feche** a atividade suspeita.

 - Se a resposta para todas as perguntas acima for não, suponha que ele seja mal-intencionado.

6. Se não houver informações sobre a conta envolvida, você poderá ir até o ponto de extremidade e verificar qual conta estava conectada no momento do alerta.

**Remediação**

Proteja seu ambiente contra essa técnica usando o seguinte processo:
1. O computador está executando uma ferramenta de verificação de vulnerabilidade?  
2. Investigue se os usuários e grupos específicos consultados no ataque são contas com privilégios ou de alto valor (ou seja, CEO, CFO, gerenciamento de TI, etc.).  Nesse caso, examine outras atividades no ponto de extremidade e monitore os computadores em que as contas consultadas são registradas, como eles são provavelmente destinos para a movimentação lateral.

## <a name="reconnaissance-using-dns"></a>Reconhecimento usando DNS

**Descrição**

O servidor DNS contém um mapa de todos os computadores, endereços IP e serviços em sua rede. Essas informações são usadas pelos invasores para mapear sua estrutura de rede e visar computadores interessantes para etapas posteriores no ataque.

Há vários tipos de consulta no protocolo DNS. O Azure ATP detecta a solicitação AXFR (transferência) proveniente de servidores não DNS.

**Investigação**

1. O computador de origem (**Proveniente de...** ) é um servidor DNS? Se sim, então, provavelmente é um falso positivo. Para validar, clique no alerta para ver sua página de detalhes. Na tabela, em **Consulta**, verifique quais domínios foram consultados. Esses domínios são existentes? Se sim, então, **Feche** a atividade suspeita (é um falso positivo). Além disso, certifique-se de que a porta 53 do UDP esteja aberta entre o sensor autônomo do Azure ATP e o computador de origem para evitar futuros falsos positivos.

2. O computador de origem está executando um verificador de segurança? Em caso afirmativo, **Exclua as entidades** no ATP, seja diretamente com **Fechar e excluir** ou por meio da página **Exclusão** (em **Configuração** – disponível para administradores do Azure ATP).

3. Se a resposta a todas as perguntas anteriores for não, continue investigando, concentrando-se no computador de origem. Clique no computador de origem para acessar a página de perfil. Verifique o que aconteceu no momento da solicitação, pesquisando atividades incomuns, como: quem estava conectado e quais recursos foram acessados. Se você tiver habilitado a integração do Windows Defender ATP, clique no selo do Windows Defender ATP ![Selo do Windows Defender ATP](./media/wd-badge.png) para continuar a investigar o computador. No Windows Defender ATP, você pode ver quais processos e alertas ocorreram no momento do alerta. 

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

## <a name="remote-execution-attempt"></a>Tentativa de execução remota

**Descrição**

Os invasores que comprometem credenciais de administrador ou que usam uma exploração de dia zero podem executar comandos remotos no controlador de domínio. Isso pode ser usado para obter a persistência, coletar informações, ataques DOS (negação de serviço) ou qualquer outro motivo. O Azure ATP detecta conexões PSexec e WMI remoto.

**Investigação**

1. Isso é comum para membros da equipe de TI e de estações de trabalho administrativas ou contas de serviço que executam tarefas administrativas nos controladores de domínio. Se for esse o caso e se o alerta for atualizado desde que o mesmo administrador e/ou computador esteja executando a tarefa, então, **Suprima** o alerta.

2. O **computador** em questão tem permissão para realizar essa execução remota em seu controlador de domínio?

 - A **conta** em questão tem permissão para realizar essa execução remota em seu controlador de domínio?

 - Se a resposta a ambas as perguntas for *Sim*, então, **Feche** o alerta.

3. Se a resposta a uma das perguntas for não, isso deverá ser considerado um positivo verdadeiro. Tente localizar a origem da tentativa verificando perfis de computador e conta. Clique no computador de origem ou na conta para acessar a página de perfil. Verifique o que aconteceu no momento dessas tentativas, pesquisando atividades incomuns, como: quem estava conectado e quais recursos foram acessados. Se você tiver habilitado a integração do Windows Defender ATP, clique no selo do Windows Defender ATP ![Selo do Windows Defender ATP](./media/wd-badge.png) para continuar a investigar o computador. No Windows Defender ATP, você pode ver quais processos e alertas ocorreram no momento do alerta. 

**Remediação**

1. Restrinja o acesso remoto aos controladores de domínio de computadores que não são da camada 0.

2. Implemente [acesso privilegiado](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access) para permitir que apenas computadores protegidos se conectem aos controladores de domínio para administração.

## <a name="suspicious-authentication-failures"></a>Falhas de autenticação suspeitas

**Descrição**

Em um ataque de força bruta, o invasor tenta autenticar com muitas senhas diferentes para diferentes contas até que uma senha correta seja encontrada para pelo menos uma conta. Uma vez encontrada, um invasor pode fazer logon usando essa conta.

Nesta detecção, um alerta é disparado quando ocorrem diversas falhas de autenticação usando Kerberos ou NTLM. Isso pode acontecer horizontalmente com um pequeno conjunto de senhas entre vários usuários, verticalmente com um grande conjunto de senhas em apenas alguns usuários ou qualquer combinação dessas duas opções. O período mínimo antes que um alerta possa ser disparado é de uma semana.

**Investigação**

1.  Clique em **Baixar detalhes** para exibir as informações completas em uma planilha do Excel. Você pode obter as seguintes informações: 
   -    Lista das contas atacadas
   -    Lista de contas adivinhadas em que as tentativas de logon terminaram com a autenticação bem-sucedida
   -    Se as tentativas de autenticação tiverem sido realizadas usando NTLM, você verá as atividades de eventos relevantes 
   -    Se as tentativas de autenticação tiverem sido realizadas usando Kerberos, você verá as atividades de rede relevantes

2.  Clique no computador de origem para acessar a página de perfil. Verifique o que aconteceu no momento dessas tentativas, pesquisando atividades incomuns, como: quem estava conectado e quais recursos foram acessados. Se você tiver habilitado a integração do Windows Defender ATP, clique no selo do Windows Defender ATP ![Selo do Windows Defender ATP](./media/wd-badge.png) para continuar a investigar o computador. No Windows Defender ATP, você pode ver quais processos e alertas ocorreram no momento do alerta. 

3.  Se a autenticação tiver sido executada usando NTLM, você vir que o alerta ocorre muitas vezes e não houver informações suficientes disponíveis sobre o servidor que tentou acessar o computador de origem, você deverá habilitar a **Auditoria de NTLM** nos controladores de domínio envolvidos. Para fazer isso, ative o evento 8004. Esse é o evento de autenticação de NTLM que inclui informações sobre o computador de origem, a conta de usuário e o **servidor** que o computador de origem tentou acessar. Depois que saber qual servidor enviou a validação de autenticação, você deverá investigar o servidor, verificando seus eventos, como 4624, para compreender melhor o processo de autenticação. 

**Remediação**

[Senhas complexas e longas](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy) fornecem o primeiro nível necessário de segurança contra ataques de força bruta.

## <a name="suspicious-domain-controller-promotion-potential-dcshadow-attack---new"></a>Promoção do controlador de domínio suspeito (possível ataque DCShadow) – novo

**Descrição**

Um ataque de sombra do controlador de domínio (DCShadow) é um ataque projetado para alterar objetos do directory usando uma replicação mal-intencionada. Esse ataque pode ser executado de qualquer computador com a criação de um controlador de domínio invasor usando um processo de replicação.
 
O DCShadow usa RPC e LDAP para:
1. Registrar a conta do computador como um controlador de domínio (usando os direitos de administrador de domínio) e
2. Executar a replicação (usando os direitos de replicação concedidos) sobre DRSUAPI e enviar alterações para objetos do directory.
 
Nessa detecção, um alerta é acionado quando um computador na rede está tentando registrar como um controlador de domínio invasor. 

**Investigação**
 
1. O computador em questão é um controlador de domínio? Por exemplo, um controlador de domínio recém-promovido que teve problemas de replicação. Em caso afirmativo, **Fechar** a atividade suspeita.
2. O computador em questão deveria estar replicando dados do Active Directory? Por exemplo, o Azure AD Connect. Se sim, **Feche e exclua** a atividade suspeita.
3. Clique no computador de origem ou na conta para acessar a página de perfil. Verifique o que aconteceu no momento da replicação, pesquisando atividades incomuns, como: quem estava conectado, com quais recursos e qual é o sistema operacional do computador?
   1. Todos os usuários que estavam conectados ao computador deveriam estar conectados a ele? Quais são os privilégios deles? Eles têm permissão para promover um servidor para controlador de domínio? (eles são administradores de domínio)?
   2. Os usuários devem acessar esses recursos?
   3. O computador executa o sistema operacional Windows Server (ou Windows/Linux)? Um computador não servidor não deve replicar os dados.
Se você tiver habilitado a integração do Windows Defender ATP, clique no selo do Windows Defender ATP ![selo do Windows Defender ATP](./media/wd-badge.png) para continuar a investigar o computador. No Windows Defender ATP, você pode ver quais processos e alertas ocorreram no momento do alerta.

4. Examine o Visualizador de Eventos para ver os [eventos do Active Directory que ele registra no log de serviços de diretório](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961809(v=technet.10)). Você pode usar o log para monitorar as alterações no Active Directory. Por padrão, o Active Directory somente registra eventos de erro crítico, mas se esse alerta for recorrente, habilite essa auditoria no controlador de domínio relevante para uma investigação adicional.

**Corrigir**

Verifique quem em sua organização tem as seguintes permissões: 
- Replicar alterações de diretório 
- Replicar todas as alterações de diretório 
 
 
Para obter mais informações, consulte [Conceder permissões do Active Directory Domain Services para sincronização de perfil no SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx). 

Você pode utilizar o [Scanner ACL do AD](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) ou criar um script do Windows PowerShell para determinar quem no domínio tem essas permissões.
 
> [!NOTE]
> As detecções de promoção do controlador de domínio suspeitas (possível ataque DCShadow) só têm suporte nos sensores do ATP. 


## <a name="suspicious-replication-request-potential-dcshadow-attack---new"></a>Solicitação de replicação suspeita (possível ataque DCShadow) – novo

**Descrição** 

A replicação do Active Directory é o processo pelo qual as alterações feitas em um controlador de domínio são sincronizadas com outros controladores de domínio. Com as permissões necessárias, os invasores podem conceder direitos para sua conta do computador, permitindo que represente um controlador de domínio. Os invasores se esforçarão para iniciar uma solicitação de replicação mal-intencionada, permitindo que alterem os objetos do Active Directory em um controlador de domínio original, o que pode dar aos invasores persistência no domínio.
Nessa detecção, um alerta é acionado quando uma solicitação de replicação suspeita é gerada em relação a um controlador de domínio original protegido pelo Azure ATP. O comportamento é uma indicação de técnicas usadas em ataques de sombra do controlador de domínio.

**Investigação** 
 
1. O computador em questão é um controlador de domínio? Por exemplo, um controlador de domínio recém-promovido que teve problemas de replicação. Em caso afirmativo, **Fechar** a atividade suspeita.
2. O computador em questão deveria estar replicando dados do Active Directory? Por exemplo, o Azure AD Connect. Se sim, **Feche e exclua** a atividade suspeita.
3. Clique no computador de origem para acessar a página de perfil. Verifique o que aconteceu no **momento** da replicação, pesquisando atividades incomuns, como: quem estava conectado, quais recursos foram usados e qual é o sistema operacional do computador?

   1.  Todos os usuários que estavam conectados ao computador deveriam estar conectados a ele? Quais são os privilégios deles? Eles têm permissão para realizar replicações (eles são administradores do domínio)?
   2.  Os usuários devem acessar esses recursos?
   3. O computador executa o sistema operacional Windows Server (ou Windows/Linux)? Um computador não servidor não deve replicar os dados.
Se você tiver habilitado a integração do Windows Defender ATP, clique no selo do Windows Defender ATP ![selo do Windows Defender ATP](./media/wd-badge.png) para continuar a investigar o computador. No Windows Defender ATP, você pode ver quais processos e alertas ocorreram no momento do alerta.
1. Examine o Visualizador de Eventos para ver os [eventos do Active Directory que ele registra no log de serviços de diretório](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961809(v=technet.10)). Você pode usar o log para monitorar as alterações no Active Directory. Por padrão, o Active Directory somente registra eventos de erro crítico, mas se esse alerta for recorrente, habilite essa auditoria no controlador de domínio relevante para uma investigação adicional.

**Remediação**

Verifique quem em sua organização tem as seguintes permissões: 
- Replicar alterações de diretório 
- Replicar todas as alterações de diretório 

Para fazer isso, você pode utilizar o [Scanner ACL do AD](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) ou criar um script do Windows PowerShell para determinar quem no domínio tem essas permissões.

> [!NOTE]
> As detecções de solicitações de replicação suspeitas (possível ataque DCShadow) só têm suporte nos sensores do ATP. 


## <a name="suspicious-service-creation"></a>Criação de serviço suspeito

**Descrição**

Um serviço suspeito foi criado em um controlador de domínio em sua organização. Esse alerta se baseia no evento 7045 para identificar a atividade suspeita. 

**Investigação**

1. Se o computador em questão for uma estação de trabalho administrativa ou um computador no qual membros da equipe de TI e contas de serviço executam tarefas administrativas, este pode ser um falso positivo e talvez você precise **Suprimir** o alerta e adicioná-lo à lista de Exclusões, se necessário.

2. O serviço é algo que você reconhece neste computador?

 - A **conta** em questão tem permissão para instalar esse serviço?

 - Se a resposta para ambas as perguntas for *sim*, **Feche** o alerta ou adicione-o à lista de Exclusões.

3. Se a resposta a uma das perguntas for *não*, então, isso deverá ser considerado um positivo verdadeiro.

**Remediação**

- Implementar o acesso com menos privilégios em computadores de domínio para permitir que apenas usuários específicos tenham o direito de criar novos serviços.

## Conexão de VPN suspeita <a name="suspicious-vpn-detection"></a>

**Descrição**

A Azure ATP aprende o comportamento da entidade dos usuários de conexões VPN em um período corrido de um mês. 

O modelo de comportamento de VPN é baseado nas seguintes atividades: os computadores aos quais os usuários se conectam e as localizações de onde eles se conectam. 

Um alerta é aberto quando há um desvio no comportamento do usuário com base no algoritmo de aprendizado de máquina.

**Investigação**

1.  O usuário em questão deveria executar essas operações?
2.  Considere os seguintes casos como possíveis falsos positivos: um usuário que alterou sua localização, um usuário que está viajando e conecta-se de um novo dispositivo.

**Remediação**

1.  Considere a possibilidade de redefinir a senha desse usuário. Isso impede que o invasor crie novas conexões VPN usando as credenciais antigas.
2.  Considere a possibilidade de impedir que esse usuário se conecte por meio da VPN.

## <a name="unusual-protocol-implementation"></a>Implementação de protocolo incomum


**Descrição**

Os invasores usam ferramentas que implementam vários protocolos (SMB, Kerberos, NTLM) de maneiras não padrão. Embora esse tipo de tráfego de rede seja aceito pelo Windows sem avisos, o Azure ATP é capaz de reconhecer possíveis casos mal-intencionados. O comportamento é uma indicação de técnicas como força bruta e de Over-Pass-the-Hash, bem como explorações usadas pelo ransomware avançado, por exemplo, WannaCry.

**Investigação**

Identifique o protocolo que seja incomum – na linha do tempo de atividade Suspeita, clique na atividade suspeita para ir para a página de detalhes; o protocolo é exibido acima da seta: Kerberos ou NTLM.

- **Kerberos**: isso geralmente será disparado se uma ferramenta de invasão como Mimikatz tiver sido usada, potencialmente executando um ataque de Overpass-the-Hash. Verifique se o computador de origem está executando um aplicativo que implementa a sua própria pilha de Kerberos, não de acordo com o RFC Kerberos. Se esse for o caso, é um positivo verdadeiro benigno e você poderá **Fechar** o alerta. Se o alerta continuar sendo disparado e esse ainda for o caso, você poderá **Suprimir** o alerta.

- **NTLM**: pode ser WannaCry ou ferramentas como Metasploit, Medusa e Hydra.  

Para determinar se este é um ataque WannaCry, realize as seguintes etapas:

1. Verifique se o computador de origem está executando uma ferramenta de ataque como Metasploit, Medusa ou Hydra.

2. Se nenhuma ferramenta de ataque for encontrada, verifique se o computador de origem está executando um aplicativo que implementa a sua própria pilha NTLM ou SMB.

3. Clique no computador de origem para acessar a página de perfil. Verifique o que aconteceu no momento do alerta, pesquisando atividades incomuns, como: quem estava conectado e quais recursos foram acessados. Se você tiver habilitado a integração do Windows Defender ATP, clique no selo do Windows Defender ATP ![selo do WD](./media/wd-badge.png) para continuar a investigar o computador. No Windows Defender ATP, você pode ver quais processos e alertas ocorreram no momento do alerta.



**Remediação**

Corrija todos os seus computadores, especialmente aplicando as atualizações de segurança.

1. [Desabilitar SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

2. [Remover WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo)

3. O WanaKiwi poderá descriptografar os dados nas mãos de algum ransoware, mas apenas se o usuário não tiver reiniciado ou desligado o computador. Para obter mais informações, consulte [Ransomware Wanna Cry](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1)


> [!NOTE]
> Para desabilitar uma atividade suspeita, contate o suporte.


## <a name="see-also"></a>Consulte Também
- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)
