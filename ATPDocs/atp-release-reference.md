---
title: Referência de versões mais antigas no ATP do Azure (Proteção Avançada contra Ameaças do Azure) | Microsoft Docs
description: Este artigo é uma referência de atualizações de versões anteriores do ATP do Azure (Proteção Avançada contra Ameaças do Azure).
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/17/2019
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: 12e05c54b4237aa04d285d342c960e536a248cdc
ms.sourcegitcommit: 814af2addf833d40d10f7594275a132f888eea9b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2019
ms.locfileid: "74153136"
---
# <a name="release-reference-of-azure-advanced-threat-protection-azure-atp"></a>Referência de versão do ATP do Azure (Proteção Avançada contra Ameaças do Azure) 

Este artigo é uma referência de todas as versões do ATP do Azure até (e incluindo) a versão 2.55. Para atualizações recentes de versões do ATP do Azure (2.56 e mais recente), confira [Novidades do ATP do Azure](atp-whats-new.md).


## <a name="azure-atp-release-255"></a>ATP do Azure versão 2.55
Lançado em 18 de novembro de 2018

- **Alerta de segurança: comunicação suspeita sobre DNS - disponibilidade geral**<br>
O alerta de segurança de [comunicação suspeita sobre DNS](suspicious-activity-guide.md) da Proteção Avançada contra Ameaças do Azure já está em disponibilidade geral. <br> Normalmente, o protocolo DNS não é monitorado na maioria das organizações e raramente é bloqueado para atividades mal-intencionadas. Isso permite que um invasor em um computador comprometido abuse do protocolo DNS. A comunicação mal-intencionada por DNS pode ser usada para extração, comando e controle de dados e/ou fuga de restrições de rede corporativa.

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-254"></a>ATP do Azure versão 2.54
Lançado em 11 de novembro de 2018

- **Aprimoramento do recurso: exclusões de domínio padrão adicionadas ao alerta de Comunicação suspeita por DNS**<br>   Nova adição de três domínios populares à lista de exclusões de domínio padrão. A lista de exclusões permanece totalmente personalizável. Para saber mais, veja [Excluindo entidades de detecções](excluding-entities-from-detections.md). 

- **Aprimoramentos de documentação: atualização de log do SIEM, diretrizes de problemas conhecidos**<br>    Mapeamento de externalId e explicações adicionais foram adicionados a descrições de log do SIEM. Para saber mais, veja [referência de log do SIEM](cef-format-sa.md). <br>Um artigo adicional para obter diretrizes de problemas conhecidos atualmente não resolvidos foi adicionado. Para saber mais, veja [Problemas conhecidos do ATP do Azure](known-issues.md).  

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-253"></a>ATP do Azure versão 2.53
Lançado em 4 de novembro de 2018

- **Aprimoramento do alerta de segurança: falhas de autenticação suspeitas**<br>
O [alerta de segurança de falha de autenticação suspeita](suspicious-activity-guide.md) da Proteção Avançada contra Ameaças do Azure agora inclui o monitoramento para detecção de ataques de força bruta de pulverização de senhas.
Em um ataque típico de **pulverização de senhas**, depois de enumerar com êxito uma lista de usuários válidos do controlador de domínio, os invasores tentam UMA senha cuidadosamente concebida em TODAS as contas de usuário conhecidas (uma senha para várias contas). Quando a pulverização de senhas inicial não tem êxito, eles tentam novamente utilizando uma senha diferente cuidadosamente concebida, normalmente após aguardar 30 minutos entre as tentativas. Esse tempo de espera permite que os invasores evitem disparar a maioria dos limites de bloqueio de conta que se baseiam no tempo. A pulverização de senhas tornou-se rapidamente uma técnica de preferência entre os invasores e testadores de intrusão. Os ataques de pulverização de senhas se mostraram eficazes na conquista de uma entrada na organização e por fazer movimentos laterais posteriores, tentando aumentar os privilégios. 

- **Aprimoramento do recurso: enviar uma mensagem de teste do Syslog**<br>   Nova funcionalidade de envio de mensagem de Syslog de teste durante o processo de configuração do SIEM. Saiba mais em [Integração com o Syslog](setting-syslog.md). 

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-252"></a>ATP do Azure versão 2.52
Lançado em 28 de outubro de 2018


