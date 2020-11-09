---
title: Validar o espelhamento de porta no Microsoft Defender para Identidade
description: Descreve como confirmar que o espelhamento de porta está configurado corretamente no Microsoft Defender para Identidade
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7a665a20da3940b3146a007eea6ee75bd35d7930
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93274042"
---
# <a name="validate-port-mirroring"></a>Validação do espelhamento de porta

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Este artigo será relevante apenas se você implantar o sensor autônomo do [!INCLUDE [Product long](includes/product-long.md)] em vez do sensor do [!INCLUDE [Product short](includes/product-short.md)].

> [!NOTE]
> Os sensores autônomos do [!INCLUDE [Product short](includes/product-short.md)] não dão suporte à coleção de entradas de log do ETW (Rastreamento de Eventos para Windows) que fornecem os dados para várias detecções. Para cobertura completa do seu ambiente, recomendamos implantar o sensor do [!INCLUDE [Product short](includes/product-short.md)].

As etapas a seguir guiarão você pelo processo de validação da configuração correta do espelhamento de porta. Para que o [!INCLUDE [Product short](includes/product-short.md)] funcione corretamente, o sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] deve ter capacidade de reconhecer o tráfego de entrada e saída do controlador de domínio. A fonte de dados principal usada pelo [!INCLUDE [Product short](includes/product-short.md)] é uma inspeção profunda de pacotes do tráfego de rede proveniente dos controladores de domínio e direcionado a eles. Para o [!INCLUDE [Product short](includes/product-short.md)] ver o tráfego de rede, o espelhamento de porta precisa ser configurado. O espelhamento de porta copia o tráfego de uma porta (de origem) para outra porta (de destino).

## <a name="validate-port-mirroring-using-net-mon"></a>Validar o espelhamento de porta usando Net Mon

1. Instale o [Monitor de Rede da Microsoft 3.4](https://www.microsoft.com/download/details.aspx?id=4865) no sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] que você deseja validar.

    > [!IMPORTANT]
    > Se optar por instalar o Wireshark a fim de validar o espelhamento de porta, reinicie o serviço do sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] após a validação.

1. Abra o Monitor de Rede e crie uma nova guia de captura.

    1. Selecione apenas o adaptador de rede de **captura** ou o adaptador de rede que estiver conectado à porta do comutador configurado como o destino do espelhamento de porta.

    1. Verifique se o Modo-P está habilitado.

    1. Clique em **Nova captura**.

        ![Criar nova imagem da guia de captura](media/port-mirroring-capture.png)

1. Na janela Exibir Filtro, insira o seguinte filtro: **KerberosV5 OU LDAP** e clique em **Aplicar**.

    ![Aplicar imagem de filtro KerberosV5 ou LDAP](media/port-mirroring-filter-settings.png)

1. Clique em **Iniciar** para iniciar a sessão de captura. Se você não vir o tráfego para e do controlador de domínio, examine a configuração do espelhamento de porta.

    ![Iniciar a captura de imagem de sessão](media/port-mirroring-capture-traffic.png)

    > [!NOTE]
    > É importante ter certeza de que você vê o tráfego para e dos controladores de domínio.

1. Se você vir o tráfego apenas em uma direção, você deve trabalhar com as equipes de rede ou de virtualização para ajudar a solucionar os problemas com a configuração do espelhamento de porta.

## <a name="see-also"></a>Consulte Também

- [Configurar o encaminhamento de eventos](configure-event-forwarding.md)
- [Configurar o espelhamento de porta](configure-port-mirroring.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
