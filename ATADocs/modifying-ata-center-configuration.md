---
title: "Alterar a configuração do Centro do ATA do Advanced Threat Analytics | Microsoft Docs"
description: "Descreve como alterar o endereço IP, a porta, a URL do console ou o certificado de seu Centro do ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1e9fa2d104c52087746e7c03fea27e3cb596adf0
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*



<a id="modifying-the-ata-center-configuration" class="xliff"></a>

# Modificar a configuração do Centro do ATA


Após a implantação inicial, as modificações no Centro do ATA deverão ser feitas com cuidado. Use os procedimentos a seguir ao atualizar o endereço IP, a porta, a URL do console e o certificado.

<a id="the-ata-center-ip-address" class="xliff"></a>

## O endereço IP do Centro do ATA

Os Gateways do ATA armazenam localmente o endereço IP do Centro do ATA ao qual eles precisam se conectar. Regularmente, eles se conectam ao Centro do ATA e obtêm as alterações de configuração. Uma alteração no modo como os Gateways do ATA se conectam ao Centro do ATA é feita em dois estágios.

-   Primeiro estágio – Atualize o endereço IP e a porta que você quer que sejam usados pelo serviço da Central do ATA. Nesse ponto, o Centro do ATA ainda está escutando no endereço IP original, e na próxima vez que o Gateway do ATA sincronizar sua configuração ele terá dois endereços IP para o Centro do ATA. Contanto que o Gateway do ATA possa se conectar usando o endereço IP original (primeiro), ele não tentará o novo endereço IP e porta.

-   Segundo estágio – Após a sincronização de todos os Gateways do ATA com a configuração atualizada, ative o novo endereço IP e a porta nos quais o Centro do ATA escuta. Quando você ativar o novo endereço IP, o serviço do Centro do ATA fará uma associação com o novo endereço IP. Os Gateways do ATA não poderão se conectar ao endereço original e agora tentarão se conectar com o segundo endereço IP (novo) para o Centro de ATA. Após a conexão com o Centro do ATA com o novo endereço IP, o Gateway do ATA obterá a configuração mais recente e terá um único endereço IP para o Centro do ATA. (A menos que você tenha iniciado o processo novamente.)

> [!NOTE]
> -   Se um Gateway do ATA estava offline durante o primeira estágio e nunca recebeu a configuração atualizada, será necessário atualizar manualmente o arquivo de configuração JSON no Gateway do ATA.
> -   Se o novo endereço IP estiver instalado no servidor do Centro do ATA, selecione-o na lista de endereços IP ao fazer a alteração. No entanto, se por algum motivo você não conseguiu instalar o endereço IP no servidor do Centro do ATA, selecionar o endereço IP personalizado e adicione-o manualmente. Você não poderá ativar o novo endereço IP até que o endereço IP esteja instalado no servidor.
> -   Se você precisar implantar um novo Gateway do ATA depois de ativar o novo endereço IP, será necessário baixar o pacote de Instalação do Gateway do ATA novamente.

<a id="the-console-url" class="xliff"></a>

## A URL do Console

A URL é usada nos seguintes cenários:

-   Instalação de Gateways do ATA – Quando um Gateway do ATA é instalado, ele registra ai próprio no Centro do ATA. Esse processo de registro é realizado pela conexão com o Console do ATA. Se você digitar um FQDN para a URL do Console do ATA, será necessário garantir que o Gateway do ATA possa resolver o FQDN para o endereço IP ao qual o Console do ATA está vinculado.

-   Alertas – Quando o ATA envia um SIEM ou alerta de email, ele inclui um link para a atividade suspeita. A parte de host do link é a configuração de URL do Console do ATA.

-   Se você instalou um certificado de sua CA (Autoridade de certificação) interna, provavelmente vai querer corresponder a URL ao nome de entidade no certificado, para que os usuários não recebam uma mensagem de aviso ao se conectar ao Console do ATA.

-   O uso de um FQDN para a URL do Console do ATA permite que você modifique o endereço IP usado pelo Console do ATA sem quebrar os alertas que foram enviados anteriormente, ou precisar baixar novamente o pacote do Gateway do ATA. Você precisa apenas atualizar o DNS com o novo endereço IP.

