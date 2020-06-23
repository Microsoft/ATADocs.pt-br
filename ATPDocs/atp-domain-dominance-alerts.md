---
title: Alertas de segurança de comprometimento de domínio do ATP do Azure
d|Description: This article explains the Azure ATP alerts issued when attacks typically part of domain dominance phase efforts are detected against your organization.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/01/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 0b3a1db5-0d43-49af-b356-7094cc85f0a5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 662ded6bef3e38079173181c41920b2f57e6407d
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2020
ms.locfileid: "84773560"
---
# <a name="tutorial-domain-dominance-alerts"></a>Tutorial: Alertas de predominância de domínio

Normalmente, os ataques cibernéticos são lançados contra alguma entidade acessível, como um usuário com poucos privilégios e, em seguida, se movem lateralmente com rapidez até que o invasor obtenha acesso a ativos valiosos. Os ativos valiosos podem ser contas confidenciais, administradores de domínio ou dados altamente confidenciais. O ATP do Azure identifica essas ameaças avançadas na origem ao longo de toda a cadeia de ataque e classifica-as nas seguintes fases:

1. [Reconhecimento](atp-reconnaissance-alerts.md)
2. [Credenciais comprometidas](atp-compromised-credentials-alerts.md)
3. [Movimentos laterais](atp-lateral-movement-alerts.md)
4. **Comprometimento de domínio**
5. [Exportação](atp-exfiltration-alerts.md)

Para entender melhor a estrutura e os componentes comuns de todos os alertas de segurança do ATP do Azure, confira [Understanding security alerts](understanding-security-alerts.md) (Entendendo os alertas de segurança).

Os alertas de segurança a seguir ajudam você a identificar e corrigir atividades suspeitas da fase de **comprometimento de domínio** detectadas pelo ATP do Azure em sua rede. Neste tutorial, saiba como entender, classificar, evitar e corrigir os ataques a seguir:

> [!div class="checklist"]
>
> * Solicitação mal-intencionada de chave mestra da API de Proteção de Dados (ID externa 2020)
> * Tentativa de execução remota de código – aprimorada (ID externa 2019)
> * Suspeita de ataque de DCShadow (promoção do controlador de domínio) (ID externa 2028)
> * Suspeita de ataque de DCShadow (solicitação de replicação do controlador de domínio) (ID externa 2029)
> * Suspeita de ataque de DCSync (replicação de serviços de diretório) (ID externa 2006)
> * Suspeita de uso de Golden Ticket (downgrade de criptografia) (ID externa 2009)
> * Suspeita de uso de Golden Ticket (dados de autorização forjados) (ID externa 2013)
> * Suspeita de uso de Golden Ticket (conta inexistente) (ID externa 2027)
> * Suspeita de uso de Golden Ticket (anomalia de tíquete) (ID externa 2032)
> * Suspeita de uso de Golden Ticket (anomalia de tempo) – (ID externa 2022)
> * Suspeita de ataque de Skeleton Key (downgrade de criptografia) (ID externa 2010)
> * Adições suspeitas a grupos confidenciais (ID 2024 externa)
> * Criação de serviço suspeito (ID externa 2026)

## <a name="malicious-request-of-data-protection-api-master-key-external-id-2020"></a>Solicitação mal-intencionada de chave mestra da API de Proteção de Dados (ID externa 2020)

*Nome anterior:* Solicitação de informações privadas para proteção contra dados mal-intencionados

**Descrição**

A DPAPI (API de Proteção de Dados) é usada pelo Windows para proteger senhas com segurança salvas por navegadores, arquivos criptografados e outros dados confidencias. Os controladores de domínio têm uma chave mestra de backup que pode ser usada para descriptografar todos os segredos criptografados com DPAPI em computadores Windows ingressados no domínio. Os invasores podem usar a chave mestra para descriptografar informações secretas protegidas por DPAPI em todos os computadores que ingressaram no domínio.
Nessa detecção, o alerta do ATP do Azure é disparado quando o DPAPI é usado para recuperar a chave mestra do backup.

**TP, B-TP ou FP?**

Scanners de segurança avançada podem gerar legitimamente esse tipo de atividade no Active Directory.

1. Verifique se o computador de origem está executando uma verificação de segurança avançada aprovada pela organização em relação ao Active Directory.

    * Se a resposta for **sim** e essa verificação não deveria estar em execução, corrija a configuração do aplicativo. Este alerta é um **B-TP** e pode ser **fechado**.
    * Se a resposta é **sim** e ele deve sempre executar tal verificação, **feche** o alerta e exclua esse computador, provavelmente trata-se de uma atividade **B-TP**.

**Entender o escopo da violação**

1. Investigue o [computador de origem](investigate-a-computer.md).
2. Se um [usuário de origem](investigate-a-user.md) existir, investigue.

**Correção sugerida e etapas de prevenção**

1. Redefina a senha do usuário de origem e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
2. Contenha o computador de origem.
    * Encontre a ferramenta que realizou o ataque e remova-a.
    * Procure usuários que estavam conectados no mesmo período em que a atividade ocorreu, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
