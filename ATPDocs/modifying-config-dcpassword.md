---
title: Alterar configuração da proteção avançada contra ameaças do Azure-senha de conectividade do domínio
description: Descreve como alterar a senha de conectividade de domínio no sensor autônomo do Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 02/19/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: e7f065fa-1ad1-4e87-bd80-99cc695efbf5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 3d35651f0741caa6189ae8ef79e14e8b0db78eff
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90827978"
---
# <a name="change-azure-atp-portal-configuration---domain-connectivity-password"></a>Alterar a configuração do portal do ATP do Azure – senha de conectividade de domínio

## <a name="change-the-domain-connectivity-password"></a>Alterar a senha de conectividade do domínio

Se você precisar modificar a senha de conectividade de domínio, certifique-se de que a senha digitada esteja correta. Se não estiver, o serviço de sensor do Azure ATP será interrompido para todos os sensores implantados.

Se você suspeitar que isso ocorreu, examine o arquivo Microsoft. Tri. sensor-Errors. log para os seguintes erros: `The supplied credential is invalid.`

Siga este procedimento para atualizar a senha da Conectividade de domínio no portal do Azure ATP:

> [!NOTE]
> Trata-se do nome de usuário e senha da implantação local do Active Directory e não do Azure AD.

1. Abra o portal do ATP do Azure, acessando o portal de URL.

1. Selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

    ![Ícone de definições de configuração do Azure ATP](media/atp-config-menu.png)

1. Selecione **Serviços de Diretório**.

    ![Imagem da senha de alteração do sensor autônomo do Azure ATP](media/directory-services.png)

1. Em **Senha**, altere a senha.

    > [!NOTE]
    > Insira aqui um usuário e senha do Active Directory e não no Azure Active Directory.

1. Clique em **Salvar**.

1. No portal do Azure ATP, em **Configuração**, vá até a página **Sensor** e verifique o status dos sensores.

## <a name="see-also"></a>Consulte Também

- [Integração com o Microsoft Defender ATP](integrate-msde.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
