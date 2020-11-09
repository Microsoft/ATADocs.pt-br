---
title: Tutorial do guia estratégico de reconhecimento do Microsoft Defender para Identidade
description: O tutorial do guia estratégico de reconhecimento do Microsoft Defender para Identidade descreve como simular ameaças de Reconhecimento para detecção pelo Defender.
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 25f21451a61f3d41b5694e3b594769e4f8b1614b
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93275759"
---
# <a name="tutorial-reconnaissance-playbook"></a>Tutorial: Guia estratégico de reconhecimento

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

O segundo tutorial desta série de quatro partes sobre alertas de segurança do [!INCLUDE [Product long](includes/product-long.md)] aborda o guia estratégico de reconhecimento. A finalidade do laboratório de alertas de segurança do [!INCLUDE [Product short](includes/product-short.md)] é ilustrar os recursos do **[!INCLUDE [Product short](includes/product-short.md)]** para identificação e detecção de atividades suspeitas e possíveis ataques contra sua rede. O guia estratégico explica como testar algumas das detecções *discretas* do [!INCLUDE [Product short](includes/product-short.md)] e enfoca os recursos baseados em *assinatura* do [!INCLUDE [Product short](includes/product-short.md)]. Este guia estratégico não inclui alertas ou detecções baseados no aprendizado de máquina avançado ou detecções comportamentais baseadas no usuário/entidade, pois isso exige um período de aprendizado de até 30 dias com tráfego de rede real. Para saber mais sobre cada tutorial desta série, confira a [Visão geral do laboratório de alertas de segurança do [!INCLUDE [Product short](includes/product-short.md)]](playbook-lab-overview.md).

Este guia estratégico ilustra os serviços de detecções de ameaça e alertas de segurança do [!INCLUDE [Product short](includes/product-short.md)] que simulam ataques em ferramentas de ataque e invasão comuns e reais disponíveis publicamente.

Neste tutorial, você vai:

> [!div class="checklist"]
>
> - Simular o reconhecimento de mapeamento de rede
> - Simular o reconhecimento do serviço de diretório
> - Simular o reconhecimento de endereço IP e de usuário (SMB)
> - Examinar os alertas de segurança do reconhecimento simulado no [!INCLUDE [Product short](includes/product-short.md)]

## <a name="prerequisites"></a>Pré-requisitos

[Um laboratório de alertas de segurança completo do [!INCLUDE [Product short](includes/product-short.md)]](playbook-setup-lab.md)

- Recomendamos seguir as instruções de configuração do laboratório com a maior fidelidade possível. Quanto mais parecido estiver seu laboratório com a configuração sugerida, mais fácil será para seguir os procedimentos de teste do [!INCLUDE [Product short](includes/product-short.md)].

## <a name="simulate-a-reconnaissance-attack"></a>Simular um ataque de reconhecimento

Depois que um invasor consegue presença em seu ambiente, começa a campanha de reconhecimento. Nesta fase, o invasor normalmente gastará um tempo pesquisando. Ele tenta descobrir computadores de interesse, enumerar usuários e grupos, reunir IPs importantes e mapear os ativos e fraquezas da sua organização. As atividades de reconhecimento permitem que os invasores tenham uma compreensão detalhada e uma mapeamento completo de seu ambiente para uso posterior.

Métodos de teste do ataque de reconhecimento:

- Reconhecimento de mapeamento de rede
- Reconhecimento do serviço de diretório
- Reconhecimento de endereço IP e de usuário (SMB)

## <a name="network-mapping-reconnaissance-dns"></a>Reconhecimento de mapeamento de rede (DNS)

Uma das primeiras coisas que um invasor tentará fazer é obter uma cópia de todas as informações de DNS. Mediante o êxito, o invasor terá acesso a informações abrangentes sobre seu ambiente que podem incluir informações semelhantes sobre seus outros ambientes ou redes.

O [!INCLUDE [Product short](includes/product-short.md)] suprime a atividade de reconhecimento de mapeamento de rede da sua **linha do tempo de atividade suspeita** até que um período de aprendizado de oito dias passe. Durante o período de aprendizado, o [!INCLUDE [Product short](includes/product-short.md)] aprende o que é normal e o que é anormal em sua rede. Após o período de aprendizado de oito dias, os eventos de reconhecimento de mapeamento de rede anormais invocam um alerta de segurança relacionado.