3. A chave privada roubada nunca é alterada. Isso significa que o ator pode sempre usar a chave roubada para descriptografar os dados protegidos no domínio de destino. Não existe uma maneira metodológica para alterar essa chave privada.
    * Para criar uma chave, use a chave privada atual, crie uma chave e criptografe novamente todas as chaves mestras de domínio com a nova chave privada.

## <a name="remote-code-execution-attempt-external-id-2019"></a>Tentativa de execução remota de código – aprimorada (ID externa 2019)

*Nome anterior:* Tentativa de execução remota de código

**Descrição**

Os invasores que comprometem credenciais de administrador ou que usam uma exploração de dia zero podem executar comandos remotos no controlador de domínio. Isso pode ser usado para obter a persistência, coletar informações, ataques DOS (negação de serviço) ou qualquer outro motivo. O ATP do Azure detecta conexões PSexec, WMI remoto e PowerShell.

**TP, B-TP ou FP**

Membros da equipe de TI, de estações de trabalho administrativas ou contas de serviço podem executar tarefas administrativas legítimas nos controladores de domínio.

1. Verifique se o usuário ou computador de origem deve executar esses tipos de comandos no controlador de domínio.
    * Se o usuário ou computador de origem precisar executar esses tipos de comandos, **feche** o alerta de segurança como uma atividade **B-TP**.
    * Se o computador de origem ou o usuário deve executar esses comandos em seu controlador de domínio e continuará a fazê-lo, trata-se de uma atividade **B-TP**. **Feche** o alerta de segurança e exclua o computador.

**Entender o escopo da violação**

1. Investigue o [usuário](investigate-a-user.md) e o [computador de origem](investigate-a-computer.md).
2. Investigue o [controlador de domínio](investigate-a-computer.md).

**Correção sugerida e etapas de prevenção:**

**Remediação**

1. Redefina a senha dos usuários de origem e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
2. Contenha os controladores de domínio com as seguintes ações:
    * Corrija a tentativa de execução remota de código.
    * Procure usuários que estavam conectados no mesmo período da atividade suspeita, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
3. Contenha o computador de origem.
    * Encontre a ferramenta que realizou o ataque e remova-a.
    * Procure usuários que estavam conectados no mesmo período da atividade suspeita, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.

**Prevenção**

1. Restrinja o acesso remoto aos controladores de domínio de computadores que não são da camada 0.
2. Implemente o [acesso privilegiado](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access). permitindo que apenas computadores protegidos se conectem aos controladores de domínio para administração.
3. Implemente o acesso com menos privilégios em computadores de domínio para permitir que usuários específicos tenham o direito de criar serviços.

> [!NOTE]
> Somente os sensores do ATP dão suporte a alertas sobre o uso de Comandos do PowerShell em tentativas de execução remota de código.

## <a name="suspected-dcshadow-attack-domain-controller-promotion-external-id-2028"></a>Suspeita de ataque de DCShadow (promoção do controlador de domínio) (ID externa 2028)

*Nome anterior:* Promoção do controlador de domínio suspeito (possível ataque DCShadow)

**Descrição**

Um ataque de sombra do controlador de domínio (DCShadow) é um ataque projetado para alterar objetos do directory usando uma replicação mal-intencionada. Esse ataque pode ser executado de qualquer computador com a criação de um controlador de domínio invasor usando um processo de replicação.

Em um ataque DCShadow, RPC e LDAP são usados para:

1. Registrar a conta do computador como um controlador de domínio (usando os direitos de administrador de domínio).
2. Executar a replicação (usando os direitos de replicação concedidos) sobre DRSUAPI e enviar alterações para objetos do directory.

Nessa detecção do ATP do Azure, um alerta de segurança é acionado quando um computador na rede tenta registrar-se como um controlador de domínio invasor.

**TP, B-TP ou FP**

Se o computador de origem for um controlador de domínio, uma resolução com falha ou de baixa certeza pode impedir que o ATP do Azure consiga confirmar a identificação.

1. Verifique se o computador de origem é um controlador de domínio.
    Se a resposta for **sim**, **feche** o alerta como uma atividade **B-TP**.

Alterações no Active Directory podem levar tempo para sincronizar.

1. O computador de origem é um controlador de domínio recém-promovido? Se a resposta for **sim**, **feche** o alerta como uma atividade **B-TP**.

Servidores e aplicativos podem replicar dados do Active Directory, tais como o Azure AD Connect ou dispositivos de monitoramento de desempenho de rede.

1. Verifique se o computador de origem deve gerar esse tipo de atividade.

    * Se a resposta for **sim**, mas o computador de origem não deverá continuar a gerar esse tipo de atividade no futuro, corrija a configuração do servidor/aplicativo. **Feche** o alerta de segurança como uma atividade **B-TP**.

    * Se a resposta for **sim** e o computador de origem deverá continuar a gerar este tipo de atividade no futuro, **feche** o alerta de segurança como uma atividade **B-TP** e exclua o computador para evitar alertas benignos adicionais.

**Entender o escopo da violação**

1. Investigue o [computador de origem](investigate-a-computer.md).
2. Examine o Visualizador de Eventos para ver os [eventos do Active Directory que ele registra no log de serviços de diretório](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961809(v=technet.10)/). Você pode usar o log para monitorar as alterações no Active Directory. Por padrão, o Active Directory registra somente eventos de erro crítico, mas se esse alerta for recorrente, habilite essa auditoria no controlador de domínio relevante para uma investigação adicional.

