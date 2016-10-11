---
title: Configurar coleta de eventos | Microsoft ATA
description: "Descreve as opções para configurar a coleta de eventos com o ATA"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 09/28/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d2c1c00ff649557c1a0a16385e025c9d597c3bbf
ms.openlocfilehash: 91ce3a3fef27673712a708aa1e92c32298cedd84


---

*Aplica-se a: Advanced Threat Analytics versão 1.6 e 1.7*



# Configurar coleta de eventos
Para aprimorar os recursos de detecção, o ATA precisa da ID 4776 do log de Eventos do Windows. Isso pode ser encaminhado o Gateway do ATA usando uma entre duas maneiras, configurando o Gateway do ATA para escutar eventos SIEM ou [Configurando o encaminhamento de eventos do Windows](#configuring-windows-event-forwarding).

## Coleta de eventos
Além de coletar e analisar o tráfego de rede para e a partir dos controladores de domínio, o ATA pode usar o evento 4776 do Windows para aprimorar a detecção da Passagem de Hash do ATA. Isso pode ser recebido de seu SIEM ou definindo o Encaminhamento de Eventos do Windows no controlador de domínio. Os eventos coletados fornecem à ATA informações adicionais que não estão disponíveis por meio do tráfego de rede do controlador de domínio.

### SIEM/Syslog
Para o ATA poder consumir dados de um servidor Syslog, você precisa fazer o seguinte:

-   Configurar seus servidores do Gateway do ATA para escutar e aceitar eventos encaminhados do servidor SIEM/Sylog.

-   Configurar seu servidor Syslog/SIEM para encaminhar eventos específicos ao Gateway do ATA.

> [!IMPORTANT]
> -   Não encaminhe todos os dados de Syslog para o Gateway do ATA.
> -   O ATA oferece suporte ao tráfego UDP do servidor SIEM/Syslog.

Consulte a documentação de produto do seu servidor SIEM/Syslog para saber como configurar o encaminhamento de eventos específicos para outro servidor. 

### Encaminhamento de eventos do Windows
Se você não usa um servidor Syslog/SIEM, é possível configurar os controladores de domínio do Windows para encaminhar a ID de Evento do Windows 4776 para ser coletada e analisada pelo ATA. A ID de Evento do Windows 4776 fornece dados sobre autenticações NTLM.

## Configuração do Gateway de ATA para escutar eventos SIEM

1.  Na configuração de ATA, na guia "Eventos", habilite **Syslog** e pressione **Salvar**.

    ![Habilitar a imagem UDP de ouvinte de syslog](media/ATA-enable-siem-forward-events.png)

2.  Configure o servidor Syslog ou SIEM para encaminhar a ID de Evento do Windows 4776 para o endereço IP de um dos Gateways ATA. Para saber mais sobre como configurar o SIEM, consulte a ajuda online do SIEM ou opções de suporte técnico para obter os requisitos de formatação específica para cada servidor SIEM.

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

### Configuração de WEF para Gateway do ATA com o espelhamento de porta

Após a configuração do espelhamento de porta nos controladores de domínio para o Gateway do ATA, siga as instruções abaixo para configurar o Encaminhamento de eventos do Windows usando a configuração Iniciada pela Origem. Essa é uma maneira para configurar o Encaminhamento de eventos do Windows. 

**Etapa 1: Adicionar a conta de serviço de rede ao Grupo de leitores de log de eventos de domínio.** 

Nesse cenário, supomos que o Gateway ATA seja membro do domínio.

1.  Abra os Usuários e Computadores do Active Directory, navegue até a pasta **BuiltIn** e clique duas vezes em **Leitores de Log de Eventos**. 
2.  Selecione **Membros**.
4.  Se **Serviço de Rede** não estiver listado, clique em **Adicionar**, digite **Serviço de Rede** no campo **Digite os nomes de objeto a serem selecionados **. Depois, clique em **Verificar Nomes** e clique em **OK** duas vezes. 

**Etapa 2: Criar uma política nos controladores de domínio para definir a configuração Configurar o Gerenciador de assinatura de destino.** 
> [!Note] 
> Você pode criar uma política de grupo para essas configurações e aplicá-la a cada controlador de domínio monitorado pelo Gateway do ATA. As etapas a seguir modificarão a política local do controlador de domínio.     

1.  Execute o seguinte comando em cada controlador de domínio: *winrm quickconfig*
2.  Em um prompt de comando, digite *gpedit.msc*.
3.  Expanda **Configuração do Computador > Modelos Administrativos > Componentes do Windows > Encaminhamento de Evento**

 ![Imagem do editor de grupo de política local](media/wef 1 local group policy editor.png)

4.  Clique duas vezes em **Configurar Gerenciador de assinatura de destino**.
   
    1.  Selecione **Habilitado**.
    2.  Em **Opções**, clique em **Mostrar**.
    3.  Em **SubscriptionManagers**, insira o seguinte valor e clique em **OK**:  *Server=http://<fqdnATAGateway>:5985/wsman/SubscriptionManager/WEC,Refresh=10* (Por exemplo: Server=http://atagateway9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10)
 
   ![Configurar a imagem de assinatura de destino](media/wef 2 config target sub manager.png)
   
    5.  Clique em **OK**.
    6.  Em um prompt de comandos com privilégios elevados, digite *gpupdate /force*. 

**Etapa 3: Executar as seguintes etapas no Gateway do ATA** 

1.  Em um prompt de comandos com privilégios elevados, digite *wecutil qc*
2.  Abra o **Visualizador de Eventos**. 
3.  Clique com o botão direito em **Assinaturas** e selecione **Criar Assinatura**. 

   1.   Insira um nome e uma descrição para a assinatura. 
   2.   Para **Log de Destino** confirme se **Eventos Encaminhados** está selecionado. Para o ATA ler os eventos, o log de destino deve ser **Eventos Encaminhados**. 
   3.   Selecione **Iniciado pelo computador de origem** e clique em **Selecionar Grupos de Computadores**.
        1.  Clique em **Adicionar Computador do Domínio**.
        2.  Insira o nome do controlador de domínio no campo **Digite o nome do objeto a ser selecionado**. Depois, clique em **Verificar Nomes** e clique em **OK**. 
       
        ![Imagem do Visualizador de Eventos](media/wef3 event viewer.png)
   
        
        3.  Clique em **OK**.
   4.   Clique em **Selecionar Eventos**.

        1. Clique em **Pelo log** e selecione **Segurança**.
        2. No campo **Inclui/Exclui ID do Evento**, digite **4776** e clique em **OK**. 

 ![Imagem do filtro de consulta](media/wef 4 query filter.png)

   5.   Clique com o botão direito na assinatura criada e selecione **Status de Tempo de Execução** para verificar se há problemas com o status. 
   6.   Depois de alguns minutos, verifique se o evento 4776 aparece nos Eventos Encaminhados no Gateway do ATA.


### Configuração do WEF para o Gateway de Lightweight do ATA
Ao instalar o Gateway Lightweight do ATA nos controladores de domínio, você pode configurar os controladores de domínio para encaminhar eventos para si mesmo. Execute as etapas a seguir para configurar o Encaminhamento de Eventos do Windows ao usar o Gateway Lightweight do ATA. Essa é uma maneira para configurar o Encaminhamento de eventos do Windows.  

**Etapa 1: Adicionar a conta de serviço de rede ao Grupo de leitores de log de eventos de domínio** 

1.  Abra os Usuários e Computadores do Active Directory, navegue até a pasta **BuiltIn** e clique duas vezes em **Leitores de Log de Eventos**. 
2.  Selecione **Membros**.
3.  Se **Serviço de Rede** não estiver listado, clique em **Adicionar** e digite **Serviço de Rede** no campo **Digite os nomes de objeto a serem selecionados **. Depois, clique em **Verificar Nomes** e clique em **OK** duas vezes. 

**Etapa 2: Executar as seguintes etapas no controlador de domínio depois que o Gateway Lightweight do ATA estiver instalado** 

1.  Em um prompt de comandos com privilégios elevados, digite *winrm quickconfig* e *wecutil qc* 
2.  Abra o **Visualizador de Eventos**. 
3.  Clique com o botão direito em **Assinaturas** e selecione **Criar Assinatura**. 

   1.   Insira um nome e uma descrição para a assinatura. 
   2.   Para **Log de Destino** confirme se **Eventos Encaminhados** está selecionado. Para o ATA ler os eventos, o log de destino deve ser Eventos Encaminhados.

        1.  Selecione **Coletor iniciado** e clique em **Selecionar Computadores**. Depois, clique em **Adicionar Computador do Domínio**.
        2.  Insira o nome do controlador de domínio em **Digite o nome do objeto a ser selecionado**. Depois, clique em **Verificar Nomes** e clique em **OK**.

            ![Imagem das propriedades da assinatura](media/wef 5 sub properties computers.png)

        3.  Clique em **OK**.
   3.   Clique em **Selecionar Eventos**.

        1.  Clique em **Pelo log** e selecione **Segurança**.
        2.  Em **Inclui/Exclui ID do Evento**, digite *4776* e clique em **OK**. 

![Imagem do filtro de consulta](media/wef 4 query filter.png)


  4.    Clique com o botão direito na assinatura criada e selecione **Status de Tempo de Execução** para verificar se há problemas com o status. 

> [!Note] 
> Talvez seja necessário reiniciar o controlador de domínio antes que a configuração tenha efeito. 

Depois de alguns minutos, verifique se o evento 4776 aparece nos Eventos Encaminhados no Gateway do ATA.



Para obter mais informações, confira: [Configurar computadores para encaminhar e coletar eventos](https://technet.microsoft.com/library/cc748890)

## Consulte Também
- [Instalar o ATA](install-ata.md)
- [Confira o fórum do ATA!!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Sep16_HO4-->


