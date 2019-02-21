---
title: Grupos de função da Proteção Avançada contra Ameaças do Azure para gerenciamento de acesso | Microsoft Docs
description: Explica passo a passo como trabalhar com grupos de função do Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 11/29/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ca68f2991d692a2eb5c3e9a257ae77ea80acb538
ms.sourcegitcommit: c48db18274edb2284e281960c6262d97f96e01d2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56263481"
---
# <a name="azure-atp-role-groups"></a>Grupos de função do Azure ATP

O Azure ATP oferece segurança baseada em funções para proteger os dados de acordo com as necessidades específicas de segurança e conformidade de uma organização. O ATP do Azure dá suporte a três funções separadas: Administradores, Usuários e Visualizadores. 

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

Grupos de função permitem o gerenciamento de acesso para o Azure ATP. Com os grupos de função, você pode separar as tarefas dentro de sua equipe de segurança e conceder apenas a quantidade de acesso que os usuários precisam para realizar seus trabalhos. Este artigo explica o gerenciamento de acesso, a autorização de funções no Azure ATP e ajuda você a colocar em funcionamento os grupos de função no Azure ATP.

> [!NOTE]
> Qualquer administrador global ou administrador de segurança no Azure Active Directory do locatário é automaticamente um administrador do Azure ATP.

## <a name="accessing-the-azure-atp-portal"></a>Acessando o portal do Azure ATP

O acesso ao portal do Azure ATP (portal.atp.azure.com) só pode ser realizado por um usuário do Azure AD com a função do diretório de administrador global ou administrador de segurança. Depois de entrar no portal com a função necessária, você poderá criar sua instância do ATP do Azure. O serviço do ATP do Azure cria três grupos de segurança no locatário do Azure Active Directory: Administradores, Usuários, Visualizadores. 

> [!NOTE]
> O acesso ao portal do ATP do Azure é permitido somente a usuários dentro dos grupos de segurança do ATP do Azure dentro do Azure Active Directory e para administradores globais e de segurança do locatário.


## <a name="types-of-azure-atp-security-groups"></a>Tipos de grupos de segurança do Azure ATP 

O ATP do Azure fornece três tipos de grupos de segurança: Os Administradores do *(nome da instância)* do ATP do Azure, Usuários do *(nome da instância)* do ATP do Azure e Visualizadores do *(nome da instância)* do ATP do Azure. A tabela a seguir descreve o tipo de acesso no portal do Azure ATP disponível para cada função. Dependendo de qual função você atribuir, várias telas e opções de menu no portal do Azure ATP não estarão disponíveis para esses usuários, da seguinte maneira:

|Atividade |Administradores do *(nome da instância)* do ATP do Azure|Usuários do *(nome da instância)* do ATP do Azure|Visualizadores do *(nome da instância)* do ATP do Azure|
|----|----|----|----|
|Fazer logon|Disponível|Disponível|Disponível|
|Alterar o status de Alertas de Segurança (abrir novamente, fechar, excluir, suprimir)|Disponível|Disponível|Não disponível|
|Compartilhar/Exportar alertas de segurança (por email, obter o link, baixar detalhes)|Disponível|Disponível|Disponível|
|Baixar um relatório|Disponível|Disponível|Disponível|
|Alterar o status dos Alertas de monitoramento|Disponível|Não disponível|Não disponível|
|Atualizar os sensores de configuração do Azure ATP (baixar, gerar chave novamente, configurar, excluir)|Disponível|Não disponível|Não disponível|
|Atualizar a configuração do Azure ATP – Fontes de dados (serviços de diretório, SIEM, VPN WD–ATP)|Disponível|Não disponível|Não disponível|
|Atualizar configuração do ATP – Atualizações|Disponível|Não disponível|Não disponível|
|Atualizar configuração do ATP – relatórios agendados|Disponível|Disponível|Não disponível|
|Atualizar configuração do ATP – Marcas de entidade (confidenciais e honeytoken)|Disponível|Disponível|Não disponível|
|Atualizar configuração do ATP – Exclusões|Disponível|Disponível|Não disponível|
|Atualizar configuração do ATP – Idioma|Disponível|Disponível|Não disponível|
|Atualizar configuração do ATP – Notificações (email e syslog)|Disponível|Disponível|Não disponível|
|Atualizar configuração do ATP – Visualizar detecções|Disponível|Disponível|Não disponível|
|Exibir perfis de entidade e alertas de segurança|Disponível|Disponível|Disponível|


Quando tentam acessar uma página que não está disponível para seus grupos de função, os usuários são redirecionados à página não autorizada do Azure ATP. 

## <a name="add-and-remove-users"></a>Adicionar e remover usuários 


O Azure ATP usa grupos de segurança do Azure AD como uma base para os grupos de função. Os grupos de funções podem ser gerenciados por meio do [https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups). Somente os usuários do Azure AD podem ser adicionados ou removidos de grupos de segurança. 

## <a name="see-also"></a>Consulte Também
- [Ferramenta de dimensionamento do ATP](http://aka.ms/aatpsizingtool)
- [Arquitetura do ATP](atp-architecture.md)
- [Instalar o Azure ATP](install-atp-step1.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)

