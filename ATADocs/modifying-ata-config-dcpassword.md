---
title: Alteração da configuração do Advanced Threat Analytics – senha de conectividade do domínio | Microsoft Docs
description: Descreve como alterar a Senha de conectividade do domínio no Gateway do ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 8dfee189f0be42e2d488506a0eaf950107061357
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54839904"
---
# <a name="change-ata-configuration---domain-connectivity-password"></a>Alteração da configuração do ATA - senha de conectividade do domínio

*Aplica-se a: Advanced Threat Analytics versão 1.9*

## <a name="change-the-domain-connectivity-password"></a>Alterar a senha de conectividade do domínio

Se você modificar a senha de conectividade do domínio, certifique-se de que a senha digitada esteja correta. Se não estiver, o serviço do Gateway do ATA deixará de ser executado em Gateways do ATA.

Se você suspeitar que isso aconteceu, no Gateway do ATA, examine o arquivo Microsoft.Tri.Gateway-Errors.log em busca dos seguintes erros: `The supplied credential is invalid.`

Para corrigir isso, siga este procedimento e atualize a Senha de conectividade do domínio na Central do ATA:

1.  Abra o Console do ATA na Central do ATA.

2.  Selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

    ![Ícone Definições de configuração do ATA](media/ATA-config-icon.png)

3.  Selecione **Serviços de Diretório**.

    ![Imagem da mudança de senha no Gateway do ATA](media/ATA-GW-change-DC-password.png)

4.  Em **Senha**, altere a senha.

    Se o Centro do ATA tiver conectividade com o domínio, use o botão **Testar Conexão** para validar as credenciais

5.  Clique em **Salvar**.

6.  Depois de alterar a senha, verifique manualmente se o serviço do Gateway do ATA está em execução nos servidores do Gateway do ATA.



## <a name="see-also"></a>Consulte Também
- [Trabalhando com o Console do ATA](working-with-ata-console.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
