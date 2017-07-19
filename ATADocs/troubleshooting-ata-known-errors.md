---
title: "Solução de problemas conhecidos do ATA | Microsoft Docs"
description: Descreve como solucionar os problemas conhecidos no Advanced Threat Analytics
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/3/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 0ded0dd064f0327f6e52f15081e2b9dce14f982b
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*



# <a name="troubleshooting-ata-known-issues"></a>Solução de problemas conhecidos do ATA

Esta seção detalha os possíveis erros nas implantações do ATA e as etapas necessárias para solucioná-los.

## <a name="ata-gateway-and-lightweight-gateway-errors"></a>Erros do Gateway e do Gateway Lightweight do ATA

|Erro do|Descrição|Resolução|
|-------------|----------|---------|
|System.DirectoryServices.Protocols.LdapException: ocorreu um erro local|Falha do Gateway do ATA ao autenticar no controlador de domínio.|1. Confirme se o registro DNS do controlador de domínio está configurado corretamente no servidor DNS. <br>2. Verifique se a hora do Gateway do ATA está sincronizada com a hora do controlador de domínio.|
|System.IdentityModel.Tokens.SecurityTokenValidationException: falha ao validar cadeia de certificados|Falha do Gateway do ATA ao validar o certificado do Centro do ATA.|1. Verifique se o certificado da autoridade de certificação raiz está instalado no repositório de certificados da autoridade de certificação confiável no Gateway do ATA. <br>2. Confirme se a CRL (lista de certificados revogados) está disponível e se é possível fazer a validação de certificados revogados.|
|Microsoft.Common.ExtendedException: falha ao analisar o tempo gerado|Falha do Gateway do ATA ao analisar as mensagens syslog que foram encaminhadas do SIEM.|Verifique se o SIEM está configurado para encaminhar as mensagens em um dos formatos compatíveis com o ATA.|
|System.ServiceModel.FaultException: ocorreu um erro ao verificar a segurança da mensagem.|Falha do Gateway do ATA ao autenticar no Centro do ATA.|Verifique se a hora do Gateway do ATA está sincronizada com a hora do Centro do ATA.|
|System.ServiceModel.EndpointNotFoundException: não foi possível se conectar ao net.tcp://center.ip.addr:443/IEntityReceiver|Falha do Gateway do ATA ao estabelecer conexão com o Centro do ATA.|Verifique se as configurações de rede estão corretas e se a conexão de rede entre o Gateway do ATA e o Centro do ATA está ativa.|
|System.DirectoryServices.Protocols.LdapException: o servidor LDAP não está disponível.|Falha do Gateway do ATA ao consultar o controlador de domínio usando o protocolo LDAP.|1. Verifique se a conta do usuário usada pelo ATA para se conectar ao domínio do Active Directory tem acesso de leitura a todos os objetos na árvore do Active Directory. <br>2. Certifique-se de que o controlador de domínio não esteja protegido contra consultas LDAP da conta de usuário usada pelo ATA.|
|Microsoft.Tri.Infrastructure.ContractException: exceção de contrato|Falha do Gateway do ATA ao sincronizar a configuração do Centro do ATA.|Conclua a configuração do Gateway do ATA no Console do ATA.|
|System.Reflection.ReflectionTypeLoadException: Não é possível carregar um ou mais dos tipos solicitados. Recupere a propriedade LoaderExceptions para maiores informações.|O Analisador de Mensagem é instalado no Gateway do ATA.| Desinstale o Analisador de Mensagem.|
|Erro [Layout] System.OutOfMemoryException: A exceção do tipo 'System.OutOfMemoryException' foi gerada.|O Gateway do ATA não tem memória suficiente.|Aumente a quantidade de memória no controlador de domínio.|
|Falha ao iniciar o consumidor ao vivo ---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException: O provedor de eventos PEFNDIS não está pronto|O PEF (Analisador de Mensagem) não foi instalado corretamente.|Se você estiver usando o Hyper-V, tente atualizar os serviços de Integração do Hyper-V, caso contrário, contate o suporte para uma solução alternativa.|
|A instalação falhou com o erro: 0x80070652|Há outras instalações pendentes no seu computador.|Aguarde até que as outras instalações sejam concluídas e, se necessário, reinicie o computador.|
|System.InvalidOperationException: Instance 'Microsoft.Tri.Gateway' não existe na Categoria especificada.|PIDs foi habilitado para nomes de processo no Gateway do ATA|Use [KB281884](https://support.microsoft.com/en-us/kb/281884) para desabilitar os PIDs em nomes de processo|
|System.InvalidOperationException: Categoria não existe.|Os contadores podem estar desabilitados no registro|Use [KB2554336](https://support.microsoft.com/en-us/kb/2554336) para recriar os Contadores de desempenho|
|System.ApplicationException: Não é possível iniciar a sessão do ETW MMA-ETW-Livecapture-a4f595bd-f567-49a7-b963-20fa4e370329|Há uma entrada do host no arquivo HOSTS que aponta para o nome curto do computador|Remova a entrada do host do arquivo C:\Windows\System32\drivers\etc\HOSTS ou altere-a para um FQDN.|
|System.IO.IOException: a autenticação falhou porque a parte remota fechou o fluxo de transporte.|O TLS 1.0 está desabilitado no Gateway ATA, mas o .Net está configurado para usar o TLS 1.2|Use uma das seguintes opções: </br> Habilitar o TLS 1.0 no Gateway ATA </br>Habilite o TLS 1.2 no .Net definindo as chaves de registro para usar os padrões do sistema operacional para LLS e TLS, da seguinte forma: `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`|
|System.TypeLoadException: não foi possível carregar o tipo 'Microsoft.Opn.Runtime.Values.BinaryValueBufferManager' do assembly 'Microsoft.Opn.Runtime, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'|Falha do Gateway do ATA ao carregar os arquivos de análise necessários.|Verifique se o Microsoft Message Analyzer está instalado no momento. Não há suporte para o Message Analyzer ser instalado com o Gateway/Gateway Lightweight do ATA. Desinstale o Message Analyzer e reinicie o serviço de Gateway.|
|Alertas de tráfego espelhado por porta descartados ao usar o Gateway Lightweight no VMware|Se você estiver usando DCs em máquinas virtuais VMware, poderá receber alertas sobre o **Tráfego de rede espelhado por porta descartado**. Isso pode ser devido a uma incompatibilidade de configuração no VMware. |Para evitar esses alertas, verifique se as configurações a seguir estão definidas como 0 ou Desabilitado: TsoEnable, LargeSendOffload, IPv4 e Descarregamento de TSO (Descarregamento de Segmentação TCP). Além disso, considere desabilitar o Descarregamento TSO gigante do IPv4. Para obter mais informações, consulte a documentação do VMware.|


## <a name="deployment-errors"></a>Erros de implantação
|Erro do|Descrição|Resolução|
|-------------|----------|---------|
|Falha na instalação do .Net Framework 4.6.1 com o erro 0x800713ec|Os pré-requisitos do .Net Framework 4.6.1 não estão instalados no servidor. |Antes de instalar o ATA, verifique se as atualizações do Windows [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) e [KB2919355](https://support.microsoft.com/kb/2919355) estão instaladas no servidor.|
|System.Threading.Tasks.TaskCanceledException: uma tarefa foi cancelada|O processo de implantação atingiu o tempo limite, uma vez que ele não pôde acessar o Centro do ATA.|1.    Verifique a conectividade de rede com o Centro do ATA navegando até ele usando seu endereço IP. <br></br>2.    Verifique a configuração de proxy ou firewall.|
|System.Net.Http.HttpRequestException: ocorreu um erro ao enviar a solicitação. ---> System.Net.WebException: o servidor remoto retornou um erro: (407) Autenticação de proxy necessária.|O processo de implantação atingiu o tempo limite, uma vez que ele não pôde acessar o Centro do ATA devido à configuração incorreta de proxy.|Desabilite a configuração de proxy antes da implantação e habilite a configuração de proxy novamente. Como alternativa, você pode configurar uma exceção no proxy.|
|Nenhum tráfego recebido do controlador de domínio, mas são observados alertas de monitoramento|    Nenhum tráfego foi recebido de um controlador de domínio usando o espelhamento de porta por meio de um Gateway do ATA|Na NIC de captura no Gateway do ATA, desabilite esses recursos em **Configurações Avançadas**:<br></br>União de Segmentos de Recebimento (IPv4)<br></br>União de Segmentos de Recebimento (IPv6)|





## <a name="see-also"></a>Consulte também
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Planejamento da capacidade do ATA](ata-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
