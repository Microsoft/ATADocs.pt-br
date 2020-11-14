---
title: Pré-requisitos do Microsoft Defender para Identidade
description: Descreve os requisitos para uma implantação bem-sucedida do Microsoft Defender para Identidade no seu ambiente
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: overview
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e3b5b67ad5330fd7be41ed63e6db105e2f1d4a9e
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93275635"
---
# <a name="product-long-prerequisites"></a>Pré-requisitos do [!INCLUDE [Product long](includes/product-long.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Este artigo descreve os requisitos para uma implantação bem-sucedida do [!INCLUDE [Product long](includes/product-long.md)] no seu ambiente.

>[!NOTE]
> Para obter informações sobre como planejar a capacidade e os recursos, confira [Planejamento da capacidade do [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md).

O [!INCLUDE [Product short](includes/product-short.md)] é composto pelo serviço de nuvem do [!INCLUDE [Product short](includes/product-short.md)], que consiste no portal do [!INCLUDE [Product short](includes/product-short.md)] e no sensor do [!INCLUDE [Product short](includes/product-short.md)]. Para obter mais informações sobre cada um dos componentes do [!INCLUDE [Product short](includes/product-short.md)], confira [Arquitetura do [!INCLUDE [Product short](includes/product-short.md)]](architecture.md).

O [!INCLUDE [Product short](includes/product-short.md)] protege seus usuários locais do Active Directory e/ou os usuários sincronizados com o Azure Active Directory. Para proteger um ambiente composto apenas por usuários do AAD, confira a [Proteção de Identidade do AAD](/azure/active-directory/identity-protection/overview).

Para criar sua instância do [!INCLUDE [Product short](includes/product-short.md)], você precisará ter um locatário do AAD com, pelo menos, um administrador da segurança/global. Cada instância do [!INCLUDE [Product short](includes/product-short.md)] dá suporte a vários limites de floresta do Active Directory e ao FFL (Nível funcional da floresta) do Windows 2003 e superior.

Este guia de pré-requisitos é dividido nas seções a seguir para garantir que você tem tudo de que precisa para implantar o [!INCLUDE [Product short](includes/product-short.md)] com êxito.

[Antes de começar](#before-you-start): Lista as informações a serem reunidas e as contas e entidades de rede de que você precisará antes de iniciar a instalação.

[Portal do [!INCLUDE [Product short](includes/product-short.md)]](#azure-atp-portal-requirements): descreve os requisitos do navegador do portal do [!INCLUDE [Product short](includes/product-short.md)].

[Sensor do [!INCLUDE [Product short](includes/product-short.md)]](#azure-atp-sensor-requirements): lista os requisitos de hardware e software do sensor do [!INCLUDE [Product short](includes/product-short.md)].

[Sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)]](#azure-atp-standalone-sensor-requirements): o sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] é instalado em um servidor dedicado e exige a configuração do espelhamento de porta no controlador de domínio para receber o tráfego de rede.

> [!NOTE]
> Os sensores autônomos do [!INCLUDE [Product short](includes/product-short.md)] não dão suporte à coleção de entradas de log do ETW (Rastreamento de Eventos para Windows) que fornecem os dados para várias detecções. Para cobertura completa do seu ambiente, recomendamos implantar o sensor do [!INCLUDE [Product short](includes/product-short.md)].

## <a name="before-you-start"></a>Antes de começar

Esta seção lista as informações que você deve obter, bem como as contas e as informações sobre entidades de rede que deve ter antes de iniciar a instalação do [!INCLUDE [Product short](includes/product-short.md)].

- Adquira uma licença do EMS E5 (Enterprise Mobility + Security 5) diretamente usando o [portal do Microsoft 365](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing) ou use o modelo de licenciamento do CSP (Parceiro de Soluções na Nuvem). Licenças autônomas do [!INCLUDE [Product short](includes/product-short.md)] também estão disponíveis.

- Confirme se os controladores de domínio nos quais você pretende instalar os sensores do [!INCLUDE [Product short](includes/product-short.md)] têm conectividade com a Internet para o serviço de nuvem do [!INCLUDE [Product short](includes/product-short.md)]. O sensor do [!INCLUDE [Product short](includes/product-short.md)] dá suporte ao uso de um proxy. Para obter mais informações sobre a configuração de proxy, confira [Como configurar um proxy para o [!INCLUDE [Product short](includes/product-short.md)]](configure-proxy.md).

- Pelo menos uma das seguintes contas de serviços de diretório com acesso de leitura a todos os objetos nos domínios monitorados:
  - Uma conta de usuário do AD **padrão** e senha. Exigidas para sensores que executam o Windows Server 2008 R2 SP1.
  - Uma **gMSA (Conta de Serviço Gerenciado de Grupo)** . Requer Windows Server 2012 ou posterior.  
  Todos os sensores devem ter permissões para recuperar a senha da conta gMSA.  
  Para saber mais sobre contas gMSA, confira [Introdução às Contas de Serviço Gerenciado de Grupo](/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts#BKMK_CreateGMSA).

    A tabela a seguir mostra quais contas de usuário do AD podem ser usadas com quais versões de servidor:

    |Tipo de conta|Windows Server 2008 R2 SP1|Windows Server 2012 ou posterior|
    |---|---|---|
    |Conta de usuário do AD **padrão**|Sim|Sim|
    |Conta **gMSA**|Não|Sim|

    > [!NOTE]
    >
    > - Para computadores sensores que executam o Windows Server 2012 e posterior, recomendamos usar uma conta **gMSA** devido à segurança aprimorada e ao gerenciamento automático de senhas.
    > - Se você tiver vários sensores, alguns executando o Windows Server 2008 e outros executando o Windows Server 2012 ou posterior, além da recomendação para usar uma conta **gMSA** , você também deverá usar pelo menos uma conta de usuário do AD **padrão**.
    > - Se você tiver definido ACLs personalizadas em várias Unidades Organizacionais (UO) em seu domínio, verifique se o usuário selecionado tem permissões de leitura para essas UOs.

- Se você executar o Wireshark no sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)], reinicie o serviço de sensor do [!INCLUDE [Product short](includes/product-short.md)] depois de interromper a captura do Wireshark. Se não reiniciar o serviço de sensor, o sensor interromperá a captura de tráfego.

- Se você tentar instalar o sensor do [!INCLUDE [Product short](includes/product-short.md)] em um computador configurado com um adaptador de Agrupamento NIC, receberá um erro de instalação. Caso deseje instalar o sensor do [!INCLUDE [Product short](includes/product-short.md)] em um computador configurado com Agrupamento NIC, confira [Problemas do Agrupamento NIC do sensor do [!INCLUDE [Product short](includes/product-short.md)]](troubleshooting-known-issues.md#nic-teaming).

- Recomendação de contêiner de **Objetos Excluídos** : O usuário deve ter permissões de somente leitura no contêiner de Objetos Excluídos. As permissões somente leitura neste contêiner permitem que o [!INCLUDE [Product short](includes/product-short.md)] detecte exclusões de usuários do Active Directory. Para obter informações sobre como configurar permissões somente leitura no contêiner Objetos Excluídos, confira a seção **Como alterar permissões em um contêiner de objetos excluídos** do artigo [Exibir ou definir permissões em um objeto do directory](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc816824(v=ws.10)).

- **Honeytoken** opcional: Uma conta de usuário que não tem nenhuma atividade de rede. Essa conta está configurada como o usuário Honeytoken do [!INCLUDE [Product short](includes/product-short.md)]. Para obter mais informações sobre como usar Honeytokens, confira [Configurar exclusões e usuário do Honeytoken](install-step7.md).

- Opcional: ao implantar o sensor autônomo, é necessário encaminhar os [eventos do Windows](configure-windows-event-collection.md#configure-event-collection) para o [!INCLUDE [Product short](includes/product-short.md)] para aprimorar ainda mais as adições a grupos confidenciais, as detecções de criação de serviço suspeito e as detecções baseadas na autenticação do [!INCLUDE [Product short](includes/product-short.md)].  O sensor do [!INCLUDE [Product short](includes/product-short.md)] recebe esses eventos automaticamente. No sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)], esses eventos podem ser recebidos do SIEM ou pela definição do Encaminhamento de Eventos do Windows no controlador de domínio. Os eventos coletados fornecem ao [!INCLUDE [Product short](includes/product-short.md)] informações adicionais que não estão disponíveis por meio do tráfego de rede do controlador de domínio.

<a name="azure-atp-portal-requirements"></a>

## <a name="product-short-portal-requirements"></a>Requisitos do portal do [!INCLUDE [Product short](includes/product-short.md)]

O acesso ao portal do [!INCLUDE [Product short](includes/product-short.md)] ocorre por meio de um navegador, que dá suporte aos seguintes navegadores e configurações:

- Um navegador compatível com TLS 1.2, como:
  - Microsoft Edge
  - Internet Explorer versão 11 e posterior
  - Google Chrome 30.0 e posterior
- Resolução de largura mínima da tela de 1.700 pixels
- Firewall/proxy aberto: para se comunicar com o serviço de nuvem do [!INCLUDE [Product short](includes/product-short.md)], a porta 443 de *.atp.azure.com precisa ser aberta no firewall/proxy.

    > [!NOTE]
    > Use também nossa marca de serviço do Azure ( **AzureAdvancedThreatProtection** ) para habilitar o acesso ao [!INCLUDE [Product short](includes/product-short.md)]. Para obter mais informações sobre marcas de serviço, confira [Marcas de serviço de rede virtual](/azure/virtual-network/service-tags-overview) ou [baixe o arquivo de marcas de serviço](https://www.microsoft.com/download/details.aspx?id=56519).

 ![Diagrama da arquitetura do [!INCLUDE [Product short](includes/product-short.md)]](media/architecture-topology.png)

> [!NOTE]
> Por padrão, o [!INCLUDE [Product short](includes/product-short.md)] dá suporte a até 200 sensores. Caso deseje instalar mais sensores, entre em contato com o suporte do [!INCLUDE [Product short](includes/product-short.md)].

## <a name="product-short-network-name-resolution-nnr-requirements"></a>Requisitos da NNR (Resolução de Nomes de Rede) do [!INCLUDE [Product short](includes/product-short.md)]

A NNR (Resolução de Nomes de Rede) é um componente principal da funcionalidade do [!INCLUDE [Product short](includes/product-short.md)]. Para resolver os endereços IP para nomes do computador, os sensores do [!INCLUDE [Product short](includes/product-short.md)] pesquisam os endereços IP usando os seguintes métodos:

- NTLM sobre RPC (porta TCP 135)
- NetBIOS (porta UDP 137)
- RDP (porta TCP 3389): apenas o primeiro pacote do **Client hello**
- Consultas ao servidor DNS usando a pesquisa de DNS reverso do endereço IP (UDP 53)

Para que os três primeiros métodos funcionem, as portas relevantes precisam ser abertas para entrada dos sensores do [!INCLUDE [Product short](includes/product-short.md)] para os dispositivos na rede. Para saber mais sobre o [!INCLUDE [Product short](includes/product-short.md)] e a NNR, confira [Política da NNR do [!INCLUDE [Product short](includes/product-short.md)]](nnr-policy.md).

Recomendamos o uso de todos os métodos para obter os melhores resultados. Se isso não for possível, você deverá usar o método de pesquisa de DNS e pelo menos um dos outros métodos.

<a name="azure-atp-sensor-requirements"></a>

## <a name="product-short-sensor-requirements"></a>Requisitos do sensor do [!INCLUDE [Product short](includes/product-short.md)]

Esta seção lista os requisitos do sensor do [!INCLUDE [Product short](includes/product-short.md)].

### <a name="general"></a>Geral

O sensor do [!INCLUDE [Product short](includes/product-short.md)] dá suporte à instalação em um controlador de domínio que executa o Windows Server 2008 R2 SP1 (não incluindo o Server Core), o Windows Server 2012, o Windows Server 2012 R2, o Windows Server 2016 (incluindo o Server Core, mas não o Nano Server) e o Windows Server 2019\* (incluindo o Server Core, mas não o Nano Server), conforme mostrado na tabela a seguir.

| Versão do sistema operacional   | Servidor com Experiência Desktop | Server Core | Nano Server    |
| -------------------------- | ------------------------------ | ----------- | -------------- |
| Windows Server 2008 R2 SP1 | &#10004;                       | &#10060;    | Não aplicável |
| Windows Server 2012        | &#10004;                       | &#10004;    | Não aplicável |
| Windows Server 2012 R2     | &#10004;                       | &#10004;    | Não aplicável |
| Windows Server 2016        | &#10004;                       | &#10004;    | &#10060;       |
| Windows Server 2019\*      | &#10004;                       | &#10004;    | &#10060;       |

\* Requer [KB4487044](https://support.microsoft.com/help/4487044/windows-10-update-kb4487044). Os sensores instalados no Server 2019 sem essa atualização serão interrompidos automaticamente.

O controlador de domínio pode ser um RODC (controlador de domínio somente leitura).

Para seus controladores de domínio se comunicarem com o serviço de nuvem, você deve abrir a porta 443 em seus firewalls e proxies para \*.atp.azure.com.

Durante a instalação, se o .NET Framework 4.7 ou posterior não estiver instalado, o .NET Framework 4.7 será instalado e poderá exigir uma reinicialização do controlador de domínio. Também poderá ser necessária uma reinicialização se ela já estiver pendente.

> [!NOTE]
> São necessários no mínimo 5 GB de espaço. Recomenda-se 10 GB. Isso inclui o espaço necessário para os binários do [!INCLUDE [Product short](includes/product-short.md)], os logs do [!INCLUDE [Product short](includes/product-short.md)] e os logs de desempenho.

### <a name="server-specifications"></a>Especificações do servidor

O sensor do [!INCLUDE [Product short](includes/product-short.md)] exige, no mínimo, dois núcleos e 6 GB de RAM instalados no controlador de domínio.
Para obter um desempenho ideal, defina a **Opção de Energia** do computador que executa o sensor do [!INCLUDE [Product short](includes/product-short.md)] como **Alto Desempenho**.

Os sensores do [!INCLUDE [Product short](includes/product-short.md)] podem ser implantados em controladores de domínio de vários tamanhos e cargas, dependendo da quantidade de recursos instalados e da quantidade de tráfego de rede entre os controladores de domínio.

Nos sistemas operacionais Windows 2008 R2 e 2012, não há suporte para o sensor do [!INCLUDE [Product short](includes/product-short.md)] em um modo [Grupo de multiprocessadores](/windows/win32/procthread/processor-groups). Para obter mais informações sobre o modo de grupo de multiprocessadores,confira [solução de problemas](troubleshooting-known-issues.md#multi-processor-group-mode).

>[!NOTE]
> Durante a execução como uma máquina virtual, memória dinâmica ou qualquer outra memória, não há suporte para o recurso de inchamento.

Para obter mais informações sobre os requisitos de hardware do sensor do [!INCLUDE [Product short](includes/product-short.md)], confira [Planejamento da capacidade do [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md).

### <a name="time-synchronization"></a>Sincronização da hora

Os servidores e controladores de domínio nos quais o sensor é instalado devem ter a hora sincronizada em um espaço de cinco minutos entre si.

### <a name="network-adapters"></a>Adaptadores de rede

O sensor do [!INCLUDE [Product short](includes/product-short.md)] monitora o tráfego local em todos os adaptadores de rede do controlador de domínio.  
Após a implantação, use o portal do [!INCLUDE [Product short](includes/product-short.md)] para modificar quais adaptadores de rede são monitorados.

Não há suporte para o sensor em controles de domínio que executem o Windows 2008 R2 com o Broadcom Network Adapter Teaming habilitado.

### <a name="ports"></a>Portas

A seguinte tabela lista o mínimo de portas exigidas pelo sensor do [!INCLUDE [Product short](includes/product-short.md)]:

|Protocolo|Transport|Porta|De|Para|
|------------|-------------|--------|-----------|
|**Portas de Internet**|||||
|SSL (*.atp.azure.com)|TCP|443|Sensor do [!INCLUDE [Product short](includes/product-short.md)]|Serviço de nuvem do [!INCLUDE [Product short](includes/product-short.md)]|
|SSL (localhost)|TCP|444|Sensor do [!INCLUDE [Product short](includes/product-short.md)]|localhost|
|**Portas internas**|||||
|DNS|TCP e UDP|53|Sensor do [!INCLUDE [Product short](includes/product-short.md)]|Servidores DNS|
|Netlogon (SMB, CIFS, SAM-R)|TCP/UDP|445|Sensor do [!INCLUDE [Product short](includes/product-short.md)]|Todos os dispositivos na rede|
|RAIO|UDP|1813|RAIO|Sensor do [!INCLUDE [Product short](includes/product-short.md)]|
|**Portas NNR**\*|||||
|NTLM via RPC|TCP|Porta 135|[!INCLUDE [Product short](includes/product-short.md)]s|Todos os dispositivos na rede|
|NetBIOS|UDP|137|[!INCLUDE [Product short](includes/product-short.md)]s|Todos os dispositivos na rede|
|RDP|TCP|3389, apenas o primeiro pacote do Client hello|[!INCLUDE [Product short](includes/product-short.md)]s|Todos os dispositivos na rede|

\* Uma dessas portas é necessária, mas é recomendável abrir todas elas.

### <a name="windows-event-logs"></a>Log de eventos do Windows

A detecção do [!INCLUDE [Product short](includes/product-short.md)] depende de [logs de eventos específicos do Windows](configure-windows-event-collection.md#configure-event-collection) que o sensor analisa dos controladores de domínio. Para que os eventos corretos sejam auditados e incluídos no log de eventos do Windows, seus controladores de domínio exigem configurações precisas de política de auditoria avançada. Para saber mais sobre como configurar as políticas corretas, confira [Verificação avançada da política de auditoria](configure-windows-event-collection.md). Para [verificar se o evento 8004 do Windows foi auditado](configure-windows-event-collection.md#configure-audit-policies) conforme necessário pelo serviço, examine as [configurações de auditoria do NTLM](/archive/blogs/askds/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7).

> [!NOTE]
> Usando a conta de usuário do serviço de diretório, o sensor consulta pontos de extremidade em sua organização para administradores locais usando SAM-R (logon de rede) para criar o [gráfico de caminho de movimento lateral](use-case-lateral-movement-path.md). Para obter mais informações, consulte [Configurar permissões necessárias do SAM-R](install-step8-samr.md).

<a name="azure-atp-standalone-sensor-requirements"></a>

## <a name="product-short-standalone-sensor-requirements"></a>Requisitos do sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)]

Esta seção lista os requisitos do sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)].

> [!NOTE]
> Os sensores autônomos do [!INCLUDE [Product short](includes/product-short.md)] não dão suporte à coleção de entradas de log do ETW (Rastreamento de Eventos para Windows) que fornecem os dados para várias detecções. Para cobertura completa do seu ambiente, recomendamos implantar o sensor do [!INCLUDE [Product short](includes/product-short.md)].

### <a name="general"></a>Geral

O sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] dá suporte à instalação em um servidor que executa o Windows Server 2012 R2 ou o Windows Server 2016 (incluindo o Server Core).
O sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] pode ser instalado em um servidor que é membro de um domínio ou um grupo de trabalho.
O sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] pode ser usado para monitorar os controladores de domínio com o Nível funcional do domínio igual ao Windows 2003 e superior.

Para que o sensor autônomo se comunique com o serviço de nuvem, a porta 443 deve estar aberta nos firewalls e proxies para *.atp.azure.com.

Para obter informações sobre como usar máquinas virtuais com o sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)], confira [Configurar o espelhamento de porta](configure-port-mirroring.md).

> [!NOTE]
> São necessários no mínimo 5 GB de espaço. Recomenda-se 10 GB. Isso inclui o espaço necessário para os binários do [!INCLUDE [Product short](includes/product-short.md)], os logs do [!INCLUDE [Product short](includes/product-short.md)] e os logs de desempenho.

### <a name="server-specifications"></a>Especificações do servidor

Para obter um desempenho ideal, defina a **Opção de Energia** do computador que executa o sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] como **Alto Desempenho**.

Um sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] pode dar suporte ao monitoramento de vários controladores de domínio, dependendo da quantidade de tráfego de rede entre os controladores de domínio.

