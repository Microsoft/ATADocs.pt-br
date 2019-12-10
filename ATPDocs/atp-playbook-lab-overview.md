---
title: Visão geral do tutorial de laboratório de Alerta de Segurança do ATP do Azure | Microsoft Docs
description: Esta visão geral do tutorial descreve as quatro partes do laboratório de Alerta de Segurança do ATP do Azure para simular ameaças que serão detectadas pelo ATP do Azure.
ms.service: azure-advanced-threat-protection
ms.topic: tutorial
author: mlottner
ms.author: mlottner
ms.date: 02/28/2019
ms.reviewer: itargoet
ms.openlocfilehash: 116f4648026d8f291a1576bb0cbd4bf392ff8a9a
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "57007442"
---
# <a name="tutorial-overview-atp-security-alert-lab"></a>Visão geral do tutorial: Laboratório de alerta de segurança do ATP

A finalidade do tutorial do laboratório de Alerta de Segurança do ATP do Azure é ilustrar os recursos do **ATP do Azure** para identificação e detecção de atividades suspeitas e possíveis ataques contra a sua rede. Este tutorial de quatro partes explica como instalar e configurar um ambiente de trabalho para testar algumas detecções *discretas* do ATP do Azure. Este laboratório se concentra nos recursos baseados em *assinatura* do ATP do Azure. O laboratório não inclui aprendizado de máquina avançado e detecções comportamentais baseadas no usuário ou em entidade, pois essas detecções exigem um período de aprendizado de até 30 dias com tráfego de rede real.

## <a name="lab-setup"></a>Configuração do laboratório

O primeiro tutorial nesta série de quatro partes, explica como criar um laboratório para testar detecções discretas do ATP do Azure. O tutorial inclui informações sobre computadores, usuários e ferramentas necessárias para configurar o laboratório e concluir os guias estratégicos. As instruções pressupõem que você sabe configurar um controlador de domínio e estações de trabalho para uso em laboratório, junto com outras tarefas administrativas. Quanto mais parecido estiver o seu laboratório com a configuração de laboratório sugerida, mais fácil será para seguir os procedimentos de teste do ATP do Azure. Após a conclusão da configuração do laboratório, use os guias estratégicos de Alerta de Segurança do ATP do Azure para testar.

> [!div class="nextstepaction"]
> [Configurar um laboratório de alerta de segurança do ATP](atp-playbook-setup-lab.md)

## <a name="reconnaissance-playbook"></a>Guia estratégico de reconhecimento

O segundo tutorial desta série de quatro partes é um guia estratégico de reconhecimento. As atividades de reconhecimento permitem que os invasores tenham uma compreensão detalhada e uma mapeamento completo de seu ambiente para uso posterior. O guia estratégico mostra alguns dos recursos do ATP do Azure para identificação e detecção de atividades suspeitas de possíveis ataques usando exemplos de ferramentas comuns de invasão e ataque disponíveis publicamente.

> [!div class="nextstepaction"]
> [Guia estratégico de reconhecimento](atp-playbook-reconnaissance.md)


## <a name="lateral-movement-playbook"></a>Guia estratégico de movimentação lateral

O guia estratégico de movimentação lateral é a terceira parte da série de quatro tutoriais. Movimentações laterais são feitas por um invasor que está tentando obter predominância de domínio. Conforme você percorre este guia estratégico, verá as detecções de ameaça de caminho de movimentação lateral e serviços de alertas de segurança do ATP do Azure das movimentações laterais simuladas executadas em seu laboratório.  

> [!div class="nextstepaction"]
> [Guia estratégico de movimentação lateral](atp-playbook-lateral-movement.md)

## <a name="domain-dominance-playbook"></a>Guia estratégico de predominância de domínio

O último tutorial da série de quatro partes é o guia estratégico de predominância de domínio. Durante a fase de predominância de domínio, um invasor já obteve as credenciais legítimas para acessar seu controlador de domínio e tentar alcançar a predominância de domínio persistente. Você simulará alguns métodos comuns de predominância de domínio para ver a detecção de ameaças e os serviços de alerta de segurança do Azure ATP focados na predominância de domínio.

> [!div class="nextstepaction"]
> [Guia estratégico de predominância de domínio](atp-playbook-domain-dominance.md)


## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o ATP do Azure e a segurança relacionada com outras pessoas? Participe da [Comunidade do ATP do Azure](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) hoje mesmo!
