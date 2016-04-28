---
# required metadata

title: Trabalhando com o Console do ATA | Microsoft Advanced Threat Analytics
description: Descreve como fazer logon no Console do ATA e nos componentes do console
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

1. No servidor do Centro de ATA, clique no ícone **Microsoft ATA Console** na área de trabalho ou abra um navegador e navegue para o Console do ATA.

    ![Ícone do servidor de ATA](media/ata-server-icon.png)

    > [!NOTE]
    > Como alternativa, você pode abrir um navegador no Centro de ATA ou no Gateway de ATA e navegar até o endereço IP configurado na instalação do Centro de ATA para o Console do ATA.    

2.  Digite seu nome de usuário e senha e clique em **Entrar**.

    ![Imagem de tela de logon no ATA](media/ATA-log-in-screen.jpg)

    > [!NOTE]
    > Você precisa fazer logon com um usuário que seja membro do grupo administrador local ou do grupo de Administradores do Microsoft Advanced Threat Analytics.

## Elementos do Console do ATA

O Console do ATA fornece uma exibição rápida de todas as atividades suspeitas em ordem cronológica e permite que você analise os detalhes de qualquer atividade ou execute ações como adicionar notas adicionais à atividade. O console também exibe alertas e notificações para realçar problemas com a rede de ATA ou novas atividades que são consideradas suspeitas.

Esses são os principais elementos do Console do ATA.


### Linha do tempo de ataque

Esta é a página padrão que é exibida quando você faz logon no Console do ATA. Por padrão, todas as atividades suspeitas abertas são mostradas na linha do tempo de ataque. Você pode filtrar a linha do tempo de ataque para mostrar as atividades suspeitas com status Todos, Aberto, Descartado ou Resolvido. Você também pode ver a severidade atribuída a cada atividade.

![Imagem da linha do tempo de ataque do ATA](media/attack-timeline.png)

Para obter mais informações, consulte [Trabalhando com atividades suspeitas](/advanced-threat-analytics/DeployUse/working-with-suspicious-activities).

### Barra de notificação

Quando uma nova atividade suspeita é detectada, a barra de notificação abrirá automaticamente no lado direito. Se houver novas atividades suspeitas desde a última vez que você entrou, a barra de notificação abrirá depois de você ter feito logon com êxito. Para acessá-la, você pode clicar na seta à direita a qualquer momento.

![Imagem da barra de notificação de ATA](media/notification-bar.png)

### Painel de filtro

Você pode filtrar quais atividades suspeitas são exibidas na linha do tempo de ataque ou exibidas na guia de atividades suspeitas de perfil de entidade com base no Status e na Severidade.

### Barra de pesquisa

Na parte superior da tela, você verá uma barra de pesquisa. Você pode pesquisar por um usuário específico, computador ou grupos no ATA. Para experimentar, basta começa a digitar.

![Imagem de pesquisa do Console do ATA](media/ATA-console-search.png)

### Centro de integridade

O Centro de integridade fornece alertas quando algo não está funcionando corretamente na rede de ATA.

![Imagem do Centro de integridade do ATA](media/health-center.png)

Sempre que o sistema encontrar um problema, como um erro de conectividade ou um Gateway de ATA desconectado, o ícone da Central de integridade informará você exibindo um ponto vermelho. ![Imagem do ponto vermelho do Centro de integridade de ATA](media/ATA-Health-Center-Alert-red-dot.png)

Como atividades suspeitas, os alertas do Centro de integridade podem ser descartados ou resolvidos e são categorizados com status Alto, Médio ou Baixo, dependendo da gravidade. Se você resolver um alerta que o serviço de ATA detecta como ativo, ele será movido automaticamente para abrir a lista de alertas. Se o sistema detectar que a causa do alerta já não existe mais (a situação foi corrigida), ele será movido automaticamente para a lista resolvida.

### Perfis de usuário e computador

O ATA cria um perfil para cada usuário e computador no domínio. No perfil de usuário, o ATA exibe informações gerais sobre o usuário, como associação de grupo, logons recentes e recursos acessados recentemente.

![Perfil de usuário](media/user-profile.png)

No perfil de computador, o ATA exibe informações gerais sobre o computador, logons recentes e recursos acessados recentemente.

![Perfil de computador](media/computer-profile.png)

O ATA fornece informações adicionais sobre as seguintes páginas: Resumo, Atividades e Atividades suspeitas.

> [!NOTE]
> Um perfil que o ATA não tenha sido capaz de resolver completamente será identificado com um ícone de círculo preenchido pela metade ao lado dele.

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
[Para obter suporte, confira nosso fórum!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


