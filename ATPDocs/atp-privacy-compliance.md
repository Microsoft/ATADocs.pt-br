---
title: Política de dados pessoais da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Fornece links para informações sobre como excluir informações particulares e dados pessoais do Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 224e629a-0e82-458c-bb03-b67070a9241d
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: d796acae64d6c6081eb9d55306b9c3b5fe901857
ms.sourcegitcommit: a0ebb0b6f140d4abf091ebd9d756b975b3d96b9d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54458494"
---
# <a name="azure-atp-data-security-and-privacy"></a>Privacidade e segurança de dados do Azure ATP

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="search-for-and-identify-personal-data"></a>Pesquisar e identificar dados pessoais 

Na Proteção Avançada contra Ameaças do Azure, você pode exibir dados pessoais identificáveis ​​do [portal do Azure ATP](workspace-portal.md) usando a [barra de pesquisa](workspace-portal.md#search-bar). 

Pesquise um usuário ou computador específico e clique na entidade para ir à [página de perfil](entity-profiles.md) do usuário ou do computador. O perfil fornece detalhes abrangentes sobre a entidade do Active Directory, incluindo atividade de rede relacionada a essa entidade e seu histórico.

Os dados pessoais do Azure ATP são coletados do Active Directory por meio do sensor do Azure ATP e armazenados em um banco de dados de back-end.

## <a name="update-personal-data"></a>Atualizar dados pessoais 

Os dados de usuário pessoais do Azure ATP são derivados do objeto do usuário no Active Directory da organização. Portanto, as alterações feitas ao perfil de usuário no AD da organização são refletidas no Azure ATP.


## <a name="delete-personal-data"></a>Excluir dados pessoais 

Depois que um usuário é excluído do Active Directory da organização, o Azure ATP exclui automaticamente o perfil de usuário e qualquer atividade de rede relacionada dentro de um ano. Você também pode [excluir](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) quaisquer alertas de segurança que contenham dados pessoais. 

## <a name="export-personal-data"></a>Exportar dados pessoais 

No Azure ATP você pode [exportar](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) as informações de alerta de segurança para o Excel. Essa função também exporta os dados pessoais. 
 
## <a name="audit-personal-data"></a>Auditar dados pessoais

O Azure ATP implementa a auditoria de alterações de dados pessoais, incluindo a exclusão e exportação de registros de dados pessoais. O tempo de retenção da trilha de auditoria é de 90 dias. A auditoria no Azure ATP é um recurso de back-end e não está acessível aos clientes.
 
## <a name="additional-resources"></a>Recursos adicionais

- Para saber mais sobre a confiança e a conformidade do Azure ATP, confira o [Portal de Confiança do Serviço](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) e o [site Conformidade do Microsoft 365 Enterprise com o RGPD](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview).