### <a name="run-nslookup-from-victimpc"></a>Executar nslookup no VictimPC

Para testar o reconhecimento de DNS, usaremos a ferramenta de linha de comando nativa, *nslookup* , para iniciar uma transferência de zona de DNS. Os servidores DNS com a configuração correta recusarão consultas desse tipo e não permitirão a tentativa de transferência de zona.

Entre no **VictimPC** usando as credenciais comprometidas de DiogoM. Execute o seguinte comando:

```dos
nslookup
```

Digite **server** , depois o endereço IP ou FQDN do DC (controlador de domínio) no qual o sensor do [!INCLUDE [Product short](includes/product-short.md)] está instalado.

```nslookup
server contosodc.contoso.azure
```

Vamos tentar transferir o domínio.

```nslookup
ls -d contoso.azure
```

- Substitua contosodc.contoso.azure e contoso.azure pelo FQDN do sensor e do nome domínio do [!INCLUDE [Product short](includes/product-short.md)], respectivamente.

 ![tentativa de comando nslookup para copiar o servidor de DNS - falha](media/playbook-recon-nslookup.png)

Se **ContosoDC** for o primeiro sensor implantado, aguarde 15 minutos para permitir que o back-end do banco de dados conclua a implantação dos microsserviços necessários.

### <a name="network-mapping-reconnaissance-dns-detected-in-product-short"></a>Reconhecimento de mapeamento de rede (DNS) detectado no [!INCLUDE [Product short](includes/product-short.md)]

Obter visibilidade desse tipo de tentativa (com êxito ou falha) é essencial para a proteção contra ameaças do domínio. Após a instalação recente do ambiente, você precisará ir para a linha do tempo **Atividades lógicas** para ver a atividade detectada.

Na Pesquisa do [!INCLUDE [Product short](includes/product-short.md)], digite **VictimPC** , depois clique para exibir a linha do tempo.

![Reconhecimento de DNS detectado pelo [!INCLUDE [Product short](includes/product-short.md)], visão de alto nível](media/playbook-recon-nslookupdetection1.png)

Procure a atividade "Consulta AXFR". O [!INCLUDE [Product short](includes/product-short.md)] detecta esse tipo de reconhecimento em seu DNS.

- Se você tiver muitas atividades, clique em **Filtrar por** e desmarque todos os tipos exceto **Consulta DNS**.

![Visualização detalhada da detecção de reconhecimento de DNS no [!INCLUDE [Product short](includes/product-short.md)]](media/playbook-recon-nslookupdetection2.png)

Se o analista de segurança determinar que essa atividade partiu de um scanner de segurança, o dispositivo específico poderá ser excluído de outros alertas de detecção. Na área superior direita do alerta, clique nos três pontos. Em seguida, selecione **Fechar e excluir MySecurityScanner**. Garantindo que esse alerta não apareça novamente quando detectado em "MySecurityScanner".

A detecção de falhas pode ser tão criteriosa quanto a detecção de ataques bem-sucedidos em um ambiente. O portal do [!INCLUDE [Product short](includes/product-short.md)] nos permite ver exatamente o resultado das ações executadas por um possível invasor. Em nossa história de ataque de reconhecimento DNS simulado, nós, atuando como os invasores, foram impedidos de despejar os registros DNS do domínio. Sua equipe de SecOps tomou conhecimento da nossa tentativa de ataque e do computador que usamos em nossa tentativa de alerta de segurança do [!INCLUDE [Product short](includes/product-short.md)].

## <a name="directory-service-reconnaissance"></a>Reconhecimento do serviço de diretório

Atuando como invasor, o próximo objetivo de reconhecimento é uma tentativa de enumerar todos os usuários e grupos na floresta. O [!INCLUDE [Product short](includes/product-short.md)] suprime a atividade de enumeração do Serviço de Diretório da sua linha do tempo de Atividade Suspeita até que um período de aprendizado de 30 dias passe. Durante período de aprendizado, o [!INCLUDE [Product short](includes/product-short.md)] aprende o que é normal e o que é anormal em sua rede. Após o período de aprendizado de 30 dias, os eventos de enumeração de serviço de diretório anormais invocam um alerta de segurança. Durante o período de aprendizado de 30 dias, você pode ver as detecções do [!INCLUDE [Product short](includes/product-short.md)] dessas atividades usando a linha do tempo de atividade de uma entidade em sua rede. As detecções do [!INCLUDE [Product short](includes/product-short.md)] dessas atividades são mostradas neste laboratório.

