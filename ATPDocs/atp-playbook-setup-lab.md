---
title: Tutorial de configuração do laboratório de alerta de segurança do ATP do Azure
description: Neste tutorial, você configura um laboratório de teste do ATP do Azure para simular ameaças que serão detectadas pelo ATP do Azure.
ms.service: azure-advanced-threat-protection
ms.topic: how-to
author: shsagir
ms.author: shsagir
ms.date: 02/28/2019
ms.reviewer: itargoet
ms.openlocfilehash: c6b1a309d86562082121806e1c81897e9632e95c
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88955098"
---
# <a name="tutorial-setup-an-atp-security-alert-lab"></a>Tutorial: Configurar um laboratório de alerta de segurança do ATP 

 A finalidade do laboratório de Alerta de Segurança do ATP do Azure é ilustrar os recursos do **ATP do Azure** para identificação e detecção de atividades suspeitas e possíveis ataques contra a sua rede. Este primeiro tutorial, de uma série com quatro partes, explica como criar um ambiente de laboratório para testar detecções *discretas* do ATP do Azure. O laboratório de alerta de segurança se concentra nos recursos *baseados em assinatura* do ATP do Azure. O laboratório não inclui aprendizado de máquina avançado, detecções comportamentais baseadas no usuário ou em entidade, pois essas detecções exigem um período de aprendizado de até 30 dias com tráfego de rede real. Para saber mais sobre cada tutorial desta série, consulte a [Visão geral do laboratório de alerta de segurança do ATP](atp-playbook-lab-overview.md). 


Neste tutorial, você vai: 

> [!div class="checklist"]
> * Configurar seu servidor e os computadores do laboratório
> * Configurar o Active Directory com usuários e grupos
> * Instalar e configurar o ATP do Azure
> * Configurar políticas locais para seu servidor e computadores
> * Simular um cenário de gerenciamento de assistência técnica usando uma tarefa agendada

## <a name="prerequisites"></a>Pré-requisitos

