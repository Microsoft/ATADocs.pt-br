---
# required metadata

title: Alteração da configuração do ATA - Certificado IIS | Microsoft Advanced Threat Analytics
description: Descreve como alterar o certificado usado pelo IIS para o Centro do ATA.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e58a0390-57ef-4c68-a987-2e75e5f3d6b3

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Alteração da configuração do ATA - Certificado IIS

>[!div class="step-by-step"]
[« Endereço IP do Console do ATA](modifying-ata-config-consoleip.md)
[Senha de conectividade do domínio »](modifying-ata-config-dcpassword.md)

## Alteração do certificado IIS
No console, você pode selecionar e alterar o certificado do serviço do Centro do ATA, mas não é possível alterar o certificado usado pelo IIS.

Se você quiser alterá-lo, use o procedimento a seguir:

> [!NOTE]
> Depois de modificar o Certificado IIS, você deve baixar o pacote de Instalação do Gateway do ATA antes de instalar novos Gateways do ATA.

Se você precisar modificar o certificado usado pelo IIS para o Centro do ATA, execute estas etapas no servidor do Centro do ATA.

1.  Instale o novo certificado no servidor do Centro do ATA.

2.  Abra o Gerenciador dos Serviços de Informações da Internet (IIS).

3.  Expanda o nome do servidor e expanda **Sites**.

4.  Selecione o site do Console do Microsoft ATA e, no painel **Ações**, clique em **Associações**.

    ![Ações de associações do Console do ATA](media/ATA-console-change-IP-bindings.jpg)

5.  Selecione **HTTPS** e clique em **Editar**.

6.  Em **Certificado SSL**, selecione o novo certificado.

7.  Baixe o pacote de Instalação do Gateway do ATA antes de instalar um novo Gateway do ATA.

>[!div class="step-by-step"]
[« Endereço IP do Console do ATA](modifying-ata-config-consoleip.md)
[Senha de conectividade do domínio »](modifying-ata-config-dcpassword.md)

## Consulte também
- [Trabalhando com o Console do ATA](working-with-ata-console.md)
- [Instalar o ATA](install-ata.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


