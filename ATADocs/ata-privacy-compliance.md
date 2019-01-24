---
title: Política de dados pessoais do Advanced Threat Analytics | Microsoft Docs
description: Fornece links para informações sobre como excluir informações particulares e dados pessoais do ATA.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/27/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 1b2d185c-62cd-45f0-b0dd-687b51317f32
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: 174c3fdace1fcb1d188e3157ae5c6d2a894f1b77
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54839870"
---
# <a name="ata-data-security-and-privacy"></a>Privacidade e segurança de dados do ATA

*Aplica-se a: Advanced Threat Analytics versão 1.9*

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="searching-for-and-identifying-personal-data"></a>Pesquisando e identificando dados pessoais 

Todos os dados no ATA relacionados a entidades são derivados do AD (Active Directory) e replicados para o ATA. Ao pesquisar dados pessoais, o primeiro local que você deve considerar para a pesquisa é o AD. 

No Centro do ATA, use a barra de pesquisa para exibir os dados de identificação pessoais que estão armazenados no banco de dados. Os usuários podem pesquisar um usuário ou dispositivo específico. Clicar na entidade abrirá a página de perfil do dispositivo ou do usuário. O perfil fornece detalhes abrangentes sobre a entidade, seu histórico e a atividade de rede relacionada, derivados do AD. 

## <a name="updating-personal-data"></a>Atualizando dados pessoais 

Os dados pessoais sobre usuários e entidades no ATA são derivados do objeto do usuário no AD da organização. Por isso, as alterações feitas no perfil do usuário no AD são refletidas no ATA. 

## <a name="deleting-personal-data"></a>Excluindo dados pessoais 

Embora os dados no ATA sejam replicados e sempre atualizados do AD, quando uma entidade é excluída no AD, os dados da entidade no ATA são mantidos para fins de investigação de segurança. 

Para excluir permanentemente os dados relacionados ao usuário do banco de dados do ATA, siga este procedimento: 

1. [Baixe](https://aka.ms/ata-gdpr-script) o script do MongoDB (gdpr.js).  

2. Copie o script para a pasta do ATA (localizada em `"C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB` e execute o seguinte comando no computador do ATA Center: 

Use o script do banco de dados do ATA GDPR para excluir entidades e dados de atividade de entidades, conforme é descrito nas seções a seguir.

### <a name="delete-entities"></a>Excluir entidades

Essa ação exclui permanentemente uma entidade do banco de dados do ATA. Para executar esse comando, forneça o nome do comando `deleteAccount` e o `SamName`, `UpnName` ou `GUID` do computador ou o nome de usuário que deseja excluir. Por exemplo: 

`"C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval "var params='deleteAccount,admin1@contoso.com';" GDPR.js`

A execução completa desse comando remove a entidade com o UPN admin1@contoso.com do banco de dados, juntamente com todas as atividades e os alertas de segurança associados à entidade. 

### <a name="delete-entity-activity-data"></a>Excluir dados de atividade da entidade

Essa ação exclui permanentemente os dados de atividades de uma entidade do banco de dados do ATA. Todas as entidades permanecem inalteradas, mas as atividades e os alertas de segurança relacionados a elas no período de tempo especificado são excluídos. 

Para executar esse comando, forneça o nome do comando `deleteOldData` e o número de dias de dados que você deseja manter no banco de dados. 

Por exemplo: 

`"C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongo.exe" ATA --eval "var params='deleteOldData,30';" GDPR.js`

Esse script remove do banco de dados todos os dados de todas as atividades e alertas de segurança da entidade com mais de 30 dias. Somente os últimos 30 dias de dados serão retidos.

## <a name="exporting-personal-data"></a>Exportando dados pessoais 

Como os dados relacionados a entidades no ATA são derivados do AD, apenas um subconjunto desses dados é armazenado no banco de dados do ATA. Por esse motivo, você deve exportar os dados relacionados a entidades do AD. 

O ATA permite que você exporte para o Excel todas as informações relacionadas à segurança, que podem incluir dados pessoais. 

 
## <a name="opt-out-of-system-generated-logs"></a>Desativar logs gerados pelo sistema 

O ATA coleta logs anônimos gerados pelo sistema sobre cada implantação e transmite esses dados por HTTPS aos servidores da Microsoft. Esses dados são usados pela Microsoft para ajudar a melhorar as versões futuras do ATA. 

Para obter mais informações, confira [Gerenciar logs gerados pelo sistema](manage-telemetry-settings.md).

Para desabilitar a coleta de dados:

1. Faça logon no Console do ATA, clique nos três pontos na barra de ferramentas e escolha **Sobre**. 
2. Desmarque a caixa para **Envie informações de uso para ajudar a melhorar a experiência do cliente no futuro**. 

## <a name="additional-resources"></a>Recursos adicionais

- Para obter informações sobre a confiança e a conformidade do ATA, confira o [Portal de Confiança do Serviço](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) e o [site Conformidade do Microsoft 365 Enterprise com o GDPR](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview).
