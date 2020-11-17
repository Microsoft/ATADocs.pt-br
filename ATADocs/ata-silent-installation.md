---
title: Instalar o Advanced Threat Analytics silenciosamente
description: Este artigo descreve como instalar silenciosamente o ATA.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 07/20/2020
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 55c12920020a0cbcda0b38e7b9d0cae083423a4e
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690968"
---
# <a name="ata-silent-installation"></a>Instalação silenciosa do ATA

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Este artigo fornece instruções de como instalar silenciosamente o ATA.

## <a name="prerequisites"></a>Pré-requisitos

A versão 1,9 do ATA requer a instalação do Microsoft .NET Framework 4.6.1.

Quando você instala ou atualiza o ATA, o .Net Framework 4.6.1 é instalado automaticamente como parte da implantação do Microsoft ATA.

> [!Note]
> A instalação do .Net Framework 4.6.1 pode exigir a reinicialização do servidor. Ao instalar o Gateway do ATA em Controladores de Domínio, considere o agendamento de uma janela de manutenção para esses Controladores de Domínio. Ao usar o método de instalação silenciosa do ATA, o instalador é configurado para reiniciar automaticamente o servidor no final da instalação (se necessário). Devido a um bug do Windows Installer, o sinalizador norestart não pode ser usado de forma confiável para garantir que o servidor não seja reiniciado, portanto, execute a instalação silenciosa somente durante uma janela de manutenção.

Para acompanhar o progresso da implantação, monitore os logs do instalador do ATA, que estão localizados em **%AppData%\Local\Temp**.

## <a name="install-the-ata-center"></a>Instalar a Central de ATA

Use o seguinte comando para instalar o Centro do ATA:

**Sintaxe**:

```dos
"Microsoft ATA Center Setup.exe" [/quiet] [/Help] [--LicenseAccepted] [NetFrameworkCommandLineArguments="/q"] [InstallationPath="<InstallPath>"] [DatabaseDataPath= "<DBPath>"] [CertificateThumbprint="<CertThumbprint>"]
```

**Opções de instalação**:

> [!div class="mx-tableFixed"]
>
> |Name|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
> |---|---|---|---|
> |Quiet|/quiet|Sim|Executa o instalador sem exibir a interface do usuário nem solicitações.|
> |Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sim|Especifica os parâmetros para a instalação do .Net Framework. Deve ser definido para impor a instalação silenciosa do .Net Framework.|
> |LicenseAccepted|--LicenseAccepted|Yes|Indica se a licença foi lida e aprovada. Deve ser definido na instalação silenciosa.|

**Parâmetros de instalação**:

> [!div class="mx-tableFixed"]
>
> |Name|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
> |---|---|---|---|
>|InstallationPath|InstallationPath=“<InstallPath>”|No|Define o caminho para a instalação dos binários do ATA. Caminho padrão: C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center|
>|DatabaseDataPath|DatabaseDataPath= “<DBPath>”|No|Define o caminho para a pasta de dados do Banco de Dados do ATA. Caminho padrão: C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|
>|CenterCertificateThumbprint|CenterCertificateThumbprint=“<CertThumbprint>”|No|Define a impressão digital do certificado para o centro do ATA. Esse certificado é usado para proteger a comunicação do gateway do ATA para o centro do ATA e para validar a identidade do site do console do ATA. Se não estiver definido, a instalação gerará um certificado autoassinado.|

**Exemplo**:

Para instalar o centro do ATA com os caminhos de instalação padrão e a impressão digital do certificado definido pelo usuário:

```dos
"Microsoft ATA Center Setup.exe" /quiet --LicenseAccepted NetFrameworkCommandLineArguments ="/q" CenterCertificateThumbprint= ‎"1E2079739F624148ABDF502BF9C799FCB8C7212F"
```

## <a name="update-the-ata-center"></a>Atualize o Centro do ATA

Use o seguinte comando para atualizar o Centro do ATA:

**Sintaxe**:

```dos
"Microsoft ATA Center Setup.exe" [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]
```

**Opções de instalação**:

> [!div class="mx-tableFixed"]
>
> |Name|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
> |---|---|---|---|
> |Quiet|/quiet|Sim|Executa o instalador sem exibir a interface do usuário nem solicitações.|
> |Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sim|Especifica os parâmetros para a instalação do .Net Framework. Deve ser definido para impor a instalação silenciosa do .Net Framework.|

Na atualização do ATA, o instalador detecta automaticamente que o ATA já está instalado no servidor, e nenhuma opção de instalação de atualização é obrigatória.

**Exemplos**:

para atualizar o Centro do ATA silenciosamente. Em ambientes grandes, a atualização do Centro do ATA pode demorar um pouco para ser concluída. Monitore os logs do ATA para acompanhar o andamento da atualização.

```dos
"Microsoft ATA Center Setup.exe" /quiet NetFrameworkCommandLineArguments="/q"
```

## <a name="uninstall-the-ata-center-silently"></a>Desinstalar o Centro do ATA silenciosamente

Use o seguinte comando para executar uma desinstalação silenciosa do Centro do ATA:

**Sintaxe**:

```dos
"Microsoft ATA Center Setup.exe" [/quiet] [/Uninstall] [/Help] [--DeleteExistingDatabaseData]
```

**Opções de instalação**:

