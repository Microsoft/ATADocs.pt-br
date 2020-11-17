---
title: Guia de atividade suspeita do ATA
description: Este artigo fornece uma lista de atividades suspeitas que o ATA pode detectar e etapas de correção.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 04/03/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1fe5fd6f-1b79-4a25-8051-2f94ff6c71c1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: eeccc1e5a5dd16b2d480bf82034a085159baff60
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690084"
---
# <a name="advanced-threat-analytics-suspicious-activity-guide"></a>Guia de atividades suspeitas Advanced Threat Analytics

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Após investigação adequada, qualquer atividade suspeita pode ser classificada como:

- **Verdadeiro positivo**: uma ação mal intencionada detectada pelo ATA.

- **Verdadeiro positivo benigno**: uma ação detectada pelo ATA que é real, mas não é mal intencionada, como um teste de penetração.
- **Falso positivo**: um alarme falso, o que significa que a atividade não aconteceu.

Para saber mais sobre como trabalhar com alertas ATA, confira [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md).

Para dúvidas ou comentários, entre em contato com a equipe do ATA em [ATAEval@microsoft.com](mailto:ATAEval@microsoft.com) .

## <a name="abnormal-modification-of-sensitive-groups"></a>Modificação anormal de grupos confidenciais

**Descrição**

Os invasores adicionam usuários a grupos altamente privilegiados. Eles fazem isso para obter acesso a mais recursos e obter persistência. As detecções contam com a criação de perfil das atividades de modificação do grupo de usuários e com o alerta para quando uma adição anormal a um grupo confidencial é vista. A criação de perfil é executada continuamente pelo ATA. O período mínimo antes do acionamento de um alerta é de um mês por controlador de domínio.

