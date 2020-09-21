---
title: Instalar a Proteção Avançada contra Ameaças do Azure silenciosamente
description: Este artigo descreve como instalar silenciosamente o Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 07/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 24eca4c6-c949-42ea-97b9-41ef0fb611f1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 07eefcf95846384ad490fa815f2415b771b73955
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90828000"
---
# <a name="azure-atp-switches-and-silent-installation"></a>Instalação silenciosa e opções do Azure ATP

Este artigo fornece diretrizes e instruções para a instalação silenciosa e opções do Azure ATP.

## <a name="prerequisites"></a>Pré-requisitos

O ATP do Azure requer a instalação do Microsoft .NET Framework 4.7 ou posterior.

Quando você instala o ATP do Azure, o .NET Framework 4.7 é instalado automaticamente como parte da implantação do ATP do Azure se o .NET Framework 4.7 ou posterior ainda não está instalado.

> [!NOTE]
> A instalação do .Net Framework 4.7 pode exigir a reinicialização do servidor. Ao instalar o sensor do ATP do Azure em controladores de domínio, considere agendar uma janela de manutenção para eles.

Ao usar a instalação silenciosa do Azure ATP, o instalador é configurado para reiniciar automaticamente o servidor no final da instalação (se necessário). Certifique-se de executar a instalação silenciosa somente durante uma janela de manutenção. Devido a um bug do Windows Installer, o sinalizador *norestart* não pode ser usado de forma confiável para garantir que o servidor não seja reiniciado.

Para acompanhar o progresso da implantação, monitore os logs do instalador do ATP do Azure localizados em `%AppData%\Local\Temp`.

## <a name="azure-atp-sensor-silent-installation"></a>Instalação silenciosa do sensor do Azure ATP

> [!NOTE]
> Ao implantar silenciosamente o sensor do Azure ATP por meio do System Center Configuration Manager ou de outro sistema de implantação de software, é recomendável criar dois pacotes de implantação:</br>– Net Framework 4.7 ou posterior, que pode incluir a reinicialização do controlador de domínio</br>– Sensor do Azure ATP. </br>Torne o sensor do Azure ATP dependente da implantação do pacote .Net Framework. </br>Obtenha o [Pacote de implantação offline do .Net Framework 4.7](https://support.microsoft.com/help/3186497/the-net-framework-4-7-offline-installer-for-windows).

Use o seguinte comando para realizar uma instalação silenciosa completa do sensor do Azure ATP:

**cmd.exe syntax**:

```dos
"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"
```

**Sintaxe do PowerShell**:

```powershell
./"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"
```

> [!NOTE]
> Ao usar a sintaxe do PowerShell, omitir o prefácio **./** resulta em um erro que impede a instalação silenciosa.

> [!NOTE]
> Copie a chave de acesso do portal do ATP do Azure, na seção **Configuração**, na página **Sensor**.

**Opções de instalação**:

> [!div class="mx-tableFixed"]
>
> |Name|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|Sim|Executa o instalador sem exibir a interface do usuário nem solicitações.|
> |Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sim|Especifica os parâmetros para a instalação do .Net Framework. Deve ser definido para impor a instalação silenciosa do .Net Framework.|

**Parâmetros de instalação**:

> [!div class="mx-tableFixed"]
>
> |Name|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
> |-------------|----------|---------|---------|
> |InstallationPath|InstallationPath=“”|Não|Define o caminho para a instalação dos binários do sensor AATP. Caminho padrão: %programfiles%\Sensor da Proteção Avançada contra Ameaças do Azure
> |AccessKey|AccessKey="\*\*"|Sim|Define a chave de acesso que é usada para registrar o sensor do ATP do Azure na instância do ATP do Azure.|

**Exemplos**:

Use o seguinte comando para instalar silenciosamente o sensor do Azure ATP:

```dos
"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="mmAOkLYCzfH8L/zUIsH24BIJBevlAWu7wUcSfIkRJufpuEojaDHYdjrNs0P3zpD+/bObKfLS0puD7biT5KDf3g=="
```

## <a name="proxy-authentication"></a>Autenticação de proxy

Use os seguintes comandos para concluir a autenticação de proxy:

**Sintaxe**:

> [!div class="mx-tableFixed"]
>
> |Name|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
> |-------------|----------|---------|---------|
> |ProxyUrl|ProxyUrl="http\://proxy.contoso.com:8080"|Não|Especifica o ProxyUrl e o número da porta para o sensor do ATP do Azure.|
> |ProxyUserName|ProxyUserName="Contoso\ProxyUser"|Não|Se o seu serviço de proxy exigir autenticação, forneça um nome de usuário no formato DOMÍNIO\usuário.|
> |ProxyUserPassword|ProxyUserPassword="P@ssw0rd"|Não|Especifica a senha para o nome de usuário do proxy. *As credenciais são criptografadas e armazenadas localmente pelo sensor do ATP do Azure.|

## <a name="update-the-azure-atp-sensor"></a>Atualizar o sensor do Azure ATP

Use o seguinte comando para atualizar silenciosamente o sensor do Azure ATP:

**Sintaxe**:

```dos
"Azure ATP sensor Setup.exe" [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]
```

**Opções de instalação**:

> [!div class="mx-tableFixed"]
>
> |Name|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|Sim|Executa o instalador sem exibir a interface do usuário nem solicitações.|
> |Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|
> |NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sim|Especifica os parâmetros para a instalação do .Net Framework. Deve ser definido para impor a instalação silenciosa do .Net Framework.|

**Exemplos**:

para atualizar silenciosamente o sensor do ATP do Azure:

```dos
"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q"
```

## <a name="uninstall-the-azure-atp-sensor-silently"></a>Desinstalar o sensor do Azure ATP silenciosamente

Use o comando a seguir para realizar uma desinstalação silenciosa do sensor do ATP do Azure:

**Sintaxe**:

```dos
"Azure ATP sensor Setup.exe" [/quiet] [/Uninstall] [/Help]
```

**Opções de instalação**:

> [!div class="mx-tableFixed"]
>
> |Name|Sintaxe|Obrigatório para desinstalação silenciosa?|Descrição|
> |-------------|----------|---------|---------|
> |Quiet|/quiet|Sim|Executa o desinstalador sem exibir a interface do usuário nem solicitações.|
> |Desinstalar|/uninstall|Sim|Executa a desinstalação silenciosa do sensor do Azure ATP do servidor.|
> |Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|

**Exemplos**:

para desinstalar silenciosamente o sensor do ATP do Azure do servidor:

```dos
"Azure ATP sensor Setup.exe" /quiet /uninstall
```

## <a name="see-also"></a>Consulte Também

- [Pré-requisitos do Azure ATP](prerequisites.md)
- [Instalar o sensor do Azure ATP](install-step4.md)
- [Configurar o sensor do Azure ATP](install-step5.md)
- [Confira o fórum do Azure ATP!](https://aka.ms/azureatpcommunity)
