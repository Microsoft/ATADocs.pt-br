---
# required metadata

title: Alteração da configuração do ATA - senha de conectividade do domínio | Microsoft Advanced Threat Analytics
description: Descreve como alterar a Senha de conectividade do domínio no Gateway do ATA.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

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

2.  Selecione a opção de configurações na barra de ferramentas e selecione **Configuração**.

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
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