>[!NOTE]
> Durante a execução como uma máquina virtual, memória dinâmica ou qualquer outra memória, não há suporte para o recurso de inchamento.

Para obter mais informações sobre os requisitos de hardware do sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)], confira [Planejamento da capacidade do [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md).

### <a name="time-synchronization"></a>Sincronização da hora

Os servidores e controladores de domínio nos quais o sensor é instalado devem ter a hora sincronizada em um espaço de cinco minutos entre si.

### <a name="network-adapters"></a>Adaptadores de rede

O sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] exige, pelo menos, um Adaptador de gerenciamento e um Adaptador de captura:

- **Adaptador de gerenciamento** - usado para as comunicações em sua rede corporativa. O sensor usará esse adaptador para consultar se o DC está protegendo e realizando a resolução para contas de computador.

    Esse adaptador deve ser configurado com as seguintes definições:

    - Endereço IP estático, incluindo o gateway padrão

    - Servidores DNS preferenciais e alternativos

    - O **sufixo DNS desta conexão** deve ser o nome DNS do domínio para cada domínio sendo monitorado.

        ![Configure o sufixo DNS nas definições avançadas de TCP/IP](media/dns-suffix.png)

        > [!NOTE]
        > Se o sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] for um membro do domínio, isso poderá ser configurado automaticamente.

