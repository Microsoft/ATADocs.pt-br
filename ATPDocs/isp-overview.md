---
title: Avaliações da situação de segurança de identidade da Proteção Avançada contra Ameaças do Azure
description: Neste artigo, você tem uma visão geral dos relatórios de avaliação de situação de segurança de identidade da ATP do Azure.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/16/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 71b15bd9-3183-4e24-b18a-705023ccc313
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 66de794ef4e715ef1ca94ca46388fc237bc04392
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90827981"
---
# <a name="azure-atps-identity-security-posture-assessments"></a>Avaliações de situação de segurança de identidade do ATP do Azure

Normalmente, organizações de todos os tamanhos têm visibilidade limitada de aplicativos e serviços locais e não sabem se eles podem ou não criar uma vulnerabilidade de segurança para a organização. O problema de visibilidade limitada é especialmente real em relação ao uso de componentes não compatíveis ou desatualizados.

Embora sua empresa possa investir tempo e esforço consideráveis em fortalecer identidades e na infraestrutura de identidade (como o Active Directory e o Active Directory Connect) de modo contínuo, é fácil ignorar configurações incorretas comuns e o uso de componentes herdados, que representam um dos maiores riscos de ameaça para sua organização. A pesquisa de segurança da Microsoft revela que a maioria dos ataques de identidade utilizam configurações incorretas comuns no Active Directory e o uso contínuo de componentes herdados (como o protocolo NTLMv1) para comprometer identidades e violar sua organização. Para combater isso de modo eficiente, a ATP do Azure agora oferece avaliações proativas de situação de segurança de identidade para detectar e sugerir ações de melhoria nas suas configurações do Active Directory local.

## <a name="what-do-azure-atp-identity-security-posture-assessments-provide"></a>O que as avaliações de situação de segurança de identidade da ATP do Azure oferecem?

- Detecções e dados contextuais sobre componentes e configurações incorretas conhecidos que podem ser explorados, além dos respectivos caminhos para corrigi-los.
- A ATP do Azure não só detecta atividades suspeitas, mas também monitora ativamente os pontos fracos das identidades locais e da infraestrutura de identidade usando o sensor da ATP do Azure.
- Os relatórios de avaliação da situação de segurança atual da organização são precisos, permitindo uma resposta rápida e um monitoramento efetivo em um ciclo contínuo.

## <a name="how-do-i-get-started"></a>Como começar?

### <a name="access"></a>Acesso

As avaliações de segurança da ATP do Azure ficam disponíveis no portal do Microsoft Cloud App Security após a ativação da integração da ATP do Azure. Para saber como integrar a ATP do Azure com o Cloud App Security, confira [Integração da ATP do Azure](/cloud-app-security/aatp-integration).

### <a name="licensing"></a>Licenciamento

Para acessar os relatórios de avaliação de segurança da ATP do Azure no Cloud App Security, não é necessário ter uma licença do Cloud App Security, somente uma licença da ATP do Azure.

## <a name="access-azure-atp-using-cloud-app-security"></a>Acessar a ATP do Azure com o Cloud App Security

Confira o [Início rápido do Cloud App Security](/cloud-app-security/getting-started-with-cloud-app-security) para conhecer melhor os fundamentos básicos de como usar o portal do Cloud App Security.

**Avaliações de situação de segurança de identidade**

A ATP do Azure oferece as seguintes avaliações de situação de segurança de identidade. Cada avaliação pode ser baixada como relatório com instruções de uso e ferramentas para criar um plano de ação de correção ou resolução.

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
    ![Acesse os relatórios de situação de segurança de identidade da ATP do Azure no Cloud App Security](media/atp-cas-isp-report-1.png)
1. Selecione **Investigar** no menu esquerdo e clique em **Situação de segurança de identidade** no menu suspenso.
1. Clique na avaliação de situação de segurança de identidade que você quer ver na lista **Relatórios de avaliação de segurança**.

## <a name="next-steps"></a>Próximas etapas

- [Saiba mais sobre como usar o Cloud App Security com a ATP do Azure](activities-filtering-mcas.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)