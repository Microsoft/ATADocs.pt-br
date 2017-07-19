---
title: "Instalação do Advanced Threat Analytics – Etapa 2 | Microsoft Docs"
description: "A etapa dois da instalação do ATA ajuda você a definir as configurações de conectividade do domínio em seu servidor do Centro do ATA"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/2/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: aa5e752fa10644165cb70d2cd8c08a1145261edb
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*



# <a name="install-ata---step-2"></a>Instalação do ATA - Etapa 2

>[!div class="step-by-step"]
[« Etapa 1](install-ata-step1.md)
[Etapa 3 »](install-ata-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Etapa 2. Forneça um Nome de usuário e uma Senha para se conectar à sua Floresta do Active Directory

Na primeira vez que você abrir o Console do ATA, a tela a seguir será exibida:

![Estágio 1 das boas-vindas do ATA](media/ATA_1.7-welcome-provide-username.png)

1.  Insira as seguintes informações e clique em **Salvar**:

    |Campo|Comentários|
    |---------|------------|
    |**Nome de usuário** (obrigatório)|Insira o nome de usuário somente leitura, por exemplo: **ATAuser**.|
    |**Senha** (obrigatório)|Digite a senha para o usuário somente leitura, por exemplo: **Lápis1**.|
    |**Domínio** (obrigatório)|Digite o domínio para o usuário somente leitura, por exemplo: **contoso.com**. **Observação:** é importante que você insira o FQDN completo do domínio onde o usuário está localizado. Por exemplo, se a conta do usuário estiver no domínio corp.contoso.com, você precisará inserir `corp.contoso.com` e não contoso.com|

2. Você pode clicar em **Testar conexão** para testar a conectividade com o domínio e verificar se as credenciais fornecidas concedem acesso. Isso só funcionará se o Centro do ATA tiver conectividade com o domínio.   

    Após a gravação, a mensagem de boas-vindas no Console mudará para o seguinte: ![Estágio 1 das boas-vindas do ATA concluído](media/ATA_1.7-welcome-provide-username-finished.png)

3. No Console, clique em **Baixar instalação do Gateway e instalar o primeiro Gateway** para continuar.


>[!div class="step-by-step"]
[« Etapa 1](install-ata-step1.md)
[Etapa 3 »](install-ata-step3.md)


## <a name="see-also"></a>Consulte Também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)
