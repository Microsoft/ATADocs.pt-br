---
title: Como investigar usuários e computadores com o Azure ATP | Microsoft Docs
description: Descreve como investigar atividades suspeitas realizadas por usuários, entidades, computadores ou dispositivos que usam o Azure ATP (Proteção Avançada contra Ameaças)
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/6/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4ef4151a311dd5b076737cba9f3c7aa7454a32a7
ms.sourcegitcommit: 714a01edc9006b38d1163d03852dafc2a5fddb5f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2018
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure versão 1.9*



# <a name="investigate-an-entity-with-azure-atp"></a>Investigar uma entidade com o Azure ATP

Este artigo descreve o processo de investigação de entidades após a detecção de atividades suspeitas com o Azure ATP (Proteção Avançada contra Ameaças). Após exibir uma atividade suspeita na linha do tempo, é possível fazer uma busca detalhada sobre a entidade envolvida na atividade e usar os seguintes parâmetros e detalhes para saber mais sobre o que aconteceu e o que você precisa fazer para minimizar o risco.

## <a name="look-at-the-entity-profile"></a>Examinar o perfil da entidade

O perfil de entidade fornece uma abrangente página da entidade, projetada para fazer investigações completas e aprofundadas de usuários, computadores, dispositivos e dos recursos a que eles têm acesso e seu histórico. A página de perfil aproveita o novo conversor de atividade lógica do Azure ATP, que pode examinar um grupo de atividades em andamento (agregadas até um minuto) e agrupá-las em uma única atividade lógica para fornecer uma melhor compreensão das atividades reais de seus usuários.

Para acessar uma página de perfil de entidade, clique no nome da entidade, como um nome de usuário, na linha do tempo de atividades suspeitas. Também é possível ver uma miniversão do perfil de entidade na página da atividade suspeita passando o mouse sobre o nome da entidade.

O perfil da entidade permite que você exiba atividades da entidade, dados de diretório e caminhos de movimentação lateral para ela. Para obter mais informações, consulte [Investigating entity profiles](entity-profiles.md) (Investigando perfis de entidade).

## <a name="check-entity-tags"></a>Verificar marcas da entidade

O Azure ATP extrai marcas do Active Directory para oferecer uma única interface para monitorar usuários e entidades do Active Directory. Essas marcas fornecem informações sobre a entidade do Active Directory, incluindo:
- Parcial: este usuário, computador ou grupo não foi sincronizado com base no domínio e foi parcialmente resolvido por meio de um catálogo global. Alguns atributos não estão disponíveis.
- Não resolvido: este computador não foi resolvido para uma entidade válida na floresta do Active Directory. Nenhuma informação sobre o diretório está disponível.
- Excluído: a entidade foi excluída do Active Directory.
- Desabilitado: a entidade está desabilitada no Active Directory.
- Bloqueado: a entidade inseriu uma senha incorreta muitas vezes e foi bloqueada.
- Expirado: a entidade está expirada no Active Directory.
- Novo: a entidade foi criada há menos de 30 dias.

## <a name="look-at-the-user-access-control-flags"></a>Examine os sinalizadores de controle de acesso de usuários

Os sinalizadores de controle de acesso de usuários também são importados do Active Directory. O Azure ATP inclui 10 sinalizadores eficazes para investigação: 
- A senha nunca expira
- Confiável para delegação
- Cartão inteligente necessário
- Senha expirada
- Senha vazia permitida
- Senha de texto sem formatação armazenada
- Não pode ser delegada
- Apenas criptografia DES
- Pré-autenticação do Kerberos não necessária
- Conta desabilitada 

O Azure ATP informa se esses sinalizadores estão Ativados ou Desativados no Azure Active Directory. Ícones coloridos indicam que o sinalizador está ativado no Active Directory; no exemplo abaixo, apenas **Conta desabilitada** está ativado no Active Directory.

 ![sinalizadores de controle de acesso de usuários](./media/user-access-flags.png)

## <a name="cross-check-with-windows-defender"></a>Verificação com o Windows Defender

Para fornecer insights sobre vários produtos, o perfil da entidade oferece uma notificação às entidades que têm alertas abertos no Windows Defender. Essa notificação informa quantos alertas abertos a entidade tem no Windows Defender e qual é o nível de gravidade deles. Clique na notificação para acessar diretamente os alertas relacionados a essa entidade no Windows Defender.


## <a name="keep-an-eye-on-sensitive-users-and-groups"></a>Fique atento aos grupos e usuários confidenciais

O Azure ATP importa informações sobre o usuário e o grupo do Azure Active Directory, permitindo que você identifique quais usuários são considerados automaticamente confidenciais por serem membros dos seguintes grupos no Active Directory:

-   Administradores
-   Usuários avançados
-   Opers. de contas
-   Operadores de Servidores
-   Operadores de Impressão
-   Operadores de cópia
-   Replicadores
-   Usuários da Área de Trabalho Remota 
-   Operadores de Configuração de Rede 
-   Criadores de confiança de floresta de entrada
-   Administradores do domínio
-   Controladores de Domínio
-   Proprietários criadores de política de grupo 
-   Controladores de domínio somente leitura 
-   Controladores de domínio somente leitura da empresa 
-   Administradores de esquemas 
-   Administrador corporativo

Além disso, é possível **marcar manualmente** entidades como confidenciais dentro do Azure ATP. Isso é importante, porque algumas detecções do Azure ATP, como a detecção de modificação de grupos confidenciais e o caminho de movimentação lateral, dependem o status de confidencialidade de uma entidade. Se você marcar manualmente usuários ou grupos adicionais como confidenciais, como membros de conselho, executivos de empresa e diretor de vendas, o Azure ATP os considerará confidenciais. Para obter mais informações, consulte [Trabalhando com contas confidenciais](sensitive-accounts.md).

## <a name="be-aware-of-lateral-movement-paths"></a>Fique atento aos caminhos de movimentação lateral

O Azure ATP pode ajudar você a impedir ataques que usam caminhos de movimento lateral. O movimento lateral ocorre quando um invasor usa proativamente contas não confidenciais para acessar contas confidenciais.

Se houver um caminho de movimentação lateral para uma entidade, na página do perfil da entidade, clique na guia **Caminhos de movimentação lateral**. O diagrama exibido fornece um mapa dos caminhos possíveis para seu usuário confidencial. 

Para obter mais informações, consulte [Investigando caminhos de movimentação lateral com o Azure ATP](use-case-lateral-movement-path.md).


## <a name="is-it-a-honeytoken-entity"></a>É uma entidade honeytoken?

Antes de continuar com sua investigação, é importante saber se a entidade é um honeytoken. Para sua conveniência, o Azure ATP permite que você marque contas e entidades como honeytokens. Em seguida, durante a investigação, quando você abrir o perfil ou o miniperfil da entidade, você verá uma notificação honeytoken alertando que a atividade que você está examinando foi realizada por uma conta marcada como um honeytoken.


    
## <a name="see-also"></a>Consulte também

- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)