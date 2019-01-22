---
title: Guia de migração de atualização do Advanced Threat Analytics para 1.9.1 | Microsoft Docs
description: Procedimentos para atualizar o ATA para a versão 1.9.1
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/10/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: 80d6b2744c3299bf92d0c4082085dbd872403cc0
ms.sourcegitcommit: 9acf035f6f2ce32290e00d2e45385ae7993bb63a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53334980"
---
# <a name="ata-version-191"></a>ATA versão 1.9.1


Este artigo descreve os problemas corrigidos na Atualização 1 do Microsoft Advanced Threat Analytics (ATA) versão 1.9. O número de compilação dessa atualização é 1.9.7412.

## <a name="fixed-issues-included-in-this-update"></a>Problemas corrigidos incluídos nessa atualização

- Possibilidade de falhas na migração entre a versão 1.8 do ATA para a versão 1.9 de grandes bancos de dados.
- O navegador poderá travar caso você use a versão mais recente do navegador Microsoft Edge e alternar usuários.
- Em alguns cenários, faltam informações sobre os dados do diretório na página de perfil do usuário.
- Ao adicionar um usuário à lista de exclusão para detecção de comportamento anormal, a exclusão nem sempre será aplicada. 
- Versão atualizada do banco de dados MongoDB.
- Ressincronização inconsistente após uma atualização para a versão 1.9 de todas as entidades do Active Directory para o ATA.
- Exportações inconsistentes de atividades suspeitas para o Microsoft Excel. Falha ocasional com geração de erro.  


## <a name="improvements-included-in-this-update"></a>Aprimoramentos incluídos nessa atualização
- Alterações necessárias para a certificação de Padrões de Acessibilidade da Microsoft (MAS).
- Inclui correções de desempenho e segurança adicionais.

## <a name="get-this-update"></a>Obter essa atualização

As atualizações do Microsoft Advanced Threat Analytics versão 1.9 estão disponíveis no Microsoft Update ou por download manual.

### <a name="microsoft-update"></a>Microsoft Update
Essa atualização está disponível no Microsoft Update. Para obter mais informações sobre como usar o Microsoft Update, confira [Como obter uma atualização pelo Windows Update](https://support.microsoft.com/help/3067639).

### <a name="manual-download"></a>Download manual
Para ter acesso o pacote autônomo para essa atualização, vá para o site do Centro de Download da Microsoft: [Faça já o download do pacote do ATA 1.9](https://www.microsoft.com/en-us/download/details.aspx?id=56725).

### <a name="prerequisites"></a>Pré-requisitos
Para instalar essa atualização, você deve ter a versão 1.9 do ATA (1.9.7312), Atualização 1 para o ATA versão 1.8 (1.8.6765) ou o ATA versão 1.8 (1.8.6645) instalado.

### <a name="restart-requirement"></a>Requisitos de reinicialização
O computador pode exigir uma reinicialização depois de aplicar essa atualização.

### <a name="update-replacement-information"></a>Atualizar informações de substituição
Esta atualização substitui o ATA versão 1.9 (1.9.7312).


## <a name="see-also"></a>Consulte também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Versões do ATA](ata-versions.md)