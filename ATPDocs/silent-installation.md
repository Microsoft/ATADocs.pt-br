---
title: Instalar o Microsoft defender para identidade silenciosamente
description: Isso descreve como instalar silenciosamente o Microsoft defender para identidade.
ms.date: 01/11/2021
ms.topic: how-to
ms.openlocfilehash: 0c22f5bcbffd415a81b84c94570cfcd7387aab56
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100534388"
---
# <a name="microsoft-defender-for-identity-switches-and-silent-installation"></a>Microsoft defender para comutadores de identidade e instalação silenciosa

Este artigo fornece orientações e instruções para [!INCLUDE [Product long](includes/product-long.md)] comutadores e instalação silenciosa.

## <a name="prerequisites"></a>Pré-requisitos

[!INCLUDE [Product short](includes/product-short.md)] requer a instalação do Microsoft .NET Framework 4,7 ou posterior.

Quando você instala [!INCLUDE [Product short](includes/product-short.md)] o, o .NET framework 4,7 é instalado automaticamente como parte da implantação do [!INCLUDE [Product short](includes/product-short.md)] se o .net Framework 4,7 ou posterior ainda não estiver instalado.

> [!NOTE]
> A instalação do .Net Framework 4.7 pode exigir a reinicialização do servidor. Ao instalar o [!INCLUDE [Product short](includes/product-short.md)] sensor em controladores de domínio, considere agendar uma janela de manutenção para os controladores de domínio.

Usando [!INCLUDE [Product short](includes/product-short.md)] a instalação silenciosa, o instalador é configurado para reiniciar automaticamente o servidor no final da instalação (se necessário). Certifique-se de executar a instalação silenciosa somente durante uma janela de manutenção. Devido a um bug do Windows Installer, o sinalizador *norestart* não pode ser usado de forma confiável para garantir que o servidor não seja reiniciado.

Para acompanhar o progresso da implantação, monitore os [!INCLUDE [Product short](includes/product-short.md)] logs do instalador, que estão localizados em `%AppData%\Local\Temp` .

## <a name="defender-for-identity-sensor-silent-installation"></a>Instalação silenciosa do sensor do defender for Identity

> [!NOTE]
> Ao implantar silenciosamente o [!INCLUDE [Product short](includes/product-short.md)] sensor por meio de System Center Configuration Manager ou outro sistema de implantação de software, é recomendável criar dois pacotes de implantação:</br>– Net Framework 4.7 ou posterior, que pode incluir a reinicialização do controlador de domínio</br>- [!INCLUDE [Product short](includes/product-short.md)] sensores. </br>Faça com que o [!INCLUDE [Product short](includes/product-short.md)] pacote do sensor dependa da implantação da implantação do pacote do .NET Framework. </br>Obtenha o [Pacote de implantação offline do .Net Framework 4.7](https://support.microsoft.com/help/3186497/the-net-framework-4-7-offline-installer-for-windows).

Use o seguinte comando para executar uma instalação totalmente silenciosa do [!INCLUDE [Product short](includes/product-short.md)] sensor:

**cmd.exe syntax**:

```dos
"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"
```

**Sintaxe do PowerShell**:

```powershell
.\"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" AccessKey="<Access Key>"
```

> [!NOTE]
> Ao usar a sintaxe do PowerShell, omitir o prefácio **./** resulta em um erro que impede a instalação silenciosa.

> [!NOTE]
> Copie a chave de acesso da [!INCLUDE [Product short](includes/product-short.md)] seção **configuração** do portal, página **sensores** .

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
> |InstallationPath|InstallationPath=“”|Não|Define o caminho para a instalação de [!INCLUDE [Product short](includes/product-short.md)] binários do sensor. Caminho padrão: %programfiles%\Sensor da Proteção Avançada contra Ameaças do Azure
> |AccessKey|AccessKey="\*\*"|Sim|Define a chave de acesso usada para registrar o [!INCLUDE [Product short](includes/product-short.md)] sensor com a [!INCLUDE [Product short](includes/product-short.md)] instância.|

**Exemplos**:

Use o seguinte comando para instalar silenciosamente o [!INCLUDE [Product short](includes/product-short.md)] sensor:

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
> |ProxyUrl|ProxyUrl="http\://proxy.contoso.com:8080"|Não|Especifica a ProxyUrl e o número da porta para o sensor do [!INCLUDE [Product short](includes/product-short.md)].|
> |ProxyUserName|ProxyUserName="Contoso\ProxyUser"|Não|Se o seu serviço de proxy exigir autenticação, forneça um nome de usuário no formato DOMÍNIO\usuário.|
> |ProxyUserPassword|ProxyUserPassword="P@ssw0rd"|Não|Especifica a senha para o nome de usuário do proxy. *As credenciais são criptografadas e armazenadas localmente pelo sensor do [!INCLUDE [Product short](includes/product-short.md)].|

Para obter mais informações sobre a configuração de proxy, consulte [definir configurações de proxy de ponto de extremidade e conectividade de Internet para seu [!INCLUDE [Product long](includes/product-long.md)] sensor](configure-proxy.md).

## <a name="update-the-defender-for-identity-sensor"></a>Atualizar o defender para o sensor de identidade

Use o seguinte comando para atualizar silenciosamente o [!INCLUDE [Product short](includes/product-short.md)] sensor:

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

Para atualizar o [!INCLUDE [Product short](includes/product-short.md)] sensor silenciosamente:

```dos
"Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q"
```

<a name="silently-uninstall-sensor"></a>

## <a name="uninstall-the-defender-for-identity-sensor-silently"></a>Desinstalar o defender para o sensor de identidade silenciosamente

Use o seguinte comando para executar uma desinstalação silenciosa do [!INCLUDE [Product short](includes/product-short.md)] sensor:

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
> |Desinstalar|/uninstall|Sim|Executa a desinstalação silenciosa do [!INCLUDE [Product short](includes/product-short.md)] sensor do servidor.|
> |Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|

**Exemplos**:

Para desinstalar silenciosamente o [!INCLUDE [Product short](includes/product-short.md)] sensor do servidor:

```dos
"Azure ATP sensor Setup.exe" /quiet /uninstall
```

## <a name="see-also"></a>Consulte Também

- [Pré-requisitos do [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Instalar o [!INCLUDE [Product short](includes/product-short.md)] sensor](install-step4.md)
- [Configurar o [!INCLUDE [Product short](includes/product-short.md)] sensor](install-step5.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
