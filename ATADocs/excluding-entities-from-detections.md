---
title: Excluindo entidades de detecção no Advanced Threat Analytics | Microsoft Docs
description: Descreve como impedir que o ATA detecte atividades de entidade específicas como suspeitas
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 344c0f33-45e1-42e2-a051-f722a4504531
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 51f733fc3d27453c07af7c169ced0db3bc38a8e4
ms.sourcegitcommit: 62b631f64a639f5df04bf805755f26c69b40e8e4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638891"
---
# <a name="excluding-entities-from-detections"></a>Excluindo entidades de detecções

*Aplica-se a: Advanced Threat Analytics versão 1.9*

Este artigo explica como excluir entidades de disparar alertas para minimizar verdadeiros positivos benignos mas ao mesmo tempo, capturar os verdadeiros positivos. Para impedir que o ATA seja ruidoso sobre as atividades que, de usuários específicos, podem ser parte de seu ritmo normal de negócios, você pode silenciar ou excluir entidades específicas da geração de alertas.

Por exemplo, se você tiver um verificador de segurança que realiza reconhecimento DNS ou um administrador que executa scripts remotamente no controlador de domínio, essas serão atividades sancionadas cujo objetivo é parte das operações de TI normais em sua organização.

Para excluir entidades da geração de alertas no ATA:

Há duas maneiras em que você pode excluir entidades, na atividade suspeita em si ou no guia **Exclusões** na página **Configuração**.

- **Na atividade suspeita**: na linha do tempo de atividade suspeita, quando você receber um alerta em uma atividade para um usuário ou computador ou endereço IP que tem permissão para executar uma atividade específica e pode realizá-lo com frequência, clique com botão direito do mouse nos três pontos no final da linha da atividade suspeita nessa entidade e selecione **Fechar e excluir**. <br></br>Isso adiciona o usuário, computador ou endereço IP à lista de exclusões da atividade suspeita. Isso fecha a atividade suspeita e ele não é listado na lista de eventos **Abrir** na **Linha do tempo de atividade suspeita**.

    ![Excluir entidades](./media/exclude-in-sa.png)

- **Na página Configuração**:  para examinar ou modificar qualquer exclusão: em **Configuração** clique em **Exclusões** e, em seguida, selecione a atividade suspeita, como **Credenciais de conta confidencial expostas**.

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
