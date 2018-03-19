---
title: "Instalar a Proteção Avançada contra Ameaças do Azure – etapa 1 | Microsoft Docs"
description: "A primeira etapa para instalar o Azure ATP envolve a criação de um espaço de trabalho para sua implantação do Azure ATP."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/11/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5eabf4fc3965e8745b7e2c0fbae4973deb358814
ms.sourcegitcommit: 912e453753156902618ae6ebb8489c2320c06fc6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/12/2018
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*


# <a name="creating-a-workspace-in-the-azure-atp-workspace-management-portal---step-1"></a>Criar um espaço de trabalho no portal de gerenciamento de espaço de trabalho do Azure ATP – etapa 1

>[!div class="step-by-step"]
[Etapa 2 »](install-atp-step2.md)

Este procedimento de instalação fornece instruções para criar e gerenciar um espaço de trabalho no portal de gerenciamento do espaço de trabalho do Azure ATP. Para obter informações sobre a arquitetura do Azure ATP, consulte [Arquitetura do Azure ATP](atp-architecture.md).

No Azure ATP, você pode gerenciar e monitorar vários espaços de trabalho. Isso é especialmente útil se você quiser criar um espaço de trabalho de demonstração e um espaço de trabalho de teste no qual pode fazer a prova de conceito do Azure ATP antes de disponibilizá-lo para toda a organização. Isso também é necessário para dar suporte a implantações com várias florestas. Um único espaço de trabalho só pode monitorar vários domínios de uma única floresta. 

> [!NOTE]
> Você pode ter um máximo de dois espaços de trabalho ativos. Depois de excluir um espaço de trabalho, você pode entrar em contato com o suporte para reativá-lo. Você pode ter um máximo de três espaços de trabalho excluídos. Para aumentar o número de espaços de trabalho salvos e excluídos, entre em contato com o suporte do Azure ATP.

## <a name="step-1-enter-the-workspace-management-portal"></a>Etapa 1. Entrar no portal de gerenciamento do espaço de trabalho

Depois de confirmar que sua rede atende aos requisitos do sensor, você poderá continuar com a criação do espaço de trabalho do Azure ATP.

> [!NOTE]
>Para acessar o portal de gerenciamento do espaço de trabalho, você precisa ser um administrador global ou um administrador de segurança no locatário.


1.  Entre no [portal de espaço de trabalho do Azure ATP](https://portal.atp.azure.com).

2.  Faça logon com sua conta de usuário do Azure Active Directory local que tenha pelo menos acesso de leitura a todos os objetos nos domínios monitorados.

## <a name="step-2-create-a-workspace"></a>Etapa 2. Criar um espaço de trabalho

1. Clique em **Criar espaço de trabalho**.

2. Na caixa de diálogo **Criar novo espaço de trabalho**, nomeie seu espaço de trabalho, decida se ele é o espaço de trabalho primário ou não e selecione uma **Geolocalização** para seu data center. Somente um espaço de trabalho pode ser definido como primário. Definir um espaço de trabalho como primário afeta as integrações – você só pode integrar o Azure ATP com o Windows Defender ATP para seu espaço de trabalho primário. Você pode alterar qual espaço de trabalho é primário posteriormente, mas, para fazer isso, você precisará remover as integrações já definidas para o espaço de trabalho primário atual.
 > [!NOTE]
 > Depois de selecionar uma Geolocalização, você não poderá modificá-la.
    ![Espaço de trabalho do Azure ATP](media/create-workspace.png)

3. Você pode clicar no link **Gerenciar funções de usuário do Azure ATP** para acessar diretamente o [Centro de administração do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) e gerenciar seus grupos de função.

 > [!NOTE]
 > Para fazer logon com êxito no Azure ATP, você precisa fazer logon com um usuário que recebeu a função adequada do Azure ATP para acessar o portal de espaço de trabalho do Azure ATP. Para obter mais informações sobre o RBAC (controle de acesso baseado em função) no Azure ATP, consulte [Como trabalhar com grupos de função do Azure ATP](atp-role-groups.md).

4. Clique no nome do novo espaço de trabalho para acessar o portal de espaço de trabalho do Azure ATP para esse espaço de trabalho.

    ![Espaços de trabalho do Azure ATP](media/atp-workspaces.png)

- Somente o espaço de trabalho primário pode ser editado. Para fazer alterações em outros espaços de trabalho, você pode excluí-los e adicioná-los novamente. Se quiser excluir o espaço de trabalho primário, primeiro você precisará desligar as integrações e definir o espaço de trabalho como não **Primário** antes que ele possa ser excluído.
- Para editar um espaço de trabalho Primário, primeiro você precisa desligar as integrações existentes no espaço de trabalho.

- Retenção de dados – espaços de trabalho excluídos não aparecem na interface do usuário. No entanto, seus dados são retidos de acordo com a [Política de retenção de dados da Microsoft](https://www.microsoft.com/trustcenter/privacy/you-own-your-data).


>[!div class="step-by-step"]
[« Pré-instalação](configure-port-mirroring.md)
[Etapa 2 »](install-atp-step2.md)


## <a name="see-also"></a>Consulte Também
- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/aatpsizingtool)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)
