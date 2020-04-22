---
title: Início rápido para conectar o ATP do Azure ao Active Directory
description: A etapa dois da instalação do Azure ATP ajuda a definir as configurações de conectividade do domínio em seu serviço de nuvem do Azure ATP
author: shsagir
ms.author: shsagir
ms.date: 01/15/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.openlocfilehash: 4d3e65aaafea7cefd4ef564c0ee0a82b8d2fdfe4
ms.sourcegitcommit: 63be53de5b84eabdeb8c006438dab45bd35a4ab7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2020
ms.locfileid: "79413733"
---
# <a name="quickstart-connect-to-your-active-directory-forest"></a>Início Rápido: Conectar à sua floresta do Active Directory

Neste início rápido, você conectará o ATP do Azure ao AD (Active Directory) para recuperar dados sobre usuários e computadores. Se você estiver conectando várias florestas, consulte o artigo [Suporte a várias florestas](atp-multi-forest.md).

## <a name="prerequisites"></a>Pré-requisitos

- Uma [instância do ATP do Azure](install-atp-step1.md).
- Confira o artigo sobre os [pré-requisitos do ATP do Azure](atp-prerequisites.md).
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

Na primeira vez em que você abre o portal do Azure ATP, a tela a seguir é exibida:

![Estágio 1 de boas-vindas do Azure ATP](media/directory-services.png)

1. Insira as seguintes informações e clique em **Salvar**:

    |Campo|Comentários|
    |---|---|
    |**Nome de usuário** (obrigatório)|Insira o nome de usuário do AD somente leitura. Por exemplo: **ATPuser**. Você deve usar uma conta de usuário do AD **padrão** ou gMSA. **Não** use o formato UPN para seu nome de usuário.|
    |**Senha** (necessário para a conta de usuário do AD padrão)|Somente para conta de usuário do AD, digite a senha para o usuário somente leitura. Por exemplo: **Lápis1**.|
    |**Conta de serviço gerenciado de grupo** (necessário para a conta gMSA)|Somente para a conta gMSA, selecione **Conta de serviço gerenciado de grupo**.|
    |**Domínio** (obrigatório)|Digite o domínio para o usuário somente leitura. Por exemplo: **contoso.com**. É importante que você insira o FQDN completo do domínio em que o usuário está localizado. Por exemplo, se a conta do usuário estiver no domínio corp.contoso.com, você precisará inserir `corp.contoso.com` e não contoso.com|

2. No portal do Azure ATP, clique em **Baixar instalação do sensor e instalar o primeiro sensor** para continuar.

## <a name="next-steps"></a>Próximas etapas

> [!div class="step-by-step"]
> [« Etapa 1 — Criar uma instância do ATP do Azure](install-atp-step1.md)
> [Etapa 3 — Baixar a instalação do sensor »](install-atp-step3.md)

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o ATP do Azure e a segurança relacionada com outras pessoas? Participe da [Comunidade do ATP do Azure](https://aka.ms/azureatpcommunity) hoje mesmo!
