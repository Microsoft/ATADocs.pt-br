---
title: Trabalhando com perfis de usuário no portal da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Descreve como investigar os usuários na tela de perfis de usuário no portal do ATP do Azure
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/02/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 17458706-79fb-4c23-aa42-66979164a45f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8c80529c5111c909bd5e2b1b0ff17933e4f30b18
ms.sourcegitcommit: a0ebb0b6f140d4abf091ebd9d756b975b3d96b9d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54458641"
---
# <a name="understanding-entity-profiles"></a>Noções básicas sobre perfis de entidade

O perfil da entidade fornece uma página da entidade abrangente, projetada para investigações completas e aprofundadas sobre usuários, computadores e dispositivos e sobre os recursos aos quais eles têm acesso e seus históricos. A página de perfil aproveita o novo conversor de atividade lógica do Azure ATP, que pode examinar um grupo de atividades em andamento (agregadas até um minuto) e agrupá-las em uma única atividade lógica para fornecer uma melhor compreensão das atividades reais de seus usuários.

Para acessar uma página de perfil de entidade, clique no nome da entidade, como um nome de usuário, na linha do tempo de atividades suspeitas.

O menu à esquerda fornece todas as informações do Active Directory disponíveis na entidade – endereço de email, domínio, data em que foi vista pela primeira vez. Se a entidade for confidencial, ele informará o motivo. Por exemplo, o usuário foi marcado como confidencial ou é membro de um grupo confidencial?
Se o usuário for confidencial, você verá o ícone sob o nome do usuário.

## <a name="view-entity-activities"></a>Exibir atividades da entidade

Para exibir todas as atividades executadas pelo usuário ou executadas em uma entidade, clique na guia **Atividades**. 

 ![atividades do perfil do usuário](media/user-profile-activities.png)

Por padrão, o painel principal do perfil de entidade exibe uma linha do tempo das atividades da entidade com um histórico de até seis meses, na qual você também pode fazer uma busca detalhada das entidades acessadas pelo usuário ou, para entidades, dos usuários que acessaram a entidade.

Na parte superior, você pode exibir os blocos de resumo que fornecem uma visão geral rápida do que você precisa entender rapidamente sobre sua entidade – em quantos computadores o usuário fez logon, quantos recursos foram acessados e os locais de onde um usuário fez logon na VPN (se configurado). 

Usando o botão **Filtrar por** acima da linha do tempo de atividades, você pode filtrar as atividades por tipo de atividade. Também é possível filtrar um tipo específico de atividade (ruído). Isso é útil para fazer investigações quando você quer entender os conceitos básicos do que uma entidade que está fazendo na rede. Você também pode ir para uma data específica e pode exportar as atividades filtradas para o Excel. O arquivo exportado fornece uma página de alterações de serviços de diretório (itens alterados no Active Directory para a conta) e uma página separada de atividades. 

## <a name="view-directory-data"></a>Exibir dados do diretório

A guia **Dados do diretório** fornece informações estáticas disponíveis do Active Directory, incluindo sinalizadores de segurança de controle de acesso de usuários. O Azure ATP também exibe as associações de grupo do usuário para que você possa determinar se ele tem uma associação direta ou uma associação recursiva. Para grupos, o Azure ATP lista membros do grupo.

 ![dados do diretório do perfil do usuário](media/user-profile-dir-data.png)

Na seção **Controle de acesso de usuários**, o Azure ATP exibe configurações de segurança que talvez precisem de sua atenção. É possível ver sinalizadores importantes sobre o usuário, como se o usuário pode pressionar enter para ignorar a senha e se o usuário tem uma senha que nunca expira, etc. 

## <a name="view-lateral-movement-paths"></a>Exibir caminhos de movimento lateral

Ao clicar na guia de Caminhos de movimento lateral, você pode exibir um mapa totalmente dinâmico e clicável que fornece uma representação visual dos caminhos de movimento lateral de e para o usuário, que podem ser usados para invadir sua rede.

O mapa fornece uma lista de quantos saltos entre computadores ou usuários um invasor teria que fazer para chegar ao usuário e comprometer uma conta confidencial e, se o usuário tiver uma conta confidencial, você poderá ver quantos recursos e contas estão conectadas diretamente.

Se não for detectado nenhum possível LMP para a entidade durante os últimos dois dias, o gráfico não será exibido. Selecione uma data diferente usando **Exibir uma data diferente** para exibir os gráficos de caminhos de movimento lateral anteriores descobertos para essa entidade. O [Relatório de caminho de movimento lateral](reports.md) está sempre disponível para fornecer informações sobre os possíveis caminhos de movimento lateral descobertos e pode ser personalizado por tempo.  

Para obter mais informações, consulte [Caminhos de movimento lateral](use-case-lateral-movement-path.md). 

 ![caminhos de movimento lateral do perfil do usuário](media/user-profile-lateral-movement-paths.png)


## <a name="see-also"></a>Consulte Também

- [Investigar caminhos de movimento lateral com o Azure ATP](use-case-lateral-movement-path.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)