---
title: Tutorial de alerta de segurança do ATP do Azure | Microsoft Docs
d|Description: This article explains how to use and understand Azure ATP security alerts.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/13/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 671747d5-faed-4352-a871-17b58fdc6574
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f215639ea72d0c767f32bd9628e1c404da23aaa0
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196390"
---
# <a name="tutorial-understanding-security-alerts"></a>Tutorial: entendendo os alertas de segurança

Os alertas de segurança do ATP do Azure explicam em linguagem clara e com gráficos, quais atividades suspeitas foram identificadas em sua rede e os atores e os computadores envolvidos nas ameaças. Os alertas são classificados por gravidade, codificados por cor para facilitar a filtragem visual e organizados por fase de ameaça. Cada alerta foi projetado para ajudar você a entender rapidamente exatamente o que está acontecendo em sua rede. As listas de evidências dos alertas contêm links diretos para os computadores e os usuários envolvidos para ajudar a tornar suas investigações fáceis e diretas.

Neste tutorial, você aprenderá a estrutura dos alertas de segurança do ATP do Azure e como usá-los: 

> [!div class="checklist"]
> * Estrutura do alerta de segurança
> * Classificações de alerta de segurança
> * Categorias de alertas de segurança
> * Investigação avançada de alerta de segurança
> * Entidades relacionadas
> * ATP do Azure e NNR (resolução de nome de rede)


## <a name="security-alert-structure"></a>Estrutura do alerta de segurança

Cada alerta de segurança do ATP do Azure inclui:
 
- **Título do alerta** <br> Nome oficial do alerta no ATP do Azure.
- **Descrição** <br> Breve explicação do que aconteceu.
- **Evidência** <br> Informações adicionais relevantes e dados relacionados sobre o que aconteceu para ajudar no processo de investigação.
- **Download do Excel** <br> Relatório do Excel detalhado para baixar para análise

![Estrutura do alerta de segurança do ATP do Azure](media/security-alert-structure.png)

## <a name="security-alert-classifications"></a>Classificações de alerta de segurança

Após investigação adequada, todos os alertas de segurança do ATP do Azure podem ser classificados como um dos seguintes tipos de atividade:

- **TP (verdadeiro positivo)**: uma ação mal-intencionada detectada pelo ATP do Azure.

- **B-TP (verdadeiro positivo benigno)**: uma ação detectada pelo ATP do Azure que é real, mas não é mal-intencionada, como um teste de penetração ou uma atividade conhecida gerada por um aplicativo aprovado.

- **FP (falso positivo)**: um alarme falso, indicando que a atividade não ocorreu.

### <a name="is-the-security-alert-a-tp-b-tp-or-fp"></a>O alerta de segurança é um TP, B-TP ou FP

Para cada alerta, faça as seguintes perguntas para determinar a classificação de alerta e ajudar a decidir o que fazer em seguida:

1. Quão comum esse alerta de segurança específico é em seu ambiente?
2. O alerta foi disparado pelos mesmos tipos de computadores ou usuários?
   Por exemplo, servidores com a mesma função ou usuários do mesmo grupo/departamento? Se os computadores ou usuários forem similares, você poderá decidir excluí-los para evitar futuros alertas FP adicionais.

Observação: um aumento de alertas exatamente do mesmo tipo normalmente reduz o nível de suspeita/prioridade do alerta. Para alertas repetidos, verifique as configurações e use os detalhes e as definições do alerta de segurança para entender exatamente o que está acontecendo que disparou as repetições. 

## <a name="security-alert-categories"></a>Categorias de alertas de segurança

Os alertas de segurança do ATP do Azure são divididos nas categorias ou fases a seguir, assim como as fases vistas em uma cadeia de eliminação de ataque cibernético típica. Saiba mais sobre cada fase e os alertas projetados para detectar cada ataque usando os links a seguir:

