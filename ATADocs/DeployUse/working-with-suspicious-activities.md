---
title: Como trabalhar com atividades suspeitas no Advanced Threat Analytics | Microsoft Docs
description: Descreve como examinar atividades suspeitas identificadas pelo ATA
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 44d7c899-816c-4f7f-91d3-84a09d291a24
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: c94f61853aa45d45600cbcc0ba0a5a64adc6fd3f


---

*Aplica-se a: Advanced Threat Analytics versão 1.7*



# <a name="working-with-suspicious-activities"></a>Trabalhando com atividades suspeitas
Este tópico explica as noções básicas de como trabalhar com a Advanced Threat Analytics.

## <a name="review-suspicious-activities-on-the-attack-time-line"></a>Examinar atividades suspeitas na linha do tempo de ataque
Depois de fazer logon no Console do ATA, você será direcionado automaticamente para a **linha do tempo de atividades suspeitas** aberta. As atividades suspeitas são listadas em ordem cronológica com as atividades suspeitas mais recentes na parte superior da linha do tempo.
Cada atividade suspeita tem as seguintes informações:

-   Entidades envolvidas, incluindo usuários, computadores, servidores, controladores de domínio e recursos.

-   Os tempos e o intervalo de tempo das atividades suspeitas.

-   A severidade da atividade suspeita: alta, média ou baixa.

-   Status: aberto, resolvido ou descartado.

-   Capacidade de

    -   Compartilhar a atividade suspeita com outras pessoas na organização por email.

    -   Exportar a atividade suspeita para o Excel.

    -   Adicionar uma anotação para a atividade suspeita.

    -   Fornecer comentários sobre a atividade suspeita.

-   Fornecer recomendações sobre como responder a atividades suspeitas.

> [!NOTE]
> -   Quando você passa o mouse sobre um usuário ou computador, é exibido um perfil simplificado da entidade que fornece informações adicionais sobre a entidade e inclui o número de atividades suspeitas vinculado à entidade.
> -   Se você clicar em uma entidade, ela levará você ao perfil de entidade de usuário ou computador.

![Imagem da linha do tempo das atividades suspeitas do ATA](media/ATA-Suspicious-Activity-Timeline.JPG)

## <a name="filter-suspicious-activities-list"></a>Filtrar lista de atividades suspeitas
Para filtrar a lista de atividades suspeitas:

1.  No painel **Filtrar por** no lado esquerdo da tela, selecione um dos seguintes: **Todos**, **Abrir**, **Resolvido** ou **Descartado**.

2.  Para filtrar a lista ainda mais, selecione **Alta**, **Média** ou **Baixa**.

**Gravidade da atividade suspeita**

-   **Baixa**

    Indica atividades suspeitas que podem levar a ataques projetados para usuários ou softwares mal-intencionados para obter acesso aos dados organizacionais.

-   **Média**

    Indica atividades suspeitas que podem colocar identidades específicas em risco de ataques mais graves que podem resultar em roubo de identidade ou escalonamento privilegiado

-   **Alta**

    Indica as atividades suspeitas que podem levar a roubo de identidade, elevação de privilégios ou outros ataques de alto impacto

**Status de atividade suspeita**

-   **Aberta**

    Todas as novas atividades suspeitas aparecem nesta lista

-   **Resolvida**

    É usado para rastrear atividades suspeitas que você identificou, pesquisou e estabeleceu como mitigado.

    > [!NOTE]
    > O ATA pode reabrir uma atividade resolvida se a mesma atividade for novamente detectada em um curto período de tempo.

-   **Ignorada**

    São atividades que você descartou manualmente. Se o ATA detectar uma atividade suspeita semelhante, será criada uma nova detecção.

## <a name="provide-input-on-a-suspicious-activity"></a>Fornecer comentários sobre uma atividade suspeita
Para permitir que o ATA saiba mais sobre a sua rede com você, algumas atividades suspeitas (reconhecimento de DNS, passagem de tíquete, enumeração de sessão SMB, comportamento anormal e execução remota) solicitam informações suas para melhorar a detecção de atividades suspeitas no futuro.

1.  Para atividades suspeitas que permitem a você fornecer informações, a pergunta de entrada é aberta automaticamente. Você será solicitado a responder perguntas sobre as atividades em sua rede e se elas devem ser consideradas suspeitas. No exemplo abaixo, você deve responder se é permitido executar ferramentas de verificação em um computador específico.

    ![O ATA fornece informações para uma imagem de atividades suspeitas](media/ATA-Input.JPG)

2.  Se você responder não, essa atividade será considerada suspeita e sempre que o ATA encontrar essa atividade no computador, você será alertado.

3.  No entanto, se você responder sim, a atividade suspeita poderá ser descartada e as atividades futuras deste tipo no computador não poderão gerar uma atividade suspeita ou vão gerar uma atividade que será automaticamente descartada.

4.  Se você não souber, você pode clicar em **Cancelar**.

## <a name="change-the-status-of-a-suspicious-activity"></a>Alterar o status de uma atividade suspeita
Você pode alterar o status de uma atividade suspeita clicando no status atual da atividade suspeita e selecionando **Abrir**, **Resolvido** ou **Descartado**.

## <a name="see-also"></a>Consulte também
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Trabalhando com as configurações de detecção do ATA](working-with-detection-settings.md)
- [Modificando a configuração do ATA](modifying-ata-configuration.md)



<!--HONumber=Feb17_HO1-->


