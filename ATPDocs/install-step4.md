---
title: Guia de início rápido – Instalar o sensor do Microsoft Defender para Identidade
description: A quarta etapa da instalação do Microsoft Defender para Identidade ajuda você a instalar o sensor do Defender para Identidade.
ms.date: 10/26/2020
ms.topic: quickstart
ms.openlocfilehash: 3688ace52e4581f8b94186c58c3e355e855e16d0
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96543987"
---
# <a name="quickstart-install-the-product-long-sensor"></a>Início Rápido: Instalar o servidor do [!INCLUDE [Product long](includes/product-long.md)]

Neste guia de início rápido, você instalará o sensor do [!INCLUDE [Product long](includes/product-long.md)] em um controlador de domínio. Se você preferir uma instalação silenciosa, consulte o artigo [Instalação silenciosa](silent-installation.md).

## <a name="prerequisites"></a>Pré-requisitos

- Uma [instância do [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md) [conectada ao Active Directory](install-step2.md).
- Uma cópia baixada do [pacote de instalação do sensor do [!INCLUDE [Product short](includes/product-short.md)]](install-step3.md) e a chave de acesso.
- Verifique se o Microsoft .NET Framework 4.7 ou posterior está instalado no computador. Se o Microsoft .NET Framework 4.7 ou posterior não estiver instalado, o pacote de instalação do sensor do [!INCLUDE [Product short](includes/product-short.md)] o instalará, o que poderá exigir uma reinicialização do servidor.

## <a name="install-the-sensor"></a>Instalar o servidor

Execute as etapas a seguir no controlador de domínio.

1. Confirme se o computador tem conectividade com os [pontos de extremidade de serviço de nuvem do [!INCLUDE [Product short](includes/product-short.md)]](configure-proxy.md#enable-access-to-azure-atp-service-urls-in-the-proxy-server) relevantes:
1. Extraia os arquivos de instalação do arquivo zip. A instalação diretamente do arquivo zip falhará.
1. Execute **Azure ATP sensor setup.exe** e siga o assistente de instalação.
1. Na página **Boas-vindas**, selecione seu idioma e clique em **Avançar**.

    ![Idioma de instalação do sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)]](media/sensor-install-language.png)

1. O assistente de instalação verifica automaticamente se o servidor é um controlador de domínio ou um servidor dedicado. Se ele for um controlador de domínio, o sensor do [!INCLUDE [Product short](includes/product-short.md)] será instalado. Se ele for um servidor dedicado, o sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] será instalado.

    Por exemplo, para um sensor do [!INCLUDE [Product short](includes/product-short.md)], será exibida a seguinte tela para informar você de que um sensor do [!INCLUDE [Product short](includes/product-short.md)] está instalado no servidor dedicado:

    ![Instalação do sensor do [!INCLUDE [Product short](includes/product-short.md)]](media/sensor-install-deployment-type.png)

    Clique em **Avançar**.

    > [!NOTE]
    > Um aviso será emitido se o controlador de domínio ou o servidor dedicado não atender aos requisitos mínimos de hardware para a instalação. O aviso não impede que você clique em **Avançar** e prossiga com a instalação. Essa ainda pode ser a opção ideal para a instalação do [!INCLUDE [Product short](includes/product-short.md)] em um ambiente de teste de laboratório pequeno, que não precisa de tanto espaço para o armazenamento de dados. Para ambientes de produção, recomendamos expressamente trabalhar com o guia de [planejamento da capacidade](capacity-planning.md) do [!INCLUDE [Product short](includes/product-short.md)] para verificar se os controladores de domínio ou os servidores dedicados atendem aos requisitos necessários.

1. Em **Configurar o sensor**, insira o caminho de instalação e a chave de acesso que você copiou na etapa anterior, com base em seu ambiente:

    ![Imagem de configuração do sensor do [!INCLUDE [Product short](includes/product-short.md)]](media/sensor-install-config.png)

    - Caminho da instalação: A localização em que o sensor do [!INCLUDE [Product short](includes/product-short.md)] está instalado. Por padrão, o caminho é %programfiles%\Azure Advanced Threat Protection sensor. Mantenha o valor padrão.
    - Chave de acesso: Recuperada por meio do portal do [!INCLUDE [Product short](includes/product-short.md)] na etapa anterior.

1. Clique em **Instalar**. Os seguintes componentes serão instalados e configurados durante a instalação do sensor do [!INCLUDE [Product short](includes/product-short.md)]:

    - KB 3047154 (somente para Windows Server 2012 R2)

        > [!IMPORTANT]
        >
        > - Não instale o KB 3047154 em um host de virtualização (o host que está executando a virtualização; não há problema em executá-lo em uma máquina virtual). Isso pode fazer com que o espelhamento de porta pare de funcionar corretamente.
        > - Se o Wireshark estiver instalado no computador do sensor do [!INCLUDE [Product short](includes/product-short.md)], depois de executar o Wireshark, você precisará reiniciar o sensor do [!INCLUDE [Product short](includes/product-short.md)], pois ele usa os mesmos drivers.

    - Serviço de sensor do [!INCLUDE [Product short](includes/product-short.md)] e serviço de atualizador do sensor do [!INCLUDE [Product short](includes/product-short.md)]
    - Microsoft Visual C++ 2013 Redistributable

## <a name="next-steps"></a>Próximas etapas

O sensor do [!INCLUDE [Product short](includes/product-short.md)] foi projetado para ter um impacto mínimo sobre os recursos do controlador de domínio e a atividade de rede. Para criar uma avaliação de desempenho, confira [Planejar a capacidade do [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md).

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o [!INCLUDE [Product short](includes/product-short.md)] e a segurança relacionada com outras pessoas? Participe da Comunidade [[!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity) hoje mesmo!
