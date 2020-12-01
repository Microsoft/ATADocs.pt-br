---
title: Guia de início rápido – Baixar o pacote de instalação do sensor do Microsoft Defender para Identidade
description: A terceira etapa da instalação do Microsoft Defender para Identidade ajuda você a baixar o pacote de instalação do sensor do Defender para Identidade.
keywords: ''
author: shsagir
ms.author: shsagir
ms.date: 10/26/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b2d1978a822b8062422c41696043b1563d8bc893
ms.sourcegitcommit: 07a855b87931875bdeca14b152b13a36db79bfa8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "94848509"
---
# <a name="quickstart-download-the-product-long-sensor-setup-package"></a>Início Rápido: Baixar o pacote de instalação do sensor do [!INCLUDE [Product long](includes/product-long.md)]

Neste guia de início rápido, você baixará o pacote de instalação do sensor do [!INCLUDE [Product long](includes/product-long.md)] no portal.

## <a name="prerequisites"></a>Pré-requisitos

- Uma [instância do [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md) [conectada ao Active Directory](install-step2.md).

## <a name="download-the-setup-package"></a>Baixar o pacote de instalação

Depois de definir as configurações de conectividade do domínio, baixe o pacote de instalação do sensor do [!INCLUDE [Product short](includes/product-short.md)]. Para obter mais informações sobre o sensor do [!INCLUDE [Product short](includes/product-short.md)], confira [Arquitetura do [!INCLUDE [Product short](includes/product-short.md)]](architecture.md).

Clique em **Baixar** na lista de etapas na parte superior da página para acessar a página **Sensores**.

![Definições de configuração do sensor do [!INCLUDE [Product short](includes/product-short.md)]](media/sensor-config.png)

Para acessar a tela de configuração do sensor mais tarde, selecione **Configuração** e, em **Sistema**, clique em **Sensores**.  

1. Clique em **Baixar** para salvar o pacote localmente.
1. Copie a **chave de** **acesso**. A chave de acesso é necessária para que o sensor do [!INCLUDE [Product short](includes/product-short.md)] se conecte à sua instância do [!INCLUDE [Product short](includes/product-short.md)]. A chave de acesso é uma senha de uso único para implantação de sensor. Depois disso, toda a comunicação é realizada usando certificados para autenticação e criptografia TLS. Use o botão **Regenerar** se você precisar regenerar a nova chave de acesso. Isso não afetará nenhum sensor implantado anteriormente, porque a chave só é usada para o registro inicial do sensor.
1. Copie o pacote para o servidor dedicado ou o controlador de domínio no qual você está instalando o sensor do [!INCLUDE [Product short](includes/product-short.md)]. Como alternativa, você pode abrir o portal do [!INCLUDE [Product short](includes/product-short.md)] por meio do servidor dedicado ou do controlador de domínio e ignorar esta etapa.

O arquivo zip inclui os seguintes arquivos:

- Instalador do sensor do [!INCLUDE [Product short](includes/product-short.md)]

- Arquivo de definição de configuração com as informações necessárias para se conectar ao serviço de nuvem do [!INCLUDE [Product short](includes/product-short.md)]

## <a name="next-steps"></a>Próximas etapas

> [!div class="step-by-step"]
> [« Etapa 2 – Conectar-se ao Active Directory](install-step2.md)
> [Etapa 4 – Instalar o sensor do [!INCLUDE [Product short](includes/product-short.md)] »](install-step4.md)

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o [!INCLUDE [Product short](includes/product-short.md)] e a segurança relacionada com outras pessoas? Participe da Comunidade [[!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/MDIcommunity) hoje mesmo!
