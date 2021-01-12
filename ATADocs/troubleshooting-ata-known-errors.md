---
title: Solução de problemas conhecidos do ATA | Microsoft Docs
description: Descreve como solucionar os problemas conhecidos no Advanced Threat Analytics
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 01/12/2021
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: b49e2b10713f23c4256a7236bfa7162189c6e43b
ms.sourcegitcommit: 373151a0e86e4933c5cb7c8f17c4d386356c98dd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2021
ms.locfileid: "98114962"
---
# <a name="troubleshooting-ata-known-issues"></a>Solução de problemas conhecidos do ATA

[!INCLUDE [Banner for top of topics](includes/banner.md)]

Esta seção detalha os possíveis erros nas implantações do ATA e as etapas necessárias para solucioná-los.

## <a name="ata-gateway-and-lightweight-gateway-errors"></a>Erros do Gateway e do Gateway Lightweight do ATA

> [!div class="mx-tableFixed"]
>
> |Erro|Descrição|Resolução|
> |-------------|----------|---------|
> |System.DirectoryServices.Protocols.LdapException: ocorreu um erro local|Falha do Gateway do ATA ao autenticar no controlador de domínio.|1. Confirme se o registro DNS do controlador de domínio está configurado corretamente no servidor DNS. <br>2. Verifique se a hora do gateway do ATA está sincronizada com a hora do controlador de domínio.|
> |System.IdentityModel.Tokens.SecurityTokenValidationException: falha ao validar cadeia de certificados|Falha do Gateway do ATA ao validar o certificado do Centro do ATA.|1. Verifique se o certificado de autoridade de certificação raiz está instalado no repositório de certificados da autoridade de certificação confiável no gateway do ATA.<br>2. valide se a CRL (lista de certificados revogados) está disponível e se a validação de revogação de certificado pode ser executada.|
> |Microsoft.Common.ExtendedException: falha ao analisar o tempo gerado|Falha do Gateway do ATA ao analisar as mensagens syslog que foram encaminhadas do SIEM.|Verifique se o SIEM está configurado para encaminhar as mensagens em um dos formatos compatíveis com o ATA.|
> |System.ServiceModel.FaultException: ocorreu um erro ao verificar a segurança da mensagem.|Falha do Gateway do ATA ao autenticar no Centro do ATA.|Verifique se a hora do Gateway do ATA está sincronizada com a hora do Centro do ATA.|
> |System.ServiceModel.EndpointNotFoundException: não foi possível se conectar ao net.tcp://center.ip.addr:443/IEntityReceiver|O gateway do ATA falhou ao estabelecer uma conexão com o centro do ATA.|Verifique se as configurações de rede estão corretas e se a conexão de rede entre o Gateway do ATA e o Centro do ATA está ativa.|
> |System.DirectoryServices.Protocols.LdapException: o servidor LDAP não está disponível.|Falha do Gateway do ATA ao consultar o controlador de domínio usando o protocolo LDAP.|1. Verifique se a conta de usuário usada pelo ATA para se conectar ao domínio de Active Directory tem acesso de leitura a todos os objetos na árvore de Active Directory.<br>2. Verifique se o controlador de domínio não está protegido para impedir consultas LDAP da conta de usuário usada pelo ATA.|
> |Microsoft.Tri.Infrastructure.ContractException: exceção de contrato|Falha do Gateway do ATA ao sincronizar a configuração do Centro do ATA.|Conclua a configuração do Gateway do ATA no Console do ATA.|
> |System.Reflection.ReflectionTypeLoadException: Não é possível carregar um ou mais dos tipos solicitados. Recupere a propriedade LoaderExceptions para maiores informações.|O Analisador de Mensagem é instalado no Gateway do ATA.| Desinstale o Analisador de Mensagem.|
> |Erro [Layout] System.OutOfMemoryException: A exceção do tipo 'System.OutOfMemoryException' foi gerada.|O Gateway do ATA não tem memória suficiente.|Aumente a quantidade de memória no controlador de domínio.|
> |Falha ao iniciar o consumidor ao vivo ---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException: O provedor de eventos PEFNDIS não está pronto|O PEF (Analisador de Mensagem) não foi instalado corretamente.|Se você estiver usando o Hyper-V, tente atualizar os serviços de Integração do Hyper-V, caso contrário, contate o suporte para uma solução alternativa.|
> |A instalação falhou com o erro: 0x80070652|Há outras instalações pendentes no seu computador.|Aguarde até que as outras instalações sejam concluídas e, se necessário, reinicie o computador.|
> |System.InvalidOperationException: Instance 'Microsoft.Tri.Gateway' não existe na Categoria especificada.|PIDs foi habilitado para nomes de processo no Gateway do ATA|Consulte [tratamento de nomes de instância duplicados](/windows/win32/perfctrs/handling-duplicate-instance-names) para desabilitar PIDs em nomes de processo|
> A categoria ' System. InvalidOperationException: não existe.|Os contadores podem estar desabilitados no registro|Use [KB2554336](https://support.microsoft.com/kb/2554336) para recriar os Contadores de desempenho|
> |System.ApplicationException: Não é possível iniciar a sessão do ETW MMA-ETW-Livecapture-a4f595bd-f567-49a7-b963-20fa4e370329|Há uma entrada do host no arquivo HOSTS que aponta para o nome curto do computador|Remova a entrada do host do arquivo C:\Windows\System32\drivers\etc\HOSTS ou altere-a para um FQDN.|
> |System. IO. IOException: falha na autenticação porque a parte remota fechou o fluxo de transporte ou não pôde criar um canal seguro de SSL/TLS|O TLS 1.0 está desabilitado no Gateway de ATA, mas o .Net está configurado para usar o TLS 1.2|Habilite o TLS 1,2 para .net definindo as chaves do registro para usar os padrões do sistema operacional para SSL e TLS, da seguinte maneira:<br></br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br> `[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SchUseStrongCrypto"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] " SchUseStrongCrypto"=dword:00000001`|
> |System.TypeLoadException: não foi possível carregar o tipo 'Microsoft.Opn.Runtime.Values.BinaryValueBufferManager' do assembly 'Microsoft.Opn.Runtime, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'|Falha do Gateway do ATA ao carregar os arquivos de análise necessários.|Verifique se o Microsoft Message Analyzer está instalado no momento. Não há suporte para o Message Analyzer ser instalado com o Gateway/Gateway Lightweight do ATA. Desinstale o Message Analyzer e reinicie o serviço de Gateway.|
> |System.Net.WebException: o servidor remoto retornou um erro: (407) Autenticação de proxy necessária|A comunicação de Gateway do ATA no centro do ATA está sendo interrompida por um servidor proxy.|Desabilite o proxy no computador do Gateway do ATA. <br></br>Observe que as configurações de proxy podem ser por conta.|
> |System.IO.DirectoryNotFoundException: o sistema não pode localizar o caminho especificado. (Exceção de HRESULT: 0x80070003)|Um ou mais dos serviços necessários para operar o ATA não foram iniciados.|Inicie os seguintes serviços: <br></br>Logs e Alertas de Desempenho (PLA), Agendador de Tarefas (agenda).|
> |System.Net.WebException: o servidor remoto retornou um erro: (403) Proibido|O gateway do ATA ou o gateway Lightweight foi proibido de estabelecer uma conexão HTTP porque o centro do ATA não é confiável.|Adicione o nome NetBIOS e o FQDN do centro do ATA à lista de sites confiáveis e desmarque o cache no Internet Explorer (ou o nome do centro do ATA, conforme especificado na configuração, se o configurado for diferente do NetBIOS/FQDN).|
> |System.Net.Http.HttpRequestException: falha na PostAsync [requestTypeName=StopNetEventSessionRequest]|O Gateway do ATA ou o Gateway Lightweight do ATA não pode parar e iniciar a sessão do ETW (Rastreamento de Eventos para Windows) que coleta o tráfego de rede devido a um problema WMI (Instrumentação de Gerenciamento do Windows)|Siga as instruções no artigo [WMI: como recriar o repositório WMI](https://blogs.technet.microsoft.com/askperf/2009/04/13/wmi-rebuilding-the-wmi-repository/) para corrigir o problema WMI|
> |System.Net.Sockets.SocketException: foi feita uma tentativa de acessar um soquete de uma maneira proibida pelas permissões de acesso dele|Outro aplicativo está usando a porta 514 no Gateway do ATA|Use `netstat -o` para estabelecer qual processo está usando essa porta.|

## <a name="deployment-errors"></a>Erros de implantação

> [!div class="mx-tableFixed"]
>
> |Erro|Descrição|Resolução|
> |-------------|----------|---------|
> |Falha na instalação do .Net Framework 4.6.1 com o erro 0x800713ec|Os pré-requisitos do .Net Framework 4.6.1 não estão instalados no servidor. |Antes de instalar o ATA, verifique se as atualizações do Windows [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) e [KB2919355](https://support.microsoft.com/kb/2919355) estão instaladas no servidor.|
> |System.Threading.Tasks.TaskCanceledException: uma tarefa foi cancelada|O processo de implantação atingiu o tempo limite, uma vez que ele não pôde acessar o Centro do ATA.|1. Verifique a conectividade de rede para o centro do ATA navegando até ele usando seu endereço IP. <br></br>2. Verifique a configuração do proxy ou do firewall.|
> |System.Net.Http.HttpRequestException: ocorreu um erro ao enviar a solicitação. ---> System.Net.WebException: o servidor remoto retornou um erro: (407) Autenticação de proxy necessária.|O processo de implantação atingiu o tempo limite, uma vez que ele não pôde acessar o Centro do ATA devido à configuração incorreta de proxy.|Desabilite a configuração de proxy antes da implantação e habilite a configuração de proxy novamente. Como alternativa, você pode configurar uma exceção no proxy.|
> |System.Net.Sockets.SocketException: uma conexão existente foi fechada forçadamente pelo host remoto||Habilite o TLS 1,2 para .net definindo as chaves do registro para usar os padrões do sistema operacional para SSL e TLS, da seguinte maneira:<br></br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SchUseStrongCrypto"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SchUseStrongCrypto"=dword:00000001`|
> |Erro [ \\ [] DeploymentModel [ \\ ]] falha na autenticação de gerenciamento [ \\ [] CurrentlyLoggedOnUser = <domain> \\ <username> status = FailedAuthentication Exception = [ \\ ]]|O processo de implantação do Gateway do ATA ou do Gateway Lightweight do ATA não conseguiu autenticar com sucesso o ATA Center|Abra um navegador no computador no qual o processo de implantação falhou e veja se você pode alcançar o Console do ATA. </br>Se não, inicie a solução de problemas para ver o motivo de o navegador não conseguir autenticar o Centro do ATA. </br>Verifique a: </br>Configuração de proxy</br>Problemas de rede</br>Configurações de política de grupo para a autenticação no computador que difere do Centro do ATA.|
> | Erro [\\[]DeploymentModel[\\]] Falha na autenticação de gerenciamento|Falha na validação do certificado do Centro|O certificado do Centro pode requerer uma conexão com a Internet para validação. Verifique se o serviço de Gateway tem a configuração de proxy adequada para habilitar a conexão e a validação.|
> | Ao implantar o centro e selecionar um certificado, um erro "sem suporte" é relatado|Isso pode acontecer se o certificado selecionado não atender aos requisitos ou se a chave privada do certificado não estiver acessível.|Verifique se você está executando a implantação com privilégios elevados (**Executar como administrador**) e se o certificado selecionado atende aos [requisitos](ata-prerequisites.md#certificates).|

## <a name="ata-center-errors"></a>Erros do Centro do ATA

> [!div class="mx-tableFixed"]
>
> |Erro|Descrição|Resolução|
> |-------------|----------|---------|
> |System.Security.Cryptography.CryptographicException: acesso negado.|O Centro do ATA falha ao usar o certificado emitido para descriptografia. Isso provavelmente ocorreu devido ao uso de um certificado com KeySpec (KeyNumber) definido como Assinatura (AT\\_SIGNATURE) que não é compatível com a descriptografia, em vez de usar o KeyExchange (AT\\_KEYEXCHANGE).|1. pare o serviço do centro do ATA. <br></br>2. exclua o certificado do centro do ATA do repositório de certificados do centro. (Antes de excluir, verifique se você tem o backup do certificado com a chave privada em um arquivo PFX). <br></br>3. Abra um prompt de comando com privilégios elevados e execute certutil-importpfx "CenterCertificate. pfx" em \\ _KEYEXCHANGE <br></br>4. Inicie o serviço do centro do ATA. <br></br>5. Verifique se tudo agora funciona conforme o esperado.|

## <a name="ata-gateway-and-lightweight-gateway-issues"></a>Erros do Gateway do ATA e do Gateway Lightweight

> [!div class="mx-tableFixed"]
>
> |Problema|Descrição|Resolução|
> |-------------|----------|---------|
> |Nenhum tráfego recebido do controlador de domínio, mas os alertas de integridade são observados|Nenhum tráfego foi recebido de um controlador de domínio usando o espelhamento de porta por meio de um Gateway do ATA|Na NIC de captura do gateway do ATA, desabilite esses recursos em **Configurações avançadas**:<br></br>União de Segmentos de Recebimento (IPv4)<br></br>União de Segmentos de Recebimento (IPv6)|
> |Este alerta de integridade é exibido: algum tráfego de rede não está sendo analisado|Se você tiver um gateway do ATA ou um gateway Lightweight em máquinas virtuais VMware, você poderá receber esse alerta de integridade. Isso ocorre devido a uma incompatibilidade de configuração no VMware.|Definir as configurações a seguir para 0 ou Desabilitado na configuração de NIC de máquina virtual: TsoEnable, LargeSendOffload, Descarregamento de TSO, Descarregamento de TSO Gigante|

## <a name="multi-processor-group-mode"></a>Modo Grupo de multiprocessadores

Para os sistemas operacionais Windows 2008R2 e 2012, o gateway do ATA não tem suporte no modo de **grupo de vários processadores** .

Soluções alternativas possíveis sugeridas:

- Se o hyperthreading estiver ativado, desative-o. Isso pode reduzir o número de núcleos lógicos o suficiente para evitar a necessidade de execução no modo **Grupo de multiprocessadores**.

- Se seu computador tiver menos de 64 núcleos lógicos e estiver em execução em um host HP, você poderá alterar a configuração do BIOS de **Otimização do Tamanho do Grupo NUMA** do padrão **Clusterizado** para **Simples**.

## <a name="see-also"></a>Consulte Também

- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Planejamento da capacidade do ATA](ata-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-collection.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