> [!NOTE]
> Depois de modificar a URL do Console do ATA, você deve baixar o pacote de Instalação do Gateway do ATA antes de instalar novos Gateways do ATA.

<a id="the-ata-center-certificate" class="xliff"></a>

## O certificado do Centro do ATA
Se os seus certificados estiverem prestes a expirar e precisarem ser renovados ou substituídos após a instalação do novo certificado no repositório de computador local no servidor do Centro do ATA, substitua o certificado com este processo em dois estágios:

-   Primeiro estágio – Atualizar o certificado que você deseja que o serviço do Centro do ATA use. Neste ponto, o serviço do Centro do ATA ainda está associado ao certificado original. Quando os Gateways do ATA sincronizarem suas configurações, terão dois possíveis certificados que serão válidos para autenticação mútua. Contanto que o Gateway do ATA possa se conectar usando o certificado original, ele não tentará o novo.

-   Segundo estágio – Após a sincronização de todos os Gateways do ATA com a configuração atualizada, você poderá ativar o novo certificado ao qual o serviço do Centro do ATA está associado. Quando você ativar o novo certificado, o serviço do Centro do ATA fará uma associação com o novo certificado. Os Gateways do ATA não serão capazes de autenticar mutuamente de forma correta o serviço do Centro do ATA, e tentarão autenticar o segundo certificado. Após a conexão com o serviço do Centro do ATA, o Gateway do ATA obterá a configuração mais recente e terá um único certificado para o Centro do ATA. (A menos que você tenha iniciado o processo novamente.)

> [!NOTE]
> -   Se um Gateway do ATA estava offline durante o primeira estágio e nunca recebeu a configuração atualizada, será necessário atualizar manualmente o arquivo de configuração JSON no Gateway do ATA.
> -   O certificado que você está usando deve ser de confiança dos Gateways do ATA.
> -   O certificado também é usado para o Console do ATA, portanto, ele deve corresponder ao endereço do Console do ATA a fim de evitar avisos do navegador
> -   Se você precisar implantar um novo Gateway do ATA depois de ativar o novo certificado, será necessário baixar o pacote de Instalação do Gateway do ATA novamente.

<a id="changing-the-ata-center-configuration" class="xliff"></a>

## Alterando a configuração do Centro do ATA

1.  Abra o Console do ATA.

2.  Selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

    ![Ícone Definições de configuração do ATA](media/ATA-config-icon.png)

3.  Selecione **Central**.

  ![Alteração da configuração do ATA](media/change-center-config.png)

4.  Em **URL**, selecione **Adicionar nome DNS/endereço IP personalizado** e o novo DNS ou endereço IP ou, em **Certificado**, selecione o novo certificado.

5.  Clique em **Salvar**.

6.  Você verá uma notificação indicando quantos Gateways do ATA foram sincronizados com a configuração mais recente.

    >[!IMPORTANT]
    >Antes de ativar a nova configuração, valide se todos os Gateways do ATA estão sincronizados com a configuração mais recente. A ativação da nova configuração antes de todos os Gateways do ATA estarem sincronizados pode fazer com que o Gateway do ATA pare de funcionar conforme o esperado. Se algum Gateway do ATA não estiver sincronizado, você receberá este erro ao clicar em Ativar:


7.  Após a sincronização de todos os Gateways do ATA, clique em **Ativar** para ativar o novo endereço IP ou certificado.

    > [!NOTE]
    > Se você inseriu um endereço IP personalizado, não conseguirá clicar em **Ativar** até que tenha instalado o endereço IP no Centro do ATA.

8.  Verifique se todos os Gateways do ATA são capazes de sincronizar suas configurações após a ativação da alteração. A barra de notificação indicará quantos Gateways do ATA tiveram suas configurações sincronizadas.




<a id="see-also" class="xliff"></a>

## Consulte também
- [Trabalhando com o Console do ATA](working-with-ata-console.md)
- [Confira o fórum do ATA!](https://aka.ms/ata-forum)
