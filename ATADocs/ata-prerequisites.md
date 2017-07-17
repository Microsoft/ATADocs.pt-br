---
title: "Pré-requisitos do Advanced Threat Analytics | Microsoft Docs"
description: "Descreve os requisitos para uma implantação bem-sucedida do ATA em seu ambiente"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/2/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: a5f90544-1c70-4aff-8bf3-c59dd7abd687
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b810d066c59ea4663157027894eb7e2a39f7ff14
ms.sourcegitcommit: 53b56220fa761671442da273364bdb3d21269c9e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*



<a id="ata-prerequisites" class="xliff"></a>

# Pré-requisitos do ATA
Este artigo descreve os requisitos para uma implantação bem-sucedida do ATA em seu ambiente

>[!NOTE]
> Para obter informações sobre como planejar a capacidade e os recursos, confira [Planejamento de capacidade do ATA](ata-capacity-planning.md).


O ATA é composto pelo Centro do ATA, pelo Gateway do ATA e/ou o Gateway Lightweight do ATA. Para saber mais sobre os componentes do ATA, confira [Arquitetura do ATA](ata-architecture.md).

O Sistema do ATA funciona nos limites da floresta do active directory e oferece suporte a FFL (Nível funcional da floresta) do Windows 2003 e superior.


[Antes de iniciar](#before-you-start): esta seção lista as informações que você deve obter e as contas e entidades de rede que você deve ter antes de iniciar a instalação de ATA.

[Central do ATA](#ata-center-requirements): esta seção lista o hardware da Central de ATA, os requisitos de software, bem como as configurações que precisam ser definidas em seu servidor da Central de ATA.

[Gateway do ATA](#ata-gateway-requirements): Esta seção lista o hardware do Gateway do ATA, os requisitos de software, bem como as configurações que precisam ser definidas em seu servidor do Gateway do ATA.

[Gateway Lightweight do ATA](#ata-lightweight-gateway-requirements): esta seção lista os requisitos de hardware e de software do Gateway Lightweight do ATA.

[Console do ATA](#ata-console): esta seção lista os requisitos do navegador para executar o Console do ATA.

![Diagrama de arquitetura do ATA](media/ATA-architecture-topology.jpg)

<a id="before-you-start" class="xliff"></a>

## Antes de começar
Esta seção lista as informações que você deve obter, as contas e entidades de rede que você deve ter antes de iniciar a instalação do ATA.


-   Conta de usuário e senha com acesso de leitura para todos os objetos nos domínios que serão monitorados.

    > [!NOTE]
    > Se você tiver definido ACLs personalizadas em várias Unidades Organizacionais (UO) em seu domínio, verifique se o usuário selecionado tem permissões de leitura para essas UOs.

-   Não instale o Microsoft Message Analyzer em um Gateway ou Gateway Lightweight do ATA. O driver do Message Analyzer conflita com os drivers do Gateway e Gateway Lightweight do ATA. Se você executar o Wireshark no Gateway do ATA, precisará reiniciar o Serviço de Gateway do Microsoft Advanced Threat Analytics após parar a captura do Wireshark. Caso contrário, o Gateway não capturará qualquer tráfego. Observe que executar o Wireshark em um Gateway Lightweight do ATA não interfere no Gateway Lightweight do ATA.

-    Recomendado: o usuário deve ter permissões de leitura somente no contêiner de Objetos Excluídos. Isso permitirá que o ATA detecte a exclusão em massa de objetos no domínio. Para obter informações sobre como configurar permissões de leitura somente no contêiner de Objetos Excluídos, confira a seção **Alterar permissões em um contêiner de objetos excluídos** no tópico [Exibir ou Definir Permissões em um Objeto de Diretório](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

-   Opcional: uma conta de usuário que não tem nenhuma atividade de rede. Essa conta será configurada como o usuário Honeytoken do ATA. Para configurar o usuário Honeytoken, será necessário a SID da conta de usuário, não o nome de usuário. Para saber mais, confira [Como trabalhar com configurações de detecção do ATA](https://docs.microsoft.com/en-us/advanced-threat-analytics/deploy-use/working-with-detection-settings).

-   Opcional: além de coletar e analisar o tráfego de rede para e nos controladores de domínio, o ATA pode usar os eventos do Windows 4776, 4732, 4733, 4728, 4729, 4756 e 4757 para aprimorar ainda mais as detecções de Pass-the-Hash, Força Bruta, Modificação para grupos confidenciais e Honey Tokens do ATA. Eles podem ser recebidos de seu SIEM ou definindo o Encaminhamento de Eventos do Windows no controlador de domínio. Os eventos coletados fornecem à ATA informações adicionais que não estão disponíveis por meio do tráfego de rede do controlador de domínio.


<a id="ata-center-requirements" class="xliff"></a>

## Requisitos da Central de ATA
Esta seção lista os requisitos para a Central de ATA.
<a id="general" class="xliff"></a>

### Geral
A Central de ATA dá suporte à instalação em um servidor executando o Windows Server 2012 R2 ou o Windows Server 2016. A Central de ATA pode ser instalada em um servidor que seja membro de um domínio ou grupo de trabalho.

Antes de instalar a Central do ATA executando o Windows 2012 R2, confirme se a seguinte atualização foi instalada: [KB2919355](https://support.microsoft.com/kb/2919355/).

Você pode verificar executando o seguinte cmdlet do Windows PowerShell: `[Get-HotFix -Id kb2919355]`.

A instalação do ATA Center como uma máquina virtual tem suporte. 

>[!NOTE] 
> Durante a execução como uma memória dinâmica da máquina virtual ou qualquer outra memória, não há suporte para o recurso de inchamento.

Se você executar a Central de ATA como uma máquina virtual, deverá finalizar o servidor antes de criar um novo ponto de verificação para evitar uma possível corrupção do banco de dados.
<a id="server-specifications" class="xliff"></a>

### Especificações do servidor
Ao trabalhar em um servidor físico, o banco de dados do ATA precisa que você **desabilite** o NUMA (acesso não uniforme a memória) no BIOS. O sistema pode referir-se ao NUMA como Nó de Intercalação, caso em que você precisará **habilitar** a Intercalação de Nó para desabilitar o NUMA. Consulte a documentação da BIOS para saber mais. Observe que isso não é pertinente quando a Central do ATA está em execução em um servidor virtual.<br>
Para ter um melhor desempenho, defina a **Opção de Energia** do Centro do ATA como **Alto Desempenho**.<br>
O número de controladores de domínio que você está monitorando e a carga em cada um dos controladores de domínio determinam as especificações do servidor necessárias. Confira [Planejamento de capacidade do ATA](ata-capacity-planning.md) para obter mais detalhes.


<a id="time-synchronization" class="xliff"></a>

### Sincronização da hora
O servidor do Centro do ATA, os servidores do Gateway do ATA e os controladores de domínio devem ter a hora sincronizada no espaço de cinco minutos entre si.


<a id="network-adapters" class="xliff"></a>

### Adaptadores de rede
Você deve ter o seguinte:
-   Pelo menos um adaptador de rede (se estiver usando o servidor físico no ambiente de VLAN, recomendamos o uso de dois adaptadores de rede)

-   Dois endereços IP (recomendado, mas não obrigatório)

A comunicação entre a Central de ATA e o Gateway de ATA é criptografada usando o SSL na porta 443. Além disso, o Console do ATA também está usando SSL na porta 443. **Dois endereços IP** são recomendados. O serviço da Central de ATA associará a porta 443 ao primeiro endereço IP e o Console do ATA associará a porta 443 ao segundo endereço IP.

> [!NOTE]
> É possível usar um único endereço IP com duas portas diferentes, mas recomendamos dois endereços IP.

<a id="ports" class="xliff"></a>

### Portas
A tabela a seguir lista as portas mínimas que devem ser abertas para que a Central de ATA funcione corretamente.

|Protocolo|Transport|Porta|Para/De|Direção|
|------------|-------------|--------|-----------|-------------|
|**SSL** (Comunicações do ATA)|TCP|443 ou configurável|Gateway do ATA|Entrada|
|**HTTP** (opcional)|TCP|80|Rede da Empresa|Entrada|
|**HTTPS**|TCP|443|Rede da Empresa e Gateway de ATA|Entrada|
|**SMTP** (opcional)|TCP|25|Servidor SMTP|Saída|
|**SMTPS** (opcional)|TCP|465|Servidor SMTP|Saída|
|**Syslog** (opcional)|TCP|514|Servidor syslog|Saída|
|**LDAP**|TCP e UDP|389|Controladores de domínio|Saída|
|**LDAPS** (opcional)|TCP|636|Controladores de domínio|Saída|
|**DNS**|TCP e UDP|53|Servidores DNS|Saída|
|**Kerberos** (opcional se ingressado no domínio)|TCP e UDP|88|Controladores de domínio|Saída|
|**Netlogon** (opcional se ingressado no domínio)|TCP e UDP|445|Controladores de domínio|Saída|
|**Horário do Windows** (opcional se ingressado no domínio)|UDP|123|Controladores de domínio|Saída|

<a id="certificates" class="xliff"></a>

### Certificados
Verifique se o Centro do ATA tem acesso ao ponto de distribuição de CRL. Se os Gateways do ATA não tiverem acesso à Internet, siga [o procedimento para importar manualmente uma CRL](https://technet.microsoft.com/library/aa996972%28v=exchg.65%29.aspx), tendo o cuidado de instalar todos os pontos de distribuição de CRL de toda a cadeia.

Para facilitar a instalação do ATA, você pode instalar certificados autoassinados durante a instalação. Após a implantação, você pode substituir o autoassinado pelo certificado de uma Autoridade de Certificação interna a ser usado pelo Gateway de ATA.<br>
> [!NOTE]
> O tipo de provedor do certificado pode ser o CSP (Provedor de Serviços de Criptografia) ou KSP (Provedor de Armazenamento de Chaves).


> Não há suporte para o uso da renovação automática de certificados.


> [!NOTE]
> Se você pretende acessar o Console do ATA a partir de outros computadores, verifique se esses computadores confiam no certificado sendo usado pelo Console do ATA, caso contrário, será exibida uma página de aviso de que há um problema com o certificado de segurança do site antes de acessar a página de logon.

<a id="ata-gateway-requirements" class="xliff"></a>

## Requisitos do Gateway do ATA
Esta seção lista os requisitos para o Gateway do ATA.
<a id="general" class="xliff"></a>

### Geral
O Gateway do ATA dá suporte à instalação em um servidor executando o Windows Server 2012 R2 ou o Windows Server 2016 (Incluindo o Server Core).
O Gateway do ATA pode ser instalado em um servidor que seja membro de um domínio ou grupo de trabalho.
O Gateway do ATA pode ser usado para monitorar Controladores de Domínio com o Nível de Domínio Funcional do Windows 2003 e posterior.

Antes de instalar o Gateway do ATA executando o Windows 2012 R2, confirme se a seguinte atualização foi instalada: [KB2919355](https://support.microsoft.com/kb/2919355/).

Você pode verificar executando o seguinte cmdlet do Windows PowerShell: `[Get-HotFix -Id kb2919355]`.


Para obter informações sobre como usar máquinas virtuais com o Gateway do ATA, confira [Configurar o espelhamento de porta](configure-port-mirroring.md).

> [!NOTE]
> É necessário um mínimo de 5 GB de espaço e recomenda-se 10 GB. Isso inclui o espaço necessário para os binários ATA, [logs ATA](troubleshooting-ata-using-logs.md) e [logs de desempenho](troubleshooting-ata-using-perf-counters.md).

<a id="server-specifications" class="xliff"></a>

### Especificações do servidor
Para ter um melhor desempenho, defina a **Opção de Energia** do Gateway de ATA para **Alto Desempenho**.<br>
Um Gateway do ATA pode dar suporte ao monitoramento de vários controladores de domínio, dependendo da quantidade de tráfego de rede para e a partir dos controladores de domínio.

>[!NOTE] 
> Durante a execução como uma memória dinâmica da máquina virtual ou qualquer outra memória, não há suporte para o recurso de inchamento.

Para saber mais sobre os requisitos de hardware do Gateway do ATA, confira [Planejamento de capacidade do ATA](ata-capacity-planning.md).

<a id="time-synchronization" class="xliff"></a>

### Sincronização da hora
O servidor do Centro do ATA, os servidores do Gateway do ATA e os controladores de domínio devem ter a hora sincronizada no espaço de cinco minutos entre si.

<a id="network-adapters" class="xliff"></a>

### Adaptadores de rede
O Gateway de ATA requer pelo menos um Adaptador de gerenciamento e pelo menos um adaptador de captura:

-   **Adaptador de gerenciamento** - será usado para as comunicações em sua rede corporativa. Esse adaptador deve ser configurado com o seguinte:

    -   Endereço IP estático, incluindo o gateway padrão

    -   Servidores DNS preferenciais e alternativos

    -   O **sufixo DNS desta conexão** deve ser o nome DNS do domínio para cada domínio sendo monitorado.

        ![Configure o sufixo DNS nas definições avançadas de TCP/IP](media/ATA-DNS-Suffix.png)

        > [!NOTE]
        > Se o Gateway do ATA for um membro do domínio, isto poderá ser configurado automaticamente.

-   **Adaptador de captura** - será usado para capturar o tráfego para e a partir dos controladores de domínio.

    > [!IMPORTANT]
    > -   Configure o espelhamento de porta do adaptador de captura como o destino do tráfego de rede do controlador de domínio. Confira [Configurar o espelhamento de porta](configure-port-mirroring.md) para saber mais. Normalmente, você precisará trabalhar com a equipe de virtualização ou de rede para configurar o espelhamento de porta.
    > -   Configure um endereço IP não roteável estático para seu ambiente sem um gateway padrão e endereço do servidor DNS. Por exemplo, 1.1.1.1/32. Isso irá assegurar que o adaptador da rede de captura poderá capturar a quantidade máxima de tráfego e que o adaptador da rede de gerenciamento será usado para enviar e receber o tráfego de rede requerido.

<a id="ports" class="xliff"></a>

### Portas
A tabela abaixo lista as portas mínimas que o Gateway do ATA requer configuradas no adaptador de gerenciamento:

|Protocolo|Transport|Porta|Para/De|Direção|
|------------|-------------|--------|-----------|-------------|
|LDAP|TCP e UDP|389|Controladores de domínio|Saída|
|LDAP seguro (LDAPS)|TCP|636|Controladores de domínio|Saída|
|LDAP para o Catálogo Global|TCP|3268|Controladores de domínio|Saída|
|LDAPS para o Catálogo Global|TCP|3269|Controladores de domínio|Saída|
|Kerberos|TCP e UDP|88|Controladores de domínio|Saída|
|Netlogon|TCP e UDP|445|Controladores de domínio|Saída|
|Tempo do Windows|UDP|123|Controladores de domínio|Saída|
|DNS|TCP e UDP|53|Servidores DNS|Saída|
|NTLM via RPC|TCP|135|Todos os dispositivos na rede|Saída|
|NetBIOS|UDP|137|Todos os dispositivos na rede|Saída|
|SSL|TCP|443 ou como configurado para o Serviço da Central|Centro do ATA:<br /><br />- Endereço IP do Serviço de Central<br />-   Endereço IP do Console|Saída|
|Syslog (opcional)|UDP|514|Servidor SIEM|Entrada|

> [!NOTE]
> Como parte do processo de resolução feito pelo Gateway de ATA, as seguintes portas precisam ser a entrada nos dispositivos na rede a partir dos Gateways de ATA.
>
> -   NTLM sobre RPC (porta TCP 135)
> -   NetBIOS (porta UDP 137)

<a id="ata-lightweight-gateway-requirements" class="xliff"></a>

## Requisitos do Gateway Lightweight do ATA
Esta seção lista os requisitos para o Gateway Lightweight do ATA.
<a id="general" class="xliff"></a>

### Geral
O Gateway Lightweight do ATA dá suporte à instalação em um controlador de domínio que executa o Windows Server 2008 R2 SP1 (sem incluir o Server Core), o Windows Server 2012, o Windows Server 2012 R2, o Windows Server 2016 (incluindo o Core, mas não o Nano).

O controlador de domínio pode ser um RODC (controlador de domínio somente leitura).

Antes de instalar o ATA Lightweight Gateway em um controlador de domínio que execute o Windows Server 2012 R2, confirme que a seguinte atualização está instalada: [KB2919355](https://support.microsoft.com/kb/2919355/).

Você pode verificar executando o seguinte cmdlet do Windows PowerShell: `[Get-HotFix -Id kb2919355]`

Se a instalação for para o Windows Server 2012 R2 Server Core, também deve ser instalada a seguinte atualização: [KB3000850](https://support.microsoft.com/help/3000850/november-2014-update-rollup-for-windows-rt-8.1%2c-windows-8.1%2c-and-windows-server-2012-r2).

 Você pode verificar executando o seguinte cmdlet do Windows PowerShell: `[Get-HotFix -Id kb3000850]`


Durante a instalação, o .Net Framework 4.6.1 é instalado e pode causar a reinicialização do controlador de domínio.


> [!NOTE]
> É necessário um mínimo de 5 GB de espaço e recomenda-se 10 GB. Isso inclui o espaço necessário para os binários ATA, [logs ATA](troubleshooting-ata-using-logs.md) e [logs de desempenho](troubleshooting-ata-using-perf-counters.md).

<a id="server-specifications" class="xliff"></a>

### Especificações do servidor

O Gateway Lightweight do ATA requer um mínimo de dois núcleos e 6 GB de RAM instalados no controlador de domínio.
Para ter um melhor desempenho, defina a **Opção de Energia** do Gateway Lightweight do ATA como **Alto Desempenho**.
O Gateway Lightweight do ATA pode ser implantado em controladores de domínio de vários tamanhos e cargas, dependendo da quantidade de tráfego de rede dos controladores de domínio e da quantidade de recursos instalados no controlador de domínio.

>[!NOTE] 
> Durante a execução como uma memória dinâmica da máquina virtual ou qualquer outra memória, não há suporte para o recurso de inchamento.

Para saber mais sobre os requisitos de hardware do Gateway Lightweight do ATA, confira [Planejamento de capacidade do ATA](ata-capacity-planning.md).

<a id="time-synchronization" class="xliff"></a>

### Sincronização da hora
O servidor do Centro do ATA, os servidores do Gateway do ATA e os controladores de domínio devem ter a hora sincronizada no espaço de cinco minutos entre si.
<a id="network-adapters" class="xliff"></a>

### Adaptadores de rede
O Gateway Lightweight do ATA monitora o tráfego local em todos os adaptadores de rede do controlador de domínio. <br>
Após a implantação, você pode usar o Console do ATA para modificar quais adaptadores de rede são monitorados.

<a id="ports" class="xliff"></a>

### Portas
A tabela abaixo lista o mínimo de portas que o Gateway Lightweight do ATA exige:

|Protocolo|Transport|Porta|Para/De|Direção|
|------------|-------------|--------|-----------|-------------|
|DNS|TCP e UDP|53|Servidores DNS|Saída|
|NTLM via RPC|TCP|135|Todos os dispositivos na rede|Saída|
|NetBIOS|UDP|137|Todos os dispositivos na rede|Saída|
|SSL|TCP|443 ou como configurado para o Serviço da Central|Centro do ATA:<br /><br />- Endereço IP do Serviço de Central<br />-   Endereço IP do Console|Saída|
|Syslog (opcional)|UDP|514|Servidor SIEM|Entrada|

> [!NOTE]
> Como parte do processo de resolução realizado pelo Gateway Lightweight do ATA, as portas a seguir precisam ser abertas na entrada dos dispositivos na rede por meio dos Gateways Lightweight do ATA.
>
> -   NTLM via RPC
> -   NetBIOS

<a id="ata-console" class="xliff"></a>

## Console do ATA
O acesso ao Console do ATA é por meio de um navegador com suporte para o seguinte:

-   Internet Explorer versão 10 e posterior

-   Microsoft Edge

-   Google Chrome 40 e posterior

-   Resolução de largura mínima da tela de 1.700 pixels

<a id="see-also" class="xliff"></a>

## Consulte também

- [Arquitetura do ATA](ata-architecture.md)
- [Instalar o ATA](install-ata-step1.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

