---
title: Avaliação de situação de segurança de identidade de protocolos herdados da Proteção Avançada contra Ameaças do Azure
description: Neste artigo, você tem uma visão geral do relatório de avaliação de situação de segurança de identificação do protocolo herdado da ATP do Azure.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 6597b8c7-f83e-43c6-8149-fb4a914a845b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2eb9fb04c5f0adee2f98d73549ece6db88b0aeac
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90827949"
---
# <a name="security-assessment-legacy-protocols-usage"></a>Avaliação de segurança: uso de protocolos herdados

## <a name="what-are-legacy-protocols"></a>O que são os protocolos herdados?

Todas as empresas de trabalho padrão querem defender a infraestrutura usando patches e protegendo o servidor, mas uma área que geralmente permanece despercebida é a desativação do protocolo herdado. Sem reduzir a exposição do protocolo herdado, fica fácil roubar credenciais.

A maioria dos protocolos herdados foram elaborados e criados antes mesmo das necessidades de segurança de hoje existirem e dos requisitos de segurança corporativa modernos ficarem claros. No entanto, os protocolos herdados permanecem inalterados e são facilmente transformados em pontos de acesso vulneráveis em todas as organizações modernas.

## <a name="what-risks-do-retained-legacy-protocols-introduce"></a>Quais riscos os protocolos herdados retidos representam?

Os métodos modernos de ataques cibernéticos geralmente fazem uso específico de protocolos herdados e os utilizam para atingir organizações que ainda têm que implementar a mitigação adequada.

A redução da superfície de ataque pode ser conquistada ao desabilitar a compatibilidade com protocolos herdados inseguros, como:

- TLS 1.0 e 1.1 (bem como todas as versões do SSL)
- Protocolo SMB v1 (SMBv1)
- LanMan (LM) / NTLMv1
- Autenticação Digest

Para desativar o uso dos protocolos herdados, primeiro, a organização deve descobrir quais entidades e aplicativos internos dependem deles. O relatório de avaliação do **uso de protocolos herdados** exibe as principais entidades descobertas usando protocolos herdados (por enquanto, NTLMv1). Com o relatório, é possível analisar imediatamente quaisquer entidades principais afetadas e tomar medidas em relação a elas, interromper o uso desses protocolos e, por fim, desabilitá-los completamente. Para saber mais sobre os perigos de usar protocolos herdados, confira [Pare de usar o LAN Manager e o NTLMv1!](/archive/blogs/miriamxyra/stop-using-lan-manager-and-ntlmv1) e [Drop The MIC 2 e explorar clientes LMv2](https://www.preempt.com/blog/active-directory-ntlm-attacks/).

## <a name="how-do-i-use-this-security-assessment"></a>Como usar a avaliação de segurança?

1. Use a tabela do relatório para descobrir quais das principais entidades descobertas estão usando protocolos herdados.

    ![Impedir o uso de protocolos herdados](media/atp-cas-isp-legacy-protocols-2.png)
1. Tome as medidas apropriadas nessas entidades para descobrir dependências.
1. Pare o uso do protocolo herdado e, em algum momento, [desabilite completamente os protocolos](/archive/blogs/miriamxyra/stop-using-lan-manager-and-ntlmv1).
1. [Remover o MIC 2 e parar de usar os clientes LMv2](https://www.preempt.com/blog/active-directory-ntlm-attacks/).

> [!NOTE]
> Essa avaliação é atualizada quase em tempo real.

## <a name="next-steps"></a>Próximas etapas

- [Filtrar atividades da ATP do Azure no Cloud App Security](activities-filtering-mcas.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)