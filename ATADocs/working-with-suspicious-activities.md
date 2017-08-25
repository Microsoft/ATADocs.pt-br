---
title: Como trabalhar com atividades suspeitas no Advanced Threat Analytics | Microsoft Docs
description: Descreve como examinar atividades suspeitas identificadas pelo ATA
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/20/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 44d7c899-816c-4f7f-91d3-84a09d291a24
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: fcee6f1887e6842d1ccdfd2863620af8a5a8279f
ms.sourcegitcommit: 129bee06ff89b72d21b64f9aa0d1a29f66bf9153
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*



# <a name="working-with-suspicious-activities"></a>Trabalhando com atividades suspeitas
Este tópico explica as noções básicas de como trabalhar com a Advanced Threat Analytics.

## <a name="review-suspicious-activities-on-the-attack-time-line"></a>Examinar atividades suspeitas na linha do tempo de ataque
Depois de fazer logon no Console do ATA, você será direcionado automaticamente para a **linha do tempo de atividades suspeitas** aberta. As atividades suspeitas são listadas em ordem cronológica com as atividades suspeitas mais recentes na parte superior da linha do tempo.
Cada atividade suspeita tem as seguintes informações:

-   Entidades envolvidas, incluindo usuários, computadores, servidores, controladores de domínio e recursos.

-   Os tempos e o intervalo de tempo das atividades suspeitas.

-   A severidade da atividade suspeita: alta, média ou baixa.

-   Status: aberto, fechado ou suprimido.

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




## <a name="remediating-suspicious-activities"></a>Corrigindo atividades suspeitas
Você pode alterar o status de uma atividade suspeita clicando no status atual da atividade suspeita e selecionando uma das seguintes opções **Aberto**, **Suprimido**, **Fechado** ou **Excluído**.
Para fazer isso, clique nos três pontos no canto superior direito de uma atividade suspeita específica para exibir a lista de ações disponíveis.

![Ações do ATA para atividades suspeitas](./media/sa-actions.png)

**Status de atividade suspeita**

-   **Abrir**: todas as novas atividades suspeitas aparecem nesta lista.

-   **Fechar**: é usado para rastrear atividades suspeitas que você identificou, pesquisou e corrigiu como mitigado.

    > [!NOTE]
    > O ATA pode reabrir uma atividade resolvida se a mesma atividade for novamente detectada em um curto período de tempo.

-   **Suprimir**: suprimir uma atividade significa que você deseja ignorá-la por enquanto e apenas ser alertado novamente se houver uma nova instância. Isso significa que, se houver um alerta semelhante o ATA não reabrirá. Mas, se o alerta parar por sete dias e for observado novamente, você será alertado novamente.

- **Excluir**: se você excluir um alerta, ele será excluído do sistema, do banco de dados e você NÃO poderá restaurá-lo. Depois de clicar em Excluir, você poderá excluir todas as atividades suspeitas do mesmo tipo.

- **Excluir**: a capacidade de excluir uma entidade de gerar mais de um determinado tipo de alertas. Por exemplo, você pode definir o ATA para excluir uma entidade específica (usuário ou computador) de emitir um alerta novamente para um determinado tipo de atividade suspeita, como um administrador específico que executa o código remoto ou um scanner de segurança que o reconhecimento de DNS. Além de ser capaz de adicionar exclusões diretamente na atividade suspeita conforme ela é detectada na linha do tempo, você também pode acessar a página Configuração até **Exclusões** e para cada atividade suspeita, você pode adicionar e remover manualmente entidades ou sub-redes excluídas (por exemplo, para Passagem de Tíquete). 
> [!NOTE]
> As páginas de configuração podem ser modificadas apenas por administradores do ATA.


## <a name="related-videos"></a>Vídeos Relacionados
- [Participar da comunidade de segurança](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community)


## <a name="see-also"></a>Consulte também
- [Manual da atividade suspeita do ATA](http://aka.ms/ataplaybook)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Modificando a configuração do ATA](modifying-ata-center-configuration.md)
