---
title: Instalação do Advanced Threat Analytics – Etapa 6 | Microsoft Docs
description: Nesta etapa da instalação do ATA, você configura fontes de dados.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: a347d8666ee8c2628592b8d4c866defd85d67ff8
ms.sourcegitcommit: b283bf66e63d76e6dba4564a229e804792794c6d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/29/2018
ms.locfileid: "47453981"
---
*Aplica-se a: Advanced Threat Analytics versão 1.9*



# <a name="install-ata---step-6"></a>Instalação do ATA - Etapa 6

> [!div class="step-by-step"]
> [«Etapa 5](install-ata-step5.md)
> [Etapa 7»](vpn-integration-install-step.md)

## <a name="step-6-configure-event-collection"></a>Etapa 6. Configurar coleta de eventos
### <a name="configure-event-collection"></a>Configurar coleta de eventos
Para aprimorar as funcionalidades de detecção, o ATA precisa dos seguintes eventos do Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757 e 7045. Eles podem ser lidos automaticamente pelo Gateway Lightweight do ATA ou no caso de o Gateway Lightweight do ATA não estar implantado, podem ser encaminhados para o Gateway do ATA de duas maneiras: configurando o Gateway do ATA para escutar o SIEM ou [Configurando o Encaminhamento de Eventos do Windows](configure-event-collection.md). 

> [!NOTE]
> Para as versões 1.8 e mais recentes do ATA, a configuração de coleta de eventos não é mais necessária para Gateways Lightweight do ATA. O Gateway Lightweight do ATA poderá ler eventos localmente, sem a necessidade de configurar o encaminhamento de eventos.

Além de coletar e analisar o tráfego de rede para e nos controladores de domínio, o ATA pode usar os eventos do Windows para aprimorar ainda mais as detecções. Ele usa o evento 4776 para NTLM que melhora várias detecções e os eventos 4732, 4733, 4728, 4729, 4756 e 4757 para aprimorar a detecção de modificações de grupo confidencial. Isso pode ser recebido de seu SIEM definindo o Encaminhamento de Eventos do Windows no controlador de domínio. Os eventos coletados fornecem à ATA informações adicionais que não estão disponíveis por meio do tráfego de rede do controlador de domínio.

#### <a name="siemsyslog"></a>SIEM/Syslog
Para o ATA poder consumir dados de um servidor Syslog, você precisa executar as seguintes etapas:

-   Configurar seus servidores do Gateway do ATA para escutar e aceitar eventos encaminhados do servidor SIEM/Sylog.
> [!NOTE]
> ATA escuta somente IPv4, não IPv6. 
-   Configurar seu servidor Syslog/SIEM para encaminhar eventos específicos ao Gateway do ATA.

> [!IMPORTANT]
> -   Não encaminhe todos os dados de Syslog para o Gateway do ATA.
> -   O ATA oferece suporte ao tráfego UDP do servidor SIEM/Syslog.

Consulte a documentação de produto do seu servidor SIEM/Syslog para saber como configurar o encaminhamento de eventos específicos para outro servidor. 

> [!NOTE]
>Se você não usa um servidor Syslog/SIEM, é possível configurar os controladores de domínio do Windows para encaminhar a ID de Evento do Windows 4776 para ser coletada e analisada pelo ATA. A ID de Evento do Windows 4776 fornece dados sobre autenticações NTLM.

#### <a name="configuring-the-ata-gateway-to-listen-for-siem-events"></a>Configuração do Gateway de ATA para escutar eventos SIEM

1.  Na configuração do ATA, em **Fontes de dados** clique em **SIEM**, ative **Syslog** e clique em **Salvar**.

    ![Habilitar a imagem UDP de ouvinte de syslog](media/ATA-enable-siem-forward-events.png)

2.  Configure o servidor Syslog ou SIEM para encaminhar a ID de Evento do Windows 4776 para o endereço IP de um dos Gateways ATA. Para saber mais sobre como configurar o SIEM, confira a ajuda online do SIEM ou opções de suporte técnico para obter os requisitos de formatação específica para cada servidor SIEM.

O ATA oferece suporte a eventos de SIEM nos seguintes formatos:  

#### <a name="rsa-security-analytics"></a>Análise de Segurança do RSA
&lt;Cabeçalho do Syslog&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   O cabeçalho do Syslog é opcional.

-   o separador de caractere "\n" é necessário entre todos os campos.

