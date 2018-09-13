---
title: Noções básicas sobre o portal de espaço de trabalho da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Descreve como fazer logon no portal de espaço de trabalho do Azure ATP e os componentes do portal de espaço de trabalho
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4ba46d60-3a74-480e-8f0f-9a082d62f343
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0fa8c1e19fde1ec779699b3a2c5411dea0908451
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166271"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*



# <a name="working-with-the-azure-atp-workspace-portal"></a>Como trabalhar com o portal de espaço de trabalho do Azure ATP

Use o portal de espaço de trabalho do Azure ATP para monitorar e responder a atividades suspeitas detectadas pelo ATP.

Digitar a tecla `?` fornece os atalhos de teclado para acessibilidade do portal de espaço de trabalho do Azure ATP. 

O portal de espaço de trabalho do Azure ATP fornece uma visão geral de todas as atividades suspeitas em ordem cronológica. Ele permite que você analise detalhes de qualquer atividade e executar ações baseadas em atividades. O portal de espaço de trabalho também exibe alertas e notificações para realçar problemas detectados pelo Azure ATP ou novas atividades consideradas suspeitas.

Este artigo descreve como trabalhar com os principais elementos do portal de espaço de trabalho do Azure ATP.


## <a name="enabling-access-to-the-azure-atp-workspace-portal"></a>Habilitando o acesso ao portal de espaço de trabalho do Azure ATP
Para fazer logon com êxito no portal de espaço de trabalho do Azure ATP, você precisa fazer logon com um usuário que foi atribuído ao grupo de segurança adequado do Azure Active Directory para acessar o portal de espaço de trabalho do Azure ATP. Para obter mais informações sobre o RBAC (controle de acesso baseado em função) no Azure ATP, consulte [Como trabalhar com grupos de função do Azure ATP](atp-role-groups.md).

## <a name="logging-into-the-azure-atp-workspace-portal"></a>Fazer logon no portal de espaço de trabalho do Azure ATP

1. Você pode entrar no portal de espaço de trabalho fazendo logon no portal de gerenciamento de espaço de trabalho [https://portal.atp.azure.com](https://portal.atp.azure.com) e, em seguida, selecionando o espaço de trabalho relevante ou navegando até a URL do espaço de trabalho: [https://*nomedoespaçodetrabalho*.atp.azure.com](https://*workspacename*.atp.azure.com).


2.  O Azure ATP dá suporte ao logon único integrado com a autenticação do Windows – se você já tiver feito logon em seu computador, o Azure ATP usará esse token para fazer logon no portal de espaço de trabalho do Azure ATP. Você também pode fazer logon usando um cartão inteligente. Suas permissões no Azure ATP correspondem à sua [função de administrador](atp-role-groups.md).

 > [!NOTE]
 > Faça logon no computador do qual deseja acessar o portal de espaço de trabalho do Azure ATP usando seu nome de usuário administrador e senha do Azure ATP. Como alternativa, você pode executar seu navegador como um usuário diferente ou se desconectar do Windows e fazer logon com o usuário administrador do Azure ATP. 


### <a name="attack-time-line"></a>Linha do tempo de ataque

Essa é a página de aterrissagem padrão exibida quando você entra no portal de espaço de trabalho do Azure ATP. Por padrão, todas as atividades suspeitas abertas são mostradas na linha do tempo de ataque. Você pode filtrar a linha do tempo de ataque para mostrar as atividades suspeitas com status Tudo, Aberto, Descartado ou Suprimido. Você também pode ver a severidade atribuída a cada atividade.

![Imagem da linha do tempo de ataques do Azure ATP](media/atp-sa-timeline.png)

Para saber mais, confira [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md).

### <a name="whats-new"></a>Novidades

Após uma nova versão do Azure ATP ser lançada, a janela **O que há de novo** é exibida na parte superior direita para que você saiba o que foi adicionado na versão mais recente. Ela também fornece um link para o download da versão.

### <a name="filtering-panel"></a>Painel de filtro

Você pode filtrar quais atividades suspeitas são exibidas na linha do tempo de ataque ou exibidas na guia de atividades suspeitas de perfil de entidade com base no Status e na Severidade.

### Barra de pesquisa <a name="search-bar"></a>

No menu superior, há uma barra de pesquisa. Você pode pesquisar por um usuário, computador ou grupo específico no Azure ATP. Para experimentar, basta começa a digitar. Na parte inferior da barra de pesquisa, o número de resultados da pesquisa encontrados é indicado. 

![Imagem da pesquisa no portal de espaço de trabalho do Azure ATP](media/atp-workspace-portal-search.png)

Se clicar no número, você pode acessar a página de resultados da pesquisa, na qual pode filtrar os resultados por tipo de entidade para uma investigação mais detalhada.

![pesquisar resultados](media/search-results.png)

### <a name="health-center"></a>Centro de integridade

O Centro de integridade fornece alertas quando algo não está funcionando corretamente em seu espaço de trabalho do Azure ATP.

![Imagem do centro de integridade do Azure ATP](media/atp-health-issue.png)

Sempre que o sistema encontrar um problema, como um erro de conectividade ou um sensor autônomo do Azure ATP desconectado, o ícone do Centro de integridade informa isso exibindo um ponto vermelho. 

![Imagem do ponto vermelho do centro de integridade do Azure ATP](media/atp-health-bar.png)

### <a name="sensitive-groups"></a>Grupos confidenciais

Para obter informações sobre grupos confidenciais no ATP, consulte [Trabalhando com grupos confidenciais](sensitive-accounts.md).

### <a name="mini-profile"></a>Miniperfil

Se você passar o mouse sobre uma entidade, em qualquer lugar no portal de espaço de trabalho em que existe uma única entidade apresentada, como um usuário ou computador, um miniperfil será aberto automaticamente exibindo as informações a seguir, se estiver disponíveis e forem relevantes:

![Imagem de miniperfil do Azure ATP](media/atp-mini-profile.png)

- Nome
- Título
- Departamento
- Marcas do AD
- Email
- Office
- Número do telefone
- Domain
- Nome SAM
- Criado em – quando a entidade foi criada no Active Directory. Se tiver sido criada antes do Azure ATP iniciar o monitoramento, não será exibida.
- Visto pela primeira vez – a primeira vez em que o Azure ATP observou uma atividade desta entidade.
- Visto pela última vez – a última vez em que o Azure ATP observou uma atividade desta entidade.
- Notificação de SA – será exibida se houver atividades suspeitas associadas à entidade.
- Notificação do WD ATP – será exibida se houver atividades suspeitas no Windows Defender ATP associadas à entidade.
- Notificação de caminhos de movimento lateral – será exibida se tiverem sido detectados caminhos de movimento lateral para esta entidade nos últimos dois dias.


## <a name="see-also"></a>Consulte Também

- [Criando espaços de trabalho do Azure ATP](install-atp-step1.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)