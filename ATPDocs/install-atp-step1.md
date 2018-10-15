---
title: Instalar a Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: A primeira etapa para instalar a ATP do Azure envolve a criação de um espaço de trabalho para sua implantação da ATP do Azure.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/4/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 97cce3de3a1cbe049523c54901ecbc9228aaee53
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48782990"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*


# <a name="creating-your-azure-atp-instance-in-the-portal---step-1"></a>Criando sua instância do Azure ATP no portal – Etapa 1

> [!div class="step-by-step"]
> [Etapa 2 »](install-atp-step2.md)

O procedimento de instalação oferece instruções para criar e gerenciar sua instância ou workspace do Azure ATP. Para obter informações sobre a arquitetura do Azure ATP, consulte [Arquitetura do Azure ATP](atp-architecture.md).

No Azure ATP, você terá uma única instância ou workspace que permite gerenciar várias florestas em um único painel de exibição. 

> [!NOTE]
> No momento, os data centers do Azure ATP são implantados na Europa, na América do Norte/América Central/Caribe e na Ásia.

## <a name="step-1-enter-the-azure-atp-portal"></a>Etapa 1. Entrar no portal do Azure ATP

Depois de confirmar que sua rede atende aos requisitos do sensor, você poderá continuar com a criação do espaço de trabalho do Azure ATP.

> [!NOTE]
>Para acessar o portal de gerenciamento, você precisa ser um administrador global ou um administrador de segurança nesse locatário.


1.  Entre no [portal da ATP do Azure](https://portal.atp.azure.com).

2.  Faça logon com sua conta de usuário do Azure Active Directory.

## <a name="step-2-create-your-workspace"></a>Etapa 2. Criar seu espaço de trabalho

1. Clique em **Criar espaço de trabalho**.

2. Na caixa de diálogo **Criar novo espaço de trabalho**, nomeie seu espaço de trabalho e selecione uma **Geolocalização** para seu data center. Seu workspace é **Primário** por padrão. 
 > [!NOTE]
 > Depois de selecionar uma Geolocalização, você não poderá modificá-la.
    ![Espaço de trabalho do Azure ATP](media/create-workspace.png)

3. Você pode clicar no link **Gerenciar funções de usuário do Azure ATP** para acessar diretamente o [Centro de administração do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) e gerenciar seus grupos de função.

 > [!NOTE]
 > Para fazer logon com êxito no Azure ATP, você precisa fazer logon com um usuário que recebeu a função adequada do Azure ATP para acessar o portal do Azure ATP. Para obter mais informações sobre o RBAC (controle de acesso baseado em função) no Azure ATP, consulte [Como trabalhar com grupos de função do Azure ATP](atp-role-groups.md).

4. Clique no nome do seu workspace para acessar o portal do Azure ATP.

    ![Espaços de trabalho do Azure ATP](media/atp-workspaces.png)

- Somente o espaço de trabalho primário pode ser editado. Se desejar excluir seu workspace primário, primeiro será necessário desligar as integrações antes de elas poderem ser excluídas.

- Retenção de dados – workspaces excluídos anteriormente não são exibidos na interface do usuário. Para obter mais informações sobre a retenção de dados do Azure ATP, veja [privacidade e segurança de dados do Azure ATP](atp-privacy-compliance.md).


>[!div class="step-by-step"]
[« Pré-instalação](atp-prerequisites.md)
[Etapa 2 »](install-atp-step2.md)



## <a name="see-also"></a>Consulte Também
- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/aatpsizingtool)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Confira o fórum do Azure ATP!](https://aka.ms/azureatpcommunity)
