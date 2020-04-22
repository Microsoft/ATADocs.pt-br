---
title: Baixar início rápido do pacote de instalação do sensor do ATP do Azure
description: A etapa três da instalação do Azure ATP ajuda a baixar o pacote de instalação do sensor do Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
ms.date: 02/19/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 95bb4ec1-841f-41b7-92fe-fbd144085724
ms.openlocfilehash: 5c8065ee0c4358b25597879881f1cc1f063d5c2f
ms.sourcegitcommit: 63be53de5b84eabdeb8c006438dab45bd35a4ab7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2020
ms.locfileid: "79413716"
---
# <a name="quickstart-download-the-azure-atp-sensor-setup-package"></a>Início Rápido: Baixar o pacote de instalação do sensor do Azure ATP

Neste início rápido, você baixará o pacote de instalação do sensor do ATP do Azure no portal.

## <a name="prerequisites"></a>Pré-requisitos

- Uma [instância do ATP do Azure](install-atp-step1.md)[conectada ao Active Directory](install-atp-step2.md).

## <a name="download-the-setup-package"></a>Baixar o pacote de instalação

Após definir as configurações de conectividade do domínio, você poderá baixar o pacote de instalação do sensor do Azure ATP. Para obter mais informações sobre o sensor do Azure ATP, consulte [Arquitetura do Azure ATP](atp-architecture.md).

Clique em **Baixar** na lista de etapas na parte superior da página para ir para a página **Sensor**.

![Definições de configuração do sensor do Azure ATP](media/atp-sensor-config.png)

 Para acessar a tela de configuração do sensor mais tarde, clique no **ícone de configurações** (canto superior direito), selecione **Configuração** e, em **Sistema**, clique em **sensor**.  

1. Clique em **sensor**.
2. Salve o pacote localmente.
3. Copie a **chave** de **acesso**. A chave de acesso é necessária para o sensor do ATP do Azure se conectar à sua instância do ATP do Azure. A chave de acesso é uma senha de uso único para implantação de sensor. Depois disso, toda a comunicação é realizada usando certificados para autenticação e criptografia TLS. Use o botão **Regenerar** se você precisar regenerar a nova chave de acesso. Isso não afetará nenhum sensor implantado anteriormente, porque a chave só é usada para o registro inicial do sensor.
4. Copie o pacote para o servidor dedicado ou controlador de domínio no qual você está instalando o sensor do ATP do Azure. Como alternativa, você pode abrir o portal do ATP do Azure por meio do servidor dedicado ou do controlador de domínio e ignorar esta etapa.

O arquivo zip inclui os seguintes arquivos:

- Instalador do sensor do Azure ATP

- Arquivo de configurações com as informações necessárias para conectar-se ao serviço de nuvem do Azure ATP

## <a name="next-steps"></a>Próximas etapas

> [!div class="step-by-step"]
> [« Etapa 2 — Conectar ao Active Directory](install-atp-step2.md)
> [Etapa 4 — Instalar o sensor do ATP do Azure »](install-atp-step4.md)

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o ATP do Azure e a segurança relacionada com outras pessoas? Participe da [Comunidade do ATP do Azure](https://aka.ms/azureatpcommunity) hoje mesmo!
