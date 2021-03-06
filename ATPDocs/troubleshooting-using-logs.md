---
title: Solução de problemas do Microsoft defender para identidade usando os logs
description: Descreve como você pode usar o Microsoft defender para logs de identidade para solucionar problemas
ms.date: 10/27/2020
ms.topic: how-to
ms.openlocfilehash: 2c902576b4cf7b0acf58371bafe4bb60404890ba
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100534507"
---
# <a name="troubleshooting-microsoft-defender-for-identity-sensor-using-the-defender-for-identity-logs"></a>Solucionando problemas do Microsoft defender for Identity sensor usando o defender para logs de identidade

Os [!INCLUDE [Product short](includes/product-short.md)] logs fornecem informações sobre o que cada componente do [!INCLUDE [Product long](includes/product-long.md)] sensor está fazendo em qualquer momento determinado.

Os [!INCLUDE [Product short](includes/product-short.md)] logs estão localizados em uma subpasta chamada **logs** onde [!INCLUDE [Product short](includes/product-short.md)] o está instalado; o local padrão é: **C:\Program programas\azure Advanced Threat \\ Protection sensor**. No local de instalação padrão, ela pode ser encontrada em: **C:\Program Files\Azure Advanced Threat Protection Sensor\version number\Logs**.

O [!INCLUDE [Product short](includes/product-short.md)] sensor tem os seguintes logs:

- **Microsoft. Tri. sensor. log** – esse log contém tudo o que acontece no [!INCLUDE [Product short](includes/product-short.md)] sensor (incluindo resolução e erros). Usado principalmente para obter o status geral de todas as operações em ordem cronológica de ocorrência.

- **Microsoft. Tri. sensor-Errors. log** – esse log contém apenas os erros que são capturados pelo [!INCLUDE [Product short](includes/product-short.md)] sensor. Usado principalmente para executar verificações de integridade e investigar problemas que precisam estar correlacionados a horários específicos.

- **Microsoft. Tri. sensor. Updater. log** -esse log é usado para o processo do atualizador do sensor, que é responsável por atualizar o [!INCLUDE [Product short](includes/product-short.md)] sensor, se configurado para fazer isso automaticamente.

> [!NOTE]
> Os três primeiros arquivos de log têm um tamanho máximo de até 50 MB. Quando esse tamanho é atingido, um novo arquivo de log é aberto e o anterior é renomeado como "&lt;nome do arquivo original&gt;-Archived-00000". Esse número aumenta a cada renomeação. Por padrão, se já houver mais de 10 arquivos do mesmo tipo, os mais antigos serão excluídos.

## <a name="defender-for-identity-deployment-logs"></a>Logs de implantação do defender for Identity

Os [!INCLUDE [Product short](includes/product-short.md)] logs de implantação estão localizados no diretório Temp do usuário que instalou o produto. No local de instalação padrão, ele pode ser encontrado em: **C:\Users\Administrator\AppData\Local\Temp** (ou em um diretório acima de% Temp%).

[!INCLUDE [Product short](includes/product-short.md)] logs de implantação de sensor:

- **Proteção Avançada contra Ameaças do Azure Microsoft.Tri.Sensor.Deployment.Deployer_YYYYMMDDHHMMSS.log** - esse arquivo de log fornece todo o processo de implantação do sensor e pode ser encontrado na pasta temporária mencionada anteriormente ou em C:\Windows\Temp.

- **Proteção avançada contra ameaças do Azure Sensor_YYYYMMDDHHMMSS. log** – esse log lista as etapas no processo de implantação do [!INCLUDE [Product short](includes/product-short.md)] sensor. Seu principal uso é acompanhar o [!INCLUDE [Product short](includes/product-short.md)] processo de implantação do sensor.

- **Proteção avançada contra ameaças do Azure Sensor_YYYYMMDDHHMMSS_001_MsiPackage. log** -esse arquivo de log lista as etapas no processo de implantação dos [!INCLUDE [Product short](includes/product-short.md)] binários do sensor. Seu principal uso é acompanhar a implantação dos [!INCLUDE [Product short](includes/product-short.md)] binários do sensor.

> [!NOTE]
> Além dos logs de implantação mencionados aqui, há outros logs que começam com "Proteção Avançada contra Ameaças ao Azure" que também pode fornecer informações adicionais sobre o processo de implantação.

## <a name="see-also"></a>Consulte Também

- [Pré-requisitos do [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Planejamento de capacidade do [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
