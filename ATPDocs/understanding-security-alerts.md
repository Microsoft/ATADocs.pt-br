---
title: Tutorial de alertas de segurança do Microsoft Defender para Identidade
description: Este artigo explica como usar e compreender os alertas de segurança do Microsoft Defender para Identidade.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 27df0fb3be637b2a3390df9378f68b2db9a10b8d
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848900"
---
# <a name="understanding-security-alerts"></a>entendendo os alertas de segurança

Os alertas de segurança do [!INCLUDE [Product long](includes/product-long.md)] explicam em linguagem clara e com elementos gráficos quais atividades suspeitas foram identificadas em sua rede e os atores e computadores envolvidos nas ameaças. Os alertas são classificados por gravidade, codificados por cor para facilitar a filtragem visual e organizados por fase de ameaça. Cada alerta foi projetado para ajudar você a entender rapidamente exatamente o que está acontecendo em sua rede. As listas de evidências dos alertas contêm links diretos para os computadores e os usuários envolvidos para ajudar a tornar suas investigações fáceis e diretas.

Neste tutorial, você aprenderá a estrutura dos alertas de segurança do [!INCLUDE [Product short](includes/product-short.md)] e como usá-los:

> [!div class="checklist"]
>
> - Estrutura do alerta de segurança
> - Classificações de alerta de segurança
> - Categorias de alertas de segurança
> - Investigação avançada de alerta de segurança
> - Entidades relacionadas
> - [!INCLUDE [Product short](includes/product-short.md)] e NNR (resolução de nomes de rede)

## <a name="security-alert-structure"></a>Estrutura do alerta de segurança

Cada alerta de segurança do [!INCLUDE [Product short](includes/product-short.md)] inclui:

- **Título do alerta**  
Nome oficial do alerta do [!INCLUDE [Product short](includes/product-short.md)].
- **Descrição**  
Breve explicação do que aconteceu.
- **Evidência**  
Informações adicionais relevantes e dados relacionados sobre o que aconteceu para ajudar no processo de investigação.
- **Download do Excel**  
Relatório do Excel detalhado para baixar para análise

![Estrutura de alerta de segurança do [!INCLUDE [Product short](includes/product-short.md)]](media/security-alert-structure.png)

## <a name="security-alert-classifications"></a>Classificações de alerta de segurança

Após investigação adequada, todos os alertas de segurança do [!INCLUDE [Product short](includes/product-short.md)] podem ser classificados como um dos seguintes tipos de atividade:

- **TP (verdadeiro positivo)** : uma ação mal-intencionada detectada pelo [!INCLUDE [Product short](includes/product-short.md)].

- **B-TP (verdadeiro positivo benigno)** : uma ação detectada pelo [!INCLUDE [Product short](includes/product-short.md)] que é real, mas não é mal-intencionada, como um teste de penetração ou uma atividade conhecida gerada por um aplicativo aprovado.

- **FP (falso positivo)** : alarme falso, o que significa que a atividade não ocorreu.

### <a name="is-the-security-alert-a-tp-b-tp-or-fp"></a>O alerta de segurança é um TP, B-TP ou FP

Para cada alerta, faça as seguintes perguntas para determinar a classificação de alerta e ajudar a decidir o que fazer em seguida:

1. Quão comum esse alerta de segurança específico é em seu ambiente?
1. O alerta foi disparado pelos mesmos tipos de computadores ou usuários?
   Por exemplo, servidores com a mesma função ou usuários do mesmo grupo/departamento? Se os computadores ou usuários forem similares, você poderá decidir excluí-los para evitar futuros alertas FP adicionais.

Observação: um aumento de alertas exatamente do mesmo tipo normalmente reduz o nível de suspeita/prioridade do alerta. Para alertas repetidos, verifique as configurações e use os detalhes e as definições do alerta de segurança para entender exatamente o que está acontecendo que disparou as repetições.

## <a name="security-alert-categories"></a>Categorias de alertas de segurança

Os alertas de segurança do [!INCLUDE [Product short](includes/product-short.md)] são divididos nas categorias ou fases a seguir, assim como as fases encontradas em uma cadeia de eliminação de ataque cibernético típica. Saiba mais sobre cada fase e os alertas projetados para detectar cada ataque usando os links a seguir:

- [Alertas de reconhecimento](reconnaissance-alerts.md)
- [Alertas de credencial comprometida](compromised-credentials-alerts.md)
- [Alertas de movimento lateral](lateral-movement-alerts.md)
- [Alertas de predominância de domínio](domain-dominance-alerts.md)
- [Alertas de exfiltração](exfiltration-alerts.md)

## <a name="advanced-security-alert-investigation"></a>Investigação avançada de alerta de segurança

Para obter mais detalhes sobre um alerta de segurança, baixe o relatório detalhado do alerta no Excel.

1. Clique nos três pontos no canto superior direito de qualquer alerta e selecione *Detalhes do Download*.

O download do Excel de cada alerta do [!INCLUDE [Product short](includes/product-short.md)] fornece as seguintes informações:

- Resumo – a primeira guia inclui os destaques do alerta
  - Título
  - Descrição
  - Hora de início (UTC)
  - Hora de término (UTC)
  - Gravidade – baixa/média/alta
  - Status – aberto/fechado
  - Hora da atualização de status (UTC)
  - Exibir no navegador
