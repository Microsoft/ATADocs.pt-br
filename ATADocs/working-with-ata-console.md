---
title: "Noções básicas sobre o console do Advanced Threat Analytics | Microsoft Docs"
description: Descreve como entrar no Console do ATA e os componentes do console
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3d687087dd9e1ae7f7642f9fdd7d89420f3bec27
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*



# <a name="working-with-the-ata-console"></a>Trabalhando com o Console do ATA

Use o Console do ATA para monitorar e responder a atividades suspeitas detectadas pelo ATA.

Digitar o ? fornecerá os atalhos de teclado para acessibilidade do Portal do ATA. 

## <a name="enabling-access-to-the-ata-console"></a>Habilitando o acesso à Console do ATA
Para fazer logon com êxito no Console do ATA, você precisa fazer logon com um usuário que recebeu a função adequada do ATA para acessar o Console do ATA. Para saber mais sobre RBAC (Controle de acesso baseado em função) no ATA, confira [Como trabalhar com grupos de função do ATA](ata-role-groups.md).

## <a name="logging-into-the-ata-console"></a>Fazer logon no Console do ATA

1. No servidor do Centro do ATA, clique no ícone **Console do Microsoft ATA** na área de trabalho ou abra um navegador e procure o Console do ATA.

    ![Ícone do servidor de ATA](media/ata-server-icon.png)

>[!NOTE]
> Também é possível abrir um navegador na Central do ATA ou no Gateway do ATA e navegar até o endereço IP configurado na instalação da Central do ATA para o Console do ATA.    

2.  Se o computador no qual o Centro do ATA está instalado e o computador do qual você está tentando acessar o Console do ATA estiverem ingressados no domínio, o ATA dará suporte ao logon único integrado com a autenticação do Windows, se você já estiver conectado no computador, o ATA usará esse token para conectá-lo ao Console do ATA. Você também pode fazer logon usando um cartão inteligente. Suas permissões no ATA corresponderão à sua [função de administrador](ata-role-groups.md).

> [!NOTE]
> Certifique-se de fazer logon no computador do qual deseja acessar o Console do ATA usando seu nome de usuário administrador e senha do ATA. Como alternativa, você pode executar seu navegador como um usuário diferente ou desconectar do Windows e fazer logon com o usuário administrador do ATA. Para solicitar que o Console do ATA peça credenciais, acesse o console usando um endereço IP e você será solicitado a inserir as credenciais.

Para fazer logon usando o SSO, certifique-se de que o site do Console do ATA esteja definido como um site de intranet local no seu navegador e de acessá-lo usando um nome curto ou um localhost.

> [!NOTE]
> Além de registrar cada atividade suspeita e alerta de integridade, cada alteração de configuração feita no Console do ATA é auditada no Log de Eventos do Windows no computador do Centro do ATA, em **Applications and services log (Log de serviços e aplicativos)** e em **Microsoft ATA**. Cada logon no console do ATA é auditado também.<br></br>  A configuração que afeta o Gateway do ATA também é registrada no Log de Eventos do Windows do computador do Gateway do ATA. 



## <a name="the-ata-console"></a>O Console do ATA

O Console do ATA fornece uma visão geral de todas as atividades suspeitas em ordem cronológica. Ele permite que você analise detalhes de qualquer atividade e executar ações baseadas em atividades. O console também exibe alertas e notificações para realçar problemas com a rede de ATA ou novas atividades que são consideradas suspeitas.

Esses são os principais elementos do Console do ATA.


### <a name="attack-time-line"></a>Linha do tempo de ataque

Essa é a página de aterrissagem exibida quando você entra no Console do ATA. Por padrão, todas as atividades suspeitas abertas são mostradas na linha do tempo de ataque. Você pode filtrar a linha do tempo de ataque para mostrar as atividades suspeitas com status Todos, Aberto, Descartado ou Resolvido. Você também pode ver a severidade atribuída a cada atividade.

![Imagem da linha do tempo de ataque do ATA](media/ATA-Suspicious-Activity-Timeline.jpg)

Para saber mais, confira [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md).

### <a name="notification-bar"></a>Barra de notificação

