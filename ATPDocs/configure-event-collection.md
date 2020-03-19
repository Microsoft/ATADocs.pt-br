---
title: Instalar a Proteção Avançada contra Ameaças do Azure
description: Nesta etapa da instalação do ATP, você configura fontes de dados.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 03/15/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 88692d1a-45a3-4d54-a549-4b5bba6c037b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4e62f333ff64291cd2858b528897afc80c4f1f44
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2020
ms.locfileid: "79411501"
---
# <a name="configure-event-collection"></a>Configurar coleta de eventos

Para aprimorar as funcionalidades de detecção, ATP do Azure precisa dos seguintes eventos do Windows: 4726, 4728, 4729, 4730, 4732, 4733, 4743, 4753, 4756, 4757, 4758, 4763, 4776, 7045 e 8004. Esses eventos podem ser lidos automaticamente pelo sensor do Azure ATP ou, caso o sensor do Azure ATP não esteja implantado, ele poderá ser encaminhado para o sensor autônomo do Azure ATP de duas maneiras: configurando o sensor autônomo do Azure ATP para escutar eventos do SIEM ou [Configurando o encaminhamento de eventos do Windows](configure-event-forwarding.md).

> [!NOTE]
>
> - Os sensores autônomos do ATP do Azure não são compatíveis com todos os tipos de fonte de dados, resultando em detecções perdidas. Para cobertura completa do seu ambiente, é recomendável implantar o sensor do ATP do Azure.
> - É importante executar o script de auditoria do Azure ATP antes de configurar a coleta de eventos para garantir que os controladores de domínio estejam configurados corretamente para registrar os eventos necessários.

Além de coletar e analisar o tráfego de rede para e dos controladores de domínio, o Azure ATP pode usar eventos do Windows para aprimorar ainda mais as detecções. A ATP do Azure usa os eventos 4776 e 8004 para NTLM, o que melhora várias detecções, e os eventos 4732, 4733, 4728, 4729, 4756, 4757, 7045 e 8004 para aprimorar a detecção de modificações de grupos confidenciais e a criação de serviços. Eles podem ser recebidos de seu SIEM ou definindo o Encaminhamento de Eventos do Windows no controlador de domínio. Os eventos coletados fornecem ao Azure ATP informações adicionais que não estão disponíveis por meio do tráfego de rede do controlador de domínio.

## <a name="ntlm-authentication-using-windows-event-8004"></a>Autenticação NTLM usando o evento 8004 do Windows

Para configurar a coleção 8004 de eventos do Windows:

1. Navegue para: Configuração do computador\Políticas\ Configurações do Windows\Configurações de segurança\Políticas locais\Opções de segurança
2. Defina a **política de grupo do domínio** da seguinte forma:
    - Segurança de rede: restringir NTLM: tráfego de NTLM de saída para servidores remotos = **Auditar todos**
    - Segurança de rede: restringir NTLM: auditar a autenticação NTLM neste domínio = **Habilitar todos**
    - Segurança de rede: restringir NTLM: auditar o tráfego NTLM de entrada = **Habilitar a auditoria de todas as contas**

Quando o evento 8004 do Windows é analisado pelo sensor da ATP do Azure, as atividades de autenticação NTLM da ATP do Azure são aprimoradas com os dados acessados pelo servidor.

## <a name="siemsyslog"></a>SIEM/Syslog

Os sensores autônomos do ATP do Azure são configurados por padrão para receber dados Syslog. Para que os sensores autônomos do ATP do Azure consigam consumir esses dados, é necessário encaminhar seus dados Syslog para o sensor.

> [!NOTE]
> O Azure ATP escuta somente IPv4, não IPv6.

> [!IMPORTANT]
>
> - Não encaminhe todos os dados de Syslog para o sensor do Azure ATP.
> - O Azure ATP dá suporte ao tráfego de UDP do servidor de SIEM/Syslog.

Consulte a documentação de produto do seu servidor SIEM/Syslog para saber como configurar o encaminhamento de eventos específicos para outro servidor.

> [!NOTE]
> Caso não use um servidor de SIEM/Syslog, você pode configurar os controladores de domínio do Windows para encaminhar todos os eventos necessários para serem coletados e analisados pelo Azure ATP.

## <a name="configuring-the-azure-atp-sensor-to-listen-for-siem-events"></a>Configuração do sensor do Azure ATP para escutar eventos de SIEM

- Configure o servidor de Syslog ou SIEM para encaminhar todos os eventos necessários para o endereço IP de um dos sensores autônomos do ATP do Azure. Para saber mais sobre como configurar o SIEM, confira a ajuda online do SIEM ou opções de suporte técnico para obter os requisitos de formatação específica para cada servidor SIEM.

O Azure ATP dá suporte a eventos de SIEM nos seguintes formatos:

