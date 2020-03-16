---
title: Instalar o Advanced Threat Analytics – etapa 2
description: A etapa dois da instalação do ATA ajuda você a definir as configurações de conectividade do domínio em seu servidor do Centro do ATA
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 12/30/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ff20bf7da1586090d2728015f08cf94d432df38f
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2020
ms.locfileid: "79410452"
---
# <a name="install-ata---step-2"></a>Instalação do ATA - Etapa 2

*Aplica-se a: Advanced Threat Analytics versão 1.9*

> [!div class="step-by-step"]
> [« Etapa 1](install-ata-step1.md)
> [Etapa 3 »](install-ata-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Etapa 2. Forneça um Nome de usuário e uma Senha para se conectar à sua Floresta do Active Directory

Na primeira vez que você abrir o Console do ATA, a tela a seguir será exibida:

![Estágio 1 das boas-vindas do ATA](media/ATA_1.7-welcome-provide-username.png)

1.  Insira as seguintes informações e clique em **Salvar**:

    |Campo|Comentários|
    |---------|------------|
    |**Nome de usuário** (obrigatório)|Insira o nome de usuário somente leitura, por exemplo: **ATAuser**. **Observação:** **Não** use o formato UPN para seu nome de usuário.|
    |**Senha** (obrigatório)|Digite a senha para o usuário somente leitura, por exemplo: **Lápis1**.|
    |**Domínio** (obrigatório)|Digite o domínio para o usuário somente leitura, por exemplo: **contoso.com**. **Observação:** é importante que você insira o FQDN completo do domínio onde o usuário está localizado. Por exemplo, se a conta do usuário estiver no domínio corp.contoso.com, você precisará inserir `corp.contoso.com` e não contoso.com|

2. Você pode clicar em **Testar conexão** para testar a conectividade com o domínio e verificar se as credenciais fornecidas concedem acesso. Isso só funciona se o Centro do ATA tiver conectividade com o domínio.    

    Após a gravação, a mensagem de boas-vindas no Console mudará para a seguinte mensagem: ![Estágio 1 das boas-vindas do ATA concluído](media/ATA_1.7-welcome-provide-username-finished.png)

3. No Console, clique em **Baixar instalação do Gateway e instalar o primeiro Gateway** para continuar.


> [!div class="step-by-step"]
> [« Etapa 1](install-ata-step1.md)
> [Etapa 3 »](install-ata-step3.md)


## <a name="see-also"></a>Confira Também
## <a name="related-videos"></a>Vídeos relacionados
- [Visão geral da implantação do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Como escolher o tipo certo de Gateway do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Confira Também
- [Guia de implantação da POC (prova de conceito) do ATA](https://aka.ms/atapoc)
- [Ferramenta de dimensionamento do ATA](https://aka.ms/atasizingtool)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)
