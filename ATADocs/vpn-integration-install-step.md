---
title: "Instalação do Advanced Threat Analytics – Etapa 7 | Microsoft Docs"
description: "Nesta etapa da instalação do ATA, você integra sua VPN."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 09/19/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e0aed853-ba52-46e1-9c55-b336271a68e7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 384384ebd6b6fadcaa5636200ccd08667d9c41a5
ms.sourcegitcommit: 34c3d6f56f175994b672842c7576040956ceea69
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/19/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*



# <a name="install-ata---step-7"></a>Instalação do ATA – Etapa 7

>[!div class="step-by-step"]
[« Etapa 5](install-ata-step5.md)
[Etapa 8 »](install-ata-step7.md)

## <a name="step-7-integrate-vpn"></a>Etapa 7. Integrar a VPN

### <a name="configuring-vpn"></a>Configurando a VPN

O ATA coleta dados da VPN que ajudam a caracterizar o local do qual os computadores se conectam à rede e a detectar conexões VPN anormais.

Para configurar dados de VPN no ATA:

1. Vá para **Configuração** e clique na guia **VPN**.

2. Insira o **Segredo compartilhado da conta** do seu servidor RADIUS. Para obter o segredo compartilhado, confira a documentação da VPN.

 ![Configurar a VPN do ATA](media/vpn.png)

3.  Depois que ela estiver habilitada, todos os Gateways do ATA e Gateways Lightweight escutarão na porta 1813 para eventos de contabilização RADIUS. 

4.  Eventos de contabilização RADIUS da VPN devem ser encaminhados para qualquer Gateway do ATA ou Gateway Lightweight do ATA após a configuração.

5.  Depois que o Gateway do ATA receber os eventos de VPN e os enviar ao Centro do ATA para processamento, o Centro do ATA precisará de conectividade com a Internet para que a porta 443 HTTPS possa resolver os endereços IP externos nos eventos de VPN para sua localização geográfica.

A chamada para resolver um endereço IP externo de um local é anônima. Nenhuma identificação pessoal será enviada nesta chamada.

Os fornecedores de VPN com suporte são:
- Microsoft
- F5
- Check Point
- Cisco ASA




>[!div class="step-by-step"]
[«Etapa 6](install-ata-step5.md)
[Etapa 8»](install-ata-step7.md)



## <a name="related-videos"></a>Vídeos Relacionados
- [Como escolher o tipo certo de Gateway do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Consulte também
- [Guia de implantação da POC (prova de conceito) do ATA](http://aka.ms/atapoc)
- [Ferramenta de dimensionamento do ATA](http://aka.ms/atasizingtool)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)

