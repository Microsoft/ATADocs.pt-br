---
title: Integração da Proteção Avançada contra Ameaças do Azure com o Windows Defender ATP | Microsoft Docs
description: Como integrar a Proteção Avançada contra Ameaças do Azure com o Windows Defender ATP para cobertura completa de detecção de ameaças
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/5/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: f6f3ed75-d6bb-4966-a9a7-5339c4f3ebac
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6d6c2cdb157d4e3f75794c8c40abfc7556e314d5
ms.sourcegitcommit: b218f60b42a25fe486d774d97719590e6fa74e10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34760066"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*

# <a name="integrating-azure-atp-with-windows-defender-atp"></a>Integrando o Azure ATP ao Windows Defender ATP

A Proteção Avançada contra Ameaças do Azure permite que você integre o Azure ATP ao Windows Defender ATP para uma solução de proteção contra ameaças ainda mais completa. Enquanto o Azure ATP monitora o tráfego em seus controladores de domínio, o Windows Defender ATP monitora seus pontos de extremidade. Juntos, eles fornecem uma única interface na qual você pode proteger seu ambiente.

Integrando o Windows Defender ATP ao Azure ATP, você pode aproveitar todo o potencial dos dois serviços e proteger seu ambiente, incluindo:

- Sensores e sensores autônomos do Azure ATP: podem ser colocados diretamente em seus controladores de domínio ou espelhamento de porta de seus controladores de domínio para o ATP, a fim de capturar e analisar o tráfego de rede de vários protocolos (por exemplo, Kerberos, DNS, RPC, NTLM e outros) para autenticação, autorização e coleta de informações. 

-   Sensores de comportamento de ponto de extremidade: inseridos no Windows 10, esses sensores coletam e processam sinais comportamentais do sistema operacional (por exemplo, processo, registro, arquivo e comunicações de rede) e enviam esses dados do sensor à sua instância de nuvem privada e isolada do Windows Defender ATP.

