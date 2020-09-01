---
title: Pré-requisitos da Proteção Avançada contra Ameaças do Azure
description: Descreve os requisitos para uma implantação bem-sucedida do Azure ATP em seu ambiente
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 07/27/2020
ms.topic: overview
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 62c99622-2fe9-4035-9839-38fec0a353da
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e0c6e9826b734e9e94e787ba62cd782eb5ef8dd6
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88956628"
---
# <a name="azure-atp-prerequisites"></a>Pré-requisitos do ATP do Azure

Este artigo descreve os requisitos para uma implantação bem-sucedida do Azure ATP em seu ambiente.

>[!NOTE]
> Para obter informações sobre como planejar a capacidade e os recursos, consulte [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md).

O ATP do Azure é composto pelo seu serviço de nuvem, que consiste no portal e no sensor do ATP do Azure. Para obter mais informações sobre cada componente do Azure ATP, confira [Arquitetura do Azure ATP](atp-architecture.md).

A ATP do Azure protege seus usuários locais do Active Directory e/ou os usuários sincronizados com o Azure Active Directory. Para proteger um ambiente composto apenas por usuários do AAD, confira a [Proteção de Identidade do AAD](/azure/active-directory/identity-protection/overview).

Para criar sua instância do Azure ATP, será necessário um locatário do AAD com pelo menos um administrador da segurança/global. Cada instância do Azure ATP dá suporte a vários limites de floresta do Active Directory e dá suporte ao FFL (Nível funcional da floresta) do Windows 2003 e posteriores.

Este guia de pré-requisitos é dividido nas seguintes seções para garantir que você tem tudo de que precisa para implantar o Azure ATP com êxito.