Para demonstrar um método comum de reconhecimento do serviço de diretório, usaremos o binário nativo da Microsoft, o *net*. Após nossa tentativa, um exame da linha do tempo de Atividade de DiogoM, nosso usuário comprometido, mostrará a detecção dessa atividade pelo [!INCLUDE [Product short](includes/product-short.md)].

### <a name="directory-service-enumeration-via-net-from-victimpc"></a>Enumeração do serviço de diretório por meio de *net* no VictimPC

Qualquer usuário ou computador autenticado pode enumerar outros usuários e grupos em um domínio. Essa capacidade de enumeração é necessária para que a maioria dos aplicativos funcionem corretamente. Nosso usuário comprometido, DiogoM, tem uma conta de domínio sem privilégios. Nesse ataque simulado, veremos exatamente como até mesmo uma conta de domínio sem privilégios ainda pode fornecer pontos de dados valiosos para um invasor.

1. No **VictimPC** , execute o seguinte comando:

    ```dos
    net user /domain
    ```

    A saída mostra todos os usuários no domínio Contoso.Azure.

    ![Enumerar todos os usuários no domínio](media/playbook-recon-dsenumeration-netusers.png)

1. Vamos tentar enumerar todos os grupos no domínio. Execute o seguinte comando:

    ```dos
    net group /domain
    ```

    A saída mostra todos os grupos no domínio Contoso.Azure. Observe um Grupo de Segurança que não é um grupo padrão: **Helpdesk**.

    ![Enumerar todos os grupos no domínio](media/playbook-recon-dsenumeration-netgroups.png)

1. Agora, vamos tentar enumerar somente o grupo Administradores de Domínio. Execute o seguinte comando:

    ```dos
    net group "Domain Admins" /domain
    ```

    ![Enumerar todos os membros do grupo Administradores de Domínio](media/playbook-recon-dsenumeration-netdomainadmins.png)

    Atuando como invasor, aprendemos que há dois membros do grupo Administradores de Domínio: **YasminC** e **ContosoAdmin** (administrador interno para o controlador de domínio). Sabendo que não há limites de segurança entre o nosso Domínio e a Floresta, nosso próximo passo é tentar enumerar os Administradores de Empresa.

1. Para tentar enumerar os Administradores de Empresa, execute o seguinte comando:

    ```dos
    net group "Enterprise Admins" /domain
    ```

    Aprendemos que há somente um Administrador de Empresa, ContosoAdmin. Essas informações não eram importantes, pois já sabíamos que não há um limite de segurança entre o nosso Domínio e a Floresta.

    ![Administradores de Empresa enumerados no domínio](media/playbook-recon-dsenumeration-netenterpriseadmins.png)

Com as informações coletadas em nosso reconhecimento, sabemos sobre o Grupo de Segurança Helpdesk. No entanto, essas informações *ainda* não são interessantes. Também sabemos que **YasminC** é membro do grupo Administradores de Domínio. Se pudermos coletar a credencial de YasminC, poderemos acessar o próprio Controlador de Domínio.

### <a name="directory-service-enumeration-detected-in-product-short"></a>Enumeração do Serviço de Diretório detectada no [!INCLUDE [Product short](includes/product-short.md)]

Se nosso laboratório tivesse *atividade real por 30 dias com o [!INCLUDE [Product short](includes/product-short.md)] instalado* , a atividade que acabamos de realizar como DiogoM provavelmente seria classificada como anormal. As atividades anormais apareceriam na linha do tempo de Atividade Suspeita. No entanto, como acabamos de instalar o ambiente, precisaremos acessar a linha do tempo de Atividades Lógicas.

Na Pesquisa do [!INCLUDE [Product short](includes/product-short.md)], vejamos a aparência da linha do tempo de Atividade Lógica de DiogoM:

![Pesquisar uma entidade específica na linha do tempo de atividade lógica](media/playbook-recon-dsenumeration-searchlogicalactivity.png)

