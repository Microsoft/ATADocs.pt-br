--
# <a name="required-metadata"></a>metadados necessários

title: Solução de problemas do log de erros do Advanced Threat Analytics | Descrição do Microsoft Docs: descreve como você pode solucionar erros comuns em palavras-chave de ATA: author: rkarlin ms.author: rkarlin manager: mbaldwin ms.date: 14/3/2017 ms.topic: article ms.prod: ms.service: advanced-threat-analytics ms.technology: ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb

# <a name="optional-metadata"></a>metadados opcionais

#<a name="robots"></a>ROBOTS:
#<a name="audience"></a>audiência:
#<a name="msdevlang"></a>ms.devlang:
ms.reviewer: arzinger

ms.suite: ems
#<a name="mstgtpltfrm"></a>ms.tgt_pltfrm:
#<a name="mscustom"></a>ms.custom:

---

*Aplica-se a: Advanced Threat Analytics versão 1.7*



# <a name="troubleshooting-the-ata-error-log"></a>Solução de problemas do log de erros do ATA
Esta seção detalha os possíveis erros nas implantações do ATA e as etapas necessárias para solucioná-los.
## <a name="ata-gateway-errors"></a>Erros do Gateway do ATA
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
|System.IO.IOException: a autenticação falhou porque a parte remota fechou o fluxo de transporte.|O TLS 1.0 está desabilitado no Gateway ATA, mas o .Net está configurado para usar o TLS 1.2|Use uma das seguintes opções: </br> Habilitar o TLS 1.0 no Gateway ATA </br>Habilite o TLS 1.2 no .Net definindo as chaves de registro para usar os padrões do sistema operacional para LLS e TLS, da seguinte forma: `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"`|



## <a name="ata-lightweight-gateway-errors"></a>Erros do Gateway Lightweight do ATA

**Erro**: alertas de tráfego espelhado por porta descartados ao usar o Gateway Lightweight no VMware

**Descrição**: se você estiver usando DCs (controladores de domínio) em máquinas virtuais VMware, você poderá receber alertas sobre o **Tráfego de rede espelhado por porta descartado**. Isso pode ser devido a uma incompatibilidade de configuração no VMware. 
**Solução**: Para evitar esses alertas, verifique se as configurações a seguir estão definidas como 0 ou Desabilitado: TsoEnable, LargeSendOffload, IPv4 e Descarregamento de TSO (Descarregamento de Segmentação TCP). Além disso, considere desabilitar o Descarregamento TSO gigante do IPv4. Para obter mais informações, consulte a documentação do VMware.


## <a name="ata-iis-errors-not-applicable-for-ata-v17-and-above"></a>Erros de IIS do ATA (não aplicável para o ATA v1.7 e superior)
|Erro do|Descrição|Resolução|
|-------------|----------|---------|
|Erro HTTP 500.19 – Erro Interno do Servidor|O módulo de Reescrita de URL para IIS não foi instalado corretamente.|Desinstale e reinstale o módulo de Reescrita de URL para IIS.<br>[Baixar o módulo de Reescrita de URL para IIS](http://go.microsoft.com/fwlink/?LinkID=615137)|

## <a name="deployment-errors"></a>Erros de implantação
|Erro do|Descrição|Resolução|
|-------------|----------|---------|
|Falha na instalação do .Net Framework 4.6.1 com o erro 0x800713ec|Os pré-requisitos do .Net Framework 4.6.1 não estão instalados no servidor. |Antes de instalar o ATA, verifique se as atualizações do Windows [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) e [KB2919355](https://support.microsoft.com/kb/2919355) estão instaladas no servidor.|

![Imagem do erro de instalação do .NET no ATA](media/netinstallerror.png)


## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planejamento da capacidade do ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurar coleta de eventos](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configuração do encaminhamento de eventos do Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