**Correção sugerida e etapas de prevenção:**

**Correção:**

1. Contenha o computador de origem.
    * Encontre a ferramenta que realizou o ataque e remova-a.
    * Procure usuários que estavam conectados no mesmo período em que a atividade ocorreu, pois eles também podem estar comprometidos.  
    Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.

**Prevenção:**

Valide as seguintes permissões:

1. Replicar alterações de diretório.
2. Replicar todas as alterações de diretório.
3. Para obter mais informações, consulte [Conceder permissões do Active Directory Domain Services para sincronização de perfil no SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx). Você pode usar o [Scanner ACL do AD](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) ou criar um script do Windows PowerShell para determinar quem no domínio tem essas permissões.

> [!NOTE]
> Os alertas de promoções do controlador de domínio suspeitas (possível ataque DCShadow) só são compatíveis com os sensores do ATP.

## <a name="suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029"></a>Suspeita de ataque de DCShadow (solicitação de replicação do controlador de domínio) (ID externa 2029)

*Nome anterior:* Solicitação de replicação suspeita (possível ataque DCShadow)

**Descrição**

A replicação do Active Directory é o processo pelo qual as alterações feitas em um controlador de domínio são sincronizadas com outros controladores de domínio. Com as permissões necessárias, os invasores podem conceder direitos para sua conta do computador, permitindo que represente um controlador de domínio. Os invasores se esforçam para iniciar uma solicitação de replicação mal-intencionada, permitindo que alterem os objetos do Active Directory em um controlador de domínio original, o que pode dar a eles persistência no domínio.
Nessa detecção, um alerta é acionado quando uma solicitação de replicação suspeita é gerada em relação a um controlador de domínio original protegido pelo Azure ATP. O comportamento é uma indicação de técnicas usadas em ataques de sombra do controlador de domínio.

**TP, B-TP ou FP**

Se o computador de origem for um controlador de domínio, uma resolução com falha ou de baixa certeza poderá impedir a identificação do ATP do Azure.

1. Verifique se o computador de origem é um controlador de domínio.
    Se a resposta for **sim**, **feche** o alerta como uma atividade **B-TP**.

Alterações no Active Directory podem levar tempo para sincronizar.

1. O computador de origem é um controlador de domínio recém-promovido? Se a resposta for **sim**, **feche** o alerta como uma atividade **B-TP**.

Servidores e aplicativos podem replicar dados do Active Directory, tais como o Azure AD Connect ou dispositivos de monitoramento de desempenho de rede.

1. Esse computador de origem devia gerar esse tipo de atividade?

    * Se a resposta for **sim**, mas o computador de origem não deverá continuar a gerar esse tipo de atividade no futuro, corrija a configuração do servidor/aplicativo. **Feche** o alerta de segurança como uma atividade **B-TP**.

    * Se a resposta for **sim** e o computador de origem deverá continuar a gerar este tipo de atividade no futuro, **feche** o alerta de segurança como uma atividade **B-TP** e exclua o computador para evitar alertas **B-TP** adicionais.

**Entender o escopo da violação**

1. Investigue o [computador](investigate-a-computer.md) de origem.

**Correção sugerida e etapas de prevenção**

**Correção:**

1. Contenha o computador de origem.
    * Encontre a ferramenta que realizou o ataque e remova-a.
    * Procure usuários que estavam conectados no mesmo período em que a atividade ocorreu, pois eles também podem estar comprometidos.
    Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
2. Corrija os dados que foram replicados nos controladores de domínio.

**Prevenção:**

Valide as seguintes permissões:

1. Replicar alterações de diretório.
2. Replicar todas as alterações de diretório.
3. Para obter mais informações, consulte [Conceder permissões do Active Directory Domain Services para sincronização de perfil no SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx). Você pode usar o [Scanner ACL do AD](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) ou criar um script do Windows PowerShell para determinar quem no domínio tem essas permissões.

> [!NOTE]
> Os alertas de solicitações de replicação suspeitas (possível ataque DCShadow) são compatíveis somente com os sensores do ATP.

## <a name="suspected-dcsync-attack-replication-of-directory-services-external-id-2006"></a>Suspeita de ataque de DCSync (replicação de serviços de diretório) (ID externa 2006)

*Nome anterior:* Replicação mal-intencionada de serviços de diretório

**Descrição**

A replicação do Active Directory é o processo pelo qual as alterações feitas em um controlador de domínio são sincronizadas com todos os outros controladores de domínio. Com as permissões necessárias, os invasores podem iniciar uma solicitação de replicação, permitindo que eles possam recuperar os dados armazenados no Active Directory, incluindo hashes de senha.

Nessa detecção, um alerta é disparado quando uma solicitação de replicação for iniciada em um computador que não seja um controlador de domínio.

> [!NOTE]
> Se você tem controladores de domínio nos quais os sensores do Azure ATP não estejam instalados, estes controladores de domínio não estão cobertos pelo Azure ATP. Ao implantar um novo controlador de domínio em um controlador de domínio não registrado ou desprotegido, ele poderá não ser identificado imediatamente pelo ATP do Azure como um controlador de domínio. É altamente recomendável instalar o sensor do Azure ATP em todos os controladores de domínio para obter uma cobertura completa.

