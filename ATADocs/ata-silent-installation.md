---
title: "Instalação do Advanced Threat Analytics Silenciosamente | Microsoft Docs"
description: Este artigo descreve como instalar o ATA silenciosamente.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/29/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c38db312ea877b63580d745153aa58ea34a160a6
ms.sourcegitcommit: 9ce330726e5de8c05eae6a20d3e6c1d8bef3cd0e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*


# <a name="ata-silent-installation"></a>Instalação silenciosa do ATA
Este artigo fornece instruções de como instalar silenciosamente o ATA.

## <a name="prerequisites"></a>Pré-requisitos

O ATA versão 1.8 requer a instalação do Microsoft .NET Framework 4.6.1. 

Quando você instala ou atualiza o ATA, o .Net Framework 4.6.1 é instalado automaticamente como parte da implantação do Microsoft ATA.

> [!Note] 
> A instalação do .Net Framework 4.6.1 pode exigir a reinicialização do servidor. Ao instalar o Gateway do ATA em Controladores de Domínio, considere o agendamento de uma janela de manutenção para esses Controladores de Domínio.
Ao usar o método de instalação silenciosa do ATA, o instalador é configurado para reiniciar automaticamente o servidor no final da instalação (se necessário). Devido a um bug do Windows Installer, o sinalizador norestart não pode ser usado de forma confiável para garantir que o servidor não será reiniciado, portanto, certifique-se executar a instalação silenciosa somente durante uma janela de manutenção.

Para acompanhar o andamento da implantação, monitore os logs do instalador do ATA localizados em **%AppData%\Local\Temp**.


## <a name="install-the-ata-center"></a>Instalar a Central de ATA

Use o seguinte comando para instalar o Centro do ATA:

**Sintaxe**:

    "Microsoft ATA Center Setup.exe" [/quiet] [/Help] [--LicenseAccepted] [NetFrameworkCommandLineArguments="/q"] [InstallationPath="<InstallPath>"] [DatabaseDataPath= "<DBPath>"] [CenterIpAddress=<CenterIPAddress>] [CenterPort=<CenterPort>] [CenterCertificateThumbprint="<CertThumbprint>"] 
    [ConsoleIpAddress=<ConsoleIPAddress>] [ConsoleCertificateThumbprint="<CertThumbprint >"]
    
**Opções de instalação**:

> [!div class="mx-tableFixed"]
|Nome|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sim|Executa o instalador sem exibir a interface do usuário nem solicitações.|
|Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sim|Especifica os parâmetros para a instalação do .Net Framework. Deve ser definido para impor a instalação silenciosa do .Net Framework.|
|LicenseAccepted|--LicenseAccepted|Sim|Indica se a licença foi lida e aprovada. Deve ser definido na instalação silenciosa.|

**Parâmetros de instalação**:

> [!div class="mx-tableFixed"]
|Nome|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
|-------------|----------|---------|---------|
|InstallationPath|InstallationPath=“<InstallPath>”|Não|Define o caminho para a instalação dos binários do ATA. Caminho padrão: C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center|
|DatabaseDataPath|DatabaseDataPath= “<DBPath>”|Não|Define o caminho para a pasta de dados do Banco de Dados do ATA. Caminho padrão: C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|
|CenterIpAddress|CenterIpAddress=<CenterIPAddress>|Sim|Define o endereço IP do Serviço do Centro do ATA|
|CenterPort|CenterPort=<CenterPort>|Sim|Define a porta de rede do Serviço do Centro do ATA|
|CenterCertificateThumbprint|CenterCertificateThumbprint=“<CertThumbprint>”|Não|Define a impressão digital do certificado para o Serviço do Centro do ATA. Este certificado é usado para proteger a comunicação entre o Centro do ATA e o Gateway do ATA. Se não estiver definido, a instalação gerará um certificado autoassinado.|
|ConsoleIpAddress|ConsoleIpAddress=<ConsoleIPAddress>|Sim|Define o endereço IP do Console do ATA|
|ConsoleCertificateThumbprint|ConsoleCertificateThumbprint=”<CertThumbprint >”|Não|Especifica a impressão digital do certificado para o Console do ATA. Esse certificado é usado para validar a identidade do site do Console do ATA. Se não for especificado, a instalação vai gerar um certificado autoassinado|

**Exemplos**: instalar a Central do ATA com caminhos de instalação padrão e um único endereço IP:

    "Microsoft ATA Center Setup.exe" /quiet --LicenseAccepted NetFrameworkCommandLineArguments="/q" CenterIpAddress=192.168.0.10
    CenterPort=444 ConsoleIpAddress=192.168.0.10

Para instalar o Centro do ATA com caminhos de instalação padrão, dois endereços IP e as impressões digitais de certificado definidas pelo usuário:

    "Microsoft ATA Center Setup.exe" /quiet --LicenseAccepted NetFrameworkCommandLineArguments ="/q" CenterIpAddress=192.168.0.10 CenterPort=443 CenterCertificateThumbprint= ‎"1E2079739F624148ABDF502BF9C799FCB8C7212F"
    ConsoleIpAddress=192.168.0.11  ConsoleCertificateThumbprint="G9530253C976BFA9342FD1A716C0EC94207BFD5A"

## <a name="update-the-ata-center"></a>Atualize o Centro do ATA

Use o seguinte comando para atualizar o Centro do ATA:

