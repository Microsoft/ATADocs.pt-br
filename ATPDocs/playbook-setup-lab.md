---
title: Tutorial de configuração do laboratório de alertas de segurança do Microsoft Defender para Identidade.
description: Neste tutorial, você aprenderá a configurar um laboratório de teste a fim de simular ameaças para detecção pelo Microsoft Defender para Identidade.
ms.date: 10/26/2020
ms.topic: tutorial
ms.openlocfilehash: 3fa1a3322a76f61f924da521654d3d722c994916
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533589"
---
# <a name="tutorial-setup-a-microsoft-defender-for-identity-security-alert-lab"></a>Tutorial: laboratório "Configurar um alerta de segurança do Microsoft Defender para Identidade"

A finalidade do laboratório de Alertas de segurança do [!INCLUDE [Product long](includes/product-long.md)] é ilustrar os recursos do **[!INCLUDE [Product short](includes/product-short.md)]** na identificação e detecção de atividades suspeitas e possíveis ataques contra sua rede. Este primeiro tutorial, de uma série com quatro partes, explica como criar um ambiente de laboratório para testar detecções *discrete* do [!INCLUDE [Product short](includes/product-short.md)]. O laboratório de alertas de segurança se concentra nos recursos *baseados em assinatura* do [!INCLUDE [Product short](includes/product-short.md)]. O laboratório não inclui aprendizado de máquina avançado, detecções comportamentais baseadas no usuário ou em entidade, pois essas detecções exigem um período de aprendizado de até 30 dias com tráfego de rede real. Para saber mais sobre cada tutorial desta série, confira a [Visão geral do laboratório de alertas de segurança do [!INCLUDE [Product short](includes/product-short.md)]](playbook-lab-overview.md).

Neste tutorial, você irá:

> [!div class="checklist"]
>
> - Configurar seu servidor e os computadores do laboratório
> - Configurar o Active Directory com usuários e grupos
> - Instalar e configurar o [!INCLUDE [Product short](includes/product-short.md)]
> - Configurar políticas locais para seu servidor e computadores
> - Simular um cenário de gerenciamento de assistência técnica usando uma tarefa agendada

## <a name="prerequisites"></a>Pré-requisitos

