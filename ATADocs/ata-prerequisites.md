---
title: Pré-requisitos do Advanced Threat Analytics | Microsoft Docs
description: Descreve os requisitos para uma implantação bem-sucedida do ATA em seu ambiente
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 9/27/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: a5f90544-1c70-4aff-8bf3-c59dd7abd687
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 008af6edacf27f5cc49f1a3e518f619a4829aae5
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56078078"
---
# <a name="ata-prerequisites"></a>Pré-requisitos do ATA

*Aplica-se a: Advanced Threat Analytics versão 1.9*

Este artigo descreve os requisitos para uma implantação bem-sucedida do ATA no seu ambiente.

> [!NOTE]
> Para obter informações sobre como planejar a capacidade e os recursos, confira [Planejamento de capacidade do ATA](ata-capacity-planning.md).


O ATA é composto pelo Centro do ATA, pelo Gateway do ATA e/ou o Gateway Lightweight do ATA. Para saber mais sobre os componentes do ATA, confira [Arquitetura do ATA](ata-architecture.md).

O Sistema do ATA funciona nos limites da floresta do active directory e oferece suporte a FFL (Nível funcional da floresta) do Windows 2003 e superior.


[Antes de começar](#before-you-start): Esta seção lista as informações que você deve obter, as contas e entidades de rede que você deve ter antes de iniciar a instalação do ATA.

[ATA Center](#ata-center-requirements): esta seção lista o hardware do ATA Center, os requisitos de software e as configurações que precisam ser definidas em seu servidor do ATA Center.

[ATA Gateway](#ata-gateway-requirements): esta seção lista o hardware do ATA Gateway, os requisitos de software e as configurações que precisam ser definidas em seu servidor do ATA Gateway.

[ATA Lightweight Gateway](#ata-lightweight-gateway-requirements): esta seção lista os requisitos de hardware e de software do ATA Lightweight Gateway.

[ATA Console](#ata-console): esta seção lista os requisitos do navegador para executar o ATA Console.

![Diagrama de arquitetura do ATA](media/ATA-architecture-topology.jpg)

## <a name="before-you-start"></a>Antes de começar
Esta seção mostra as informações que você deve obter, bem como as contas e entidades de rede que você deve ter antes de iniciar a instalação do ATA.


-   Conta de usuário e senha com acesso de leitura para todos os objetos nos domínios monitorados.

    > [!NOTE]
    > Se você tiver definido ACLs personalizadas em várias Unidades Organizacionais (UO) em seu domínio, verifique se o usuário selecionado tem permissões de leitura para essas UOs.

-   Não instale o Microsoft Message Analyzer em um Gateway ou um Gateway Lightweight do ATA. O driver do Message Analyzer conflita com os drivers do Gateway e Gateway Lightweight do ATA. Se você executar o Wireshark no Gateway do ATA, precisará reiniciar o Serviço de Gateway do Microsoft Advanced Threat Analytics após parar a captura do Wireshark. Caso contrário, o Gateway para de capturar o tráfego. Executar o Wireshark em um Gateway Lightweight do ATA não interfere no Gateway Lightweight do ATA.

-    Recomendado: O usuário deve ter permissões de somente leitura no contêiner de Objetos Excluídos. Isso permite que o ATA detecte a exclusão em massa de objetos no domínio. Para saber mais sobre como configurar permissões de somente leitura no contêiner Objetos Excluídos, confira a seção **Alterar permissões em um contêiner de objetos excluídos** no artigo [Exibir ou definir permissões em um Objeto de Diretório](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

-   Opcional: uma conta de usuário que não tem nenhuma atividade de rede. Essa conta está configurada como um usuário Honeytoken do ATA. Para configurar uma conta como um usuário Honeytoken, somente o nome de usuário é necessário. Para obter mais informações sobre configuração de Honeytoken, consulte [Configurar as exclusões de endereço IP e o usuário Honeytoken](install-ata-step7.md).

-   Opcional: além de coletar e analisar o tráfego de rede para e nos controladores de domínio, o ATA pode usar os eventos do Windows 4776, 4732, 4733, 4728, 4729, 4756 e 4757 para aprimorar ainda mais as detecções de Pass-the-Hash, Força Bruta, Modificação para grupos confidenciais e Honey Tokens do ATA. Esses eventos podem ser recebidos de seu SIEM ou definindo o Encaminhamento de Eventos do Windows no controlador de domínio. Os eventos coletados fornecem à ATA informações adicionais que não estão disponíveis por meio do tráfego de rede do controlador de domínio.


## <a name="ata-center-requirements"></a>Requisitos da Central de ATA
Esta seção lista os requisitos para a Central de ATA.
### <a name="general"></a>Geral
A Central de ATA dá suporte à instalação em um servidor executando o Windows Server 2012 R2 ou o Windows Server 2016. 

 > [!NOTE]
 > A Central do ATA não é compatível com o núcleo do Windows Server.

A Central de ATA pode ser instalada em um servidor que seja membro de um domínio ou grupo de trabalho.

Antes de instalar o ATA Center em execução no Windows 2012 R2, confirme se a seguinte atualização foi instalada: [KB2919355](https://support.microsoft.com/kb/2919355/).

Você pode verificar executando o seguinte cmdlet do Windows PowerShell: `[Get-HotFix -Id kb2919355]`.

A instalação do ATA Center como uma máquina virtual tem suporte. 

> [!NOTE] 
> Durante a execução como uma memória dinâmica da máquina virtual ou qualquer outra memória, não há suporte para o recurso de inchamento.

Se você executar a Central de ATA como uma máquina virtual, deverá finalizar o servidor antes de criar um novo ponto de verificação para evitar uma possível corrupção do banco de dados.

### <a name="server-specifications"></a>Especificações do servidor

Ao trabalhar em um servidor físico, o banco de dados do ATA precisa que você **desabilite** o NUMA (acesso não uniforme a memória) no BIOS. O sistema pode referir-se ao NUMA como Nó de Intercalação, caso em que você precisará **habilitar** a Intercalação de Nó para desabilitar o NUMA. Para obter mais informações, confira a documentação do BIOS.<br>

Para ter um melhor desempenho, defina a **Opção de Energia** do Centro do ATA como **Alto Desempenho**.<br>
O número de controladores de domínio que você está monitorando e a carga em cada um dos controladores de domínio determina as especificações de servidor necessárias. Para saber mais, confira [Planejamento de capacidade de ATA](ata-capacity-planning.md).


### <a name="time-synchronization"></a>Sincronização da hora

O servidor do Centro do ATA, os servidores do Gateway do ATA e os controladores de domínio devem ter a hora sincronizada no espaço de cinco minutos entre si.


### <a name="network-adapters"></a>Adaptadores de rede

Você deve ter o seguinte:
-   Pelo menos um adaptador de rede (se estiver usando o servidor físico no ambiente de VLAN, recomendamos o uso de dois adaptadores de rede)

-   Um endereço IP para comunicação entre o Centro do ATA e o Gateway do ATA, que é criptografado com o SSL na porta 443. (O serviço do ATA é associado a todos os endereços IP que o Centro do ATA tem na porta 443.)

### <a name="ports"></a>Portas
A tabela a seguir lista as portas mínimas que devem ser abertas para que a Central de ATA funcione corretamente.

|Protocolo|Transport|Porta|Para/De|Direção|
|------------|-------------|--------|-----------|-------------|
|**SSL** (Comunicações do ATA)|TCP|443|Gateway do ATA|Entrada|
|**HTTP** (opcional)|TCP|80|Rede da Empresa|Entrada|
|**HTTPS**|TCP|443|Rede da Empresa e Gateway de ATA|Entrada|
|**SMTP** (opcional)|TCP|25|Servidor SMTP|Saída|
|**SMTPS** (opcional)|TCP|465|Servidor SMTP|Saída|
|**Syslog** (opcional)|TCP/UPS/TLS (configurável)|514 (padrão)|Servidor syslog|Saída|
|**LDAP**|TCP e UDP|389|Controladores de domínio|Saída|
|**LDAPS** (opcional)|TCP|636|Controladores de domínio|Saída|
|**DNS**|TCP e UDP|53|Servidores DNS|Saída|
|**Kerberos** (opcional se ingressado no domínio)|TCP e UDP|88|Controladores de domínio|Saída|
|**Horário do Windows** (opcional se ingressado no domínio)|UDP|123|Controladores de domínio|Saída|

> [!NOTE]
> O LDAP é necessário para testar as credenciais serem usadas entre os Gateways do ATA e os controladores de domínio. Os testes executados do Centro do ATA para um controlador de domínio para testar a validade dessas credenciais, depois do qual o Gateway do ATA usa o LDAP como parte do processo de resolução normal.

### <a name="certificates"></a>Certificados

Para instalar e implantar o ATA rapidamente, você pode instalar os certificados autoassinados durante a instalação. Se você tiver optado por usar certificados autoassinados, após a implantação inicial será recomendável substituir os certificados autoassinados por certificados de uma Autoridade de Certificação interna a ser usada pelo Centro de ATA.


Verifique se que os Gateways de ATA e o Centro de ATA têm acesso ao ponto de distribuição de CRL. Se eles não tiverem acesso à Internet, siga [o procedimento para importar manualmente uma CRL](https://technet.microsoft.com/library/aa996972%28v=exchg.65%29.aspx), tendo o cuidado de instalar todos os pontos de distribuição de CRL de toda a cadeia.

O certificado deve ter:
-   Uma chave privada
-   Um tipo de provedor do CSP (Provedor de Serviços de Criptografia) ou KSP (Provedor de Armazenamento de Chaves)
-   Um comprimento de chave pública de 2048 bits
-   Um valor definido para os sinalizadores de uso KeyEncipherment e ServerAuthentication
-   O valor KeySpec (KeyNumber) de "KeyExchange" (AT\_KEYEXCHANGE). Observe que o valor de "Signature" (AT\_SIGNATURE) não tem suporte. 

Por exemplo, você pode usar os modelos padrão **servidor Web** ou **Computador**.

> [!WARNING]
> Não há suporte para o processo de renovação de um certificado existente. A única maneira de renovar um certificado é criando um novo certificado e configurando o ATA para usar o novo certificado.


> [!NOTE]
> - Se você pretende acessar o Console do ATA a partir de outros computadores, verifique se esses computadores confiam no certificado sendo usado pelo Centro do ATA, caso contrário, será exibida uma página de aviso informando que há um problema com o certificado de segurança do site antes de acessar a página de logon.
> - Começando com o ATA versão 1.8, os Gateways de ATA e Gateways Lightweight estão gerenciando seus próprios certificados e não precisam de nenhuma interação do administrador para gerenciá-los.

## <a name="ata-gateway-requirements"></a>Requisitos do Gateway do ATA
Esta seção lista os requisitos para o Gateway do ATA.
### <a name="general"></a>Geral
O Gateway do ATA permite instalação em um servidor executando o Windows Server 2012 R2 ou o Windows Server 2016 (incluindo o núcleo do servidor).
O Gateway do ATA pode ser instalado em um servidor que seja membro de um domínio ou grupo de trabalho.
O Gateway do ATA pode ser usado para monitorar Controladores de Domínio com o Nível de Domínio Funcional do Windows 2003 e posterior.

Antes de instalar o ATA Gateway em execução no Windows 2012 R2, confirme se a seguinte atualização foi instalada: [KB2919355](https://support.microsoft.com/kb/2919355/).

Você pode verificar executando o seguinte cmdlet do Windows PowerShell: `[Get-HotFix -Id kb2919355]`.


Para obter informações sobre como usar máquinas virtuais com o Gateway do ATA, confira [Configurar o espelhamento de porta](configure-port-mirroring.md).

> [!NOTE]
> É necessário um mínimo de 5 GB de espaço e recomenda-se 10 GB. Isso inclui o espaço necessário para os binários do ATA, os logs do ATA e os [logs de desempenho](troubleshooting-ata-using-perf-counters.md).

### <a name="server-specifications"></a>Especificações do servidor
Para ter um melhor desempenho, defina a **Opção de Energia** do Gateway de ATA para **Alto Desempenho**.<br>
Um Gateway do ATA pode dar suporte ao monitoramento de vários controladores de domínio, dependendo da quantidade de tráfego de rede para e a partir dos controladores de domínio.

> [!NOTE] 
> Durante a execução como uma memória dinâmica da máquina virtual ou qualquer outra memória, não há suporte para o recurso de inchamento.

Para saber mais sobre os requisitos de hardware do Gateway do ATA, confira [Planejamento de capacidade do ATA](ata-capacity-planning.md).

### <a name="time-synchronization"></a>Sincronização da hora
O servidor do Centro do ATA, os servidores do Gateway do ATA e os controladores de domínio devem ter a hora sincronizada no espaço de cinco minutos entre si.

### <a name="network-adapters"></a>Adaptadores de rede
O Gateway de ATA requer pelo menos um Adaptador de gerenciamento e pelo menos um adaptador de captura:

-   **Adaptador de gerenciamento** - usado para as comunicações em sua rede corporativa. Esse adaptador deve ser configurado com as seguintes definições:

    -   Endereço IP estático, incluindo o gateway padrão

    -   Servidores DNS preferenciais e alternativos

    -   O **sufixo DNS desta conexão** deve ser o nome DNS do domínio para cada domínio sendo monitorado.

        ![Configure o sufixo DNS nas definições avançadas de TCP/IP](media/ATA-DNS-Suffix.png)

        > [!NOTE]
        > Se o Gateway do ATA for um membro do domínio, isto poderá ser configurado automaticamente.

-   **Adaptador de captura** - usado para capturar o tráfego dos controladores de domínio.

    > [!IMPORTANT]
    > -   Configure o espelhamento de porta do adaptador de captura como o destino do tráfego de rede do controlador de domínio. Para saber mais, confira [Configurar o espelhamento de porta](configure-port-mirroring.md). Normalmente, você precisa trabalhar com a equipe de virtualização ou de rede para configurar o espelhamento de porta.
    > -   Configure um endereço IP não roteável estático para seu ambiente sem um gateway padrão e endereço do servidor DNS. Por exemplo, 1.1.1.1/32. Isso assegura que o adaptador da rede de captura poderá capturar a quantidade máxima de tráfego e que o adaptador da rede de gerenciamento será usado para enviar e receber o tráfego de rede solicitado.

### <a name="ports"></a>Portas
A tabela abaixo lista as portas mínimas que o Gateway do ATA requer configuradas no adaptador de gerenciamento:

|Protocolo|Transport|Porta|Para/De|Direção|
|------------|-------------|--------|-----------|-------------|
|LDAP|TCP e UDP|389|Controladores de domínio|Saída|
|LDAP seguro (LDAPS)|TCP|636|Controladores de domínio|Saída|
|LDAP para o Catálogo Global|TCP|3268|Controladores de domínio|Saída|
|LDAPS para o Catálogo Global|TCP|3269|Controladores de domínio|Saída|
|Kerberos|TCP e UDP|88|Controladores de domínio|Saída|
|Netlogon (SMB, CIFS, SAM-R)|TCP e UDP|445|Todos os dispositivos na rede|Saída|
|Tempo do Windows|UDP|123|Controladores de domínio|Saída|
|DNS|TCP e UDP|53|Servidores DNS|Saída|
|NTLM via RPC|TCP|135|Todos os dispositivos na rede|Ambos|
|NetBIOS|UDP|137|Todos os dispositivos na rede|Ambos|
|SSL|TCP|443|Centro de ATA|Saída|
|Syslog (opcional)|UDP|514|Servidor SIEM|Entrada|


> [!NOTE]
> Como parte do processo de resolução feito pelo Gateway de ATA, as seguintes portas precisam ser a entrada nos dispositivos na rede a partir dos Gateways de ATA.
>
> -   NTLM sobre RPC (porta TCP 135)
> -   NetBIOS (porta UDP 137)
> - Usando a conta de usuário do serviço de diretório, o Gateway do ATA consulta pontos de extremidade em sua organização para administradores locais usando SAM-R (logon de rede) para criar o [grafo de caminho de movimentação lateral](use-case-lateral-movement-path.md). Para obter mais informações, consulte [Configurar permissões necessárias do SAM-R](install-ata-step9-samr.md).
> - As seguintes portas precisam estar abertas para entrada em dispositivos na rede do Gateway do ATA:
>   -   NTLM via RPC (porta TCP 135) para fins de resolução
>   -   NetBIOS (porta UDP 137) para fins de resolução

## <a name="ata-lightweight-gateway-requirements"></a>Requisitos do Gateway Lightweight do ATA
Esta seção lista os requisitos para o Gateway Lightweight do ATA.
### <a name="general"></a>Geral
O Gateway Lightweight do ATA dá suporte à instalação em um controlador de domínio que executa o Windows Server 2008 R2 SP1 (sem incluir o Server Core), o Windows Server 2012, o Windows Server 2012 R2, o Windows Server 2016 (incluindo o Core, mas não o Nano).

O controlador de domínio pode ser um RODC (controlador de domínio somente leitura).

Antes de instalar o ATA Lightweight Gateway em um controlador de domínio que execute o Windows Server 2012 R2, confirme se a seguinte atualização está instalada: [KB2919355](https://support.microsoft.com/kb/2919355/).

Você pode verificar executando o seguinte cmdlet do Windows PowerShell: `[Get-HotFix -Id kb2919355]`

Se a instalação for para o Windows Server 2012 R2 Server Core, também deve ser instalada a seguinte atualização: [KB3000850](https://support.microsoft.com/help/3000850/november-2014-update-rollup-for-windows-rt-8.1%2c-windows-8.1%2c-and-windows-server-2012-r2).

 Você pode verificar executando o seguinte cmdlet do Windows PowerShell: `[Get-HotFix -Id kb3000850]`


Durante a instalação, o .Net Framework 4.6.1 é instalado e pode causar a reinicialização do controlador de domínio.


> [!NOTE]
> É necessário um mínimo de 5 GB de espaço e recomenda-se 10 GB. Isso inclui o espaço necessário para os binários do ATA, os logs do ATA e os [logs de desempenho](troubleshooting-ata-using-perf-counters.md).

### <a name="server-specifications"></a>Especificações do servidor

O Gateway Lightweight do ATA requer um mínimo de dois núcleos e 6 GB de RAM instalados no controlador de domínio.
Para ter um melhor desempenho, defina a **Opção de Energia** do Gateway Lightweight do ATA como **Alto Desempenho**.
O Gateway Lightweight do ATA pode ser implantado em controladores de domínio de vários tamanhos e cargas, dependendo da quantidade de tráfego de rede dos controladores de domínio e da quantidade de recursos instalados no controlador de domínio.

> [!NOTE] 
> Durante a execução como uma memória dinâmica da máquina virtual ou qualquer outra memória, não há suporte para o recurso de inchamento.

Para saber mais sobre os requisitos de hardware do Gateway Lightweight do ATA, confira [Planejamento de capacidade do ATA](ata-capacity-planning.md).

### <a name="time-synchronization"></a>Sincronização da hora

O servidor do Centro do ATA, os servidores do Gateway Lightweight do ATA e os controladores de domínio devem ter a hora sincronizada no espaço de cinco minutos entre si.

### <a name="network-adapters"></a>Adaptadores de rede

O Gateway Lightweight do ATA monitora o tráfego local em todos os adaptadores de rede do controlador de domínio. <br>
Após a implantação, você pode usar o Console do ATA para modificar quais adaptadores de rede são monitorados.

> [!NOTE]
> Não há suporte para o Gateway Lightweight em controles de domínio que executem o Windows 2008 R2 com o Broadcom Network Adapter Teaming habilitado.

### <a name="ports"></a>Portas
A tabela abaixo lista o mínimo de portas que o Gateway Lightweight do ATA exige:

|Protocolo|Transport|Porta|Para/De|Direção|
|------------|-------------|--------|-----------|-------------|
|DNS|TCP e UDP|53|Servidores DNS|Saída|
|NTLM via RPC|TCP|135|Todos os dispositivos na rede|Ambos|
|NetBIOS|UDP|137|Todos os dispositivos na rede|Ambos|
|SSL|TCP|443|Centro de ATA|Saída|
|Syslog (opcional)|UDP|514|Servidor SIEM|Entrada|
|Netlogon (SMB, CIFS, SAM-R)|TCP e UDP|445|Todos os dispositivos na rede|Saída|

> [!NOTE]
> Como parte do processo de resolução realizado pelo Gateway Lightweight do ATA, as portas a seguir precisam ser abertas na entrada dos dispositivos na rede por meio dos Gateways Lightweight do ATA.
>
> -   NTLM via RPC
> -   NetBIOS
> - Usando a conta de usuário do serviço de diretório, o Gateway Lightweight do ATA consulta pontos de extremidade em sua organização para administradores locais usando SAM-R (logon de rede) para criar o [grafo de caminho de movimentação lateral](use-case-lateral-movement-path.md). Para obter mais informações, consulte [Configurar permissões necessárias do SAM-R](install-ata-step9-samr.md).
> - As seguintes portas precisam estar abertas para entrada em dispositivos na rede do Gateway do ATA:
>   -   NTLM via RPC (porta TCP 135) para fins de resolução
>   -   NetBIOS (porta UDP 137) para fins de resolução

## <a name="ata-console"></a>Console do ATA
O acesso ao Console do ATA é por meio de um navegador, oferecendo suporte a definições e navegadores:

-   Internet Explorer versão 10 e posterior

-   Microsoft Edge

-   Google Chrome 40 e posterior

-   Resolução de largura mínima da tela de 1.700 pixels

## <a name="related-videos"></a>Vídeos Relacionados
- [Como escolher o tipo certo de Gateway do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Consulte Também
- [Ferramenta de dimensionamento do ATA](http://aka.ms/atasizingtool)
- [Arquitetura do ATA](ata-architecture.md)
- [Instalar o ATA](install-ata-step1.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)


