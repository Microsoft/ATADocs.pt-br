---
title: Guia de início rápido – Conectar o Microsoft Defender para Identidade ao Active Directory
description: A segunda etapa da instalação do Microsoft Defender para Identidade ajuda você a definir as configurações de conectividade de domínio no serviço de nuvem do Defender para Identidade
ms.date: 10/26/2020
ms.topic: quickstart
ms.openlocfilehash: b1379570d87957fc943bf8b0727b6b0294f26695
ms.sourcegitcommit: b6da51c97e8fb70ca04c0c0d5ea694700db9de86
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/21/2021
ms.locfileid: "98634549"
---
# <a name="quickstart-connect-to-your-active-directory-forest"></a>Início Rápido: Conectar à sua floresta do Active Directory

Neste guia de início rápido, você conectará o [!INCLUDE [Product long](includes/product-long.md)] ao AD (Active Directory) para recuperar dados sobre usuários e computadores. Se você estiver conectando várias florestas, consulte o artigo [Suporte a várias florestas](multi-forest.md).

## <a name="prerequisites"></a>Pré-requisitos

- Uma [instância do [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md).
- Examine o artigo [Pré-requisitos do [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md).
- Pelo menos uma das seguintes contas de serviços de diretório com acesso de leitura a todos os objetos nos domínios monitorados:
  - Uma conta de usuário do AD **padrão** e senha. Exigidas para sensores que executam o Windows Server 2008 R2 SP1.
  - Uma **gMSA (Conta de Serviço Gerenciado de Grupo)** . Requer Windows Server 2012 ou posterior.  
  Todos os sensores devem ter permissões para recuperar a senha da conta gMSA. Para obter informações sobre como criar uma conta gMSA, confira [Configurar uma conta gMSA](#how-to-set-up-a-gmsa-account).

    > [!NOTE]
    >
    > - Para computadores sensores que executam o Windows Server 2012 e posterior, recomendamos usar uma conta **gMSA** devido à segurança aprimorada e ao gerenciamento automático de senhas.
    > - Se você tiver vários sensores, alguns executando o Windows Server 2008 e outros executando o Windows Server 2012 ou posterior, além da recomendação para usar uma conta **gMSA**, você também deverá usar pelo menos uma conta de usuário do AD **padrão**.

### <a name="how-to-set-up-a-gmsa-account"></a>Como configurar uma conta gMSA

1. Crie uma [conta gMSA](/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts#BKMK_CreateGMSA).
1. Crie um novo [grupo de segurança contendo todos os controladores de domínio com sensores (executando o Windows Server 2012 ou posterior)](/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts#BKMK_AddMemberHosts) com permissões para recuperar a senha da conta gMSA. (Recomendado)

## <a name="provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Fornecer um nome de usuário e uma senha para se conectar à sua Floresta do Active Directory

Na primeira vez em que você abre o portal do [!INCLUDE [Product short](includes/product-short.md)], a seguinte tela é exibida:

![Estágio 1 de boas-vindas, configurações de Serviços de Diretório](media/directory-services.png)

1. Insira as seguintes informações e clique em **Salvar**:

    |Campo|Comentários|
    |---|---|
    |**Nome de usuário** (obrigatório)|Insira o nome de usuário do AD somente leitura. Por exemplo: **DefenderForIdentityUser**. Você deve usar uma conta de usuário do AD **padrão** ou gMSA. **Não** use o formato UPN para seu nome de usuário.<br />**OBSERVAÇÃO:** Recomendamos que você evite usar contas atribuídas a usuários específicos.|
    |**Senha** (necessário para a conta de usuário do AD padrão)|Somente para conta de usuário do AD, digite a senha para o usuário somente leitura. Por exemplo: **Lápis1**.|
    |**Conta de serviço gerenciado de grupo** (necessário para a conta gMSA)|Somente para a conta gMSA, selecione **Conta de serviço gerenciado de grupo**.|
    |**Domínio** (obrigatório)|Digite o domínio para o usuário somente leitura. Por exemplo: **contoso.com**. É importante que você insira o FQDN completo do domínio em que o usuário está localizado. Por exemplo, se a conta do usuário estiver no domínio corp.contoso.com, você precisará inserir `corp.contoso.com` e não contoso.com|

1. No portal do [!INCLUDE [Product short](includes/product-short.md)], clique em **Baixar instalação do sensor e instalar o primeiro sensor** para continuar.

## <a name="next-steps"></a>Próximas etapas

> [!div class="step-by-step"]
> [« Etapa 1 – Criar uma instância do [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
> [Etapa 3 – Baixar a instalação do sensor »](install-step3.md)

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o [!INCLUDE [Product short](includes/product-short.md)] e a segurança relacionada com outras pessoas? Participe da Comunidade [[!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity) hoje mesmo!
