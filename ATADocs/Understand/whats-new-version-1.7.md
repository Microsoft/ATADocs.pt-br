---
title: "Novidades na versão 1.7 do ATA | Microsoft ATA"
description: "Lista as novidades na nova versão 1.7 do ATA e seus problemas conhecidos"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 
ms.reviewer: 
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ae6a3295d2fffabdb8e5f713674379e4af499ac2
ms.openlocfilehash: af9101260b1a0d5d9da32398f638f76e0c8c40a7


---

# Novidades na versão 1.7 do ATA
Estas notas de versão fornecem informações sobre problemas conhecidos nesta versão da Advanced Threat Analytics.

## Quais são as novidades na atualização 1.7 do ATA?
A atualização 1.7 do ATA fornece melhorias nas seguintes áreas:

-   Detecções novas e atualizadas

-   Controle de acesso baseado em função

-   Compatível com Windows Server 2016 e o Windows Server Core

-   Aprimoramentos da experiência do usuário


### Detecções novas e atualizadas


- **Reconhecimento usando a enumeração dos serviços de diretório** Como parte da fase de reconhecimento, os invasores coletam informações sobre as entidades na rede usando métodos diferentes. A enumeração dos serviços de diretório usando o protocolo SAM-R permite que os invasores obtenham a lista de usuários e grupos em um domínio e compreendam a interação entre as diferentes entidades. 

- **Aprimoramentos de passagem de hash** Para melhorar a detecção de Passagem de Hash, adicionamos outros modelos comportamentais aos padrões de autenticação de entidades. Esses modelos permitem que o ATA correlacione o comportamento da entidade com autenticações NTLM suspeitas e diferencie ataques de Passagem de Hash reais do comportamento de cenários falsos positivos.

- **Aprimoramentos de Passagem de tíquete** Para detectar com êxito ataques avançados em geral e, particularmente, o ataque de Passagem de Tíquete, a correlação entre um endereço IP e a conta do computador deve ser precisa. Esse é um desafio em ambientes nos quais os endereços IP mudam rapidamente por padrão (por exemplo, redes Wi-Fi e várias máquinas virtuais compartilhando no mesmo host). Para superar esse desafio e melhorar a precisão da detecção de Passagem de tíquete, o mecanismo NNR (Resolução de Nome de Rede) do ATA foi aprimorado consideravelmente a fim de reduzir os falsos positivos.

- **Aprimoramentos para comportamentos anormais** No ATA 1.7, os dados de autenticação de NTLM foram adicionados como uma fonte de dados para as detecções de comportamento anormal, fornecendo os algoritmos com uma cobertura mais ampla do comportamento da entidade na rede. 

- **Aprimoramentos para implementação de protocolo incomum** Agora, o ATA detecta a implementação incomum de protocolo no protocolo Kerberos, juntamente com anomalias adicionais no protocolo NTLM. Especificamente, essas novas anomalias para Kerberos são usadas normalmente em ataques Excesso de passagem de Hash.


### Infraestrutura

- **Controle de acesso baseado em função** O recurso RBAC (Controle de acesso baseado em função). O ATA 1.7 inclui três funções: Administrador do ATA, Analista do ATA e Executivo do ATA.

- **Suporte para Windows Server 2016 e Windows Server Core** O ATA 1.7 oferece suporte à implantação de Lightweight Gateways em controladores de domínio que executam o Server Core para Windows Server 2012 e o Server Core para Windows Server 2012 R2. Além disso, esta versão oferece suporte ao Windows Server 2016 para os componentes do Centro de ATA e do Gateway do ATA.

### Experiência de usuário
- **Experiência de configuração** Nesta versão, a experiência de configuração do ATA foi reprojetada para proporcionar uma experiência de usuário melhor e para oferecer um suporte mais adequado a ambientes com vários Gateways do ATA. Esta versão também apresenta a página de atualização do Gateway do ATA para um gerenciamento mais simples das atualizações automáticas para os diversos Gateways.

## Problemas conhecidos
A seguir estão os problemas conhecidos existentes nesta versão.

### Atualização automática do Gateway pode falhar
**Sintomas:** em ambientes com links WAN lentos, a atualização do Gateway do ATA pode atingir o tempo limite para a atualização (100 segundos) e não ser concluída.
No Console do ATA, o Gateway do ATA terá o status de "Atualizando (baixando pacote)" por um longo período e, eventualmente, falhará.

**Solução alternativa:** para contornar esse problema, baixe o pacote mais recente do Gateway do ATA no Console do ATA e atualize o Gateway do ATA manualmente.

### Falha de migração ao atualizar do ATA 1.6
Ao atualizar para o ATA 1.7, o processo de atualização pode falhar com o seguinte código de erro *0x80070643*:

