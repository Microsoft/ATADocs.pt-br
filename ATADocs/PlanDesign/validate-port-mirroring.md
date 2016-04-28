---
# required metadata

title: Validação do espelhamento de porta | Microsoft Advanced Threat Analytics
description: Descreve como validar que o espelhamento de porta está configurado corretamente
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: ebd41719-c91a-4fdd-bcab-2affa2a2cace

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Validação do espelhamento de porta
As etapas a seguir guiarão você pelo processo de validação da configuração correta do espelhamento de porta. Para que o ATA funcione corretamente, o Gateway de ATA deve ser capaz de ver o tráfego para e do controlador de domínio. A fonte de dados principal usada pelo ATA é uma inspeção profunda de pacotes do tráfego de rede para e dos controladores de domínio. Para o ATA ver o tráfego de rede, o espelhamento de porta precisa ser configurado. O espelhamento de porta copia o tráfego de uma porta (de origem) para outra porta (de destino).

1.  Instale o [Microsoft Network Monitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865) ou outra ferramenta de detecção de rede.

    > [!IMPORTANT]
    > Não instale o Microsoft Message Analyzer ou qualquer outro software de captura de tráfego no Gateway de ATA.

2.  Abra o Monitor de Rede e crie uma nova guia de captura.

    1.  Selecione apenas o adaptador de rede de **captura** ou o adaptador de rede que estiver conectado à porta do comutador configurado como o destino do espelhamento de porta.

    2.  Verifique se o Modo-P está habilitado.

    3.  Clique em **Nova captura**.

        ![Criar nova imagem da guia de captura](media/ATA-Port-Mirroring-Capture.jpg)

3.  Na janela Filtro de exibição, digite o seguinte filtro: **KerberosV5 OU LDAP** e, em seguida, **Aplicar**.

    ![Aplicar imagem de filtro KerberosV5 ou LDAP](media/ATA-Port-Mirroring-filter-settings.jpg)

4.  Clique em **Iniciar** para iniciar a sessão de captura. Se você não vir o tráfego para e do controlador de domínio, examine a configuração do espelhamento de porta.

    > [!NOTE]
    > É importante ter certeza de que você vê o tráfego para e dos controladores de domínio.
    >
    > ![Iniciar a captura de imagem de sessão](media/ATA-Port-Mirroring-Capture-traffic.jpg)

5.  Se você vir somente o tráfego em uma direção, você deve trabalhar com as equipes de rede ou de virtualização para ajudar a solucionar os problemas de sua configuração de espelhamento de porta.

## Consulte também

- [Configurar o espelhamento de porta](configure-port-mirroring.md)
- [Para obter suporte, confira nosso fórum!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


