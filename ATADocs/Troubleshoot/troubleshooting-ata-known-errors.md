---
title: "Solução de problemas do log de erros do ATA | Microsoft Advanced Threat Analytics"
description: "Descreve como é possível solucionar erros comuns no ATA"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e0745079465aecefd26571eea894d19b82cbc216
ms.openlocfilehash: c72bca3cb1eef1f3fb59f666c6143cf5c095bde9


---

# Solução de problemas do log de erros do ATA
Esta seção detalha os possíveis erros nas implantações do ATA e as etapas necessárias para solucioná-los.
## Erros do Gateway do ATA
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
|Falha ao iniciar o consumidor ao vivo ---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException: O provedor de eventos PEFNDIS não está pronto|O PEF (Analisador de Mensagem) não foi instalado corretamente.|Entre em contato com o suporte para uma solução alternativa.|
|A instalação falhou com o erro: 0x80070652|Há outras instalações pendentes no seu computador.|Aguarde até que as outras instalações sejam concluídas e, se necessário, reinicie o computador.|

## Erros do Console do ATA
|Erro do|Descrição|Resolução|
|-------------|----------|---------|
|Erro HTTP 500.19 – Erro Interno do Servidor|O módulo de Reescrita de URL para IIS não foi instalado corretamente.|Desinstale e reinstale o módulo de Reescrita de URL para IIS.<br>[Baixar o módulo de Reescrita de URL para IIS](http://go.microsoft.com/fwlink/?LinkID=615137)|

## Erros de implantação
|Erro do|Descrição|Resolução|
|-------------|----------|---------|
|Falha na instalação do .Net Framework 4.6.1 com o erro 0x800713ec|Os pré-requisitos do .Net Framework 4.6.1 não estão instalados no servidor. |Antes de instalar o ATA, verifique se as atualizações do Windows [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) e [KB2919355](https://support.microsoft.com/kb/2919355) estão instaladas no servidor.|

![Imagem do erro de instalação do .NET no ATA](media/netinstallerror.png)


## Consulte também
- [Pré-requisitos do ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planejamento da capacidade de ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurar coleta de eventos](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configuração do encaminhamento de eventos do Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO1-->


