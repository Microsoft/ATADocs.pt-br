---
title: Início rápido para instalar o sensor do ATP do Azure
description: A etapa quatro da instalação do Azure ATP ajuda a instalar o sensor do Azure ATP.
author: shsagir
ms.author: shsagir
ms.date: 10/31/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6a38a61e5028003ba10ad6929e24e63e81418f7b
ms.sourcegitcommit: 63be53de5b84eabdeb8c006438dab45bd35a4ab7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2020
ms.locfileid: "79413699"
---
# <a name="quickstart-install-the-azure-atp-sensor"></a>Início Rápido: Instalar o sensor do Azure ATP

Neste início rápido, você instalará o sensor do ATP do Azure em um controlador de domínio. Se você preferir uma instalação silenciosa, consulte o artigo [Instalação silenciosa](atp-silent-installation.md).

## <a name="prerequisites"></a>Pré-requisitos

- Uma [instância do ATP do Azure](install-atp-step1.md)[conectada ao Active Directory](install-atp-step2.md).
- Uma cópia baixada de seu [pacote de instalação do sensor do ATP](install-atp-step3.md) e a chave de acesso.
- Verifique se o Microsoft .NET Framework 4.7 está instalado no computador. Se o .NET Framework 4.7 não estiver instalado, o pacote de instalação do sensor do ATP do Azure o instalará, o que poderá exigir uma reinicialização do servidor.

## <a name="install-the-sensor"></a>Instalar o servidor

Execute as etapas a seguir no controlador de domínio.

1. Verifique se a máquina tem conectividade com os pontos de extremidade de serviço de nuvem do ATP do Azure relevantes:
   - Ocidental
      - [https://triprd1wceuw1sensorapi.atp.azure.com](https://triprd1wceuw1sensorapi.atp.azure.com) 
      - [https://triprd1wceun1sensorapi.atp.azure.com](https://triprd1wceun1sensorapi.atp.azure.com)
   - EUA 
      - [https://triprd1wcuse1sensorapi.atp.azure.com](https://triprd1wcuse1sensorapi.atp.azure.com)
      - [https://triprd1wcusw1sensorapi.atp.azure.com](https://triprd1wcusw1sensorapi.atp.azure.com)
      - [https://triprd1wcuswb1sensorapi.atp.azure.com](https://triprd1wcuswb1sensorapi.atp.azure.com)
   - GCC High dos EUA
      - [https://triff1wcva1sensorapi.atp.azure.us](https://triff1wcva1sensorapi.atp.azure.us)
   - Ásia
      - [https://triprd1wcasse1sensorapi.atp.azure.com](https://triprd1wcasse1sensorapi.atp.azure.com)

2. Extraia os arquivos de instalação do arquivo zip. A instalação diretamente do arquivo zip falhará.

3. Execute **Azure ATP sensor setup.exe** e siga o assistente de instalação.

4. Na página **Boas-vindas**, selecione seu idioma e clique em **Avançar**.

    ![Idioma de instalação do sensor autônomo do Azure ATP](media/sensor-install-language.png)


5. O assistente de instalação verifica automaticamente se o servidor é um controlador de domínio ou um servidor dedicado. Se for um controlador de domínio, o sensor do ATP do Azure será instalado. Se for um servidor dedicado, o sensor autônomo do ATP do Azure será instalado.
    
    Por exemplo, para um sensor do ATP do Azure, a tela a seguir será exibida informando que um sensor do ATP do Azure está instalado em seu servidor dedicado:
    
    ![Instalação do sensor do ATP do Azure](media/sensor-install-deployment-type.png)

   Clique em **Avançar**.

    > [!NOTE] 
    > Um aviso será emitido se o controlador de domínio ou o servidor dedicado não atender aos requisitos mínimos de hardware para a instalação. O aviso não impede que você clique em **Avançar** e prossiga com a instalação. Essa ainda pode ser a opção certa para a instalação do ATP do Azure em um ambiente de teste de laboratório pequeno, que não precisa de tanto espaço para armazenamento de dados. Para ambientes de produção, é altamente recomendável trabalhar com o guia de [planejamento de capacidade](atp-capacity-planning.md) do Azure ATP para certificar-se de que seus controladores de domínio ou servidores dedicados atendam aos requisitos necessários.

6. Em **Configurar o sensor**, insira o caminho de instalação e a chave de acesso que você copiou na etapa anterior, com base em seu ambiente:

    ![Imagem de configuração do sensor do ATP do Azure](media/sensor-install-config.png)

      - Caminho da instalação: O local em que o sensor do ATP do Azure está instalado. Por padrão, o caminho é %programfiles%\Azure Advanced Threat Protection sensor. Mantenha o valor padrão.

     - Chave de acesso: Recuperada por meio do portal do ATP do Azure na etapa anterior.
    
7. Clique em **Instalar**. Os componentes a seguir serão instalados e configurados durante a instalação do sensor autônomo do Azure ATP:

    - KB 3047154 (somente para Windows Server 2012 R2)

        > [!IMPORTANT]
        > - Não instale o KB 3047154 em um host de virtualização (o host que está executando a virtualização; não há problema em executá-lo em uma máquina virtual). Isso pode fazer com que o espelhamento de porta pare de funcionar corretamente. 
        > - Se o Wireshark estiver instalado no computador do sensor do ATP, depois de executar o Wireshark, você precisará reiniciar o sensor do ATP, pois ela usa os mesmos drivers.

    - Serviço de sensor do Azure ATP e serviço do atualizador do sensor do Azure ATP
    - Microsoft Visual C++ 2013 Redistributable


## <a name="next-steps"></a>Próximas etapas

O sensor do ATP do Azure foi projetado para ter um impacto mínimo sobre os recursos do controlador de domínio e a atividade de rede. Para criar uma avaliação de desempenho, consulte a [capacidade do plano para sua solução do ATP do Azure](install-atp-step5.md).


## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o ATP do Azure e a segurança relacionada com outras pessoas? Participe da [Comunidade do ATP do Azure](https://aka.ms/azureatpcommunity) hoje mesmo!
