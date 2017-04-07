---
title: "Alteração da configuração do Advanced Threat Analytics – senha de conectividade do domínio | Microsoft Docs"
description: "Descreve como alterar a Senha de conectividade do domínio no Gateway do ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e9cb7bcf6f32559f7b2f330df4333c3fdc55a283
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*Aplica-se a: Advanced Threat Analytics versão 1.7*



# <a name="change-ata-configuration---domain-connectivity-password"></a>Alteração da configuração do ATA - senha de conectividade do domínio

>[!div class="step-by-step"]
[« URL do Console do ATA](modifying-ata-config-consoleurl.md)


## <a name="change-the-domain-connectivity-password"></a>Alterar a senha de conectividade do domínio
Se você modificar a senha de conectividade do domínio, certifique-se de que a senha digitada esteja correta. Se não estiver, o serviço do Gateway do ATA deixará de ser executado em Gateways do ATA.

Se você suspeitar que isso aconteceu, no Gateway do ATA, examine o arquivo Microsoft.Tri.Gateway-Errors.log em busca do seguinte: `The supplied credential is invalid.`

Para corrigir isso, siga este procedimento e atualize a Senha de conectividade do domínio na Central do ATA:

1.  Abra o Console do ATA na Central do ATA.

2.  Selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

    ![Ícone Definições de configuração do ATA](media/ATA-config-icon.JPG)

3.  Selecione **Serviços de Diretório**.

    ![Imagem da mudança de senha no Gateway do ATA](media/ATA-GW-change-DC-password.png)

4.  Em **Senha**, altere a senha.

    Se a Central do ATA tiver conectividade com o domínio, use o botão **Testar Conexão** para validar as credenciais

5.  Clique em **Salvar**.

6.  Depois de alterar a senha, verifique manualmente se o serviço do Gateway do ATA está em execução nos servidores do Gateway do ATA.

>[!div class="step-by-step"]
[« URL do Console do ATA](modifying-ata-config-consoleurl.md)

## <a name="see-also"></a>Consulte Também
- [Trabalhando com o Console do ATA](working-with-ata-console.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
