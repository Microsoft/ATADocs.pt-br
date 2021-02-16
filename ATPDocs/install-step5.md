---
title: Configurar o Microsoft defender para configurações do sensor de identidade conceitual
description: A etapa cinco da instalação do Microsoft defender para identidade ajuda você a definir as configurações para o sensor autônomo do defender para identidade.
ms.date: 09/15/2019
ms.topic: how-to
ms.openlocfilehash: 42dc42caad1b76cf706cf85d34fd60f5c7a52756
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100534002"
---
# <a name="configure-microsoft-defender-for-identity-sensor-settings"></a>Configurar o Microsoft defender para configurações do sensor de identidade

Neste artigo, você aprenderá a definir corretamente [!INCLUDE [Product long](includes/product-long.md)] as configurações do sensor para começar a ver os dados. Você precisará fazer configuração e integração adicionais para aproveitar os [!INCLUDE [Product short](includes/product-short.md)] recursos completos do.

## <a name="prerequisites"></a>Pré-requisitos

- Uma [instância do [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md) [conectada ao Active Directory](install-step2.md).
- Uma cópia baixada do [pacote de instalação do sensor do [!INCLUDE [Product short](includes/product-short.md)]](install-step3.md) e a chave de acesso.

## <a name="configure-sensor-settings"></a>Definir as configurações do sensor

Após a [!INCLUDE [Product short](includes/product-short.md)] instalação do sensor, faça o seguinte para definir [!INCLUDE [Product short](includes/product-short.md)] as configurações do sensor.

1. Clique em **Iniciar** para abrir o navegador e entrar no [!INCLUDE [Product short](includes/product-short.md)] Portal.

1. No [!INCLUDE [Product short](includes/product-short.md)] portal, vá para **configuração** e, em **sistema**, selecione **sensores**.

    ![Página do sensor](media/sensor-config.png)

1. Clique no sensor que deseja configurar e insira as seguintes informações:

    ![Definir as configurações do sensor](media/sensor-config-2.png)

    - **Descrição**: Insira uma descrição para o [!INCLUDE [Product short](includes/product-short.md)] sensor (opcional).
    - **Controladores de domínio (FQDN)** (necessário para o [!INCLUDE [Product short](includes/product-short.md)] sensor autônomo, isso não pode ser alterado para o [!INCLUDE [Product short](includes/product-short.md)] sensor): Insira o FQDN completo do controlador de domínio e clique no sinal de adição para adicioná-lo à lista. Por exemplo, **dc01.contoso.com**

    As informações a seguir se aplicam aos servidores digitados na lista **Controladores de Domínio**:
    - Todos os controladores de domínio cujo tráfego está sendo monitorado por meio do espelhamento de porta pelo [!INCLUDE [Product short](includes/product-short.md)] sensor autônomo devem ser listados na lista **controladores de domínio** . Se um controlador de domínio não estiver listado em **Controladores de Domínio**, a detecção de atividades suspeitas pode não funcionar conforme o esperado.
    - Pelo menos um controlador de domínio na lista deve ser um catálogo global. Isso permite que o [!INCLUDE [Product short](includes/product-short.md)] resolva os objetos de usuário e computador em outros domínios na floresta.

    - **Capturar adaptadores de rede** (obrigatório):

    - Para [!INCLUDE [Product short](includes/product-short.md)] sensores, todos os adaptadores de rede usados para comunicação com outros computadores em sua organização.
    - Para o [!INCLUDE [Product short](includes/product-short.md)] sensor autônomo em um servidor dedicado, selecione os adaptadores de rede configurados como a porta de espelho de destino. Esses adaptadores de rede recebem o tráfego do controlador de domínio espelhado.

1. Clique em **Salvar**.

## <a name="validate-installations"></a>Validar instalações

Para validar que o [!INCLUDE [Product short](includes/product-short.md)] sensor foi implantado com êxito, verifique o seguinte:

1. Verifique se o serviço chamado **Sensor de Proteção Avançada contra Ameaças do Azure** está em execução. Depois de salvar as [!INCLUDE [Product short](includes/product-short.md)] configurações do sensor, pode levar alguns segundos para que o serviço seja iniciado.

1. Se o serviço não iniciar, examine o arquivo "Microsoft.Tri.sensor-Errors.log", localizado na seguinte pasta padrão: "%programfiles%\Azure Advanced Threat Protection sensor\Version X\Logs".

    >[!NOTE]
    > A versão das [!INCLUDE [Product short](includes/product-short.md)] atualizações com frequência, para verificar a versão mais recente, no [!INCLUDE [Product short](includes/product-short.md)] portal, vá para **configuração** e, em seguida, **sobre**.

1. Vá para a [!INCLUDE [Product short](includes/product-short.md)] URL da instância. No [!INCLUDE [Product short](includes/product-short.md)] portal, pesquise algo na barra de pesquisa, como um usuário ou grupo em seu domínio.

1. Verifique [!INCLUDE [Product short](includes/product-short.md)] a conectividade em qualquer dispositivo de domínio usando as seguintes etapas:
    1. Abra um prompt de comando
    1. Digite `nslookup`
    1. Digite **servidor** , em seguida, o FQDN ou o endereço IP do controlador de domínio em que o [!INCLUDE [Product short](includes/product-short.md)] sensor está instalado. Por exemplo, `server contosodc.contoso.azure`
        - Certifique-se de substituir ContosoDC. contoso. Azure e contoso. Azure pelo FQDN do seu [!INCLUDE [Product short](includes/product-short.md)] sensor e nome de domínio, respectivamente.
    1. Digite `ls -d contoso.azure`
    1. Repita as etapas 3 e 4 para cada sensor que você quer testar.
    1. No [!INCLUDE [Product short](includes/product-short.md)] console do, abra o perfil de entidade do computador do qual executou o teste de conectividade.
    1. Verifique a atividade lógica relacionada e confirme a conectividade.

    > [!NOTE]
    >Se o controlador de domínio que você quer testar for o primeiro sensor implantado, aguarde pelo menos 15 minutos para permitir que o back-end do banco de dados conclua a implantação inicial dos microsserviços necessários antes de tentar verificar a atividade lógica relacionada desse controlador de domínio.

## <a name="next-steps"></a>Próximas etapas

- [Configuração de proxy](configure-proxy.md)
- [Política de auditoria avançada](configure-windows-event-collection.md)
- [Configurar o [!INCLUDE [Product short](includes/product-short.md)] para realizar chamadas remotas para SAM](install-step8-samr.md)

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o [!INCLUDE [Product short](includes/product-short.md)] e a segurança relacionada com outras pessoas? Participe da Comunidade [[!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity) hoje mesmo!
