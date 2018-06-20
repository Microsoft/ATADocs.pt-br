---
title: Grupos de função da Proteção Avançada contra Ameaças do Azure para gerenciamento de acesso | Microsoft Docs
description: Explica passo a passo como trabalhar com grupos de função do Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 77a2464634b4286d2f6d35504e9ab7512cf7b612
ms.sourcegitcommit: 324dc941282f2948366afa5a919bda0b029bd59d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2018
ms.locfileid: "34444766"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*




# <a name="azure-atp-role-groups"></a>Grupos de função do Azure ATP

O Azure ATP oferece segurança baseada em funções para proteger os dados de acordo com as necessidades específicas de segurança e conformidade de uma organização. O Azure ATP dá suporte a três funções distintas: Administradores, Usuários e Visualizadores. 

> [!NOTE]
> Se você tiver interesse em visualizar ou excluir dados pessoais, consulte as diretrizes da Microsoft no [Gerente de Conformidade da Microsoft](https://servicetrust.microsoft.com/ComplianceManager) e na [seção RGPD do site de Conformidade Corporativa do Microsoft 365 Enterprise](https://docs.microsoft.com/en-us/microsoft-365/compliance/gdpr). Se você estiver procurando informações gerais sobre o RGPD, confira a seção [RGPD do Portal de Confiança do Serviço](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

Grupos de função permitem o gerenciamento de acesso para o Azure ATP. Com os grupos de função, você pode separar as tarefas dentro de sua equipe de segurança e conceder apenas a quantidade de acesso que os usuários precisam para realizar seus trabalhos. Este artigo explica o gerenciamento de acesso e a autorização de funções no Azure ATP, além de ajudar você a colocar em funcionamento os grupos de função no Azure ATP.

> [!NOTE]
> Qualquer administrador global ou administrador de segurança no Azure Active Directory do locatário é automaticamente um administrador do Azure ATP.

## <a name="accessing-the-workspace-management-portal"></a>Acessando o portal de gerenciamento do espaço de trabalho

O acesso ao portal de gerenciamento do espaço de trabalho (portal.atp.azure.com) só pode ser realizado por um usuário do Azure AD que tem a função do diretório de administrador global ou administrador de segurança. Após entrar no portal, você pode criar espaços de trabalho diferentes. Para cada espaço de trabalho, o serviço do Azure ATP cria três grupos de segurança em seu locatário do Azure Active Directory: Administradores, Usuários e Visualizadores. 

> [!NOTE]
> O acesso ao portal de espaço de trabalho do Azure ATP é concedido somente a usuários dentro dos grupos de segurança do Azure AD para esse espaço de trabalho e para administradores globais e administradores de segurança.


## <a name="types-of-azure-atp-security-groups"></a>Tipos de grupos de segurança do Azure ATP 

O Azure ATP apresenta três tipos de grupo de segurança: Administradores do *nome do espaço de trabalho* do Azure ATP, Usuários do *nome do espaço de trabalho* do Azure ATP e Visualizadores do *nome do espaço de trabalho* do Azure ATP. A tabela a seguir descreve o tipo de acesso no portal de espaço de trabalho do Azure ATP disponível por função. Dependendo de qual função você atribuir, várias telas e opções de menu no portal de espaço de trabalho do Azure ATP não estarão disponíveis. Veja a seguir:

|Atividade |Administradores do *nome do espaço de trabalho* Azure ATP|Usuários do *nome do espaço de trabalho* Azure ATP|Visualizadores do *nome do espaço de trabalho* Azure ATP|
|----|----|----|----|
|Fazer logon|Disponível|Disponível|Disponível|
|Alterar o status de atividades suspeitas|Disponível|Disponível|Não disponível|
|Compartilhar/Exportar atividade suspeita por email/link|Disponível|Disponível|Disponível|
|Alterar o status dos Alertas de monitoramento|Disponível|Não disponível|Não disponível|
|Atualizar configuração do Azure ATP|Disponível|Não disponível|Não disponível|
|sensor – Adicionar|Disponível|Não disponível|Não disponível|
|sensor – Excluir |Disponível|Não disponível|Não disponível|
|CD Monitorado – Adicionar |Disponível|Não disponível|Não disponível|
|CD Monitorado – Excluir|Disponível|Não disponível|Não disponível|
|Exibir alertas e atividades suspeitas|Disponível|Disponível|Disponível|


Quando tentam acessar uma página que não está disponível para seus grupos de função, os usuários são redirecionados à página não autorizada do Azure ATP. 

## <a name="add-and-remove-users"></a>Adicionar e remover usuários 

O Azure ATP usa grupos de segurança do Azure AD como uma base para os grupos de função. Os grupos de função podem ser gerenciados por meio dos [https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All groups](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All groups).  Somente usuários do AAD podem ser adicionados ou removidos de grupos de segurança. 


## <a name="see-also"></a>Consulte Também
- [Ferramenta de dimensionamento do ATA](http://aka.ms/aatpsizingtool)
- [Arquitetura do ATA](atp-architecture.md)
- [Instalar o ATA](install-atp-step1.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)

