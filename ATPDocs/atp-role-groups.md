---
title: Grupos de função da Proteção Avançada contra Ameaças do Azure para gerenciamento de acesso | Microsoft Docs
description: Explica passo a passo como trabalhar com grupos de função do Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/07/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7ae3f0adca3137664f0a89c15e8feee71d0cd915
ms.sourcegitcommit: c4978be196e0039c7a5d5887bec4cbc5c01d64f9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2018
ms.locfileid: "48848606"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*




# <a name="azure-atp-role-groups"></a>Grupos de função do Azure ATP

O Azure ATP oferece segurança baseada em funções para proteger os dados de acordo com as necessidades específicas de segurança e conformidade de uma organização. O Azure ATP dá suporte a três funções distintas: Administradores, Usuários e Visualizadores. 

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

Grupos de função permitem o gerenciamento de acesso para o Azure ATP. Com os grupos de função, você pode separar as tarefas dentro de sua equipe de segurança e conceder apenas a quantidade de acesso que os usuários precisam para realizar seus trabalhos. Este artigo explica o gerenciamento de acesso, a autorização de funções no Azure ATP e ajuda você a colocar em funcionamento os grupos de função no Azure ATP.

> [!NOTE]
> Qualquer administrador global ou administrador de segurança no Azure Active Directory do locatário é automaticamente um administrador do Azure ATP.

## <a name="accessing-the-azure-atp-portal"></a>Acessando o portal do Azure ATP

O acesso ao portal do Azure ATP (portal.atp.azure.com) só pode ser realizado por um usuário do Azure AD com a função do diretório de administrador global ou administrador de segurança. Após entrar no portal, você pode criar espaços de trabalho. O serviço do Azure ATP cria três grupos de segurança no locatário do Azure Active Directory: Administradores, Usuários e Visualizadores. 

> [!NOTE]
> O acesso ao portal do Azure ATP é concedido somente a usuários dentro dos grupos de segurança do Azure ATP dentro do Azure Active Directory e para administradores globais e administradores de segurança do locatário.


## <a name="types-of-azure-atp-security-groups"></a>Tipos de grupos de segurança do Azure ATP 

O Azure ATP fornece três tipos de grupos de segurança: Administradores do *(nome do workspace)* do Azure ATP, Usuários do *(nome do workspace)* do Azure ATP e Visualizadores do *(nome do workspace)* do Azure ATP. A tabela a seguir descreve o tipo de acesso no portal do Azure ATP disponível para cada função. Dependendo de qual função você atribuir, várias telas e opções de menu no portal do Azure ATP não estarão disponíveis para esses usuários, da seguinte maneira:

|Atividade |Administradores do *(nome do workspace)* do Azure ATP|Usuários do *(nome do workspace)* do Azure ATP|Visualizadores do *(nome do workspace)* do Azure ATP|
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
- [Confira o fórum do Azure ATP!](https://aka.ms/azureatpcommunity)