- **Adaptador de captura** - usado para capturar o tráfego dos controladores de domínio.

    > [!IMPORTANT]
    >
    > - Configure o espelhamento de porta do adaptador de captura como o destino do tráfego de rede do controlador de domínio. Para saber mais, confira [Configurar o espelhamento de porta](configure-port-mirroring.md). Normalmente, você precisa trabalhar com a equipe de virtualização ou de rede para configurar o espelhamento de porta.
    > - Configure um endereço IP não roteável estático (com máscara /32) para seu ambiente sem um gateway de sensor padrão e sem endereço do servidor DNS. Por exemplo, 10.10.0.10/32. Isso assegura que o adaptador da rede de captura poderá capturar a quantidade máxima de tráfego e que o adaptador da rede de gerenciamento será usado para enviar e receber o tráfego de rede solicitado.

### <a name="ports"></a>Portas

A seguinte tabela lista o mínimo de portas que o sensor autônomo do [!INCLUDE [Product short](includes/product-short.md)] exige que estejam configuradas no adaptador de gerenciamento:

|Protocolo|Transport|Porta|De|Para|
|------------|-------------|--------|-----------|
|**Portas de Internet**||||
|SSL (*.atp.azure.com)|TCP|443|Sensor do [!INCLUDE [Product short](includes/product-short.md)]|Serviço de nuvem do [!INCLUDE [Product short](includes/product-short.md)]|
|SSL (localhost)|TCP|444|Sensor do [!INCLUDE [Product short](includes/product-short.md)]|localhost|
|**Portas internas**||||
|LDAP|TCP e UDP|389|Sensor do [!INCLUDE [Product short](includes/product-short.md)]|Controladores de domínio|
|LDAP seguro (LDAPS)|TCP|636|Sensor do [!INCLUDE [Product short](includes/product-short.md)]|Controladores de domínio|
|LDAP para o Catálogo Global|TCP|3268|Sensor do [!INCLUDE [Product short](includes/product-short.md)]|Controladores de domínio|
|LDAPS para o Catálogo Global|TCP|3269|Sensor do [!INCLUDE [Product short](includes/product-short.md)]|Controladores de domínio|
|Kerberos|TCP e UDP|88|Sensor do [!INCLUDE [Product short](includes/product-short.md)]|Controladores de domínio|
|Netlogon (SMB, CIFS, SAM-R)|TCP e UDP|445|Sensor do [!INCLUDE [Product short](includes/product-short.md)]|Todos os dispositivos na rede|
|Tempo do Windows|UDP|123|Sensor do [!INCLUDE [Product short](includes/product-short.md)]|Controladores de domínio|
|DNS|TCP e UDP|53|Sensor do [!INCLUDE [Product short](includes/product-short.md)]|Servidores DNS|
|Syslog (opcional)|TCP/UDP|514, dependendo da configuração|Servidor SIEM|Sensor do [!INCLUDE [Product short](includes/product-short.md)]|
|RAIO|UDP|1813|RAIO|Sensor do [!INCLUDE [Product short](includes/product-short.md)]|
|**Portas NNR** \*|||||
|NTLM via RPC|TCP|135|[!INCLUDE [Product short](includes/product-short.md)]s|Todos os dispositivos na rede|
|NetBIOS|UDP|137|[!INCLUDE [Product short](includes/product-short.md)]s|Todos os dispositivos na rede|
|RDP|TCP|3389, apenas o primeiro pacote do Client hello|[!INCLUDE [Product short](includes/product-short.md)]s|Todos os dispositivos na rede|

\* Uma dessas portas é necessária, mas é recomendável abrir todas elas.

> [!NOTE]
>
> - Usando a conta de usuário do serviço de diretório, o sensor consulta pontos de extremidade em sua organização para administradores locais usando SAM-R (logon de rede) para criar o [gráfico de caminho de movimento lateral](use-case-lateral-movement-path.md). Para obter mais informações, consulte [Configurar permissões necessárias do SAM-R](install-step8-samr.md).

## <a name="see-also"></a>Consulte Também

- [Ferramenta de dimensionamento do [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/aatpsizingtool)
- [Arquitetura do [!INCLUDE [Product short](includes/product-short.md)]](architecture.md)
- [Instalar o [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [NNR (resolução de nomes de rede)](nnr-policy.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
