---
title: Monitorar controladores de domínio e sensores instalados em seus controladores de domínio, usando a Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Descreve como monitorar os sensores do ATP do Azure e a cobertura dos sensores usando o ATP do Azure
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 02/13/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 92decce8-b3ae-4d32-8407-a95314a66863
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6b3c8e978f16893d70c44c0fd3d04ce381c1bb5d
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196779"
---
# <a name="monitoring-your-domain-controller-coverage"></a>Monitorando a cobertura do controlador de domínio

Assim que o primeiro sensor do ATP do Azure é instalado e configurado em um controlador de domínio na rede, o ATP do Azure começa a monitorar os controladores de domínio do ambiente. 

Durante a instalação, é recomendado selecionar pelo menos um controlador de domínio de sensor do ATP do Azure como o candidato a sincronizador de domínio por domínio. Um dos trabalhos do sensor do sincronizador de domínio é garantir que os controladores de domínio sejam pesquisados ativamente por esse sensor específico. Os controladores de domínio podem adquirir e perder o status de candidato a sincronizador de domínio após a configuração inicial. Quando nenhum controlador de domínio é selecionado como candidato a sincronizador de domínio, apenas o monitoramento passivo da atividade de rede nos seus controladores de domínio está ocorrendo. Confira [Configuração do sensor do ATP do Azure](install-atp-step5.md) para obter mais informações de como configurar um sensor do Azure e defini-lo como um **candidato a sincronizador de domínio**. 

Assim que um sensor do ATP do Azure estiver instalado e configurado em um controlador de domínio na rede, o sensor passará a se comunicar com o serviço ATP do Azure constantemente enviando informações de status, integridade e a versão do sensor, além de eventos e alterações do Active Directory.  

### <a name="domain-controller-status"></a>Status do controlador de domínio

O ATP do Azure monitora seu ambiente continuamente em busca de controladores de domínio não monitorados introduzidos no ambiente e relata-os, ajudando a gerenciar a cobertura completa do ambiente. 

1. Para verificar o status dos controladores de domínio monitorados e não monitorados detectados e seus status, acesse a área **Configuração** do portal do ATP do Azure, na seção **Sistema** e selecione **Sensores**.
   
     ![Monitoramento de status do sensor do ATP do Azure](media/atp-sensors-status-monitoring.png)

2. Os controladores de domínio atuais monitorados e não monitorados são exibidos na parte superior da tela. Para baixar os detalhes de status de monitoramento dos controladores de domínio, selecione **Baixar detalhes**. 

O download do Excel da cobertura do controlador de domínio fornece as seguintes informações de todos os controladores de domínio detectados na sua organização:

|Título|Descrição|
|----|----|
|nome_do_host|Nome do computador|
|Nome de domínio|Nome de domínio|
|Monitorado|Status de monitoramento do ATP do Azure|
|Tipo de sensor|Sensor do ATP do Azure ou sensor autônomo do ATP do Azure|
|Unidade organizacional|Local dentro do Active Directory |
|Versão do sistema operacional| Versão do sistema operacional detectado|
|Endereço IP|Endereço IP detectado| 


> [!NOTE]
> As páginas de configuração do portal do ATP do Azure podem ser modificadas apenas por administradores do ATP do Azure.


## <a name="see-also"></a>Consulte Também

- [Arquitetura do ATP do Azure](atp-architecture.md)
- [Configurando os sensores do ATP do Azure](install-atp-step5.md)
- [Suporte para várias florestas](atp-multi-forest.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
