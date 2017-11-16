---
title: "Novidades na versão 1.8 do ATA | Microsoft Docs"
description: "Lista as novidades na nova versão 1.8 do ATA e seus problemas conhecidos"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 9/03/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 9592d413-df0e-4cec-8e03-be1ae00ba5dc
ms.reviewer: 
ms.suite: ems
ms.openlocfilehash: 71e7f723d02b4e86f1799e5a92998363766de7a2
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2017
---
# <a name="whats-new-in-ata-version-18"></a>Novidades na versão 1.8 do ATA

A versão mais recente da atualização do ATA pode ser [baixada do Centro de Download](https://www.microsoft.com/download/details.aspx?id=55536) ou a versão completa pode ser baixada do [centro Eval](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).

Essas notas de versão fornecem informações sobre atualizações, novos recursos, correções de bug e problemas conhecidos nesta versão da Advanced Threat Analytics.



## <a name="new--updated-detections"></a>Detecções novas e atualizadas

- A implementação de protocolo incomum foi aperfeiçoada para ser capaz de detectar malware WannaCry.

- NOVO! **Modificação anormal de grupos confidenciais** – Como parte da fase de elevação de privilégio, os invasores modificam grupos com altos privilégios para obter acesso a recursos confidenciais. Agora o ATA detecta quando há uma alteração anormal em um grupo com privilégios elevados.
- NOVO! **Falhas de autenticação suspeitas** (força bruta comportamental) – Os invasores tentam usar força bruta em credenciais para comprometer contas. Agora o ATA emite um alerta quando o comportamento de autenticação com falha anormal é detectado.   

- **Tentativa de execução remota – execução WMI** – Os invasores podem tentar controlar sua rede executando códigos remotamente em seu controlador de domínio. O ATA aprimorou a detecção de execução remota para incluir a detecção de métodos WMI para executar código remotamente.

- Reconhecimento usando consultas de serviço de diretório – Essa detecção foi aprimorada para poder capturar consultas em uma única entidade confidencial e reduzir o número de falsos positivos gerados na versão anterior. Se você tiver desabilitado isso na versão 1.7, instalar a versão 1.8 agora o habilitará automaticamente.

- Atividade Golden Ticket do Kerberos – O ATA 1.8 inclui uma técnica adicional para detectar ataques de golden ticket.
    - Agora, o ATA detecta atividades suspeitas em que o tempo de vida do golden ticket expirou. Se um tíquete Kerberos é usado por mais do que o tempo de vida permitido, o ATA detecta isso como uma atividade suspeita em que um Golden ticket provavelmente foi criado.
- Melhorias foram feitas nas seguintes detecções para remover falsos positivos conhecidos:  
    - Detecção de elevação de privilégios (PAC forjado) 
    - Atividade de downgrade de criptografia (Skeleton Key)
    - Implementação de protocolo incomum
    - Confiança quebrada

## <a name="improved-triage-of-suspicious-activities"></a>Triagem de atividades suspeitas aprimorada

-   NOVO! O ATA 1.8 permite que você execute as seguintes atividades suspeitas durante o processo de triagem: 
    - **Excluir entidades** de gerar futuras atividades suspeitas para impedir que o ATA alerte quando detectar verdadeiros positivos benignos (como um administrador executando código remoto ou detectando scanners de segurança).
    - **Impedir que atividades suspeitas recorrentes** gerem alertas.
    - **Excluir atividades suspeitas** da linha do tempo de ataque.
-   O processo para acompanhar alertas de atividade suspeita agora é mais eficiente. A linha do tempo de atividades suspeitas foi redefinida. No ATA 1.8, você poderá ver muito mais atividades suspeitas em uma única tela, que contém as melhores informações para fins de triagem e investigação. 

## <a name="new-reports-to-help-you-investigate"></a>Novos relatórios para ajudá-lo a investigar 
-   NOVO! O **relatório de resumo** foi adicionado para permitir que você veja todos os dados resumidos do ATA, incluindo atividades suspeitas, problemas de integridade e muito mais. Você pode até mesmo definir um relatório personalizado que é gerado automaticamente de forma recorrente.
-   NOVO! O **relatório de grupos confidenciais** foi adicionado para que você possa ver todas as alterações feitas em grupos confidenciais durante um certo período.


## <a name="infrastructure-improvements"></a>Melhorias na infraestrutura

-   O desempenho do Centro do ATA foi aprimorado. No ATA 1.8 o Centro do ATA pode lidar com mais de um milhão de pacotes por segundo.
-   O Gateway Lightweight do ATA poderá ler eventos localmente, sem a necessidade de configurar o encaminhamento de eventos.
-   Agora você pode configurar separadamente um email para alertas de monitoramento e para atividades suspeitas.

## <a name="security-improvements"></a>Aprimoramentos de segurança

-   NOVO! **Logon único para o gerenciamento do ATA**. O ATA dá suporte ao logon único integrado com a autenticação do Windows – se você já fez logon em seu computador, o ATA usará esse token para fazer o logon no Console do ATA. Você também pode fazer logon usando um cartão inteligente. Scripts de instalação silenciosa para o Gateway de ATA e para o Gateway Lightweight do ATA agora usam o contexto do usuário conectado, sem a necessidade de fornecer credenciais.
-   Os privilégios do sistema local foram removidos do processo do Gateway do ATA, portanto, agora você pode usar contas virtuais (disponíveis apenas em Gateways do ATA autônomos), contas de serviço gerenciadas e contas de serviço gerenciado de grupo para executar o processo do Gateway do ATA.   
-   Foram adicionados logs de auditoria para o Centro do ATA e para os Gateways do ATA e todas as ações agora podem ser registradas no Log de Eventos do Windows.
-   Foi adicionado suporte para certificados KSP para o Centro do ATA.

## <a name="additional-changes"></a>Alterações adicionais

- A opção para adicionar anotações foi removida de Atividades suspeitas
- As recomendações para redução de atividades suspeitas foram removidas da linha do tempo de Atividades suspeitas.
- Começando com o ATA versão 1.8, os Gateways de ATA e Gateways Lightweight estão gerenciando seus próprios certificados e não precisam de nenhuma interação do administrador para gerenciá-los.

## <a name="known-issues"></a>Problemas conhecidos

> [!WARNING]
> Para evitar esses problemas conhecidos, atualize ou implante usando a versão 1.8 atualização 1.

### <a name="ata-gateway-on-windows-server-core"></a>Gateway do ATA no Windows Server Core

**Sintomas**: atualizar um Gateway do ATA 1.8 no Windows Server 2012R2 Core com o .Net framework 4.7 pode falhar com o erro: *O gateway do Microsoft Advanced Threat Analytics parou de funcionar*. 

![Erro de núcleo de gateway](./media/gateway-core-error.png)

No Windows Server 2016 Core, você não poderá ver o erro, mas o processo falhará quando você tentar instalar e os eventos 1000 e 1001 (falha de processo) serão registrados no Log de Eventos do aplicativo no servidor.

**Descrição**: há um problema com o .NET framework 4.7 que faz com que os aplicativos que usam a tecnologia WPF (como o ATA) falhem ao carregar. Para obter mais informações, [consulte KB 4034015](https://support.microsoft.com/help/4034015/wpf-window-can-t-be-loaded-after-you-install-the-net-framework-4-7-on). 

**Solução alternativa**: desinstale o .Net 4.7 [Consulte KB 3186497](https://support.microsoft.com/help/3186497/the-net-framework-4-7-offline-installer-for-windows) para reverter a versão do .NET para .NET 4.6.2 e, em seguida, atualize o Gateway de ATA para a versão 1.8. Após a atualização do ATA, você pode reinstalar o .NET 4.7.  Haverá uma atualização para corrigir esse problema em uma versão futura.

### <a name="lightweight-gateway-event-log-permissions"></a>Permissões de log de eventos do Gateway Lightweight

**Sintomas**: quando você atualiza o ATA para a versão 1.8, aplicativos ou serviços que anteriormente tinham permissões para acessar o Log de Eventos de Segurança podem perder as permissões. 

**Descrição**: para facilitar a implantação do ATA, o ATA 1.8 acessa seu Log de Eventos de Segurança diretamente, sem a necessidade de configuração do Windows Event Forwarding. Ao mesmo tempo, o ATA é executado como um serviço local de baixa permissão para manter a segurança mais forte. Para fornecer acesso para o ATA leia os eventos, o serviço do ATA concede a si mesmo permissões para o Log de Eventos de Segurança. Quando isso acontece, as permissões definidas anteriormente para outros serviços podem ser desabilitadas.

**Solução alternativa**: execute o seguinte script do Windows PowerShell. Isso remove as permissões adicionadas incorretamente no registro do ATA e as adiciona por meio de uma API diferente. Isso pode restaurar permissões para outros aplicativos. Se não estiver, eles precisarão ser restaurados manualmente. Haverá uma atualização para corrigir esse problema em uma versão futura. 

       $ATADaclEntry = "(A;;0x1;;;S-1-5-80-1717699148-1527177629-2874996750-2971184233-2178472682)"
        try {
        $SecurityDescriptor = Get-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\Eventlog\Security -Name CustomSD
        $ATASddl = "O:BAG:SYD:" + $ATADaclEntry 
        if($SecurityDescriptor.CustomSD -eq $ATASddl) {
        Remove-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\Eventlog\Security -Name CustomSD
        }
    }
    catch
    {
    # registry key does not exist
    }

    $EventLogConfiguration = New-Object -TypeName System.Diagnostics.Eventing.Reader.EventLogConfiguration("Security")
    $EventLogConfiguration.SecurityDescriptor = $EventLogConfiguration.SecurityDescriptor + $ATADaclEntry

### <a name="proxy-interference"></a>Interferência de proxy

**Sintomas**: depois de atualizar para o ATA 1.8 o serviço de Gateway do ATA pode falhar ao iniciar. No log de erros do ATA, você verá a seguinte exceção: *System.Net.Http.HttpRequestException: ocorreu um erro ao enviar a solicitação.---> System.Net.WebException: o servidor remoto retornou um erro: (407) autenticação de proxy necessária.*

**Descrição**: iniciando na versão 1.8 do ATA, o Gateway do ATA se comunica com o centro do ATA usando o protocolo http. Se o computador no qual você instalou o Gateway do ATA usa um servidor proxy para conectar-se ao centro do ATA, ela poderá quebrar essa comunicação. 

**Solução alternativa**: desabilite o uso de um servidor proxy na conta de serviço de Gateway do ATA. Haverá uma atualização para corrigir esse problema em uma versão futura.

### <a name="report-settings-reset"></a>Redefinição de configurações de Relatório

**Sintomas**: qualquer configuração que foi feita para os relatórios agendados é limpa quando você atualiza para 1.8 atualização 1.

**Descrição**: atualizar para 1.8 atualização 1 do 1.8 redefine as configurações de agendamento dos relatórios.

**Solução alternativa**: antes de atualizar para o 1.8 atualização 1, faça uma cópia das configurações de relatório e as insira novamente, isso também pode ser feito por meio de um script, para saber mais, confira [Exportar e importar a configuração do ATA](ata-configuration-file.md).


## <a name="see-also"></a>Consulte também
[Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Atualizar o ATA para a versão 1.8 — guia de migração](ata-update-1.8-migration-guide.md)

