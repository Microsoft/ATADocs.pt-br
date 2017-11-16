---
title: "Instalação do Advanced Threat Analytics – Etapa 7 | Microsoft Docs"
description: "Nesta etapa da instalação do ATA, você integra sua VPN."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e0aed853-ba52-46e1-9c55-b336271a68e7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 2eab8649f225071ad548a8134b385d46f02b3222
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*



# <a name="install-ata---step-7"></a>Instalação do ATA – Etapa 7

>[!div class="step-by-step"]
[« Etapa 5](install-ata-step5.md)
[Etapa 8 »](install-ata-step7.md)

## <a name="step-7-integrate-vpn"></a>Etapa 7. Integrar a VPN

O Microsoft Advanced Threat Analytics (ATA) versão 1.8 pode coletar informações contábeis de soluções de VPN. Quando configurada, a página de perfil do usuário inclui informações de conexões de VPN, tais como os endereços IP e os locais de origem das conexões. Isso complementa o processo de investigação, fornecendo informações adicionais sobre a atividade de usuário. A chamada para resolver um endereço IP externo de um local é anônima. Nenhuma identificação pessoal será enviada nesta chamada.

O ATA integra-se à solução de VPN escutando eventos contábeis do RADIUS encaminhados para os Gateways do ATA. Este mecanismo é baseado em Contabilização RADIUS padrão ([RFC 2866](https://tools.ietf.org/html/rfc2866)) e têm suporte dos seguintes fornecedores de VPN:

-   Microsoft
-   F5
-   Check Point
-   Cisco ASA

## <a name="prerequisites"></a>Pré-requisitos

Para habilitar a integração de VPN, verifique se você definiu os seguintes parâmetros:

-   Abra a porta UDP 1813 nos Gateways do ATA e Gateways Lightweight do ATA.

-   Conecte-se à Central do ATA para a Internet para que ela possa consultar o local de endereços IP de entrada.

O exemplo abaixo usa o Servidor de Roteamento e Acesso Remoto (RRAS) da Microsoft para descrever o processo de configuração de VPN.

Se você estiver usando uma solução de VPN de terceiros, confira a documentação deles para obter instruções sobre como habilitar a Contabilização RADIUS.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Configurar a Contabilização de RADIUS no sistema de VPN

Execute as seguintes etapas em seu servidor RRAS.
 
1.  Abra o console de Roteamento e Acesso Remoto.
2.  Clique com o botão direito do mouse no nome do servidor e clique em **Propriedades**.
3.  Na guia **Segurança**, em **Provedor de contabilização**, selecione **Contabilização RADIUS** e clique em **Configurar**.

    ![Configuração RADIUS](./media/radius-setup.png)

4.  Na janela **Adicionar Servidor RADIUS**, digite o **Nome do servidor** do Gateway do ATA ou Gateway Lightweight do ATA mais próximo. Em **Porta**, verifique se o padrão de 1813 está configurado. Clique em **Alteração** e digite uma nova cadeia de caracteres alfanuméricos secreta compartilhada da qual você possa se lembrar. Você precisa preenchê-la mais tarde em sua Configuração do ATA. Marque a caixa **Enviar mensagens de Contabilização RADIUS Ligada e Desligada** caixa e, em seguida, clique em **OK** em todas as caixas de diálogo abertas.
 
     ![Configuração de VPN](./media/vpn-set-accounting.png)
     
### <a name="configure-vpn-in-ata"></a>Configurar VPN no ATA

O ATA coleta dados da VPN que ajudam a caracterizar o local do qual os computadores se conectam à rede e a detectar conexões VPN anormais.

Para configurar dados de VPN no ATA:

1.  No console do ATA, abra a página Configuração do ATA e vá para **VPN**.
 
  ![Menu de configuração do ATA](./media/config-menu.png)

2.  Ativar **Contabilização Radius** e digite o **Segredo Compartilhado** configurado anteriormente em seu servidor VPN do RRAS. Em seguida, clique em **Salvar**.
 

  ![Configurar a VPN do ATA](./media/vpn.png)


Depois que ela estiver habilitada, todos os Gateways do ATA e Gateways Lightweight escutarão na porta 1813 para eventos de contabilização RADIUS. 

A instalação está concluída e você pode ver atividade de VPN na página de perfil do usuário:
 
   ![Configuração de VPN](./media/vpn-user.png)

Depois que o Gateway do ATA receber os eventos de VPN e os enviar ao Centro do ATA para processamento, o Centro do ATA precisará de conectividade com a Internet para que a porta 443 HTTPS possa resolver os endereços IP externos nos eventos de VPN para sua localização geográfica.





>[!div class="step-by-step"]
[«Etapa 6](install-ata-step5.md)
[Etapa 8»](install-ata-step7.md)



## <a name="related-videos"></a>Vídeos Relacionados
- [Visão geral da implantação do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Como escolher o tipo certo de Gateway do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Consulte também
- [Guia de implantação da POC (prova de conceito) do ATA](http://aka.ms/atapoc)
- [Ferramenta de dimensionamento do ATA](http://aka.ms/atasizingtool)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)

