---
title: Integração do Microsoft defender para identidade com o Microsoft defender para ponto de extremidade
description: Como integrar o Microsoft defender para identidade com o Microsoft defender for Endpoint para cobertura de detecção de ameaças completas
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
ms.openlocfilehash: d0e059516346d5b2c832e5bd5ea73008b1f51082
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93278070"
---
# <a name="integrate-product-long-with-microsoft-defender-for-endpoint"></a>Integre [!INCLUDE [Product long](includes/product-long.md)] com o Microsoft defender para ponto de extremidade

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

[!INCLUDE [Product long](includes/product-long.md)] o permite a integração [!INCLUDE [Product long](includes/product-long.md)] com o defender for Endpoint, para uma solução de proteção contra ameaças ainda mais completa. Embora [!INCLUDE [Product short](includes/product-short.md)] o monitore o tráfego em seus controladores de domínio, o defender for Endpoint monitora seus pontos de extremidade, fornecendo, juntos, uma única interface da qual você pode proteger seu ambiente.

Integrando o defender for Endpoint ao [!INCLUDE [Product short](includes/product-short.md)] , você pode aproveitar todo o poder de ambos os serviços e proteger seu ambiente, incluindo:

- Sensores comportamentais de ponto de extremidade: inseridos no Windows 10, esses sensores coletam e processam sinais comportamentais do sistema operacional (por exemplo, processo, registro, arquivo e comunicações de rede) e enviam esses dados de sensor para sua instância privada, isolada e em nuvem do defender para ponto de extremidade.

