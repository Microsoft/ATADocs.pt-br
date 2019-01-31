---
title: Instalar a Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: A etapa três da instalação do Azure ATP ajuda a baixar o pacote de instalação do sensor do Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/02/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 95bb4ec1-841f-41b7-92fe-fbd144085724
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4816fe56b8a28d349c970be5a304d025875de748
ms.sourcegitcommit: 19ff0ed88e450506b5725bbcbb0d0bd2f0c5e4bb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/27/2019
ms.locfileid: "55085224"
---
# <a name="install-azure-atp---step-3"></a>Instalar o Azure ATP – etapa 3

> [!div class="step-by-step"]
> [« Etapa 2](install-atp-step2.md)
> [Etapa 4 »](install-atp-step4.md)

## <a name="download-the-azure-atp-sensor-setup-package"></a>Baixar o pacote de instalação do sensor do Azure ATP
Após definir as configurações de conectividade do domínio, você poderá baixar o pacote de instalação do sensor do Azure ATP. O pacote de instalação do sensor do Azure ATP pode ser instalado em um servidor dedicado ou em um controlador de domínio. Ao instalar diretamente em um controlador de domínio, ele é instalado como um sensor do Azure ATP e ao instalar em um servidor dedicado usando o espelhamento de porta, ele é instalado como um sensor autônomo do Azure ATP. Para obter mais informações sobre o sensor do Azure ATP, consulte [Arquitetura do Azure ATP](atp-architecture.md). 

Clique em **Baixar** na lista de etapas na parte superior da página para ir para a página **Sensor**.

![Definições de configuração do sensor do Azure ATP](media/atp-sensor-config.png)

> [!NOTE] 
> Para acessar a tela de configuração do sensor mais tarde, clique no **ícone de configurações** (canto superior direito), selecione **Configuração** e, em **Sistema**, clique em **sensor**.  

1.  Clique em **sensor**.
2.  Salve o pacote localmente.
3.  Copie a **Chave** **de acesso**. A chave de acesso é necessária para o sensor do ATP do Azure se conectar à sua instância do ATP do Azure. A chave de acesso é uma senha de uso único para implantação de sensor. Depois disso, toda a comunicação é realizada usando certificados para autenticação e criptografia TLS. Use o botão **Regenerar** se você precisar regenerar a nova chave de acesso. Isso não afetará nenhum sensor implantado anteriormente, porque a chave só é usada para o registro inicial do sensor.
4.  Copie o pacote para o servidor dedicado ou controlador de domínio no qual você está instalando o sensor do Azure ATP. Como alternativa, você pode abrir o portal do ATP do Azure por meio do servidor dedicado ou do controlador de domínio e ignorar esta etapa.

O arquivo zip inclui os seguintes arquivos:

-   Instalador do sensor do Azure ATP

-   Arquivo de configurações com as informações necessárias para conectar-se ao serviço de nuvem do Azure ATP


> [!div class="step-by-step"]
> [« Etapa 2](install-atp-step2.md)
> [Etapa 4 »](install-atp-step4.md)


## <a name="see-also"></a>Consulte Também

- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/aatpsizingtool)

- [Configurar coleta de eventos](configure-event-collection.md)

- [Pré-requisitos do Azure ATP](atp-prerequisites.md)

- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)