Quando uma nova atividade suspeita é detectada, a barra de notificação abrirá automaticamente no lado direito. Se houver novas atividades suspeitas desde a última vez que você entrou, a barra de notificação abrirá depois de você ter feito logon com êxito. Você pode clicar na seta à direita a qualquer momento para acessar a barra de notificação.

![Imagem da barra de notificação de ATA](media/notification-bar-1.7.png)

### <a name="filtering-panel"></a>Painel de filtro

Você pode filtrar quais atividades suspeitas são exibidas na linha do tempo de ataque ou exibidas na guia de atividades suspeitas de perfil de entidade com base no Status e na Severidade.

### <a name="search-bar"></a>Barra de pesquisa

No menu superior, você encontrará uma barra de pesquisa. Você pode pesquisar por um usuário específico, computador ou grupos no ATA. Para experimentar, basta começa a digitar.

![Imagem de pesquisa do Console do ATA](media/ATA-console-search.png)

### <a name="health-center"></a>Centro de integridade

O Centro de integridade fornece alertas quando algo não está funcionando corretamente na implantação do ATA.

![Imagem do Centro de integridade do ATA](media/ATA-Health-Issue.jpg)

Sempre que o sistema encontrar um problema, como um erro de conectividade ou um Gateway de ATA desconectado, o ícone da Central de integridade informará você exibindo um ponto vermelho. ![Imagem do ponto vermelho do Centro de integridade de ATA](media/ATA-Health-Center-Alert-red-dot.png)

Os alertas do Centro de Integridade podem ser descartados ou resolvidos e são categorizados com status Alto, Médio ou Baixo, dependendo da gravidade. Se você resolver um alerta que o serviço de ATA detecta como ativo, ele será movido automaticamente para abrir a lista de alertas. Se o sistema detectar que a causa do alerta já não existe mais (a situação foi corrigida), ele será movido automaticamente para a lista resolvida.

### <a name="user-and-computer-profiles"></a>Perfis de usuário e computador

O ATA cria um perfil para cada usuário e computador na rede. No perfil de usuário, o ATA exibe informações gerais, como associação de grupo, logons recentes e recursos acessados recentemente. Ele também fornece uma lista de locais em que o usuário conectou por meio de VPN. Para obter uma lista de associações de grupo que o ATA considera confidencial, consulte abaixo.

![Perfil de usuário](media/user-profile.png)

No perfil de computador, o ATA exibe informações gerais, como logons recentes e recursos acessados recentemente.

![Perfil de computador](media/computer-profile.png)

O ATA fornece informações adicionais sobre as entidades (computadores, dispositivos, usuários) nas seguintes páginas: resumo, atividades e atividades suspeitas.

Um perfil que o ATA não tenha sido capaz de resolver completamente será identificado com um ícone de círculo preenchido pela metade ao lado dele.


![Imagem de perfil não resolvido do ATA](media/ATA-Unresolved-Profile.jpg)

### <a name="sensitive-groups"></a>Grupos confidenciais

A lista de grupos a seguir é considerada **Confidencial** pelo ATA. Esses grupos serão sinalizados como tendo privilégios administrativos e gerarão alertas que correspondem às contas confidenciais:

- Controladores de domínio de empresa somente leitura 
- Administradores do domínio 
- Controladores de Domínio 
- Administradores de esquemas,
- Administrador corporativo 
- Proprietários criadores de política de grupo 
- Controladores de domínio somente leitura 
- Administradores  
- Usuários avançados  
- Opers. de contas  
- Operadores de Servidores   
- Operadores de impressão,
- Operadores de backup,
- Replicadores 
- Usuários da Área de Trabalho Remota 
- Operadores de Configuração de Rede 
- Criadores de confiança de floresta de entrada 
- Administradores do DNS 


### <a name="mini-profile"></a>Miniperfil

Em qualquer lugar no console onde exista uma única entidade apresentada, como um usuário ou computador, se você passar o mouse sobre a entidade, um miniperfil será aberto automaticamente, exibindo as informações a seguir, se disponíveis:

![Imagem de miniperfil do ATA](media/ATA-mini-profile.jpg)

-   Nome

-   Imagem

-   Email

-   Telefone:

-   Número de atividades suspeitas por severidade



## <a name="see-also"></a>Consulte também
[Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
