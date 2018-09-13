---
title: Instalar a Proteção Avançada contra Ameaças do Azure – etapa 2 | Microsoft Docs
description: A etapa dois da instalação do Azure ATP ajuda a definir as configurações de conectividade do domínio em seu serviço de nuvem do Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ae8a95f0-278c-4a12-ae69-14282364fba1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b2f83da3192770ddde05b04bed46a558a4491290
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44125882"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*



# <a name="install-azure-atp---step-2"></a>Instalar o Azure ATP – etapa 2

>[!div class="step-by-step"]
[« Etapa 1](install-atp-step1.md)
[Etapa 3 »](install-atp-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>Etapa 2. Fornecer um nome de usuário e uma senha para se conectar à sua Floresta do Active Directory

Na primeira vez em que você abre o portal do espaço de trabalho do Azure ATP, a tela a seguir é exibida:

![Estágio 1 de boas-vindas do Azure ATP](media/directory-services.png)

> [!IMPORTANT]
> Aqui, as credenciais do usuário devem ser de uma conta de usuário no Active Directory local. 


1.  Insira as seguintes informações e clique em **Salvar**:

    |Campo|Comentários|
    |---------|------------|
    |**Nome de usuário** (obrigatório)|Insira o nome de usuário somente leitura do Active Directory, por exemplo: **ATPuser**.|
    |**Senha** (obrigatório)|Digite a senha para o usuário somente leitura, por exemplo: **Lápis1**.|
    |**Domínio** (obrigatório)|Digite o domínio para o usuário somente leitura, por exemplo: **contoso.com**. **Observação:** é importante que você insira o FQDN completo do domínio onde o usuário está localizado. Por exemplo, se a conta do usuário estiver no domínio corp.contoso.com, você precisará inserir `corp.contoso.com` e não contoso.com|

3. No portal do espaço de trabalho, clique em **Baixar instalação do sensor e instalar o primeiro sensor** para continuar.


>[!div class="step-by-step"]
[« Etapa 1](install-atp-step1.md)
[Etapa 3 »](install-atp-step3.md)


## <a name="see-also"></a>Consulte Também
- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/aatpsizingtool)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)