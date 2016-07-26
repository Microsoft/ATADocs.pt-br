---
title: Instalar o ATA silenciosamente | Microsoft ATA
description: Este artigo descreve como instalar o ATA silenciosamente.
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: ef4477dbd7f894ecd371008cf0d2325179c55bf5


---

# Instalação silenciosa do ATA
Este artigo fornece instruções de como instalar silenciosamente o ATA.
## Pré-requisitos

O Microsoft ATA v1.6 exige a instalação do Microsoft .NET Framework 4.6.1. 

Quando você instala ou atualiza o ATA, o .Net Framework 4.6.1 é instalado automaticamente como parte da implantação do Microsoft ATA.

> [!Note] 
> A instalação do .Net Framework 4.6.1 pode exigir a reinicialização do servidor. Ao instalar o Gateway do ATA em Controladores de Domínio, considere o agendamento de uma janela de manutenção para esses Controladores de Domínio.
Ao usar o método de instalação silenciosa do ATA, o instalador é configurado para reiniciar automaticamente o servidor no final da instalação (se necessário). Para evitar a reinicialização do servidor como parte da instalação, use o sinalizador `-NoRestart`. Com o sinalizador `-NoRestart`, quando a reinicialização for obrigatória como parte da instalação, o instalador ficará pausado até que o servido seja reiniciado. Para acompanhar o andamento da implantação, monitore os logs do instalador do ATA localizados em **%AppData%\Local\Temp**.


## Instalar a Central de ATA

Use o seguinte comando para instalar o Centro do ATA:

**Sintaxe**:

    “Microsoft ATA Center Setup.exe” [/quiet] [/NoRestart] [/Help] [--LicenseAccepted] [NetFrameworkCommandLineArguments=”/q”] [InstallationPath=“<InstallPath>”] [DatabaseDataPath= “<DBPath>”] [CenterIpAddress=<CenterIPAddress>] [CenterPort=<CenterPort>] [CenterCertificateThumbprint=“<CertThumbprint>”] 
    [ConsoleIpAddress=<ConsoleIPAddress>] [ConsoleCertificateThumbprint=”<CertThumbprint >”]
    
**Opções de instalação**:

|Nome|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sim|Executa o instalador sem exibir a interface do usuário nem solicitações.|
|NoRestart|/norestart|Não|Suprime todas as tentativas de reinicialização. Por padrão, a interface do usuário será solicitada antes da reinicialização.|
|Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sim|Especifica os parâmetros para a instalação do .Net Framework. Deve ser definido para impor a instalação silenciosa do .Net Framework.|
|LicenseAccepted|--LicenseAccepted|Sim|Indica se a licença foi lida e aprovada. Deve ser definido na instalação silenciosa.|

**Parâmetros de instalação**:

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

    “Microsoft ATA Center Setup.exe” /quiet --LicenseAccepted NetFrameworkCommandLineArguments="/q" CenterIpAddress=192.168.0.10
    CenterPort=444 ConsoleIpAddress=192.168.0.10

Para instalar o Centro do ATA com caminhos de instalação padrão, dois endereços IP e as impressões digitais de certificado definidas pelo usuário:

    “Microsoft ATA Center Setup.exe” /quiet --LicenseAccepted NetFrameworkCommandLineArguments ="/q" CenterIpAddress=192.168.0.10 CenterPort=443 CenterCertificateThumbprint= ‎"1E2079739F624148ABDF502BF9C799FCB8C7212F”
    ConsoleIpAddress=192.168.0.11  ConsoleCertificateThumbprint=”G9530253C976BFA9342FD1A716C0EC94207BFD5A”

## Atualize o Centro do ATA

Use o seguinte comando para atualizar o Centro do ATA:

**Sintaxe**:

    Microsoft ATA Center Setup.exe” [/quiet] [-NoRestart] /Help] [NetFrameworkCommandLineArguments=”/q”]


**Opções de instalação**:

|Nome|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sim|Executa o instalador sem exibir a interface do usuário nem solicitações.|
|NoRestart|/norestart|Não|Suprime todas as tentativas de reinicialização. Por padrão, a interface do usuário será solicitada antes da reinicialização.|
|Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sim|Especifica os parâmetros para a instalação do .Net Framework. Deve ser definido para impor a instalação silenciosa do .Net Framework.|


Na atualização do ATA, o instalador detecta automaticamente que o ATA já está instalado no servidor, e nenhuma opção de instalação de atualização é obrigatória.

**Exemplos**: atualizar a Central do ATA no modo silencioso. Em ambientes grandes, a atualização do Centro do ATA pode demorar um pouco para ser concluída. Monitore os logs do ATA para acompanhar o andamento da atualização.

        “Microsoft ATA Center Setup.exe” /quiet NetFrameworkCommandLineArguments="/q"

## Desinstalar o Centro do ATA silenciosamente

Use o seguinte comando para realizar uma desinstalação silenciosa da Central do ATA: **Sintaxe**:

    Microsoft ATA Center Setup.exe [/quiet] [/Uninstall] [/NoRestart] [/Help]
     [--DeleteExistingDatabaseData]

