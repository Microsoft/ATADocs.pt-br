---
title: Configurar coleta de eventos | Microsoft ATA
description: "Descreve as opções para configurar a coleta de eventos com o ATA"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 6876339e1303438da10a56e23d8eb831cc17050c


---

# Configurar coleta de eventos
Para aprimorar os recursos de detecção, o ATA precisa da ID 4776 do log de Eventos do Windows. Isso pode ser encaminhado o Gateway do ATA usando uma entre duas maneiras, configurando o Gateway do ATA para escutar eventos SIEM ou [Configurando o encaminhamento de eventos do Windows](#configuring-windows-event-forwarding).

## Coleta de eventos
Além de coletar e analisar o tráfego de rede para e a partir dos controladores de domínio, o ATA pode usar o evento 4776 do Windows para aprimorar a detecção da Passagem de Hash do ATA. Isso pode ser recebido de seu SIEM ou definindo o Encaminhamento de Eventos do Windows no controlador de domínio. Os eventos coletados fornecem à ATA informações adicionais que não estão disponíveis por meio do tráfego de rede do controlador de domínio.

### SIEM/Syslog
Para o ATA poder consumir dados de um servidor Syslog, você precisa fazer o seguinte:

-   Configurar um dos servidores do Gateway do ATA para escutar e aceitar eventos encaminhados do servidor SIEM/Sylog.

-   Configurar seu servidor Syslog/SIEM para encaminhar eventos específicos ao Gateway do ATA.

> [!IMPORTANT]
> -   Não encaminhe todos os dados de Syslog para o Gateway do ATA.
> -   O ATA oferece suporte ao tráfego UDP do servidor SIEM/Syslog.

Consulte a documentação de produto do seu servidor SIEM/Syslog para saber como configurar o encaminhamento de eventos específicos para outro servidor. 

### Encaminhamento de eventos do Windows
Se você não usa um servidor Syslog/SIEM, é possível configurar os controladores de domínio do Windows para encaminhar a ID de Evento do Windows 4776 para ser coletada e analisada pelo ATA. A ID de Evento do Windows 4776 fornece dados sobre autenticações NTLM.

## Configuração do Gateway de ATA para escutar eventos SIEM

1.  Na configuração do Gateway do ATA, habilite **UDP de Ouvinte de Syslog**.

    Defina o Endereço IP de Escuta conforme descrito na figura abaixo. A porta padrão é a 514.

    ![Habilitar a imagem UDP de ouvinte de syslog](media/ATA-enable-siem-forward-events.png)

2.  Configure o servidor Syslog ou SIEM para encaminhar a ID de Evento do Windows 4776 para o endereço IP selecionado acima. Para saber mais sobre como configurar o SIEM, consulte a ajuda online do SIEM ou opções de suporte técnico para obter os requisitos de formatação específica para cada servidor SIEM.

### Suporte a SIEM
O ATA oferece suporte a eventos de SIEM nos seguintes formatos:

#### Análise de Segurança do RSA
&lt;Cabeçalho do syslog&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   O cabeçalho do Syslog é opcional.

-   o separador de caractere "\n" é necessário entre todos os campos.

-   Os campos, em ordem, são:

    1.  Constante RsaSA (deve aparecer).

    2.  O carimbo de hora do evento real (verifique se ele não é o carimbo de hora de chegada no SIEM, ou do envio para o ATA). Preferência de precisão em milissegundos, isso é muito importante.

    3.  A ID de evento do Windows

    4.  O nome do provedor de eventos do windows

    5.  O nome do log de eventos do Windows

    6.  O nome do computador que está recebendo o evento (o controlador de domínio neste caso)

    7.  O nome do usuário que está autenticando

    8.  O nome do host de origem

    9. O código resultante do NTLM

-   A ordem é importante, e nada mais deve ser incluído na mensagem.

#### HP Arcsight
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|O controlador de domínio tentou validar as credenciais de uma conta.|Baixo| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Motivo ou Código de erro

-   Deve estar em conformidade com a definição de protocolo.

-   Nenhum cabeçalho de syslog.

-   A parte do cabeçalho (a parte separada por uma barra vertical) deve existir (conforme mencionado no protocolo).

-   As seguintes chaves na parte _Extensão_ devem estar presentes no evento:

    -   externalId = a ID de evento do Windows

    -   rt = o carimbo de hora do evento real (verifique se ele não é o carimbo de hora de chegada no SIEM, ou do envio para nós). Preferência de precisão em milissegundos, isso é muito importante.

    -   cat = o nome do log de eventos do Windows

    -   shost = o nome do host de origem

    -   dhost = o computador que está recebendo o evento (o controlador de domínio neste caso)

    -   duser = o usuário que está autenticando

-   A ordem não é importante para a parte _Extensão_

-   Deve haver uma chave personalizada e um keyLable para esses dois campos:

    -   “EventSource”

    -   “Motivo ou Código de erro” = o código resultante do NTLM

#### Splunk
&lt;Cabeçalho do syslog&gt;\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

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

    -   TimeGenerated = O carimbo de hora do evento real (verifique se não é o carimbo de hora de chegada no SIEM, ou do envio para o ATA). O formato deve corresponder a yyyyMMddHHmmss.FFFFFF, preferencialmente com precisão de milissegundos, isso é muito importante.

    -   ComputerName = o nome do host de origem

    -   Mensagem = o texto do evento original do evento do Windows

-   A Chave da Mensagem e o valor DEVEM ser os últimos.

-   A ordem não é importante para os pares de chave=valor

#### QRadar
O QRadar permite a coleta de eventos por meio de um agente. Se os dados forem reunidos usando um agente, o formato de hora será coletado sem dados de milissegundos. Uma vez que o ATA precisa dos dados de milissegundos, é necessário definir o QRadar para usar a coleta de eventos do Windows sem agente. Para obter mais informações, confira [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: Agentless Windows Events Collection using the MSRPC Protocol").

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

Os campos necessários são:

- O tipo de agente para a coleta
- O nome do provedor do log de eventos do Windows
- A fonte do log de eventos do Windows
- O nome de domínio totalmente qualificado do DC
- A ID de evento do Windows

TimeGenerated é o carimbo de data/hora do evento real (verifique se não é o carimbo de data/hora de chegada no SIEM, ou do envio para o ATA). O formato deve corresponder a aaaaMMddHHmmss.FFFFFF, preferencialmente com precisão de milissegundos, isso é muito importante.

A mensagem é o texto do evento original do evento do Windows

Certifique-se de ter \t entre os pares de chave=valor.

>[!NOTE] 
> Não há suporte ao uso do WinCollect para a coleta de eventos do Windows.

## Configuração do encaminhamento de eventos do Windows
Se você não tiver um servidor SIEM, configure os controladores de domínio para encaminhar a ID de Evento do Windows 4776 diretamente para um dos seus Gateways do ATA.

1.  Faça logon em todos os controladores de domínio e máquinas do Gateway do ATA usando uma conta de domínio com privilégios de administrador.
2. Verifique se todos os controladores de domínio e Gateways do ATA que você está conectando estão associados ao mesmo domínio.
3.  Em cada controlador de domínio, digite o seguinte em um prompt de comando elevado:
```
winrm quickconfig
```
4.  No Gateway do ATA, digite o seguinte em um prompt de comando elevado:
```
wecutil qc
```
5.  Em cada controlador de domínio, em **Usuários e Computadores do Active Directory**, navegue até a pasta **Builtin** e clique duas vezes no grupo **Leitores de Log de Eventos**.<br>
![wef_ad_eventlogreaders](media/wef_ad_eventlogreaders.png)<br>
Clique com o botão direito e selecione **Propriedades**. Na guia **Membros**, adicione a conta de computador de cada Gateway do ATA.
![wef_ad event log reader popup](media/wef_ad-event-log-reader-popup.png)
6.  No Gateway do ATA, abra o Visualizador de Eventos e clique com o botão direito em **Assinaturas** e escolha **Criar Assinatura**.  

    a. Em **Tipo de assinatura e computadores de origem**, clique em **Selecionar Computadores**, adicione os controladores de domínio e teste a conectividade.
    ![wef_subscription prop](media/wef_subscription-prop.png)

    b. Em **Eventos a serem coletados**, clique em **Selecionar Eventos**. Selecione **Pelo log** e role a tela selecionar **Segurança**. Em seguida, em **Inclui/Exclui Identificações de Evento**, digite **4776**.<br>
    ![wef_4776](media/wef_4776.png)

    c. Em **Alterar a conta de usuário ou definir configurações avançadas**, clique em **Avançado**.
Defina o **Protocolo** como **HTTP** e a **Porta** como **5985**.<br>
    ![wef_http](media/wef_http.png)

7.  [Opcional] Se você quiser um intervalo de sondagem menor, no Gateway do ATA, defina a pulsação da assinatura como 5 segundos para uma taxa de sondagem mais rápida.
    wecutil ss <CollectionName>/cm:custom wecutil ss <CollectionName> /hi:5000

8. Na página de configuração do Gateway do ATA, habilite **Coleta de Encaminhamento de Eventos do Windows**.

> [!NOTE]
> Quando você habilitar essa configuração, o Gateway do ATA procurará no log de Eventos Encaminhados por Eventos do Windows que foram encaminhados a ele pelos controladores de domínio.

Para obter mais informações, confira: [Configurar computadores para encaminhar e coletar eventos](https://technet.microsoft.com/library/cc748890)

## Consulte também
- [Instalar o ATA](install-ata.md)
- [Confira o fórum do ATA!!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=Jul16_HO3-->


