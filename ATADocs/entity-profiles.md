---
title: Trabalhando com perfis de entidade no console do Advanced Threat Analytics
description: Descreve como investigar entidades na tela de perfis de usuários no console do ATA
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/25/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 581a3257-32dc-453f-b84e-b9f99186f5d3
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 02cd26323be6ae79524d4912674380af23d2c3af
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88954792"
---
# <a name="investigating-entity-profiles"></a>Investigando perfis de entidade


*Aplica-se a: Advanced Threat Analytics versão 1.9*

O perfil de entidade fornece um painel projetado para fazer investigações completas e aprofundadas de usuários, de computadores, de dispositivos e dos recursos a que eles têm acesso e do histórico deles. A página de perfil aproveita o novo conversor de atividade lógica do ATA, que pode examinar um grupo de atividades em andamento (agregadas até um minuto) e agrupá-las em uma única atividade lógica para fornecer uma melhor compreensão das atividades reais de seus usuários.

Para acessar uma página de perfil de entidade, clique no nome da entidade, como um nome de usuário, na linha do tempo de atividades suspeitas.

O menu à esquerda fornece todas as informações do Active Directory disponíveis na entidade – endereço de email, domínio, data em que foi vista pela primeira vez. Se a entidade for confidencial, ele informará o motivo. Por exemplo, o usuário foi marcado como confidencial ou é membro de um grupo confidencial?
Se o usuário for confidencial, você verá o ícone sob o nome do usuário.

## <a name="view-entity-activities"></a>Exibir atividades da entidade

Para exibir todas as atividades executadas pelo usuário ou executadas em uma entidade, clique na guia **Atividades**. 

 ![atividades do perfil do usuário](media/user-profile-activities.png)

Por padrão, o painel principal do perfil de entidade exibe uma linha do tempo das atividades da entidade com um histórico de até seis meses, na qual você também pode fazer uma busca detalhada das entidades acessadas pelo usuário ou, para entidades, dos usuários que acessaram a entidade.

Na parte superior, você pode exibir os blocos de resumo que fornecem uma visão geral rápida do que você precisa entender rapidamente sobre sua entidade. Esses blocos mudam de acordo com o tipo de entidade. Para um usuário, você verá:
- Quantas atividades suspeitas abertas existem para o usuário
- Em quantos computadores o usuário fez logon
- Quantos recursos o usuário acessou
- De quais locais o usuário fez logon na VPN

  ![menu de entidade](media/entity-menu.png)

Para computadores, você verá:
- Quantas atividades suspeitas abertas existem para o computador
- Quantos usuários fizeram logon no computador
- Quantos recursos o computador acessou
- Quantas VPN de locais foram acessadas do computador
- Uma lista de quais endereços IP o computador foi usado
  
  ![computador de menu de entidade](media/entity-computer.png)

Usando o botão **Filtrar por** acima da linha do tempo de atividades, você pode filtrar as atividades por tipo de atividade. Também é possível filtrar um tipo específico de atividade (ruído). Isso é muito útil para fazer investigações quando você quiser entender o básico do que uma entidade está fazendo na rede. Você também pode ir para uma data específica e pode exportar as atividades filtradas para o Excel. O arquivo exportado fornece uma página de alterações de serviços de diretório (itens alterados no Active Directory para a conta) e uma página separada de atividades. 

## <a name="view-directory-data"></a>Exibir dados do diretório

A guia **Dados do diretório** fornece informações estáticas disponíveis do Active Directory, incluindo sinalizadores de segurança de controle de acesso de usuários. O ATA também exibe as associações a grupos do usuário para que você possa determinar se ele tem uma associação direta ou recursiva. Para grupos, o ATA lista membros do grupo.

 ![dados do diretório do perfil do usuário](media/user-profile-dir-data.png)

Na seção **Controle de Acesso de Usuários**, o ATA exibe configurações de segurança que talvez precisem de sua atenção. Você pode ver sinalizadores importantes sobre o usuário, por exemplo, se o usuário pode pressionar Enter para ignorar a senha, se o usuário tem uma senha que nunca expira etc. 

## <a name="view-lateral-movement-paths"></a>Exibir caminhos de movimento lateral

Ao clicar na guia de **Caminhos de movimento lateral**, será possível exibir um mapa totalmente dinâmico e clicável que fornecerá uma representação visual dos caminhos de movimento lateral de e para o usuário, os quais podem ser usados para invadir sua rede.

O mapa fornece uma lista de quantos saltos entre computadores ou usuários um invasor precisaria dar para chegar ao usuário e comprometer uma conta confidencial e, se o usuário tiver uma conta confidencial, você poderá ver quantos recursos e contas estão conectados diretamente. Para obter mais informações, consulte [Caminhos de movimento lateral](use-case-lateral-movement-path.md). 

 ![caminhos de movimento lateral do perfil do usuário](media/user-profile-lateral-movement-paths.png)


## <a name="see-also"></a>Consulte Também
[Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
      