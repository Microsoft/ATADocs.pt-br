---
title: Guia de início rápido – Criar sua instância do Microsoft Defender para Identidade
description: Guia de início rápido para a criação da instância da sua implantação do Microsoft Defender para Identidade, que é a primeira etapa para instalar o Defender para Identidade.
ms.date: 10/26/2020
ms.topic: quickstart
ms.openlocfilehash: 9860a8893ac16448b92961df9cf25801f68786b6
ms.sourcegitcommit: af41733212c2102c223fed8c8602a21a1f667080
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100515352"
---
# <a name="quickstart-create-your-product-long-instance"></a>Início Rápido: Criar sua instância do [!INCLUDE [Product long](includes/product-long.md)]

Neste guia de início rápido, você criará sua instância do [!INCLUDE [Product long](includes/product-long.md)] no portal do [!INCLUDE [Product short](includes/product-short.md)]. No [!INCLUDE [Product short](includes/product-short.md)], você terá uma só instância, anteriormente chamada de workspace. Uma única instância permite gerenciar várias florestas em um único painel de exibição.

> [!IMPORTANT]
> No momento, os data centers do [!INCLUDE [Product short](includes/product-short.md)] estão implantados na Europa, no Reino Unido, na América do Norte/América Central/Caribe e na Ásia. A instância é criada automaticamente no data center geograficamente mais próximo ao seu Azure AD (Azure Active Directory). Depois de criadas, as instâncias do [!INCLUDE [Product short](includes/product-short.md)] não poderão ser movidas.

## <a name="prerequisites"></a>Pré-requisitos

- Uma [licença do [!INCLUDE [Product long](includes/product-long.md)]](technical-faq.yml#licensing-and-privacy).
- Você precisará ser um [administrador global ou um administrador da segurança no locatário](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#available-roles) para acessar o portal do [!INCLUDE [Product short](includes/product-short.md)].
- Examine o artigo [Arquitetura do [!INCLUDE [Product short](includes/product-short.md)]](architecture.md).
- Examine o artigo [Pré-requisitos do [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md).

## <a name="sign-in-to-the-product-short-portal"></a>Entre no portal do [!INCLUDE [Product short](includes/product-short.md)]

Depois de verificar que a sua rede atende aos requisitos do sensor, inicie a criação da instância do [!INCLUDE [Product short](includes/product-short.md)].

1. Acesse o [portal do [!INCLUDE [Product short](includes/product-short.md)]](https://portal.atp.azure.com)*.

1. Entre com sua conta de usuário do Azure Active Directory.

\* Os clientes do GCC High precisam usar o portal do [[!INCLUDE [Product short](includes/product-short.md)] GCC High](http://portal.atp.azure.us).

## <a name="create-your-instance"></a>Criar sua instância

1. Clique em **Criar instância**.

    ![Criar uma instância do [!INCLUDE [Product short](includes/product-short.md)]](media/create-instance.png)

1. Sua instância do [!INCLUDE [Product short](includes/product-short.md)] é nomeada automaticamente com o nome de domínio inicial do Azure AD e criada no data center mais próximo do seu Azure AD.

    ![Instância do Azure criada](media/instance-created.png)

    > [!NOTE]
    > Para entrar no [!INCLUDE [Product short](includes/product-short.md)], você precisará se conectar com um usuário que recebeu uma função do [!INCLUDE [Product short](includes/product-short.md)] com direitos para acessar o portal do [!INCLUDE [Product short](includes/product-short.md)]. Para saber mais sobre RBAC (controle de acesso baseado em função) no [!INCLUDE [Product short](includes/product-short.md)], confira [Trabalhar com grupos de função do [!INCLUDE [Product short](includes/product-short.md)]](role-groups.md).

1. Selecione **Configuração**, **Gerenciar grupos de funções** e use o link [Centro de Administração do Azure AD](/azure/active-directory/active-directory-assign-admin-roles-azure-portal) para gerenciar seus grupos de funções.

    ![Gerenciar grupos de funções](media/creation-manage-role-groups.png)

- Retenção de dados: as instâncias do [!INCLUDE [Product short](includes/product-short.md)] já excluídas não são exibidas na interface do usuário. Para obter mais informações sobre a retenção de dados do [!INCLUDE [Product short](includes/product-short.md)], confira [Privacidade e segurança de dados do [!INCLUDE [Product short](includes/product-short.md)]](privacy-compliance.md).

## <a name="next-steps"></a>Próximas etapas

> [!div class="step-by-step"]
> [« Pré-requisitos](prerequisites.md)
> [Etapa 2 — Conectar ao Active Directory »](install-step2.md)

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o [!INCLUDE [Product short](includes/product-short.md)] e a segurança relacionada com outras pessoas? Participe da Comunidade [[!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity) hoje mesmo!
