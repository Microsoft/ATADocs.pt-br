---
title: Microsoft defender para avaliações de postura de segurança de identidade da identidade
description: Este artigo fornece uma visão geral do Microsoft defender para relatórios de avaliação de postura de segurança de identidade da identidade.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 3b3f20ac50e3b5b687dd6ece8b421c84288a3126
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533844"
---
# <a name="microsoft-defender-for-identitys-identity-security-posture-assessments"></a>Microsoft defender para avaliações de postura de segurança de identidade da identidade

Normalmente, organizações de todos os tamanhos têm visibilidade limitada de aplicativos e serviços locais e não sabem se eles podem ou não criar uma vulnerabilidade de segurança para a organização. O problema de visibilidade limitada é especialmente real em relação ao uso de componentes não compatíveis ou desatualizados.

Embora sua empresa possa investir tempo e esforço consideráveis em fortalecer identidades e na infraestrutura de identidade (como o Active Directory e o Active Directory Connect) de modo contínuo, é fácil ignorar configurações incorretas comuns e o uso de componentes herdados, que representam um dos maiores riscos de ameaça para sua organização. A pesquisa de segurança da Microsoft revela que a maioria dos ataques de identidade utilizam configurações incorretas comuns no Active Directory e o uso contínuo de componentes herdados (como o protocolo NTLMv1) para comprometer identidades e violar sua organização. Para combater isso efetivamente, o [!INCLUDE [Product long](includes/product-long.md)] agora oferece avaliações proativas de postura de segurança de identidade para detectar e sugerir ações de aperfeiçoamento em suas configurações Active Directory locais.

## <a name="what-do-defender-for-identity-identity-security-posture-assessments-provide"></a>O que o defender para avaliações de postura de segurança de identidade de identidade fornece?

- Detecções e dados contextuais sobre componentes e configurações incorretas conhecidos que podem ser explorados, além dos respectivos caminhos para corrigi-los.
- [!INCLUDE [Product short](includes/product-short.md)] detecta não apenas atividades suspeitas, mas também monitora ativamente as identidades locais e a infraestrutura de identidade para pontos fracos, usando o [!INCLUDE [Product short](includes/product-short.md)] sensor existente.
- Os relatórios de avaliação da situação de segurança atual da organização são precisos, permitindo uma resposta rápida e um monitoramento efetivo em um ciclo contínuo.

## <a name="how-do-i-get-started"></a>Como começar?

### <a name="access"></a>Acesso

[!INCLUDE [Product short](includes/product-short.md)] as avaliações de segurança estão disponíveis usando o portal de Microsoft Cloud App Security depois de ativar a [!INCLUDE [Product short](includes/product-short.md)] integração. Para saber como integrar o [!INCLUDE [Product short](includes/product-short.md)] Cloud app Security, consulte [ [!INCLUDE [Product short](includes/product-short.md)] integração](/cloud-app-security/aatp-integration).

### <a name="licensing"></a>Licenças

O acesso [!INCLUDE [Product short](includes/product-short.md)] a relatórios de avaliação de segurança no Cloud app Security não requer uma licença de Cloud app Security, apenas uma [!INCLUDE [Product short](includes/product-short.md)] licença é necessária.

## <a name="access-defender-for-identity-using-cloud-app-security"></a>Acessar o defender para identidade usando o Cloud App Security

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
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
