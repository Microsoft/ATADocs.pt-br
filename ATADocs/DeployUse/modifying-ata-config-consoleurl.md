---
title: "Alteração da configuração do ATA - Endereço IP do Console do ATA | Microsoft Advanced Threat Analytics"
description: "Descreve como alterar o endereço IP do Console do ATA, usado para criar um atalho até o Console do ATA em Gateways do ATA."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 08/24/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 50118465-df34-4e04-b0cc-48808b6a96b1
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 050f1ef0b39d69b64ede53243a7fa2d33d0e4813
ms.openlocfilehash: b3d11a87f1909c1fd964fa990e5d36a91691a844


---

*Aplica-se a: Advanced Threat Analytics versão 1.7*



# Alteração da configuração do ATA - URL do Console do ATA

>[!div class="step-by-step"]
[«Certificado da Central do ATA](modifying-ata-config-centercert.md)
[Senha de conectividade do domínio »](modifying-ata-config-dcpassword.md)

## Alterar a URL do Console do ATA
Por padrão, a URL do Console do ATA é o endereço IP selecionado como o endereço IP do Console do ATA durante a instalação do Centro do ATA.

A URL é usada nos seguintes cenários:

-   Instalação de Gateways do ATA – Quando um Gateway do ATA é instalado, ele registra ai próprio no Centro do ATA. Esse processo de registro é realizado pela conexão com o Console do ATA. Se você digitar um FQDN para a URL do Console do ATA, será necessário garantir que o Gateway do ATA possa resolver o FQDN para o endereço IP ao qual o Console do ATA está vinculado.

-   Alertas – Quando o ATA envia um SIEM ou alerta de email, ele inclui um link para a atividade suspeita. A parte de host do link é a configuração de URL do Console do ATA.

-   Se você instalou um certificado de sua CA (Autoridade de certificação) interna, provavelmente vai querer corresponder a URL ao nome de entidade no certificado, para que os usuários não recebam uma mensagem de aviso ao se conectar ao Console do ATA.

-   O uso de um FQDN para a URL do Console do ATA permite que você modifique o endereço IP usado pelo Console do ATA sem quebrar os alertas que foram enviados anteriormente, ou precisar baixar novamente o pacote do Gateway do ATA. Você precisa apenas atualizar o DNS com o novo endereço IP.

> [!NOTE]
> Depois de modificar a URL do Console do ATA, você deve baixar o pacote de Instalação do Gateway do ATA antes de instalar novos Gateways do ATA.

Se você precisar modificar a URL do Console do ATA, execute estas etapas no servidor da Central do ATA.

1.  Abra o Console do ATA.

2.  Selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

    ![Ícone Definições de configuração do ATA](media/ATA-config-icon.JPG)

3.  Selecione **Central**.

4.  Em **Endereço de IP do Console**, selecione um dos endereços IP existentes

5.  Em **URL do Console**, modifique a URL, conforme o necessário:

    ![URL do Console do ATA](media/ATA-chge-center-URL.png)
6.  Clique em **Salvar**.

>[!div class="step-by-step"]
[«Certificado da Central do ATA](modifying-ata-config-centercert.md)
[Senha de conectividade do domínio »](modifying-ata-config-dcpassword.md)


## Consulte também
- [Trabalhando com o Console do ATA](working-with-ata-console.md)
- [Instalar o ATA](install-ata.md)
- [Confira o fórum do ATA!](https://aka.ms/ata-forum)



<!--HONumber=Aug16_HO5-->


