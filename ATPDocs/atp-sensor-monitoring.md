---
title: Monitorar controladores de domínio e sensores instalados em seus controladores de domínio, usando a Proteção Avançada contra Ameaças do Azure
description: Descreve como monitorar os sensores do ATP do Azure e a cobertura dos sensores usando o ATP do Azure
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 04/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 92decce8-b3ae-4d32-8407-a95314a66863
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 022f813ecb999309091a46639a257bac343ee286
ms.sourcegitcommit: 63be53de5b84eabdeb8c006438dab45bd35a4ab7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2020
ms.locfileid: "81462161"
---
# <a name="monitoring-your-domain-controller-coverage"></a>Monitorando a cobertura do controlador de domínio

Assim que o primeiro sensor do ATP do Azure é instalado e configurado em um controlador de domínio na rede, o ATP do Azure começa a monitorar os controladores de domínio do ambiente.

Assim que um sensor do ATP do Azure estiver instalado e configurado em um controlador de domínio na rede, o sensor passará a se comunicar com o serviço ATP do Azure constantemente enviando informações de status, integridade e a versão do sensor, além de eventos e alterações do Active Directory.

## <a name="domain-controller-status"></a>Status do controlador de domínio

O ATP do Azure monitora seu ambiente continuamente em busca de controladores de domínio não monitorados introduzidos no ambiente e relata-os, ajudando a gerenciar a cobertura completa do ambiente.

1. Para verificar o status dos controladores de domínio monitorados e não monitorados detectados e seus status, acesse a área **Configuração** do portal do ATP do Azure, na seção **Sistema** e selecione **Sensores**.

    ![Monitoramento de status do sensor do ATP do Azure](media/atp-sensors-status-monitoring.png)

2. Os controladores de domínio atuais monitorados e não monitorados são exibidos na parte superior da tela. Para baixar os detalhes de status de monitoramento dos controladores de domínio, selecione **Baixar detalhes**.

O download do Excel da cobertura do controlador de domínio fornece as seguintes informações de todos os controladores de domínio detectados na sua organização:

|Título|Descrição|
|----|----|
|Nome do host|Nome do computador|
|Nome de domínio|Nome de domínio|
|Monitorado|Status de monitoramento do ATP do Azure|
|Tipo de sensor|Sensor do ATP do Azure ou sensor autônomo do ATP do Azure|
|Unidade organizacional|Local dentro do Active Directory |
|Versão do sistema operacional| Versão do sistema operacional detectado|
|Endereço IP|Endereço IP detectado|

## <a name="search-domain-controllers"></a>Pesquisar controladores de domínio

Gerenciar sua frota de sensores e controladores de domínio pode ser desafiador. Para facilitar a localização e a identificação, os controladores de domínio podem ser pesquisados usando o recurso de pesquisa na lista de sensores da ATP do Azure.

1. Para pesquisar os controladores de domínio, vá para a área de **Configuração** do portal da ATP do Azure, na seção **Sistema**, selecione **Sensores**.
1. Selecione a opção de filtros na coluna **Controlador de domínio** na lista tabela do controlador de domínio.
1. Insira o nome que você deseja pesquisar. Atualmente, não há suporte para caracteres curinga no campo de pesquisa.

    ![Controlador de domínio de pesquisa da ATP do Azure](media/search-sensor.png)

> [!NOTE]
> As páginas de configuração do portal do ATP do Azure podem ser modificadas apenas por administradores do ATP do Azure.

## <a name="see-also"></a>Confira Também

- [Arquitetura do ATP do Azure](atp-architecture.md)
- [Configurando os sensores do ATP do Azure](install-atp-step5.md)
- [Suporte para várias florestas](atp-multi-forest.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
