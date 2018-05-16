---
title: "Instalar a Proteção Avançada contra Ameaças do Azure – etapa 6 | Microsoft Docs"
description: "Nesta etapa da instalação do ATP, você integra sua VPN."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/14/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 0d9d2a1d-6c76-4909-b6f9-58523df16d4f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d29210983f3f9f879b462ef760d0b3fe6e53cd5d
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2018
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*



# <a name="install-azure-atp---step-6"></a>Instalar o Azure ATP – etapa 6

>[!div class="step-by-step"]
[«Etapa 5](install-atp-step5.md)
[Etapa 7»](install-atp-step7.md)

## <a name="step-6-integrate-vpn"></a>Etapa 6. Integrar a VPN

O Azure ATP (Proteção Avançada contra Ameaças) pode coletar informações de contabilidade de soluções de VPN. Quando configurada, a página de perfil do usuário inclui informações de conexões de VPN, tais como os endereços IP e os locais de origem das conexões. Isso complementa o processo de investigação, fornecendo informações adicionais sobre a atividade de usuário, bem como uma nova detecção para conexões de VPN anormais. A chamada para resolver um endereço IP externo de um local é anônima. Nenhuma identificação pessoal será enviada nesta chamada.

O Azure ATP integra-se à sua solução de VPN escutando eventos de contabilidade do RADIUS encaminhados para os sensores do Azure ATP. Este mecanismo é baseado em Contabilização RADIUS padrão ([RFC 2866](https://tools.ietf.org/html/rfc2866)) e têm suporte dos seguintes fornecedores de VPN:

-   Microsoft
-   F5
-   Check Point
-   Cisco ASA

## <a name="prerequisites"></a>Pré-requisitos

Para habilitar a integração de VPN, verifique se você definiu os seguintes parâmetros:

-   Abra a porta UDP 1813 em seus sensores autônomos do Azure ATP e no sensor do Azure ATP.


O exemplo abaixo usa o Servidor de Roteamento e Acesso Remoto (RRAS) da Microsoft para descrever o processo de configuração de VPN.

Se estiver usando uma solução de VPN de terceiros, confira a documentação para obter instruções de como habilitar a Contabilidade do RADIUS.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Configurar a Contabilização de RADIUS no sistema de VPN

Execute as seguintes etapas em seu servidor RRAS.
 
1.  Abra o console de Roteamento e Acesso Remoto.
2.  Clique com o botão direito do mouse no nome do servidor e clique em **Propriedades**.
3.  Na guia **Segurança**, em **Provedor de contabilização**, selecione **Contabilização RADIUS** e clique em **Configurar**.

    ![Configuração RADIUS](./media/radius-setup.png)

4.  Na janela **Adicionar servidor RADIUS**, digite o **Nome do servidor** do sensor autônomo do Azure ATP ou sensor do Azure ATP mais próximo. Em **Porta**, verifique se o padrão de 1813 está configurado. Clique em **Alteração** e digite uma nova cadeia de caracteres alfanuméricos secreta compartilhada da qual você possa se lembrar. Você precisa preenchê-la mais tarde em sua Configuração do Azure ATP. Marque a caixa **Enviar mensagens de Contabilização RADIUS Ligada e Desligada** caixa e, em seguida, clique em **OK** em todas as caixas de diálogo abertas.
 
     ![Configuração de VPN](./media/vpn-set-accounting.png)
     
### <a name="configure-vpn-in-atp"></a>Configurar VPN no ATP

O Azure ATP coleta dados da VPN que ajudam a caracterizar os locais dos quais os computadores se conectam à rede e a detectar conexões VPN anormais.

Para configurar dados de VPN no ATP:

1.  No portal de espaço de trabalho do Azure ATP, clique na engrenagem de configuração e, em seguida, em **VPN**.
 

2.  Ativar **Contabilização Radius** e digite o **Segredo Compartilhado** configurado anteriormente em seu servidor VPN do RRAS. Em seguida, clique em **Salvar**.
 

  ![Configurar VPN do Azure ATP](./media/atp-vpn-radius.png)


Depois que isso for habilitado, todos os sensores e os sensores autônomos do Azure ATP escutam na porta 1813 para eventos de contabilidade do RADIUS. 

Sua instalação foi concluída. 

Depois que o sensor do Azure ATP receber os eventos de VPN e os enviar para o serviço de nuvem do Azure ATP para processamento, o perfil de entidade indicará locais distintos de VPN acessados e as atividades no perfil indicarão os locais.





>[!div class="step-by-step"]
[«Etapa 6](install-atp-step5.md)
[Etapa 7»](install-atp-step7.md)


## <a name="see-also"></a>Consulte Também
- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/aatpsizingtool)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)