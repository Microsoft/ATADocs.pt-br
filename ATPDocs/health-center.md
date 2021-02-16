---
title: Monitorar a integridade e os eventos do sistema Microsoft defender for Identity
description: Use o centro de integridade para verificar como o Microsoft defender for Identity Service está funcionando e seja alertado sobre possíveis problemas e exibir eventos do sistema no Visualizador de eventos.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: ac03020c559a860fded89a496bc927da06fce3d9
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100534286"
---
# <a name="work-with-microsoft-defender-for-identity-health-and-events"></a>Trabalhar com o Microsoft defender para eventos e integridade de identidade

## <a name="microsoft-defender-for-identity-health-center"></a>Centro de integridade do Microsoft defender para identidade

O [!INCLUDE [Product long](includes/product-long.md)] centro de integridade permite que você saiba como sua [!INCLUDE [Product short](includes/product-short.md)] instância está sendo executada e alerta quando há problemas.

## <a name="working-with-the-defender-for-identity-health-center"></a>Trabalhando com o defender para o centro de integridade de identidade

O [!INCLUDE [Product short](includes/product-short.md)] centro de integridade permite que você saiba que há um problema gerando um alerta (um ponto vermelho) acima do ícone da central de integridade na barra de navegação.

![[! INCLUIR [produto curto] (inclui/produto-curto. MD)] barra de ferramentas de ponto vermelho do centro de integridade](media/health-bar.png)

### <a name="managing-defender-for-identity-health"></a>Gerenciando o defender para integridade de identidade

Para verificar a integridade geral da sua [!INCLUDE [Product short](includes/product-short.md)] instância, selecione **Health** ![ [! INCLUIR [produto curto] (inclui/produto-curto. MD)] ícone do centro de integridade](media/red-dot.png)

- Todos os problemas abertos podem ser gerenciados configurando-os para **Fechar** ou **Suprimir** clicando nos três pontos no canto do alerta e fazendo sua escolha.

- **Abrir**: todas as novas atividades suspeitas aparecem nesta lista.

- **Fechar**: é usado para rastrear atividades suspeitas que você identificou, pesquisou e corrigiu como mitigado.

    > [!NOTE]
    > [!INCLUDE [Product short](includes/product-short.md)] poderá reabrir uma atividade fechada se a mesma atividade for detectada novamente em um curto período de tempo.

- **Suprimir**: suprimir uma atividade significa que você deseja ignorá-la por enquanto e apenas ser alertado novamente se houver uma nova instância. Se houver um alerta semelhante [!INCLUDE [Product short](includes/product-short.md)] , ele não será reaberto. Mas, se o alerta parar por sete dias e, depois, for observado novamente, você será alertado novamente.

- **Reabrir**: você pode reabrir um alerta fechado ou suprimido para que ele seja exibido novamente como **Aberto** na linha do tempo.

- **Excluir**: na linha do tempo de alerta de segurança, você também tem a opção de excluir um problema de integridade. Se você excluir um alerta, ele será excluído da instância e você NÃO poderá restaurá-lo. Após clicar em Excluir, será possível excluir todos os alertas de segurança do mesmo tipo.

![[! INCLUIR [produto curto] (inclui/produto-curto. MD)] imagem de problemas do centro de integridade](media/health-issue.png)

## <a name="see-also"></a>Consulte Também

- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
