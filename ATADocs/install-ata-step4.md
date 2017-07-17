---
title: "Instalação do Advanced Threat Analytics – Etapa 4 | Microsoft Docs"
description: "A Etapa quatro da instalação do ATA ajuda você a instalar o Gateway do ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/18/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 2713f6939c8756d0ecb438e866e6649f13d3c490
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*



<a id="install-ata---step-4" class="xliff"></a>

# Instalação do ATA - Etapa 4

>[!div class="step-by-step"]
[« Etapa 3](install-ata-step3.md)
[Etapa 5 »](install-ata-step5.md)

<a id="step-4-install-the-ata-gateway" class="xliff"></a>

## Etapa 4. Instalar o Gateway do ATA

Antes de instalar o Gateway do ATA, verifique se o espelhamento de porta está configurado corretamente e se o Gateway do ATA pode ver o tráfego chegando e saindo dos controladores de domínio. Confira [Validar o espelhamento de porta](validate-port-mirroring.md) para saber mais.


> [!IMPORTANT]
> Verifique se o [KB2919355](http://support.microsoft.com/kb/2919355/) foi instalado.  Execute o seguinte cmdlet do PowerShell para verificar se o hotfix foi instalado:
>
> `Get-HotFix -Id kb2919355`

Execute as seguintes etapas no servidor do Gateway do ATA.

1.  Extraia os arquivos do arquivo zip. 
> [!NOTE] 
> A instalação diretamente do arquivo zip falhará.

2.  Execute **Microsoft ATA Gateway Setup.exe** e siga o assistente de instalação.

3.  Na página **Boas-vindas**, selecione seu idioma e clique em **Avançar**.

4.  O assistente de instalação verificará automaticamente se o servidor é um controlador de domínio ou um servidor dedicado. Se for um controlador de domínio, o Gateway Lightweight do ATA será instalado, se for um servidor dedicado, o Gateway do ATA será instalado. 
    
    Por exemplo, no caso de um Gateway do ATA, a tela a seguir será exibida informando que um Gateway do ATA será instalado em seu servidor dedicado:
    
    ![Instalação do Gateway do ATA](media/ata-gw-install.png) Clique em **Avançar**.

    > [!NOTE] 
    > Se o controlador de domínio ou servidor dedicado não atender aos requisitos mínimos de hardware para a instalação, você receberá um aviso. Isso não impede você de clicar em **Avançar** e prosseguir com a instalação. Essa pode ser a opção certa para a instalação do ATA em um ambiente de teste de laboratório pequeno no qual você não precisará de tanto espaço para armazenamento de dados. Para ambientes de produção, é altamente recomendável trabalhar com o guia de [planejamento de capacidade](ata-capacity-planning.md) do ATA para certificar-se de que seus controladores de domínio ou servidores dedicados atendam aos requisitos necessários.

4.  Em **Configurar o Gateway**, insira as seguintes informações com base em seu ambiente:

    ![Imagem da configuração do gateway de ATA](media/ata-gw-configure.png)

    > [!NOTE]
    > Quando você implanta o Gateway do ATA, não precisa fornecer credenciais. Se a instalação do Gateway do ATA não conseguir recuperar suas credenciais usando o logon único (por exemplo, isso pode acontecer se o Centro do ATA não está no domínio, se o Gateway do ATA não está no domínio, você não precisa das credenciais de administrador do ATA), será solicitado que você forneça credenciais, como na tela a seguir. 

  ![Fornecer credenciais do Gateway do ATA](media/ata-install-credentials.png)

   - Caminho de Instalação: esse é o local em que o Gateway do ATA será instalado. Por padrão, é %programfiles%\Microsoft Advanced Threat Analytics\Gateway. Mantenha o valor padrão.
    
5. Clique em **Instalar**. Os componentes a seguir serão instalados e configurados durante a instalação do Gateway do ATA:

    -   KB 3047154 (somente para Windows Server 2012 R2)

        > [!IMPORTANT]
        > -   Não instale o KB 3047154 em um host de virtualização (o host que está executando a virtualização; não há problema em executá-lo em uma máquina virtual). Isso pode fazer com que o espelhamento de porta pare de funcionar corretamente. 
        > -   Não instale o Message Analyzer, o Wireshark ou qualquer outro software de captura de rede no Gateway do ATA. Se você precisa capturar o tráfego de rede, instale e use o Microsoft Network Monitor 3.4.

    -   Serviço do Gateway do ATA
    -   Microsoft Visual C++ 2013 Redistributable
    -   Conjunto de coleta de dados do Monitor de Desempenho Personalizado

5.  Após a conclusão da instalação, para o Gateway do ATA, clique em **Iniciar** para abrir o navegador e entrar no Console do ATA. Para o Gateway Lightweight do ATA, clique em **Concluir**.


>[!div class="step-by-step"]
[« Etapa 3](install-ata-step3.md)
[Etapa 5 »](install-ata-step5.md)

<a id="see-also" class="xliff"></a>

## Consulte também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)
