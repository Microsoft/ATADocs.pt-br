---
title: O que há de novo na versão 1,5 do Advanced Threat Analytics
description: Lista as novidades na versão 1.5 do ATA e seus problemas conhecidos
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 01/23/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: a0d64aff-ca9e-4300-b3f8-eb3c8b8ae045
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 76f6c7dcd083d1e84443fefcaff4c753ea6bf272
ms.sourcegitcommit: 8c0222dc8333b5aa47430c5daee9bc7f1d82df31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81524711"
---
# <a name="whats-new-in-ata-version-15"></a>Novidades na versão 1.5 do ATA
Essas notas de versão fornecem informações sobre problemas conhecidos nesta versão da Advanced Threat Analytics.

## <a name="whats-new-in-the-ata-15-update"></a>Quais são as novidades na atualização 1.5 do ATA?
A atualização 1.5 do ATA fornece melhorias nas seguintes áreas:

-   Tempo de detecção mais rápido

-   Algoritmo de detecção automática avançado para os dispositivos NAT (conversão de endereços de rede)

-   Processo de resolução de nomes avançado para dispositivos não associados a um domínio

-   Suporte para a migração de dados durante as atualizações de produto

-   Melhor capacidade de resposta da interface do usuário para atividades suspeitas com milhares de entidades envolvidas

-   Resolução automática de alertas de integridade aprimorada

-   Contadores de desempenho adicionais para monitoramento e solução de problemas avançados

## <a name="known-issues"></a>Problemas conhecidos
A seguir estão os problemas conhecidos existentes nesta versão.

### <a name="new-ata-gateway-installation-fails"></a>Falha na instalação do novo Gateway do ATA
Depois de atualizar sua implantação do ATA para a versão 1.5, você obterá o seguinte erro ao instalar um novo Gateway do ATA: o gateway do Microsoft Advanced Threat Analytics não está instalado

![Erro de GW do ATA](media/ata-install-error.png)

<b>Solução alternativa:</b> envie um email para <ataeval@microsoft.com> e solicite etapas de solicitação alternativa.
### <a name="deployment"></a>Implantação
A pasta especificada para o "Caminho de dados do banco de dados" e "Caminho de diário do banco de dados" deve estar vazia (sem arquivos ou subpastas).
Se não estiver vazia, a implantação não poderá avançar.

### <a name="installation-from-zip-file"></a>Instalação do arquivo Zip
Ao instalar o Gateway de ATA, certifique-se de extrair os arquivos do arquivo zip para um diretório local e instalá-lo de lá. Não instale o Gateway de ATA diretamente de dentro do arquivo zip ou a instalação falhará.

### <a name="configuration"></a>Configuração
Depois de definir a configuração de um Gateway do ATA, ele é iniciado pela primeira vez, o rótulo "Não sincronizado" é exibido até o serviço ter sido totalmente iniciado, o que pode levar até 10 minutos na primeira vez que o serviço é iniciado.

### <a name="network-capture-software"></a>Software de captura de rede
No Gateway do ATA, o único software de captura de rede com suporte que pode ser instalado é o [Microsoft Network Monitor 3.4](https://www.microsoft.com/download/details.aspx?id=4865). Não instale o Microsoft Message Analyzer ou qualquer outro software de captura de rede. A instalação de outro software fará com que o Gateway de ATA pare de funcionar corretamente.

### <a name="kb-on-virtualization-host"></a>Base de dados de conhecimento sobre host de virtualização
Não instale a Base de dados de conhecimento 3047154 em um host de virtualização. Isso pode fazer com que o espelhamento de porta pare de funcionar corretamente.

## <a name="see-also"></a>Consulte Também

[Atualizar o ATA para a versão 1.5 — guia de migração](ata-update-1.5-migration-guide.md)

[Atualizar o ATA para a versão 1.6 — guia de migração](ata-update-1.6-migration-guide.md)

[Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
