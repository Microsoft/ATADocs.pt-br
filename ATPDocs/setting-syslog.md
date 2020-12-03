---
title: Definir as configurações de Syslog no Microsoft Defender para Identidade
description: Descreve como fazer com que o Microsoft Defender para Identidade notifique você (por email ou por encaminhamento de eventos do Defender para Identidade) quando detectar atividades suspeitas
ms.date: 10/27/2020
ms.topic: how-to
ms.openlocfilehash: 587fd2cab00b982ace580ef2b8b587157c960891
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96544344"
---
# <a name="integrate-with-syslog"></a>Integrar com o Syslog

> [!NOTE]
> Os recursos do [!INCLUDE [Product long](includes/product-long.md)] explicados nesta página também podem ser acessados usando o novo [portal](https://portal.cloudappsecurity.com).

O [!INCLUDE [Product long](includes/product-long.md)] poderá notificar você quando detectar atividades suspeitas enviando alertas de segurança e de integridade para seu servidor Syslog por meio de um sensor indicado.

Após habilitar as notificações do Syslog, você poderá definir o seguinte:

|Campo|Descrição|
|---------|---------------|
|sensor|Selecione um sensor designado para ser responsável por agregar todos os eventos de Syslog e encaminhá-los para seu servidor de SIEM.|
|Ponto de extremidade de serviço|FQDN do servidor Syslog e, opcionalmente, altere o número da porta (padrão: 514)|
|Transport|Pode ser UDP, TCP ou TLS (Syslog protegido)|
|Formato|Este é o formato usado pelo [!INCLUDE [Product short](includes/product-short.md)] para enviar eventos ao servidor SIEM – RFC 5424 ou RFC 3164.|

1. Antes de configurar as notificações do Syslog, trabalhe com seu administrador do SIEM para descobrir as seguintes informações:

    - FQDN ou Endereço IP do servidor SIEM
    - Porta na qual o servidor SIEM está escutando
    - Qual transporte usar: UDP, TCP ou TLS (Syslog protegido)
    - Formato no qual enviar os dados, RFC 3164 ou 5424

1. Abra o portal do [!INCLUDE [Product short](includes/product-short.md)].
1. Clique em **Configurações**.
1. No submenu **Notificações e Relatórios**, selecione **Notificações**.
1. Na opção **Serviço Syslog**, clique em **Configurar**.
1. Selecione o **Sensor**.
1. Insira a URL do **Ponto de extremidade de serviço**.
1. Selecione o protocolo de **Transporte** (TCP ou UDP).
1. Selecione o formato (RFC 3164 ou RFC 5424).
1. Selecione **Enviar mensagem de teste do Syslog** e verifique se a mensagem foi recebida na sua solução de infraestrutura do Syslog.
1. Clique em **Salvar**.

Para revisar ou modificar suas configurações do Syslog.

1. Clique em **Notificações** e, em **Notificações do Syslog**, clique em **Configurar** e insira as seguintes informações:

    ![Imagem de configurações do servidor Syslog [!INCLUDE [Product short](includes/product-short.md)]](media/syslog.png)

1. Você pode selecionar quais eventos enviar ao servidor do Syslog. Em **Notificações do Syslog**, especifique quais notificações devem ser enviadas ao servidor do Syslog: novos alertas de segurança, alertas de segurança atualizados e novos problemas de integridade.

> [!NOTE]
> Caso planeje criar automação ou scripts para logs de SIEM do [!INCLUDE [Product short](includes/product-short.md)], recomendamos usar o campo **externalId** a fim de identificar o tipo de alerta em vez de usar o nome do alerta para essa finalidade. Nomes de alertas, ocasionalmente, podem ser modificados, enquanto o **externalId** de cada alerta é permanente. Para saber mais, confira [Referência de log de SIEM do [!INCLUDE [Product short](includes/product-short.md)]](cef-format-sa.md).

## <a name="see-also"></a>Consulte Também

- [Trabalhando com contas confidenciais](sensitive-accounts.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