- **Aprimoramento do alerta de segurança: tentativa de execução remota de código**<br>
O [alerta de segurança de tentativa de execução remota de código](suspicious-activity-guide.md) do ATP do Azure agora inclui monitoramento para tentativas suspeitas de execução remota de código do PowerShell em seus controladores de domínio. O PowerShell Remoto é um método comum para a execução de comandos administrativos válidos, mas é com frequência usado maliciosamente em uma tentativa de executar scripts em pontos de extremidade remotos. 

- **Aprimoramento do recurso: definir o agendamento de relatórios**
<br>Agora você pode definir uma hora específica para agendar seus relatórios do ATP do Azure usando a função [relatórios](reports.md#). 

- **Adição de configuração: RBAC (Controle de Acesso Baseado em Função)**
<br>Configure as funções de segurança do seu locatário no Centro de administração do AAD (Azure Active Directory) diretamente do novo link de administrador no Portal do ATP do Azure. 

- **Estrutura e conteúdo de documentação revisados**
<br>As recentes alterações de conteúdo para a documentação do ATP do Azure incluem novos artigos, fornecendo uma lista completa de todas as atividades monitoradas do ATP do Azure, instruções de filtragem de atividade, bem como uma reformulação da estrutura de site de documentação para melhor capacidade de utilização:
  - [Atividades monitoradas do ATP do Azure](monitored-activities.md) 
  - [Filtragem de atividades do ATP do Azure](atp-activities-search.md) 
  - [Documentação do ATP do Azure](https://docs.microsoft.com/azure-advanced-threat-protection/)  

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-251"></a>ATP do Azure versão 2.51
Lançado em 21 de outubro de 2018

- Você pode agora habilitar/desabilitar a **integração WD-ATP** na tela [Configuração](integrate-wd-atp.md#how-to-integrate-azure-atp-with-windows-defender-atp) do portal do ATP do Azure. (Para acessar essa funcionalidade, o usuário do ATP do Azure deve ser um Administrador de segurança ou Global no locatário do AAD).

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-250"></a>Azure ATP versão 2.50
Lançado em 14 de outubro de 2018
- Essa versão inclui correções e melhorias para vários problemas.


## <a name="azure-atp-release-249"></a>Azure ATP versão 2.49
Lançado em 7 de outubro de 2018
-   **Novas detecções: comunicação suspeita de DNS** (versão prévia)<br>Nova detecção adicionada para ajudar a proteger contra ataques de comunicação suspeita de DNS:

    -   Essa detecção ajuda a detectar ataques contra o protocolo DNS. Na maioria das organizações, o protocolo DNS não é monitorado e raramente é bloqueado para atividade mal-intencionada. Permitir que um invasor em um computador comprometido abuse do protocolo DNS. A comunicação mal-intencionada por DNS pode ser usada para extração, comando e controle de dados e/ou fuga de restrições de rede corporativa.

- **Nova funcionalidade** <br>**Função de usuário** do Azure ATP aprimorada com as seguintes funcionalidades:
  - Alterar o status de alertas de segurança (abrir novamente, fechar, excluir, suprimir)
  - Definir relatórios agendados
  - Definir marcas de entidade (confidenciais e honeytoken)
  - Exclusão de detecção
  - Alterar idioma
  - Definir notificações por email ou syslog


- Um aumento temporário no **Reconhecimento usando os alertas de segurança das consultas de serviços de diretório** que ocorreu em 16 de setembro de 2018 foi identificado e resolvido. 

- Essa versão também inclui correções e melhorias para vários problemas.


## <a name="azure-atp-release-248"></a>Azure ATP versão 2.48
Lançado em 16 de setembro de 2018
- **Alerta de segurança:** Reconhecimento usando consultas de serviços de diretório

  Esse alerta de segurança melhorou os infográficos e as evidências. 

- **Excluir entidades de detecções** 

  Para reduzir os falsos positivos, você pode optar por excluir entidades das seguintes detecções: 
  - Conexão VPN suspeita (exclusão de usuário)
  - Promoção do controlador de domínio suspeito (possível ataque DCShadow)
  - Solicitação de replicação suspeita (possível ataque DCShadow)

- Essa versão também inclui correções e melhorias para vários problemas.


## <a name="azure-atp-release-247"></a>ATP do Azure versão 2.47
Lançado em 2 de setembro de 2018

- **Verificação de política de auditoria avançada da ATP do Azure**
 
A Proteção Avançada contra Ameaças agora verifica as políticas de auditoria avançadas existentes de seu controlador de domínio e recomenda alterações de política para fornecer a máxima cobertura do serviço de ATP do Azure para sua organização. 

**Essa nova verificação permite que você:**
  -  Identifique eventos ausentes de seus Logs de Eventos do Windows que atualmente são excluídos da sua cobertura da ATP do Azure.
  -  Verifique se as configurações são as ideais e faça alterações de acordo com as recomendações de alerta de integridade fornecidas.
  -  Será emitido um único alerta de integridade agregado para todos os controladores de domínio, incluindo sugestões de correção (se/conforme necessário).

Revise como [Configurar políticas de auditoria avançadas](atp-advanced-audit-policy.md) para garantir que seu sistema esteja configurado corretamente. 
- Essa versão também inclui correções e melhorias para vários problemas.

## <a name="azure-atp-release-246"></a>Azure ATP versão 2.46

Lançado em 26 de agosto de 2018

- Essa versão inclui correções e melhorias para vários problemas.

## <a name="azure-atp-release-245"></a>Azure ATP versão 2.45

Lançado em 19 de agosto de 2018

- **O Azure ATP adiciona o ETW (Rastreamento de Eventos para Windows) como uma fonte de dados adicional**  <br> O ETW (Rastreamento de Eventos para Windows) é adicionado como fonte de dados adicional, além do tráfego de rede existente e dos eventos do Windows. O ETW fornece detecções de atividades suspeitas adicionais, incluindo: promoções do controlador de domínio suspeitas e solicitações de replicação do controlador de domínio suspeitas (ambas são possíveis ataques DCShadow). <br>
Somente sensores do ATP instalados em controladores de domínio têm suporte detecções baseadas no ETW. As detecções do ETW não têm suporte nos sensores autônomos do ATP. <br>  

- **Quatro novas detecções agora em disponibilidade geral** <br>
  - Conexão de VPN suspeita
  - Golden Ticket do Kerberos – conta não existente 
  - Promoção do controlador de domínio suspeita (possível ataque DcShadow) – detecção baseada no ETW, só disponível nos sensores do ATP 
  - Solicitação de replicação do controlador de domínio suspeita (possível ataque DcShadow) – detecção baseada no ETW, só disponível nos sensores do ATP

- Essa versão também inclui correções e melhorias para vários problemas.


## <a name="azure-atp-release-244"></a>Azure ATP versão 2.44

Lançado em 12 de agosto de 2018

- Essa versão inclui correções e melhorias para vários problemas.
- Os arquivos de log criados no computador do sensor não incluem o log de "Estatística de Exceção".


## <a name="azure-atp-release-243"></a>Azure ATP versão 2.43

Lançamento de 5 de agosto de 2018

- Essa versão inclui correções e melhorias para vários problemas.



## <a name="azure-atp-release-242"></a>Azure ATP versão 2.42

Lançado em 29 de julho de 2018

- Essa versão inclui correções e melhorias para vários problemas. 


## <a name="azure-atp-release-241"></a>Azure ATP versão 2.41

Lançado em 22 de julho de 2018

- **O suporte de várias florestas do Azure ATP está sendo distribuído gradualmente (visualização)** <br> Agora, o ATP do Azure pode dar suporte a organizações com várias florestas, permitindo monitorar a atividade e os perfis de usuário entre florestas. Essa nova funcionalidade permite que você:

  - Exiba e investigue as atividades executadas pelos usuários em várias florestas de um único painel de controle.
  - Melhore a detecção e reduza os falsos positivos, fornecendo integração avançada do Active Directory e a resolução de conta.
  - Obtenha melhores alertas de monitoramento e emissão de relatórios para cobertura entre organizações.


-   **Novas detecções: DCShadow**<br>Duas novas detecções foram adicionadas para ajudar a proteger contra ataques de sombra do controlador de domínio (DCShadow):

    -   Promoção do controlador de domínio suspeito (possível ataque DCShadow) – essa detecção ajuda a detectar ataques nos quais uma máquina representa um controlador de domínio e tenta usar a replicação para propagar alterações em outros controladores de domínio em seu domínio.

    -   Solicitação de replicação suspeita (possível ataque DCShadow) – essa detecção ajuda a proteger contra ataques que tentam executar a promoção DC dos computadores que não são controladores de domínio para alterar objetos do directory.

-   **Informações aprimoradas de downgrade de criptografia**<br>Agora a detecção de downgrade de criptografia fornece mais informações sobre o tipo específico de ataque detectado: overpass-the-hash, golden ticket e skeleton key. Além disso, esses alertas foram agregados para permitir uma investigação mais fácil.
- Essa versão inclui correções e melhorias para vários problemas. 


## <a name="azure-atp-release-240"></a>Azure ATP versão 2.40

Lançado em 15 de julho de 2018

- A detecção de pass-the-ticket agora inclui uma seção de evidências na página de detalhes do alerta. Isso fornece informações adicionais para a investigação do alerta.

- Os sinalizadores de controle de acesso do usuário, que podem ser encontrados no perfil de um usuário nos Dados do diretório, agora incluem uma legenda para permitir um melhor entendimento dos atributos que estão habilitados e desativados.  

## <a name="azure-atp-release-239"></a>Azure ATP versão 2.39

Lançado em 5 de julho de 2018
-   **Nova detecção adicionada: Golden Ticket do Kerberos – conta não existente** (versão prévia)<br>Essa nova detecção ajuda a proteger sua organização contra ataques em que um golden ticket é criado para uma conta que não existe no seu domínio. Para saber mais, confira o [Guia de atividades suspeitas da Proteção Avançada contra Ameaças do Azure](suspicious-activity-guide.md)

- Essa versão inclui correções e melhorias para vários problemas. 


## <a name="azure-atp-release-238"></a>Azure ATP versão 2.38

Lançado em 1º de julho de 2018

- Esta versão inclui correções e aprimoramentos para vários problemas, bem como os aprimoramentos do portal do Azure ATP.

## <a name="azure-atp-release-237"></a>Azure ATP versão 2.37

Lançado em 24 de junho de 2018

- Essa versão inclui correções e melhorias para vários problemas. 

## <a name="azure-atp-release-236"></a>Azure ATP versão 2.36

Lançado em 17 de junho de 2018

- Essa versão inclui correções e melhorias para vários problemas. 


## <a name="azure-atp-release-235"></a>Azure ATP versão 2.35

Lançamento em 10 de junho de 2018
 
- **Novas detecções de versão prévia**<br></br>De agora em diante, a Azure ATP aproveitará o fato de que é um serviço de nuvem, no qual novos recursos podem ser entregues em ciclos rápidos, e fornecerá novas detecções com a maior rapidez possível. Essas novas detecções serão marcadas como "versão prévia" quando forem lançadas pela primeira vez. Normalmente, uma nova detecção passa de versão prévia para disponibilidade geral em poucas semanas. Por padrão, você verá as detecções de versão prévia. Para obter informações de como recusar, confira [detecções de versão prévia](working-with-suspicious-activities.md#preview-detections).
 
- **Detecção de VPN suspeita**<br></br>Esta versão apresenta uma versão prévia da detecção de VPN suspeita. A Azure ATP aprende o comportamento de VPN do usuário, incluindo os computadores aos quais os usuários se conectam e as localizações de onde eles se conectam e alerta você quando há algum desvio do comportamento esperado. Para obter mais informações, confira [Detecção de VPN suspeita](suspicious-activity-guide.md).

- **Atualização atrasada**<br></br>Agora existe a opção de configurar os sensores da Azure ATP para serem atualizados mais tarde, sempre que a Azure ATP for atualizada. Agora é possível configurar cada sensor da Azure ATP para **Atualização atrasada**, para que ele seja atualizado 24 horas depois que o serviço de nuvem Azure ATP for atualizado. Esse recurso permite que você teste a atualização em sensores de teste específicos e apenas atualize os sensores de produção mais tarde. Se você descobrir algum problema durante o primeiro ciclo de atualização, abra um tíquete de suporte. Para obter mais informações, confira [Atualizar sensores da Azure ATP](sensor-update.md).

- **A detecção de implementação de protocolo incomum foi atualizada**<br></br>A detecção de implementação de protocolo incomum agora fornece mais informações. Agora você pode ver qual ferramenta de possível ataque a Azure ATP suspeita que esteja ativa em sua rede. Para obter mais informações, confira o [Guia de atividades suspeitas](suspicious-activity-guide.md).
 
- **Alerta de sensor desatualizado**<br></br>A Azure ATP inclui um novo alerta de monitoramento para informar se um sensor está mais de três versões desatualizado. Se esse alerta aparecer, você deverá atualizar o sensor ou investigar por que o sensor não está sendo atualizado automaticamente. Se o alerta persistir, desinstale e reinstale o sensor.

- Essa versão inclui correções e melhorias para vários problemas. 

## <a name="azure-atp-release-234"></a>Azure ATP versão 2.34

Lançado em 3 de junho de 2018
 
- Essa versão inclui correções e melhorias para vários problemas. 

 
## <a name="azure-atp-release-233"></a>Azure ATP versão 2.33

Lançamento: 27 de maio de 2018

- Recurso de versão prévia: o ATP do Azure agora é compatível com novos idiomas e 13 novas localidades:
    - Tcheco
    - Húngaro
    - Italiano
    - Coreano
    - Holandês
    - Polonês
    - Português (Brasil)
    - Português (Portugal)
    - Rússia
    - Sueco
    - Turco
    - Chinês (China)
    - Chinês (Taiwan)


## <a name="azure-atp-release-232"></a>Azure ATP versão 2.32

Lançado em 13 de maio de 2018
 
- Essa versão inclui correções e melhorias para vários problemas. 

## <a name="azure-atp-release-231"></a>Azure ATP versão 2.31

Lançamento em 6 de maio de 2018
 
- Foram feitas melhorias na resolução de nome. Como parte desse esforço, além da resolução ativa RPC e NetBIOS, o sensor pode emitir um pacote Client Hello TLS para a porta RDP (3389) do ponto de extremidade. 
- Essa versão inclui correções e melhorias para vários problemas. 

## <a name="azure-atp-release-230"></a>Azure ATP versão 2.30

Lançado em 29 de abril de 2018
 
- Agora, as atividades suspeitas de downgrade de criptografia incluem uma seção de evidências que descreve os sintomas detectados pelo Azure ATP e que fazem com que ele suspeite de uma atividade de downgrade de criptografia. 
-   Agora, o Azure ATP usa o Azure Email Orchestrator para todos os emails enviados do Azure ATP, inclusive atividades suspeitas, alertas de monitoramento e relatórios. Você verá que essas notificações de email agora seguem um formato consistente para facilitar o uso e que arquivos do Excel terão um link para download no console.
 
 
## <a name="azure-atp-release-229"></a>Azure ATP versão 2.29

Lançado em 22 de abril de 2018
 
- Essa versão inclui correções e melhorias para vários problemas. 
 
 
## <a name="azure-atp-release-228"></a>Azure ATP versão 2.28

Lançado em 15 de abril de 2018
 
-   Os usuários que são membros dos grupos de funções Usuários do Azure ATP e Visualizadores do Azure ATP agora têm permissões para ver alertas de monitoramento.
- Essa versão inclui correções e melhorias para vários problemas. 


## <a name="azure-atp-release-227"></a>Azure ATP versão 2.27

Lançado em 8 de abril de 2018

- Agora você tem a capacidade de fornecer comentários do usuário na barra de navegação superior. Clicar no Smiley na barra de menu habilita você a enviar um email à equipe da Proteção Avançada contra Ameaças do Azure com seus comentários.

- Essa versão inclui correções e melhorias para vários problemas. 
 

## <a name="azure-atp-release-226"></a>Azure ATP versão 2.26

Lançado em 25 de março de 2018

- Quando o ATP do Azure alerta sobre uma atividade suspeita que você identifica como um positivo benigno (uma ação legítima que não é uma atividade suspeita), você tem a opção de excluir computadores e endereços IP de mais detecções, como: downgrade de criptografia, força bruta de LDAP, PAC forjado, força bruta e Pass-the-hash.
-   O desempenho do sensor do Azure ATP foi aprimorado.
-   Uma nova região foi adicionada para a implantação do Workspace. Agora é possível implantar um workspace na Ásia. 


## <a name="azure-atp-release-225"></a>Azure ATP versão 2.25

Lançada em 18 de março de 2018

- Agora há compatibilidade com a MFA (Autenticação Multifator) no Azure ATP. Os locatários usando MFA agora podem entrar no portal do Azure ATP.
- O Azure ATP agora tem uma página [**Status do sistema**](https://health.atp.azure.com/) para fornecer informações sobre se o Portal de Gerenciamento do workspace está funcionando e ativo, se há problemas com as detecções e se o sensor pode enviar tráfego para a nuvem. Você pode acessar o **Status do sistema** na barra de menus do Azure ATP.


## <a name="azure-atp-release-224"></a>Versão 2.24 do Azure ATP

Lançada em 11 de março de 2018

**Detecções novas e atualizadas**
  - Criação de serviços suspeitos – invasores tentam executar serviços suspeitos na sua rede. Agora, o Azure ATP gera um alerta ao identificar que um novo serviço que parece suspeito está sendo executado por uma pessoa em um computador específico. Essa detecção se baseia em eventos (e não no tráfego de rede) e ocorre em qualquer controlador de domínio da rede que esteja encaminhando o evento 7045 para o Azure ATP. Para saber mais, consulte o [Guia de atividades suspeitas](suspicious-activity-guide.md).

**Investigação aprimorada**
  - O Azure ATP tem um [perfil de entidade](entity-profiles.md) aperfeiçoado. O perfil de entidade oferece uma plataforma projetada para investigações aprofundadas das atividades do usuário – como os recursos acessados, computadores em que fizeram logon, e muito mais. O perfil de entidade também fornece os dados de diretório e permite identificar possíveis caminhos de movimentação lateral de/para a entidade. Assim, é possível saber mais sobre violações em potencial na sua organização.

  - Com o ATP, é possível marcar manualmente as entidades como *confidenciais*, a fim de aperfeiçoar as detecções e o monitoramento. Essa marcação afeta diversas detecções do Azure ATP, como a detecção de modificação de grupos confidenciais e o [caminho de movimentação lateral](use-case-lateral-movement-path.md), que dependem de entidades consideradas confidenciais.

**Novos relatórios para ajudá-lo a investigar**
  - O [relatório de senhas expostas em texto não criptografado](reports.md) permite detectar quando os serviços enviam credenciais de conta em texto sem formatação. Assim, é possível investigar os serviços e aprimorar o nível de segurança da rede. Esse relatório substitui os alertas de atividade suspeita em texto não criptografado.
  - O [relatório de caminhos de movimento lateral para contas confidenciais](reports.md) lista as contas confidenciais que estão expostas por meio de caminhos de movimentação lateral. Dessa forma, é possível reduzir esses caminhos e fortalecer sua rede a fim de minimizar o risco de superfície de ataque. Assim, você pode impedir a movimentação lateral, para que os invasores não se movimentem entre usuários e computadores ao longo da rede até encontrarem o prêmio máximo da segurança virtual: suas credenciais de conta do administrador.

- Agora, é possível acessar facilmente a documentação em um link fornecido com um alerta de atividade suspeita, a fim de exibir as [etapas de investigação a serem seguidas](suspicious-activity-guide.md). 

**Melhorias de desempenho**
 -  A infraestrutura do sensor do Azure ATP teve seu desempenho aprimorado: a exibição agregada do tráfego permite otimizar a CPU e o pipeline de pacotes. Além disso, reutiliza soquetes para os controladores de domínio minimizarem as sessões de SSL para o DC.

## <a name="see-also"></a>Consulte Também
- [O que é o Azure Advanced Threat Protection?](what-is-atp.md)
- [Perguntas frequentes](atp-technical-faq.md)
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
