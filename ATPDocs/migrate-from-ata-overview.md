---
title: Análise avançada de ameaças ao Microsoft defender para movimentação de identidade
description: Saiba como mover uma instalação existente do Advanced Threat Analytics para o Microsoft defender para identidade.
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
ms.openlocfilehash: 032a5f289657485b744ad335dc51777a8ba72602
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93275043"
---
# <a name="advanced-threat-analytics-ata-to-product-long"></a>ATA (Advanced Threat Analytics) para [!INCLUDE [Product long](includes/product-long.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

> [!NOTE]
> A versão final do ATA está [disponível para o público geral](https://support.microsoft.com/help/4568997/update-3-for-microsoft-advanced-threat-analytics-1-9). O ATA terminará o suporte base em 12 de janeiro de 2021. O suporte estendido continuará até janeiro de 2026. Para obter mais informações, leia [nosso blog](https://techcommunity.microsoft.com/t5/microsoft-security-and/end-of-mainstream-support-for-advanced-threat-analytics-january/ba-p/1539181).

Use este guia para mover de uma instalação existente do ATA para o [!INCLUDE [Product long](includes/product-long.md)] serviço do (). O guia explica os [!INCLUDE [Product short](includes/product-short.md)] pré-requisitos e requisitos e detalha como planejar e concluir sua movimentação. As etapas e dicas de validação para aproveitar as mais recentes soluções de proteção contra ameaças e segurança com o [!INCLUDE [Product short](includes/product-short.md)] após a instalação também estão incluídas.

Para saber mais sobre as diferenças entre o ATA e [!INCLUDE [Product short](includes/product-short.md)] o, consulte as [ [!INCLUDE [Product short](includes/product-short.md)] perguntas](technical-faq.md#what-is-azure-atp)frequentes.

Neste guia, você:

> [!div class="checklist"]
>
> - Examinar e confirmar os [!INCLUDE [Product short](includes/product-short.md)] pré-requisitos de serviço
> - Documentará sua configuração do ATA existente
> - Planejará sua migração
> - Configurar e configurar seu [!INCLUDE [Product short](includes/product-short.md)]  serviço
> - Executará verificações pós-migração
> - Desprogramará o ATA após a conclusão da migração

> [!NOTE]
> A mudança para o [!INCLUDE [Product short](includes/product-short.md)] do ATA é possível de qualquer versão do ATA. No entanto, como os dados não podem ser movidos do ATA para [!INCLUDE [Product short](includes/product-short.md)] o, é recomendável manter os dados do centro do ATA e os alertas necessários para investigações contínuas até que todos os alertas do ATA sejam fechados ou corrigidos.

## <a name="prerequisites"></a>Pré-requisitos

- Um locatário Azure Active Directory com pelo menos um administrador global/de segurança é necessário para criar uma [!INCLUDE [Product short](includes/product-short.md)] instância. Cada [!INCLUDE [Product short](includes/product-short.md)] instância dá suporte a vários Active Directory limites de floresta e FFL (nível funcional de floresta) do Windows 2003 e superior.

- [!INCLUDE [Product short](includes/product-short.md)] requer o .NET Framework 4,7 ou posterior e pode exigir um controlador de domínio (reiniciar) se a versão atual do .NET Framework não for 4,7 ou posterior.

- Verifique se os controladores de domínio atendem a todos os [ [!INCLUDE [Product short](includes/product-short.md)] requisitos do sensor](prerequisites.md#azure-atp-sensor-requirements) e se o seu ambiente atende a todos os [ [!INCLUDE [Product short](includes/product-short.md)] requisitos](prerequisites.md).

- Valide se todos os controladores de domínio que você planeja usar têm acesso suficiente à Internet para o [!INCLUDE [Product short](includes/product-short.md)] serviço. Verifique e confirme se os controladores de domínio atendem aos [ [!INCLUDE [Product short](includes/product-short.md)] requisitos de configuração de proxy](configure-proxy.md).

> [!NOTE]
> Este guia de migração foi projetado [!INCLUDE [Product short](includes/product-short.md)] apenas para sensores.

## <a name="plan"></a>Plano

Reúna as informações a seguir antes de começar a migração:

1. Detalhes de conta da sua conta dos [Serviços de Diretório](install-step2.md).
1. [Configurações](setting-syslog.md) de notificação do Syslog.
1. [Detalhes de notificação](notifications.md) por email.
1. Associação ao grupo de funções do ATA
1. Integração de VPN
1. Exclusões de alertas
    - As exclusões não são transferidas do ATA para o [!INCLUDE [Product short](includes/product-short.md)] , de modo que os detalhes de cada exclusão são necessários para [replicar as exclusões no [!INCLUDE [Product short](includes/product-short.md)] ](excluding-entities-from-detections.md).
1. Detalhes de conta para contas HoneyToken.
    - Se você ainda não tiver contas dedicadas do HoneyToken, saiba mais sobre o [HoneyTokens no [!INCLUDE [Product short](includes/product-short.md)] ](install-step7.md) e crie novas contas para usar com essa finalidade.
1. Lista completa de todas as entidades (computadores, grupos, usuários) que você deseja marcar manualmente como entidades confidenciais.
    - Saiba mais sobre a importância de [entidades confidenciais](sensitive-accounts.md) no [!INCLUDE [Product short](includes/product-short.md)] .
1. [Detalhes](reports.md) do agendamento de relatórios (lista de relatórios e tempo agendado).

> [!NOTE]
> Não desinstale o Centro de ATA até que todos os Gateways do ATA sejam removidos. Desinstalar o Centro de ATA com Gateways de ATA ainda em execução deixa sua organização exposta sem nenhuma proteção contra ameaças.

## <a name="move"></a>Mover

Conclua a mudança para [!INCLUDE [Product short](includes/product-short.md)] em duas etapas fáceis:

### <a name="step-1-create-and-install-product-short-instance-and-sensors"></a>Etapa 1: criar e instalar [!INCLUDE [Product short](includes/product-short.md)] instância e sensores

1. [Criar sua nova [!INCLUDE [Product short](includes/product-short.md)] instância](install-step1.md)

1. Desinstale o Gateway Lightweight do ATA em todos os controladores de domínio.

1. Instale o [!INCLUDE [Product short](includes/product-short.md)] sensor em todos os controladores de domínio:
    - [Baixe os [!INCLUDE [Product short](includes/product-short.md)] arquivos do sensor](install-step3.md).
    - [Recuperar seu [!INCLUDE [Product short](includes/product-short.md)] Chave de acesso](install-step3.md#download-the-setup-package).
    - [Instale [!INCLUDE [Product short](includes/product-short.md)] os sensores em seus controladores de domínio](install-step4.md).

### <a name="step-2-configure-and-validate-product-short-instance"></a>Etapa 2: configurar e validar a [!INCLUDE [Product short](includes/product-short.md)] instância

- [Configurar o sensor](install-step5.md)

> [!NOTE]
> Determinadas tarefas na lista a seguir não podem ser concluídas antes de instalar [!INCLUDE [Product short](includes/product-short.md)] sensores e, em seguida, concluir uma sincronização inicial, como selecionar entidades para marcação **confidencial** manual. Espere até 2 horas para a conclusão da sincronização inicial.

#### <a name="configuration"></a>Configuração

Entre no [!INCLUDE [Product short](includes/product-short.md)] portal e conclua as tarefas de configuração a seguir.

| Etapa    | Ação | Status |
|--------------|------------|------------------|
| 1  | Definir [atualizações atrasadas em uma seleção de controladores de domínio](sensor-update.md) | - [ ] |
| 2  | Detalhes de conta dos [Serviços de Diretório](install-step2.md)| - [ ] |
| 3  | Configurar [notificações do Syslog](setting-syslog.md) | - [ ] |
| 4  | Informações sobre [Integrar VPN](install-step6-vpn.md)| - [ ] |
| 5  | Configurar a [integração do WDATP](integrate-mde.md)| - [ ] |
| 6  | Definir contas [HoneyTokens](install-step7.md)| - [ ] |
| 7  | Marcar [Entidades confidenciais](sensitive-accounts.md)| - [ ] |
| 8  | Criar [exclusões de alerta de segurança](excluding-entities-from-detections.md)| - [ ] |
| 9 | [Alternâncias de notificação por email](notifications.md) | - [ ] |
| 10  | [Configurações do relatório de agendamento](reports.md) (lista de relatórios e tempo agendado)| - [ ] |
| 11  | Configurar [permissões baseadas em funções](role-groups.md) | - [ ] |
| 12  | [Configuração de notificação de SIEM (endereço IP)](configure-event-collection.md#siemsyslog)| - [ ] |

#### <a name="validation"></a>Validação

No [!INCLUDE [Product short](includes/product-short.md)] Portal:

- Examine os [alertas de integridade](health-center.md) em busca de sinais de problemas de serviço.
- Examine [!INCLUDE [Product short](includes/product-short.md)] [os logs de erros do sensor](troubleshooting-using-logs.md) para verificar se há erros incomuns.

## <a name="after-the-move"></a>Após a migração

Esta seção do guia explica as ações que podem ser executadas após a conclusão da migração.

> [!NOTE]
> Não há suporte para a importação de alertas de segurança existentes do ATA para o [!INCLUDE [Product short](includes/product-short.md)] . Registre ou corrija todos os alertas do ATA existentes antes de desativar o Centro de ATA.

- **Desativar o Centro de ATA**  
  - Para fazer referência aos dados do Centro de ATA após a migração, é recomendável manter os dados do centro online durante um período de tempo. Após desativar o Centro de ATA, o número de recursos normalmente poderá ser reduzido, principalmente se os recursos forem uma Máquina Virtual.

- **Fazer backup do Mongo DB**  
  - Se desejar manter os dados do ATA por tempo indeterminado, [faça backup do Mongo DB](/advanced-threat-analytics/ata-database-management#backing-up-the-ata-database).

## <a name="mission-accomplished"></a>Missão cumprida

Parabéns! A mudança do ATA para o [!INCLUDE [Product short](includes/product-short.md)] foi concluída.

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre [[!INCLUDE [Product short](includes/product-short.md)]](what-is.md) recursos, funcionalidade e [alertas de segurança](understanding-security-alerts.md).

## <a name="join-the-community"></a>Participe da comunidade

Você tem mais perguntas ou um interesse em discutir [!INCLUDE [Product short](includes/product-short.md)] e segurança relacionada com outras pessoas? Junte-se à [ [!INCLUDE [Product short](includes/product-short.md)] comunidade](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) hoje mesmo!
