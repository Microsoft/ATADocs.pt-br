---
title: Microsoft defender para avaliações de postura de segurança de identidade da identidade
description: Este artigo fornece uma visão geral do Microsoft defender para relatórios de avaliação de postura de segurança de identidade da identidade.
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
ms.openlocfilehash: c5f6eed2ee9220555bbd870f66e2cacbbb82ed1c
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93275099"
---
# <a name="product-longs-identity-security-posture-assessments"></a>[!INCLUDE [Product long](includes/product-long.md)]avaliações da postura de segurança de identidade

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Normalmente, organizações de todos os tamanhos têm visibilidade limitada de aplicativos e serviços locais e não sabem se eles podem ou não criar uma vulnerabilidade de segurança para a organização. O problema de visibilidade limitada é especialmente real em relação ao uso de componentes não compatíveis ou desatualizados.

Embora sua empresa possa investir tempo e esforço consideráveis em fortalecer identidades e na infraestrutura de identidade (como o Active Directory e o Active Directory Connect) de modo contínuo, é fácil ignorar configurações incorretas comuns e o uso de componentes herdados, que representam um dos maiores riscos de ameaça para sua organização. A pesquisa de segurança da Microsoft revela que a maioria dos ataques de identidade utilizam configurações incorretas comuns no Active Directory e o uso contínuo de componentes herdados (como o protocolo NTLMv1) para comprometer identidades e violar sua organização. Para combater isso efetivamente, o [!INCLUDE [Product long](includes/product-long.md)] agora oferece avaliações proativas de postura de segurança de identidade para detectar e sugerir ações de aperfeiçoamento em suas configurações Active Directory locais.

## <a name="what-do-product-short-identity-security-posture-assessments-provide"></a>O que as [!INCLUDE [Product short](includes/product-short.md)] avaliações de postura de segurança de identidade fornecem?

- Detecções e dados contextuais sobre componentes e configurações incorretas conhecidos que podem ser explorados, além dos respectivos caminhos para corrigi-los.
- [!INCLUDE [Product short](includes/product-short.md)] detecta não apenas atividades suspeitas, mas também monitora ativamente as identidades locais e a infraestrutura de identidade para pontos fracos, usando o [!INCLUDE [Product short](includes/product-short.md)] sensor existente.
- Os relatórios de avaliação da situação de segurança atual da organização são precisos, permitindo uma resposta rápida e um monitoramento efetivo em um ciclo contínuo.

## <a name="how-do-i-get-started"></a>Como começar?

### <a name="access"></a>Acesso

[!INCLUDE [Product short](includes/product-short.md)] as avaliações de segurança estão disponíveis usando o portal de Microsoft Cloud App Security depois de ativar a [!INCLUDE [Product short](includes/product-short.md)] integração. Para saber como integrar o [!INCLUDE [Product short](includes/product-short.md)] Cloud app Security, consulte [ [!INCLUDE [Product short](includes/product-short.md)] integração](/cloud-app-security/aatp-integration).

### <a name="licensing"></a>Licenciamento

O acesso [!INCLUDE [Product short](includes/product-short.md)] a relatórios de avaliação de segurança no Cloud app Security não requer uma licença de Cloud app Security, apenas uma [!INCLUDE [Product short](includes/product-short.md)] licença é necessária.

## <a name="access-product-short-using-cloud-app-security"></a>Acesso [!INCLUDE [Product short](includes/product-short.md)] usando Cloud app Security

Confira o [Início rápido do Cloud App Security](/cloud-app-security/getting-started-with-cloud-app-security) para conhecer melhor os fundamentos básicos de como usar o portal do Cloud App Security.

**Avaliações de situação de segurança de identidade**

[!INCLUDE [Product short](includes/product-short.md)] oferece as seguintes avaliações de postura de segurança de identidade. Cada avaliação pode ser baixada como relatório com instruções de uso e ferramentas para criar um plano de ação de correção ou resolução.

**Relatórios de avaliação**

- [Controladores de domínio com o serviço de Spooler de Impressão disponível](cas-isp-print-spooler.md)
- [Entidades inativas em grupos confidenciais](cas-isp-dormant-entities.md)
- [Entidades que expõem credenciais em texto não criptografado](cas-isp-clear-text.md)
- [Uso da LAPS da Microsoft](cas-isp-laps.md)
- [Uso de protocolos herdados](cas-isp-legacy-protocols.md)
- [LMP (caminhos de movimento lateral) mais arriscados](cas-isp-riskiest-lmp.md)
- [Controladores de domínio não monitorados](cas-isp-unmonitored-domain-controller.md)
- [Atributos de conta não seguros](cas-isp-unsecure-account-attributes.md)
- [Delegação de Kerberos não segura](cas-isp-unconstrained-kerberos.md)
- [Atributos do histórico de SID não seguros](cas-isp-unsecure-sid-history-attribute.md)
- [Uso de criptografia fraca](cas-isp-weak-cipher.md)

Para acessar as avaliações de situação de segurança de identidade:

1. Abra o portal do **Microsoft Cloud App Security**.
    ![Acessar o [! INCLUIR [produto curto] (inclui/produto-curto. MD)] relatórios de postura de segurança de identidade no Cloud App Security](media/cas-isp-report-1.png)
1. Selecione **Investigar** no menu esquerdo e clique em **Situação de segurança de identidade** no menu suspenso.
1. Clique na avaliação de situação de segurança de identidade que você quer ver na lista **Relatórios de avaliação de segurança**.

## <a name="next-steps"></a>Próximas etapas

- [Saiba mais sobre como usar Cloud App Security com [!INCLUDE [Product short](includes/product-short.md)]](activities-filtering-mcas.md)
- [Confira o [!INCLUDE [Product short](includes/product-short.md)] Fórum!](https://aka.ms/MDIcommunity)