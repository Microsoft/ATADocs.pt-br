---
title: Monitorando controladores de domínio e sensores instalados instalados em seus controladores de domínio usando o Microsoft defender para identidade
description: Descreve como monitorar o Microsoft defender para sensores de identidade e cobertura de sensor usando o defender for Identity
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
ms.openlocfilehash: 20e02b3281480024b67a1ef5908d82586c11f955
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94849008"
---
# <a name="monitoring-your-domain-controller-coverage"></a>Monitorando a cobertura do controlador de domínio

Assim que o primeiro [!INCLUDE [Product long](includes/product-long.md)] sensor for instalado e configurado em qualquer controlador de domínio em sua rede, o [!INCLUDE [Product short](includes/product-short.md)] começará a monitorar o ambiente para controladores de domínio.

Depois que um [!INCLUDE [Product short](includes/product-short.md)] sensor é instalado e configurado em um controlador de domínio em sua rede, o sensor se comunica com o [!INCLUDE [Product short](includes/product-short.md)] serviço em uma base constante enviando o status do sensor, informações de integridade e versão e coletou Active Directory eventos e alterações.

## <a name="domain-controller-status"></a>Status do controlador de domínio

[!INCLUDE [Product short](includes/product-short.md)] monitora continuamente seu ambiente para controladores de domínio não monitorados introduzidos em seu ambiente e relata sobre eles para ajudá-lo a gerenciar a cobertura completa de seu ambiente.

1. Para verificar o status de seus controladores de domínio monitorados e não monitorados detectados e seu status, vá para a área de **configuração** do [!INCLUDE [Product short](includes/product-short.md)] portal e, na seção **sistema** , selecione **sensores**.

    ![[! INCLUIR [produto curto] (inclui/produto-curto. MD)] monitoramento de status do sensor](media/sensors-status-monitoring.png)

1. Os controladores de domínio atuais monitorados e não monitorados são exibidos na parte superior da tela. Para baixar os detalhes de status de monitoramento dos controladores de domínio, selecione **Baixar detalhes**.

O download do Excel da cobertura do controlador de domínio fornece as seguintes informações de todos os controladores de domínio detectados na sua organização:

|Título|Descrição|
|----|----|
|Nome do host|Nome do computador|
|Nome de domínio|Nome de domínio|
|Monitorado|[!INCLUDE [Product short](includes/product-short.md)] status do monitoramento|
|Tipo de sensor|[!INCLUDE [Product short](includes/product-short.md)] sensor ou [!INCLUDE [Product short](includes/product-short.md)] sensor autônomo|
|Unidade organizacional|Local dentro do Active Directory |
|Versão do sistema operacional| Versão do sistema operacional detectado|
|Endereço IP|Endereço IP detectado|

## <a name="search-domain-controllers"></a>Pesquisar controladores de domínio

Gerenciar sua frota de sensores e controladores de domínio pode ser desafiador. Para facilitar a localização e a identificação, os controladores de domínio podem ser pesquisados usando o recurso de pesquisa na [!INCLUDE [Product short](includes/product-short.md)] lista de sensores.

1. Para pesquisar os controladores de domínio, vá para a área de **configuração** do [!INCLUDE [Product short](includes/product-short.md)] portal e, na seção **sistema** , selecione **sensores**.
1. Selecione a opção de filtros na coluna **Controlador de domínio** na lista tabela do controlador de domínio.
1. Insira o nome que você deseja pesquisar. Atualmente, não há suporte para caracteres curinga no campo de pesquisa.

    ![[! INCLUIR [produto curto] (inclui/produto-curto. MD)] Pesquisar controlador de domínio](media/search-sensor.png)

> [!NOTE]
> [!INCLUDE [Product short](includes/product-short.md)] as páginas de configuração do portal podem ser modificadas [!INCLUDE [Product short](includes/product-short.md)] somente por administradores.

## <a name="see-also"></a>Consulte Também

- [Arquitetura do [!INCLUDE [Product short](includes/product-short.md)]](architecture.md)
- [Configurando [!INCLUDE [Product short](includes/product-short.md)] sensores](install-step5.md)
- [Suporte para várias florestas](multi-forest.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
