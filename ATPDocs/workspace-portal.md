---
title: Noções básicas sobre o portal do Microsoft Defender para Identidade
description: Descreve como fazer logon no portal do Microsoft Defender para Identidade e os componentes desse portal
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e695bd20717bbb26cffcd5a6cb069eb2c520c876
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94847591"
---
# <a name="working-with-the-product-long-portal"></a>Trabalhar com o portal do [!INCLUDE [Product long](includes/product-long.md)]

> [!NOTE]
> Todos os recursos do [!INCLUDE [Product long](includes/product-long.md)] explicados nesta página também podem ser acessados usando o novo portal do [Cloud App Security](https://portal.cloudappsecurity.com).

Use o portal do [!INCLUDE [Product long](includes/product-long.md)] para monitorar e responder a atividades suspeitas detectadas pelo [!INCLUDE [Product short](includes/product-short.md)].

A tecla `?` fornece os atalhos de teclado para acessibilidade do Portal do [!INCLUDE [Product short](includes/product-short.md)].

O portal do [!INCLUDE [Product short](includes/product-short.md)] fornece uma visão geral de todas as atividades suspeitas em ordem cronológica. Ele permite que você analise detalhes de qualquer atividade e executar ações baseadas em atividades. O portal do [!INCLUDE [Product short](includes/product-short.md)] também exibe alertas e notificações para realçar problemas detectados pelo [!INCLUDE [Product short](includes/product-short.md)] ou novas atividades consideradas suspeitas.

Este artigo descreve como trabalhar com os principais elementos do portal do [!INCLUDE [Product short](includes/product-short.md)].

## <a name="enabling-access-to-the-product-short-portal"></a>Habilitar o acesso ao portal do [!INCLUDE [Product short](includes/product-short.md)]

Para fazer logon com êxito no portal do [!INCLUDE [Product short](includes/product-short.md)], é necessário fazer isso com um usuário atribuído a um grupo de segurança do Azure Active Directory que tenha acesso ao portal do [!INCLUDE [Product short](includes/product-short.md)].
Para saber mais sobre RBAC (controle de acesso baseado em função) no [!INCLUDE [Product short](includes/product-short.md)], confira [Trabalhar com grupos de função do [!INCLUDE [Product short](includes/product-short.md)]](role-groups.md).

## <a name="logging-into-the-product-short-portal"></a>Fazer logon no portal do [!INCLUDE [Product short](includes/product-short.md)]

1. Você pode entrar no portal do [!INCLUDE [Product short](includes/product-short.md)] fazendo logon no portal do [https://portal.atp.azure.com](https://portal.atp.azure.com) e selecionando sua instância ou navegando até a URL da instância: `https://*instancename*.atp.azure.com`.

1. O [!INCLUDE [Product short](includes/product-short.md)] dá suporte ao logon único integrado com a autenticação do Windows – se você já tiver feito logon em seu computador, o [!INCLUDE [Product short](includes/product-short.md)] usará esse token para conectar você ao portal do [!INCLUDE [Product short](includes/product-short.md)]. Você também pode fazer logon usando um cartão inteligente. Suas permissões no [!INCLUDE [Product short](includes/product-short.md)] correspondem à sua [função de administrador](role-groups.md).

   > [!NOTE]
   > Lembre-se de fazer logon no computador no qual deseja acessar o portal do [!INCLUDE [Product short](includes/product-short.md)] usando seu nome de usuário administrador e sua senha do [!INCLUDE [Product short](includes/product-short.md)]. Como alternativa, execute o navegador como um usuário diferente ou se desconecte do Windows e faça logon com o usuário administrador do [!INCLUDE [Product short](includes/product-short.md)]. Ao contrário do portal do [!INCLUDE [Product short](includes/product-short.md)], o novo portal do [Cloud App Security](https://portal.cloudappsecurity.com) oferece logon de vários usuários e não requer licença adicional para uso com o [!INCLUDE [Product short](includes/product-short.md)].

### <a name="attack-time-line"></a>Linha do tempo de ataque

A linha do tempo de ataque é a página de destino padrão exibida quando você entra no portal do [!INCLUDE [Product short](includes/product-short.md)]. Por padrão, todas as atividades suspeitas abertas são mostradas na linha do tempo de ataque. Você pode filtrar a linha do tempo de ataque para mostrar as atividades suspeitas com status Tudo, Aberto, Descartado ou Suprimido. Você também pode ver a severidade atribuída a cada atividade.

![Imagem da linha do tempo de ataque do [!INCLUDE [Product short](includes/product-short.md)]](media/sa-timeline.png)

Para obter mais informações, consulte [Trabalhando com alertas de segurança](working-with-suspicious-activities.md).

### <a name="whats-new"></a>Novidades

Após uma nova versão do [!INCLUDE [Product short](includes/product-short.md)] ser lançada, a janela **Novidades** será exibida na parte superior direita, para que você saiba o que foi adicionado na versão mais recente. Ela também fornece um link para o download da versão.

### <a name="filtering-panel"></a>Painel de filtro

Você pode filtrar quais atividades suspeitas são exibidas na linha do tempo de ataque ou exibidas na guia de atividades suspeitas de perfil de entidade com base no Status e na Severidade.

<a name="search-bar"></a>

### <a name="search-bar"></a>Barra de pesquisa

No menu superior, há uma barra de pesquisa. Você pode pesquisar por um usuário, computador ou grupo específico no [!INCLUDE [Product short](includes/product-short.md)]. Para experimentar, basta começa a digitar. Na parte inferior da barra de pesquisa, o número de resultados da pesquisa encontrados é indicado.

![Imagem de pesquisa no portal do [!INCLUDE [Product short](includes/product-short.md)]](media/workspace-portal-search.png)

Se clicar no número, você pode acessar a página de resultados da pesquisa, na qual pode filtrar os resultados por tipo de entidade para uma investigação mais detalhada.

![pesquisar resultados](media/search-results.png)

### <a name="health-center"></a>Centro de integridade

O Centro de integridade fornece alertas quando algo não está funcionando corretamente em sua instância do [!INCLUDE [Product short](includes/product-short.md)].

![Imagem do Centro de integridade do [!INCLUDE [Product short](includes/product-short.md)]](media/health-issue.png)

Sempre que o sistema encontra um problema, como um erro de conectividade ou um sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] desconectado, o ícone do Centro de integridade informa isso exibindo um ponto vermelho.

![Imagem do ponto vermelho do Centro de integridade [!INCLUDE [Product short](includes/product-short.md)]](media/health-bar.png)

### <a name="sensitive-groups"></a>Grupos confidenciais

Para saber mais sobre grupos confidenciais no [!INCLUDE [Product short](includes/product-short.md)], confira [Trabalhar com grupos confidenciais](sensitive-accounts.md).

### <a name="mini-profile"></a>Miniperfil

Se você passar o mouse sobre uma entidade, em qualquer lugar no portal do [!INCLUDE [Product short](includes/product-short.md)] em que haja uma única entidade apresentada, como um usuário ou computador, um miniperfil será aberto automaticamente exibindo as seguintes informações, se estiverem disponíveis e forem relevantes:

![Imagem do miniperfil do [!INCLUDE [Product short](includes/product-short.md)]](media/mini-profile.png)

- Name
- Título
- Departamento
- Marcas do AD
- Email
- Office
- Número do telefone
- Domain
- Nome SAM
- Criado em – quando a entidade foi criada no Active Directory. Se ela tiver sido criada antes do [!INCLUDE [Product short](includes/product-short.md)] iniciar o monitoramento, não será exibida.
- Visto pela primeira vez – a primeira vez em que o [!INCLUDE [Product short](includes/product-short.md)] observou uma atividade desta entidade.
- Visto por último – a última vez que o [!INCLUDE [Product short](includes/product-short.md)] observou uma atividade desta entidade.
- Notificação de SA – será exibida se houver atividades suspeitas associadas à entidade.
- Notificação do WD ATP – será exibida se houver atividades suspeitas no Microsoft Defender para Ponto de Extremidade associadas à entidade.
- Notificação de caminhos de movimento lateral – será exibida se tiverem sido detectados caminhos de movimento lateral para esta entidade nos últimos dois dias.

## <a name="see-also"></a>Consulte Também

- [Criar instâncias do [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
