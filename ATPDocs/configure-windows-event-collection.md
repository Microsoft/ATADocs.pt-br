---
title: Configurar a coleção de Eventos do Windows na Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Nesta etapa da instalação da ATP, você configura a coleção de Eventos do Windows.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 88692d1a-45a3-4d54-a549-4b5bba6c037b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0478ab7dea7a8476faf61175654e6c50b10e9418
ms.sourcegitcommit: 0a98c0c151be2a81a3bb9ff1301d35a3091079ea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71217732"
---
# <a name="configure-windows-event-collection"></a>Configurar a coleção de Eventos do Windows

Para aprimorar os recursos de detecção de ameaças, a ATP do Azure (Proteção Avançada contra Ameaças do Azure) precisa dos seguintes eventos do Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757, 7045 e 8004. Esses eventos podem ser lidos automaticamente pelo sensor da ATP do Azure ou, caso o sensor da ATP do Azure não esteja implantado, eles poderão ser encaminhados para o sensor autônomo da ATP do Azure de duas maneiras: [configurando o sensor autônomo da ATP do Azure](configure-event-forwarding.md) para escutar eventos do SIEM ou [Configurando o encaminhamento de eventos do Windows](configure-event-forwarding.md).

> [!NOTE]
> É importante revisar e verificar suas [políticas de auditoria](atp-advanced-audit-policy.md) antes de configurar a coleta de eventos para garantir que os controladores de domínio estejam configurados corretamente para registrar os eventos necessários. 

Além de coletar e analisar o tráfego de rede para e dos controladores de domínio, o Azure ATP pode usar eventos do Windows para aprimorar ainda mais as detecções. A ATP do Azure usa os eventos 4776 e 8004 para NTLM, o que melhora várias detecções, e os eventos 4732, 4733, 4728, 4729, 4756, 4757, 7045 e 8004 para aprimorar a detecção de modificações de grupos confidenciais e a criação de serviços. Eles podem ser recebidos de seu SIEM ou definindo o Encaminhamento de Eventos do Windows no controlador de domínio. Os eventos coletados fornecem ao Azure ATP informações adicionais que não estão disponíveis por meio do tráfego de rede do controlador de domínio.

## <a name="ntlm-authentication-using-windows-event-8004"></a>Autenticação NTLM usando o evento 8004 do Windows

Para configurar a coleção 8004 de eventos do Windows:
1. Navegue para: Configuração do computador\Políticas\ Configurações do Windows\Configurações de segurança\Políticas locais\Opções de segurança
2. Defina a **política de grupo do domínio** da seguinte forma:
   - Segurança de rede: restringir NTLM: tráfego de NTLM de saída para servidores remotos = **Auditar todos**
   - Segurança de rede: restringir NTLM: auditar a autenticação NTLM neste domínio = **Habilitar todos**
   - Segurança de rede: restringir NTLM: auditar o tráfego NTLM de entrada = **Habilitar a auditoria de todas as contas**

Quando o evento 8004 do Windows é analisado pelo sensor da ATP do Azure, as atividades de autenticação NTLM da ATP do Azure são aprimoradas com os dados acessados pelo servidor.

## <a name="see-also"></a>Consulte Também
- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/aatpsizingtool)
- [Referência de logs de SIEM do Azure ATP](cef-format-sa.md)
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
