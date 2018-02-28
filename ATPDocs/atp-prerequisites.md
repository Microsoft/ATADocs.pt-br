---
title: "Pré-requisitos da Proteção Avançada contra Ameaças do Azure | Microsoft Docs"
description: "Descreve os requisitos para uma implantação bem-sucedida do Azure ATP em seu ambiente"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 62c99622-2fe9-4035-9839-38fec0a353da
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 819eeb73c57e7b1de5e7e5e837aa2d6db2e0848d
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2018
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*



# <a name="azure-atp-prerequisites"></a>Pré-requisitos do Azure ATP
Este artigo descreve os requisitos para uma implantação bem-sucedida do Azure ATP em seu ambiente.

>[!NOTE]
> Para obter informações sobre como planejar a capacidade e os recursos, consulte [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md).


O Azure ATP é composto pelo serviço de nuvem do Azure ATP, que consiste no portal de gerenciamento de espaço de trabalho e em um portal de espaço de trabalho, pelo sensor autônomo do Azure ATO e/ou pelo sensor do Azure ATP. Para obter mais informações sobre os componentes do Azure ATP, consulte [Arquitetura do Azure ATP](atp-architecture.md).

Cada espaço de trabalho do Azure ATP dá suporte a um limite de floresta do Active Directory e dá suporte ao FFL (Nível funcional da floresta) do Windows 2003 e posteriores. Para implantações com várias florestas, um espaço de trabalho separado do Azure ATP é necessário para cada floresta.