**TP, B-TP ou FP**

Se o computador de origem for um controlador de domínio, uma resolução com falha ou de baixa certeza poderá impedir a identificação do ATP do Azure.

1. Verifique se o computador de origem é um controlador de domínio.
    Se a resposta for **sim**, **feche** o alerta como uma atividade **B-TP**.

Alterações no Active Directory podem levar tempo para sincronizar.

1. O computador de origem é um controlador de domínio recém-promovido? Se a resposta for **sim**, **feche** o alerta como uma atividade **B-TP**.

Servidores e aplicativos podem replicar dados do Active Directory, tais como o Azure AD Connect ou dispositivos de monitoramento de desempenho de rede.

1. Esse computador de origem devia gerar esse tipo de atividade?

    * Se a resposta for **sim**, mas o computador de origem não deverá continuar a gerar esse tipo de atividade no futuro, corrija a configuração do servidor/aplicativo. **Feche** o alerta de segurança como uma atividade **B-TP**.

    * Se a resposta for **sim** e o computador de origem deverá continuar a gerar este tipo de atividade no futuro, **feche** o alerta de segurança como uma atividade **B-TP** e exclua o computador para evitar alertas benignos adicionais.

**Entender o escopo da violação**

1. Investigue o [usuário](investigate-a-user.md) e o [computador](investigate-a-computer.md) de origem.

**Correção sugerida e etapas de prevenção:**

**Correção:**

1. Redefina a senha dos usuários de origem e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
2. Contenha o computador de origem.
    * Encontre a ferramenta que realizou o ataque e remova-a.
    * Procure usuários que estavam conectados no mesmo período em que a atividade ocorreu, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.

**Prevenção:**

Valide as seguintes permissões:

1. Replicar alterações de diretório.
2. Replicar todas as alterações de diretório.
3. Para obter mais informações, consulte [Conceder permissões do Active Directory Domain Services para sincronização de perfil no SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx). Você pode usar o [Scanner ACL do AD](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) ou criar um script do Windows PowerShell para determinar quem no domínio tem essas permissões.

## <a name="suspected-golden-ticket-usage-encryption-downgrade-external-id-2009"></a>Suspeita de uso de Golden Ticket (downgrade de criptografia) (ID externa 2009)

*Nome anterior:* Atividade de downgrade de criptografia

**Descrição**

O downgrade de criptografia é um método de enfraquecer o Kerberos fazendo downgrade do nível de criptografia de diferentes campos do protocolo que normalmente têm o nível mais alto de criptografia. Um campo criptografado enfraquecido pode ser um alvo mais fácil para tentativas de força bruta offline. Vários métodos de ataque utilizam criptografias Kerberos fracas. Nessa detecção, o ATP do Azure aprende os tipos de criptografia Kerberos usados por computadores e usuários e alerta você quando é usada uma criptografia mais fraca e que seja incomum para o usuário e/ou o computador de origem e que corresponda a técnicas de ataque conhecidas.

Em um alerta de Golden Ticket, o método de criptografia do campo TGT da mensagem TGS_REQ (solicitação de serviço) do computador de origem foi detectado como um downgrade em comparação com o comportamento aprendido anteriormente. Isso não tem base em uma anomalia de tempo (como na outra detecção Golden Ticket). Além disso, no caso desse alerta, não houve nenhuma solicitação de autenticação Kerberos associada à solicitação de serviço anterior detectada pelo ATP do Azure.

**TP, B-TP ou FP**

Alguns recursos legítimos não dão suporte à criptografia forte e podem disparar este alerta.

1. Todos os usuários de origem compartilham algo em comum?
   1. Por exemplo, todos os membros da equipe de marketing estão acessando um recurso específico que pode fazer com que o alerta seja disparado?
   2. Verifique os recursos acessados por esses tíquetes.
      * Confira isso no Active Directory verificando o atributo *msDS-SupportedEncryptionTypes*, da conta de serviço do recurso.
   3. Se houver apenas um recurso sendo acessado, verifique se é um recurso válido que esses usuários devem acessar.

      Se a resposta a uma das perguntas anteriores for **sim**, provavelmente essa será uma atividade **T-BP**. Verifique se o recurso pode dar suporte a uma codificação de criptografia forte, implemente uma codificação de criptografia mais forte sempre que possível e **feche** o alerta de segurança.

Os aplicativos podem ser autenticados usando uma codificação de criptografia inferior. Alguns estão autenticando em nome dos usuários, como servidores do IIS e SQL.

1. Verifique se todos os usuários de origem compartilham algo em comum.
    * Por exemplo, todos os membros de sua equipe de vendas usam um aplicativo específico que pode disparar o alerta?
    * Verifique se há aplicativos desse tipo no computador de origem.
    * Verifique as funções do computador.  
    Eles são servidores que funcionam com esses tipos de aplicativos?

     Se a resposta a uma das perguntas anteriores for **sim**, provavelmente essa será uma atividade **T-BP**. Verifique se o recurso pode dar suporte a uma codificação de criptografia forte, implemente uma codificação de criptografia mais forte sempre que possível e **feche** o alerta de segurança.