[Antes de começar](#before-you-start): Lista as informações a serem reunidas e as contas e entidades de rede de que você precisará antes de iniciar a instalação.

[Portal do ATP do Azure](#azure-atp-portal-requirements): Descreve os requisitos do navegador do portal do ATP do Azure.

[Sensor do ATP do Azure](#azure-atp-sensor-requirements): Lista os requisitos de hardware e software do sensor do ATP do Azure.

[Sensor autônomo do ATP do Azure](#azure-atp-standalone-sensor-requirements): O Sensor autônomo do ATP do Azure é instalado em um servidor dedicado e requer a configuração do espelhamento de porta do controlador de domínio para receber o tráfego de rede.

> [!NOTE]
> Os sensores autônomos do ATP do Azure não dão suporte à coleção de entradas de log do ETW (Rastreamento de Eventos para Windows) que fornecem os dados para várias detecções. Para cobertura completa do seu ambiente, é recomendável implantar o sensor do ATP do Azure.

## <a name="before-you-start"></a>Antes de começar

Esta seção mostra as informações que você deve obter, bem como as contas e informações sobre entidades de rede que deve ter antes de iniciar a instalação do ATP do Azure.

- Adquira uma licença do EMS E5 (Enterprise Mobility + Security 5) diretamente usando o [portal do Microsoft 365](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing) ou use o modelo de licenciamento do CSP (Parceiro de Soluções na Nuvem). As licenças autônomas do ATP do Azure também estão disponíveis.

- Verifique se os controladores de domínio nos quais você pretende instalar sensores do Azure ATP têm conectividade com a Internet para o Serviço de Nuvem do Azure ATP. O sensor do ATP do Azure tem suporte para o uso de um proxy. Para obter mais informações sobre a configuração de proxy, confira [Configuring a proxy for Azure ATP](configure-proxy.md) (Configurando um proxy para o Azure ATP).

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
    > - Se você tiver vários sensores, alguns executando o Windows Server 2008 e outros executando o Windows Server 2012 ou posterior, além da recomendação para usar uma conta **gMSA**, você também deverá usar pelo menos uma conta de usuário do AD **padrão**.
    > - Se você tiver definido ACLs personalizadas em várias Unidades Organizacionais (UO) em seu domínio, verifique se o usuário selecionado tem permissões de leitura para essas UOs.

- Se executar o Wireshark no sensor autônomo do ATP do Azure, reinicie o serviço de sensor da Proteção Avançada contra Ameaças do Azure quando interromper a captura do Wireshark. Se não reiniciar o serviço de sensor, o sensor interromperá a captura de tráfego.

- Se tentar instalar o sensor do ATP do Azure em um computador configurado com um adaptador de Agrupamento NIC, você receberá um erro de instalação. Se desejar instalar o sensor do Azure ATP em um computador configurado com Agrupamento NIC, confira [Problemas do Agrupamento NIC do Sensor do Azure ATP](troubleshooting-atp-known-issues.md#nic-teaming).

- Recomendação de contêiner de **Objetos Excluídos**: O usuário deve ter permissões de somente leitura no contêiner de Objetos Excluídos. Permissões somente leitura neste contêiner permitem que a ATP do Azure detecte exclusões de usuários do seu Active Directory. Para obter informações sobre como configurar permissões somente leitura no contêiner Objetos Excluídos, confira a seção **Como alterar permissões em um contêiner de objetos excluídos** do artigo [Exibir ou definir permissões em um objeto do directory](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc816824(v=ws.10)).

- **Honeytoken** opcional: Uma conta de usuário que não tem nenhuma atividade de rede. Essa conta está configurada como um usuário Honeytoken do Azure ATP. Para obter mais informações sobre como usar Honeytokens, confira [Configurar exclusões e usuário do Honeytoken](install-atp-step7.md).

- Opcional: Ao implantar o sensor autônomo, é necessário encaminhar [eventos do Windows](configure-windows-event-collection.md#configure-event-collection) para a ATP do Azure para aprimorar ainda mais as detecções baseadas na autenticação da ATP do Azure, as adições a grupos confidenciais e as detecções de criação de serviço suspeito.  O sensor do Azure ATP recebe esses eventos automaticamente. No sensor autônomo do Azure ATP, esses eventos podem ser recebidos do SIEM ou definindo o Encaminhamento de Eventos do Windows no controlador de domínio. Os eventos coletados fornecem ao Azure ATP informações adicionais que não estão disponíveis por meio do tráfego de rede do controlador de domínio.

## <a name="azure-atp-portal-requirements"></a>Requisitos do portal do Azure ATP

O acesso ao portal do Azure ATP ocorre por meio de um navegador que dá suporte aos seguintes navegadores e configurações:

- Um navegador compatível com TLS 1.2, como:
  - Microsoft Edge
  - Internet Explorer versão 11 e posterior
  - Google Chrome 30.0 e posterior
- Resolução de largura mínima da tela de 1.700 pixels
- Firewall/proxy aberto – para se comunicar com o serviço de nuvem do ATP do Azure, você deve abrir a porta 443 de *.atp.azure.com no firewall/proxy.

    > [!NOTE]
    > Você também pode usar nossa marca de serviço do Azure (**AzureAdvancedThreatProtection**) para habilitar o acesso ao ATP do Azure. Para obter mais informações sobre marcas de serviço, confira [Marcas de serviço de rede virtual](/azure/virtual-network/service-tags-overview) ou [baixe o arquivo de marcas de serviço](https://www.microsoft.com/download/details.aspx?id=56519).

 ![diagrama da arquitetura do Azure ATP](media/azure-atp-architecture.png)

> [!NOTE]
> Por padrão, a ATP do Azure dá suporte a até 200 sensores. Para instalar mais sensores, fale com o suporte da ATP do Azure.

## <a name="azure-atp-network-name-resolution-nnr-requirements"></a>Requisitos da NNR (resolução de nome de rede) da ATP do Azure

A NNR (resolução de nomes de rede) é um componente principal da funcionalidade da ATP do Azure. Para resolver os endereços IP para nomes do computador, os sensores do ATP do Azure pesquisam os endereços IP usando os seguintes métodos:

- NTLM sobre RPC (porta TCP 135)
- NetBIOS (porta UDP 137)
- RDP (porta TCP 3389): apenas o primeiro pacote do **Client hello**
- Consultas ao servidor DNS usando a pesquisa de DNS reverso do endereço IP (UDP 53)

Para que os três primeiros métodos funcionem, as portas relevantes devem ser abertas para entrada dos sensores da ATP do Azure para dispositivos na rede. Saiba mais sobre a ATP do Azure e a NNR em [Política da NNR da ATP do Azure](atp-nnr-policy.md).

Recomendamos o uso de todos os métodos para obter os melhores resultados. Se isso não for possível, você deverá usar o método de pesquisa de DNS e pelo menos um dos outros métodos.

## <a name="azure-atp-sensor-requirements"></a>Requisitos do sensor do Azure ATP

Esta seção lista os requisitos do sensor do Azure ATP.

### <a name="general"></a>Geral

> [!NOTE]
> Certifique-se de que o [KB4487044](https://support.microsoft.com/help/4487044/windows-10-update-kb4487044) esteja instalado ao usar o Server 2019. Os sensores da ATP do Azure já instalados nos servidores 2019 sem essa atualização serão interrompidos automaticamente.

O sensor da ATP do Azure dá suporte à instalação em um controlador de domínio que executa o Windows Server 2008 R2 SP1 (sem incluir o Server Core), o Windows Server 2012, o Windows Server 2012 R2, o Windows Server 2016 (incluindo o Windows Server Core, mas não o Windows Nano Server) e o Windows Server 2019 (incluindo o Windows Core, mas não o Windows Nano Server).

O controlador de domínio pode ser um RODC (controlador de domínio somente leitura).

Para seus controladores de domínio se comunicarem com o serviço de nuvem, você deve abrir a porta 443 em seus firewalls e proxies para *. atp.azure.com.

Durante a instalação, se o .NET Framework 4.7 ou posterior não estiver instalado, o .NET Framework 4.7 será instalado e poderá exigir uma reinicialização do controlador de domínio. Também poderá ser necessária uma reinicialização se ela já estiver pendente.

> [!NOTE]
> São necessários no mínimo 5 GB de espaço. Recomenda-se 10 GB. Isso inclui o espaço necessário para os binários do Azure ATP, logs do Azure ATP e logs de desempenho.

### <a name="server-specifications"></a>Especificações do servidor

O sensor do ATP do Azure requer um mínimo de dois núcleos e 6 GB de RAM instalados no controlador de domínio.
Para ter desempenho ideal, defina a **Opção de Energia** do computador que executa o sensor do ATP do Azure como **Alto Desempenho**.

É possível implantar o sensor do ATP do Azure em controladores de domínio de vários tamanhos e cargas, dependendo da quantidade de recursos instalados e da quantidade de tráfego de rede dos controladores de domínio.

Para os sistemas operacionais Windows 2008R2 e 2012, o sensor do ATP do Azure não tem suporte em um modo [Grupo de multiprocessadores](/windows/win32/procthread/processor-groups). Para obter mais informações sobre o modo de grupo de multiprocessadores,confira [solução de problemas](troubleshooting-atp-known-issues.md#multi-processor-group-mode).

>[!NOTE]
> Durante a execução como uma máquina virtual, memória dinâmica ou qualquer outra memória, não há suporte para o recurso de inchamento.

Para obter mais informações sobre os requisitos de hardware do sensor do Azure ATP, consulte [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md).

### <a name="time-synchronization"></a>Sincronização da hora

Os servidores e controladores de domínio nos quais o sensor é instalado devem ter a hora sincronizada em um espaço de cinco minutos entre si.

### <a name="network-adapters"></a>Adaptadores de rede

O sensor do Azure ATP monitora o tráfego local em todos os adaptadores de rede do controlador de domínio.  
Após a implantação, use o portal do ATP do Azure para modificar quais adaptadores de rede são monitorados.

Não há suporte para o sensor em controles de domínio que executem o Windows 2008 R2 com o Broadcom Network Adapter Teaming habilitado.

### <a name="ports"></a>Portas

A tabela abaixo lista o mínimo de portas que o sensor do Azure ATP exige:

|Protocolo|Transport|Porta|De|Para|Direção|
|------------|-------------|--------|-----------|-------------|
|**Portas de Internet**||||||
|SSL (*.atp.azure.com)|TCP|443|Sensor do Azure ATP|Serviço de nuvem do Azure ATP|Saída|
|SSL (localhost)|TCP|444|Sensor do Azure ATP|localhost|Ambos|
|**Portas internas**||||||
|DNS|TCP e UDP|53|Sensor do Azure ATP|Servidores DNS|Saída|
|Netlogon (SMB, CIFS, SAM-R)|TCP/UDP|445|Sensor do Azure ATP|Todos os dispositivos na rede|Saída|
|Syslog (opcional)|TCP/UDP|514, dependendo da configuração|Servidor SIEM|Sensor do Azure ATP|Entrada|
|RAIO|UDP|1813|RAIO|Sensor do Azure ATP|Entrada|
|**Portas NNR**\*||||||
|NTLM via RPC|TCP|Porta 135|Sensores ATP|Todos os dispositivos na rede|Entrada|
|NetBIOS|UDP|137|Sensores ATP|Todos os dispositivos na rede|Entrada|
|RDP|TCP|3389, apenas o primeiro pacote do Client hello|Sensores ATP|Todos os dispositivos na rede|Entrada|

\* Uma dessas portas é necessária, mas é recomendável abrir todas elas.

### <a name="windows-event-logs"></a>Log de eventos do Windows

A detecção da ATP do Azure depende de [logs de eventos específicos do Windows](configure-windows-event-collection.md#configure-event-collection) que o sensor analisa dos controladores de domínio. Para que os eventos corretos sejam auditados e incluídos no log de eventos do Windows, seus controladores de domínio exigem configurações precisas de política de auditoria avançada. Para saber mais sobre como configurar as políticas corretas, confira [Verificação avançada da política de auditoria](configure-windows-event-collection.md). Para [verificar se o evento 8004 do Windows foi auditado](configure-windows-event-collection.md#configure-audit-policies) conforme necessário pelo serviço, examine as [configurações de auditoria do NTLM](/archive/blogs/askds/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7).

> [!NOTE]
>
> - Usando a conta de usuário do serviço de diretório, o sensor consulta pontos de extremidade em sua organização para administradores locais usando SAM-R (logon de rede) para criar o [gráfico de caminho de movimento lateral](use-case-lateral-movement-path.md). Para obter mais informações, consulte [Configurar permissões necessárias do SAM-R](install-atp-step8-samr.md).

## <a name="azure-atp-standalone-sensor-requirements"></a>Requisitos do sensor autônomo do Azure ATP

Esta seção lista os requisitos do sensor autônomo do Azure ATP.

> [!NOTE]
> Os sensores autônomos do ATP do Azure não dão suporte à coleção de entradas de log do ETW (Rastreamento de Eventos para Windows) que fornecem os dados para várias detecções. Para cobertura completa do seu ambiente, é recomendável implantar o sensor do ATP do Azure.

### <a name="general"></a>Geral

O sensor autônomo do Azure ATP dá suporte à instalação em um servidor executando o Windows Server 2012 R2 ou o Windows Server 2016 (incluindo o Server Core).
A sensor autônomo do Azure ATP pode ser instalado em um servidor que é membro de um domínio ou grupo de trabalho.
O sensor autônomo do Azure ATP pode ser usado para monitorar Controladores de domínio com o Nível de domínio funcional do Windows 2003 e posterior.

Para que o sensor autônomo se comunique com o serviço de nuvem, a porta 443 deve estar aberta nos firewalls e proxies para *.atp.azure.com.

Para obter informações sobre como usar máquinas virtuais com o sensor autônomo do Azure ATP, consulte [Configurar o espelhamento de porta](configure-port-mirroring.md).

> [!NOTE]
> São necessários no mínimo 5 GB de espaço. Recomenda-se 10 GB. Isso inclui o espaço necessário para os binários do Azure ATP, logs do Azure ATP e logs de desempenho.

### <a name="server-specifications"></a>Especificações do servidor

Para ter desempenho ideal, defina a **Opção de Energia** do computador que executa o sensor autônomo do ATP do Azure como **Alto Desempenho**.<br>
Um sensor autônomo do ATP do Azure pode ter suporte para monitoramento de vários controladores de domínio, dependendo da quantidade de tráfego de rede dos controladores de domínio.

>[!NOTE]
> Durante a execução como uma máquina virtual, memória dinâmica ou qualquer outra memória, não há suporte para o recurso de inchamento.

Para obter mais informações sobre os requisitos de hardware do sensor autônomo do Azure ATP, consulte [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md).

### <a name="time-synchronization"></a>Sincronização da hora

Os servidores e controladores de domínio nos quais o sensor é instalado devem ter a hora sincronizada em um espaço de cinco minutos entre si.

### <a name="network-adapters"></a>Adaptadores de rede

O sensor autônomo do Azure ATP requer pelo menos um adaptador de gerenciamento e pelo menos um adaptador de captura:

- **Adaptador de gerenciamento** - usado para as comunicações em sua rede corporativa. O sensor usará esse adaptador para consultar se o DC está protegendo e realizando a resolução para contas de computador. <br>Esse adaptador deve ser configurado com as seguintes definições:

    - Endereço IP estático, incluindo o gateway padrão

    - Servidores DNS preferenciais e alternativos

    - O **sufixo DNS desta conexão** deve ser o nome DNS do domínio para cada domínio sendo monitorado.

        ![Configure o sufixo DNS nas definições avançadas de TCP/IP](media/ATP-DNS-Suffix.png)

        > [!NOTE]
        > Se o sensor autônomo do Azure ATP for um membro do domínio, isto poderá ser configurado automaticamente.

- **Adaptador de captura** - usado para capturar o tráfego dos controladores de domínio.

    > [!IMPORTANT]
    >
    > - Configure o espelhamento de porta do adaptador de captura como o destino do tráfego de rede do controlador de domínio. Para saber mais, confira [Configurar o espelhamento de porta](configure-port-mirroring.md). Normalmente, você precisa trabalhar com a equipe de virtualização ou de rede para configurar o espelhamento de porta.
    > - Configure um endereço IP não roteável estático (com máscara /32) para seu ambiente sem um gateway de sensor padrão e sem endereço do servidor DNS. Por exemplo, 10.10.0.10/32. Isso assegura que o adaptador da rede de captura poderá capturar a quantidade máxima de tráfego e que o adaptador da rede de gerenciamento será usado para enviar e receber o tráfego de rede solicitado.

### <a name="ports"></a>Portas

A tabela abaixo lista as portas mínimas que o sensor autônomo do Azure ATP requer que estejam configuradas no adaptador de gerenciamento:

|Protocolo|Transport|Porta|De|Para|Direção|
|------------|-------------|--------|-----------|-------------|
|**Portas de Internet**|||||
|SSL (*.atp.azure.com)|TCP|443|Sensor do ATP do Azure|Serviço de nuvem do Azure ATP|Saída|
|**Portas internas**|||||
|LDAP|TCP e UDP|389|Sensor do ATP do Azure|Controladores de domínio|Saída|
|LDAP seguro (LDAPS)|TCP|636|Sensor do ATP do Azure|Controladores de domínio|Saída|
|LDAP para o Catálogo Global|TCP|3268|Sensor do ATP do Azure|Controladores de domínio|Saída|
|LDAPS para o Catálogo Global|TCP|3269|Sensor do ATP do Azure|Controladores de domínio|Saída|
|Kerberos|TCP e UDP|88|Sensor do ATP do Azure|Controladores de domínio|Saída|
|Netlogon (SMB, CIFS, SAM-R)|TCP e UDP|445|Sensor do ATP do Azure|Todos os dispositivos na rede|Saída|
|Tempo do Windows|UDP|123|Sensor do ATP do Azure|Controladores de domínio|Saída|
|DNS|TCP e UDP|53|Sensor do ATP do Azure|Servidores DNS|Saída|
|Syslog (opcional)|TCP/UDP|514, dependendo da configuração|Servidor SIEM|Sensor do ATP do Azure|Entrada|
|RAIO|UDP|1813|RAIO|Sensor do Azure ATP|Entrada|
|**Portas NNR** \*||||||
|NTLM via RPC|TCP|135|Sensores ATP|Todos os dispositivos na rede|Entrada|
|NetBIOS|UDP|137|Sensores ATP|Todos os dispositivos na rede|Entrada|
|RDP|TCP|3389, apenas o primeiro pacote do Client hello|Sensores ATP|Todos os dispositivos na rede|Entrada|

\* Uma dessas portas é necessária, mas é recomendável abrir todas elas.

> [!NOTE]
>
> - Usando a conta de usuário do serviço de diretório, o sensor consulta pontos de extremidade em sua organização para administradores locais usando SAM-R (logon de rede) para criar o [gráfico de caminho de movimento lateral](use-case-lateral-movement-path.md). Para obter mais informações, consulte [Configurar permissões necessárias do SAM-R](install-atp-step8-samr.md).

## <a name="see-also"></a>Consulte Também

- [Ferramenta de dimensionamento do Azure ATP](https://aka.ms/aatpsizingtool)
- [Arquitetura do Azure ATP](atp-architecture.md)
- [Instalar o Azure ATP](install-atp-step1.md)
- [NNR (resolução de nomes de rede)](atp-nnr-policy.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)