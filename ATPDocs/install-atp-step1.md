---
title: Início rápido para criar sua instância do ATP do Azure | Microsoft Docs
description: Início rápido para criar a instância para sua implantação do ATP do Azure, que é a primeira etapa para instalar o ATP do Azure.
keywords: ''
author: mlottner
ms.author: mlottner
ms.date: 10/31/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 18a9feba8344ce88c4afb2ed3911b51aea0b9e07
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "73462318"
---
# <a name="quickstart-create-your-azure-atp-instance"></a>Início Rápido: Criar sua instância do Azure ATP

Neste início rápido, você criará sua instância do ATP do Azure no portal do ATP do Azure. No ATP do Azure, você terá uma única instância, anteriormente chamada de workspace. Uma única instância permite gerenciar várias florestas em um único painel de exibição.

> [!IMPORTANT]
> No momento, os data centers do Azure ATP são implantados na Europa, na América do Norte/América Central/Caribe e na Ásia. A instância é criada automaticamente no data center geograficamente mais próximo ao seu Azure AD (Azure Active Directory). Após a criação, as instâncias do ATP do Azure não podem ser movidas.

## <a name="prerequisites"></a>Pré-requisitos

- Uma [licença do ATP do Azure](atp-technical-faq.md#licensing-and-privacy).
- Para acessar o portal do ATP do Azure, você precisa ser [administrador global ou de segurança no locatário](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#available-roles).
- Confira o artigo sobre a [arquitetura do ATP do Azure](atp-architecture.md).
- Confira o artigo sobre os [pré-requisitos do ATP do Azure](atp-prerequisites.md). 

## <a name="sign-in-to-the-azure-atp-portal"></a>Entrar no portal do ATP do Azure

Depois de verificar que sua rede atende aos requisitos do sensor, inicie a criação da instância do ATP do Azure.

1. Acesse o [portal do ATP do Azure](https://portal.atp.azure.com).

2. Entre com sua conta de usuário do Azure Active Directory.

* Clientes do GCC High devem usar o portal do [ATP do Azure para GCC High](http://portal.atp.azure.us).  

## <a name="create-your-instance"></a>Criar sua instância

1. Clique em **Criar instância**. 

    ![Criar uma instância do ATP do Azure](media/create-instance.png)

2. Sua instância do ATP do Azure é nomeada automaticamente com o nome de domínio inicial do Azure AD e criada no data center mais próximo do seu Azure AD. 

    ![Instância do Azure criada](media/instance-created.png)

    > [!NOTE]
    > Para entrar no ATP do Azure, você precisará entrar com um usuário atribuído a uma função do ATP do Azure com direitos para acessar o portal do ATP do Azure. Para obter mais informações sobre o RBAC (controle de acesso baseado em função) no Azure ATP, consulte [Como trabalhar com grupos de função do Azure ATP](atp-role-groups.md).
 
3. Clique em **Configuração**, **Gerenciar grupos de funções** e use o link [Centro de Administração do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) para gerenciar seus grupos de funções.

    ![Gerenciar grupos de funções](media/creation-manage-role-groups.png)

- Retenção de dados – as instâncias do ATP do Azure já excluídas não são exibidas na interface do usuário. Para obter mais informações sobre a retenção de dados do Azure ATP, veja [privacidade e segurança de dados do Azure ATP](atp-privacy-compliance.md).

## <a name="next-steps"></a>Próximas etapas

> [!div class="step-by-step"]
> [« Pré-requisitos](atp-prerequisites.md)
> [Etapa 2 — Conectar ao Active Directory »](install-atp-step2.md)

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o ATP do Azure e a segurança relacionada com outras pessoas? Participe da [Comunidade do ATP do Azure](https://aka.ms/azureatpcommunity) hoje mesmo!

