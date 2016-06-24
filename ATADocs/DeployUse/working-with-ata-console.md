---
# required metadata

title: Trabalhando com o Console do ATA | Microsoft Advanced Threat Analytics
description: Descreve como entrar no Console do ATA e os componentes do console
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Trabalhando com o Console do ATA

Use o Console do ATA para monitorar e responder a atividades suspeitas detectadas pelo ATA.

## Habilitando o acesso à Console do ATA
Qualquer usuário que seja membro do grupo Administradores local no servidor do Console do ATA tem permissão para efetuar login no Console do ATA e gerenciar configurações de ATA.
Para permitir que um usuário faça logon no Console do ATA sem se tornar um administrador local, adicione-o ao grupo local: **Administradores do Microsoft Advanced Threat Analytics**.

## Fazer logon no Console do ATA

1. No servidor do Centro do ATA, clique no ícone **Console do Microsoft ATA** na área de trabalho ou abra um navegador e procure o Console do ATA.

    ![Ícone do servidor de ATA](media/ata-server-icon.png)

    > [!NOTE] Como alternativa, você pode abrir um navegador no Centro do ATA ou no Gateway do ATA e navegar até o endereço IP configurado na instalação do Centro do ATA para o Console do ATA.    

2.  Digite seu nome de usuário e senha e clique em **Entrar**.

![Imagem de tela de logon no ATA](media/ATA-log-in-screen.jpg)

    > [!NOTE]
    > You have to log in with a user who is a member of the local administrator group OR of the Microsoft Advanced Threat Analytics Administrators group.

## O Console do ATA

O Console do ATA fornece uma visão geral de todas as atividades suspeitas em ordem cronológica. Ele permite que você analise detalhes de qualquer atividade e executar ações baseadas em atividades. O console também exibe alertas e notificações para realçar problemas com a rede de ATA ou novas atividades que são consideradas suspeitas.

Esses são os principais elementos do Console do ATA.


### Linha do tempo de ataque

Essa é a página de aterrissagem exibida quando você entra no Console do ATA. Por padrão, todas as atividades suspeitas abertas são mostradas na linha do tempo de ataque. Você pode filtrar a linha do tempo de ataque para mostrar as atividades suspeitas com status Todos, Aberto, Descartado ou Resolvido. Você também pode ver a severidade atribuída a cada atividade.

![Imagem da linha do tempo de ataque do ATA](media/attack-timeline.png)

Para saber mais, confira [Trabalhando com atividades suspeitas](/advanced-threat-analytics/deploy-use/working-with-suspicious-activities).

### Barra de notificação

Quando uma nova atividade suspeita é detectada, a barra de notificação abrirá automaticamente no lado direito. Se houver novas atividades suspeitas desde a última vez que você entrou, a barra de notificação abrirá depois de você ter feito logon com êxito. Você pode clicar na seta à direita a qualquer momento para acessar a barra de notificação.

![Imagem da barra de notificação de ATA](media/notification-bar.png)

### Painel de filtro

Você pode filtrar quais atividades suspeitas são exibidas na linha do tempo de ataque ou exibidas na guia de atividades suspeitas de perfil de entidade com base no Status e na Severidade.

### Barra de pesquisa

No menu superior, você encontrará uma barra de pesquisa. Você pode pesquisar por um usuário específico, computador ou grupos no ATA. Para experimentar, basta começa a digitar.

![Imagem de pesquisa do Console do ATA](media/ATA-console-search.png)

### Centro de integridade

O Centro de integridade fornece alertas quando algo não está funcionando corretamente na implantação do ATA.

![Imagem do Centro de integridade do ATA](media/health-center.png)

Sempre que o sistema encontrar um problema, como um erro de conectividade ou um Gateway de ATA desconectado, o ícone da Central de integridade informará você exibindo um ponto vermelho. ![Imagem do ponto vermelho do Centro de integridade de ATA](media/ATA-Health-Center-Alert-red-dot.png)

Os alertas do Centro de Integridade podem ser descartados ou resolvidos e são categorizados com status Alto, Médio ou Baixo, dependendo da gravidade. Se você resolver um alerta que o serviço de ATA detecta como ativo, ele será movido automaticamente para abrir a lista de alertas. Se o sistema detectar que a causa do alerta já não existe mais (a situação foi corrigida), ele será movido automaticamente para a lista resolvida.

### Perfis de usuário e computador

O ATA cria um perfil para cada usuário e computador na rede. No perfil de usuário, o ATA exibe informações gerais, como associação de grupo, logons recentes e recursos acessados recentemente.

![Perfil de usuário](media/user-profile.png)

No perfil de computador, o ATA exibe informações gerais, como logons recentes e recursos acessados recentemente.

![Perfil de computador](media/computer-profile.png)

O ATA fornece informações adicionais sobre as entidades (computadores, dispositivos, usuários) nas seguintes páginas: resumo, atividades e atividades suspeitas.

Um perfil que o ATA não tenha sido capaz de resolver completamente será identificado com um ícone de círculo preenchido pela metade ao lado dele.


![Imagem de perfil não resolvido do ATA](media/ATA-Unresolved-Profile.jpg)

### Miniperfil

Em qualquer lugar no console onde exista uma única entidade apresentada, como um usuário ou computador, se você passar o mouse sobre a entidade, um miniperfil será aberto automaticamente, exibindo as informações a seguir, se disponíveis:

![Imagem de miniperfil do ATA](media/ATA-mini-profile.jpg)

-   Nome

-   Imagem

-   Email

-   Telefone:

-   Número de atividades suspeitas por severidade



## Consulte também
[Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