**Sintaxe**:

    "Microsoft ATA Center Setup.exe" [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**Opções de instalação**:

> [!div class="mx-tableFixed"]
|Nome|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sim|Executa o instalador sem exibir a interface do usuário nem solicitações.|
|Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sim|Especifica os parâmetros para a instalação do .Net Framework. Deve ser definido para impor a instalação silenciosa do .Net Framework.|


Na atualização do ATA, o instalador detecta automaticamente que o ATA já está instalado no servidor, e nenhuma opção de instalação de atualização é obrigatória.

**Exemplos**: atualizar a Central do ATA no modo silencioso. Em ambientes grandes, a atualização do Centro do ATA pode demorar um pouco para ser concluída. Monitore os logs do ATA para acompanhar o andamento da atualização.

        "Microsoft ATA Center Setup.exe" /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-ata-center-silently"></a>Desinstalar o Centro do ATA silenciosamente

Use o seguinte comando para realizar uma desinstalação silenciosa da Central do ATA: **Sintaxe**:

    Microsoft ATA Center Setup.exe [/quiet] [/Uninstall] [/Help]
     [--DeleteExistingDatabaseData]

**Opções de instalação**:

> [!div class="mx-tableFixed"]
|Nome|Sintaxe|Obrigatório para desinstalação silenciosa?|Descrição|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sim|Executa o desinstalador sem exibir a interface do usuário nem solicitações.|
|Desinstalar|/uninstall|Sim|Executa a desinstalação silenciosa do Centro do ATA no servidor.|
|Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|

**Parâmetros de instalação**:

> [!div class="mx-tableFixed"]
|Nome|Sintaxe|Obrigatório para desinstalação silenciosa?|Descrição|
|-------------|----------|---------|---------|
|DeleteExistingDatabaseData|DeleteExistingDatabaseData|Não|Exclui todos os arquivos do banco de dados existente.|

**Exemplos**: desinstalar a Central do ATA do servidor no modo silencioso, removendo todos os dados do banco de dados existente:


    "Microsoft ATA Center Setup.exe" /quiet /uninstall --DeleteExistingDatabaseData

## <a name="ata-gateway-silent-installation"></a>Instalação silenciosa do Gateway do ATA

> [!NOTE]
> Ao implantar silenciosamente o Gateway Lightweight do ATA por meio do System Center Configuration Manager ou de outro sistema de implantação de software, é recomendável criar dois pacotes de implantação:</br>– Net Framework 4.6.1 incluindo inicializar o controlador de domínio</br>– Gateway do ATA. </br>Torne o pacote Gateway do ATA dependente da implantação do pacote .Net Framework. </br>Obtenha o pacote [de implantação offline do .Net Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49982). 


Use o seguinte comando para instalar silenciosamente o Gateway do ATA:

**Sintaxe**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments ="/q"] 
    [ConsoleAccountName="<AccountName>"] 
    [ConsoleAccountPassword="<AccountPassword>"]

> [!NOTE]
> Se você estiver trabalhando em um computador ingressado no domínio e tiver conectado usando seu nome de usuário e senha de administrador do ATA, não será necessário fornecer suas credenciais aqui.


**Opções de instalação**:

> [!div class="mx-tableFixed"]
|Nome|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sim|Executa o instalador sem exibir a interface do usuário nem solicitações.|
|Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sim|Especifica os parâmetros para a instalação do .Net Framework. Deve ser definido para impor a instalação silenciosa do .Net Framework.|

**Parâmetros de instalação**:

> [!div class="mx-tableFixed"]
|Nome|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
|-------------|----------|---------|---------|
|ConsoleAccountName|ConsoleAccountName=”<AccountName>”|Sim|Define o nome da conta do usuário (user@domain.com) usada para registrar o Gateway do ATA no Centro do ATA.|
|ConsoleAccountPassword|ConsoleAccountPassword=”<AccountPassword>”|Sim|Define a senha para a conta do usuário (user@domain.com) usada para registrar o Gateway do ATA no Centro do ATA.|

**Exemplos**: para instalar silenciosamente o log do Gateway do ATA no computador ingressado no domínio com suas credenciais de administrador do ATA e não será necessário especificar as credenciais. Caso contrário, registre-o no Centro do ATA usando as credenciais especificadas:

    "Microsoft ATA Gateway Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" 
    ConsoleAccountName="user@contoso.com" ConsoleAccountPassword="userpwd"
    

## <a name="update-the-ata-gateway"></a>Atualizar o Gateway do ATA

Use o seguinte comando para atualizar silenciosamente o Gateway do ATA:

**Sintaxe**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**Opções de instalação**:

> [!div class="mx-tableFixed"]
|Nome|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sim|Executa o instalador sem exibir a interface do usuário nem solicitações.|
|Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sim|Especifica os parâmetros para a instalação do .Net Framework. Deve ser definido para impor a instalação silenciosa do .Net Framework.|


**Exemplos**: atualizar o Gateway do ATA no modo silencioso:

        Microsoft ATA Gateway Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-ata-gateway-silently"></a>Desinstalar o Gateway do ATA silenciosamente

Use o seguinte comando para realizar uma desinstalação silenciosa do Gateway do ATA: **Sintaxe**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/Uninstall] [/Help]
    
**Opções de instalação**:

> [!div class="mx-tableFixed"]
|Nome|Sintaxe|Obrigatório para desinstalação silenciosa?|Descrição|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sim|Executa o desinstalador sem exibir a interface do usuário nem solicitações.|
|Desinstalar|/uninstall|Sim|Executa a desinstalação silenciosa do Gateway do ATA do servidor.|
|Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|

**Exemplos**: desinstalar o Gateway do ATA do servidor no modo silencioso:


    Microsoft ATA Gateway Setup.exe /quiet /uninstall
    









## <a name="see-also"></a>Consulte também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)