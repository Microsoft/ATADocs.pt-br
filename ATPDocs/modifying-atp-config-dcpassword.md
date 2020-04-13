---
title: Alterar a configuração da Proteção Avançada contra Ameaças do Azure – senha de conectividade de domínio
description: Descreve como alterar a senha de conectividade de domínio no sensor autônomo do Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 02/19/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: e7f065fa-1ad1-4e87-bd80-99cc695efbf5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 77ec242769d15eb3681f9e511709a0e6953878e8
ms.sourcegitcommit: bf5f58317121f1fb0fffc83d8b419cdd7ef27d9a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/05/2020
ms.locfileid: "80669515"
---
# <a name="change-azure-atp-portal-configuration---domain-connectivity-password"></a>Alterar a configuração do portal do ATP do Azure – senha de conectividade de domínio

## <a name="change-the-domain-connectivity-password"></a>Alterar a senha de conectividade do domínio

Se você precisar modificar a senha de conectividade de domínio, certifique-se de que a senha digitada esteja correta. Se não estiver, o serviço de sensor do Azure ATP será interrompido para todos os sensores implantados.

Se você suspeitar que isso aconteceu, examine o arquivo Microsoft.Tri.sensor-Errors.log em busca dos seguintes erros: `The supplied credential is invalid.`

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

- [Integração com o Microsoft Defender ATP](integrate-wd-atp.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
