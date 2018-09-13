---
title: Instalar a Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Nesta etapa da instalação do ATP, você configura fontes de dados.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/15/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 88692d1a-45a3-4d54-a549-4b5bba6c037b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 91e3caf8e15313069e4c2cec194a11855fd45c24
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44126171"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*



# <a name="configure-event-collection"></a>Configurar coleta de eventos

Para aprimorar as funcionalidades de detecção, o Azure ATP precisa dos seguintes eventos do Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757 e 7045. Eles podem ser lidos automaticamente pelo sensor do Azure ATP ou, caso o sensor do Azure ATP não esteja implantado, ele poderá ser encaminhado para o sensor autônomo do Azure ATP de duas maneiras: configurando o sensor autônomo do Azure ATP para escutar eventos do SIEM ou [Configurando o Encaminhamento de Eventos do Windows](configure-event-forwarding.md).

> [!NOTE]
> É importante executar o script de auditoria do ATA antes de configurar a coleta de eventos para garantir que os controladores de domínio estejam configurados corretamente para registrar os eventos necessários. 

Além de coletar e analisar o tráfego de rede para e dos controladores de domínio, o Azure ATP pode usar eventos do Windows para aprimorar ainda mais as detecções. Ele usa o evento 4776 para NTLM, o que melhora várias detecções e os eventos 4732, 4733, 4728, 4729, 4756, 4757 e 7045 para aprimorar a detecção de modificações de grupos confidenciais e a criação de serviços. Isso pode ser recebido de seu SIEM definindo o Encaminhamento de Eventos do Windows no controlador de domínio. Os eventos coletados fornecem ao Azure ATP informações adicionais que não estão disponíveis por meio do tráfego de rede do controlador de domínio.

## <a name="siemsyslog"></a>SIEM/Syslog
Para que o Azure ATP possa consumir dados de um servidor Syslog, você precisa executar as seguintes etapas:

-   Configurar seus servidores do sensor do Azure ATP para escutar e aceitar eventos encaminhados do servidor de SIEM/Sylog.

 > [!NOTE]
 > O Azure ATP escuta somente IPv4, não IPv6. 

-   Configurar seu servidor de SIEM/Syslog para encaminhar eventos específicos ao sensor do Azure ATP.

> [!IMPORTANT]
> -   Não encaminhe todos os dados de Syslog para o sensor do Azure ATP.
> -   O Azure ATP dá suporte ao tráfego de UDP do servidor de SIEM/Syslog.

Consulte a documentação de produto do seu servidor SIEM/Syslog para saber como configurar o encaminhamento de eventos específicos para outro servidor. 

> [!NOTE]
>Caso não use um servidor de SIEM/Syslog, você pode configurar os controladores de domínio do Windows para encaminhar todos os eventos necessários para serem coletados e analisados pelo ATA.

## <a name="configuring-the-azure-atp-sensor-to-listen-for-siem-events"></a>Configuração do sensor do Azure ATP para escutar eventos de SIEM

1.  Na configuração do Azure ATP, em **Fontes de dados**, clique em **SIEM**, ative **Syslog** e clique em **Salvar**.

    ![Habilitar a imagem UDP de ouvinte de syslog](media/atp-siem-config.png)

2.  Configure o servidor de Syslog ou SIEM para encaminhar todos os eventos necessários para o endereço IP de um dos sensores do Azure ATP. Para saber mais sobre como configurar o SIEM, confira a ajuda online do SIEM ou opções de suporte técnico para obter os requisitos de formatação específica para cada servidor SIEM.

O Azure ATP dá suporte a eventos de SIEM nos seguintes formatos:  

## <a name="rsa-security-analytics"></a>Análise de Segurança do RSA
&lt;Cabeçalho do Syslog&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   O cabeçalho do Syslog é opcional.

-   o separador de caractere "\n" é necessário entre todos os campos.

