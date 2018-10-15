---
title: Alterar a configuração da Proteção Avançada contra Ameaças do Azure – senha de conectividade de domínio | Microsoft Docs
description: Descreve como alterar a senha de conectividade de domínio no sensor autônomo do Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: e7f065fa-1ad1-4e87-bd80-99cc695efbf5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a175a23a087b11d481dbcf055bff4fe5577b4f8e
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783110"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*



# <a name="change-azure-atp-workspace-portal-configuration---domain-connectivity-password"></a>Alterar a configuração do portal do espaço de trabalho do Azure ATP – senha de conectividade de domínio



## <a name="change-the-domain-connectivity-password"></a>Alterar a senha de conectividade do domínio
Se você precisar modificar a senha de conectividade de domínio, certifique-se de que a senha digitada esteja correta. Se não estiver, o serviço de sensor do Azure ATP será interrompido para todos os sensores implantados.

Se você suspeitar que isso aconteceu, no sensor autônomo do Azure ATP, examine o arquivo Microsoft.Tri.sensor-Errors.log em busca dos seguintes erros: `The supplied credential is invalid.`

Siga este procedimento para atualizar a senha da Conectividade de domínio no portal do Azure ATP:

> [!NOTE]
> Trata-se do nome de usuário e senha da implantação local do Active Directory e não do Azure AD.

1.  Abra o portal do Azure ATP acessando a URL do workspace.

2.  Selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

    ![Ícone de definições de configuração do Azure ATP](media/atp-config-menu.png)

3.  Selecione **Serviços de Diretório**.

    ![Imagem da senha de alteração do sensor autônomo do Azure ATP](media/directory-services.png)

4.  Em **Senha**, altere a senha.

 > [!NOTE]
 > Insira aqui um usuário e senha do Active Directory e não no Azure Active Directory.

5.  Clique em **Salvar**.

6.  Depois de alterar a senha, verifique manualmente se o serviço do sensor autônomo do Azure ATP está em execução nos servidores do sensor autônomo do Azure ATP.

7. No portal do Azure ATP, em **Configuração**, vá até a página **Sensor** e verifique o status dos sensores.

## <a name="see-also"></a>Consulte Também

- [Integração com o Windows Defender ATP](integrate-wd-atp.md)
- [Confira o fórum do Azure ATP!](https://aka.ms/azureatpcommunity)