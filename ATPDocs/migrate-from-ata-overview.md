---
title: Migração do Advanced Threat Analytics para a Proteção Avançada contra Ameaças do Azure
description: Saiba como migrar uma instalação existente do Advanced Threat Analytics para a ATP do Azure.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/21/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: e734e382-c4b1-43ca-9a8d-96c91daf2578
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e959e6c0134cf23355b7c1bc89c7e35166230fb9
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912186"
---
# <a name="advanced-threat-analytics-ata-to-azure-advanced-threat-protection-azure-atp"></a>ATA (Advanced Threat Analytics) para o ATP do Azure (Proteção Avançada contra Ameaças do Azure)

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

> [!NOTE]
> A versão final do ATA está [disponível para o público geral](https://support.microsoft.com/help/4568997/update-3-for-microsoft-advanced-threat-analytics-1-9). O ATA terminará o suporte base em 12 de janeiro de 2021. O suporte estendido continuará até janeiro de 2026. Para obter mais informações, leia [nosso blog](https://techcommunity.microsoft.com/t5/microsoft-security-and/end-of-mainstream-support-for-advanced-threat-analytics-january/ba-p/1539181).

Use este guia para migrar de uma instalação do ATA existente para o serviço do ATP do Azure (Proteção Avançada contra Ameaças do Azure). O guia explica os pré-requisitos e os requisitos do ATP do Azure e detalha como planejar e concluir sua migração. Também estão incluídas etapas e dicas de validação para usar a proteção contra ameaças e as soluções de segurança mais recentes com o ATP do Azure após a instalação.

Saiba mais sobre as diferenças entre o ATA e o ATP do Azure nas [perguntas frequentes sobre o ATP do Azure](technical-faq.md#what-is-azure-atp).

Neste guia, você:

> [!div class="checklist"]
>
> - Examinará e confirmará os pré-requisitos do serviço do ATP do Azure
> - Documentará sua configuração do ATA existente
> - Planejará sua migração
> - Instalará e configurará o serviço do ATP do Azure
> - Executará verificações pós-migração
> - Desprogramará o ATA após a conclusão da migração

> [!NOTE]
> Migrar do ATA para o ATP do Azure é possível em qualquer versão do ATA. No entanto, como os dados não podem ser movidos do ATA para o ATP do Azure, é recomendável reter o data center e os alertas do ATA necessários para investigações contínuas até que os alertas do ATA sejam fechados ou corrigidos.

## <a name="prerequisites"></a>Pré-requisitos

- Um locatário do Azure Active Directory com pelo menos um administrador global/de segurança é necessário para criar uma instância do ATP do Azure. Cada instância do Azure ATP dá suporte a vários limites de floresta do Active Directory e dá suporte ao FFL (Nível funcional da floresta) do Windows 2003 e posteriores.

- O ATP do Azure exigirá o .NET Framework 4.7 ou posterior e poderá requerer um controlador de domínio (reinício) se sua versão atual do .NET Framework não for a 4.7 ou posterior.

- Verifique se seus controladores de domínio atendem a todos os [requisitos de sensor do ATP do Azure](prerequisites.md#azure-atp-sensor-requirements) e seu ambiente atende a todos os [requisitos do ATP do Azure](prerequisites.md).

- Valide que todos os controladores de domínio que você planeja usar têm acesso suficiente à Internet para o serviço ATP do Azure. Verifique e confirme que seus controladores de domínio atendem aos [requisitos de configuração de proxy do ATP do Azure](configure-proxy.md).

> [!NOTE]
> Este guia de migração foi criado somente para sensores do ATP do Azure.

## <a name="plan"></a>Plano

Reúna as informações a seguir antes de começar a migração:

1. Detalhes de conta da sua conta dos [Serviços de Diretório](install-step2.md).
1. [Configurações](setting-syslog.md) de notificação do Syslog.
1. [Detalhes de notificação](notifications.md) por email.
1. Associação ao grupo de funções do ATA
1. Integração de VPN
1. Exclusões de alertas
    - As exclusões não podem ser transferíveis do ATA para o ATP do Azure, portanto, os detalhes de cada exclusão são necessários para [replicar as exclusões no ATP do Azure](excluding-entities-from-detections.md).
1. Detalhes de conta para contas HoneyToken.
    - Se você ainda não tiver contas HoneyToken dedicadas, saiba mais sobre [HoneyTokens no ATP do Azure](install-step7.md) e crie contas a serem usadas para essa finalidade.
1. Lista completa de todas as entidades (computadores, grupos, usuários) que você deseja marcar manualmente como entidades confidenciais.
    - Saiba mais sobre a importância das [Entidades confidenciais](sensitive-accounts.md) no ATP do Azure.
1. [Detalhes](reports.md) do agendamento de relatórios (lista de relatórios e tempo agendado).

> [!NOTE]
> Não desinstale o Centro de ATA até que todos os Gateways do ATA sejam removidos. Desinstalar o Centro de ATA com Gateways de ATA ainda em execução deixa sua organização exposta sem nenhuma proteção contra ameaças.

## <a name="move"></a>Mover

Conclua sua migração para o ATP do Azure em duas etapas simples:

### <a name="step-1-create-and-install-azure-atp-instance-and-sensors"></a>Etapa 1: Criar e instalar a instância e sensores do ATP do Azure

1. [Criar sua instância do ATP do Azure](install-step1.md)

1. Desinstale o Gateway Lightweight do ATA em todos os controladores de domínio.

1. Instale o sensor do ATP do Azure em todos os controladores de domínio:
    - [Baixe arquivos de sensor do ATP do Azure](install-step3.md).
    - [Recupere sua chave de acesso do ATP do Azure](install-step3.md#download-the-setup-package).
    - [Instale os sensores do ATP do Azure em seus controladores de domínio](install-step4.md).

### <a name="step-2-configure-and-validate-azure-atp-instance"></a>Etapa 2: Configurar e validar instância do ATP do Azure

- [Configurar o sensor](install-step5.md)

> [!NOTE]
> Determinadas tarefas na lista a seguir não podem ser concluídas antes de instalar sensores do ATP do Azure e de concluir uma sincronização inicial, como selecionar entidades para marcação **Confidencial** manual. Espere até 2 horas para a conclusão da sincronização inicial.

#### <a name="configuration"></a>Configuração

Entre no portal do ATP do Azure e conclua as tarefas de configuração a seguir.

| Etapa    | Ação | Status |
|--------------|------------|------------------|
| 1  | Definir [atualizações atrasadas em uma seleção de controladores de domínio](sensor-update.md) | - [ ] |
| 2  | Detalhes de conta dos [Serviços de Diretório](install-step2.md)| - [ ] |
| 3  | Configurar [notificações do Syslog](setting-syslog.md) | - [ ] |
| 4  | Informações sobre [Integrar VPN](install-step6-vpn.md)| - [ ] |
| 5  | Configurar a [integração do WDATP](integrate-msde.md)| - [ ] |
| 6  | Definir contas [HoneyTokens](install-step7.md)| - [ ] |
| 7  | Marcar [Entidades confidenciais](sensitive-accounts.md)| - [ ] |
| 8  | Criar [exclusões de alerta de segurança](excluding-entities-from-detections.md)| - [ ] |
| 9 | [Alternâncias de notificação por email](notifications.md) | - [ ] |
| 10  | [Configurações do relatório de agendamento](reports.md) (lista de relatórios e tempo agendado)| - [ ] |
| 11  | Configurar [permissões baseadas em funções](role-groups.md) | - [ ] |
| 12  | [Configuração de notificação de SIEM (endereço IP)](configure-event-collection.md#siemsyslog)| - [ ] |

#### <a name="validation"></a>Validação

No portal do ATP do Azure:

- Examine os [alertas de integridade](health-center.md) em busca de sinais de problemas de serviço.
- Examine os [logs de erros do sensor](troubleshooting-using-logs.md) do ATP do Azure quanto a erros incomuns.

## <a name="after-the-move"></a>Após a migração

Esta seção do guia explica as ações que podem ser executadas após a conclusão da migração.

> [!NOTE]
> Não há suporte à importação de alertas de segurança existentes do ATA para o ATP. Registre ou corrija todos os alertas do ATA existentes antes de desativar o Centro de ATA.

- **Desativar o Centro de ATA**  
  - Para fazer referência aos dados do Centro de ATA após a migração, é recomendável manter os dados do centro online durante um período de tempo. Após desativar o Centro de ATA, o número de recursos normalmente poderá ser reduzido, principalmente se os recursos forem uma Máquina Virtual.

- **Fazer backup do Mongo DB**  
  - Se desejar manter os dados do ATA por tempo indeterminado, [faça backup do Mongo DB](/advanced-threat-analytics/ata-database-management#backing-up-the-ata-database).

## <a name="mission-accomplished"></a>Missão cumprida

Parabéns! Sua migração do ATA para o ATP do Azure foi concluída.

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre os recursos, a funcionalidade e os [alertas de segurança](what-is.md) do [ATP do Azure](understanding-security-alerts.md).

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o ATP do Azure e a segurança relacionada com outras pessoas? Participe da [Comunidade do ATP do Azure](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) hoje mesmo!