---
title: "Excluindo entidades de detecção no Advanced Threat Analytics | Microsoft Docs"
description: "Descreve como impedir que o ATA detecte atividades de entidade específicas como suspeitas"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/9/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 344c0f33-45e1-42e2-a051-f722a4504531
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ff60b026c754a27da62c01ce6c551d206338ef4e
ms.sourcegitcommit: be6bdfa24a9b25a3375a4768d513b93900b3a498
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*



# <a name="excluding-entities-from-detections"></a>Excluindo entidades de detecções
Este tópico explica como excluir entidades de disparar alertas para minimizar verdadeiros positivos benignos mas ao mesmo tempo, capturar os verdadeiros positivos. Para impedir que o ATA seja desnecessariamente ruidoso sobre as atividades que, de usuários específicos, podem ser parte de seu ritmo normal de negócios, você pode silenciar ou excluir entidades específicas da geração de alertas.

Por exemplo, se você tiver um verificador de segurança que realiza reconhecimento DNS ou um administrador que executa scripts remotamente no controlador de domínio, essas serão atividades sancionadas cujo objetivo é parte das operações de TI normais em sua organização.

Para excluir entidades da geração de alertas no ATA:

Há duas maneiras em que você pode excluir entidades, na atividade suspeita em si ou no guia **Exclusões** na página **Configuração**.

- **Na atividade suspeita**: na linha do tempo de atividade suspeita, quando você receber um alerta em uma atividade para um usuário ou computador ou endereço IP que tem permissão para executar uma atividade específica e pode realizá-lo com frequência, clique com botão direito do mouse nos três pontos no final da linha da atividade suspeita nessa entidade e selecione **Fechar e excluir**. <br></br>Isso adicionará o usuário, computador ou endereço IP à lista de exclusões da atividade suspeita. Isso também fechará a atividade suspeita e ele não será listado na lista de eventos **Abrir** na **Linha do tempo de atividade suspeita**.

    ![Excluir entidades](./media/exclude-in-sa.png)

- **Na página Configuração**: para examinar ou modificar qualquer exclusão configurada: em **Configuração** clique em **Exclusões** e, em seguida, selecione a atividade suspeita, como **Credenciais de conta confidencial expostas**.

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