-   Os campos, em ordem, são:

    1.  Constante RsaSA (deve aparecer).

    2.  O carimbo de hora do evento real (verifique se ele não é o carimbo de hora de chegada no SIEM, ou do envio para o ATA). Preferencialmente com a precisão em milissegundos, isso é importante.

    3.  A ID de evento do Windows

    4.  O nome do provedor de eventos do Windows

    5.  O nome do log de eventos do Windows

    6.  O nome do computador que está recebendo o evento (o controlador de domínio neste caso)

    7.  O nome do usuário que está autenticando

    8.  O nome do host de origem

    9. O código resultante do NTLM

-   A ordem é importante, e nada mais deve ser incluído na mensagem.

#### <a name="hp-arcsight"></a>HP Arcsight
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|O controlador de domínio tentou validar as credenciais de uma conta.|Baixo| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Motivo ou Código de erro

-   Deve estar em conformidade com a definição de protocolo.

-   Nenhum cabeçalho de syslog.

-   A parte do cabeçalho (a parte separada por uma barra vertical) deve existir (conforme mencionado no protocolo).

-   As seguintes chaves na parte _Extensão_ devem estar presentes no evento:

    -   externalId = a ID de evento do Windows

    -   rt = o carimbo de hora do evento real (verifique se ele não é o carimbo de hora de chegada no SIEM, ou do envio para o ATA). Preferencialmente com a precisão em milissegundos, isso é importante.

    -   cat = o nome do log de eventos do Windows

    -   shost = o nome do host de origem

    -   dhost = o computador que está recebendo o evento (o controlador de domínio neste caso)

    -   duser = o usuário que está autenticando

-   A ordem não é importante para a parte _Extensão_

-   Deve haver uma chave personalizada e um keyLable para esses dois campos:

    -   “EventSource”

    -   “Motivo ou Código de erro” = o código resultante do NTLM

#### <a name="splunk"></a>Splunk
&lt;Cabeçalho do Syslog&gt;\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

O computador tentou validar as credenciais de uma conta.

Pacote de autenticação:              MICROSOFT_AUTHENTICATION_PACKAGE_V1_0

Conta de Logon: Administrador

Estação de Trabalho de Origem:       SIEM

Código de erro:         0x0

-   O cabeçalho do Syslog é opcional.

-   Há um separador de caracteres "\r\n" entre todos os campos obrigatórios.

-   Os campos estão no formato chave=valor.

-   As chaves a seguir devem existir e ter um valor:

    -   EventCode = a ID de evento do Windows

    -   Logfile = o nome do log de eventos do Windows

    -   SourceName = o nome do provedor de eventos do Windows

    -   TimeGenerated = O carimbo de hora do evento real (verifique se não é o carimbo de hora de chegada no SIEM, ou do envio para o ATA). O formato deve corresponder a aaaaMMddHHmmss.FFFFFF, preferencialmente com precisão de milissegundos, isso é importante.

    -   ComputerName = o nome do host de origem

    -   Mensagem = o texto do evento original do evento do Windows

-   A Chave da Mensagem e o valor DEVEM ser os últimos.

-   A ordem não é importante para os pares de chave=valor

#### <a name="qradar"></a>QRadar
O QRadar permite a coleta de eventos por meio de um agente. Se os dados forem reunidos usando um agente, o formato de hora será coletado sem dados de milissegundos. Uma vez que o ATA precisa dos dados de milissegundos, é necessário definir o QRadar para usar a coleta de eventos do Windows sem agente. Para obter mais informações, veja [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: Agentless Windows Events Collection using the MSRPC Protocol") (QRadar: Coleção de eventos do Windows sem agente usando o protocolo MSRPC).

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

Os campos necessários são:

- O tipo de agente para a coleta
- O nome do provedor do log de eventos do Windows
- A fonte do log de eventos do Windows
- O nome de domínio totalmente qualificado do DC
- A ID de evento do Windows

TimeGenerated é o carimbo de data/hora do evento real (verifique se não é o carimbo de data/hora de chegada no SIEM, ou do envio para o ATA). O formato deve corresponder a aaaaMMddHHmmss.FFFFFF, preferencialmente com precisão de milissegundos, isso é importante.

A mensagem é o texto do evento original do evento do Windows

Certifique-se de ter \t entre os pares de chave=valor.

>[!NOTE] 
> Não há suporte ao uso do WinCollect para a coleta de eventos do Windows.



> [!div class="step-by-step"]
> [«Etapa 5](install-ata-step5.md)
> [Etapa 7»](vpn-integration-install-step.md)



## <a name="related-videos"></a>Vídeos Relacionados
- [Visão geral da implantação do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Como escolher o tipo certo de Gateway do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Consulte Também
- [Guia de implantação da POC (prova de conceito) do ATA](http://aka.ms/atapoc)
- [Ferramenta de dimensionamento do ATA](http://aka.ms/atasizingtool)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)

