---
title: Excluindo entidades de detecções na Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Descreve como impedir que o Azure ATP detecte atividades de entidades específicas como suspeitas
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/2/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: cae3ed45-8fbc-4f25-ba24-3cc407c6ea93
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2a91ebbe3811aeefe6fcef660807976794513f32
ms.sourcegitcommit: 14c05a210ae92d35100c984ff8c6d171db7c3856
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39567824"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*



# <a name="excluding-entities-from-detections"></a>Excluindo entidades de detecções
Este artigo explica como excluir entidades de disparar alertas para minimizar verdadeiros positivos benignos mas ao mesmo tempo, capturar os verdadeiros positivos. Para impedir que o Azure ATP seja ruidoso quando atividades que, vindas de usuários específicos, podem fazer parte de seu ritmo normal de negócios, você pode silenciar ou excluir entidades específicas da geração de alertas.

Por exemplo, se você tiver um verificador de segurança que realiza reconhecimento DNS ou um administrador que executa scripts remotamente no controlador de domínio, essas serão atividades sancionadas cujo objetivo é parte das operações de TI normais em sua organização. Para obter mais informações sobre as detecções do Azure ATP para ajudá-lo a decidir quais entidades excluir, consulte o [Guia atividades suspeitas](suspicious-activity-guide.md).

Para excluir entidades da geração de alertas no Azure ATP:

Há duas maneiras em que você pode excluir entidades, na atividade suspeita em si ou no guia **Exclusões** na página **Configuração**.

- **Na atividade suspeita**: na linha do tempo de atividades suspeitas, quando você receber um alerta em uma atividade para um usuário ou computador ou endereço IP que tem permissão para executar uma atividade específica e pode realizá-lo com frequência, clique com botão direito do mouse nos três pontos no final da linha da atividade suspeita nessa entidade e selecione **Fechar e excluir**. <br></br>Isso adiciona o usuário, computador ou endereço IP à lista de exclusões da atividade suspeita. Isso fecha a atividade suspeita, e ela não aparece mais na lista de eventos **Abrir** na **Linha do tempo de atividade suspeita**.

    ![Excluir entidades](./media/exclude-in-sa.png)

- **Na página Configuração**: para examinar ou modificar exclusões: em **Configuração**, clique em **Exclusões** e, em seguida, selecione a atividade suspeita, como **Reconhecimento de DNS**.

    ![Configuração de exclusão](./media/exclusions.png)

Para adicionar uma entidade à configuração de **Exclusões**: insira o nome da entidade, clique no sinal de mais e, em seguida, clique em **Salvar** na parte inferior da página.

Para remover de uma entidade da configuração **Exclusões**: clique no sinal de menos ao lado do nome da entidade e, em seguida, clique em **Salvar** na parte inferior da página.

É recomendável que você adicione exclusões para detecções somente depois de receber alertas do tipo e determinar que eles são positivos benignos verdadeiros. 

> [!NOTE]
> Para sua proteção, nem todas as detecções oferecem a possibilidade de configurar exclusões. 

Algumas das detecções fornecem dicas que ajudam você a decidir o que excluir. 

Cada exclusão depende do contexto, em alguns você pode definir os usuários enquanto em outros você pode configurar computadores ou endereços IP. 

Quando você tiver a possibilidade de exclusão de um endereço IP ou de um computador (você pode excluir um ou outro), você não precisará fornecer os dois.

> [!NOTE]
> As páginas de configuração podem ser modificadas apenas por administradores do Azure ATP.


## <a name="see-also"></a>Consulte Também

- [Integrando com o Windows Defender ATP](integrate-wd-atp.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)