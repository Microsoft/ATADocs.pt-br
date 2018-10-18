---
title: Trabalhando com alertas de segurança na Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Descreve como examinar os alertas de segurança emitidos pelo Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: a06004bd-9f77-4e8e-a0e5-4727d6651a0f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 59bc8cdb995b1f7473efb7c0e601aca50a9ccafe
ms.sourcegitcommit: 58c75026e5ec4dcab3b0852a41f9f0a0ad6f22eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2018
ms.locfileid: "49315822"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*



# <a name="working-with-security-alerts"></a>Trabalhando com alertas de segurança
Este artigo explica noções básicas de como trabalhar com a Proteção Avançada contra Ameaças do Azure.

## Examine os alertas de segurança na linha do tempo do ataque <a name="review-suspicious-activities-on-the-attack-time-line"></a>
Após fazer logon no portal do Azure ATP, você será levado automaticamente à **Linha do tempo de alertas de segurança** aberta. Os alertas de segurança são listados em ordem cronológica com o alerta mais recente na parte superior da linha do tempo.
Cada alerta de segurança tem as seguintes informações:

-   Entidades envolvidas, incluindo usuários, computadores, servidores, controladores de domínio e recursos.

-   O horário e o período das atividades suspeitas que iniciaram o alerta de segurança.

-   Gravidade do alerta: alta, média ou baixa.

-   Status: aberto, fechado ou suprimido.

-   Capacidade de

    -   Compartilhe o alerta de segurança com outras pessoas da sua organização por email.

    -   Exporte o alerta de segurança para o Excel.

> [!NOTE]
> -   Quando você passa o mouse sobre um usuário ou computador, é exibido um perfil simplificado da entidade que fornece informações adicionais sobre a entidade e inclui o número de alertas de segurança vinculado à entidade.
> -   Se você clicar em uma entidade, ela levará você ao perfil de entidade de usuário ou computador.

![Imagem da linha do tempo de alertas de segurança do Azure ATP](media/atp-sa-timeline.png)

## Detecções de versão prévia<a name="preview-detections"></a>

A equipe de pesquisa da Azure ATP (Proteção Avançada contra Ameaças do Azure) trabalha constantemente para implementar novas detecções para ataques recém-descobertos. Já que a ATP do Azure é um serviço de nuvem, essas novas detecções são lançadas rapidamente para permitir que os clientes da ATP do Azure se beneficiem das novas detecções o mais breve possível.

Essas detecções são marcadas como uma notificação de versão prévia para ajudar a identificar as novas detecções e saber que elas são novas para o produto. Se você desabilitar as detecções de versão prévia, elas não serão exibidas no console da Azure ATP (nem na linha do tempo nem nos perfis de entidade) e novos alertas não serão abertos.

![VPN de detecção de versão prévia](./media/preview-detection-vpn.png) 

Por padrão, as detecções de versão prévia são habilitadas na Azure ATP. 

Para desabilitar as detecções de versão prévia:

1. No console da Azure ATP, clique no símbolo de engrenagem de configurações.
2. No menu à esquerda, em Versão prévia, clique em **Detecções**.
3. Use o controle deslizante para habilitar e desabilitar às detecções de versão prévia.
 
![detecções de versão prévia](./media/preview-detections.png) 


## <a name="filter-security-alerts-list"></a>Filtrar lista de alertas de segurança
Para filtrar lista de alertas de segurança:

1.  No painel **Filtrar por** no lado esquerdo da tela, selecione uma das seguintes opções: **Tudo**, **Aberto**, **Fechado** ou **Suprimido**.

2.  Para filtrar a lista ainda mais, selecione **Alta**, **Média** ou **Baixa**.

**Gravidade da atividade suspeita**

-   **Baixa**

    Indica atividades que podem levar a ataques projetados para usuários ou softwares mal-intencionados para obter acesso aos dados organizacionais.

-   **Média**

    Indica atividades que podem colocar identidades específicas em risco de ataques mais graves que podem resultar em roubo de identidade ou escalonamento privilegiado

-   **Alta**

    Indica as atividades que podem levar a roubo de identidade, elevação de privilégios ou outros ataques de alto impacto


## <a name="managing-security-alerts"></a>Gerenciando alertas de segurança
É possível alterar o status de um alerta de segurança clicando em seu status atual e selecionando uma das seguintes opções **Aberto**, **Suprimido**, **Fechado** ou **Excluído**.
Para fazer isso, clique nos três pontos no canto superior direito de um alerta específico para revelar a lista de ações disponíveis.

![Ações para alertas de segurança do Azure ATP](./media/atp-sa-actions.png)

**Status do alerta de segurança**

-   **Aberto**: todos os novos alertas de segurança são exibidos nessa lista.

-   **Fechado**: é usado para rastrear alertas de segurança que você identificou, pesquisou e corrigiu como mitigado.

    > [!NOTE]
    > Se a mesma atividade for detectada novamente em um curto período, o Azure ATP poderá reabrir um alerta fechado.

-   **Suprimir**: suprimir um alerta significa que você deseja ignorá-lo por enquanto e apenas ser alertado novamente se houver uma nova instância. Isso significa que, se houver um alerta semelhante, o Azure ATP não o reabrirá. Mas, se o alerta parar por sete dias e for observado novamente, você será alertado novamente.

- **Excluir**: se você excluir um alerta, ele será excluído do sistema, do banco de dados e você NÃO poderá restaurá-lo. Após clicar em Excluir, será possível excluir todos os alertas de segurança do mesmo tipo.

- **Excluir**: a capacidade de excluir uma entidade de gerar mais de um determinado tipo de alertas. Por exemplo, você pode configurar o Azure ATP para impedir que uma entidade (usuário ou computador) específica emita novamente um alerta para um determinado tipo de atividade, como um administrador específico que executa código remoto ou um verificador de segurança que faz o reconhecimento de DNS. Além de ser capaz de adicionar exclusões diretamente no alerta de segurança conforme ele é detectado na linha do tempo, também é possível acessar a página Configuração até **Exclusões** e para cada alerta de segurança, é possível adicionar e remover manualmente entidades ou sub-redes excluídas (por exemplo, para Pass-the-Ticket). 

> [!NOTE]
> As páginas de configuração podem ser modificadas apenas por administradores do Azure ATP.


## <a name="see-also"></a>Consulte Também

- [Trabalhando com o portal do Azure ATP](workspace-portal.md)
- [Confira o fórum do Azure ATP!](https://aka.ms/azureatpcommunity)