### <a name="rsa-security-analytics"></a>Análise de Segurança do RSA

&lt;Cabeçalho do Syslog&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

- O cabeçalho do Syslog é opcional.

- O separador de caractere "\n" é necessário entre todos os campos.
- Os campos, em ordem, são:
    1. Constante RsaSA (deve aparecer).
    2. O carimbo de data/hora do evento real (certifique-se de que não seja o carimbo de data/hora da chegada ao SIEM ou do envio ao ATP). Preferencialmente com a precisão em milissegundos, isso é importante.
    3. A ID de evento do Windows
    4. O nome do provedor de eventos do Windows
    5. O nome do log de eventos do Windows
    6. O nome do computador que está recebendo o evento (o controlador de domínio neste caso)
    7. O nome do usuário que está autenticando
    8. O nome do host de origem
    9. O código resultante do NTLM
- A ordem é importante, e nada mais deve ser incluído na mensagem.

### <a name="hp-arcsight"></a>HP Arcsight

CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|O controlador de domínio tentou validar as credenciais de uma conta.|Baixo| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Motivo ou Código de erro

- Deve estar em conformidade com a definição de protocolo.

- Nenhum cabeçalho de syslog.
- A parte do cabeçalho (a parte separada por uma barra vertical) deve existir (como mencionado no protocolo).
- As seguintes chaves na parte _Extensão_ devem estar presentes no evento:
  - externalId = a ID de evento do Windows
  - rt = o carimbo de data/hora do evento real (certifique-se de que não seja o carimbo de data/hora da chegada ao SIEM ou do envio ao ATP). Preferencialmente com a precisão em milissegundos, isso é importante.
  - cat = o nome do log de eventos do Windows
  - shost = o nome do host de origem
  - dhost = o computador que está recebendo o evento (o controlador de domínio neste caso)
  - duser = o usuário que está autenticando
- A ordem não é importante para a parte _Extensão_

- Deve haver uma chave personalizada e um keyLable para esses dois campos:
  - "EventSource"
  - "Motivo ou Código de erro" = o código resultante do NTLM

### <a name="splunk"></a>Splunk

&lt;Cabeçalho do Syslog&gt;\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

O computador tentou validar as credenciais de uma conta.

Página de autenticação: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0

Conta de logon: Administrador

Estação de Trabalho de Origem: SIEM

Código de erro: 0x0

- O cabeçalho do Syslog é opcional.

- Há um separador de caracteres "\r\n" entre todos os campos obrigatórios.
- Os campos estão no formato chave=valor.
- As chaves a seguir devem existir e ter um valor:
  - EventCode = a ID de evento do Windows
  - Logfile = o nome do log de eventos do Windows
  - SourceName = o nome do provedor de eventos do Windows
  - TimeGenerated = o carimbo de data/hora do evento real (certifique-se de que não seja o carimbo de data/hora da chegada ao SIEM ou do envio para o ATP). O formato deve corresponder a aaaaMMddHHmmss.FFFFFF, preferencialmente com precisão de milissegundos, isso é importante.
  - ComputerName = o nome do host de origem
  - Mensagem = o texto do evento original do evento do Windows
- A Chave da Mensagem e o valor DEVEM ser os últimos.
- A ordem não é importante para os pares de chave=valor

### <a name="qradar"></a>QRadar

O QRadar permite a coleta de eventos por meio de um agente. Se os dados forem reunidos usando um agente, o formato de hora será coletado sem dados de milissegundos. Uma vez que o Azure ATP precisa de dados de milissegundos, é necessário configurar o QRadar para usar a coleta de eventos do Windows sem agente. Para obter mais informações, confira [http://www-01.ibm.com/support/docview.wss?uid=swg21700170](http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: Coleção de Eventos do Windows sem Agente usando o protocolo MSRPC").

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

Os campos necessários são:

- O tipo de agente para a coleta
- O nome do provedor do log de eventos do Windows
- A fonte do log de eventos do Windows
- O nome de domínio totalmente qualificado do DC
- A ID de evento do Windows

TimeGenerated é o carimbo de data/hora do evento real (certifique-se de que não seja o carimbo de data/hora da chegada ao SIEM ou do envio para o ATP). O formato deve corresponder a aaaaMMddHHmmss.FFFFFF, preferencialmente com precisão de milissegundos, isso é importante.

A mensagem é o texto do evento original do evento do Windows

Certifique-se de ter \t entre os pares de chave=valor.

>[!NOTE]
> Não há suporte ao uso do WinCollect para a coleta de eventos do Windows.

## <a name="see-also"></a>Consulte Também

- [Ferramenta de dimensionamento do Azure ATP](https://aka.ms/aatpsizingtool)
- [Referência de logs de SIEM do Azure ATP](cef-format-sa.md)
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
