---
title: "Alteração da configuração do ATA – senha de conectividade do domínio | Microsoft ATA"
description: "Descreve como alterar a Senha de conectividade do domínio no Gateway do ATA."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 7b8904bcb379004b2038e6b9a14c87c3914f1e1f


---

# Alteração da configuração do ATA - senha de conectividade do domínio

>[!div class="step-by-step"]
[« Certificado IIS](modifying-ata-config-iiscert.md)


## Alterar a senha de conectividade do domínio
Se você modificar a senha de conectividade do domínio, certifique-se de que a senha digitada esteja correta. Se não estiver, o serviço do Gateway do ATA deixará de ser executado em Gateways do ATA.

Se você suspeitar que isso aconteceu, no Gateway do ATA, examine o arquivo Microsoft.Tri.Gateway-Errors.log em busca do seguinte:
`The supplied credential is invalid.`

Para corrigir isso, siga este procedimento e atualize a Senha de conectividade do domínio no Gateway do ATA:

1.  Abra o Console do ATA no Gateway do ATA.

2.  Selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

    ![Ícone Definições de configuração do ATA](media/ATA-config-icon.JPG)

3.  Selecione **Geral**.

    ![Imagem da mudança de senha no Gateway do ATA](media/ATA-GW-change-DC-password.JPG)

4.  Em **Geral**, altere a senha.

5.  Clique em **Salvar**.

6.  Depois de alterar a senha, verifique manualmente se o serviço do Gateway do ATA está em execução nos servidores do Gateway do ATA.

>[!div class="step-by-step"]
[« Certificado IIS](modifying-ata-config-iiscert.md)

## Consulte também
- [Trabalhando com o Console do ATA](working-with-ata-console.md)
- [Instalar o ATA](install-ata.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO4-->


