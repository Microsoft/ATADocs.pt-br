---
title: "Alteração da configuração do ATA – Endereço IP do Centro do ATA | Microsoft ATA"
description: "Descreve como alterar o endereço IP, porta ou certificado de seu Centro do ATA."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 4eb552b9f7d42895abf08ec4cd9216b5204c5e0b


---

# Alteração da configuração do ATA - Endereço IP do Centro do ATA

>[!div class="step-by-step"]
[Certificado do Centro do ATA »](modifying-ata-config-centercert.md)

Após a implantação inicial, as modificações no Centro do ATA deverão ser feitas com cuidado. Use os procedimentos a seguir ao atualizar o endereço IP e a porta ou o certificado.

## Alteração do endereço IP usado pelo servidor do Centro do ATA
Se você precisar alterar o endereço IP do Centro do ATA, além da porta ou do certificado, leve o seguinte em consideração.

Os Gateways do ATA armazenam localmente o endereço IP do Centro do ATA ao qual eles precisam se conectar. Regularmente, eles se conectam ao Centro do ATA e obtêm as alterações de configuração. Uma alteração no modo como os Gateways do ATA se conectam ao Centro do ATA é feita em dois estágios.

-   Primeiro estágio – Atualize o endereço IP e a porta que você quer que sejam usados pelo serviço da Central do ATA. Nesse ponto, o Centro do ATA ainda está escutando no endereço IP original, e na próxima vez que o Gateway do ATA sincronizar sua configuração ele terá dois endereços IP para o Centro do ATA. Contanto que o Gateway do ATA possa se conectar usando o endereço IP original (primeiro), ele não tentará o novo endereço IP e porta.

-   Segundo estágio – Após a sincronização de todos os Gateways do ATA com a configuração atualizada, ative o novo endereço IP e a porta nos quais o Centro do ATA escuta. Quando você ativar o novo endereço IP, o serviço do Centro do ATA fará uma associação com o novo endereço IP. Os Gateways do ATA não poderão se conectar ao endereço original e agora tentarão se conectar com o segundo endereço IP (novo) para o Centro de ATA. Após a conexão com o Centro do ATA com o novo endereço IP, o Gateway do ATA obterá a configuração mais recente e terá um único endereço IP para o Centro do ATA. (A menos que você tenha iniciado o processo novamente.)

> [!NOTE]
> -   Se um Gateway do ATA estava offline durante o primeira estágio e nunca recebeu a configuração atualizada, será necessário atualizar manualmente o arquivo de configuração JSON no Gateway do ATA.
> -   Se o novo endereço IP estiver instalado no servidor do Centro do ATA, selecione-o na lista de endereços IP ao fazer a alteração. No entanto, se por algum motivo você não conseguiu instalar o endereço IP no servidor do Centro do ATA, selecionar o endereço IP personalizado e adicione-o manualmente. Você não poderá ativar o novo endereço IP até que o endereço IP esteja instalado no servidor.
> -   Se você precisar implantar um novo Gateway do ATA depois de ativar o novo endereço IP, será necessário baixar o pacote de Instalação do Gateway do ATA novamente.

1.  Abra o Console do ATA.

2.  Selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

    ![Ícone Definições de configuração do ATA](media/ATA-config-icon.JPG)

3.  Selecione **Geral**.

4.  Em **Endereço IP do Serviço do Centro do ATA: porta**, escolha um dos endereços IP existentes ou selecione **Adicionar endereço IP personalizado** e digite um endereço IP.

5.  Clique em **Salvar**.

6.  Você verá uma notificação indicando quantos Gateways do ATA foram sincronizados com a configuração mais recente.

    ![Imagem de gateways sincronizados no Centro do ATA](media/ATA-chge-IP-after-clicking-save.png)

    >[!IMPORTANT]
    >Antes de ativar a nova configuração, valide se todos os Gateways do ATA estão sincronizados com a configuração mais recente. A ativação da nova configuração antes de todos os Gateways do ATA estarem sincronizados pode fazer com que o Gateway do ATA pare de funcionar conforme o esperado. Se algum Gateway do ATA não estiver sincronizado, você receberá este erro ao clicar em Ativar:
    >
    >    ![Erro de sincronização de Gateway do ATA](media/ataGW-not-synced.png)


7.  Após a sincronização de todos os Gateways do ATA, clique em **Ativar** para ativar o novo endereço IP.

    > [!NOTE]
    > Se você inseriu um endereço IP personalizado, não conseguirá clicar em **Ativar** até que tenha instalado o endereço IP no Centro do ATA.

8.  Verifique se todos os Gateways do ATA são capazes de sincronizar suas configurações após a ativação da alteração. A barra de notificação indicará quantos Gateways do ATA tiveram suas configurações sincronizadas.

>[!div class="step-by-step"]
[Alteração do certificado do Centro do ATA »](modifying-ata-config-centercert.md)


## Consulte também
- [Trabalhando com o Console do ATA](working-with-ata-console.md)
- [Instalar o ATA](install-ata.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO4-->


