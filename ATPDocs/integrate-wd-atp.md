---
title: Integração da Proteção Avançada contra Ameaças do Azure com o Microsoft Defender ATP
description: Como integrar a Proteção Avançada contra Ameaças do Azure com o Microsoft Defender ATP para cobertura completa de detecção de ameaças
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 02/19/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: f6f3ed75-d6bb-4966-a9a7-5339c4f3ebac
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: df24013a5796d342ffc42b6f2c68f729a590d183
ms.sourcegitcommit: bf5f58317121f1fb0fffc83d8b419cdd7ef27d9a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/05/2020
ms.locfileid: "80669584"
---
# <a name="integrate-azure-atp-with-microsoft-defender-atp"></a>Integração do ATP do Azure com o Microsoft Defender ATP

A Proteção Avançada contra Ameaças do Azure permite que você integre o Azure ATP ao Microsoft Defender ATP para uma solução de proteção contra ameaças ainda mais completa. Enquanto o Azure ATP monitora o tráfego em seus controladores de domínio, o Microsoft Defender ATP monitora seus pontos de extremidade. Juntos, eles fornecem uma única interface na qual você pode proteger seu ambiente.

Com a integração do Microsoft Defender ATP ao Azure ATP, você pode aproveitar todo o potencial dos dois serviços e proteger seu ambiente, incluindo:

- Sensores de comportamento de ponto de extremidade: inseridos no Windows 10, esses sensores coletam e processam sinais comportamentais do sistema operacional (por exemplo, processo, registro, arquivo e comunicações de rede) e enviam esses dados do sensor à sua instância de nuvem privada e isolada do Microsoft Defender ATP.

- Análise de segurança da nuvem: aproveitando Big Data, machine learning e uma visão única da Microsoft de todo o ecossistema do Windows (como a [Ferramenta de Remoção de Software Mal-Intencionado da Microsoft](https://www.microsoft.com/download/malicious-software-removal-tool-details.aspx)), produtos de nuvem corporativos (como o Office 365) e ativos online (como reputação de URLs do SmartScreen e o Bing), os sinais comportamentais são traduzidos em insights, detecções e respostas recomendadas a ameaças avançadas.

- Inteligência contra ameaças: gerada por equipes de segurança e caçadores da Microsoft e ampliada pela inteligência contra ameaças fornecida por parceiros, a inteligência contra ameaças permite que o Microsoft Defender ATP identifique ferramentas, técnicas e procedimentos do invasor e gere alertas quando essas atividades forem observadas nos dados coletados pelo sensor.

A tecnologia do Azure ATP detecta várias atividades suspeitas, concentrando-se em várias fases da cadeia do ataque cibernético, incluindo:

- Reconhecimento, durante o qual os invasores coletam informações sobre como o ambiente foi compilado criado, o que são os ativos diferentes e quais entidades existem. Geralmente, eles criam o plano para as próximas fases do ataque aqui.

- Ciclo de movimentação lateral, durante o qual um invasor investe tempo e esforço na propagação da superfície de seu ataque dentro de sua rede.

- Controle do domínio (persistência), durante o qual um invasor captura as informações permitindo que retome sua campanha usando vários conjuntos de pontos de entrada, credenciais e técnicas.

Ao mesmo tempo, o Microsoft Defender ATP aproveita a tecnologia e a experiência da Microsoft para detectar ataques cibernéticos sofisticados, fornecendo:

- Detecção de ataques avançada, habilitada para a nuvem e baseada em comportamento  
Localiza os ataques que passaram por todas as outras proteções (detecção pós-violação), fornece alertas acionáveis correlacionados sobre adversários conhecidos e desconhecidos que estão tentando ocultar suas atividades em pontos de extremidade.

- Linha do tempo avançada para investigação forense e mitigação  
Investigue facilmente o escopo da violação ou comportamentos suspeitos em qualquer computador por meio de uma linha do tempo avançada. Inventário de arquivos, URLs e conexões de rede em toda a rede. Obtenha insights adicionais usando a coleta e análise profunda ("detonação") para qualquer arquivo ou URL.

- Base de dados de conhecimento de inteligência contra ameaças exclusiva incorporada  
A óptica incomparável com relação às ameaças fornece detalhes sobre o ator e o contexto da intenção para cada detecção de ameaça baseada em inteligência – combinando fontes de inteligência próprias e de terceiros.

## <a name="prerequisites"></a>Pré-requisitos

Para habilitar esse recurso, é necessária uma licença para o ATP do Azure e o Microsoft Defender ATP.

## <a name="how-to-integrate-azure-atp-with-microsoft-defender-atp"></a>Como integrar o ATP do Azure ao Microsoft Defender ATP

1. No portal do ATP do Azure, abra **Configuração**.

    ![Menu Configuração do ATP do Azure](./media/atp-configuration-wd.png)
2. Na lista Configurações, selecione **Microsoft Defender ATP** e defina a alternância de integração como **Ativa**.

    ![Habilitar a integração do Windows Defender](./media/enable-integration.png)

3. No [portal do Microsoft Defender ATP](https://securitycenter.windows.com/preferences/advanced), vá até **Configurações**, **Recursos avançados** e defina **Integração do Azure ATP** como **ATIVO**.

    ![Habilitar integração do Microsoft Defender ATP](./media/wd-atp-enable.png)

4. Para verificar o status da integração, no portal do ATP do Azure, vá até **Configurações** > **Integração do Microsoft Defender ATP**. Você pode ver o status da integração e, se algo estiver errado, você verá um erro.

## <a name="how-it-works"></a>Como funciona

Após o ATP do Azure e o Microsoft Defender ATP serem totalmente integrados, no portal do ATP do Azure, no pop-up do miniperfil e na página do perfil de entidade, cada entidade que existir no Microsoft Defender ATP incluirá uma notificação para mostrar que ela foi integrada ao Microsoft Defender ATP.

 ![Alertas do Microsoft Defender ATP](./media/profile-alerts-wd.png)

Se a entidade contiver alertas no Microsoft Defender ATP, haverá um número ao lado da notificação para informar quantos alertas foram gerados.

 ![Alertas do ATP do Azure](./media/atp-integrated-wd-icon-alerts.png)

Se clicar na notificação, você será direcionado para o portal do Microsoft Defender ATP, no qual poderá exibir e atenuar os alertas. Se a entidade não for reconhecida pelo Microsoft Defender ATP, a notificação será esmaecida.

 ![Esmaecimento do Microsoft Defender ATP](./media/wd-grey.png)

No portal do Microsoft Defender ATP, clique em um ponto de extremidade para exibir os alertas do ATP do Azure. Se você clicar nos alertas para esta entidade no Microsoft Defender ATP, a página de perfil da entidade será aberta no Azure ATP.

 > [!NOTE]
 > No momento, a integração do Azure ATP com o Microsoft Defender ATP é compatível apenas com usuários e computadores do AD local. Os usuários do Azure AD e as máquinas virtuais que são gerenciadas no Azure não serão exibidos como parte da integração

![Alertas do Microsoft Defender ATP](./media/wd-atp-alerts.png)

## <a name="see-also"></a>Consulte Também

- [Investigando caminhos de movimento lateral com o Azure ATP](use-case-lateral-movement-path.md)
- [Ferramenta de dimensionamento do Azure ATP](https://aka.ms/aatpsizingtool)
- [Arquitetura do Azure ATP](atp-architecture.md)
- [Instalar o ATP](install-atp-step1.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
