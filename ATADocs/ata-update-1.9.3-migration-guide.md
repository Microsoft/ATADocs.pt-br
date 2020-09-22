---
title: Atualização do Advanced Threat Analytics para o guia de migração do 1.9.3
description: Procedimento para atualizar o ATA para a versão 1.9.3
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/14/2020
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: 58866e849b15a36a3f9be843a3195d4e5b248635
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90909755"
---
# <a name="ata-version-193"></a>Versão 1.9.3 do ATA

[!INCLUDE [Rebranding notice](includes/rebranding.md)]
Estamos felizes em anunciar a disponibilidade do Microsoft Advanced Threat Analytics 1,9 atualização 3.

Este artigo descreve os problemas corrigidos na atualização 3 do Microsoft Advanced Threat Analytics (ATA) versão 1,9. O número de Build desta atualização é 1.9.7561.

## <a name="improvements-included-in-this-update"></a>Aprimoramentos incluídos nessa atualização

- Atualizado o MongoDB para a versão 3.6.18 para melhorar a compatibilidade e atualizações de segurança.
- Atualização da inicialização e do jQuery NPM pacotes para a versão 3.4.1 para atualizações de segurança.
- Recursos de acessibilidade do portal aprimorados.
- Aviso de adiantamento melhorado para a expiração do certificado central para três meses antes da expiração (anteriormente, três semanas). Além disso, o aviso agora fornece uma descrição mais clara da severidade de falha ao renovar o certificado.
- Detalhes aprimorados fornecidos com erros de verificação de credencial ao testar conexões de serviços de diretório.
- O log de erros agora contém informações mais detalhadas se houver problemas relacionados ao contador de desempenho.
- O log de implantação agora contém informações mais detalhadas sobre problemas de conexão durante a implantação do gateway.
- Aprimoramentos de desempenho gerais.

## <a name="fixed-issues-included-in-this-update"></a>Problemas corrigidos incluídos nessa atualização

- Corrige um problema em que as permissões de log de segurança não são definidas corretamente para algumas implantações.
- Corrige um problema no qual algumas traduções estão ausentes em alguns idiomas.
- Corrige um problema no qual uma mensagem de erro pode aparecer quando você navega por uma página de perfil de conta.
- Corrige um problema em que alguns recursos de acessibilidade não funcionam corretamente.

## <a name="how-to-get-this-update"></a>Como obter essa atualização

As atualizações para o Microsoft ATA estão disponíveis em Microsoft Update ou por download manual.

### <a name="microsoft-update"></a>Microsoft Update

Essa atualização está disponível no Microsoft Update. Para obter mais informações sobre como usar o Microsoft Update, confira [Como obter uma atualização pelo Windows Update](https://support.microsoft.com/help/3067639).

### <a name="microsoft-download-center"></a>Centro de Download da Microsoft

Para obter o pacote autônomo para esta atualização, vá para o site do centro de download da Microsoft: [Baixe o pacote 1.9.3 do ATA agora](https://www.microsoft.com/download/details.aspx?id=56725).

### <a name="prerequisites"></a>Pré-requisitos

Para instalar esta atualização, é necessário ter uma das seguintes versões do ATA instalada:

- Atualização 2 para o ATA 1,9 (versão 1.9.7478)
- Atualização 2 para o ATA 1,9 (versão 1.9.7475)
- Atualização 1 para o ATA 1.9 (versão 1.9.7412)
- ATA 1.9 (versão 1.9.7312)
- Atualização 1 para o ATA 1.8 (versão 1.8.6765)
- ATA 1.8 (versão 1.8.6645)

### <a name="restart-requirement"></a>Requisitos de reinicialização

Pode ser necessário reiniciar o computador após aplicar esta atualização.

### <a name="update-replacement-information"></a>Atualizar informações de substituição

Esta atualização substitui a atualização 2 para o ATA 1,9 (versão 1.9.7478).

## <a name="see-also"></a>Confira também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Versões do ATA](ata-versions.md)