- Análise de segurança de nuvem: aproveitando Big Data, machine learning e uma visão única da Microsoft de todo o ecossistema do Windows (como a [Ferramenta de Remoção de Software Mal-Intencionado da Microsoft](https://www.microsoft.com/download/malicious-software-removal-tool-details.aspx)), produtos de nuvem corporativos (como o Office 365) e ativos online (como reputação de URLs do SmartScreen e o Bing), os sinais comportamentais são traduzidos em insights, detecções e respostas recomendadas a ameaças avançadas.

- Inteligência contra ameaças: gerada por equipes de segurança e caçadores da Microsoft e ampliada pela inteligência contra ameaças fornecida por parceiros, a inteligência contra ameaças permite que o Windows Defender ATP identifique ferramentas, técnicas e procedimentos do invasor e gere alertas quando eles forem observados nos dados coletados pelo sensor.

A tecnologia do Azure ATP detecta várias atividades suspeitas, concentrando-se em várias fases da cadeia do ataque cibernético, incluindo:

- Reconhecimento, durante o qual os invasores coletam informações sobre como o ambiente foi compilado criado, o que são os ativos diferentes e quais entidades existem. Geralmente, eles criam o plano para as próximas fases do ataque.

- Ciclo de movimentação lateral, durante o qual um invasor investe tempo e esforço na propagação da superfície de seu ataque dentro de sua rede.

- Controle do domínio (persistência), durante o qual um invasor captura as informações permitindo que retome sua campanha usando vários conjuntos de pontos de entrada, credenciais e técnicas.

Ao mesmo tempo, o Windows Defender ATP aproveita a tecnologia e a experiência da Microsoft para detectar ataques cibernéticos sofisticados, fornecendo:

- Detecção de ataques avançada, habilitada para a nuvem e baseada em comportamento<br></br>Localiza os ataques que passaram por todas as outras proteções (detecção pós-violação), fornece alertas acionáveis correlacionados sobre adversários conhecidos e desconhecidos que estão tentando ocultar suas atividades em pontos de extremidade.

- Linha do tempo avançada para investigação forense e mitigação<br></br>Investigue facilmente o escopo da violação ou comportamentos suspeitos em qualquer computador por meio de uma linha do tempo avançada. Inventário de arquivos, URLs e conexões de rede em toda a rede. Obtenha insights adicionais usando a coleta e análise profunda ("denotação") para qualquer arquivo ou URL.

- Base de dados de conhecimento de inteligência contra ameaças exclusiva incorporada<br></br>A ótica incomparável com relação às ameaças fornece detalhes sobre o ator e o contexto da intenção para cada detecção de ameaça baseada em inteligência – combinando fontes de inteligência próprias e de terceiros.

## <a name="prerequisites"></a>Pré-requisitos

Para habilitar esse recurso, você precisa de uma licença para o Azure ATP e o Windows Defender ATP. 


## <a name="how-to-integrate-azure-atp-with-windows-defender-atp"></a>Como integrar o Azure ATP ao Windows Defender ATP

1. Defina o espaço de trabalho que você deseja integrar como **Primário**. Apenas um espaço de trabalho pode ser o espaço de trabalho primário e apenas um espaço de trabalho primário pode ser integrado a outros serviços. Se, em algum momento no futuro, você quiser que este espaço de trabalho não seja mais o espaço de trabalho primário, primeiro você precisará remover a integração antes que possa defini-lo como não primário.

 ![espaço de trabalho primário](./media/primary-workspace.png)

2. Clique em **Configuração** e, em **Fontes de dados**, selecione **Windows Defender ATP**. Em seguida, clique no link para **Gerenciamento de espaço de trabalho**. Isso só estará disponível se você tiver uma licença do Windows Defender ATP e já tiver executado o processo de ambientação do Windows Defender ATP. 

3. Em seu espaço de trabalho primário, clique na engrenagem de configurações.

 ![integração do espaço de trabalho](./media/edit-workspace.png)
 
3. Defina a integração como **Ativo**. 

 ![habilitar integração](./media/enable-integration.png)

4. No [Portal do Windows Defender ATP](https://beta.securitycenter.windows.com/preferences/advanced), vá até **Configurações**, **Recursos avançados** e defina **Integração do Azure ATP** como **ATIVO**. 

 ![Habilitar integração do Windows Defender ATP](./media/wd-atp-enable.png)

5. Para verificar o status da integração, no portal de espaço de trabalho do Azure ATP, vá até **Configurações** e, em seguida, **Integração do Windows Defender ATP**. Você pode ver o status da integração. Se algo estiver errado, você verá um erro. Você também pode ver qual espaço de trabalho está integrado ao Windows Defender ATP.

## <a name="how-it-works"></a>Como funciona

Após o Azure ATP e o Windows Defender ATP serem totalmente integrados, no portal de espaço de trabalho do Azure ATP, no pop-up do miniperfil e na página do perfil de entidade, cada entidade que existir no Windows Defender ATP inclui uma notificação para mostrar que ela está integrada ao Windows Defender ATP. 

 ![Alertas do Windows Defender ATP](./media/profile-alerts-wd.png)

Se a entidade contiver alertas no Windows Defender ATP, haverá um número ao lado da notificação para informar quantos alertas foram gerados.

 ![Alertas do Azure ATP](./media/atp-integrated-wd-icon-alerts.png)

Se clicar na notificação, você será direcionado para o portal do Windows Defender ATP, no qual poderá exibir e atenuar alertas. Se a entidade não for reconhecida pelo Windows Defender ATP, a notificação será esmaecida. 

 ![Windows Defender ATP cinza](./media/wd-grey.png)

No portal do Windows Defender ATP, quando clica em um ponto de extremidade, você pode exibir alertas do Azure ATP. Se você clicar nos alertas para esta entidade no Windows Defender ATP, a página de perfil da entidade será aberta no Azure ATP. 
 
 > ![NOTE] No momento, a integração do Azure ATP com o Windows Defender ATP dá suporte apenas a usuários e computadores do AD local. Os usuários do Azure AD e as máquinas virtuais que são gerenciadas no Azure não serão exibidos como parte da integração 

![Alertas do Windows Defender ATP](./media/wd-atp-alerts.png)


## <a name="see-also"></a>Consulte Também

- [Investigando caminhos de movimento lateral com o Azure ATP](use-case-lateral-movement-path.md)
- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/aatpsizingtool)
- [Arquitetura do Azure ATP](atp-architecture.md)
- [Instalar o ATP](install-atp-step1.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)