[Antes de começar](#before-you-start): esta seção lista as informações que você deve obter e as contas e entidades de rede que você deve ter antes de começar a instalação do Azure ATP.

[Portal de gerenciamento de espaço de trabalho do Azure ATP](#azure-atp-workspace-management-portal-and-workspace-portal-requirements): esta seção descreve os requisitos de navegador do portal de gerenciamento de espaço de trabalho.

[Portal de espaço de trabalho do Azure ATP](#azure-atp-workspace-management-portal-and-workspace-portal-requirements): esta seção descreve os requisitos de navegador para executar o portal de espaço de trabalho do Azure ATP.

[Sensor autônomo do Azure ATP](#azure-atp-sensor-requirements): esta seção lista os requisitos de software e hardware do sensor autônomo do Azure ATP, bem como as configurações que você precisa definir nos servidores do sensor autônomo do Azure ATP.

[Sensor do Azure ATP](#azure-atp-lightweight-sensor-requirements): esta seção lista os requisitos de hardware e software do sensor do Azure ATP.

![diagrama da arquitetura do Azure ATP](media/ATP-architecture-topology.png)

## <a name="before-you-start"></a>Antes de começar
Esta seção lista as informações que você deve obter e as contas e entidades de rede que deve ter antes de iniciar a instalação do Azure ATP.


-   Uma conta de usuário e senha **local** do Azure AD com acesso de leitura para todos os objetos nos domínios monitorados.

    > [!NOTE]
    > Se você tiver definido ACLs personalizadas em várias Unidades Organizacionais (UO) em seu domínio, verifique se o usuário selecionado tem permissões de leitura para essas UOs.

-   Se executar o Wireshark no sensor autônomo do Azure ATP, você precisará reiniciar o serviço de sensor da Proteção Avançada contra Ameaças do Azure após parar a captura do Wireshark. Caso contrário, o sensor para de capturar o tráfego.

- Se tentar instalar o sensor do ATP em um computador configurado com um adaptador de agrupamento NIC, você receberá um erro de instalação. Se quiser instalar o sensor do ATP em um computador configurado com agrupamento NIC, entre em contato com seu representante de suporte do Azure ATP.

-    Recomendado: o usuário deve ter permissões de leitura somente no contêiner Objetos Excluídos. Isso permite que o Azure ATP detecte a exclusão em massa de objetos no domínio. Para saber mais sobre como configurar permissões de somente leitura no contêiner Objetos Excluídos, confira a seção **Alterar permissões em um contêiner de objetos excluídos** no artigo [Exibir ou definir permissões em um Objeto de Diretório](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

-   Opcional: uma conta de usuário que não tem nenhuma atividade de rede. Essa conta está configurada como o usuário Honeytoken do Azure ATP. Para obter mais informações, consulte [Configurar exclusões e usuário Honeytoken](install-atp-step7.md).

-   Opcional: ao implantar o sensor autônomo, é necessário encaminhar os eventos do Windows 4776, 4732, 4733, 4728, 4729, 4756, 4757 e 7045 para o ATP para melhorar ainda mais as detecções de Pass-the-Hash, força bruta, modificação de grupos confidenciais, Honey Tokens e criação de serviços mal-intencionados do Azure ATP. No sensor do Azure ATP, esses eventos são recebidos automaticamente. No sensor autônomo do Azure ATP, esses eventos podem ser recebidos de seu SIEM ou definindo o Encaminhamento de Eventos do Windows no controlador de domínio. Os eventos coletados fornecem ao Azure ATP informações adicionais que não estão disponíveis por meio do tráfego de rede do controlador de domínio.


## <a name="azure-atp-workspace-management-portal-and-workspace-portal-requirements"></a>Requisitos do portal de espaço de trabalho e do portal de gerenciamento de espaço de trabalho do Azure ATP
O acesso ao portal de espaço de trabalho do Azure ATP e ao portal de gerenciamento de espaço de trabalho do Azure ATP é feito por meio de um navegador, com suporte para os navegadores e configurações a seguir:
-   Microsoft Edge
-   Internet Explorer versão 10 e posterior
-   Google Chrome 4.0 e posterior
-   Resolução de largura mínima da tela de 1.700 pixels
-   Firewall/proxy aberto – para se comunicar com o serviço de nuvem do Azure ATP, você deve abrir: *. atp.azure.com porta 443 em seu firewall/proxy. 

## <a name="azure-atp-standalone-sensor-requirements"></a>Requisitos do sensor autônomo do Azure ATP
Esta seção lista os requisitos do sensor autônomo do Azure ATP.
### <a name="general"></a>Geral
O sensor autônomo do Azure ATP dá suporte à instalação em um servidor executando o Windows Server 2012 R2 ou o Windows Server 2016 (incluindo o Server Core).
A sensor autônomo do Azure ATP pode ser instalado em um servidor que é membro de um domínio ou grupo de trabalho.
O sensor autônomo do Azure ATP pode ser usado para monitorar Controladores de domínio com o Nível de domínio funcional do Windows 2003 e posterior.

Para seus controladores de domínio se comunicarem com o serviço de nuvem, você deve abrir a porta 443 em seus firewalls e proxies para *. atp.azure.com.


Para obter informações sobre como usar máquinas virtuais com o sensor autônomo do Azure ATP, consulte [Configurar o espelhamento de porta](configure-port-mirroring.md).

> [!NOTE]
> É necessário um mínimo de 5 GB de espaço e recomenda-se 10 GB. Isso inclui o espaço necessário para os binários do Azure ATP, logs do Azure ATP e logs de desempenho.

### <a name="server-specifications"></a>Especificações do servidor
Para ter um melhor desempenho, defina a **Opção de Energia** do sensor autônomo do Azure ATP como **Alto Desempenho**.<br>
Um sensor autônomo do Azure ATP pode dar suporte ao monitoramento de vários controladores de domínio, dependendo da quantidade de tráfego de rede dos controladores de domínio.

>[!NOTE] 
> Durante a execução como uma máquina virtual, memória dinâmica ou qualquer outra memória, não há suporte para o recurso de inchamento.

Para obter mais informações sobre os requisitos de hardware do sensor autônomo do Azure ATP, consulte [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md).

### <a name="time-synchronization"></a>Sincronização da hora

Os servidores e controladores de domínio nos quais o sensor é instalado devem ter a hora sincronizada em um espaço de cinco minutos entre si.


### <a name="network-adapters"></a>Adaptadores de rede
O sensor autônomo do Azure ATP requer pelo menos um adaptador de gerenciamento e pelo menos um adaptador de captura:

-   **Adaptador de gerenciamento** - usado para as comunicações em sua rede corporativa. Esse adaptador deve ser configurado com as seguintes definições:

    -   Endereço IP estático, incluindo o sensor padrão

    -   Servidores DNS preferenciais e alternativos

    -   O **sufixo DNS desta conexão** deve ser o nome DNS do domínio para cada domínio sendo monitorado.

        ![Configure o sufixo DNS nas definições avançadas de TCP/IP](media/ATP-DNS-Suffix.png)

        > [!NOTE]
        > Se o sensor autônomo do Azure ATP for um membro do domínio, isto poderá ser configurado automaticamente.

-   **Adaptador de captura** - usado para capturar o tráfego dos controladores de domínio.

    > [!IMPORTANT]
    > -   Configure o espelhamento de porta do adaptador de captura como o destino do tráfego de rede do controlador de domínio. Para saber mais, confira [Configurar o espelhamento de porta](configure-port-mirroring.md). Normalmente, você precisa trabalhar com a equipe de virtualização ou de rede para configurar o espelhamento de porta.
    > -   Configure um endereço IP não roteável estático para seu ambiente sem um sensor padrão e endereço do servidor DNS. Por exemplo, 1.1.1.1/32. Isso assegura que o adaptador da rede de captura poderá capturar a quantidade máxima de tráfego e que o adaptador da rede de gerenciamento será usado para enviar e receber o tráfego de rede solicitado.

### <a name="ports"></a>Portas
A tabela abaixo lista as portas mínimas que o sensor autônomo do Azure ATP requer que estejam configuradas no adaptador de gerenciamento:

|Protocolo|Transport|Porta|Para/De|Direção|
|------------|-------------|--------|-----------|-------------|
|LDAP|TCP e UDP|389|Controladores de domínio|Saída|
|LDAP seguro (LDAPS)|TCP|636|Controladores de domínio|Saída|
|LDAP para o Catálogo Global|TCP|3268|Controladores de domínio|Saída|
|LDAPS para o Catálogo Global|TCP|3269|Controladores de domínio|Saída|
|SSL (*.atp.azure.com)|TCP|443|Serviço de nuvem do Azure ATP|Saída|
|Kerberos|TCP e UDP|88|Controladores de domínio|Saída|
|Netlogon (SMB, CIFS, SAM-R)|TCP e UDP|445|Controladores de domínio|Saída|
|Tempo do Windows|UDP|123|Controladores de domínio|Saída|
|DNS|TCP e UDP|53|Servidores DNS|Saída|
|NTLM via RPC|TCP|135|Todos os dispositivos na rede|Saída|
|NetBIOS|UDP|137|Todos os dispositivos na rede|Saída|
|Syslog (opcional)|TCP/UDP|514, dependendo da configuração|Servidor SIEM|Entrada|
|RADIUS|UDDP|1813|RADIUS|Entrada|

> [!NOTE]
> - Usando a conta de usuário do serviço de diretório, o sensor consulta pontos de extremidade em sua organização para administradores locais usando SAM-R (logon de rede) para criar o [gráfico de caminho de movimento lateral](use-case-lateral-movement-path.md). Para obter mais informações, consulte [Configurar permissões necessárias do SAM-R](install-atp-step8-samr.md).
> - As seguintes portas precisam estar abertas para entrada em dispositivos na rede de sensores autônomos do Azure ATP:
>   -   NTLM via RPC (porta TCP 135) para fins de resolução
>   -   NetBIOS (porta UDP 137) para fins de resolução
>   -   Consultas de SAM-R (porta TCP/UDP 445) para fins de detecção


## <a name="azure-atp-sensor-requirements"></a>Requisitos do sensor do Azure ATP
Esta seção lista os requisitos do sensor do Azure ATP.
### <a name="general"></a>Geral
O sensor do Azure ATP dá suporte à instalação em um controlador de domínio que executa o Windows Server 2008 R2 SP1 (sem incluir o Server Core), o Windows Server 2012, o Windows Server 2012 R2, o Windows Server 2016 (incluindo o Core, mas não o Nano).

O controlador de domínio pode ser um RODC (controlador de domínio somente leitura).

Para seus controladores de domínio se comunicarem com o serviço de nuvem, você deve abrir a porta 443 em seus firewalls e proxies para *. atp.azure.com.

Durante a instalação, o .Net Framework 4.7 é instalado e pode causar uma reinicialização do controlador de domínio.


> [!NOTE]
> É necessário um mínimo de 5 GB de espaço e recomenda-se 10 GB. Isso inclui o espaço necessário para os binários do Azure ATP, logs do Azure ATP e logs de desempenho.

### <a name="server-specifications"></a>Especificações do servidor

O sensor do Azure ATP requer um mínimo de dois núcleos e 6 GB de RAM instalados no controlador de domínio.
Para ter um melhor desempenho, defina a **Opção de Energia** do sensor do Azure ATP como **Alto Desempenho**.
O sensor do Azure ATP pode ser implantado em controladores de domínio de vários tamanhos e cargas, dependendo da quantidade de tráfego de rede dos controladores de domínio e da quantidade de recursos instalados no controlador de domínio.

>[!NOTE] 
> Durante a execução como uma máquina virtual, memória dinâmica ou qualquer outra memória, não há suporte para o recurso de inchamento.

Para obter mais informações sobre os requisitos de hardware do sensor do Azure ATP, consulte [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md).

### <a name="time-synchronization"></a>Sincronização da hora

Os servidores e controladores de domínio nos quais o sensor é instalado devem ter a hora sincronizada em um espaço de cinco minutos entre si.

### <a name="network-adapters"></a>Adaptadores de rede

O sensor do Azure ATP monitora o tráfego local em todos os adaptadores de rede do controlador de domínio. <br>
Após a implantação, você pode usar o portal de espaço de trabalho do Azure ATP para modificar quais adaptadores de rede são monitorados.

Não há suporte para o sensor em controles de domínio que executem o Windows 2008 R2 com o Broadcom Network Adapter Teaming habilitado.

### <a name="ports"></a>Portas
A tabela abaixo lista o mínimo de portas que o sensor do Azure ATP exige:

|Protocolo|Transport|Porta|Para/De|Direção|
|------------|-------------|--------|-----------|-------------|
|SSL (*.atp.azure.com)|TCP|443|Serviço de nuvem do Azure ATP|Saída|
|DNS|TCP e UDP|53|Servidores DNS|Saída|
|NTLM via RPC|TCP|135|Todos os dispositivos na rede|Saída|
|Netlogon (SMB, CIFS, SAM-R)|TCP/UDP|445|Controladores de domínio|Saída|
|NetBIOS|UDP|137|Todos os dispositivos na rede|Saída|
|Syslog (opcional)|TCP/UDP|514, dependendo da configuração|Servidor SIEM|Entrada|
|RADIUS|UDDP|1813|RADIUS|Entrada|

> [!NOTE]
> - Usando a conta de usuário do serviço de diretório, o sensor consulta pontos de extremidade em sua organização para administradores locais usando SAM-R (logon de rede) para criar o [gráfico de caminho de movimento lateral](use-case-lateral-movement-path.md).
> - As seguintes portas precisam estar abertas para entrada em dispositivos na rede de sensores do Azure ATP:
>   -   NTLM via RPC (porta TCP 135) para fins de resolução
>   -   NetBIOS (porta UDP 137) para fins de resolução
>   -   Consultas de SAM-R (porta TCP/UDP 445) para fins de detecção





## <a name="see-also"></a>Consulte Também
- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/aatpsizingtool)
- [Arquitetura do Azure ATP](atp-architecture.md)
- [Instalar o ATP](install-atp-step1.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)