1. [Um controlador de domínio de laboratório e duas estações de trabalho de laboratório](#servers-and-computers).
    - Vá em frente e [hidrate o Active Directory (AD) com usuários](#bkmk_hydrate).

1. Uma [instância do [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md) [conectada ao AD](install-step2.md).
1. [Baixe](install-step3.md) e [instale a versão mais recente do sensor do [!INCLUDE [Product short](includes/product-short.md)]](install-step4.md) no controlador de domínio do seu laboratório.
1. Familiaridade com [Estações de trabalho com acesso privilegiado](/windows-server/identity/securing-privileged-access/privileged-access-workstations) e [política SAMR](/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).

## <a name="recommendations"></a>Recomendações

Recomendamos seguir as instruções de configuração do laboratório com a maior fidelidade possível. Quanto mais parecido estiver seu laboratório com a configuração sugerida, mais fácil será para seguir os procedimentos de teste do [!INCLUDE [Product short](includes/product-short.md)]. Após terminar a configuração do laboratório, você poderá executar ações com as ferramentas sugeridas de pesquisa de invasão e examinar as detecções dessas ações pelo [!INCLUDE [Product short](includes/product-short.md)].

A configuração de seu laboratório completo deve estar a mais próxima possível do diagrama a seguir:

![Configuração do laboratório de teste do [!INCLUDE [Product short](includes/product-short.md)]](media/playbook-setup-lab.png)

### <a name="servers-and-computers"></a>Servidores e computadores

Esta tabela detalha os computadores e as configurações necessárias. Os endereços IP servem para referência, assim você pode acompanhar com facilidade.

Nos exemplos dos tutoriais, o nome NetBIOS da Floresta é **CONTOSO.AZURE**.

| FQDN | Sistema operacional | IP | Finalidade |
|------|-------|---------|--------------|
| ContosoDC.contoso.azure | Windows Server 2012 R2 | 10.0.24.4 | Controlador de domínio com o sensor do [!INCLUDE [Product short](includes/product-short.md)] instalado localmente |
| VictimPC.contoso.azure | Windows 10 | 10.0.24.5 |PC da vítima |
| AdminPC.contoso.azure | Windows 10  | 10.0.24.6 | PC do administrador de domínio (também conhecido como "Estação de Trabalho Administrativa Segura" ou "Estação de Trabalho Administrativa Privilegiada") |

### <a name="active-directory-users-and-groups"></a>Usuários e grupos do Active Directory

Neste laboratório, há três usuários principais e uma conta de serviço. A conta de serviço é do [!INCLUDE [Product short](includes/product-short.md)] e é usada para sincronização de LDAP e SAMR.

Há um SG (grupo de segurança) de "Helpdesk" do qual Eduardo HelpDesk é membro. Esse SG simula Helpdesk. O SG é emparelhado com um Objeto de Política de Grupo que concede aos membros do Helpdesk os direitos de Administrador Local em seus respectivos computadores. Essa configuração é usada para simular um modelo administrativo realista em um ambiente de produção.

| Completo | Nome completo | SAMAccount | Finalidade |
|--|--|--|
| Diogo Martins | DiogoM | Próxima vítima de um ataque de phishing muito eficaz |
| Eduardo HelpDesk | RonHD | Eduardo é o "cara" da equipe de TI da Contoso. EduardoHD é membro do grupo de segurança de "Helpdesk". |
| Yasmin Correia | YasminC | Na Contoso, esse usuário é nosso Administrador de Domínio. |
| Serviço do[!INCLUDE [Product short](includes/product-short.md)] | AATPService | Conta de serviço do [!INCLUDE [Product short](includes/product-short.md)] | account |

## <a name="defender-for-identity-base-lab-environment"></a>Ambiente de laboratório básico do Defender para Identidade

Para configurar esse laboratório base, adicionaremos usuários e grupos ao Active Directory e editaremos uma política SAM e um grupo confidencial no [!INCLUDE [Product short](includes/product-short.md)].

<a name="bkmk_hydrate"></a>

### <a name="hydrate-active-directory-users-on-contosodc"></a> Hidratar os usuários do Active Directory no ContosoDC

Para simplificar o laboratório, automatizamos o processo para criar usuários e grupos fictícios no Active Directory. Esse script é executado como um pré-requisito para este tutorial. Você pode usar ou modificar o script para hidratar o ambiente do Active Directory do seu laboratório. Se você preferir não usar um script, faça tudo manualmente.

Como Administrador de Domínio, no ContosoDC, execute o seguinte para hidratar nossos usuários do Active Directory:

```powerShell
# Store the user passwords as variables
$SamiraASecurePass = ConvertTo-SecureString -String 'NinjaCat123' -AsPlainText -Force
$ronHdSecurePass = ConvertTo-SecureString -String 'FightingTiger$' -AsPlainText -Force
$jefflSecurePass = ConvertTo-SecureString -String 'Password$fun' -AsPlainText -Force
$AATPService = ConvertTo-SecureString -String 'Password123!@#' -AsPlainText -Force

# Create new AD user SamiraA and add her to the domain admins group
New-ADUser -Name SamiraA -DisplayName "Samira Abbasi" -PasswordNeverExpires $true -AccountPassword $samiraASecurePass -Enabled $true
Add-ADGroupMember -Identity "Domain Admins" -Members SamiraA

# Create new AD user RonHD, create new Helpdesk SG, add RonHD to the Helpdesk SG
New-ADUser -Name RonHD -DisplayName "Ron Helpdesk" -PasswordNeverExpires $true -AccountPassword $ronHdSecurePass -Enabled $true
New-ADGroup -Name Helpdesk -GroupScope Global -GroupCategory Security
Add-ADGroupMember -Identity "Helpdesk" -Members "RonHD"

# Create new AD user JeffL
New-ADUser -Name JeffL -DisplayName "Jeff Leatherman" -PasswordNeverExpires $true -AccountPassword $jefflSecurePass -Enabled $true

# Take note of the "AATPService" user below which will be our service account for Defender for Identity.
# Create new AD user Defender for Identity Service

New-ADUser -Name AatpService -DisplayName "Azure ATP/ATA Service" -PasswordNeverExpires $true -AccountPassword $AATPService -Enabled $true
```

### <a name="configure-sam-r-capabilities-from-contosodc"></a>Configurar recursos de SAM-R no ContosoDC

Para permitir que o Serviço do [!INCLUDE [Product short](includes/product-short.md)] execute corretamente a enumeração SAM-R e crie caminhos de Movimentação Lateral, você precisará editar a política SAM.

1. Encontre sua política de SAM em: **Políticas\> Configurações do Windows \> Configurações de Segurança \> Políticas Locais \> Opções de segurança\> "Acesso à rede: restringir clientes com permissão para efetuar chamadas remotas para SAM"** _

    ![Modificação da Política de Grupo para permitir que [!INCLUDE [Product short](includes/product-short.md)] use os recursos do caminho de Movimentação Lateral.](media/playbook-labsetup-localgrouppolicies3.png)

1. Adicione a conta do serviço do [!INCLUDE [Product short](includes/product-short.md)], AATPService, à lista de contas aprovadas capazes de executar essa ação em seus sistemas modernos do Windows.

    ![Adicione o serviço](media/samr-add-service.png)

### <a name="add-sensitive-group-to-defender-for-identity"></a>Adicionar um grupo confidencial ao Defender para Identidade

A adição do grupo de segurança "Helpdesk" como um **Grupo confidencial** permitirá que você use o recurso de Gráfico de Movimentação Lateral do [!INCLUDE [Product short](includes/product-short.md)]. Marcar usuários e grupos altamente confidenciais que não são necessariamente Administradores de Domínio, mas têm privilégios em inúmeros recursos, é uma prática recomendada.

1. No portal do [!INCLUDE [Product short](includes/product-short.md)], selecione **Configuração**.

1. Em **Detecção** selecione **Marcas de entidade**.

    ![Marcas de entidade do [!INCLUDE [Product short](includes/product-short.md)]](media/entity-tags.png)
1. Na seção **Confidencial**, digite o nome "Helpdesk" para **Grupos confidenciais** e clique no sinal **+** para adicioná-los.
    ![Marca do "Helpdesk" como um grupo confidencial do [!INCLUDE [Product short](includes/product-short.md)] para habilitar Gráficos de Movimentação Lateral e relatórios para esse grupo privilegiado](media/playbook-labsetup-helpdesksensitivegroup.png)
1. Clique em **Salvar**.

### <a name="defender-for-identity-lab-base-setup-checklist"></a>Lista de verificação de configuração básica do laboratório do Defender para Identidade

Neste ponto, você deve ter um laboratório base do [!INCLUDE [Product short](includes/product-short.md)]. O [!INCLUDE [Product short](includes/product-short.md)] deve estar pronto para ser usado, e os usuários testados. Examine a lista de verificação para ter certeza de que o laboratório base foi concluído.

| Etapa  | Etapa | Ação | Status |
|--|--|--|
| 1 | Sensor do [!INCLUDE [Product short](includes/product-short.md)] instalado no ContosoDC (etapa de pré-requisito) | - [ ] |
| 2 | Os usuários e grupos são criados no Active Directory | - [ ] |
| 3 | Privilégios da conta de serviço do [!INCLUDE [Product short](includes/product-short.md)] configurados corretamente para SAMR | - [ ] |
| 4 | Grupo de segurança Helpdesk adicionado como **Grupo confidencial** no [!INCLUDE [Product short](includes/product-short.md)] | - [ ] |](includes/product-other.md)]| - [ ] |

## <a name="set-up-the-lab-workstations"></a>Configurar as estações de trabalho de laboratório

Após configurar seu laboratório base do [!INCLUDE [Product short](includes/product-short.md)], comece a configuração da estação de trabalho a fim de se preparar para os três próximos tutoriais desta série. Vamos hidratar nosso VictimPC e AdminPC para fazer com que este laboratório pareça ativo.

### <a name="victimpc-local-policies"></a>Políticas locais de VictimPC

A próxima etapa do laboratório é concluir a configuração de política local. **VictimPC** tem DiogoM e o grupo de segurança Helpdesk como membros do grupo Administradores locais. Como acontece em muitas organizações, DiogoM é Administrador de seu próprio dispositivo, **VictimPC**.

Como administrador local, ele configura políticas locais executando o script automatizado do PowerShell:

```powerShell
# Add JeffL to local Administrators group on VictimPC
Add-LocalGroupMember -Group "Administrators" -Member "Contoso\JeffL"
# Add Helpdesk to local Administrators group on VictimPC
Add-LocalGroupMember -Group "Administrators" -Member "Contoso\Helpdesk"
```

Inspecione o grupo de Administradores no **VictimPC** e verifique se ele tem pelo menos Helpdesk e DiogoM como membros:

![Helpdesk e JeffV devem estar no grupo Administrador Local de VictimPC](media/playbook-labsetup-localgrouppolicies2.png)

<a name="helpdesk-simulation"></a>

### <a name="simulate-helpdesk-support-on-victimpc"></a> Simular o suporte de assistência técnica no VictimPC

Para simular uma rede funcional e gerenciada, crie uma Tarefa Agendada no computador **VictimPC** para executar o processo de "cmd.exe" como **EduardoHD**.

1. Em um **console elevado do PowerShell** no VictimPC, execute o seguinte comando:

    ```powerShell
    $action = New-ScheduledTaskAction -Execute 'cmd.exe'
    $trigger = New-ScheduledTaskTrigger -AtLogOn
    $runAs = 'Contoso\RonHD'
    $ronHHDPass = 'FightingTiger$'
    Register-ScheduledTask -TaskName "RonHD Cmd.exe - AATP SA Playbook" -Trigger $trigger -User $runAs -Password $ronHHDPass -Action $action
    ```

1. Entre no computador como **DiogoM**. O processo de Cmd.exe iniciará no contexto do EduardoHD depois do logon, simulando o gerenciamento do computador por Helpdesk.

### <a name="turn-off-antivirus-on-victimpc"></a>Desativar o antivírus em VictimPC

Para realizar o teste, desative qualquer solução antivírus em execução no ambiente do laboratório. Isso garantirá que possamos nos concentrar no [!INCLUDE [Product short](includes/product-short.md)] durante estes exercícios e não em técnicas de evasão antivírus.

Sem desativar primeiro as soluções antivírus, você não conseguirá baixar algumas das ferramentas na próxima seção. Além disso, se o antivírus for habilitado após o preparo das ferramentas de ataque, será necessário baixar novamente as ferramentas depois de desabilitar o antivírus.

### <a name="stage-common-hacker-tools"></a>Preparar ferramentas de invasão comuns

> [!WARNING]
> As ferramentas a seguir são apresentadas apenas para fins de pesquisa. A Microsoft **não** é proprietária dessas ferramentas, e a Microsoft não oferece, nem pode oferecer, garantia do comportamento delas. Essas ferramentas **só** devem ser executadas em um ambiente de laboratório de teste.

Para executar os guias estratégicos de Alertas de segurança do [!INCLUDE [Product short](includes/product-short.md)], você precisará das seguintes ferramentas.

| Ferramenta | URL |
|----|-----|
| Mimikatz | [GitHub - Mimikatz](https://github.com/gentilkiwi/mimikatz) |
| PowerSploit | [GitHub - PowerSploit](https://github.com/PowerShellMafia/PowerSploit) |
| PsExec | [Microsoft Docs](/sysinternals/downloads/psexec) |
| NetSess | [JoeWare Tools](https://www.joeware.net/freetools) |

Agradecemos aos criadores dessas ferramentas de pesquisa por ajudar a comunidade a entender melhor os riscos e impactos cibernéticos.

### <a name="adminpc-local-policies"></a>Políticas locais de AdminPC

**AdminPC** precisa adicionar **Helpdesk** ao grupo Administradores locais. Depois, remover "Administradores de Domínio" do grupo Administradores locais. Essa etapa garante que Yasmin, Administradora de Domínio, não seja uma Administradora de AdminPC. Essa é uma melhor prática em proteção de credencial. Execute essa etapa manualmente ou use o script do PowerShell fornecido.

1. Adicione **Helpdesk** ao **AdminPC** e *remova* "Administradores de Domínio" do Grupo Administrador Local executando o seguinte script do PowerShell:

    ```powerShell
    # Add Helpdesk to local Administrators group
    Add-LocalGroupMember -Group "Administrators" -Member "Contoso\Helpdesk"
    # Remove Domain Admins from local Administrators group
    Remove-LocalGroupMember -Group "Administrators" -Member "Domain Admins"
    ```

1. Depois de executar o script, **Helpdesk** fica na lista **Administradores** > **Membros** locais de **AdminPC**.
![Helpdesk no Grupo de Administradores Locais para AdminPC](media/playbook-labsetup-localgrouppolicies1.png)

### <a name="simulate-domain-activities-from-adminpc"></a>Simular atividades de domínio do AdminPC

YasminC precisa de atividades de domínio simuladas. Essa etapa pode ser feita manualmente ou com o script do PowerShell fornecido. O script do PowerShell acessa o controlador de domínio a cada cinco minutos e resultará na atividade de rede simulada como Yasmin.

Como **YasminC**, execute o seguinte script em um prompt do PowerShell no AdminPC:

```powerShell
while ($true)
{
    Invoke-Expression "dir \\ContosoDC\c$"
    Start-Sleep -Seconds 300
}
```

### <a name="workstation-setup-checklist"></a>Lista de verificação de instalação da estação de trabalho

Examine a lista de verificação para ter certeza de que a configuração da estação de trabalho foi concluída.

| Etapa | Agir| Etapa | Ação | Status |
|--|--|--|
| 1 | Adicionar DiogoM e Helpdesk como administradores locais em VictimPC | - [ ] |
| 2 | Criar Tarefa Agendada em execução como EduardoHD no VictimPC | - [ ] |
| 3 | Desativar a solução antivírus em VictimPC | - [ ] |
| 4 | Preparar ferramentas de invasão em VictimPC | - [ ] |
| 5 | Adicionar Helpdesk e remover Administradores de Domínio do grupo de administradores locais do AdminPC | - [ ] |
| 6 | Executar o script do PowerShell como Yasmin para simular atividades de domínio | - [ ] |PowerShell como Yasmin para simular atividades de domínio | - [ ] |

## <a name="mission-accomplished"></a>Missão cumprida!

Seu laboratório do [!INCLUDE [Product short](includes/product-short.md)] agora está pronto para uso. Os métodos usados nessa configuração foram escolhidos sabendo que os recursos devem ser gerenciados (por *algo* ou *alguém*) e que o gerenciamento exige privilégios de administrador local. Há outras maneiras de simular um fluxo de trabalho de gerenciamento no laboratório, como:

- Entrar e sair do VictimPC com a conta do EduardoHD
- Adicionar outra versão de uma Tarefa Agendada
- Uma sessão RDP
- Executar um "runas" na linha de comando

Para obter melhores resultados, escolha um método de simulação que você possa automatizar em seu laboratório para fins de consistência.

## <a name="next-steps"></a>Próximas etapas

Teste seu ambiente de laboratório do [!INCLUDE [Product short](includes/product-short.md)] usando os guias estratégicos de Alertas de segurança do [!INCLUDE [Product short](includes/product-short.md)] para cada fase da cadeia de eliminação de ataque cibernético, começando com a fase de reconhecimento.

> [!div class="nextstepaction"]
> [Guia estratégico de reconhecimento do [!INCLUDE [Product short](includes/product-short.md)]](playbook-reconnaissance.md)

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou quer discutir sobre o [!INCLUDE [Product short](includes/product-short.md)] e a segurança relacionada com outras pessoas? Participe da Comunidade [[!INCLUDE [Product short](includes/product-short.md)]](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) hoje mesmo!