- [Alertas de reconhecimento](atp-reconnaissance-alerts.md)
- [Alertas de credencial comprometida](atp-compromised-credentials-alerts.md)
- [Alertas de movimento lateral](atp-lateral-movement-alerts.md)
- [Alertas de predominância de domínio](atp-domain-dominance-alerts.md)
- [Alertas de exfiltração](atp-exfiltration-alerts.md)

## <a name="advanced-security-alert-investigation"></a>Investigação avançada de alerta de segurança

Para obter mais detalhes sobre um alerta de segurança, baixe o relatório detalhado do alerta no Excel.

1. Clique nos três pontos no canto superior direito de qualquer alerta e selecione *Detalhes do Download*.
 
O download do Excel de cada alerta do ATP do Azure fornece as seguintes informações:   
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
- Todas as atividades brutas capturadas pelos sensores do ATP do Azure relacionadas ao alerta (atividades de rede ou evento), incluindo:
  - Atividades de rede
  - Atividades de evento

![Entidades envolvidas](media/involved-entities.png)

### <a name="related-entities"></a>Entidades relacionadas

Em cada alerta, a última guia fornece as **Entidades Relacionadas**. As entidades relacionadas são todas as entidades envolvidas em uma atividade suspeita, sem a separação da "função" que tiveram no alerta. Cada entidade tem dois arquivos JSON, o JSON da entidade exclusiva e o JSON do perfil da entidade exclusiva. Use esses dois arquivos JSON para saber mais sobre a entidade e para ajudá-lo a investigar o alerta. 
 
**JSON da entidade exclusiva**
 
Inclui os dados que o ATP do Azure aprendeu com o Active Directory sobre a conta. Isso inclui todos os atributos como *Nome Diferenciado*, *SID*, <em>LockoutTime e *PasswordExpiryTime</em>. Para contas de usuário, inclui dados como *Departamento*, *Email* e *PhoneNumber*. Para contas de computador, inclui dados como *OperatingSystem*, <em>IsDomainController e *DnsName</em>.

**JSON do perfil da entidade exclusiva**

Inclui todos os dados que o ATP do Azure criou sobre o perfil da entidade. O ATP do Azure usa as atividades de rede e de evento capturadas para saber mais sobre os usuários e computadores do ambiente. O ATP do Azure cria perfis de informações relevantes por entidade. Essas informações contribuem com as funcionalidades de identificação de ameaças do ATP do Azure.

![Entidades relacionadas](media/related-entities.png)
 
### <a name="how-can-i-use-azure-atp-information-in-an-investigation"></a>Como usar as informações do ATP do Azure em uma investigação? 

As investigações podem ter o máximo possível de detalhes necessários. Aqui estão algumas ideias de maneiras de investigar usando os dados fornecidos pelo ATP do Azure.

- Verifique se todos os usuários relacionados pertencem ao mesmo grupo ou departamento.
- Os usuários relacionados compartilham recursos, aplicativos ou computadores?
- Essa é uma conta ativa, mesmo que o PasswordExpiryTime já tenha passado?

## <a name="azure-atp-and-nnr-network-name-resolution"></a>ATP do Azure e NNR (resolução de nome de rede)

As funcionalidades de detecção do ATP do Azure baseiam-se na NNR (resolução de nome de rede) para resolver os IPs para os computadores da organização. Usando a NNR, o ATP do Azure é capaz de correlacionar atividades brutas (que contêm endereços IP) e os computadores relevantes envolvidos em cada atividade. Com base nas atividades brutas, o ATP do Azure cria perfis de entidades, incluindo computadores, bem como gera alertas.

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

Para obter mais informações de como trabalhar com alertas de segurança do ATP do Azure, confira [Trabalhando com alertas de segurança](working-with-suspicious-activities.md).

## <a name="see-also"></a>Consulte Também

- [Investigar um usuário](investigate-a-user.md)
- [Investigar um computador](investigate-a-computer.md)
- [Trabalhando com caminhos de movimento lateral](use-case-lateral-movement-path.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