-   Os campos, em ordem, são:

    1.  Constante RsaSA (deve aparecer).

    2.  O carimbo de data/hora do evento real (certifique-se de que não é o carimbo de data/hora da chegada ao SIEM ou do envio ao ATP). Preferencialmente com a precisão em milissegundos, isso é importante.

    3.  A ID de evento do Windows

    4.  O nome do provedor de eventos do Windows

    5.  O nome do log de eventos do Windows

    6.  O nome do computador que está recebendo o evento (o controlador de domínio neste caso)

    7.  O nome do usuário que está autenticando

    8.  O nome do host de origem

    9. O código resultante do NTLM

-   A ordem é importante, e nada mais deve ser incluído na mensagem.

## <a name="hp-arcsight"></a>HP Arcsight
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|O controlador de domínio tentou validar as credenciais de uma conta.|Baixo| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Motivo ou Código de erro

-   Deve estar em conformidade com a definição de protocolo.

-   Nenhum cabeçalho de syslog.

-   A parte do cabeçalho (a parte separada por uma barra vertical) deve existir (conforme mencionado no protocolo).

-   As seguintes chaves na parte _Extensão_ devem estar presentes no evento:

    -   externalId = a ID de evento do Windows

    -   rt = o carimbo de data/hora do evento real (certifique-se de que não é o carimbo de data/hora da chegada ao SIEM ou do envio ao ATP). Preferencialmente com a precisão em milissegundos, isso é importante.

    -   cat = o nome do log de eventos do Windows

    -   shost = o nome do host de origem

    -   dhost = o computador que está recebendo o evento (o controlador de domínio neste caso)

    -   duser = o usuário que está autenticando

-   A ordem não é importante para a parte _Extensão_

-   Deve haver uma chave personalizada e um keyLable para esses dois campos:

    -   “EventSource”

    -   “Motivo ou Código de erro” = o código resultante do NTLM

## <a name="splunk"></a>Splunk
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

    -   TimeGenerated = o carimbo de data/hora do evento real (certifique-se de que não é o carimbo de data/hora da chegada ao SIEM ou do envio para o ATP). O formato deve corresponder a aaaaMMddHHmmss.FFFFFF, preferencialmente com precisão de milissegundos, isso é importante.

    -   ComputerName = o nome do host de origem

    -   Mensagem = o texto do evento original do evento do Windows

-   A Chave da Mensagem e o valor DEVEM ser os últimos.

-   A ordem não é importante para os pares de chave=valor

## <a name="qradar"></a>QRadar
O QRadar permite a coleta de eventos por meio de um agente. Se os dados forem reunidos usando um agente, o formato de hora será coletado sem dados de milissegundos. Uma vez que o Azure ATP precisa de dados de milissegundos, é necessário configurar o QRadar para usar a coleta de eventos do Windows sem agente. Para obter mais informações, veja [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: Agentless Windows Events Collection using the MSRPC Protocol") (QRadar: Coleção de eventos do Windows sem agente usando o protocolo MSRPC).

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

Os campos necessários são:

- O tipo de agente para a coleta
- O nome do provedor do log de eventos do Windows
- A fonte do log de eventos do Windows
- O nome de domínio totalmente qualificado do DC
- A ID de evento do Windows

TimeGenerated é o carimbo de data/hora do evento real (certifique-se de que não é o carimbo de data/hora da chegada ao SIEM ou do envio para o ATP). O formato deve corresponder a aaaaMMddHHmmss.FFFFFF, preferencialmente com precisão de milissegundos, isso é importante.

A mensagem é o texto do evento original do evento do Windows

Certifique-se de ter \t entre os pares de chave=valor.

>[!NOTE] 
> Não há suporte ao uso do WinCollect para a coleta de eventos do Windows.




## <a name="see-also"></a>Consulte Também
- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/aatpsizingtool)
- [Referência de logs de SIEM do Azure ATP](cef-format-sa.md)
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)