**Entender o escopo da violação**

1. Investigue o [computador de origem e os recursos](investigate-a-computer.md) que foram acessados.
2. Investigue os [usuários](investigate-a-computer.md).

**Correção sugerida e etapas de prevenção**

**Remediação**

1. Redefina a senha do usuário de origem e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
2. Contenha o computador de origem.
    * Encontre a ferramenta que realizou o ataque e remova-a.
    * Procure usuários que estavam conectados no horário da atividade, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
    * Se o Microsoft Defender ATP estiver instalado – use **klist.exe purge** para excluir todos os tíquetes da sessão de logon especificada e evitar o uso dos tíquetes no futuro.
2. Contenha os recursos que foram acessados por esse tíquete.
3. Altere o Tíquete de concessão de tíquete Kerberos (KRBTGT) duas vezes de acordo com as diretrizes em [Scripts de redefinição de senha da conta KRBTGT disponíveis agora para clientes](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) usando a [ferramenta Redefinir chaves/senha da conta KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).
    * A redefinição dupla do KRBTGT invalida todos os tíquetes Kerberos nesse domínio. A invalidação de todos os tíquetes Kerberos no domínio significa que **todos** os serviços serão interrompidos e não funcionarão novamente até que sejam renovados ou em alguns casos, que o serviço seja reiniciado.
    * **Planeje cuidadosamente antes de executar a redefinição dupla do KRBTGT. A redefinição dupla do KRBTGT afeta todos os computadores, servidores e usuários no ambiente.**

