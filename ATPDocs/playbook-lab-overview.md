---
title: Visão geral do tutorial do laboratório de alerta de segurança do Microsoft Defender para Identidade
description: Esta visão geral do tutorial descreve as quatro partes do laboratório de alerta de segurança do Microsoft Defender para Identidade para simular ameaças que serão detectadas por esse serviço.
ms.date: 10/26/2020
ms.topic: tutorial
ms.openlocfilehash: 61602a6bb7d3037d2278c2f492395ed058e8910b
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533555"
---
# <a name="tutorial-overview-microsoft-defender-for-identity-security-alert-lab"></a>Visão geral do tutorial: Laboratório de alerta de segurança do Microsoft Defender para Identidade

A finalidade do tutorial do laboratório de alerta de segurança do [!INCLUDE [Product long](includes/product-long.md)] é ilustrar os recursos do **[!INCLUDE [Product short](includes/product-short.md)]** para identificação e detecção de atividades suspeitas e possíveis ataques contra sua rede. Este tutorial de quatro partes explica como instalar e configurar um ambiente de trabalho para testar algumas detecções *discretas* do [!INCLUDE [Product short](includes/product-short.md)]. Este laboratório se concentra nos recursos baseados em *assinatura* do [!INCLUDE [Product short](includes/product-short.md)]. O laboratório não inclui aprendizado de máquina avançado e detecções comportamentais baseadas no usuário ou em entidade, pois essas detecções exigem um período de aprendizado de até 30 dias com tráfego de rede real.

## <a name="lab-setup"></a>Configuração do laboratório

O primeiro tutorial dessa série de quatro partes explica como criar um laboratório para testar detecções discretas do [!INCLUDE [Product short](includes/product-short.md)]. O tutorial inclui informações sobre computadores, usuários e ferramentas necessárias para configurar o laboratório e concluir os guias estratégicos. As instruções pressupõem que você sabe configurar um controlador de domínio e estações de trabalho para uso em laboratório, junto com outras tarefas administrativas. Quanto mais parecido estiver seu laboratório com a configuração sugerida, mais fácil será para seguir os procedimentos de teste do [!INCLUDE [Product short](includes/product-short.md)]. Após a conclusão da configuração do laboratório, use os guias estratégicos de Alerta de segurança do [!INCLUDE [Product short](includes/product-short.md)] para testar.

> [!div class="nextstepaction"]
> [Configurar um laboratório de alerta de segurança do ATP](playbook-setup-lab.md)

## <a name="reconnaissance-playbook"></a>Guia estratégico de reconhecimento

O segundo tutorial desta série de quatro partes é um guia estratégico de reconhecimento. As atividades de reconhecimento permitem que os invasores tenham uma compreensão detalhada e uma mapeamento completo de seu ambiente para uso posterior. O guia estratégico mostra alguns dos recursos do [!INCLUDE [Product short](includes/product-short.md)] para identificação e detecção de atividades suspeitas de possíveis ataques usando exemplos de ferramentas comuns de invasão e ataque disponíveis publicamente.

> [!div class="nextstepaction"]
> [Guia estratégico de reconhecimento](playbook-reconnaissance.md)

## <a name="lateral-movement-playbook"></a>Guia estratégico de movimentação lateral

O guia estratégico de movimentação lateral é a terceira parte da série de quatro tutoriais. Movimentações laterais são feitas por um invasor que está tentando obter predominância de domínio. Conforme você percorrer este guia estratégico, verá as detecções de ameaça de caminho de movimentação lateral e serviços de alertas de segurança do [!INCLUDE [Product short](includes/product-short.md)] das movimentações laterais simuladas executadas em seu laboratório.  

> [!div class="nextstepaction"]
> [Guia estratégico de movimentação lateral](playbook-lateral-movement.md)

## <a name="domain-dominance-playbook"></a>Guia estratégico de predominância de domínio

O último tutorial da série de quatro partes é o guia estratégico de predominância de domínio. Durante a fase de predominância de domínio, um invasor já obteve as credenciais legítimas para acessar seu controlador de domínio e tentar alcançar a predominância de domínio persistente. Você simulará alguns métodos comuns de predominância de domínio para ver a detecção de ameaças e os serviços de alerta de segurança do [!INCLUDE [Product short](includes/product-short.md)] focados na predominância de domínio.

> [!div class="nextstepaction"]
> [Guia estratégico de predominância de domínio](playbook-domain-dominance.md)


## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o [!INCLUDE [Product short](includes/product-short.md)] e a segurança relacionada com outras pessoas? Participe da Comunidade [[!INCLUDE [Product short](includes/product-short.md)]](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) hoje mesmo!
