---
title: Instalar a Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: A primeira etapa para instalar a ATP do Azure envolve a criação de um espaço de trabalho para sua implantação da ATP do Azure.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/02/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: df3e75970a797307991620e21629df589406cc40
ms.sourcegitcommit: 19ff0ed88e450506b5725bbcbb0d0bd2f0c5e4bb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/27/2019
ms.locfileid: "55085207"
---
# <a name="creating-your-azure-atp-instance-in-the-azure-atp-portal---step-1"></a>Criando sua instância do ATP do Azure no portal do ATP do Azure – Etapa 1

> [!div class="step-by-step"]
> [Etapa 2 »](install-atp-step2.md)

O procedimento de instalação oferece instruções para criar e gerenciar sua instância (chamada anteriormente de workspace) do ATP do Azure. Para obter informações sobre a arquitetura do Azure ATP, consulte [Arquitetura do Azure ATP](atp-architecture.md).

No ATP do Azure, uma única instância permite gerenciar várias florestas em um único painel de exibição. 

> [!NOTE]
> No momento, os data centers do Azure ATP são implantados na Europa, na América do Norte/América Central/Caribe e na Ásia. A instância é criada automaticamente no data center geograficamente mais próximo ao seu AAD. Após a criação, as instâncias do ATP do Azure não podem ser movidas. 

## <a name="enter-the-azure-atp-portal"></a>Entrar no portal do Azure ATP

Depois de verificar que sua rede atende aos requisitos do sensor, continue com a criação da instância do ATP do Azure.

> [!NOTE]
>Para acessar o portal do ATP do Azure, você precisa ser administrador global ou de segurança no locatário.


1.  Entre no [portal da ATP do Azure](https://portal.atp.azure.com).

2.  Faça logon com sua conta de usuário do Azure Active Directory.

## <a name="create-your-instance"></a>Criar sua instância

1. Clique em **Criar instância**. 

    ![Criar uma instância do ATP do Azure](media/create-instance.png)

2. Sua instância do ATP do Azure é nomeada automaticamente com o nome de domínio inicial do AAD, alocada ao data center localizado mais perto de seu AAD e criada. 

    ![Instância do Azure criada](media/instance-created.png)

    > [!NOTE]
    > Para fazer logon no ATP do Azure, você precisará fazer logon com um usuário atribuído a uma função do ATP do Azure com direitos para acessar o portal do ATP do Azure. Para obter mais informações sobre o RBAC (controle de acesso baseado em função) no Azure ATP, consulte [Como trabalhar com grupos de função do Azure ATP](atp-role-groups.md).
 
3. Clique em **Configuração**, **Gerenciar grupos de funções** e use o link [Centro de Administração do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) para gerenciar seus grupos de funções. .

    ![Gerenciar grupos de funções](media/creation-manage-role-groups.png)

- Retenção de dados – as instâncias do ATP do Azure já excluídas não são exibidas na interface do usuário. Para obter mais informações sobre a retenção de dados do Azure ATP, veja [privacidade e segurança de dados do Azure ATP](atp-privacy-compliance.md).


> [!div class="step-by-step"]
> [« Pré-instalação](atp-prerequisites.md)
> [Etapa 2 »](install-atp-step2.md)



## <a name="see-also"></a>Consulte Também
- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/aatpsizingtool)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