4. Verifique se todos os controladores de domínio com sistemas operacionais até o Windows Server 2012 R2 estão instalados com o [KB3011780](https://www.microsoft.com/download/details.aspx?id=44978) e todos os servidores membros e controladores de domínio até 2012 R2 estão atualizados com o [KB2496930](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privileg). Para obter mais informações, consulte  [PAC Prata](https://technet.microsoft.com/library/security/ms11-013.aspx)  e  [PAC Forjado](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="suspected-golden-ticket-usage-forged-authorization-data-external-id-2013"></a>Suspeita de uso de Golden Ticket (dados de autorização forjados) (ID externa 2013)

Nome anterior: Elevação de privilégios usando dados de autorização forjados

**Descrição**

As vulnerabilidades conhecidas em versões mais antigas do Windows Server permitem que os invasores manipulem o PAC (Certificado de Atributo Privilegiado), um campo no tíquete Kerberos que contém os dados de autorização do usuário (no Active Directory essa é a associação de grupo), concedendo ao invasor privilégios adicionais.

**TP, B-TP ou FP**

Em computadores nos quais foram aplicados os patches MS14-068 (controlador de domínio) ou MS11-013 (servidor), tentativas de ataque não terão êxito e gerarão o erro de Kerberos.

1. Verifique quais recursos foram acessados na lista de evidências de alerta de segurança e se as tentativas tiveram êxito ou falharam.
2. Verifique se os patches foram aplicados nos computadores acessados, conforme descrito acima.
    * Se os patches foram aplicados nos computadores, **feche** o alerta de segurança como uma atividade **B-TP**.

Sabe-se que alguns sistemas operacionais ou aplicativos modificam os dados de autorização. Por exemplo, serviços de Linux e Unix têm seu próprio mecanismo de autorização, o qual pode disparar o alerta.

1. O computador de origem está executando um sistema operacional ou aplicativo que tem seu próprio mecanismo de autorização?
    * Se o computador de origem estiver executando esse tipo de mecanismo de autorização, considere atualizar o sistema operacional ou corrigir a configuração do aplicativo. **Feche** o alerta como uma atividade **B-TP**.

**Entender o escopo da violação**

1. Investigue o [computador de origem](investigate-a-computer.md).
2. Se houver um [usuário de origem](investigate-a-user.md), investigue.
3. Verificar quais recursos foram acessados com êxito e [investigue](investigate-a-computer.md).

**Correção sugerida e etapas de prevenção**

1. Redefina a senha do usuário de origem e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
2. Conter o computador de origem
    * Encontre a ferramenta que realizou o ataque e remova-a.
    * Procure por usuários que estavam conectados em horário próximo àquele da atividade, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
3. Altere o Tíquete de concessão de tíquete Kerberos (KRBTGT) duas vezes de acordo com as diretrizes em [Scripts de redefinição de senha da conta KRBTGT disponíveis agora para clientes](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) usando a [ferramenta Redefinir chaves/senha da conta KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).
    * A redefinição dupla do KRBTGT invalida todos os tíquetes Kerberos nesse domínio. A invalidação de todos os tíquetes Kerberos no domínio significa que **todos** os serviços serão interrompidos e não funcionarão novamente até que sejam renovados ou em alguns casos, que o serviço seja reiniciado. Planeje cuidadosamente antes de realizar a redefinição dupla do KRBTGT, porque ela afeta todos os computadores, servidores e usuários no ambiente.
4. Verifique se todos os controladores de domínio com sistemas operacionais até o Windows Server 2012 R2 estão instalados com o [KB3011780](https://www.microsoft.com/download/details.aspx?id=44978) e todos os servidores membros e controladores de domínio até 2012 R2 estão atualizados com o [KB2496930](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privileg). Para obter mais informações, consulte  [PAC Prata](https://technet.microsoft.com/library/security/ms11-013.aspx)  e  [PAC Forjado](https://technet.microsoft.com/library/security/ms14-068.aspx).

## <a name="suspected-golden-ticket-usage-nonexistent-account-external-id-2027"></a>Suspeita de uso de Golden Ticket (conta inexistente) (ID externa 2027)

Nome anterior: Golden Ticket do Kerberos

**Descrição**

Os invasores com direitos de administrador de domínio podem comprometer a conta KRBTGT. Ao usar a conta KRBTGT, eles podem criar um tíquete de concessão de tíquete Kerberos (TGT) que fornece autorização para qualquer recurso e define a expiração do tíquete para qualquer momento arbitrário. Esse TGT falso é chamado de "Golden Ticket" e permite que os invasores obtenham persistência na rede. Nessa detecção, um alerta é disparado por uma conta inexistente.

**TP, B-TP ou FP**

Alterações no Active Directory podem levar tempo para sincronizar.
1. O usuário é um usuário de domínio válido e conhecido?
2. O usuário foi adicionado recentemente?
3. O usuário foi excluído recentemente do Active Directory?

Se a resposta a todas as perguntas anteriores for **sim**, **feche** o alerta como uma atividade **B-TP**.

**Entender o escopo da violação**

1. Investigue o [computador de origem e os recursos acessados](investigate-a-computer.md).

**Correção sugerida e etapas de prevenção**

1. Conter os computadores de origem
    * Encontre a ferramenta que realizou o ataque e remova-a.
    * Procure por usuários que estavam conectados em horário próximo àquele da atividade, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
    * Se o Microsoft Defender ATP estiver instalado – use **klist.exe purge** para excluir todos os tíquetes da sessão de logon especificada e evitar o uso dos tíquetes no futuro.
2. Contenha os recursos que foram acessados por esse tíquete.
3. Altere o Tíquete de concessão de tíquete Kerberos (KRBTGT) duas vezes de acordo com as diretrizes em [Scripts de redefinição de senha da conta KRBTGT disponíveis agora para clientes](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) usando a [ferramenta Redefinir chaves/senha da conta KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).
    * A redefinição dupla do KRBTGT invalida todos os tíquetes Kerberos nesse domínio. A invalidação de todos os tíquetes Kerberos no domínio significa que **todos** os serviços serão interrompidos e não funcionarão novamente até que sejam renovados ou em alguns casos, que o serviço seja reiniciado. Planeje cuidadosamente antes de realizar a redefinição dupla do KRBTGT, porque ela afeta todos os computadores, servidores e usuários no ambiente.

## <a name="suspected-golden-ticket-usage-ticket-anomaly-external-id-2032"></a>Suspeita de uso de Golden Ticket (anomalia de tíquete) (ID externa 2032)

**Descrição**

Os invasores com direitos de administrador de domínio podem comprometer a conta KRBTGT. Ao usar a conta KRBTGT, eles podem criar um tíquete de concessão de tíquete Kerberos (TGT) que fornece autorização para qualquer recurso e define a expiração do tíquete para qualquer momento arbitrário. Esse TGT falso é chamado de "Golden Ticket" e permite que os invasores obtenham persistência na rede. Os Golden Tickets forjados desse tipo têm características exclusivas que essa detecção foi projetada especificamente para identificar. 

**TP, B-TP ou FP**

Os serviços de federação podem gerar tíquetes que disparam esse alerta.
1. O computador de origem hospeda serviços de federação que geram esses tipos de tíquetes?
    * Se o computador de origem hospedar serviços que geram esses tipos de tíquetes, feche o alerta de segurança como uma atividade **B-TP**.

**Entender o escopo da violação**

1. Investigue o [computador de origem e os recursos acessados](investigate-a-computer.md).
2. Investigue o [usuário de origem](investigate-a-user.md).

**Correção sugerida e etapas de prevenção**

1. Conter os computadores de origem
    * Encontre a ferramenta que realizou o ataque e remova-a.
    * Procure por usuários que estavam conectados em horário próximo àquele da atividade, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
    * Se o Microsoft Defender ATP estiver instalado – use **klist.exe purge** para excluir todos os tíquetes da sessão de logon especificada e evitar o uso dos tíquetes no futuro.
2. Contenha os recursos que foram acessados por esse tíquete.
3. Altere o Tíquete de concessão de tíquete Kerberos (KRBTGT) duas vezes de acordo com as diretrizes em [Scripts de redefinição de senha da conta KRBTGT disponíveis agora para clientes](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) usando a [ferramenta Redefinir chaves/senha da conta KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).
    * A redefinição dupla do KRBTGT invalida todos os tíquetes Kerberos nesse domínio. A invalidação de todos os tíquetes Kerberos no domínio significa que **todos** os serviços são interrompidos e não funcionam novamente até que sejam renovados ou em alguns casos, que o serviço seja reiniciado.

    **Planeje cuidadosamente antes de executar uma redefinição dupla do KRBTGT. A redefinição afeta todos os computadores, servidores e usuários no ambiente.**

## <a name="suspected-golden-ticket-usage-time-anomaly-external-id-2022"></a>Suspeita de uso de Golden Ticket (anomalia de tempo) – (ID externa 2022)

Nome anterior: Golden Ticket do Kerberos

**Descrição**

Os invasores com direitos de administrador de domínio podem comprometer a conta KRBTGT. Ao usar a conta KRBTGT, eles podem criar um tíquete de concessão de tíquete Kerberos (TGT) que fornece autorização para qualquer recurso e define a expiração do tíquete para qualquer momento arbitrário. Esse TGT falso é chamado de "Golden Ticket" e permite que os invasores obtenham persistência na rede. Esse alerta é disparado quando um tíquete de concessão de tíquete Kerberos é usado por mais tempo do que o permitido pela especificação Máximo tempo de vida do tíquete de usuário.

**TP, B-TP ou FP**

1. Nas últimas horas, houve alguma alteração à configuração**Tempo de vida máximo para tíquete de usuário** na política de grupo que fosse capaz de afetar o alerta?
2. O sensor autônomo do ATP do Azure envolvido neste alerta é uma máquina virtual?
    * Se o sensor autônomo do ATP do Azure está envolvido, ele foi recentemente retomado de um estado salvo?
3. Há um problema de sincronização de horário na rede, em que nem todos os computadores estão sincronizados?
    * Clique no botão **Detalhes do download** para exibir o alerta de segurança do arquivo do Excel de relatório, exibir as atividades de rede relacionadas e verificar se há uma diferença entre "StartTime" e "DomainControllerStartTime".

Se a resposta às perguntas anteriores for **sim**, **feche** o alerta de segurança como uma atividade **B-TP**.

**Entender o escopo da violação**

1. Investigue o [computador de origem e os recursos acessados](investigate-a-computer.md).
2. Investigue o [usuário comprometido](investigate-a-user.md).

**Correção sugerida e etapas de prevenção**

1. Contenha o computador de origem.
    * Encontre a ferramenta que realizou o ataque e remova-a.
    * Procure por usuários que estavam conectados em horário próximo àquele da atividade, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
    * Se o Microsoft Defender ATP estiver instalado – use **klist.exe purge** para excluir todos os tíquetes da sessão de logon especificada e evitar o uso dos tíquetes no futuro.
2. Contém os recursos acessados por esse tíquete.
3. Altere o Tíquete de concessão de tíquete Kerberos (KRBTGT) duas vezes de acordo com as diretrizes em [Scripts de redefinição de senha da conta KRBTGT disponíveis agora para clientes](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) usando a [ferramenta Redefinir chaves/senha da conta KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51).
    * A redefinição dupla do KRBTGT invalida todos os tíquetes Kerberos nesse domínio. A invalidação de todos os tíquetes Kerberos no domínio significa que **todos** os serviços são interrompidos e não funcionam novamente até que sejam renovados ou, em alguns casos, que o serviço seja reiniciado.

    **Planeje cuidadosamente antes de executar uma redefinição dupla do KRBTGT. A redefinição afeta todos os computadores, servidores e usuários no ambiente.**

## <a name="suspected-skeleton-key-attack-encryption-downgrade-external-id-2010"></a>Suspeita de ataque de skeleton key (downgrade de criptografia) (ID externa 2010)

*Nome anterior:* Atividade de downgrade de criptografia

**Descrição**

O downgrade de criptografia é um método de enfraquecer o Kerberos usando um nível de criptografia que sofreu downgrade em diferentes campos do protocolo, que normalmente têm o nível mais alto de criptografia. Um campo criptografado enfraquecido pode ser um alvo mais fácil para tentativas de força bruta offline. Vários métodos de ataque utilizam criptografias Kerberos fracas. Nessa detecção, o ATP do Azure aprende os tipos de criptografia Kerberos usados por computadores e usuários. O alerta será emitido quando for usada uma criptografia mais fraca que seja incomum para o usuário e/ou computador de origem e que corresponda a técnicas de ataque conhecidas.

Skeleton Key é um malware que é executado nos controladores de domínio e permite a autenticação no domínio com qualquer conta sem saber sua senha. Este malware geralmente usa algoritmos de criptografia mais fracos para fazer o hash das senhas do usuário no controlador de domínio. Nesse alerta, o comportamento aprendido da criptografia de mensagem KRB_ERR anterior, do controlador de domínio para a conta que solicita um tíquete, sofreu downgrade.

**Entender o escopo da violação**

1. Investigue o [controlador de domínio](investigate-a-computer.md).
2. Verifique se a Skeleton Key afetou os controladores de domínio usando o [scanner gravado pela equipe do ATP do Azure](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73).
3. Investigue os [usuários](investigate-a-user.md) e [computadores](investigate-a-computer.md) envolvidos.

**Correção sugerida e etapas de prevenção**

1. Redefina as senhas dos usuários comprometidos e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
2. Conter o controlador de domínio.
    * Remover o malware. Para saber mais, veja [Análise do malware Skeleton Key](https://www.virusbulletin.com/virusbulletin/2016/01/paper-digital-bian-lian-face-changing-skeleton-key-malware).
    * Procure usuários que estavam conectados no mesmo período em que a atividade suspeita ocorreu, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.

## <a name="suspicious-additions-to-sensitive-groups-external-id-2024"></a>Adições suspeitas a grupos confidenciais (ID 2024 externa)

**Descrição**

Os invasores adicionam usuários a grupos altamente privilegiados. A adição de usuários é realizada para obter acesso a mais recursos e obter persistência. Essa detecção conta com a criação de perfil de atividades de modificação do grupo de usuários e com o alerta para quando uma adição anormal a um grupo confidencial é vista. O ATP do Azure cria perfis continuamente.

Para ver uma definição de grupos confidenciais no Azure ATP, consulte [Trabalhando com contas confidenciais](sensitive-accounts.md).

A detecção depende de eventos auditados em controladores de domínio. Verifique se os controladores de domínio estão [auditando os eventos necessários](atp-advanced-audit-policy.md).

**Período de aprendizado**

Quatro semanas por controlador de domínio, começando no primeiro evento.

**TP, B-TP ou FP**

Modificações de grupo legítimas que raramente ocorrem e que o sistema não aprende como "normais" podem disparar um alerta. Esses alertas seriam considerados **B-TP**.
1. A modificação do grupo é legítima?
    * Se a modificação do grupo é legítima, **feche** o alerta de segurança como uma atividade **B-TP**.

**Entender o escopo da violação**

1. Investigue os usuários adicionados a grupos.
    * Concentre-se nas atividades deles após a adição deles aos grupos confidenciais.
2. Investigue o usuário de origem.
    * Baixe o relatório **Modificação de grupos confidenciais** para ver quais outras modificações foram feitas e por quem durante o mesmo período de tempo.
3. Investigue os computadores nos quais o usuário de origem fez logon na época da atividade.

**Correção sugerida e etapas de prevenção**

**Correção:**

1. Redefina a senha do usuário de origem e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
    * Procure o computador no qual o usuário de origem estava ativo.
    * Verifique em quais computadores o usuário estava conectado em horário próximo ao da atividade. Verifique se esses computadores estão comprometidos.
    * Se os usuários estiverem comprometidos, redefina as senhas deles e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.

**Prevenção:**

1. Para evitar ataques futuros, minimize a quantidade de pessoas autorizadas a modificar grupos confidenciais.
2. Configure o Privileged Access Management para Active Directory se aplicável.

## <a name="suspicious-service-creation-external-id-2026"></a>Criação de serviço suspeito (ID externa 2026)

*Nome anterior:* Criação de serviço suspeito

**Descrição**

Um serviço suspeito foi criado em um controlador de domínio em sua organização. Esse alerta se baseia no evento 7045 para identificar a atividade suspeita.

**TP, B-TP ou FP**

Algumas tarefa administrativa são realizadas de modo legítimo em controladores de domínio por membros da equipe de TI, estações de trabalho administrativas ou contas de serviço.

1. O usuário/computador de origem deveria executar esses tipos de serviços no controlador de domínio?
    * Se o usuário ou computador de origem deveria executar esses tipos de serviços e não deve continuar a fazê-lo, **feche** o alerta como uma atividade **B-TP**.
    * Se o usuário ou computador de origem deveria executar esses tipos de serviços e deve continuar a fazê-lo, **feche** o alerta de segurança como uma atividade **B-TP** e exclua esse computador.

**Entender o escopo da violação**

1. Investigue o [usuário de origem](investigate-a-user.md).
2. Investigue os [computadores de destino](investigate-a-computer.md) nos quais os serviços foram criados.

**Correção sugerida e etapas de prevenção**

**Remediação**

1. Redefina a senha do usuário de origem e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
2. Conter os controladores de domínio.
    * Corrigir o serviço suspeito.
    * Procure usuários que estavam conectados no horário da atividade, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
3. Localize o computador no qual o usuário de origem estava ativo.
    * Verifique os computadores aos quais o usuário estava conectado no horário da atividade e verifique se esses computadores também estão comprometidos.

**Prevenção:**

1. Restrinja o acesso remoto aos controladores de domínio de computadores que não são da camada 0.
2. Implemente [acesso privilegiado](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/securing-privileged-access) para permitir que apenas computadores protegidos se conectem aos controladores de domínio para administradores.
3. Implemente o acesso com menos privilégios em computadores de domínio para permitir apenas que usuários específicos tenham o direito de criar serviços.

> [!div class="nextstepaction"]
> [Tutorial de alertas de exportação](atp-exfiltration-alerts.md)

## <a name="see-also"></a>Consulte Também

* [Investigar um computador](investigate-a-computer.md)
* [Trabalhando com alertas de segurança](working-with-suspicious-activities.md)
* [Trabalhando com caminhos de movimento lateral](use-case-lateral-movement-path.md)
* [Alertas de reconhecimento](atp-reconnaissance-alerts.md)
* [Alertas de credencial comprometida](atp-compromised-credentials-alerts.md)
* [Alertas de movimento lateral](atp-lateral-movement-alerts.md)
* [Alertas de exfiltração](atp-exfiltration-alerts.md)
* [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