1. [Um controlador de domínio de laboratório e duas estações de trabalho de laboratório](#servers-and-computers).
   - Vá em frente e [hidrate o Active Directory (AD) com usuários](#bkmk_hydrate).
1. Uma [instância do ATP do Azure](install-atp-step1.md)[conectada ao AD](install-atp-step2.md).
1. [Baixe](install-atp-step3.md) e [instale a versão mais recente do sensor do ATP do Azure](install-atp-step4.md) no controlador de domínio do seu laboratório.
1. Familiaridade com [Estações de trabalho com acesso privilegiado](/windows-server/identity/securing-privileged-access/privileged-access-workstations) e [política SAMR](/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).

## <a name="recommendations"></a>Recomendações

Recomendamos seguir as instruções de configuração do laboratório com a maior fidelidade possível. Quanto mais parecido estiver o seu laboratório com a configuração de laboratório sugerida, mais fácil será para seguir os procedimentos de teste do ATP do Azure. Após terminar a configuração do laboratório, você poderá executar ações com as ferramentas sugeridas de pesquisa de invasão e examinar as detecções do ATP do Azure dessas ações.

A configuração de seu laboratório completo deve estar a mais próxima possível do diagrama a seguir:

![Configuração do laboratório de teste do ATP do Azure](media/playbook-atp-setup-lab.png)

### <a name="servers-and-computers"></a>Servidores e computadores

Esta tabela detalha os computadores e as configurações necessárias. Os endereços IP servem para referência, assim você pode acompanhar com facilidade.

Nos exemplos dos tutoriais, o nome NetBIOS da Floresta é **CONTOSO.AZURE**.

|  FQDN | SO | IP | Finalidade |
|------|-------|---------|--------------|
| ContosoDC.contoso.azure | Windows Server 2012 R2 | 10.0.24.4 | Controlador de domínio com sensor do ATP do Azure instalado localmente |
| VictimPC.contoso.azure | Windows 10 | 10.0.24.5 |PC da vítima |
| AdminPC.contoso.azure | Windows 10  | 10.0.24.6 | PC do administrador de domínio (também conhecido como "Estação de Trabalho Administrativa Segura" ou "Estação de Trabalho Administrativa Privilegiada") |

### <a name="active-directory-users-and-groups"></a>Usuários e grupos do Active Directory

Neste laboratório, há três usuários principais e uma conta de serviço. A conta de serviço é para o ATP do Azure e é usada para sincronização de LDAP e SAMR.

Há um SG (Grupo de Segurança) "Helpdesk" do qual o Eduardo HelpDesk é membro. Esse SG simula Helpdesk. O SG é emparelhado com um Objeto de Política de Grupo que concede aos membros do Helpdesk os direitos de Administrador Local em seus respectivos computadores. Essa configuração é usada para simular um modelo administrativo realista em um ambiente de produção.

| Nome Completo    | SAMAccount |Finalidade|
|--------------|------------|--------------------------------------------------------------------------------------------------|
| Diogo Martins  | DiogoM  | Próxima vítima de um ataque de phishing muito eficaz  |
| Eduardo HelpDesk  | RonHD  |Eduardo é o cara da equipe de TI da Contoso. EduardoHD é membro do grupo de segurança "Helpdesk". |
| Yasmin Correia | YasminC  | Na Contoso, esse usuário é nosso Administrador de Domínio. |
| Serviço do ATP do Azure | AATPService | Conta de serviço do ATP do Azure |

## <a name="azure-atp-base-lab-environment"></a>Ambiente de laboratório base do ATP do Azure

Para configurar esse laboratório base adicionaremos usuários e grupos ao Active Directory, editaremos uma política de SAM e um grupo confidencial no ATP do Azure.

### <a name="hydrate-active-directory-users-on-contosodc"></a><a name="bkmk_hydrate"></a> Hidratar os usuários do Active Directory no ContosoDC

Para simplificar o laboratório, automatizamos o processo para criar usuários e grupos fictícios no Active Directory. Esse script é executado como um pré-requisito para este tutorial. Você pode usar ou modificar o script para hidratar o ambiente do Active Directory do seu laboratório. Se você preferir não usar um script, faça tudo manualmente.

Como Administrador de Domínio, no ContosoDC, execute o seguinte para hidratar nossos usuários do Active Directory:

``` PowerShell

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

# Take note of the "AATPService" user below which will be our service account for Azure ATP.
# Create new AD user Azure ATP Service

New-ADUser -Name AatpService -DisplayName "Azure ATP/ATA Service" -PasswordNeverExpires $true -AccountPassword $AATPService -Enabled $true

```

### <a name="configure-sam-r-capabilities-from-contosodc"></a>Configurar recursos de SAM-R no ContosoDC

Para permitir que o serviço do ATP do Azure execute corretamente a enumeração de SAM-R e crie caminhos de Movimentação Lateral, você precisará editar a política de SAM.

1. Encontre sua política de SAM em: **Políticas\> Configurações do Windows \> Configurações de Segurança \> Políticas Locais \> Opções de segurança\> "Acesso à rede: restringir clientes com permissão para efetuar chamadas remotas para SAM"** _

    ![Modifique a Política de Grupo para permitir que o ATP do Azure use os recursos do caminho de Movimentação Lateral.](media/playbook-labsetup-localgrouppolicies3.png)

1. Adicione a conta do serviço ATP do Azure, AATPService, à lista de contas aprovadas capazes de executar essa ação em seus sistemas modernos do Windows.

    ![Adicione o serviço](media/samr-add-service.png)

### <a name="add-sensitive-group-to-azure-atp"></a>Adicionar grupo confidencial ao ATP do Azure

A adição do Grupo de Segurança "Helpdesk" como um **Grupo confidencial** permitirá que você use o recurso de Gráfico de Movimentação Lateral do ATP do Azure. Marcar usuários e grupos altamente confidenciais que não são necessariamente Administradores de Domínio, mas têm privilégios em inúmeros recursos, é uma prática recomendada.

1. No portal do Azure ATP, clique na engrenagem de **Configuração** na barra de menus.

1. Em **Detecção**, clique em **Marcas de entidade**.

    ![Marcas de entidade do Azure ATP](media/entity-tags.png)

1. Na seção **Confidencial**, digite o nome "Helpdesk" para **Grupos confidenciais** e clique no sinal **+** para adicioná-los.

    ![Marque "Helpdesk" como um grupo confidencial do ATP do Azure para habilitar os Gráficos de Movimentação Lateral e os relatórios para esse grupo privilegiado](media/playbook-labsetup-helpdesksensitivegroup.png)

1. Clique em **Salvar**.

### <a name="azure-atp-lab-base-setup-checklist"></a>Lista de verificação de configuração base do Laboratório de ATP do Azure

Neste ponto, você deve ter um laboratório base de ATP do Azure. O ATP do Azure deve estar pronto para ser usado, e os usuários foram testados. Examine a lista de verificação para ter certeza de que o laboratório base foi concluído.  

| Etapa    | Ação | Status |
|--------------|------------|------------------|
| 1  | Sensor do ATP do Azure instalado no ContosoDC (etapa pré-requisito)| - [ ] |
| 2  | Os usuários e grupos são criados no Active Directory  | - [ ] |
| 3  | Privilégios da conta de serviço do ATP do Azure configurados corretamente para SAMR | - [ ] |
| 4  | Grupo de segurança Helpdesk adicionado como **Grupo confidencial** no ATP do Azure| - [ ] |

## <a name="set-up-the-lab-workstations"></a>Configurar as estações de trabalho de laboratório

Após configurar seu laboratório base do ATP do Azure, comece a configuração da estação de trabalho para se preparar para os três próximos tutoriais desta série. Vamos hidratar nosso VictimPC e AdminPC para fazer com que este laboratório pareça ativo.

### <a name="victimpc-local-policies"></a>Políticas locais de VictimPC

A próxima etapa do laboratório é concluir a configuração de política local. **VictimPC** tem DiogoM e o grupo de segurança Helpdesk como membros do grupo Administradores locais. Como acontece em muitas organizações, DiogoM é Administrador de seu próprio dispositivo, **VictimPC**.

Como administrador local, ele configura políticas locais executando o script automatizado do PowerShell:

``` PowerShell
# Add JeffL to local Administrators group on VictimPC
Add-LocalGroupMember -Group "Administrators" -Member "Contoso\JeffL"
# Add Helpdesk to local Administrators group on VictimPC
Add-LocalGroupMember -Group "Administrators" -Member "Contoso\Helpdesk"
```

Inspecione o grupo de Administradores no **VictimPC** e verifique se ele tem pelo menos Helpdesk e DiogoM como membros:

![Helpdesk e JeffV devem estar no grupo Administrador Local de VictimPC](media/playbook-labsetup-localgrouppolicies2.png)

### <a name="simulate-helpdesk-support-on-victimpc"></a><a name="helpdesk-simulation"></a> Simular o suporte de assistência técnica no VictimPC

Para simular uma rede funcional e gerenciada, crie uma Tarefa Agendada no computador **VictimPC** para executar o processo de "cmd.exe" como **EduardoHD**.

1. Em um **console elevado do PowerShell** no VictimPC, execute o seguinte comando:

    ``` PowerShell
    $action = New-ScheduledTaskAction -Execute 'cmd.exe'
    $trigger = New-ScheduledTaskTrigger -AtLogOn
    $runAs = 'Contoso\RonHD'
    $ronHHDPass = 'FightingTiger$'
    Register-ScheduledTask -TaskName "RonHD Cmd.exe - AATP SA Playbook" -Trigger $trigger -User $runAs -Password $ronHHDPass -Action $action
    ```

1. Entre no computador como **DiogoM**. O processo de Cmd.exe iniciará no contexto do EduardoHD depois do logon, simulando o gerenciamento do computador por Helpdesk.

### <a name="turn-off-antivirus-on-victimpc"></a>Desativar o antivírus em VictimPC

Para realizar o teste, desative qualquer solução antivírus em execução no ambiente do laboratório. Isso garante que possamos nos concentrar no ATP do Azure durante esses exercícios e não em técnicas de evasão antivírus.

Sem desativar primeiro as soluções antivírus, você não conseguirá baixar algumas das ferramentas na próxima seção. Além disso, se o antivírus for habilitado após o preparo das ferramentas de ataque, será necessário baixar novamente as ferramentas depois de desabilitar o antivírus.

### <a name="stage-common-hacker-tools"></a>Preparar ferramentas de invasão comuns

> [!WARNING]
> As ferramentas a seguir são apresentadas apenas para fins de pesquisa. A Microsoft **não** é proprietária dessas ferramentas, e a Microsoft não oferece, nem pode oferecer, garantia do comportamento delas. Essas ferramentas **só** devem ser executadas em um ambiente de laboratório de teste.

Para executar os guias estratégicos de Alerta de Segurança do ATP do Azure, você precisará destas ferramentas.

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

    ``` PowerShell
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

```PowerShell

while ($true)
{
    Invoke-Expression "dir \\ContosoDC\c$"
    Start-Sleep -Seconds 300
}

```

### <a name="workstation-setup-checklist"></a>Lista de verificação de instalação da estação de trabalho

Examine a lista de verificação para ter certeza de que a configuração da estação de trabalho foi concluída.

| Etapa    | Ação | Status |
|--------------|------------|------------------|
| 1  | Adicionar DiogoM e Helpdesk como administradores locais em VictimPC | - [ ] |
| 2  | Criar Tarefa Agendada em execução como EduardoHD no VictimPC | - [ ] |
| 3  | Desativar a solução antivírus em VictimPC | - [ ] |
| 4  | Preparar ferramentas de invasão em VictimPC| - [ ] |
| 5  | Adicionar Helpdesk e remover Administradores de Domínio do grupo de administradores locais do AdminPC| - [ ] |
| 6  | Executar o script do PowerShell como Yasmin para simular atividades de domínio | - [ ] |

## <a name="mission-accomplished"></a>Missão cumprida!

Seu laboratório do ATP do Azure está pronto para ser usado. Os métodos usados nessa configuração foram escolhidos sabendo que os recursos devem ser gerenciados (por *algo* ou *alguém*) e que o gerenciamento exige privilégios de administrador local. Há outras maneiras de simular um fluxo de trabalho de gerenciamento no laboratório, como:

- Entrar e sair do VictimPC com a conta do EduardoHD
- Adicionar outra versão de uma Tarefa Agendada
- Uma sessão RDP
- Executar um "runas" na Linha de Comando

 Para obter melhores resultados, escolha um método de simulação que você possa automatizar em seu laboratório para fins de consistência.


## <a name="next-steps"></a>Próximas etapas

Teste o seu ambiente de laboratório do ATP do Azure usando os guias estratégicos de Alerta de Segurança do ATP do Azure para cada fase da cadeia de encerramento do ataque cibernético, começando com a fase de reconhecimento.  

> [!div class="nextstepaction"]
> [Guia estratégico de Reconhecimento do ATP do Azure](atp-playbook-reconnaissance.md)


## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o ATP do Azure e a segurança relacionada com outras pessoas? Participe da [Comunidade do ATP do Azure](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) hoje mesmo!