![Erro ao atualizar o ATA para 1.7](media/ata-update-error.png)

Examine o log de implantação para descobrir a causa da falha. O log de implantação está localizado no seguinte local,**%temp%\..\Microsoft Advanced Thread Analytics Center_{date_stamp}_MsiPackage.log**. 

A tabela a seguir lista os erros para procura e o script Mongo correspondente para corrigir o erro. Consulte o exemplo abaixo da tabela sobre como executar o script Mongo:

| Erro no arquivo de log de implantação                                                                                                                  | Script do Mongo                                                                                                                                                                         |
|---|---|
| System.FormatException: Size {size}, é maior do que MaxDocumentSize 16777216 <br>Mais para baixo no arquivo:<br>  Microsoft.Tri.Center.Deployment.Package.Actions.DatabaseActions.MigrateUniqueEntityProfiles(Boolean isPartial)                                                                                        | db.UniqueEntityProfile.find().forEach(function(obj){if(Object.bsonsize(obj) > 12582912) {print(obj._id);print(Object.bsonsize(obj));db.UniqueEntityProfile.remove({_id:obj._id});}}) |
| System.OutOfMemoryException: a exceção do tipo 'System.OutOfMemoryException' foi lançada<br>Mais para baixo no arquivo:<br>Microsoft.Tri.Center.Deployment.Package.Actions.DatabaseActions.ReduceSuspiciousActivityDetailsRecords(IMongoCollection`1 suspiciousActivityCollection, Int32 deletedDetailRecordMaxCount) | db.SuspiciousActivity.find().forEach(function(obj){if(Object.bsonsize(obj) > 500000),{print(obj._id);print(Object.bsonsize(obj));db.SuspiciousActivity.remove({_id:obj._id});}})     |
|System.Security.Cryptography.CryptographicException: Comprimento inválido<br>Mais para baixo no arquivo:<br> Microsoft.Tri.Center.Deployment.Package.Actions.DatabaseActions.MigrateCenterSystemProfile(IMongoCollection`1 systemProfileCollection)| CenterThumbprint=db.SystemProfile.find({_t:"CenterSystemProfile"}).toArray()[0].Configuration.SecretManagerConfiguration.CertificateThumbprint;db.SystemProfile.update({_t:"CenterSystemProfile"},{$set:{"Configuration.ManagementClientConfiguration.ServerCertificateThumbprint":CenterThumbprint}})|


Para executar o script apropriado, siga as etapas a seguir. 

1.  Em um prompt de comandos com privilégios elevados, navegue até o local a seguir: **\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**
2.  Digite – **Mongo.exe ATA**   (*Observação*: ATA deve estar em letras maiúsculas.)
3.  Cole o script que coincide com o erro no log de implantação da tabela acima.

![Script do Mongo ATA](media/ATA-mongoDB-script.png)

Neste ponto, você deve ser capaz de reiniciar a atualização.

### O ATA relata um grande número de atividades suspeitas de "*Reconhecimento usando enumerações de serviços de diretório*":
 
Será mais provável que isso ocorra se houver uma ferramenta de varredura de rede em execução em todos os (ou vários) computadores cliente da organização. Se esse problema estiver ocorrendo:

1. Se você puder identificar o motivo ou o aplicativo específico que está em execução nos computadores cliente, envie um email para ATAEval em Microsoft.com com as informações.
2. Use o seguinte script mongo para ignorar todos esses eventos (veja acima como executar o script mongo):

db.SuspiciousActivity.update({_t: "SamrReconnaissanceSuspiciousActivity"}, {$set: {Status: "Dismissed"}}, {multi: true})

### O ATA envia notificações para atividades suspeitas ignoradas:
Se as notificações foram configuradas, o ATA poderá continuar enviando notificações (email, syslog e logs de eventos) para atividades suspeitas ignoradas.
Não há solução alternativa para esse problema no momento. 

### O Gateway do ATA poderá falhar ao se registrar com o Centro do ATA se o TLS 1.0 e o TLS 1.1 estiverem desabilitados:
Se o TLS 1.0 e o TLS 1.1 estiverem desabilitados no Gateway do ATA (ou Lightweight Gateway), o gateway poderá falhar ao se registrar no Centro do ATA

### A renovação de certificado automática para os certificados usados pelo ATA não tem suporte
O uso da renovação de certificado automática pode fazer com que o ATA pare de funcionar quando o certificado for renovado automaticamente. 


## Confira Também
[Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Atualizar o ATA para a versão 1.7 — guia de migração](ata-update-1.7-migration-guide.md)




<!--HONumber=Sep16_HO2-->


