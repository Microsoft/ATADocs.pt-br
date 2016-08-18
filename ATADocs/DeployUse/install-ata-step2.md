---
title: "Instalar o ATA – Etapa 2 | Microsoft ATA"
description: "A etapa dois da instalação do ATA ajuda você a definir as configurações de conectividade do domínio em seu servidor do Centro do ATA"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 65ec5c86478e9ded096b899d64eb257257095eaf


---

# Instalação do ATA - Etapa 2

>[!div class="step-by-step"]
[« Etapa 1](install-ata-step1.md)
[Etapa 3 »](install-ata-step3.md)

## Etapa 2. Definir configurações gerais do Gateway do ATA
As definições na guia de configurações **Gerais** se aplicam a todos os Gateways do ATA gerenciados pelo Centro do ATA.

Para definir as configurações gerais do Gateway do ATA, siga este procedimento:

1.  Abra o Console do ATA e faça logon. Para obter instruções, confira [Working with the ATA Console](working-with-ata-console.md) (Como trabalhar com o Console do ATA).

2.  Clique no ícone Configurações e selecione **Configuração**.

    ![Definições de configuração do Gateway do ATA](media/ATA-config-icon.JPG)

3.  Na guia **Geral**, em **Gateways do ATA**, insira as informações a seguir e clique em **Salvar**.

    |Campo|Comentários|
    |---------|------------|
    |**Nome de usuário** (obrigatório)|Insira o nome de usuário somente leitura, por exemplo: **usuário1**.|
    |**Senha** (obrigatório)|Digite a senha para o usuário somente leitura, por exemplo: **Lápis1**. **Observação:** certifique-se de que essa senha esteja correta. Se você salvar a senha incorreta, o Serviço do ATA interromperá a execução nos servidores de Gateway do ATA.|
    |**Domínio** (obrigatório)|Digite o domínio para o usuário somente leitura, por exemplo: **contoso.com**. **Observação:** é importante que você insira o FQDN completo do domínio onde o usuário está localizado. Por exemplo, se a conta do usuário estiver no domínio corp.contoso.com, você precisará inserir `corp.contoso.com` e não contoso.com|
    |Atualizar todos os Gateways do ATA automaticamente |Se você habilitar essa configuração, nos lançamentos de versões futuras, quando você atualizar o Centro do ATA, todos os Gateways do ATA serão automaticamente atualizados.|

    ![Imagem configurações de conectividade do Domínio do ATA](media/ata-domain-connectivity-user.jpg)



>[!div class="step-by-step"]
[« Etapa 1](install-ata-step1.md)
[Etapa 3 »](install-ata-step3.md)


## Consulte também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Jul16_HO4-->


