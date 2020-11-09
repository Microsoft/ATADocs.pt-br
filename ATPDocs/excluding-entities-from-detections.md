---
title: Excluir entidades de detecções no Microsoft Defender para Identidade
description: Descreve como impedir que o Microsoft Defender para Identidade detecte atividades de entidades específicas como suspeitas
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e87d71ead236d36e032a43c825980f98f7f15eb4
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93277175"
---
# <a name="excluding-entities-from-detections"></a>Excluindo entidades de detecções

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Este artigo explica como excluir entidades do disparo de alertas. Determinadas entidades são excluídas para minimizar verdadeiros positivos benignos, assegurando que você possa capturar os verdadeiros positivos. Para impedir que o [!INCLUDE [Product long](includes/product-long.md)] crie ruído sobre atividades que, vindas de usuários específicos, podem fazer parte de seu ritmo normal de negócios, você pode silenciar ou excluir entidades específicas da geração de alertas. Além disso, determinadas entidades populares são excluídas por padrão.

Por exemplo, se você tiver um verificador de segurança que realiza reconhecimento DNS ou um administrador que executa scripts remotamente no controlador de domínio, e se essas forem atividades sancionadas cuja intenção for parte das operações de TI normais em sua organização, elas poderão ser excluídas. Para saber mais sobre cada detecção do [!INCLUDE [Product short](includes/product-short.md)] e entender quais entidades excluir, confira o [Guia de alertas de segurança](suspicious-activity-guide.md).

## <a name="entities-excluded-by-default-from-raising-alerts"></a>Entidades excluídas por padrão da geração de alertas

 Para determinados alertas, como **Comunicação suspeita sobre DNS** , exclusões automáticas de domínio são adicionadas pelo [!INCLUDE [Product short](includes/product-short.md)] com base em pesquisa e nos comentários dos clientes.

![Comunicação suspeita em exclusões automáticas de DNS](media/dns-auto-exclusions.png)

## <a name="exclude-entities-from-raising-alerts"></a>Excluir entidades da geração de alertas

Há duas maneiras para você excluir entidades manualmente, seja diretamente do alerta de segurança ou da guia **Exclusões** na página **Configuração**.

- **No alerta de segurança** : na linha do tempo de Atividade, quando você recebe um alerta em uma atividade para um usuário, computador ou endereço IP que **tem** permissão para executar uma atividade específica e pode fazer isso com frequência, faça o seguinte:
  - Clique com o botão direito do mouse nos três pontos no final da linha para o alerta de segurança nessa entidade e selecione **Fechar e excluir**. Isso adiciona o usuário, computador ou endereço IP à lista de exclusões desse alerta de segurança. Ele fecha o alerta de segurança e o alerta não está mais listado na lista de eventos **Aberto** na **linha do tempo de Alerta**.

    ![Excluir entidades](media/exclude-in-sa.png)

- **Na página Configuração** :  Para examinar ou modificar exclusões: em **Configurações** > **Detecção** , clique em **Exclusões** e selecione o alerta de segurança ao qual aplicar a exclusão, como **Reconhecimento de DNS**.

    ![Configuração de exclusão](media/exclusions.png)

Para adicionar uma entidade à configuração de **Exclusões** : insira o nome da entidade, clique no sinal de mais e, em seguida, clique em **Salvar** na parte inferior da página.

Para remover de uma entidade da configuração **Exclusões** : clique no sinal de menos ao lado do nome da entidade e, em seguida, clique em **Salvar** na parte inferior da página.

É recomendável que você adicione exclusões para detecções somente depois de receber alertas desse tipo específico *e* determinar que eles são positivos benignos verdadeiros.

> [!NOTE]
> Para sua proteção, nem todas as detecções oferecem a possibilidade de configurar exclusões.

Algumas das detecções fornecem dicas que ajudam você a decidir o que excluir.

Cada exclusão depende do contexto, em alguns você pode definir os usuários enquanto em outros você pode configurar computadores ou endereços IP.

Quando você tiver a possibilidade de exclusão de um endereço IP ou de um computador (você pode excluir um ou outro), não precisará fornecer os dois.

> [!NOTE]
> As páginas de configuração podem ser modificadas apenas por administradores do [!INCLUDE [Product short](includes/product-short.md)].

## <a name="see-also"></a>Confira Também

- [Guia de alertas de segurança do [!INCLUDE [Product short](includes/product-short.md)]](suspicious-activity-guide.md)
- [Fazer a integração com o Microsoft Defender para Ponto de Extremidade](integrate-mde.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