> [!div class="mx-tableFixed"]
>
> |Name|Sintaxe|Obrigatório para desinstalação silenciosa?|Descrição|
> |---|---|---|---|
> |Quiet|/quiet|Sim|Executa o desinstalador sem exibir a interface do usuário nem solicitações.|
> |Desinstalar|/uninstall|Sim|Executa a desinstalação silenciosa do Centro do ATA no servidor.|
> |Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|

**Parâmetros de instalação**:

> [!div class="mx-tableFixed"]
>
> |Name|Sintaxe|Obrigatório para desinstalação silenciosa?|Descrição|
> |---|---|---|---|
> |DeleteExistingDatabaseData|DeleteExistingDatabaseData|No|Exclui todos os arquivos do banco de dados existente.|

**Exemplos**:

para desinstalar silenciosamente o Centro do ATA do servidor, removendo todos os dados do banco de dados existente:

```dos
"Microsoft ATA Center Setup.exe" /quiet /uninstall --DeleteExistingDatabaseData
```

## <a name="ata-gateway-silent-installation"></a>Instalação silenciosa do gateway do ATA

> [!NOTE]
> Ao implantar silenciosamente o Gateway Lightweight do ATA por meio do System Center Configuration Manager ou de outro sistema de implantação de software, é recomendável criar dois pacotes de implantação:</br>– Net Framework 4.6.1 incluindo inicializar o controlador de domínio</br>– Gateway do ATA. </br>Torne o pacote Gateway do ATA dependente da implantação do pacote .Net Framework. </br>Obtenha o pacote [de implantação offline do .Net Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49982).

Use o seguinte comando para instalar silenciosamente o Gateway do ATA:

**Sintaxe**:

```dos
"Microsoft ATA Gateway Setup.exe" [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"] [ConsoleAccountName="<AccountName>"] [ConsoleAccountPassword="<AccountPassword>"]
```

> [!NOTE]
> Se você estiver trabalhando em um computador ingressado no domínio e tiver conectado usando seu nome de usuário e senha de administrador do ATA, não será necessário fornecer suas credenciais aqui.

**Opções de instalação**:

> [!div class="mx-tableFixed"]
>
> |Name|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
> |---|---|---|---|
> |Quiet|/quiet|Sim|Executa o instalador sem exibir a interface do usuário nem solicitações.|
> |Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sim|Especifica os parâmetros para a instalação do .Net Framework. Deve ser definido para impor a instalação silenciosa do .Net Framework.|

**Parâmetros de instalação**:

> [!div class="mx-tableFixed"]
>
> |Name|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
> |---|---|---|---|
>|InstallationPath|InstallationPath=“<InstallPath>”|No|Define o caminho para a instalação dos binários do ATA. Caminho padrão: C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center
>|ConsoleAccountName|ConsoleAccountName=”<AccountName>”|Yes|Define o nome da conta do usuário (user@domain.com) usada para registrar o Gateway do ATA no Centro do ATA.|
>|ConsoleAccountPassword|ConsoleAccountPassword=”<AccountPassword>”|Yes|Define a senha para a conta do usuário (user@domain.com) usada para registrar o Gateway do ATA no Centro do ATA.|

**Exemplos**:

Para instalar silenciosamente o ATA Gateway, entre no computador no domínio com suas credenciais de administrador do ATA de modo que não seja necessário especificar as credenciais como parte da instalação. Caso contrário, registre-o no Centro do ATA usando as credenciais especificadas:

```dos
"Microsoft ATA Gateway Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" ConsoleAccountName="user@contoso.com" ConsoleAccountPassword="userpwd"
```

## <a name="update-the-ata-gateway"></a>Atualizar o Gateway do ATA

Use o seguinte comando para atualizar silenciosamente o Gateway do ATA:

**Sintaxe**:

```dos
"Microsoft ATA Gateway Setup.exe" [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]
```

**Opções de instalação**:

> [!div class="mx-tableFixed"]
>
> |Name|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
> |---|---|---|---|
> |Quiet|/quiet|Sim|Executa o instalador sem exibir a interface do usuário nem solicitações.|
> |Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sim|Especifica os parâmetros para a instalação do .Net Framework. Deve ser definido para impor a instalação silenciosa do .Net Framework.|

**Exemplos**:

para atualizar o Gateway do ATA silenciosamente:

```dos
"Microsoft ATA Gateway Setup.exe" /quiet NetFrameworkCommandLineArguments="/q"
```

## <a name="uninstall-the-ata-gateway-silently"></a>Desinstalar o Gateway do ATA silenciosamente

Use o seguinte comando para executar uma desinstalação silenciosa do Gateway do ATA:

**Sintaxe**:

```dos
"Microsoft ATA Gateway Setup.exe" [/quiet] [/Uninstall] [/Help]
```

**Opções de instalação**:

> [!div class="mx-tableFixed"]
>
> |Name|Sintaxe|Obrigatório para desinstalação silenciosa?|Descrição|
> |---|---|---|---|
> |Quiet|/quiet|Sim|Executa o desinstalador sem exibir a interface do usuário nem solicitações.|
> |Desinstalar|/uninstall|Sim|Executa a desinstalação silenciosa do Gateway do ATA do servidor.|
> |Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|

**Exemplos**:

para desinstalar silenciosamente o Gateway do ATA do servidor:

```dos
"Microsoft ATA Gateway Setup.exe" /quiet /uninstall
```

## <a name="see-also"></a>Consulte Também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)
