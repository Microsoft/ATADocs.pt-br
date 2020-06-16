---
title: Instalar o Advanced Threat Analytics – etapa 4
description: A Etapa quatro da instalação do ATA ajuda você a instalar o Gateway do ATA.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1b66474219101f9d5c7f9ce38b3a7e3ff34b6f50
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2020
ms.locfileid: "84775192"
---
# <a name="install-ata---step-4"></a>Instalação do ATA - Etapa 4

*Aplica-se a: Advanced Threat Analytics versão 1.9*

> [!div class="step-by-step"]
> [« Etapa 3](install-ata-step3.md)
> [Etapa 5 »](install-ata-step5.md)

## <a name="step-4-install-the-ata-gateway"></a>Etapa 4. Instalar o Gateway do ATA

Antes de instalar o Gateway do ATA, verifique se o espelhamento de porta está configurado corretamente e se o Gateway do ATA pode ver o tráfego chegando e saindo dos controladores de domínio. Para saber mais, confira [Validar o espelhamento de porta](validate-port-mirroring.md).


> [!IMPORTANT]
> Verifique se o [KB2919355](https://support.microsoft.com/kb/2919355/) foi instalado.  Execute o seguinte cmdlet do PowerShell para verificar se o hotfix foi instalado:
>
> `Get-HotFix -Id kb2919355`

Execute as seguintes etapas no servidor do Gateway do ATA.

1. Extraia os arquivos do arquivo zip. 
   > [!NOTE] 
   > A instalação diretamente do arquivo zip falha.
    
2. Execute **Microsoft ATA Gateway Setup.exe** e siga o assistente de instalação.
    
3. Na página **Boas-vindas**, selecione seu idioma e clique em **Avançar**.
    
4. O assistente de instalação verifica automaticamente se o servidor é um controlador de domínio ou um servidor dedicado. Se for um controlador de domínio, o Gateway Lightweight do ATA será instalado, se for um servidor dedicado, o Gateway do ATA será instalado. 
    
   Por exemplo, para um Gateway do ATA, a tela a seguir será exibida informando que um Gateway do ATA será instalado em seu servidor dedicado:
    
   ![Instalação do Gateway do ATA](media/ata-gw-install.png) Clique em **Avançar**.
    
   > [!NOTE] 
   > Se o controlador de domínio ou servidor dedicado não atender aos requisitos mínimos de hardware para a instalação, você receberá um aviso. Isso não impede você de clicar em **Avançar** e prosseguir com a instalação. Essa pode ser a opção certa para a instalação do ATA em um ambiente de teste de laboratório pequeno no qual você não precisará de tanto espaço para armazenamento de dados. Para ambientes de produção, é altamente recomendável trabalhar com o guia de [planejamento de capacidade](ata-capacity-planning.md) do ATA para certificar-se de que seus controladores de domínio ou servidores dedicados atendam aos requisitos necessários.
    
5. Em **Configurar o Gateway**, insira as seguintes informações com base em seu ambiente:
    
   ![Imagem da configuração do gateway de ATA](media/ata-gw-configure.png)
    
   > [!NOTE]
   > Quando você implanta o Gateway do ATA, não precisa fornecer credenciais. Se a instalação do Gateway do ATA não conseguir recuperar suas credenciais usando o logon único (por exemplo, isso pode acontecer se o Centro do ATA não estiver no domínio, nesse caso, você não precisa das credenciais de administrador do ATA), você receberá uma solicitação para fornecer credenciais, como na tela a seguir: 
   
    ![Fornecer credenciais do gateway do ATA](media/ata-install-credentials.png)
   
    - Caminho de Instalação: esse é o local em que o Gateway do ATA é instalado. Por padrão, é %programfiles%\Microsoft Advanced Threat Analytics\Gateway. Mantenha o valor padrão.
   
6. Clique em **Instalar**. Os componentes a seguir serão instalados e configurados durante a instalação do Gateway do ATA:
    
    -   KB 3047154 (somente para Windows Server 2012 R2)
    
        > [!IMPORTANT]
        > -   Não instale o KB 3047154 em um host de virtualização (o host que está executando a virtualização; não há problema em executá-lo em uma máquina virtual). Isso pode fazer com que o espelhamento de porta pare de funcionar corretamente. 
        > -   Não instale o Message Analyzer, o Wireshark ou qualquer outro software de captura de rede no Gateway do ATA. Se você precisa capturar o tráfego de rede, instale e use o Microsoft Network Monitor 3.4.
    
    -   Serviço do Gateway do ATA
    -   Microsoft Visual C++ 2013 Redistributable
    -   Conjunto de coleta de dados do Monitor de Desempenho Personalizado
    
7. Após a conclusão da instalação, para o gateway do ATA, clique em **Iniciar** para abrir o navegador e faça logon no console do ATA, para o gateway Lightweight do ATA, clique em **concluir**.


> [!div class="step-by-step"]
> [« Etapa 3](install-ata-step3.md)
> [Etapa 5 »](install-ata-step5.md)


## <a name="related-videos"></a>Vídeos Relacionados
- [Visão geral da implantação do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Como escolher o tipo certo de Gateway do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>Consulte Também
- [Guia de implantação da POC (prova de conceito) do ATA](https://aka.ms/atapoc)
- [Ferramenta de dimensionamento do ATA](https://aka.ms/atasizingtool)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)