**Opções de instalação**:

|Nome|Sintaxe|Obrigatório para desinstalação silenciosa?|Descrição|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sim|Executa o desinstalador sem exibir a interface do usuário nem solicitações.|
|Desinstalar|/uninstall|Sim|Executa a desinstalação silenciosa do Centro do ATA no servidor.|
|NoRestart|/norestart|Não|Suprime todas as tentativas de reinicialização. Por padrão, a interface do usuário será solicitada antes da reinicialização.|
|Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|

**Parâmetros de instalação**:

|Nome|Sintaxe|Obrigatório para desinstalação silenciosa?|Descrição|
|-------------|----------|---------|---------|
|DeleteExistingDatabaseData|DeleteExistingDatabaseData|Não|Exclui todos os arquivos do banco de dados existente.|

**Exemplos**: desinstalar a Central do ATA do servidor no modo silencioso, removendo todos os dados do banco de dados existente:


    “Microsoft ATA Center Setup.exe” /quiet /uninstall --DeleteExistingDatabaseData

## Instalação silenciosa do Gateway do ATA
Use o seguinte comando para instalar silenciosamente o Gateway do ATA:

**Sintaxe**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/NoRestart] [/Help] [NetFrameworkCommandLineArguments ="/q"] 
    [GatewayCertificateThumbprint=”<CertThumbprint >”] [ConsoleAccountName=”<AccountName>”] 
    [ConsoleAccountPassword=”<AccountPassword>”]

**Opções de instalação**:

|Nome|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sim|Executa o instalador sem exibir a interface do usuário nem solicitações.|
|NoRestart|/norestart|Não|Suprime todas as tentativas de reinicialização. Por padrão, a interface do usuário será solicitada antes da reinicialização.|
|Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sim|Especifica os parâmetros para a instalação do .Net Framework. Deve ser definido para impor a instalação silenciosa do .Net Framework.|
|LicenseAccepted|--LicenseAccepted|Sim|Indica se a licença foi lida e aprovada. Deve ser definido na instalação silenciosa.|

**Parâmetros de instalação**:

|Nome|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
|-------------|----------|---------|---------|
|GatewayCertificateThumbprint|GatewayCertificateThumbprint=”<CertThumbprint >”|Não|Define a impressão digital do certificado para o serviço do Centro do ATA. Este certificado é usado para proteger a comunicação entre o Centro do ATA e o Gateway do ATA. Se não estiver definido, a instalação gerará um certificado autoassinado.|
|ConsoleAccountName|ConsoleAccountName=”<AccountName>”|Sim|Define o nome da conta do usuário (usuario@dominio.com) que é usada para registrar o Gateway do ATA no Centro do ATA.|
|ConsoleAccountPassword|ConsoleAccountPassword=”<AccountPassword>”|Sim|Define a senha da conta do usuário (usuario@dominio.com) que é usada para registrar o Gateway do ATA no Centro do ATA.|

**Exemplos**: instalar o Gateway do ATA no modo silencioso e registrá-lo na Central do ATA usando as credenciais especificadas:

    “Microsoft ATA Gateway Setup.exe” /quiet NetFrameworkCommandLineArguments="/q" 
    ConsoleAccountName=”user@contoso.com” ConsoleAccountPassword=“userpwd”
    

## Atualizar o Gateway do ATA

Use o seguinte comando para atualizar silenciosamente o Gateway do ATA:

**Sintaxe**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/NoRestart] /Help] [NetFrameworkCommandLineArguments="/q"]


**Opções de instalação**:

|Nome|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sim|Executa o instalador sem exibir a interface do usuário nem solicitações.|
|NoRestart|/norestart|Não|Suprime todas as tentativas de reinicialização. Por padrão, a interface do usuário será solicitada antes da reinicialização.|
|Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sim|Especifica os parâmetros para a instalação do .Net Framework. Deve ser definido para impor a instalação silenciosa do .Net Framework.|


**Exemplos**: atualizar o Gateway do ATA no modo silencioso:

        Microsoft ATA Gateway Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## Desinstalar o Gateway do ATA silenciosamente

Use o seguinte comando para realizar uma desinstalação silenciosa do Gateway do ATA: **Sintaxe**:

    Microsoft ATA Gateway Setup.exe [/quiet] [/Uninstall] [/NoRestart] [/Help]
    
**Opções de instalação**:

|Nome|Sintaxe|Obrigatório para desinstalação silenciosa?|Descrição|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sim|Executa o desinstalador sem exibir a interface do usuário nem solicitações.|
|Desinstalar|/uninstall|Sim|Executa a desinstalação silenciosa do Gateway do ATA do servidor.|
|NoRestart|/norestart|Não|Suprime todas as tentativas de reinicialização. Por padrão, a interface do usuário será solicitada antes da reinicialização.|
|Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|

**Exemplos**: desinstalar o Gateway do ATA do servidor no modo silencioso:


    Microsoft ATA Gateway Setup.exe /quiet /uninstall
    









## Consulte também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)


<!--HONumber=Jul16_HO3-->