- Análise de segurança da nuvem: aproveitando Big Data, machine learning e uma visão única da Microsoft de todo o ecossistema do Windows (como a [Ferramenta de Remoção de Software Mal-Intencionado da Microsoft](https://www.microsoft.com/download/malicious-software-removal-tool-details.aspx)), produtos de nuvem corporativos (como o Microsoft 365) e ativos online (como reputação de URLs do SmartScreen e o Bing), os sinais comportamentais são traduzidos em insights, detecções e respostas recomendadas a ameaças avançadas.

- Inteligência contra ameaças: gerada pelo Microsoft caçadores, pelas equipes de segurança e aumentada pela inteligência contra ameaças fornecida por parceiros, a inteligência contra ameaças permite que o defender para o ponto de extremidade identifique ferramentas, técnicas, procedimentos e alertas do invasor quando essas atividades são observadas nos dados do sensor coletados.

[!INCLUDE [Product short](includes/product-short.md)] a tecnologia detecta várias atividades suspeitas, concentrando-se em várias fases da cadeia de eliminação de ataque cibernético, incluindo:

- Reconhecimento, durante o qual os invasores coletam informações sobre como o ambiente foi compilado criado, o que são os ativos diferentes e quais entidades existem. Geralmente, eles criam o plano para as próximas fases do ataque aqui.

- Ciclo de movimentação lateral, durante o qual um invasor investe tempo e esforço na propagação da superfície de seu ataque dentro de sua rede.

- Controle do domínio (persistência), durante o qual um invasor captura as informações permitindo que retome sua campanha usando vários conjuntos de pontos de entrada, credenciais e técnicas.

Ao mesmo tempo, o defender for Endpoint aproveita a tecnologia e a experiência da Microsoft para detectar ataques cibernéticos sofisticados, fornecendo:

- Detecção de ataques avançada, habilitada para a nuvem e baseada em comportamento  
Localiza os ataques que o fizeram após todas as outras defesas (detecção de pós-violação), fornece alertas acionáveis e correlacionados para adversários conhecidos e desconhecidos tentando ocultar suas atividades nos pontos de extremidade.

- Linha do tempo avançada para investigação forense e mitigação  
Investigue facilmente o escopo da violação ou comportamentos suspeitos em qualquer computador por meio de uma linha do tempo avançada. Inventário de arquivos, URLs e conexões de rede em toda a rede. Obtenha insights adicionais usando a coleta e análise profunda ("detonação") para qualquer arquivo ou URL.

- Base de dados de conhecimento de inteligência de ameaças exclusiva interna  
A óptica incomparável com relação às ameaças fornece detalhes sobre o ator e o contexto da intenção para cada detecção de ameaça baseada em inteligência – combinando fontes de inteligência próprias e de terceiros.

## <a name="prerequisites"></a>Pré-requisitos

Para habilitar esse recurso, você precisa de uma licença para o [!INCLUDE [Product short](includes/product-short.md)] e o defender for Endpoint.

<a name="how-to-integrate-azure-atp-with-microsoft-defender-atp"></a>

## <a name="how-to-integrate-product-short-with-defender-for-endpoint"></a>Como integrar [!INCLUDE [Product short](includes/product-short.md)] com o defender para ponto de extremidade

1. No [!INCLUDE [Product short](includes/product-short.md)] portal, selecione **configuração**.

    ![[! INCLUIR [produto curto] (inclui/produto-curto. MD)] menu de configuração](media/msde-configuration.png)
1. Na lista configurações, selecione **Microsoft defender para ponto de extremidade** e defina a opção integração ativar como **ativado**.

    ![Habilitar a integração do Windows Defender](media/msde-enable-integration.png)

1. No [portal do defender for Endpoint](https://securitycenter.windows.com/preferences/advanced), vá para **configurações** , **recursos avançados** e defina **[!INCLUDE [Product long](includes/product-long.md)] integração** como **ativado**.

    ![Integração do defender para ponto de extremidade habilitar](media/msde-enable.png)

1. Para verificar o status da integração, no [!INCLUDE [Product short](includes/product-short.md)] portal, vá para **configurações**  >  **Microsoft defender para integração de ponto de extremidade**. Você pode ver o status da integração e, se algo estiver errado, você verá um erro.

## <a name="how-it-works"></a>Como isso funciona

Depois que o [!INCLUDE [Product short](includes/product-short.md)] e o defender for Endpoint são totalmente integrados, no [!INCLUDE [Product short](includes/product-short.md)] portal, no pop-up de mini-perfil e na página de perfil de entidade, cada entidade que existe no defender para ponto de extremidade inclui uma notificação para mostrar que ele está integrado ao defender para ponto de extremidade.

 ![Perfil de alertas do defender for Endpoint](media/profile-alerts-msde.png)

Se a entidade contiver alertas no defender para ponto de extremidade, haverá um número próximo à notificação para que você saiba quantos alertas foram gerados.

 ![[! INCLUIR alertas [produto curto] (inclui/produto-curto. MD)]](media/msde-icon-alerts.png)

Se você clicar na notificação, você será levado ao defender para o portal de ponto de extremidade, onde poderá exibir e atenuar os alertas. Se a entidade não for reconhecida pelo defender for Endpoint, a notificação ficará esmaecida.

 ![Defender para ponto de extremidade cinza](media/msde-grey.png)

No portal do defender for Endpoint, clique em um ponto de extremidade para exibir [!INCLUDE [Product short](includes/product-short.md)] alertas. Se você clicar nos alertas para esta entidade no defender para ponto de extremidade, a página de perfil da entidade será aberta no [!INCLUDE [Product short](includes/product-short.md)] .

 > [!NOTE]
 > Atualmente, [!INCLUDE [Product short](includes/product-short.md)] a integração com o defender for Endpoint dá suporte apenas a usuários e computadores do AD local. Os usuários do Azure AD e as máquinas virtuais que são gerenciadas no Azure não serão exibidos como parte da integração

![Alertas do defender for Endpoint](media/msde-alerts.png)

## <a name="see-also"></a>Consulte Também

- [Investigando caminhos de movimento lateral com [!INCLUDE [Product short](includes/product-short.md)]](use-case-lateral-movement-path.md)
- [[!INCLUDE [Product short](includes/product-short.md)] ferramenta de dimensionamento](https://aka.ms/aatpsizingtool)
- [[!INCLUDE [Product short](includes/product-short.md)] arquitectura](architecture.md)
- [Pré-instalação [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [Confira o [!INCLUDE [Product short](includes/product-short.md)] Fórum!](https://aka.ms/MDIcommunity)
