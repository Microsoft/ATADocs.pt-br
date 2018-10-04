---
title: Instalar a Proteção Avançada contra Ameaças do Azure – etapa 4 | Microsoft Docs
description: A etapa quatro da instalação do Azure ATP ajuda a instalar o sensor autônomo do Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/25/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 51911e39-76c7-4dcd-bc0b-ec6235d0403f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 87a2b47261293fffffe9d822d698b551a332a481
ms.sourcegitcommit: b283bf66e63d76e6dba4564a229e804792794c6d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/29/2018
ms.locfileid: "47454132"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*



# <a name="install-azure-atp---step-4"></a>Instalar o Azure ATP – etapa 4

> [!div class="step-by-step"]
> [« Etapa 3](install-atp-step3.md)
> [Etapa 5 »](install-atp-step5.md)

## <a name="step-4-install-the-azure-atp-sensor"></a>Etapa 4. Instalar o sensor do Azure ATP

Antes de instalar o sensor autônomo do Azure ATP em um servidor dedicado, verifique se o espelhamento de porta está configurado corretamente e se o sensor autônomo do Azure ATP pode ver o tráfego chegando e saindo dos controladores de domínio. 


> [!IMPORTANT]
>Verifique se o .NET Framework 4.7 está instalado no computador. Se o .Net Framework 4.7 não estiver instalado, o pacote de instalação do sensor do Azure ATP o instalará, o que requer uma reinicialização do servidor.

Execute as seguintes etapas no servidor do sensor do Azure ATP ou no controlador de domínio.

1. Verifique se a máquina tem conectividade com o ponto de extremidade de serviço de nuvem do Azure ATP relevante:
  - https://triprd1wceuw1sensorapi.atp.azure.com (na Europa)  
  - https://triprd1wcuse1sensorapi.atp.azure.com (nos EUA)
  - https://triprd1wcasse1sensorapi.atp.azure.com (na Ásia)

2. Extraia os arquivos de instalação do arquivo zip. 
> [!NOTE] 
> A instalação diretamente do arquivo zip falha.

3.  Execute **Azure ATP sensor setup.exe** e siga o assistente de instalação.

4.  Na página **Boas-vindas**, selecione seu idioma e clique em **Avançar**.

     ![Idioma de instalação do sensor autônomo do Azure ATP](media/sensor-install-language.png)


5.  O assistente de instalação verifica automaticamente se o servidor é um controlador de domínio ou um servidor dedicado. Se for um controlador de domínio, o sensor do Azure ATP será instalado, se for um servidor dedicado, o sensor autônomo do Azure ATP será instalado. 
    
    Por exemplo, para um sensor autônomo do Azure ATP, a tela a seguir será exibida informando que um sensor autônomo do Azure ATP está instalado em seu servidor dedicado:
    
    ![Instalação do sensor autônomo do Azure ATP](media/sensor-install-deployment-type.png)

    Clique em **Avançar**.

    > [!NOTE] 
    > Se o controlador de domínio ou servidor dedicado não atender aos requisitos mínimos de hardware para a instalação, você receberá um aviso. Isso não impede você de clicar em **Avançar** e prosseguir com a instalação. Essa pode ser a opção certa para a instalação do Azure ATP em um ambiente de teste de laboratório pequeno, no qual você não precisará de tanto espaço para armazenamento de dados. Para ambientes de produção, é altamente recomendável trabalhar com o guia de [planejamento de capacidade](atp-capacity-planning.md) do Azure ATP para certificar-se de que seus controladores de domínio ou servidores dedicados atendam aos requisitos necessários.

6.  Em **Configurar o sensor**, insira o caminho de instalação e a chave de acesso que você copiou na etapa anterior, com base em seu ambiente:

    ![Imagem de configuração de sensor autônomo do Azure ATP](media/sensor-install-config.png)

      - Caminho de instalação: é o local em que o sensor autônomo do Azure ATP é instalado. Por padrão, é %programfiles%\Azure Advanced Threat Protection sensor. Mantenha o valor padrão.

      - Chave de acesso: é recuperada por meio do portal do espaço de trabalho na etapa anterior.
    
7. Clique em **Instalar**. Os componentes a seguir serão instalados e configurados durante a instalação do sensor autônomo do Azure ATP:

    -   KB 3047154 (somente para Windows Server 2012 R2)

        > [!IMPORTANT]
        > -   Não instale o KB 3047154 em um host de virtualização (o host que está executando a virtualização; não há problema em executá-lo em uma máquina virtual). Isso pode fazer com que o espelhamento de porta pare de funcionar corretamente. 
        > -   Se o Wireshark estiver instalado no computador do sensor do ATP, depois de executar o Wireshark, você precisará reiniciar o sensor do ATP, pois ela usa os mesmos drivers.

    -   Serviço de sensor do Azure ATP e serviço do atualizador do sensor do Azure ATP
    -   Microsoft Visual C++ 2013 Redistributable

8.  Após a conclusão da instalação, clique em **Iniciar** para abrir o navegador e faça logon portal de espaço de trabalho do Azure ATP.


> [!div class="step-by-step"]
> [« Etapa 3](install-atp-step3.md)
> [Etapa 5 »](install-atp-step5.md)


## <a name="see-also"></a>Consulte Também

- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/aatpsizingtool)

- [Configurar coleta de eventos](configure-event-collection.md)

- [Pré-requisitos do Azure ATP](atp-prerequisites.md)

- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)
