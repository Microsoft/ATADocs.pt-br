---
title: Trabalhar com alertas de segurança no Microsoft Defender para Identidade
description: Descreve como examinar os alertas de segurança emitidos pelo Microsoft Defender para Identidade
ms.date: 10/27/2020
ms.topic: how-to
ms.openlocfilehash: 8cd2cf79ef590d852c66a426d0217104f55b29a1
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96544582"
---
# <a name="working-with-security-alerts"></a>Trabalhando com alertas de segurança

> [!NOTE]
> Os recursos do [!INCLUDE [Product long](includes/product-long.md)] explicados nesta página também podem ser acessados usando o novo [portal](https://portal.cloudappsecurity.com).

Este artigo explica noções básicas de como trabalhar com os alertas de segurança do [!INCLUDE [Product long](includes/product-long.md)].

<a name="review-suspicious-activities-on-the-attack-time-line"></a>

## <a name="review-security-alerts-on-the-attack-timeline"></a>Examinar os alertas de segurança na linha do tempo do ataque 

Após fazer logon no portal do [!INCLUDE [Product short](includes/product-short.md)], você será levado automaticamente à **Linha do tempo de alertas de segurança** aberta. Os alertas de segurança são listados em ordem cronológica com o alerta mais recente na parte superior da linha do tempo.

Cada alerta de segurança tem as seguintes informações:

- Entidades envolvidas, incluindo usuários, computadores, servidores, controladores de domínio e recursos.

- O horário e o período das atividades suspeitas que iniciaram o alerta de segurança.
- Gravidade do alerta: alta, média ou baixa.
- Status: Aberto, fechado ou suprimido.
- Capacidade de:
  - Compartilhe o alerta de segurança com outras pessoas da sua organização por email.
  - Baixe o alerta de segurança em formato do Excel.

> [!NOTE]
>
> - Quando você passa o mouse sobre um usuário ou computador, um miniperfil de entidade é exibido. O miniperfil fornece informações adicionais sobre a entidade e inclui o número de alertas de segurança vinculados à entidade.
> - Clicar na entidade leva ao perfil de entidade do usuário ou do computador.

![Imagem da linha do tempo de alertas de segurança do [!INCLUDE [Product short](includes/product-short.md)]](media/sa-timeline.png)

## <a name="security-alert-categories"></a>Categorias de alertas de segurança

Os alertas de segurança do [!INCLUDE [Product short](includes/product-short.md)] são divididos nas categorias ou fases a seguir, assim como as fases vistas em uma cadeia de eliminação de ataque cibernético típica.

- [Alertas de reconhecimento](reconnaissance-alerts.md)
- [Alertas de credencial comprometida](compromised-credentials-alerts.md)
- [Alertas de movimento lateral](lateral-movement-alerts.md)
- [Alertas de predominância de domínio](domain-dominance-alerts.md)
- [Alertas de exfiltração](exfiltration-alerts.md)

## <a name="preview-detections"></a>Detecções de versão prévia <a name="preview-detections"></a>

A equipe de pesquisa do [!INCLUDE [Product short](includes/product-short.md)] trabalha constantemente para implementar novas detecções de ataques recém-descobertos. Como o [!INCLUDE [Product short](includes/product-short.md)] é um serviço de nuvem, essas novas detecções são lançadas rapidamente para permitir que os clientes do [!INCLUDE [Product short](includes/product-short.md)] se beneficiem das novas detecções o mais breve possível.

Essas detecções são marcadas como uma notificação de versão prévia para ajudar a identificar as novas detecções e saber que elas são novas para o produto. Se você desativar as detecções de versão prévia, elas não serão exibidas no console do [!INCLUDE [Product short](includes/product-short.md)] (nem na linha do tempo nem nos perfis de entidade) e novos alertas não serão abertos.

![Detecção de versão prévia na linha do tempo](media/preview-detection-in-timeline.png)

Por padrão, as detecções de versão prévia são habilitadas no [!INCLUDE [Product short](includes/product-short.md)].

Para desabilitar as detecções de versão prévia:

1. No console do [!INCLUDE [Product short](includes/product-short.md)], selecione **Configuração**.
1. No menu à esquerda, em **Versão prévia**, clique em **Detecções**.
1. Use o controle deslizante para habilitar e desabilitar às detecções de versão prévia.

![detecções de versão prévia](media/preview-detections.png)

## <a name="filter-security-alerts-list"></a>Filtrar lista de alertas de segurança

Para filtrar lista de alertas de segurança:

1. No painel **Filtrar por** no lado esquerdo da tela, selecione uma das seguintes opções: **Tudo**, **Aberto**, **Fechado** ou **Suprimido**.

1. Para filtrar a lista ainda mais, selecione **Alta**, **Média** ou **Baixa**.

**Gravidade da atividade suspeita**

- **Baixa**

    Indica atividades que podem levar a ataques projetados para usuários ou softwares mal-intencionados para obter acesso aos dados organizacionais.

- **Média**

    Indica atividades que podem colocar identidades específicas em risco de ataques mais graves que podem resultar em roubo de identidade ou escalonamento privilegiado

- **Alta**

    Indica as atividades que podem levar a roubo de identidade, elevação de privilégios ou outros ataques de alto impacto

## <a name="managing-security-alerts"></a>Gerenciando alertas de segurança

É possível alterar o status de um alerta de segurança clicando em seu status atual e selecionando uma das seguintes opções **Aberto**, **Suprimido**, **Fechado** ou **Excluído**.
Para fazer isso, clique nos três pontos no canto superior direito de um alerta específico para revelar a lista de ações disponíveis.

![Ações do [!INCLUDE [Product short](includes/product-short.md)] para alertas de segurança](media/sa-actions.png)

**Status do alerta de segurança**

- **Abrir**: Todos os novos alertas de segurança são exibidos nessa lista.

- **Fechar**: É usado para rastrear alertas de segurança que você identificou, pesquisou e corrigiu como mitigado.

- **Suprimir**: Suprimir um alerta significa que você deseja ignorá-la por enquanto e apenas ser alertado novamente se houver uma nova instância. Isso significa que, se houver um alerta semelhante, o [!INCLUDE [Product short](includes/product-short.md)] não reabrirá. Porém, se o alerta parar por sete dias e então for observado novamente, um novo alerta será aberto.

- **Excluir**: Se você excluir um alerta, ele será excluído do sistema, do banco de dados e você NÃO poderá restaurá-lo. Após clicar em Excluir, será possível excluir todos os alertas de segurança do mesmo tipo.

- **Excluir**: A capacidade de excluir uma entidade de gerar mais de um determinado tipo de alertas. Por exemplo, você pode configurar o [!INCLUDE [Product short](includes/product-short.md)] para impedir que uma entidade (usuário ou computador) específica emita novamente um alerta para determinado tipo de atividade, como um administrador específico que executa código remoto ou um verificador de segurança que faz o reconhecimento de DNS. Além de ser capaz de adicionar exclusões diretamente no alerta de segurança conforme ele é detectado na linha do tempo, também é possível acessar a página Configuração até **Exclusões** e para cada alerta de segurança, é possível adicionar e remover manualmente entidades ou sub-redes excluídas (por exemplo, para Pass-the-Ticket).

> [!NOTE]
> As páginas de configuração podem ser modificadas apenas por administradores do [!INCLUDE [Product short](includes/product-short.md)].

## <a name="see-also"></a>Consulte Também

- [Trabalhar com o portal do [!INCLUDE [Product short](includes/product-short.md)]](workspace-portal.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