Para obter uma definição de grupos confidenciais no ATA, consulte [Trabalhando com o console do ATA](working-with-ata-console.md#sensitive-groups).

A detecção depende de [eventos auditados em controladores de domínio](configure-event-collection.md).
Para verificar se seus controladores de domínio realizam a auditoria de eventos necessários, use a ferramenta referenciada em [Auditoria do ATA (AuditPol, Aplicação de configurações de auditoria avançadas, descoberta de serviço do Gateway Lightweight)](https://aka.ms/ataauditingblog).

**Investigação**

1. A modificação do grupo é legítima? </br>As modificações de grupo legítimas que raramente ocorrem e não foram aprendidas como "normais" podem causar um alerta, o que seria considerado um verdadeiro positivo benigno.

1. Se o objeto adicionado for uma conta de usuário, verifique quais ações a conta de usuário realizou após ser adicionada ao grupo de administrador. Vá para a página do usuário no ATA para obter mais contexto. Houve alguma outra atividade suspeita associada à conta antes ou após a adição ocorrer? Baixe o relatório **Modificação de grupos confidenciais** para ver quais outras modificações foram feitas e por quem durante o mesmo período de tempo.

**Remediação**

Minimize a quantidade de pessoas que estão autorizadas a modificar grupos confidenciais.

Configure [Privileged Access Management para Active Directory](/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) se aplicável.

## <a name="broken-trust-between-computers-and-domain"></a>Confiança quebrada entre domínio e computadores

> [!NOTE]
> O alerta de confiança quebrada entre domínio e computadores foi preterido e só aparece nas versões anteriores ao ATA 1.9.

**Descrição**

Confiança quebrada significa que os requisitos de segurança do Active Directory podem não estar em vigor para estes computadores. Isso é considerado uma falha de conformidade e segurança de linha de base e um alvo fácil para os invasores. Nessa detecção, um alerta será acionado se mais de cinco falhas de autenticação Kerberos forem vistas de uma conta de computador no período de 24 horas.

**Investigação**

O computador que está sendo investigado permite que os usuários de domínio façam logon?
- Se sim, é possível ignorar esse computador nas etapas remediação.

**Remediação**

Ingresse novamente o computador no domínio se necessário ou redefina a senha do computador.

## <a name="brute-force-attack-using-ldap-simple-bind"></a>Ataque de força bruta usando associação simples LDAP

**Descrição**

>[!NOTE]
> A principal diferença entre **Falhas de autenticação suspeitas** e esta detecção é que, nessa detecção, o ATA pode determinar se senhas diferentes foram usadas.

Em um ataque de força bruta, o invasor tenta autenticar com muitas senhas diferentes para diferentes contas até que uma senha correta seja encontrada para pelo menos uma conta. Uma vez encontrada, um invasor pode fazer logon usando essa conta.

Nessa detecção, um alerta é disparado quando o ATA detecta um grande número de autenticações de associação simples. Isso pode ser *horizontalmente* com um pequeno conjunto de senhas entre vários usuários; ou *verticalmente "* com um grande conjunto de senhas em apenas alguns usuários; ou qualquer combinação dessas duas opções.

**Investigação**

1. Se houver muitas contas envolvidas, clique em **Baixar detalhes** para exibir a lista em uma planilha do Excel.

1. Clique no alerta para ir até a página dedicada. Verifique se alguma tentativa de logon terminou com uma autenticação bem-sucedida. As tentativas aparecerem como **Contas adivinhadas** no lado direito do infográfico. Se sim, alguma das **Contas adivinhadas** é normalmente usada pelo computador de origem? Se sim, **Omita** a atividade suspeita.

1. Se não houver nenhuma **Conta adivinhada**, alguma das **Contas atacadas** é normalmente usada no computador de origem? Se sim, **Omita** a atividade suspeita.

**Remediação**

[Senhas complexas e longas](/windows/device-security/security-policy-settings/password-policy) fornecem o primeiro nível necessário de segurança contra ataques de força bruta.

## <a name="encryption-downgrade-activity"></a>Atividade de downgrade de criptografia

**Descrição**

O downgrade de criptografia é um método para enfraquecer o Kerberos fazendo um downgrade do nível de criptografia de diferentes campos do protocolo que normalmente são criptografados usando o nível mais elevado de criptografia. Um campo criptografado enfraquecido pode ser um alvo mais fácil para tentativas de força bruta offline. Vários métodos de ataque utilizam criptografias Kerberos fracas. Nessa detecção, o ATA aprende os tipos de criptografia Kerberos usados por computadores e usuários e alerta você quando uma criptografia mais fraca é usada que: (1) seja incomum para o computador de origem e/ou o usuário; e (2) corresponda a técnicas de ataque conhecidas.

Há três tipos de detecção:

1. Skeleton Key – é um malware que é executado nos controladores de domínio e permite a autenticação no domínio com qualquer conta sem saber sua senha. Este malware geralmente usa algoritmos de criptografia mais fracos para fazer o hash das senhas do usuário no controlador de domínio. Nesta detecção, o método de criptografia da mensagem KRB_ERR do controlador de domínio para a conta, solicitando um tíquete, passou por um downgrade em comparação com o comportamento aprendido anteriormente.

1. Golden Ticket – em um alerta [Golden Ticket](#golden-ticket), o método de criptografia do campo TGT da mensagem TGS_REQ (solicitação de serviço) do computador de origem foi desatualizado em comparação com o comportamento aprendido anteriormente. Isso não tem base em uma anomalia de tempo (como na outra detecção Golden Ticket). Além disso, não houve nenhuma solicitação de autenticação Kerberos associada à solicitação de serviço anterior detectada pelo ATA.

1. Overpass-the-Hash – um invasor pode usar um hash roubado fraco para criar um tíquete forte com uma solicitação do Kerberos AS. Nesta detecção, o tipo de criptografia de mensagem AS_REQ do computador de origem passou por downgrade em comparação com o comportamento aprendido anteriormente (ou seja, o computador estava usando AES).

**Investigação**

Primeiro, verifique a descrição do alerta para ver quais dos três tipos de detecção acima você está lidando. Para obter mais informações, baixe a planilha do Excel.

1. Skeleton Key – você pode verificar se a Skeleton Key afetou os controladores de domínio usando o [analisador gravado pela equipe do ATA](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73). Se o analisador encontrar malware em 1 ou mais controladores de domínio, é um verdadeiro positivo.
1. Bilhete dourado – na planilha do Excel, vá para a guia **atividade de rede** . Você verá que o campo de downgrade relevante é **solicitar tipo de criptografia de tíquete** e **tipos de criptografia com suporte do computador de origem** lista métodos de criptografia mais fortes.
    1. Verifique o computador de origem e a conta, ou se houver vários computadores de origem e contas, verifique se eles têm algo em comum (por exemplo, toda a equipe de marketing usa um aplicativo específico que pode estar fazendo com que o alerta seja disparado). Há casos em que um aplicativo personalizado raramente usado faz autenticação usando uma codificação de criptografia inferior. Verifique se há algum desses aplicativos personalizados no computador de origem. Nesse caso, ele é provavelmente um positivo verdadeiro benigno e pode ser **Suprimido**.
    1. Verifique o recurso acessado por esses tíquetes, se houver um recurso que todos estão acessando, valide-o, verifique se ele é um recurso válido que ele deveria acessar. Além disso, verifique se o recurso de destino dá suporte a métodos de criptografia forte. Você pode verificar isso no Active Directory verificando o atributo `msDS-SupportedEncryptionTypes`, da conta de serviço do recurso.
1. Overpass-The-hash – na planilha do Excel, vá para a guia **atividade de rede** . Você verá que o campo downgrade relevante é o **tipo de criptografia de carimbo de data/hora criptografado** e os tipos de **criptografia com suporte do computador de origem** contêm métodos de criptografia mais fortes
    1. há casos em que esse alerta pode ser disparado quando os usuários fazem logon usando cartões inteligentes se a configuração do cartão inteligente foi alterada recentemente. Verifique se ocorreram alterações como essa para a(s) conta(s) envolvida(s). Nesse caso, ele é provavelmente um positivo verdadeiro benigno e pode ser **Suprimido**.
    1. Verifique o recurso acessado por esses tíquetes, se houver um recurso que todos estão acessando, valide-o, verifique se ele é um recurso válido que ele deveria acessar. Além disso, verifique se o recurso de destino dá suporte a métodos de criptografia forte. Você pode verificar isso no Active Directory verificando o atributo `msDS-SupportedEncryptionTypes`, da conta de serviço do recurso.

**Remediação**

1. Skeleton Key – Remova malware. Para saber mais, veja [Análise do malware Skeleton Key](https://www.virusbulletin.com/virusbulletin/2016/01/paper-digital-bian-lian-face-changing-skeleton-key-malware).

1. Golden Ticket – Siga as instruções das atividades suspeitas do [Golden Ticket](#golden-ticket).
    Além disso, como a criação de um bilhete dourado exige direitos de administrador de domínio, implemente [as recomendações de passagem de hash](https://www.microsoft.com/download/details.aspx?id=36036).

1. Overpass-the-Hash – Se a conta envolvida não for confidencial, então, redefina a senha dessa conta. Isso impede que o invasor crie novos tíquetes Kerberos do hash de senha, embora os tíquetes existentes ainda possam ser usados até expirarem. Se for uma conta confidencial, você deve considerar redefinir a conta KRBTGT duas vezes como na atividade suspeita de tíquete dourado. Redefinir o KRBTGT duas vezes invalida todos os tíquetes Kerberos nesse domínio, portanto, planeje antes de fazer isso. Consulte as diretrizes em [Scripts de redefinição de senha da conta KRBTGT disponíveis agora para os clientes](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/). Consulte também usando a [redefinir as senhas/chaves da conta KRBTGT

    ferramenta] ( https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51) . Como essa é uma técnica de movimentação lateral, siga as práticas recomendadas das [recomendações de Passagem de hash](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="honeytoken-activity"></a>Atividade de Honeytoken

**Descrição**

As contas Honeytoken são contas fictícias configuradas para identificar e rastrear atividades mal-intencionadas que envolvem essas contas. Contas de Honeytoken devem ser deixadas como não utilizadas, enquanto têm um nome atraente para atrair invasores (por exemplo, SQL-Admin). Qualquer atividade delas pode indicar comportamento mal-intencionado.

Para obter mais informações sobre contas do honey token, confira [Instalar o ATA – Etapa 7](install-ata-step7.md).

**Investigação**

1. Verifique se o proprietário do computador de origem usou a conta Honeytoken para autenticar, usando o método descrito na página de atividades suspeitas (por exemplo, Kerberos, LDAP, NTLM).

1. Navegue até as páginas de perfil de computador(es) de origem e verifique quais outras contas se autenticaram por meio delas. Verifique com os proprietários dessas contas se eles usaram a conta Honeytoken.

1. Isso pode ser um logon não interativo, portanto, certifique-se de verificar se há aplicativos ou scripts que são executados no computador de origem.

Se depois de executar as etapas 1 a 3, se não houver evidência de uso benigno, suponha que isso seja mal-intencionado.

**Remediação**

Certifique-se de que as contas Honeytoken sejam usadas apenas para sua finalidade pretendida, caso contrário, elas podem gerar muitos alertas.

## <a name="identity-theft-using-pass-the-hash-attack"></a>Roubo de identidade usando o ataque de passagem de Hash

**Descrição**

Pass-the-Hash é uma técnica de movimento lateral em que os invasores roubam o hash NTLM de um usuário de um computador e o usam para acessar outro computador.

**Investigação**

O hash utilizado era de um computador de propriedade ou usado regularmente pelo usuário alvo? Em caso afirmativo, o alerta é um falso positivo, caso contrário, ele é provavelmente um positivo verdadeiro.

**Remediação**

1. Se a conta envolvida não for confidencial, redefina a senha dessa conta. Redefinir a senha impede que o invasor crie novos tíquetes Kerberos de hash de senha. Os tíquetes existentes ainda podem ser usados até expirarem.

1. Se a conta envolvida for confidencial, considere redefinir a conta KRBTGT duas vezes, como na atividade suspeita do Golden Ticket. Redefinir o KRBTGT duas vezes invalida todos os tíquetes de Kerberos do domínio, portanto, planeje de acordo com o impacto antes de fazer isso. Confira as diretrizes em [Scripts de redefinição de senha da conta KRBTGT disponíveis agora para clientes](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), confira também como usar a [ferramenta Redefinir chaves/senha da conta KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Como essa é normalmente uma técnica de movimentação lateral, siga as práticas recomendadas das [recomendações de Passagem de hash](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="identity-theft-using-pass-the-ticket-attack"></a>Roubo de identidade usando o ataque Pass-the-Ticket

**Descrição**

Pass-the-Ticket é uma técnica de movimento lateral em que os invasores roubam um tíquete Kerberos de um computador e o usam para acessar outro computador reutilizando o tíquete roubado. Nessa detecção, um tíquete Kerberos é visto sendo usado em dois (ou mais) computadores diferentes.

**Investigação**

1. Clique no botão **Baixar detalhes** para exibir a lista completa de endereços IP envolvidos. O endereço IP de um ou ambos os computadores faz parte de uma sub-rede alocada de um pool de DHCP subdimensionado, por exemplo, Wi-Fi ou VPN? O endereço IP é compartilhado? Por exemplo, por um dispositivo NAT? Se a resposta para qualquer uma dessas perguntas for sim, o alerta será um falso positivo.

1. Há um aplicativo personalizado que encaminha os tíquetes em nome dos usuários? Nesse caso, é um positivo verdadeiro benigno.

**Remediação**

1. Se a conta envolvida não for confidencial, então, redefina a senha dessa conta. Reenviar a senha impede que o invasor crie novos tíquetes Kerberos de hash de senha. Todos os tíquetes existentes permanecem utilizáveis até que expirem.

1. Se for uma conta confidencial, você deve considerar redefinir a conta KRBTGT duas vezes como na atividade suspeita de tíquete dourado. Redefinir o KRBTGT duas vezes invalida todos os tíquetes Kerberos nesse domínio, portanto, planeje antes de fazer isso. Consulte as diretrizes em [Scripts de redefinição de senha da conta KRBTGT disponíveis agora para clientes](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/), consulte também como usar a [ferramenta Redefinir chaves/senha da conta KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).  Como essa é uma técnica de movimentação lateral, siga as práticas recomendadas nas [recomendações de Passagem de hash](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="kerberos-golden-ticket-activity"></a>Atividade Golden Ticket do Kerberos<a name="golden-ticket"></a>

**Descrição**

Os invasores com direitos de administrador de domínio podem comprometer sua [conta KRBTGT](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn745899(v=ws.11)#Sec_KRBTGT). Os invasores podem usar a conta KRBTGT para criar um Tíquete de Concessão de Tíquete Kerberos (TGT) fornecendo autorização para qualquer recurso. A expiração do tíquete pode ser definida para qualquer horário arbitrário. Esse TGT falso é chamado de "Golden Ticket" e permite que os invasores obtenham e mantenham a persistência na sua rede.

Nessa detecção, um alerta é acionado quando um tíquete de concessão de tíquete Kerberos (TGT) for usado por mais tempo do que o permitido conforme especificado na política de segurança [Tempo de vida máximo para tíquete de usuário](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj852169(v=ws.11)).

**Investigação**

1. Houve alguma alteração recente (dentro das últimas horas) feita no **tempo de vida máximo para a configuração de tíquete de usuário** na diretiva de grupo? Em caso afirmativo, **feche** o alerta (ele era um falso positivo).

1. O Gateway do ATA envolvido nesse alerta é uma máquina virtual? Se Sim, ele retomou recentemente de um estado salvo? Em caso afirmativo, **feche** este alerta.

1. Se a resposta para as perguntas acima for não, suponha que ele seja mal-intencionado.

**Remediação**

Altere o Tíquete de concessão de tíquete Kerberos (KRBTGT) duas vezes de acordo com as diretrizes em [Scripts de redefinição de senha da conta KRBTGT disponíveis agora para clientes](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) usando a [ferramenta Redefinir chaves/senha da conta KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). Redefinir o KRBTGT duas vezes invalida todos os tíquetes Kerberos nesse domínio, portanto, planeje antes de fazer isso.
Além disso, como a criação de um bilhete dourado exige direitos de administrador de domínio, implemente [as recomendações de passagem de hash](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="malicious-data-protection-private-information-request"></a>Solicitação mal-intencionada de informações privadas para proteção de dados

**Descrição**

A DPAPI (API de Proteção de Dados) é usada pelo Windows para proteger senhas com segurança salvas por navegadores, arquivos criptografados e outros dados confidencias. Os controladores de domínio têm uma chave mestra de backup que pode ser usada para descriptografar todos os segredos criptografados com DPAPI em computadores Windows ingressados no domínio. Os invasores podem usar essa chave mestra para descriptografar informações secretas protegidas por DPAPI em todos os computadores que ingressaram no domínio.
Nessa detecção, um alerta é acionado quando o DPAPI é usado para recuperar a chave mestra do backup.

**Investigação**

1. O computador de origem está executando uma verificação de segurança avançada aprovada pela organização em relação ao Active Directory?

1. Em caso positivo e se ele sempre tiver de fazer isso, **Feche e exclua** a atividade suspeita.

1. Em caso positivo e se ele não tiver de fazer isso, **Feche a atividade suspeita.

**Remediação**

Para usar DPAPI, um invasor precisa de direitos de administrador de domínio. Implemente as [recomendações de Pass the hash](https://www.microsoft.com/download/details.aspx?id=36036).

## <a name="malicious-replication-of-directory-services"></a>Replicação mal-intencionada de serviços de diretório

**Descrição**

A replicação do Active Directory é o processo pelo qual as alterações feitas em um controlador de domínio são sincronizadas com todos os outros controladores de domínio. Com as permissões necessárias, os invasores podem iniciar uma solicitação de replicação, permitindo que eles possam recuperar os dados armazenados no Active Directory, incluindo hashes de senha.

Nessa detecção, um alerta é disparado quando uma solicitação de replicação for iniciada em um computador que não seja um controlador de domínio.

**Investigação**

1. O computador em questão é um controlador de domínio? Por exemplo, um controlador de domínio recém-promovido que teve problemas de replicação. Em caso afirmativo, **Fechar** a atividade suspeita.
1. O computador em questão deveria estar replicando dados do Active Directory? Por exemplo, o Azure AD Connect. Se sim, **Feche e exclua** a atividade suspeita.
1. Clique no computador de origem ou na conta para acessar a página de perfil. Verifique o que aconteceu no momento da replicação, pesquisando atividades incomuns, como: quem estava conectado e quais recursos foram acessados.

**Remediação**

Valide as seguintes permissões:

- Replicar alterações de diretório

- Replicar todas as alterações de diretório

Para obter mais informações, consulte [Conceder permissões do Active Directory Domain Services para sincronização de perfil no SharePoint Server 2013](/SharePoint/administration/user-profile-service-administration).
Você pode utilizar o [Scanner ACL do AD](/archive/blogs/pfesweplat/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool) ou criar um script do Windows PowerShell para determinar quem no domínio tem essas permissões.

## <a name="massive-object-deletion"></a>Exclusão de objeto grande

**Descrição**

Em alguns cenários, os invasores executam ataques de negação de serviço (DoS) em vez de apenas roubar informações. Excluir um grande número de contas é um método de tentativa de ataque DoS.

Nessa detecção, um alerta é disparado a qualquer momento em que mais de 5% de todas as contas for excluído. A detecção requer o acesso de leitura ao contêiner do objeto excluído.
Para obter informações sobre como configurar permissões de somente leitura no contêiner Objetos excluídos, confira a seção **Alterar permissões em um contêiner de objetos excluídos** no tópico [Exibir ou definir permissões em um objeto de diretório](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc816824(v=ws.10)).

**Investigação**

Examine a lista de contas excluídas e determine se há um padrão ou um motivo comercial que justifique uma exclusão em larga escala.

**Remediação**

Remova as permissões para usuários que podem excluir contas no Active Directory. Para obter mais informações, consulte [Exibir ou definir permissões em um objeto de diretório](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc816824(v=ws.10)).

## <a name="privilege-escalation-using-forged-authorization-data"></a>Elevação de privilégios usando dados de autorização forjados

**Descrição**

Vulnerabilidades conhecidas em versões mais antigas do Windows Server permitem que os invasores manipulem o PAC (Certificado de Acesso Privilegiado). O PAC é um campo no tíquete Kerberos que tem os dados de autorização do usuário (no Active Directory essa é a associação de grupo) e concede privilégios adicionais aos invasores.

**Investigação**

1. Clique no alerta para acessar a página de detalhes.

1. O computador de destino (sob a coluna **ACESSADO**) tem patch MS14-068 (controlador de domínio) ou MS11-013 (servidor)? Se sim, **Feche** a atividade suspeita (é um falso positivo).

1. Se o computador de destino não for corrigido, o computador de origem executa um sistema operacional/aplicativo (na coluna **DE**) conhecido para modificar o PAC? Em caso afirmativo, **Suprima** a atividade suspeita (é um positivo verdadeiro benigno).

1. Se a resposta às duas perguntas anteriores for não, assuma que essa atividade é mal-intencionada.

**Remediação**

Verifique se todos os controladores de domínio com sistemas operacionais até o Windows Server 2012 R2 estão instalados com o [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege) e todos os servidores membros e controladores de domínio até 2012 R2 estão atualizados com KB2496930. Para obter mais informações, consulte [PAC Prata](/security-updates/SecurityBulletins/2011/ms11-013) e [PAC Forjado](/security-updates/SecurityBulletins/2014/ms14-068).

## <a name="reconnaissance-using-account-enumeration"></a>Reconhecimento de enumeração de conta

**Descrição**

No reconhecimento de enumeração de conta, um invasor usa um dicionário com milhares de nomes de usuário ou ferramentas como KrbGuess para tentar adivinhar nomes de usuário em seu domínio. O invasor faz solicitações Kerberos usando esses nomes para tentar localizar um nome de usuário válido no domínio. Se uma estimativa com êxito determinar um nome de usuário, o invasor obterá o erro de Kerberos **Pré-autenticação necessária** em vez de **Entidade de segurança desconhecida**.

Nesta detecção, o ATA pode detectar de onde veio o ataque, o número total de tentativas de previsão e quantas foram correspondidos. Se houver muitos usuários desconhecidos, o ATA detectará como uma atividade suspeita.

**Investigação**

1. Clique no alerta para ver sua página de detalhes.

    1. Este computador host deve consultar o controlador de domínio quanto à existência de contas (por exemplo, os servidores Exchange)?

1. Há um script ou aplicativo em execução no host que pode gerar esse comportamento?

    Se a resposta para qualquer uma dessas perguntas for sim, **feche** as atividades suspeitas (é um positivo verdadeiro benigno) e exclua o host da atividade suspeita.

1. Baixe os detalhes do alerta em uma planilha do Excel para convenientemente ver a lista de tentativas de conta, dividido em contas existentes e não existentes. Se você observar a folha de contas não existentes na planilha e as contas parecerem familiares, elas poderão ser contas desabilitadas ou funcionários que saíram da empresa. Nesse caso, é improvável que a tentativa é proveniente de um dicionário. Provavelmente, é um aplicativo ou um script que está verificando quais contas que ainda existem no Active Directory, significando que é um positivo verdadeiro benigno.

1. Se os nomes forem muito desconhecidos, alguma das tentativas de estimativa corresponderá aos nomes de conta existentes no Active Directory? Se não houver nenhuma correspondência, a tentativa foi inútil, mas você deve prestar atenção ao alerta para ver se ele é atualizado ao longo do tempo.

1. Se qualquer uma das tentativas de suposição corresponder nomes de contas existentes, o invasor sabe da existência de contas em seu ambiente e pode tentar usar força bruta para acessar seu domínio usando os nomes de usuário descobertos. Verifique os nomes de conta que foram adivinhados para ver se há atividades suspeitas adicionais. Verifique se todas as contas correspondentes são contas confidenciais.

**Remediação**

[Senhas complexas e longas](/windows/device-security/security-policy-settings/password-policy) fornecem o primeiro nível necessário de segurança contra ataques de força bruta.

## <a name="reconnaissance-using-directory-services-queries"></a>Reconhecimento usando consultas de serviços de diretório

**Descrição**

O reconhecimento de serviços de diretório é usado pelos invasores para mapear a estrutura de diretório e visar contas com privilégios para as etapas posteriores em um ataque. O protocolo SAM-R (Remoto do Gerenciador de Conta de Segurança) é um dos métodos usados para consultar o diretório para realizar esse mapeamento.

Nessa detecção, nenhum alerta será disparado no primeiro mês após a implantação do ATA. Durante o período de aprendizado, o ATA cria perfis de quais consultas SAM-R são feitas de quais computadores, de consultas de enumeração e individuais de contas confidenciais.

**Investigação**

1. Clique no alerta para ver sua página de detalhes. Verifique quais consultas foram executadas (por exemplo, administradores corporativos ou administrador) e se elas foram bem-sucedidas.

1. Essas consultas devem ser feitas do computador de origem em questão?

1. Se sim e se o alerta for atualizado, **Suprima** a atividade suspeita.

1. Se sim e se não precisar fazer mais isso, **Feche** a atividade suspeita.

1. Se houver informações sobre a conta envolvida: essas consultas devem ser feitas por essa conta ou essa conta normalmente faz logon no computador de origem?

   - Se sim e se o alerta for atualizado, **Suprima** a atividade suspeita.

   - Se sim e se não precisar fazer mais isso, **Feche** a atividade suspeita.

   - Se a resposta para todas as perguntas acima for não, suponha que ele seja mal-intencionado.

1. Se não houver informações sobre a conta envolvida, você poderá ir até o ponto de extremidade e verificar qual conta estava conectada no momento do alerta.

**Remediação**

Use a [ferramenta SAMRi10](https://gallery.technet.microsoft.com/SAMRi10-Hardening-Remote-48d94b5b) para proteger seu ambiente contra essa técnica.
Se a ferramenta não for aplicável ao seu controlador de domínio:
1. O computador está executando uma ferramenta de verificação de vulnerabilidade?
1. Investigue se os usuários e grupos específicos consultados no ataque são contas com privilégios ou de alto valor (ou seja, CEO, CFO, gerenciamento de TI, etc.).  Nesse caso, examine outras atividades no ponto de extremidade e monitore os computadores em que as contas consultadas são registradas, como eles são provavelmente destinos para a movimentação lateral.

## <a name="reconnaissance-using-dns"></a>Reconhecimento usando DNS

**Descrição**

O servidor DNS contém um mapa de todos os computadores, endereços IP e serviços em sua rede. Essas informações são usadas pelos invasores para mapear sua estrutura de rede e visar computadores interessantes para etapas posteriores no ataque.

Há vários tipos de consulta no protocolo DNS. O ATA detecta a solicitação AXFR (transferência) proveniente de servidores não DNS.

**Investigação**

1. O computador de origem (**Proveniente de...**) é um servidor DNS? Se sim, então, provavelmente é um falso positivo. Para validar, clique no alerta para ver sua página de detalhes. Na tabela, em **Consulta**, verifique quais domínios foram consultados. Esses domínios são existentes? Se sim, então, **Feche** a atividade suspeita (é um falso positivo). Além disso, certifique-se de que a porta 53 do UDP esteja aberta entre o Gateway do ATA e o computador de origem para evitar futuros falsos positivos.
1. O computador de origem está executando um verificador de segurança? Em caso afirmativo, **exclua** as entidades no ATA, seja diretamente com **fechar e excluir** ou por meio da página de **exclusão** (em **configuração** – disponível para administradores do ATA).
1. Se a resposta a todas as perguntas anteriores for não, continue investigando, concentrando-se no computador de origem. Clique no computador de origem para acessar a página de perfil. Verifique o que aconteceu no momento da solicitação, pesquisando atividades incomuns, como: quem estava conectado e quais recursos foram acessados.

**Remediação**

A proteção de um servidor DNS interno para impedir que o reconhecimento usando DNS ocorra pode ser obtida desabilitando ou restringindo as transferências de zona apenas para endereços IP específicos. Para obter mais informações sobre como restringir transferências de zona, consulte [Restringir transferências de zona](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649273(v=ws.10)).
A modificação de transferências de zona é uma tarefa entre uma lista de verificação que deve ser resolvida para [proteger seus servidores DNS contra ataques internos e externos](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770432(v=ws.11)).

## <a name="reconnaissance-using-smb-session-enumeration"></a>Reconhecimento usando a enumeração da sessão SMB

**Descrição**

A enumeração do protocolo SMB (Bloco de mensagens de servidor) permite que invasores obtenham informações sobre onde os usuários se conectaram recentemente. Depois que os invasores tiverem essas informações, eles podem mover lateralmente na rede para obter uma determinada conta confidencial.

Nessa detecção, um alerta é acionado quando uma enumeração de sessão SMB é executada em um controlador de domínio.

**Investigação**

1. Clique no alerta para ver sua página de detalhes. Verifique as contas que realizaram a operação e quais contas foram expostas, se houver.

   - Há algum tipo de verificador de segurança em execução no computador de origem? Se sim, **Feche e exclua** a atividade suspeita.

1. Verifique quais usuários envolvidos realizaram a operação. Eles normalmente se registram no computador de origem ou eles são administradores que deveriam realizar essas ações?

1. Se sim e se o alerta for atualizado, **Suprima** a atividade suspeita.

1. Se sim e não deve ser atualizado, **Feche** a atividade suspeita.

1. Se a resposta para todas as perguntas acima for não, assuma que a atividade é mal-intencionada.

**Remediação**

Use a [ferramenta Net Cease](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b) para proteger seu ambiente contra esse tipo de ataque.

## <a name="remote-execution-attempt-detected"></a>Tentativa de execução remota detectada

**Descrição**

Os invasores que comprometem credenciais de administrador ou que usam uma exploração de dia zero podem executar comandos remotos no controlador de domínio. Isso pode ser usado para obter a persistência, coletar informações, ataques DOS (negação de serviço) ou qualquer outro motivo. O ATA detecta conexões PSexec e WMI remoto.

**Investigação**

1. Isso é comum para membros da equipe de TI, de estações de trabalho administrativas e contas de serviço que executam tarefas administrativas nos controladores de domínio. Se for esse o caso e se o alerta for atualizado porque o mesmo administrador ou computador está executando a tarefa, **Suprima** o alerta.
1. O computador em questão tem permissão para realizar essa execução remota em seu controlador de domínio?
   - A conta em questão tem permissão para realizar essa execução remota em seu controlador de domínio?
   - Se a resposta a ambas as perguntas for sim, **feche** o alerta.
1. Se a resposta a uma das perguntas for não, essa atividade deverá ser considerada um positivo verdadeiro. Tente localizar a origem da tentativa verificando perfis de computador e conta. Clique no computador de origem ou na conta para acessar a página de perfil. Verifique o que aconteceu no momento dessas tentativas, pesquisando atividades incomuns, como: quem estava conectado e quais recursos foram acessados.

**Remediação**

1. Restrinja o acesso remoto aos controladores de domínio de computadores que não são da camada 0.

1. Implemente [acesso privilegiado](/windows-server/identity/securing-privileged-access/securing-privileged-access) para permitir que apenas computadores protegidos se conectem aos controladores de domínio para administração.

## <a name="sensitive-account-credentials-exposed--services-exposing-account-credentials"></a>Credenciais de contas confidenciais expostas e serviços que expõem credenciais da conta

> [!NOTE]
> Essa atividade suspeita foi preterida e só aparece nas versões do ATA anteriores à 1.9. Para o ATA 1.9 e posterior, veja [Relatórios](reports.md).

**Descrição**

Alguns serviços enviam as credenciais de conta em texto sem formatação. Isso pode ocorrer até mesmo para contas confidenciais. Os invasores que monitoram o tráfego de rede podem capturar e reutilizar essas credenciais para fins mal-intencionados. Qualquer senha de texto não criptografada para uma conta confidencial dispara o alerta, enquanto para contas não confidenciais o alerta é disparado se cinco ou mais contas diferentes enviarem senhas em texto não criptografado no mesmo computador de origem.

**Investigação**

Clique no alerta para ver sua página de detalhes. Veja quais contas foram expostas. Se houver muitas contas assim, clique em **Baixar detalhes** para exibir a lista em uma planilha do Excel.

Geralmente, há um script ou aplicativo herdado nos computadores de origem que usa a associação simples LDAP.

**Remediação**

Verifique a configuração nos computadores de origem e certifique-se de não usar a associação LDAP simples. Em vez de usar as ligações LDAP simples, use LDAP SALS ou LDAPS.

## <a name="suspicious-authentication-failures"></a>Falhas de autenticação suspeitas

**Descrição**

Em um ataque de força bruta, o invasor tenta autenticar com muitas senhas diferentes para diferentes contas até que uma senha correta seja encontrada para pelo menos uma conta. Uma vez encontrada, um invasor pode fazer logon usando essa conta.

Nesta detecção, um alerta é disparado quando ocorrem diversas falhas de autenticação usando Kerberos ou NTLM. Isso pode acontecer horizontalmente com um pequeno conjunto de senhas entre vários usuários, verticalmente com um grande conjunto de senhas em apenas alguns usuários ou qualquer combinação dessas duas opções. O período mínimo antes que um alerta possa ser disparado é de uma semana.

**Investigação**

1. Clique em **Baixar detalhes** para exibir as informações completas em uma planilha do Excel. Você pode obter as seguintes informações:
   - Lista das contas atacadas
   - Lista de contas adivinhadas em que as tentativas de logon terminaram com a autenticação bem-sucedida
   - Se as tentativas de autenticação tiverem sido realizadas usando NTLM, você verá as atividades de eventos relevantes
   - Se as tentativas de autenticação tiverem sido realizadas usando Kerberos, você verá as atividades de rede relevantes
1. Clique no computador de origem para acessar a página de perfil. Verifique o que aconteceu no momento dessas tentativas, pesquisando atividades incomuns, como: quem estava conectado e quais recursos foram acessados.
1. Se a autenticação tiver sido executada usando NTLM, você vir que o alerta ocorre muitas vezes e não houver informações suficientes disponíveis sobre o servidor que tentou acessar o computador de origem, você deverá habilitar a **Auditoria de NTLM** nos controladores de domínio envolvidos. Para fazer isso, ative o evento 8004. Esse é o evento de autenticação de NTLM que inclui informações sobre o computador de origem, a conta de usuário e o **servidor** que o computador de origem tentou acessar. Depois que souber qual servidor enviou a validação de autenticação, você deverá investigar o servidor, verificando seus eventos, como 4624, para compreender melhor o processo de autenticação.

**Remediação**

[Senhas complexas e longas](/windows/device-security/security-policy-settings/password-policy) fornecem o primeiro nível necessário de segurança contra ataques de força bruta.

## <a name="suspicious-service-creation"></a>Criação de serviço suspeita <a name="suspicious-service-creation"></a>

**Descrição**

Os invasores tentam executar serviços suspeitos em sua rede. O ATA emite um alerta quando um novo serviço suspeito é criado em um controlador de domínio. Esse alerta baseia-se no evento 7045 e é detectado em cada controlador de domínio coberto por um Gateway do ATA ou por um Gateway Lightweight.

**Investigação**

1. Se o computador em questão for uma estação de trabalho administrativa ou um computador no qual membros da equipe de TI e contas de serviço executam tarefas administrativas, este pode ser um falso positivo e talvez você precise **Suprimir** o alerta e adicioná-lo à lista de Exclusões, se necessário.

1. O serviço é algo que você reconhece neste computador?

   - A **conta** em questão tem permissão para instalar esse serviço?

   - Se a resposta para ambas as perguntas for *sim*, **Feche** o alerta ou adicione-o à lista de Exclusões.

1. Se a resposta a uma das perguntas for *não*, então, isso deverá ser considerado um positivo verdadeiro.

**Remediação**

- Implemente o acesso com menos privilégios em computadores de domínio para permitir que apenas usuários específicos tenham o direito de criar novos serviços.

## <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>Suspeita de roubo de identidade com base no comportamento anormal

**Descrição**

O ATA aprende o comportamento de entidade para usuários, computadores e recursos em um período de três semanas corridas. O modelo de comportamento é baseado nas seguintes atividades: os computadores nos quais as entidades se registram, os recursos para os quais a entidade solicitou acesso e a hora em que essas operações foram realizadas. O ATA envia um alerta quando há um desvio do comportamento da entidade com base nos algoritmos de aprendizado de máquina.

**Investigação**

1. O usuário em questão deveria executar essas operações?

1. Considere os seguintes casos como possíveis falsos positivos: um usuário que retornou de férias, a equipe de TI que realiza o acesso em excesso como parte de seu serviço (por exemplo um aumento no suporte de help desk em um determinado dia ou semana), aplicativos de área de trabalho remota. + Se você **Fechar e excluir** o alerta, o usuário não será mais parte da detecção

**Remediação**

 Diferentes ações devem ser tomadas, dependendo do que causou esse comportamento anormal. Por exemplo, se a rede foi verificada, o computador de origem deve ser bloqueado da rede (a menos que seja aprovado).

## <a name="unusual-protocol-implementation"></a>Implementação de protocolo incomum

**Descrição**

Os invasores usam ferramentas que implementam vários protocolos (SMB, Kerberos, NTLM) de maneiras não padrão. Embora esse tipo de tráfego de rede seja aceito pelo Windows sem avisos, o ATA é capaz de reconhecer possíveis mal-intencionados. O comportamento é uma indicação de técnicas como Over-Pass-the-Hash, bem como explorações usadas por ransomware avançado, como WannaCry.

**Investigação**

Identifique o protocolo que seja incomum – na linha do tempo de atividade suspeita, clique na atividade suspeita para acessar a página de detalhes; o protocolo é exibido acima da seta: Kerberos ou NTLM.

- **Kerberos**: geralmente disparado se uma ferramenta de invasão como Mimikatz foi potencialmente usada no ataque de Overpass-the-Hash. Verifique se o computador de origem está executando um aplicativo que implementa a sua própria pilha de Kerberos, isto não está de acordo com o RFC Kerberos. Nesse caso, ele é um positivo verdadeiro benigno e o alerta pode ser **Fechado**. Se o alerta continuar sendo disparado e esse ainda for o caso, você poderá **Suprimir** o alerta.

- **NTLM**: pode ser WannaCry ou ferramentas como Metasploit, Medusa e Hydra.

Para determinar se esta atividade é um ataque WannaCry, realize as seguintes etapas:

1. Verifique se o computador de origem está executando uma ferramenta de ataque como Metasploit, Medusa ou Hydra.

1. Se nenhuma ferramenta de ataque for encontrada, verifique se o computador de origem está executando um aplicativo que implementa a sua própria pilha NTLM ou SMB.

1. Caso contrário, verifique se é causado pelo WannaCry executando um script de verificação de WannaCry, por exemplo [este analisador](https://github.com/apkjet/TrustlookWannaCryToolkit/tree/master/scanner) no computador de origem envolvido na atividade suspeita. Se o analisador descobrir que o computador está infectado ou vulnerável, aplique patches no computador, remova o malware e bloqueie-o da rede.

1. Se o script não considerar que o computador está infectado ou vulnerável, então, ele ainda poderá estar infectado, mas o SMBv1 pode ter sido desabilitado ou o computador foi corrigido, o que afetaria a ferramenta de verificação.

**Remediação**

Aplique as correções mais recentes a todas as suas máquinas e verifique se todas as atualizações de segurança foram aplicadas.

1. [Desabilitar SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

1. [Remover WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo)

1. Os dados no controle de alguns software de ransomware, às vezes, podem ser descriptografados. A descriptografia só é possível se o usuário não tiver reiniciado ou desligado o computador. Para obter mais informações, consulte [Ransomware Wanna Cry](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1)

>[!NOTE]
> Para desabilitar um alerta de atividade suspeita, contate o suporte.

## <a name="related-videos"></a>Vídeos Relacionados

- [Participar da comunidade de segurança](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community)

## <a name="see-also"></a>Consulte Também

- [Manual da atividade suspeita do ATA](https://aka.ms/ataplaybook)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
