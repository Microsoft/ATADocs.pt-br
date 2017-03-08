---
title: "Instalação do Advanced Threat Analytics – Etapa 4 | Microsoft Docs"
description: "A Etapa quatro da instalação do ATA ajuda você a instalar o Gateway do ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: a5a9b0672fa6a571e265ff5472cb7f7d1cfb034f
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*Aplica-se a: Advanced Threat Analytics versão 1.7*



# <a name="install-ata---step-4"></a>Instalação do ATA - Etapa 4

>[!div class="step-by-step"]
[« Etapa 3](install-ata-step3.md)
[Etapa 5 »](install-ata-step5.md)

## <a name="step-4-install-the-ata-gateway"></a>Etapa 4. Instalar o Gateway do ATA

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
    
    Por exemplo, no caso de um Gateway Lightweight do ATA, a tela a seguir será exibida informando que um Gateway Lightweight do ATA será instalado em seu controlador de domínio:
    
    ![Instalação do Gateway Lightweight do ATA](media/ATA-lightweight-gateway-install-selected.png) Clique em **Avançar**.

    > [!NOTE] 
    > Se o controlador de domínio ou servidor dedicado não atender aos requisitos mínimos de hardware para a instalação, você receberá um aviso. Isso não impede você de clicar em **Avançar** e prosseguir com a instalação. Essa pode ser a opção certa para a instalação do ATA em um ambiente de teste de laboratório pequeno no qual você não precisará de tanto espaço para armazenamento de dados. Para ambientes de produção, é altamente recomendável trabalhar com o guia de [planejamento de capacidade](/advanced-threat-analytics/plan-design/ata-capacity-planning) do ATA para certificar-se de que seus controladores de domínio ou servidores dedicados atendam aos requisitos necessários.

4.  Na página **Configuração do Gateway do ATA** insira as informações a seguir com base em seu ambiente:

    ![Imagem da configuração do gateway de ATA](media/ATA-Gateway-Configuration.png)

    |Campo|Descrição|Comentários|
    |---------|---------------|------------|
    |Caminho da Instalação|Esse é o local onde o Gateway do ATA será instalado. Por padrão, é %programfiles%\Microsoft Advanced Threat Analytics\Gateway|Mantenha o valor padrão|
    |Certificado SSL do Serviço do Gateway|Esse é o certificado que será usado pelo Gateway do ATA.|Use um certificado autoassinado apenas para ambientes de laboratório.|
    |Registro de Gateway|Digite o Nome de Usuário e a Senha do administrador do ATA.|Para o Gateway do ATA registrar-se no Centro do ATA, digite o nome de usuário e a senha do usuário que instalou o Centro do ATA. Esse usuário deve ser membro de um dos seguintes grupos locais no Centro do ATA.<br /><br />-   Administradores<br />-   Administradores do Microsoft Advanced Threat Analytics **Observação:** essas credenciais são usadas apenas para registro e não são armazenadas no ATA.|
    
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

## <a name="see-also"></a>Consulte também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)

