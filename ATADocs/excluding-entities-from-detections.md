---
title: Excluindo entidades de detecções no Advanced Threat Analytics
description: Descreve como impedir que o ATA detecte atividades de entidade específicas como suspeitas
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 344c0f33-45e1-42e2-a051-f722a4504531
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 84e4b6e5951bf16281c60c87e46ce1a799795c55
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2020
ms.locfileid: "84775328"
---
# <a name="excluding-entities-from-detections"></a>Excluindo entidades de detecções

*Aplica-se a: Advanced Threat Analytics versão 1.9*

Este artigo explica como excluir entidades de disparar alertas para minimizar verdadeiros positivos benignos mas ao mesmo tempo, capturar os verdadeiros positivos. Para impedir que o ATA seja ruidoso sobre as atividades que, de usuários específicos, podem ser parte de seu ritmo normal de negócios, você pode silenciar ou excluir entidades específicas da geração de alertas.

Por exemplo, se você tiver um verificador de segurança que realiza reconhecimento DNS ou um administrador que executa scripts remotamente no controlador de domínio, essas serão atividades sancionadas cujo objetivo é parte das operações de TI normais em sua organização.

Para excluir entidades da geração de alertas no ATA:

Há duas maneiras em que você pode excluir entidades, na atividade suspeita em si ou no guia **Exclusões** na página **Configuração**.

- **Na atividade suspeita**: na linha do tempo de atividade suspeita, quando você receber um alerta em uma atividade para um usuário ou computador ou endereço IP que tem permissão para executar uma atividade específica e pode realizá-lo com frequência, clique com botão direito do mouse nos três pontos no final da linha da atividade suspeita nessa entidade e selecione **Fechar e excluir**. <br></br>Isso adiciona o usuário, computador ou endereço IP à lista de exclusões da atividade suspeita. Ele fecha a atividade suspeita e não está mais listado na lista **abrir** eventos na **linha do tempo de atividade suspeita**.

    ![Excluir entidades](./media/exclude-in-sa.png)

- **Na página Configuração**: para examinar ou modificar qualquer exclusão: em **Configuração** clique em **Exclusões** e, em seguida, selecione a atividade suspeita, como **Credenciais de conta confidencial expostas**.

    ![Configuração de exclusão](./media/exclusions-config-page.png)

Para remover de uma entidade da configuração **Exclusões**: clique no sinal de menos ao lado do nome da entidade e, em seguida, clique em **Salvar** na parte inferior da página.

É recomendável que você adicione exclusões para detecções somente depois de receber alertas do tipo e determinar que eles são positivos benignos verdadeiros. 

> [!NOTE]
> Para sua proteção, nem todas as detecções oferecem a possibilidade de configurar exclusões. 

Algumas das detecções fornecem dicas que ajudam você a decidir o que excluir. 

Cada exclusão depende do contexto, em alguns você pode definir os usuários enquanto em outros você pode configurar computadores ou endereços IP. 

Quando você tiver a possibilidade de exclusão de um endereço IP ou de um computador (você pode excluir um ou outro), você não precisará fornecer os dois.

> [!NOTE]
> As páginas de configuração podem ser modificadas apenas por administradores do ATA.


## <a name="see-also"></a>Consulte Também
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Modificando a configuração do ATA](modifying-ata-center-configuration.md)
