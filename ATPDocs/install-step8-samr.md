---
title: Configurar SAM-R para habilitar a detecção de caminho de movimento lateral no Microsoft defender para identidade
description: Explica como configurar o Microsoft defender para identidade para fazer chamadas remotas para SAM
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: f1870161b60b975eef818d0a6d6cae63a4fb12c3
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100534269"
---
# <a name="configure-microsoft-defender-for-identity-to-make-remote-calls-to-sam"></a>Configurar o Microsoft defender para identidade para fazer chamadas remotas para SAM

[!INCLUDE [Product long](includes/product-long.md)]a detecção de [caminho de movimento lateral](use-case-lateral-movement-path.md) depende de consultas que identificam administradores locais em computadores específicos. Essas consultas são executadas com o protocolo SAM-R, usando a [!INCLUDE [Product short](includes/product-short.md)] conta de serviço criada durante a [!INCLUDE [Product short](includes/product-short.md)] etapa de instalação  [2. Conecte-se ao AD](install-step2.md).

## <a name="configure-sam-r-required-permissions"></a>Configurar permissões necessárias do SAM-R

Para garantir que os clientes e servidores do Windows permitam que sua [!INCLUDE [Product short](includes/product-short.md)] conta execute Sam-R, é necessário fazer uma modificação no **política de grupo** para adicionar a [!INCLUDE [Product short](includes/product-short.md)] conta de serviço além das contas configuradas listadas na política de acesso à **rede** . Certifique-se de aplicar políticas de grupo a todos os computadores **, exceto controladores de domínio**.

> [!Note]
> Antes de aplicar novas políticas como essa, é fundamental garantir que o ambiente permaneça seguro e que nenhuma alteração afete a compatibilidade do aplicativo. Para isso, primeiro habilite e verifique a compatibilidade das alterações propostas no modo de auditoria antes de fazer alterações no ambiente de produção.

1. Localize a política:

   - Nome da política: Acesso à rede – restringir clientes com permissão para efetuar chamadas remotas para SAM
   - Localização: Configuração do computador, Configurações do Windows, Configurações de segurança, Políticas locais, Opções de segurança

    ![Localize a política](media/samr-policy-location.png)

1. Adicione o [!INCLUDE [Product short](includes/product-short.md)] serviço à lista de contas aprovadas capazes de executar essa ação nos sistemas modernos do Windows.

    ![Adicione o serviço](media/samr-add-service.png)

3. O **serviço AATP** (o [!INCLUDE [Product short](includes/product-short.md)] serviço criado durante a instalação) agora tem os privilégios necessários para executar Sam-R no ambiente.

Para saber mais sobre SAM-R e essa Política de Grupo, consulte [Acesso à rede: restringir clientes com permissão para efetuar chamadas remotas para SAM](/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).

## <a name="see-also"></a>Consulte Também

- [Investigando ataques de caminho de movimento lateral com [!INCLUDE [Product short](includes/product-short.md)]](use-case-lateral-movement-path.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
