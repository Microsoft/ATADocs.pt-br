---
title: Alterar o Microsoft defender para configuração de identidade-senha de conectividade do domínio
description: Descreve como alterar a senha de conectividade de domínio no sensor autônomo do Microsoft defender para identidade.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ef931c90558ffaea1a24d8682cc8091a845aeea8
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94847404"
---
# <a name="change-product-long-portal-configuration---domain-connectivity-password"></a>Alterar [!INCLUDE [Product long](includes/product-long.md)] configuração do portal-senha de conectividade do domínio

## <a name="change-the-domain-connectivity-password"></a>Alterar a senha de conectividade do domínio

Se você precisar modificar a senha de conectividade de domínio, certifique-se de que a senha digitada esteja correta. Se não for, o [!INCLUDE [Product long](includes/product-long.md)] serviço de sensor será interrompido para todos os sensores implantados.

Se você suspeitar que isso ocorreu, examine o arquivo Microsoft. Tri. sensor-Errors. log para os seguintes erros: `The supplied credential is invalid.`

Siga este procedimento para atualizar a senha de conectividade do domínio no [!INCLUDE [Product short](includes/product-short.md)] Portal:

> [!NOTE]
> Trata-se do nome de usuário e senha da implantação local do Active Directory e não do Azure AD.

1. Abra o [!INCLUDE [Product short](includes/product-short.md)] portal acessando a URL do Portal.

1. Selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

    ![Ícone de definições de configuração do [!INCLUDE [Product short](includes/product-short.md)]](media/config-menu.png)

1. Selecione **Serviços de Diretório**.

    ![[! INCLUIR [produto curto] (inclui/Product-short. MD)] imagem de alteração de senha do sensor autônomo](media/directory-services.png)

1. Em **Senha**, altere a senha.

    > [!NOTE]
    > Insira aqui um usuário e senha do Active Directory e não no Azure Active Directory.

1. Clique em **Save** (Salvar).

1. No portal do [!INCLUDE [Product short](includes/product-short.md)], selecione **Configuração**.
1. Em **sistema**, selecione a página **sensores** e verifique o status dos sensores.

## <a name="see-also"></a>Consulte Também

- [Integração ao Microsoft Defender para Ponto de Extremidade](integrate-mde.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
