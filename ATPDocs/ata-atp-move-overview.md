---
title: Migração do Advanced Threat Analytics para a Proteção Avançada contra Ameaças do Azure
description: Saiba como migrar uma instalação existente do Advanced Threat Analytics para a ATP do Azure.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 10/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: e734e382-c4b1-43ca-9a8d-96c91daf2578
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4a26195a6ceba0a32e9cf2d698574ca0acc7ef15
ms.sourcegitcommit: 93baa30e7f9f3b0e6a3ffcd2b9a25bc349798781
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/18/2020
ms.locfileid: "79504202"
---
# <a name="advanced-threat-analytics-ata-to-azure-advanced-threat-protection-azure-atp"></a>ATA (Advanced Threat Analytics) para o ATP do Azure (Proteção Avançada contra Ameaças do Azure)

Use este guia para migrar de uma instalação do ATA existente para o serviço do ATP do Azure (Proteção Avançada contra Ameaças do Azure). O guia explica os pré-requisitos e os requisitos do ATP do Azure e detalha como planejar e concluir sua migração. Também estão incluídas etapas e dicas de validação para usar a proteção contra ameaças e as soluções de segurança mais recentes com o ATP do Azure após a instalação.

Saiba mais sobre as diferenças entre o ATA e o ATP do Azure nas [perguntas frequentes sobre o ATP do Azure](https://docs.microsoft.com/azure-advanced-threat-protection/atp-technical-faq#what-is-azure-atp).

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

- O ATP do Azure requererá o .Net Framework 4.7 e poderá requerer um controlador de domínio (reinício) se sua versão atual do .Net Framework não for a 4.7.

- Verifique se seus controladores de domínio atendem a todos os [requisitos de sensor do ATP do Azure](https://docs.microsoft.com/azure-advanced-threat-protection/atp-prerequisites#azure-atp-sensor-requirements) e seu ambiente atende a todos os [requisitos do ATP do Azure](https://docs.microsoft.com/azure-advanced-threat-protection/atp-prerequisites).

- Valide que todos os controladores de domínio que você planeja usar têm acesso suficiente à Internet para o serviço ATP do Azure. Verifique e confirme que seus controladores de domínio atendem aos [requisitos de configuração de proxy do ATP do Azure](https://docs.microsoft.com/azure-advanced-threat-protection/configure-proxy).

> [!NOTE]
> Este guia de migração foi criado somente para sensores do ATP do Azure. Para saber mais, confira [escolher o sensor certo para sua implantação](https://docs.microsoft.com/azure-advanced-threat-protection/atp-capacity-planning#choosing-the-right-sensor-type-for-your-deployment).

## <a name="plan"></a>Plano

Reúna as informações a seguir antes de começar a migração:

1. Detalhes de conta da sua conta dos [Serviços de Diretório](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step2).
1. [Configurações](https://docs.microsoft.com/azure-advanced-threat-protection/setting-syslog) de notificação do Syslog.
1. [Detalhes de notificação](https://docs.microsoft.com/azure-advanced-threat-protection/notifications) por email.
1. Associação ao grupo de funções do ATA
1. Integração de VPN
1. Exclusões de alertas
    - As exclusões não podem ser transferíveis do ATA para o ATP do Azure, portanto, os detalhes de cada exclusão são necessários para [replicar as exclusões no ATP do Azure](https://docs.microsoft.com/azure-advanced-threat-protection/excluding-entities-from-detections).
1. Detalhes de conta para contas HoneyToken.
    - Se você ainda não tiver contas HoneyToken dedicadas, saiba mais sobre [HoneyTokens no ATP do Azure](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step7) e crie contas a serem usadas para essa finalidade.
1. Lista completa de todas as entidades (computadores, grupos, usuários) que você deseja marcar manualmente como entidades confidenciais.
    - Saiba mais sobre a importância das [Entidades confidenciais](https://docs.microsoft.com/azure-advanced-threat-protection/sensitive-accounts) no ATP do Azure.
1. [Detalhes](https://docs.microsoft.com/azure-advanced-threat-protection/reports) do agendamento de relatórios (lista de relatórios e tempo agendado).
1. Identificação e detalhes de cada Gateway Lightweight do ATA que é um candidato a Sincronizador de Domínio do ATP do Azure.
    - Saiba mais sobre a importância de [candidatos a Sincronizador de Domínio](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step5#configure-sensor-settings) no ATP do Azure.

> [!NOTE]
> Não desinstale o Centro de ATA até que todos os Gateways do ATA sejam removidos. Desinstalar o Centro de ATA com Gateways de ATA ainda em execução deixa sua organização exposta sem nenhuma proteção contra ameaças.

## <a name="move"></a>Mover

Conclua sua migração para o ATP do Azure em duas etapas simples:

### <a name="step-1-create-and-install-azure-atp-instance-and-sensors"></a>Etapa 1: Criar e instalar a instância e sensores do ATP do Azure

1. [Criar sua instância do ATP do Azure](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step1)

2. Desinstale o Gateway Lightweight do ATA em todos os controladores de domínio.

3. Instale o sensor do ATP do Azure em todos os controladores de domínio:
    - [Baixe arquivos de sensor do ATP do Azure](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step3).
    - [Recupere sua chave de acesso do ATP do Azure](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step3#download-the-setup-package).
    - [Instale os sensores do ATP do Azure em seus controladores de domínio](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step4).

### <a name="step-2-configure-and-validate-azure-atp-instance"></a>Etapa 2: Configurar e validar instância do ATP do Azure

- [Configurar o sensor](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step5)

> [!NOTE]
> Determinadas tarefas na lista a seguir não podem ser concluídas antes de instalar sensores do ATP do Azure e de concluir uma sincronização inicial, como selecionar entidades para marcação **Confidencial** manual. Espere até 2 horas para a conclusão da sincronização inicial.

#### <a name="configuration"></a>Configuração

Entre no portal do ATP do Azure e conclua as tarefas de configuração a seguir.

| Etapa    | Ação | Status |
|--------------|------------|------------------|
| 1  | Definir [atualizações atrasadas em uma seleção de controladores de domínio](https://docs.microsoft.com/azure-advanced-threat-protection/sensor-update) | - [ ] |
| 2  | Detalhes de conta dos [Serviços de Diretório](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step2)| - [ ] |
| 3  | Configurar [candidatos a Sincronizador de Domínio](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step5#configure-sensor-settings) | - [ ] |
| 4  | Configurar [notificações do Syslog](https://docs.microsoft.com/azure-advanced-threat-protection/setting-syslog) | - [ ] |
| 5  | Informações sobre [Integrar VPN](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step6-vpn)| - [ ] |
| 6  | Configurar a [integração do WDATP](https://docs.microsoft.com/azure-advanced-threat-protection/integrate-wd-atp)| - [ ] |
| 7  | Definir contas [HoneyTokens](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step7)| - [ ] |
| 8  | Marcar [Entidades confidenciais](https://docs.microsoft.com/azure-advanced-threat-protection/sensitive-accounts)| - [ ] |
| 9  | Criar [exclusões de alerta de segurança](https://docs.microsoft.com/azure-advanced-threat-protection/excluding-entities-from-detections)| - [ ] |
| 10 | [Alternâncias de notificação por email](https://docs.microsoft.com/azure-advanced-threat-protection/notifications) | - [ ] |
| 11  | [Configurações do relatório de agendamento](https://docs.microsoft.com/azure-advanced-threat-protection/reports) (lista de relatórios e tempo agendado)| - [ ] |
| 12  | Configurar [permissões baseadas em funções](https://docs.microsoft.com/azure-advanced-threat-protection/atp-role-groups) | - [ ] |
| 12  | [Configuração de notificação de SIEM (endereço IP)](https://docs.microsoft.com/azure-advanced-threat-protection/configure-event-collection#siemsyslog)| - [ ] |

#### <a name="validation"></a>Validação

No portal do ATP do Azure:

- Examine os [alertas de integridade](https://docs.microsoft.com/azure-advanced-threat-protection/atp-health-center) em busca de sinais de problemas de serviço.
- Examine os [logs de erros do sensor](https://docs.microsoft.com/azure-advanced-threat-protection/troubleshooting-atp-using-logs) do ATP do Azure quanto a erros incomuns.

## <a name="after-the-move"></a>Após a migração

Esta seção do guia explica as ações que podem ser executadas após a conclusão da migração.

> [!NOTE]
> Não há suporte à importação de alertas de segurança existentes do ATA para o ATP. Registre ou corrija todos os alertas do ATA existentes antes de desativar o Centro de ATA.

- **Desativar o Centro de ATA**  
  - Para fazer referência aos dados do Centro de ATA após a migração, é recomendável manter os dados do centro online durante um período de tempo. Após desativar o Centro de ATA, o número de recursos normalmente poderá ser reduzido, principalmente se os recursos forem uma Máquina Virtual.

- **Fazer backup do Mongo DB**  
  - Se desejar manter os dados do ATA por tempo indeterminado, [faça backup do Mongo DB](https://docs.microsoft.com/advanced-threat-analytics/ata-database-management#backing-up-the-ata-database).

## <a name="mission-accomplished"></a>Missão cumprida

Parabéns! Sua migração do ATA para o ATP do Azure foi concluída.

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre os recursos, a funcionalidade e os [alertas de segurança](https://docs.microsoft.com/azure-advanced-threat-protection/what-is-atp) do [ATP do Azure](https://docs.microsoft.com/azure-advanced-threat-protection/understanding-security-alerts).

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o ATP do Azure e a segurança relacionada com outras pessoas? Participe da [Comunidade do ATP do Azure](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) hoje mesmo!
