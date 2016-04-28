---
# required metadata

title: Pré-requisitos do ATA | Microsoft Advanced Threat Analytics
description: Descreve os requisitos para uma implantação bem-sucedida do ATA em seu ambiente
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a5f90544-1c70-4aff-8bf3-c59dd7abd687

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Pré-requisitos do ATA
Este artigo descreve os requisitos para uma implantação bem-sucedida do ATA em seu ambiente

O ATA é composto por dois componentes: a Central de ATA e o Gateway do ATA. Para obter mais informações sobre os componentes do ATA, confira [Arquitetura do ATA](/advanced-threat-analytics/Understand/ata-architecture).

[Antes de iniciar](#before-you-start): esta seção lista as informações que você deve obter e as contas e entidades de rede que você deve ter antes de iniciar a instalação de ATA.

[Central de ATA](#ata-center-requirements): esta seção lista o hardware da Central de ATA, os requisitos de software, bem como as configurações que precisam ser definidas em seu servidor da Central de ATA.

[Gateway do ATA](#ata-gateway-requirements): Esta seção lista o hardware do Gateway do ATA, os requisitos de software, bem como as configurações que precisam ser definidas em seu servidor do Gateway do ATA.

[Console do ATA](#ata-console): esta seção lista os requisitos do navegador para executar o Console do ATA.

![Diagrama de arquitetura do ATA](media/ATA-architecture-topology.jpg)

## Antes de começar
Esta seção lista as informações que você deve obter, as contas e entidades de rede que você deve ter antes de iniciar a instalação do ATA.

-   **Controladores de domínio** em execução no Windows Server 2008 e posterior.

-   **Conta de usuário e senha** com acesso de leitura para **todos os objetos** nos domínios que serão monitorados.

    > [!NOTE]
    > Se você tiver definido ACLs personalizadas em várias Unidades Organizacionais (UO) em seu domínio, verifique se o usuário selecionado tem permissões de leitura para essas UOs.

    Opcional: O usuário deve ter permissões de leitura somente no contêiner de Objetos Excluídos. Isso permitirá que o ATA detecte a exclusão em massa de objetos no domínio. Para obter informações sobre como configurar permissões de leitura somente no contêiner de Objetos Excluídos, confira a seção **Alterar permissões em um contêiner de objetos excluídos** no tópico [Exibir ou Definir Permissões em um Objeto de Diretório](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx).

-   Opcional: uma conta de usuário que não tem nenhuma atividade de rede. Essa conta será configurada como o usuário Honeytoken do ATA. Para configurar o usuário Honeytoken, será necessário a SID da conta de usuário, não o nome de usuário.

-   Opcional: além de coletar e analisar o tráfego de rede para e a partir dos controladores de domínio, o ATA pode usar o evento 4776 do Windows para aprimorar a detecção da Passagem de Hash do ATA. Isso pode ser recebido de seu SIEM ou definindo o Encaminhamento de Eventos do Windows no controlador de domínio. Os eventos coletados fornecem à ATA informações adicionais que não estão disponíveis por meio do tráfego de rede do controlador de domínio.

-   Pode ser útil ter uma lista de todas as sub-redes usadas em sua rede para a VPN e o Wi-Fi, que reatribui endereços IP entre os dispositivos em um período muito curto de tempo (em segundos ou minutos).  Convém identificar essas sub-redes de concessão de curto prazo para que o ATA possa reduzir seu tempo de vida do cache para aceitar a reatribuição rápida entre os dispositivos. Confira [Instalar o ATA](/advanced-threat-analytics/DeployUse/install-ata) para uma configuração de sub-rede de concessão de curto prazo.

## Requisitos da Central de ATA
Esta seção lista os requisitos para a Central de ATA.

A Central de ATA dá suporte à instalação em um servidor executando o Windows Server 2012 R2. Execute o Windows Update e verifique se todas as atualizações importantes estão instaladas.
 O número de controladores de domínio que você está monitorando e a carga em cada um dos controladores determina os requisitos de hardware.

A instalação do ATA Center como uma máquina virtual tem suporte. Para saber mais, confira [Configurar o espelhamento de porta](configure-port-mirroring.md).

Se você executar a Central de ATA como uma máquina virtual, deverá finalizar o servidor antes de criar um novo ponto de verificação para evitar uma possível corrupção do banco de dados.

> [!NOTE]
> - A Central de ATA pode ser instalada em um servidor que seja membro de um domínio ou grupo de trabalho.
>
> - A Central de ATA requer um mínimo de 21 dias de dados para a análise de comportamento do usuário.
>
> - Para obter mais informações sobre os requisitos de hardware, confira [Planejamento de capacidade de ATA](ata-capacity-planning.md).


### Sincronização da hora
O servidor da Central de ATA, os servidores do Gateway de ATA e os controladores de domínio devem ter a hora sincronizada para 5 minutos entre si.

### Configurações BIOS
O banco de dados de ATA requer que você **desabilite** o acesso de memória não uniforme (NUMA) no BIOS. O sistema pode referir-se ao NUMA como Nó de Intercalação, caso em que você precisará **habilitar** a Intercalação de Nó. Consulte a documentação da BIOS para saber mais.

### Adaptadores de rede
Requisitos:

-   Um adaptador de rede

-   Dois endereços IP

A comunicação entre a Central de ATA e o Gateway de ATA é criptografada usando o SSL na porta 443. Além disso, o Console de ATA é executado no IIS e protegido usando o SSL na porta 443. **Dois endereços IP** são recomendados. O serviço da Central de ATA associará a porta 443 ao primeiro endereço IP e o IIS associará a porta 443 ao segundo endereço IP.

> [!NOTE]
> É possível usar um único endereço IP com duas portas diferentes, mas recomendamos dois endereços IP.

### Portas
A tabela a seguir lista as portas mínimas que devem ser abertas para que a Central de ATA funcione corretamente.

Nessa tabela, o endereço IP 1 é vinculado ao serviço da Central de ATA e o endereço IP 2 é vinculado ao serviço do IIS para o Console do ATA.

|Protocolo|Transport|Porta|Para/De|Direção|Endereço IP|
|------------|-------------|--------|-----------|-------------|--------------|
|**SSL** (Comunicações do ATA)|TCP|443 ou configurável|Gateway do ATA|Entrada|Endereço IP 1|
|**HTTP**|TCP|80|Rede da Empresa|Entrada|Endereço IP 2|
|**HTTPS**|TCP|443|Rede da Empresa e Gateway de ATA|Entrada|Endereço IP 2|
|**SMTP** (opcional)|TCP|25|Servidor SMTP|Saída|Endereço IP 2|
|**SMTPS** (opcional)|TCP|465|Servidor SMTP|Saída|Endereço IP 2|
|**Syslog** (opcional)|TCP|514|Servidor syslog|Saída|Endereço IP 2|

### Certificados
Verifique se que os Gateways de ATA têm acesso ao ponto de distribuição de CRL. Se os Gateways do ATA não tiverem acesso à Internet, execute [o procedimento para importar manualmente uma CRL](https://technet.microsoft.com/en-us/library/aa996972%28v=exchg.65%29.aspx), tendo o cuidado de instalar todos os pontos de distribuição de CRL da cadeia inteira.

Para facilitar a instalação da Central de ATA, você pode instalar os certificados autoassinados durante a instalação da Central de ATA. Após a implantação, você pode substituir o autoassinado pelo certificado de uma Autoridade de Certificação interna a ser usado pelo Gateway de ATA.

> [!NOTE]
> Os certificados autoassinados devem ser usados somente para a implantação de laboratório.

A Central de ATA exige certificados para os seguintes serviços:

-   Serviços de Informação da Internet (IIS) – certificado do servidor Web

-   Serviço de Central de ATA – certificado de autenticação de servidor

> [!NOTE]
> Se você pretende acessar o Console do ATA a partir de outros computadores, verifique se esses computadores confiam no certificado sendo usado pelo IIS, caso contrário, será exibida uma página de aviso de que há um problema com o certificado de segurança do site antes de acessar a página de logon.

## Requisitos do Gateway do ATA
O Gateway do ATA dá suporte à instalação em um servidor executando o Windows Server 2012 R2.

Execute o Windows Update e verifique se todas as atualizações **importantes** foram instaladas.
Antes de instalar o Gateway de ATA, confirme se a atualização foi instalada: [KB2919355](https://support.microsoft.com/en-us/kb/2919355/).

Você pode verificar executando o seguinte cmdlet do Windows PowerShell: `[Get-HotFix -Id kb2919355]`.

> [!NOTE]
> -   O Gateway do ATA pode ser instalado em um servidor que seja membro de um domínio ou grupo de trabalho.
> -   O Gateway do ATA não pode ser instalado em um controlador de domínio.

Para obter informações sobre como usar máquinas virtuais com o Gateway de ATA, confira [Configurar o espelhamento de porta](configure-port-mirroring.md).

> [!NOTE]
> Se você executar o Gateway do ATA como uma máquina virtual, finalize o servidor antes de criar um novo ponto de verificação para evitar uma possível corrupção do banco de dados.

Um Gateway do ATA pode dar suporte ao monitoramento de vários controladores de domínio, dependendo da quantidade de tráfego de rede para e a partir dos controladores de domínio.
Para obter mais informações, consulte [Planejamento de capacidade de ATA](ata-capacity-planning.md).

### Configurações da energia
Para ter um melhor desempenho, defina a **Opção de Energia** do Gateway de ATA para **Alto Desempenho**.

### Sincronização da hora
O servidor do ATA Center e o servidor do Gateway do ATA devem ter a hora sincronizada para 5 minutos entre si.

E mais, o Gateway do ATA e os controladores de domínio conectados devem ter a hora sincronizada para 5 minutos entre si.

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
    > -   Configure o espelhamento de porta do adaptador de captura como o destino do tráfego de rede do controlador de domínio. Confira [Configurar o espelhamento de porta](configure-port-mirroring.md) para obter mais informações. Normalmente, você precisará trabalhar com a equipe de virtualização ou de rede para configurar o espelhamento de porta.
    > -   Configure um endereço IP não roteável estático para seu ambiente sem um gateway padrão e endereço do servidor DNS. Por exemplo, 1.1.1.1/32. Isso irá assegurar que o adaptador da rede de captura poderá capturar a quantidade máxima de tráfego e que o adaptador da rede de gerenciamento será usado para enviar e receber o tráfego de rede requerido.

### Portas
A tabela a seguir lista as portas mínimas que o Gateway de ATA requer configuradas no adaptador de gerenciamento.

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
|SSL|TCP|443 ou como configurado para o Serviço da Central|ATA Center:<br /><br />- Endereço IP do Serviço de Central<br />-   Endereço IP do IIS|Saída|
|Syslog (opcional)|UDP|514|Servidor SIEM|Entrada|

> [!NOTE]
> Como parte do processo de resolução feito pelo Gateway de ATA, as seguintes portas precisam ser a entrada nos dispositivos na rede a partir dos Gateways de ATA.
>
> -   NTLM via RPC
> -   NetBIOS

### Certificados
Para facilitar a instalação da Central de ATA, você pode instalar os certificados autoassinados durante a instalação da Central de ATA. Após a implantação, você pode substituir o autoassinado pelo certificado de uma Autoridade de Certificação interna a ser usado pelo Gateway de ATA.

> [!NOTE]
> Os certificados autoassinados devem ser usados somente para a implantação de laboratório.

Um certificado que oferece suporte para a **Autenticação do Servidor** precisa ser instalado no armazenamento do Computador do Gateway de ATA no armazenamento do Computador Local. A Central de ATA deve confiar nesse certificado.

## Console do ATA
O acesso ao Console do ATA é por meio de um navegador com suporte para o seguinte:

-   Internet Explorer versão 10 e posterior

-   Google Chrome 40 e posterior

-   Resolução de largura mínima da tela de 1.700 pixels

## Consulte também
- [Arquitetura do ATA](/advanced-threat-analytics/Understand/ata-architecture)
- [Instalar o ATA](/advanced-threat-analytics/DeployUse/install-ata)
- [Para obter suporte, confira nosso fórum!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


