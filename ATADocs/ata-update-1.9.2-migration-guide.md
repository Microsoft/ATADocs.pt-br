---
title: Guia de migração de atualização para a versão 1.9.2 do Advanced Threat Analytics | Microsoft Docs
description: Procedimentos para atualizar o ATA para a versão 1.9.2
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 04/02/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: d7149197933800697d26b42196dcc4c9121ea593
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2020
ms.locfileid: "75907553"
---
# <a name="ata-version-192"></a>ATA versão 1.9.2


Estamos felizes em anunciar a disponibilidade da Atualização 2 do Microsoft Advanced Threat Analytics 1.9.

Este artigo descreve os problemas corrigidos na Atualização 2 do Microsoft Advanced Threat Analytics (ATA) versão 1.9. O número do build dessa atualização é 1.9.7478.

## <a name="improvements-included-in-this-update"></a>Aprimoramentos incluídos nessa atualização

Esta atualização inclui o Windows Server 2019 (inclusive as versões Core, mas não Nano) como um sistema operacional com suporte para os componentes do gateway Centro, Gateway e Lightweight.

Esta atualização também inclui melhorias de desempenho e estabilidade, juntamente com correções de problemas relatados por clientes.

## <a name="fixed-issues-included-in-this-update"></a>Problemas corrigidos incluídos nessa atualização

- Corrige um problema em que a exibição de dados do diretório mostra o gerente direto e as associações recursivas.
- Corrige um problema em que a configuração de URL do Centro do ATA nem sempre mostra os IPs locais ou o nome do computador local.
- Corrige um problema de download de alerta de integridade quando o alerta de integridade contém um gateway inexistente.
- Corrige problemas de tradução.
- Corrige um problema em que a versão do banco de dados do MongoDB não foi atualizada.
- Corrige um cenário raro em que problemas de memória alta ocorreriam durante a sincronização do Active Directory.
- Corrige um cenário raro em que o console apenas permitia a seleção de um certificado sem suporte.
- Corrige um cenário raro em que uma instância de falso positivo da mensagem “Suspeita de roubo de identidade com base no comportamento anormal” era recebida.
- Corrige um caso raro em que ocorria um salto na linha do tempo quando os alertas eram atualizados automaticamente.

## <a name="get-this-update"></a>Obter essa atualização

Para obter o pacote autônomo para esta atualização, vá para o site do centro de download da Microsoft: [Baixe o pacote 1.9.2 do ATA agora](https://www.microsoft.com/en-us/download/details.aspx?id=56725).

### <a name="prerequisites"></a>Pré-requisitos

Para instalar esta atualização, é necessário ter uma das seguintes versões do ATA instalada: 
- Atualização 1 para o ATA 1.9 (versão 1.9.7412)
- ATA 1.9 (versão 1.9.7312)
- Atualização 1 para o ATA 1.8 (versão 1.8.6765)
- ATA 1.8 (versão 1.8.6645)

### <a name="restart-requirement"></a>Requisitos de reinicialização

Pode ser necessário reiniciar o computador após aplicar esta atualização.

### <a name="update-replacement-information"></a>Atualizar informações de substituição

Esta atualização substitui a versão 1.9.1 (1.9.7412) do ATA.


## <a name="see-also"></a>Veja também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Versões do ATA](ata-versions.md)