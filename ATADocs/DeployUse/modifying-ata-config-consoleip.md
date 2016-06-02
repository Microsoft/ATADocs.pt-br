---
# required metadata

title: Alteração da configuração do ATA - Endereço IP do Console do ATA | Microsoft Advanced Threat Analytics
description: Descreve como alterar o endereço IP do Console do ATA, usado para criar um atalho até o Console do ATA em Gateways do ATA.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 50118465-df34-4e04-b0cc-48808b6a96b1

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Alteração da configuração do ATA - Endereço IP do Console do ATA

>[!div class="step-by-step"]
[« Certificado do Centro do ATA](modifying-ata-config-centercert.md)
[Certificado IIS »](modifying-ata-config-iiscert.md)

## Alterar o endereço IP do Console do ATA
Por padrão, a URL do Console do ATA é o endereço IP selecionado como o endereço IP do Console do ATA durante a instalação do Centro do ATA.

A URL é usada nos seguintes cenários:

-   Instalação de Gateways do ATA – Quando um Gateway do ATA é instalado, ele registra ai próprio no Centro do ATA. Esse processo de registro é realizado pela conexão com o Console do ATA. Se você digitar um FQDN para a URL do Console do ATA, será necessário garantir que o Gateway do ATA possa resolver o FQDN para o endereço IP ao qual o Console do ATA está vinculado em um IIS. Além disso, a URL é usada para criar o atalho até o Console do ATA em Gateways do ATA.

-   Alertas – Quando o ATA envia um SIEM ou alerta de email, ele inclui um link para a atividade suspeita. A parte de host do link é a configuração de URL do Console do ATA.

-   Se você instalou um certificado de sua CA (Autoridade de certificação) interna, provavelmente vai querer corresponder a URL ao nome de entidade no certificado, para que os usuários não recebam uma mensagem de aviso ao se conectar ao Console do ATA.

-   O uso de um FQDN para a URL do Console do ATA permite que você modifique o endereço IP usado pelo IIS para o Console do ATA sem quebrar os alertas que foram enviados anteriormente, ou precisar baixar novamente o pacote do Gateway do ATA. Você precisa apenas atualizar o DNS com o novo endereço IP.

> [!NOTE]
> Depois de modificar a URL do Console do ATA, você deve baixar o pacote de Instalação do Gateway do ATA antes de instalar novos Gateways do ATA.

Se você precisar modificar o endereço IP usado pelo IIS para o Console do ATA, execute estas etapas no servidor do Centro do ATA.

1.  Instale o endereço IP no servidor do Centro do ATA.

2.  Abra o Gerenciador dos Serviços de Informações da Internet (IIS).

3.  Expanda o nome do servidor e expanda **Sites**.

4.  Selecione o site do Console do Microsoft ATA e, no painel **Ações**, clique em **Associações**.

    ![Imagem de ação de associações do Console do ATA](media/ATA-console-change-IP-bindings.jpg)

5.  Selecione **HTTP** e clique em **Editar** para selecionar o novo endereço IP. Faça o mesmo para **HTTPS**, selecionando o mesmo endereço IP.

    ![Imagem de edição de associação do site](media/ATA-change-console-IP.jpg)

6.  No painel **Ação**, clique em **Reiniciar** em **Gerenciar Site**.

7.  Abra um prompt de comando do administrador e digite os comandos a seguir para atualizar o driver HTTP.SYS:

    -   Para adicionar o novo endereço IP - `netsh http add iplisten ipaddress=newipaddress`

    -   Para ver se o novo endereço está sendo usado - `netsh http show iplisten`

    -   Para excluir o endereço IP antigo – `netsh http delete iplisten ipaddress=oldipaddress`

8.  Se a URL do Console do ATA ainda estiver usando um endereço IP, atualize a URL do Console do ATA para o novo endereço IP e baixe o pacote de Instalação do Gateway do ATA antes de implantar novos Gateways do ATA.

9. Se a URL do Console do ATA for um FQDN, atualize o DNS com o novo endereço IP para o FQDN.

>[!div class="step-by-step"]
[« Certificado do Centro do ATA](modifying-ata-config-centercert.md)
[Certificado IIS »](modifying-ata-config-iiscert.md)


## Consulte também
- [Trabalhando com o Console do ATA](working-with-ata-console.md)
- [Instalar o ATA](install-ata.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


