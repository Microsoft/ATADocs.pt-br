---
title: Instalar a Proteção Avançada contra Ameaças do Azure silenciosamente | Microsoft Docs
description: Este artigo descreve como instalar silenciosamente o Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/11/2017
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 24eca4c6-c949-42ea-97b9-41ef0fb611f1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f27020f1b4a5fa7aa8fefbda28eac0c2ad6c64d0
ms.sourcegitcommit: 912e453753156902618ae6ebb8489c2320c06fc6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/12/2018
ms.locfileid: "29856474"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*


# <a name="azure-atp-silent-installation"></a>Instalação silenciosa do Azure ATP
Este artigo fornece instruções de como instalar silenciosamente o Azure ATP.

## <a name="prerequisites"></a>Pré-requisitos

O Azure ATP requer a instalação do Microsoft .NET Framework 4.7. 

Quando você instala o Azure ATP, o .Net Framework 4.7 é instalado automaticamente como parte da implantação do Azure ATP.

> [!IMPORTANT] 
> Verifique se a versão instalada do .Net Framework é a mais recente. Se uma versão anterior do .Net estiver instalada, a instalação silenciosa do Azure ATP ficará presa em um loop e não será realizada. 

> [!NOTE] 
> A instalação do .Net Framework 4.7 pode exigir a reinicialização do servidor. Ao instalar o sensor do Azure ATP em Controladores de domínio, considere agendar uma janela de manutenção para esses Controladores de domínio.
Ao usar o método de instalação silenciosa do Azure ATP, o instalador é configurado para reiniciar automaticamente o servidor no final da instalação (se necessário). Devido a um bug do Windows Installer, o sinalizador *norestart* não pode ser usado de forma confiável para garantir que o servidor não seja reiniciado, portanto, execute a instalação silenciosa somente durante uma janela de manutenção.

Para acompanhar o andamento da implantação, monitore os logs do instalador do Azure ATP localizados em **%AppData%\Local\Temp**.



## <a name="azure-atp-sensor-silent-installation"></a>Instalação silenciosa do sensor do Azure ATP

> [!NOTE]
> Ao implantar silenciosamente o sensor do Azure ATP por meio do System Center Configuration Manager ou de outro sistema de implantação de software, é recomendável criar dois pacotes de implantação:</br>– Net Framework 4.7, incluindo inicializar o controlador de domínio</br>– Sensor do Azure ATP. </br>Torne o sensor do Azure ATP dependente da implantação do pacote .Net Framework. </br>Obtenha o [Pacote de implantação offline do .Net Framework 4.7](https://www.microsoft.com/download/details.aspx?id=49982). 


Use o seguinte comando para instalar silenciosamente o sensor do Azure ATP:

**Sintaxe**:

    Azure ATP sensor Setup.exe [/AccessKey=<Access Key>] [/quiet] [/Help] [NetFrameworkCommandLineArguments ="/q"] 
   

> [!NOTE]
> Copie a chave de acesso do portal de espaço de trabalho em **Configuração** e, em seguida, **sensor**.


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
|AccessKey|AccessKey="**"|Sim|Define a chave de acesso que é usada para registrar o sensor do Azure ATP com o espaço de trabalho do Azure ATP.|

**Exemplos**: para instalar silenciosamente o sensor do Azure ATP, faça logon no computador ingressado no domínio com suas credenciais de administrador do Azure ATP de modo que não seja necessário especificar as credenciais como parte da instalação. Caso contrário, registre-o no serviço de nuvem do Azure ATP usando as credenciais especificadas:

    "Azure ATP sensor Setup.exe" /quiet NetFrameworkCommandLineArguments="/q" 
    AccessKey="3WlO0uKW7lY6Lk0+dfkfkJQ0qZV6aSq5WxLf71+fuBhggCl/BMs9JxfAwi7oy9vYGviazUS1EPpzte7z8s4grw==" 
    

## <a name="update-the-azure-atp-sensor"></a>Atualizar o sensor do Azure ATP

Use o seguinte comando para atualizar silenciosamente o sensor do Azure ATP:

**Sintaxe**:

    Azure ATP  sensor Setup.exe [/quiet] [/Help] [NetFrameworkCommandLineArguments="/q"]


**Opções de instalação**:

> [!div class="mx-tableFixed"]
|Nome|Sintaxe|Obrigatório para instalação silenciosa?|Descrição|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sim|Executa o instalador sem exibir a interface do usuário nem solicitações.|
|Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|Sim|Especifica os parâmetros para a instalação do .Net Framework. Deve ser definido para impor a instalação silenciosa do .Net Framework.|


**Exemplos**: para atualizar o sensor do Azure ATP silenciosamente:

        Azure ATP sensor Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## <a name="uninstall-the-azure-atp-sensor-silently"></a>Desinstalar o sensor do Azure ATP silenciosamente

Use o seguinte comando para realizar uma desinstalação silenciosa do sensor do ATP do Azure: **Sintaxe**:

    Azure ATP sensor Setup.exe [/quiet] [/Uninstall] [/Help]
    
**Opções de instalação**:

> [!div class="mx-tableFixed"]
|Nome|Sintaxe|Obrigatório para desinstalação silenciosa?|Descrição|
|-------------|----------|---------|---------|
|Quiet|/quiet|Sim|Executa o desinstalador sem exibir a interface do usuário nem solicitações.|
|Desinstalar|/uninstall|Sim|Executa a desinstalação silenciosa do sensor do Azure ATP do servidor.|
|Ajuda|/help|Não|Fornece ajuda e referência rápida. Exibe o uso correto do comando de configuração, incluindo uma lista de todas as opções e comportamentos.|

**Exemplos**: para desinstalar silenciosamente o sensor do Azure ATP do servidor:


    Azure ATP sensor Setup.exe /quiet /uninstall
    



## <a name="see-also"></a>Consulte Também

- [Configurar o encaminhamento de eventos](configure-event-forwarding.md)
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)