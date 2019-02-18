---
title: Início rápido para conectar o ATP do Azure ao Active Directory | Microsoft Docs
description: A etapa dois da instalação do Azure ATP ajuda a definir as configurações de conectividade do domínio em seu serviço de nuvem do Azure ATP
author: mlottner
ms.author: mlottner
ms.date: 02/05/2019
ms.topic: conceptual
ms.service: azure-advanced-threat-protection
ms.openlocfilehash: 404252e7fb9d71a067def9b28870d68736a493dd
ms.sourcegitcommit: 96752da28f43896e7b8e5945947b32c4810bdff6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/07/2019
ms.locfileid: "55831405"
---
# <a name="quickstart-connect-to-your-active-directory-forest"></a>Início Rápido: Conectar à sua floresta do Active Directory

Neste início rápido, você conectará o ATP do Azure ao AD (Active Directory) para recuperar dados sobre usuários e computadores. Se você estiver conectando várias florestas, consulte o artigo [Suporte a várias florestas](atp-multi-forest.md).

## <a name="prerequisites"></a>Pré-requisitos

- Uma [instância do ATP do Azure](install-atp-step1.md).
- Confira o artigo sobre os [pré-requisitos do ATP do Azure](atp-prerequisites.md).
- Uma conta de usuário e senha **local** do Microsoft Azure AD com acesso de leitura para todos os objetos nos domínios monitorados.

## <a name="provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Fornecer um nome de usuário e uma senha para se conectar à sua Floresta do Active Directory

Na primeira vez em que você abre o portal do Azure ATP, a tela a seguir é exibida:

![Estágio 1 de boas-vindas do Azure ATP](media/directory-services.png)


1. Insira as seguintes informações e clique em **Salvar**:

    |Campo|Comentários|
    |---------|------------|
    |**Nome de usuário** (obrigatório)|Insira o nome de usuário somente leitura do Active Directory. Por exemplo: **ATPuser**.  Você deve usar uma conta de usuário do AD **local**. **Não** use o formato UPN para seu nome de usuário.|
    |**Senha** (obrigatório)|Digite a senha para o usuário somente leitura. Por exemplo: **Lápis1**.|
    |**Domínio** (obrigatório)|Digite o domínio para o usuário somente leitura. Por exemplo: **contoso.com**. É importante que você insira o FQDN completo do domínio em que o usuário está localizado. Por exemplo, se a conta do usuário estiver no domínio corp.contoso.com, você precisará inserir `corp.contoso.com` e não contoso.com|

2. No portal do Azure ATP, clique em **Baixar instalação do sensor e instalar o primeiro sensor** para continuar.


## <a name="next-steps"></a>Próximas etapas

> [!div class="step-by-step"]
> [« Etapa 1 — Criar uma instância do ATP do Azure](install-atp-step1.md)
> [Etapa 3 — Baixar a instalação do sensor »](install-atp-step3.md)

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o ATP do Azure e a segurança relacionada com outras pessoas? Participe da [Comunidade do ATP do Azure](https://aka.ms/azureatpcommunity) hoje mesmo!
