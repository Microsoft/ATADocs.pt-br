---
title: Guia de início rápido – Instalar o sensor do Microsoft Defender para Identidade
description: A quarta etapa da instalação do Microsoft Defender para Identidade ajuda você a instalar o sensor do Defender para Identidade.
ms.date: 02/17/2021
ms.topic: quickstart
ms.openlocfilehash: a9837c36dcdb90dba124eda5f8d6b9f082787d74
ms.sourcegitcommit: 5bf0c6a204b71126306a0c64108eaf9cb7fc042f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/18/2021
ms.locfileid: "101097395"
---
# <a name="quickstart-install-the-microsoft-defender-for-identity-sensor"></a>Guia de início rápido: instalar o sensor do Microsoft Defender para Identidade

Neste guia de início rápido, você instalará o sensor do [!INCLUDE [Product long](includes/product-long.md)] em um controlador de domínio. Se você preferir uma instalação silenciosa, consulte o artigo [Instalação silenciosa](silent-installation.md).

## <a name="prerequisites"></a>Pré-requisitos

- Uma [instância do [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md) [conectada ao Active Directory](install-step2.md).
- Uma cópia baixada do [pacote de instalação do sensor do [!INCLUDE [Product short](includes/product-short.md)]](install-step3.md) e a chave de acesso.
- Verifique se o Microsoft .NET Framework 4.7 ou posterior está instalado no computador. Se o Microsoft .NET Framework 4.7 ou posterior não estiver instalado, o pacote de instalação do sensor do [!INCLUDE [Product short](includes/product-short.md)] o instalará, o que poderá exigir uma reinicialização do servidor.
- Para executar instalações de sensores em servidores do AD FS, caso esteja usando um SQL Server externo, configure o SQL Server para permitir que a conta de *Serviço de diretório* (**Configuração** > **Serviços de diretório** > **Nome de usuário**) tenha opções de *conexão*, *entrada* e *leitura*, bem como possa *selecionar* permissões para acessar o banco de dados **AdfsConfiguration**.

## <a name="install-the-sensor"></a>Instalar o servidor

Execute as etapas a seguir no controlador de domínio.

1. Verifique se o computador tem conectividade com pontos de extremidade relevantes do [serviço de nuvem do [!INCLUDE [Product short](includes/product-short.md)]](configure-proxy.md#enable-access-to-azure-atp-service-urls-in-the-proxy-server).
1. Extraia os arquivos de instalação do arquivo zip. A instalação diretamente do arquivo zip falhará.
1. Execute **o setup.exe do sensor do Azure ATP** com privilégios elevados (**Executar como administrador**) e siga o assistente de instalação.
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

## <a name="post-installation-steps-for-ad-fs-servers"></a>Etapas de pós-instalação para servidores do AD FS

Use as etapas a seguir para configurar o Microsoft Defender para Identidade depois de concluir a instalação do sensor em um servidor do AD FS.

1. No portal do [!INCLUDE [Product short](includes/product-short.md)], selecione a opção **Configuração**

1. Em **Sistema**, selecione a opção **Sensores**.

    ![Página de configuração do sensor do [!INCLUDE [Product short](includes/product-short.md)]](media/sensor-config.png)

1. Selecione o sensor instalado no servidor do AD FS.
1. Na janela pop-up, insira o FQDN dos controladores de domínio do resolvedor no campo **Controlador de Domínio do Resolvedor**, clique no ícone de sinal de adição **(+)** , depois em **Salvar**.  

    ![Configurar o resolvedor do sensor do AD FS do [!INCLUDE [Product short](includes/product-short.md)]](media/sensor-config-adfs-resolver.png)

    Inicializar o sensor poderá levar alguns minutos. Nesse momento, o status do serviço do sensor do AD FS deverá mudar de **interrompido** para **em execução**.

## <a name="next-steps"></a>Próximas etapas

O sensor do [!INCLUDE [Product short](includes/product-short.md)] foi projetado para ter um impacto mínimo sobre os recursos do controlador de domínio e a atividade de rede. Para criar uma avaliação de desempenho, confira [Planejar a capacidade do [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md).

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o [!INCLUDE [Product short](includes/product-short.md)] e a segurança relacionada com outras pessoas? Participe da Comunidade [[!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity) hoje mesmo!