- Todas as entidades envolvidas (contas, computadores e recursos) são listadas, separadas por função.
  - Origem, destino ou atacado, dependendo do alerta.
- A maioria das guias inclui os seguintes dados por entidade:
  - Nome
  - Detalhes
  - Tipo
  - SamName
  - Computador de Origem
  - Usuário de origem (se disponível)
  - Controladores de Domínio
  - Recurso acessado: Tempo, Computador, Nome, Detalhes, Tipo, Serviço.
  - Guias adicionais por alerta:
    - Nas contas atacadas, quando o ataque suspeito usou força bruta.
    - Nos servidores DNS (Sistema de Nomes de Domínio) quando a suspeita de ataque envolveu reconhecimento de mapeamento de rede (DNS).
  - Entidades relacionadas: ID, Tipo, Nome, JSON da Entidade Exclusiva, JSON do Perfil da Entidade Exclusiva
- Todas as atividades brutas capturadas pelos sensores do [!INCLUDE [Product short](includes/product-short.md)] relacionadas ao alerta (atividades de rede ou evento), incluindo:
  - Atividades de rede
  - Atividades de evento

![Entidades envolvidas](media/involved-entities.png)

### <a name="related-entities"></a>Entidades relacionadas

Em cada alerta, a última guia fornece as **Entidades Relacionadas**. As entidades relacionadas são todas aquelas envolvidas em uma atividade suspeita, sem a separação da "função" que desempenharam no alerta. Cada entidade tem dois arquivos JSON, o JSON da entidade exclusiva e o JSON do perfil da entidade exclusiva. Use esses dois arquivos JSON para saber mais sobre a entidade e para ajudá-lo a investigar o alerta.

**JSON da entidade exclusiva**

Inclui os dados que o [!INCLUDE [Product short](includes/product-short.md)] aprendeu com o Active Directory sobre a conta. Isso inclui todos os atributos como *Distinguished Name*, *SID*, *LockoutTime* e *PasswordExpiryTime*. Para contas de usuário, inclui dados como *Departamento*, *Email* e *PhoneNumber*. Para contas de computador, inclui dados como *OperatingSystem*, *IsDomainController* e *DnsName*.

**JSON do perfil da entidade exclusiva**

Inclui todos os dados que o [!INCLUDE [Product short](includes/product-short.md)] criou sobre o perfil da entidade. O [!INCLUDE [Product short](includes/product-short.md)] usa as atividades de rede e de evento capturadas para saber mais sobre os usuários e computadores do ambiente. O [!INCLUDE [Product short](includes/product-short.md)] cria perfis de informações relevantes por entidade. Essas informações contribuem com as funcionalidades de identificação de ameaças do [!INCLUDE [Product short](includes/product-short.md)].

![Entidades relacionadas](media/related-entities.png)

### <a name="how-can-i-use-product-short-information-in-an-investigation"></a>Como posso usar as informações do [!INCLUDE [Product short](includes/product-short.md)] em uma investigação?

As investigações podem ter o máximo possível de detalhes necessários. Confira algumas ideias de maneiras de investigar usando os dados fornecidos pelo [!INCLUDE [Product short](includes/product-short.md)].

- Verifique se todos os usuários relacionados pertencem ao mesmo grupo ou departamento.
- Os usuários relacionados compartilham recursos, aplicativos ou computadores?
- Essa é uma conta ativa, mesmo que o PasswordExpiryTime já tenha passado?

## <a name="product-short-and-nnr-network-name-resolution"></a>[!INCLUDE [Product short](includes/product-short.md)] e NNR (resolução de nomes de rede)

As funcionalidades de detecção do [!INCLUDE [Product short](includes/product-short.md)] baseiam-se na NNR (resolução de nomes de rede) a fim de resolver os IPs para os computadores da organização. Usando a NNR, o [!INCLUDE [Product short](includes/product-short.md)] consegue correlacionar atividades brutas (que contêm endereços IP) e os computadores relevantes envolvidos em cada atividade. Com base nas atividades brutas, o [!INCLUDE [Product short](includes/product-short.md)] cria perfis de entidades, incluindo computadores, e gera alertas.

Os dados de NNR são cruciais para detectar os seguintes alertas:

- Suspeita de roubo de identidade (Pass-the-Ticket)
- Suspeita de ataque de DCSync (replicação de serviços de diretório)
- Reconhecimento de mapeamento de rede (DNS)

Use as informações de NNR fornecidas na guia **Atividades de Rede** do relatório de download do alerta para determinar se um alerta é um **FP**. Em caso de alerta **FP**, é comum que o resultado de certeza de NNR seja fornecido com confiança baixa.

Os dados do relatório de download aparecem em duas colunas:

- **Computador de origem/destino**

  - *Certeza* – a certeza de baixa resolução pode indicar uma resolução de nomes incorreta.
- **Computador de origem/destino**
  - *Método de resolução* – fornece os métodos de NNR usados para resolver o IP para o computador da organização.

![Atividades de rede](media/network-activities.png)

Para saber mais sobre como trabalhar com alertas de segurança do [!INCLUDE [Product short](includes/product-short.md)], confira [Trabalhar com alertas de segurança](working-with-suspicious-activities.md).

## <a name="see-also"></a>Consulte Também

- [Investigar um usuário](investigate-a-user.md)
- [Investigar um computador](investigate-a-computer.md)
- [Trabalhando com caminhos de movimento lateral](use-case-lateral-movement-path.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
