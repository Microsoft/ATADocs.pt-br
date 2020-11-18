---
title: Política de dados pessoais do Microsoft defender para identidade
description: Fornece links para informações sobre como excluir informações particulares e dados pessoais do Microsoft defender para identidade.
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: ophir
ms.suite: ems
ms.openlocfilehash: 648d12d6135e5ab09319580142807f930e595eda
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94846962"
---
# <a name="product-long-data-security-and-privacy"></a>[!INCLUDE [Product long](includes/product-long.md)] segurança e privacidade de dados

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="search-for-and-identify-personal-data"></a>Pesquisar e identificar dados pessoais

No [!INCLUDE [Product short](includes/product-short.md)] , você pode exibir dados pessoais identificáveis no [ [!INCLUDE [Product long](includes/product-long.md)] portal](workspace-portal.md) usando a [barra de pesquisa](workspace-portal.md#search-bar).

Pesquise um usuário ou computador específico e clique na entidade para ir à [página de perfil](entity-profiles.md) do usuário ou do computador. O perfil fornece detalhes abrangentes sobre a entidade do Active Directory, incluindo atividade de rede relacionada a essa entidade e seu histórico.

[!INCLUDE [Product short](includes/product-short.md)] os dados pessoais são coletados de Active Directory por meio do [!INCLUDE [Product short](includes/product-short.md)] sensor e armazenados em um banco de dados de back-end.

## <a name="update-personal-data"></a>Atualizar dados pessoais

[!INCLUDE [Product short](includes/product-short.md)]os dados pessoais do usuário são derivados do objeto do usuário no Active Directory da organização. Portanto, as alterações feitas no perfil do usuário no AD da organização são refletidas no [!INCLUDE [Product short](includes/product-short.md)] .

## <a name="delete-personal-data"></a>Excluir dados pessoais

- Depois que um usuário é excluído da Active Directory da organização, [!INCLUDE [Product short](includes/product-short.md)] o exclui automaticamente o perfil do usuário e qualquer atividade de rede relacionada em um ano. Você também pode [excluir](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) quaisquer alertas de segurança que contenham dados pessoais.

- Recomendam-se permissões **somente leitura** no contêiner de **Objetos Excluídos**. Para saber mais sobre como a permissão de contêiner de objetos * * excluídos é usada pelo [!INCLUDE [Product short](includes/product-short.md)] serviço, consulte a recomendação de contêiner de objetos excluídos em [ [!INCLUDE [Product short](includes/product-short.md)] pré-requisitos](prerequisites.md#before-you-start).

## <a name="export-personal-data"></a>Exportar dados pessoais

No [!INCLUDE [Product short](includes/product-short.md)] , você tem a capacidade de [Exportar](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) informações de alerta de segurança para o Excel. Essa função também exporta os dados pessoais.

## <a name="audit-personal-data"></a>Auditar dados pessoais

[!INCLUDE [Product short](includes/product-short.md)] implementa a auditoria de alterações de dados pessoais, incluindo a exclusão e a exportação de registros de dados pessoais. O tempo de retenção da trilha de auditoria é de 90 dias. A auditoria no [!INCLUDE [Product short](includes/product-short.md)] é um recurso de back-end e não acessível aos clientes.

## <a name="additional-resources"></a>Recursos adicionais

- Para obter informações sobre [!INCLUDE [Product short](includes/product-short.md)] confiança e conformidade, consulte o [portal de confiança do serviço](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) e o site de conformidade do [Microsoft 365 Enterprise GDPR](/microsoft-365/compliance/gdpr?view=o365-worldwide&preserve-view=true).

## <a name="security-and-privacy-for-product-short-us-government-gcc-high-customers"></a>Segurança e privacidade para [!INCLUDE [Product short](includes/product-short.md)] clientes do governo dos EUA gcc High

Para obter informações adicionais sobre [!INCLUDE [Product short](includes/product-short.md)] os padrões de conformidade e o local dos dados do cliente para clientes de gcc do governo dos EUA, consulte o [Enterprise Mobility + Security para a descrição do serviço do governo dos EUA](/enterprise-mobility-security/solutions/ems-govt-service-description).