Podemos ver quando DiogoM entrou no VictimPC usando o protocolo Kerberos. Além disso, vemos que DiogoM, no VictimPC, enumerou todos os usuários no domínio.

![Linha do tempo de atividade lógica do DiogoM](media/playbook-recon-dsenumeration-jeffvlogicalactivity.png)

Muitas atividades são registradas na linha do tempo de Atividade Lógica, tornando-a um recurso importante para execução de DFIR (Resposta a incidente e análises forenses digitais). Você pode ver até mesmo as atividades de detecção inicial não realizadas pelo [!INCLUDE [Product short](includes/product-short.md)], mas sim pelo Microsoft Defender para Ponto de Extremidade, pelo Microsoft 365, entre outros.

Olhando a **página do ContosoDC** , também podemos ver os computadores nos quais DiogoM entrou.

![Computadores nos quais DiogoM entrou](media/playbook-recon-dsenumeration-jeffvloggedin.png)

Também podemos obter Dados de Diretório, incluindo Associações e Controles de Acesso de DiogoM, tudo de dentro do [!INCLUDE [Product short](includes/product-short.md)].

![Dados do diretório de DiogoM no [!INCLUDE [Product short](includes/product-short.md)]](media/playbook-recon-dsenumeration-jeffvdirectorydata.png)

Agora, nossa atenção mudará para a Enumeração de Sessão do SMB.

## <a name="user-and-ip-address-reconnaissance-smb"></a>Reconhecimento de endereço IP e de usuário (SMB)

A pasta **sysvol** do Active Directory é uma das mais importantes, senão *a* mais importante, no compartilhamento de rede no ambiente. Cada computador e usuário deve ser capaz de acessar esse compartilhamento de rede específico para efetuar pull das Políticas de Grupo. Um invasor pode obter muitas informações da enumeração de quem tem sessões ativas com a pasta sysvol.

Nossa próxima etapa é a Enumeração da Sessão SMB no recurso ContosoDC. Queremos saber quem mais tem sessões com o compartilhamento SMB, e *de qual IP*.

### <a name="use-joewares-netsessexe-from-victimpc"></a>Usar NetSess.exe da JoeWare no VictimPC

Execute a ferramenta **NetSess** da JoeWare no ContosoDC no contexto de um usuário autenticado, nesse caso, ContosoDC:

```dos
NetSess.exe ContosoDC
```

![Os invasores usam o reconhecimento de SMB para identificar os usuários e seus endereços IP](media/playbook-recon-smbrecon.png)

Já sabemos que YasminC é um Administrador de Domínio. Esse ataque nos proporcionou um endereço IP de YasminC como 10.0.24.6. Como invasor, aprendemos exatamente quem precisamos comprometer. Também conseguimos o local de rede onde essa credencial está conectada.

### <a name="user-and-ip-address-reconnaissance-smb-detected-in-product-short"></a>Reconhecimento de endereço IP e de usuário (SMB) detectado no [!INCLUDE [Product short](includes/product-short.md)]

Agora podemos ver o que o [!INCLUDE [Product short](includes/product-short.md)] detectou para nós:

![Detecção de reconhecimento SMB pelo [!INCLUDE [Product short](includes/product-short.md)]](media/playbook-recon-smbrecon-detection1.png)

Não só somos alertados sobre essa atividade, também somos alertados sobre as contas expostas e seus respectivos endereços IP *nesse ponto no tempo*. Como o SOC (Center de Operações de Segurança), não temos apenas a tentativa e seu status, mas também o que foi enviado de volta ao invasor. Essas informações ajudam em nossa investigação.

## <a name="next-steps"></a>Próximas etapas

Normalmente, a próxima fase na cadeia de encerramento de ataque é uma tentativa de movimentação lateral.

> [!div class="nextstepaction"]
> [Guia estratégico de movimentação lateral do [!INCLUDE [Product short](includes/product-short.md)]](playbook-lateral-movement.md)

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou quer discutir sobre o [!INCLUDE [Product short](includes/product-short.md)] e a segurança relacionada com outras pessoas? Participe da [Comunidade do [!INCLUDE [Product short](includes/product-short.md)]](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) hoje mesmo!
