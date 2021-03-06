---
title: Como investigar usuários e computadores com o Microsoft Defender para Identidade
description: Descreve como investigar atividades suspeitas realizadas por usuários, entidades, computadores ou dispositivos que usam o Microsoft Defender para Identidade
ms.date: 10/26/2020
ms.topic: tutorial
ms.openlocfilehash: 2a98e9134959261f075412f05d39ac2bf9d21218
ms.sourcegitcommit: f92dca4dc3d8a25b1a06f68ac7a9f8318105bcd8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/17/2021
ms.locfileid: "100630593"
---
# <a name="tutorial-investigate-an-entity"></a>Tutorial: Investigar uma entidade

> [!NOTE]
> Os recursos do [!INCLUDE [Product long](includes/product-long.md)] explicados nesta página também podem ser acessados usando o novo [portal](https://portal.cloudappsecurity.com).

Neste tutorial, você aprenderá a investigar entidades conectadas a atividades suspeitas detectadas pelo [!INCLUDE [Product long](includes/product-long.md)]. Após exibir um alerta de segurança na linha do tempo, você aprenderá a fazer drill down na entidade envolvida no alerta e a usar os seguintes parâmetros e detalhes para saber mais sobre o que aconteceu e o que você precisará fazer para minimizar o risco.

> [!div class="checklist"]
>
> - Verificar o perfil da entidade
> - Verificar marcas da entidade
> - Verificar os sinalizadores de controle de conta de usuário
> - Verificação com o Windows Defender
> - Fique atento aos grupos e usuários confidenciais
> - Examinar os potenciais caminhos de movimentação lateral
> - Verificar o status de honeytoken

## <a name="check-the-entity-profile"></a>Verificar o perfil da entidade

O perfil de entidade fornece uma abrangente página da entidade, projetada para fazer investigações completas e aprofundadas de usuários, computadores, dispositivos e dos recursos a que eles têm acesso e junto com o histórico. A página de perfil aproveita o novo conversor de atividade lógica do [!INCLUDE [Product short](includes/product-short.md)], que pode examinar um grupo de atividades em andamento (agregadas até um minuto) e agrupá-las em uma única atividade lógica para fornecer uma melhor compreensão das atividades reais de seus usuários.

Para acessar uma página de perfil de entidade, clique no nome da entidade, como um nome de usuário, na linha do tempo de alerta de segurança. Também é possível ver uma miniversão do perfil da entidade na página de alerta de segurança passando o mouse sobre o nome da entidade.

O perfil da entidade permite que você exiba as atividades, os dados de diretório e os [caminhos de movimentação lateral](use-case-lateral-movement-path.md) da entidade. Para obter mais informações sobre entidades, confira [Noções básicas sobre perfis de entidade](entity-profiles.md).

## <a name="check-entity-tags"></a>Verificar marcas da entidade

O [!INCLUDE [Product short](includes/product-short.md)] extrai marcas do Active Directory para oferecer uma só interface para monitorar os usuários e as entidades do Active Directory.
Essas marcas fornecem informações sobre a entidade do Active Directory, incluindo:

- Parcial: Este usuário, computador ou grupo não foi sincronizado com base no domínio e foi parcialmente resolvido por meio de um catálogo global. Alguns atributos não estão disponíveis.
- Não resolvido: Este computador não foi resolvido para uma entidade válida na floresta do Active Directory. Nenhuma informação sobre o diretório está disponível.
- Excluído: A entidade foi excluída do Active Directory.
- Desabilitado: A entidade está desabilitada no Active Directory.
- Bloqueado: A entidade inseriu uma senha incorreta muitas vezes e foi bloqueada.
- Expirado: A entidade está expirada no Active Directory.
- Novo: A entidade foi criada há menos de 30 dias.

## <a name="check-user-account-control-flags"></a>Verificar os sinalizadores de controle de conta de usuário

Os sinalizadores de controle de contas de usuários também são importados do Active Directory. Os dados do diretório de entidades do [!INCLUDE [Product short](includes/product-short.md)] incluem dez sinalizadores eficazes para investigação:

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

O [!INCLUDE [Product short](includes/product-short.md)] informa se esses sinalizadores estão Ativados ou Desativados no Azure Active Directory. Ícones coloridos e a alternância correspondente indicam o status de cada sinalizador. No exemplo a seguir, somente **A senha nunca expira** está ativo no Active Directory.

 ![sinalizadores de controle de conta de usuário](media/user-access-flags.png)

## <a name="cross-check-with-windows-defender"></a>Verificação com o Windows Defender

Para fornecer insights sobre vários produtos, o perfil da entidade oferece uma notificação às entidades que têm alertas abertos no Windows Defender. Essa notificação informa quantos alertas abertos a entidade tem no Windows Defender e qual é o nível de gravidade deles. Clique na notificação para acessar diretamente os alertas relacionados a essa entidade no Windows Defender.

## <a name="keep-an-eye-on-sensitive-users-and-groups"></a>Fique atento aos grupos e usuários confidenciais

O [!INCLUDE [Product short](includes/product-short.md)] importa informações sobre o usuário e o grupo do Azure Active Directory, permitindo que você identifique quais usuários são considerados automaticamente confidenciais por serem membros dos seguintes grupos do Active Directory:

- Administradores
- Usuários avançados
- Opers. de contas
- Operadores de Servidores
- Operadores de Impressão
- Operadores de cópia
- Replicadores
- Usuários da Área de Trabalho Remota
- Operadores de Configuração de Rede
- Criadores de confiança de floresta de entrada
- Administradores do domínio
- Controladores de Domínio
- Proprietários criadores de política de grupo
- Controladores de domínio somente leitura
- Controladores de domínio somente leitura da empresa
- Administradores de esquemas
- Administrador corporativo

Além disso, é possível **marcar manualmente** entidades como confidenciais no [!INCLUDE [Product short](includes/product-short.md)]. Isso é importante, porque algumas detecções do [!INCLUDE [Product short](includes/product-short.md)], como a detecção de modificação de grupos confidenciais e o caminho de movimentação lateral, dependem do status de confidencialidade de uma entidade. Se você marcar manualmente usuários ou grupos adicionais como confidenciais, como membros de conselho, executivos de empresa e diretores de vendas, o [!INCLUDE [Product short](includes/product-short.md)] vai considerá-los confidenciais. Para obter mais informações, consulte [Trabalhando com contas confidenciais](manage-sensitive-honeytoken-accounts.md).

## <a name="review-lateral-movement-paths"></a>Examinar caminhos de movimento lateral

O [!INCLUDE [Product short](includes/product-short.md)] pode ajudar você a impedir ataques que usam caminhos de movimentação lateral. O movimento lateral ocorre quando um invasor usa proativamente contas não confidenciais para acessar contas confidenciais.

Se houver um caminho de movimentação lateral para uma entidade, na página do perfil da entidade, clique na guia **Caminhos de movimentação lateral**. O diagrama exibido fornece um mapa dos caminhos possíveis para seu usuário confidencial.

Para obter mais informações, confira [Como investigar caminhos de movimentação lateral com o [!INCLUDE [Product short](includes/product-short.md)]](use-case-lateral-movement-path.md).

## <a name="check-honeytoken-status"></a>Verificar o status de honeytoken

Antes de continuar com sua investigação, é importante saber se a entidade é um honeytoken. É possível marcar contas e entidades como honeytokens no [!INCLUDE [Product short](includes/product-short.md)]. Ao abrir o perfil de entidade ou o perfil simplificado de uma conta ou entidade marcada como um honeytoken, você verá a notificação do honeytoken. Ao investigar, a notificação de honeytoken avisa que a atividade em revisão foi executada por uma conta que você marcou como um honeytoken.

## <a name="see-also"></a>Consulte também

- [Trabalhando com alertas de segurança](working-with-suspicious-activities.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
