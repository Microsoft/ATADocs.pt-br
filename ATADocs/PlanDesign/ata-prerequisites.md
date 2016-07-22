---
title: "Pré-requisitos do ATA | Microsoft Advanced Threat Analytics"
description: "Descreve os requisitos para uma implantação bem-sucedida do ATA em seu ambiente"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a5f90544-1c70-4aff-8bf3-c59dd7abd687
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 1f85b9a0f51bd18edaa91ea208d6e6c7c7de56cc
ms.openlocfilehash: da887431d8e63a7ae8ceeb3e7e22011d356e3590


---

# Pré-requisitos do ATA
Este artigo descreve os requisitos para uma implantação bem-sucedida do ATA em seu ambiente

>[!NOTE]
> Para obter informações sobre como planejar a capacidade e os recursos, confira [Planejamento de capacidade do ATA](ata-capacity-planning.md).


O ATA é composto pelo Centro do ATA, pelo Gateway do ATA e/ou o Gateway Lightweight do ATA. Para saber mais sobre os componentes do ATA, confira [Arquitetura do ATA](ata-architecture.md).


[Antes de iniciar](#before-you-start): esta seção lista as informações que você deve obter e as contas e entidades de rede que você deve ter antes de iniciar a instalação de ATA.

[Central do ATA](#ata-center-requirements): esta seção lista o hardware da Central de ATA, os requisitos de software, bem como as configurações que precisam ser definidas em seu servidor da Central de ATA.

[Gateway do ATA](#ata-gateway-requirements): Esta seção lista o hardware do Gateway do ATA, os requisitos de software, bem como as configurações que precisam ser definidas em seu servidor do Gateway do ATA.

[Gateway Lightweight do ATA](#ata-lightweight-gateway-requirements): esta seção lista os requisitos de hardware e de software do Gateway Lightweight do ATA.

[Console do ATA](#ata-console): esta seção lista os requisitos do navegador para executar o Console do ATA.

![Diagrama de arquitetura do ATA](media/ATA-architecture-topology.jpg)

## Antes de começar
Esta seção lista as informações que você deve obter, as contas e entidades de rede que você deve ter antes de iniciar a instalação do ATA.


-   Conta de usuário e senha com acesso de leitura para todos os objetos nos domínios que serão monitorados.

    > [!NOTE]
    > Se você tiver definido ACLs personalizadas em várias Unidades Organizacionais (UO) em seu domínio, verifique se o usuário selecionado tem permissões de leitura para essas UOs.

-   Ter uma lista de todas as sub-redes usadas em sua rede para a VPN e o Wi-Fi, que reatribui endereços IP entre os dispositivos em um período muito curto de tempo (em segundos ou minutos).  Convém identificar essas sub-redes de concessão de curto prazo para que o ATA possa reduzir seu tempo de vida do cache para aceitar a reatribuição rápida entre os dispositivos. Confira [Instalar o ATA](/advanced-threat-analytics/deploy-use/install-ata) para uma configuração de sub-rede de concessão de curto prazo.
-   Verifique se o Analisador de Mensagem e o Wire Shark não estão instalados no Gateway do ATA ou na Central do ATA.
-    Opcional: O usuário deve ter permissões de leitura somente no contêiner de Objetos Excluídos. Isso permitirá que o ATA detecte a exclusão em massa de objetos no domínio. Para obter informações sobre como configurar permissões de leitura somente no contêiner de Objetos Excluídos, confira a seção **Alterar permissões em um contêiner de objetos excluídos** no tópico [Exibir ou Definir Permissões em um Objeto de Diretório](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

-   Opcional: uma conta de usuário que não tem nenhuma atividade de rede. Essa conta será configurada como o usuário Honeytoken do ATA. Para configurar o usuário Honeytoken, será necessário a SID da conta de usuário, não o nome de usuário.

-   Opcional: além de coletar e analisar o tráfego de rede para e a partir dos controladores de domínio, o ATA pode usar o evento 4776 do Windows para aprimorar a detecção da Passagem de Hash do ATA. Isso pode ser recebido de seu SIEM ou definindo o Encaminhamento de Eventos do Windows no controlador de domínio. Os eventos coletados fornecem à ATA informações adicionais que não estão disponíveis por meio do tráfego de rede do controlador de domínio.


## Requisitos da Central de ATA
Esta seção lista os requisitos para a Central de ATA.
### Geral
A Central de ATA dá suporte à instalação em um servidor executando o Windows Server 2012 R2. A Central de ATA pode ser instalada em um servidor que seja membro de um domínio ou grupo de trabalho.

Antes de instalar a Central do ATA, confirme se a seguinte atualização foi instalada: [KB2919355](https://support.microsoft.com/kb/2919355/).

Você pode verificar executando o seguinte cmdlet do Windows PowerShell: `[Get-HotFix -Id kb2919355]`.

A instalação do ATA Center como uma máquina virtual tem suporte. 

Se você executar a Central de ATA como uma máquina virtual, deverá finalizar o servidor antes de criar um novo ponto de verificação para evitar uma possível corrupção do banco de dados.
### Especificações do servidor
Ao trabalhar em um servidor físico, o banco de dados do ATA precisa que você **desabilite** o NUMA (acesso não uniforme a memória) no BIOS. O sistema pode referir-se ao NUMA como Nó de Intercalação, caso em que você precisará **habilitar** a Intercalação de Nó para desabilitar o NUMA. Consulte a documentação da BIOS para saber mais. Observe que isso não é pertinente quando a Central do ATA está em execução em um servidor virtual.<br>
Para ter um melhor desempenho, defina a **Opção de Energia** do Centro do ATA como **Alto Desempenho**.<br>
O número de controladores de domínio que você está monitorando e a carga em cada um dos controladores de domínio determinam as especificações do servidor necessárias. Confira [Planejamento de capacidade do ATA](ata-capacity-planning.md) para obter mais detalhes.

>[!NOTE] 
> Durante a execução como uma memória dinâmica da máquina virtual ou qualquer outra memória, não há suporte para o recurso de inchamento.

### Sincronização da hora
O servidor do Centro do ATA, os servidores do Gateway do ATA e os controladores de domínio devem ter a hora sincronizada no espaço de cinco minutos entre si.


### Adaptadores de rede
Você deve ter o seguinte:
-   Pelo menos um adaptador de rede

-   Dois endereços IP (recomendado, mas não obrigatório)

A comunicação entre a Central de ATA e o Gateway de ATA é criptografada usando o SSL na porta 443. Além disso, o Console de ATA é executado no IIS e protegido usando o SSL na porta 443. **Dois endereços IP** são recomendados. O serviço da Central de ATA associará a porta 443 ao primeiro endereço IP e o IIS associará a porta 443 ao segundo endereço IP.

> [!NOTE]
> É possível usar um único endereço IP com duas portas diferentes, mas recomendamos dois endereços IP.

### Portas
A tabela a seguir lista as portas mínimas que devem ser abertas para que a Central de ATA funcione corretamente.

Nessa tabela, o endereço IP 1 é vinculado ao serviço do Centro do ATA e o endereço IP 2 é vinculado ao serviço do IIS para o Console do ATA:

|Protocolo|Transport|Porta|Para/De|Direção|Endereço IP|
|------------|-------------|--------|-----------|-------------|--------------|
|**SSL** (Comunicações do ATA)|TCP|443 ou configurável|Gateway do ATA|Entrada|Endereço IP 1|
|**HTTP**|TCP|80|Rede da Empresa|Entrada|Endereço IP 2|
|**HTTPS**|TCP|443|Rede da Empresa e Gateway de ATA|Entrada|Endereço IP 2|
|**SMTP** (opcional)|TCP|25|Servidor SMTP|Saída|Endereço IP 2|
|**SMTPS** (opcional)|TCP|465|Servidor SMTP|Saída|Endereço IP 2|
|**Syslog** (opcional)|TCP|514|Servidor syslog|Saída|Endereço IP 2|

### Certificados
Verifique se o Centro do ATA tem acesso ao ponto de distribuição de CRL. Se os Gateways do ATA não tiverem acesso à Internet, siga [o procedimento para importar manualmente uma CRL](https://technet.microsoft.com/library/aa996972%28v=exchg.65%29.aspx), tendo o cuidado de instalar todos os pontos de distribuição de CRL de toda a cadeia.

Para facilitar a instalação da Central de ATA, você pode instalar os certificados autoassinados durante a instalação da Central de ATA. Após a implantação, você pode substituir o autoassinado pelo certificado de uma Autoridade de Certificação interna a ser usado pelo Gateway de ATA.<br>
> [!NOTE]
> O tipo de provedor do certificado deve ser o CSP (provedor de serviços de criptografia).


A Central de ATA exige certificados para os seguintes serviços:

-   Serviços de Informação da Internet (IIS) – certificado do servidor Web

-   Serviço de Central de ATA – certificado de autenticação de servidor

> [!NOTE]
> Se você pretende acessar o Console do ATA a partir de outros computadores, verifique se esses computadores confiam no certificado sendo usado pelo IIS, caso contrário, será exibida uma página de aviso de que há um problema com o certificado de segurança do site antes de acessar a página de logon.

## Requisitos do Gateway do ATA
Esta seção lista os requisitos para o Gateway do ATA.
### Geral
O Gateway do ATA dá suporte à instalação em um servidor executando o Windows Server 2012 R2.
O Gateway do ATA pode ser instalado em um servidor que seja membro de um domínio ou grupo de trabalho.

Antes de instalar o Gateway do ATA, confirme se a seguinte atualização foi instalada: [KB2919355](https://support.microsoft.com/kb/2919355/).

Você pode verificar executando o seguinte cmdlet do Windows PowerShell: `[Get-HotFix -Id kb2919355]`.

Para obter informações sobre como usar máquinas virtuais com o Gateway do ATA, confira [Configurar o espelhamento de porta](/advanced-threat-analytics/deploy-use/configure-port-mirroring).

### Especificações do servidor
Para ter um melhor desempenho, defina a **Opção de Energia** do Gateway de ATA para **Alto Desempenho**.<br>
Um Gateway do ATA pode dar suporte ao monitoramento de vários controladores de domínio, dependendo da quantidade de tráfego de rede para e a partir dos controladores de domínio.

>[!NOTE] 
> Durante a execução como uma memória dinâmica da máquina virtual ou qualquer outra memória, não há suporte para o recurso de inchamento.

### Sincronização da hora
O servidor do Centro do ATA, os servidores do Gateway do ATA e os controladores de domínio devem ter a hora sincronizada no espaço de cinco minutos entre si.

### Adaptadores de rede
O Gateway de ATA requer pelo menos um Adaptador de gerenciamento e pelo menos um adaptador de captura:

-   **Adaptador de gerenciamento** - será usado para as comunicações em sua rede corporativa. Esse adaptador deve ser configurado com o seguinte:

    -   Endereço IP estático, incluindo o gateway padrão

    -   Servidores DNS preferenciais e alternativos

    -   O **sufixo DNS desta conexão** deve ser o nome DNS do domínio para cada domínio sendo monitorado.

        ![Configure o sufixo DNS nas definições avançadas de TCP/IP](media/ATA-DNS-Suffix.png)

        > [!NOTE]
        > Se o Gateway de ATA for um membro do domínio, isto será configurado automaticamente.

-   **Adaptador de captura** - será usado para capturar o tráfego para e a partir dos controladores de domínio.

    > [!IMPORTANT]
    > -   Configure o espelhamento de porta do adaptador de captura como o destino do tráfego de rede do controlador de domínio. Confira [Configurar o espelhamento de porta](/advanced-threat-analytics/deploy-use/configure-port-mirroring) para saber mais. Normalmente, você precisará trabalhar com a equipe de virtualização ou de rede para configurar o espelhamento de porta.
    > -   Configure um endereço IP não roteável estático para seu ambiente sem um gateway padrão e endereço do servidor DNS. Por exemplo, 1.1.1.1/32. Isso irá assegurar que o adaptador da rede de captura poderá capturar a quantidade máxima de tráfego e que o adaptador da rede de gerenciamento será usado para enviar e receber o tráfego de rede requerido.

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
|SSL|TCP|443 ou como configurado para o Serviço da Central|Centro do ATA:<br /><br />- Endereço IP do Serviço de Central<br />-   Endereço IP do IIS|Saída|
|Syslog (opcional)|UDP|514|Servidor SIEM|Entrada|

> [!NOTE]
> Como parte do processo de resolução feito pelo Gateway de ATA, as seguintes portas precisam ser a entrada nos dispositivos na rede a partir dos Gateways de ATA.
>
> -   NTLM via RPC
> -   NetBIOS

### Certificados
Verifique se o Centro do ATA tem acesso ao ponto de distribuição de CRL. Se os Gateways do ATA não tiverem acesso à Internet, execute o procedimento para importar manualmente uma CRL, tendo o cuidado de instalar todos os pontos de distribuição de CRL da cadeia inteira.<br>
Para facilitar a instalação da Central de ATA, você pode instalar os certificados autoassinados durante a instalação da Central de ATA. Após a implantação, você pode substituir o autoassinado pelo certificado de uma Autoridade de Certificação interna a ser usado pelo Gateway de ATA.

> [!NOTE]
> O tipo de provedor do certificado deve ser o CSP (provedor de serviços de criptografia).<br>

Um certificado que oferece suporte para a **Autenticação do Servidor** precisa ser instalado no armazenamento do Computador do Gateway de ATA no armazenamento do Computador Local. A Central de ATA deve confiar nesse certificado.

## Requisitos do Gateway Lightweight do ATA
Esta seção lista os requisitos para o Gateway Lightweight do ATA.
### Geral
O Gateway Lightweight do ATA dá suporte à instalação em um controlador de domínio que executa o Windows Server 2008 R2 SP1, o Windows Server 2012 ou o Windows Server 2012 R2.

O controlador de domínio pode ser um RODC (controlador de domínio somente leitura).

O controlador de domínio não pode ser o Server Core.

Antes de instalar o Gateway Lightweight do ATA em um controlador de domínio que executa o Windows Server 2012 R2 SP1, confirme se a seguinte atualização foi instalada: [KB2919355](https://support.microsoft.com/kb/2919355/).
Você pode verificar executando o seguinte cmdlet do Windows PowerShell: `[Get-HotFix -Id kb2919355]`.

### Especificações do servidor

O Gateway Lightweight do ATA requer um mínimo de dois núcleos e 6 GB de RAM instalados no controlador de domínio.
Para ter um melhor desempenho, defina a **Opção de Energia** do Gateway Lightweight do ATA como **Alto Desempenho**.
O Gateway Lightweight do ATA pode ser implantado em controladores de domínio de vários tamanhos e cargas, dependendo da quantidade de tráfego de rede dos controladores de domínio e da quantidade de recursos instalados no controlador de domínio.

>[!NOTE] 
> Durante a execução como uma memória dinâmica da máquina virtual ou qualquer outra memória, não há suporte para o recurso de inchamento.


### Sincronização da hora
O servidor do Centro do ATA, os servidores do Gateway do ATA e os controladores de domínio devem ter a hora sincronizada no espaço de cinco minutos entre si.
### Adaptadores de rede
O Gateway Lightweight do ATA monitora o tráfego local em todos os adaptadores de rede do controlador de domínio. <br>
Após a implantação, você pode usar o Console do ATA para modificar quais adaptadores de rede são monitorados.

### Portas
A tabela abaixo lista o mínimo de portas que o Gateway Lightweight do ATA exige:

|Protocolo|Transport|Porta|Para/De|Direção|
|------------|-------------|--------|-----------|-------------|
|DNS|TCP e UDP|53|Servidores DNS|Saída|
|NTLM via RPC|TCP|135|Todos os dispositivos na rede|Saída|
|NetBIOS|UDP|137|Todos os dispositivos na rede|Saída|
|SSL|TCP|443 ou como configurado para o Serviço da Central|Centro do ATA:<br /><br />- Endereço IP do Serviço de Central<br />-   Endereço IP do IIS|Saída|
|Syslog (opcional)|UDP|514|Servidor SIEM|Entrada|

> [!NOTE]
> Como parte do processo de resolução realizado pelo Gateway Lightweight do ATA, as portas a seguir precisam ser abertas na entrada dos dispositivos na rede por meio dos Gateways Lightweight do ATA.
>
> -   NTLM via RPC
> -   NetBIOS

### Certificados
Verifique se o Centro do ATA tem acesso ao ponto de distribuição de CRL. Se os Gateways Lightweight do ATA não tiverem acesso à Internet, execute o procedimento para importar manualmente uma CRL, tendo o cuidado de instalar todos os pontos de distribuição de CRL da cadeia inteira.
Para facilitar a instalação da Central de ATA, você pode instalar os certificados autoassinados durante a instalação da Central de ATA. Após a implantação, você pode substituir o autoassinado pelo certificado de uma Autoridade de Certificação interna a ser usado pelo Gateway Lightweight do ATA.
> [!NOTE]
> O tipo de provedor do certificado deve ser o CSP (provedor de serviços de criptografia).

Um certificado que dá suporte à Autenticação do Servidor precisa ser instalado no armazenamento do Computador do Gateway Lightweight do ATA no repositório Computador Local. A Central de ATA deve confiar nesse certificado.

## Console do ATA
O acesso ao Console do ATA é por meio de um navegador com suporte para o seguinte:

-   Internet Explorer versão 10 e posterior

-   Google Chrome 40 e posterior

-   Resolução de largura mínima da tela de 1.700 pixels

## Consulte também

- [Arquitetura do ATA](ata-architecture.md)
- [Instalar o ATA](/advanced-threat-analytics/deploy-use/install-ata)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Jun16_HO5-->


