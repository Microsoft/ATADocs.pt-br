---
title: Instalação do Advanced Threat Analytics – Etapa 3 | Microsoft Docs
description: A etapa três da instalação do ATA ajuda você a baixar o pacote de instalação do Gateway do ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 7fb024e6-297a-4ad9-b962-481bb75a0ba3
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 15d1ea65e18f8557c4d36363a381d05c0f9421a7
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "65195877"
---
# <a name="install-ata---step-3"></a>Instalação do ATA - Etapa 3

*Aplica-se a: Advanced Threat Analytics versão 1.9*

> [!div class="step-by-step"]
> [« Etapa 2](install-ata-step2.md)
> [Etapa 4 »](install-ata-step4.md)

## <a name="step-3-download-the-ata-gateway-setup-package"></a>Etapa 3. Baixe o pacote de instalação do Gateway do ATA

Após definir as configurações de conectividade do domínio, você poderá baixar o pacote de instalação do Gateway do ATA. O Gateway do ATA do pode ser instalado em um servidor dedicado ou em um controlador de domínio. Se você instalá-lo em um controlador de domínio, ele será instalado como um Gateway Lightweight do ATA. Para obter mais informações sobre o Gateway Lightweight do ATA, confira [Arquitetura do ATA](ata-architecture.md). 

Clique em **Baixar Instalação do Gateway** na lista de etapas na parte superior da página para ir para a página **Gateways**.

![Definições de configuração do Gateway do ATA](media/ATA_1.7-welcome-download-gateway.PNG)

> [!NOTE] 
> Para acessar a tela de configuração Gateway posteriormente, clique no **ícone de configurações** (canto superior direito) e selecione **Configuração** e em **Sistema**, clique em **Gateways**.  

1.  Clique em **Instalação do Gateway**.
  ![Baixar a Instalação do Gateway do ATA](media/download-gateway-setup.png)
2.  Salve o pacote localmente.
3.  Copie o pacote para o servidor dedicado ou controlador de domínio no qual você está instalando o Gateway do ATA Como alternativa, você pode abrir o Console do ATA do controlador de domínio ou servidor dedicado e ignorar esta etapa.

O arquivo zip inclui os seguintes arquivos:

-   Instalador do Gateway do ATA

-   Arquivo de configurações com as informações necessárias para conectar-se à Central de ATA


> [!div class="step-by-step"]
> [« Etapa 2](install-ata-step2.md)
> [Etapa 4 »](install-ata-step4.md)


## <a name="related-videos"></a>Vídeos Relacionados
- [Visão geral da implantação do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Como escolher o tipo certo de Gateway do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>Confira Também
- [Guia de implantação da POC (prova de conceito) do ATA](http://aka.ms/atapoc)
- [Ferramenta de dimensionamento do ATA](http://aka.ms/atasizingtool)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)
