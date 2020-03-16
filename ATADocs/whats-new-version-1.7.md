---
title: Novidades na versão 1.7 do ATA
description: Lista as novidades na nova versão 1.7 do ATA e seus problemas conhecidos
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 1/23/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: be9ee613-4eb3-40f1-8973-e7f0a707ff57
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: db393df81a922cf7362e5705376c9d72fe13e363
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2020
ms.locfileid: "79414379"
---
# <a name="whats-new-in-ata-version-17"></a>Novidades na versão 1.7 do ATA
Estas notas de versão fornecem informações sobre problemas conhecidos nesta versão da Advanced Threat Analytics.

## <a name="whats-new-in-the-ata-17-update"></a>Quais são as novidades na atualização 1.7 do ATA?
A atualização 1.7 do ATA fornece melhorias nas seguintes áreas:

-   Detecções novas e atualizadas

-   Controle de acesso baseado em funções

-   Suporte para Windows Server 2016 e Windows Server 2016 Core

-   Aprimoramentos da experiência do usuário

-   Alterações secundárias


### <a name="new--updated-detections"></a>Detecções novas e atualizadas


- **Reconhecimento usando a enumeração dos serviços de diretório** Como parte da fase de reconhecimento, os invasores coletam informações sobre as entidades na rede usando métodos diferentes. A enumeração dos serviços de diretório usando o protocolo SAM-R permite que os invasores obtenham a lista de usuários e grupos em um domínio e compreendam a interação entre as diferentes entidades. 

- **Aprimoramentos de passagem de hash** Para melhorar a detecção de Passagem de Hash, adicionamos outros modelos comportamentais aos padrões de autenticação de entidades. Esses modelos permitem que o ATA correlacione o comportamento da entidade com autenticações NTLM suspeitas e diferencie ataques de Passagem de Hash reais do comportamento de cenários falsos positivos.

- **Aprimoramentos de Passagem de tíquete** Para detectar com êxito ataques avançados em geral e, particularmente, o ataque de Passagem de Tíquete, a correlação entre um endereço IP e a conta do computador deve ser precisa. Esse é um desafio em ambientes nos quais os endereços IP mudam rapidamente por padrão (por exemplo, redes Wi-Fi e várias máquinas virtuais compartilhando no mesmo host). Para superar esse desafio e melhorar a precisão da detecção de Passagem de tíquete, o mecanismo NNR (Resolução de Nome de Rede) do ATA foi aprimorado consideravelmente a fim de reduzir os falsos positivos.

- **Aprimoramentos para comportamentos anormais** No ATA 1.7, os dados de autenticação de NTLM foram adicionados como uma fonte de dados para as detecções de comportamento anormal, fornecendo os algoritmos com uma cobertura mais ampla do comportamento da entidade na rede. 

- **Aprimoramentos para implementação de protocolo incomum** Agora, o ATA detecta a implementação incomum de protocolo no protocolo Kerberos, juntamente com anomalias adicionais no protocolo NTLM. Especificamente, essas novas anomalias para Kerberos são usadas normalmente em ataques Excesso de passagem de Hash.


### <a name="infrastructure"></a>Infraestrutura

- **Controle de acesso baseado em função** O recurso RBAC (Controle de acesso baseado em função). O ATA 1.7 inclui três funções: Administrador do ATA, Analista do ATA e Executivo do ATA.

- **Suporte para Windows Server 2016 e Windows Server Core** O ATA 1.7 dá suporte à implantação de Lightweight Gateways em controladores de domínio que executam o Windows Server 2008 R2 SP1 (sem incluir o Server Core), o Windows Server 2012, o Windows Server 2012 R2, o Windows Server 2016 (incluindo o Core, mas não o Nano). Além disso, esta versão oferece suporte ao Windows Server 2016 para os componentes do Centro de ATA e do Gateway do ATA.

### <a name="user-experience"></a>Experiência do usuário
- **Experiência de configuração** Nesta versão, a experiência de configuração do ATA foi reprojetada para proporcionar uma experiência de usuário melhor e para oferecer um suporte mais adequado a ambientes com vários Gateways do ATA. Esta versão também apresenta a página de atualização do Gateway do ATA para um gerenciamento mais simples das atualizações automáticas para os diversos Gateways.

## <a name="known-issues"></a>Problemas conhecidos
A seguir estão os problemas conhecidos existentes nesta versão.

### <a name="gateway-automatic-update-may-fail"></a>Atualização automática do Gateway pode falhar
**Sintomas:** em ambientes com links WAN lentos, a atualização do Gateway do ATA pode atingir o tempo limite para a atualização (100 segundos) e não ser concluída.
No Console do ATA, o Gateway do ATA terá o status de "Atualizando (baixando pacote)" por um longo período e, eventualmente, falhará.
**Solução alternativa:** para contornar esse problema, baixe o pacote mais recente do Gateway do ATA no Console do ATA e atualize o Gateway do ATA manualmente.

> [!IMPORTANT]
>  Não há suporte para a renovação automática de certificados para os certificados usados pelo ATA. O uso desses certificados pode fazer com que o ATA deixe de funcionar quando o certificado é renovado automaticamente. 

### <a name="no-browser-support-for-jis-encoding"></a>Não há suporte do navegador para codificação JIS
**Sintomas:** o Console ATA podem não funcionar conforme o esperado em navegadores que usam a codificação JIS **Solução:** alterar a codificação do navegador Unicode UTF-8.
 
### <a name="dropped-port-mirror-traffic-when-using-vmware"></a>Tráfego espelhado por porta descartado ao usar o VMware

Alertas de tráfego espelhado por porta descartados ao usar o gateway lightweight no VMware.

Se você estiver usando controladores de domínio em máquinas virtuais VMware, você poderá receber alertas sobre o **Tráfego de rede espelhado por porta descartado**. Isso pode ocorrer devido a uma incompatibilidade de configuração no VMware. Para evitar esses alertas, verifique se as configurações a seguir estão definidas como 0 ou Desabilitado na máquina virtual:  

- TsoEnable
- LargeSendOffload(IPv4)
- Descarregamento TSO IPv4

Além disso, considere desabilitar o Descarregamento TSO gigante do IPv4. Para obter mais informações, consulte a documentação do VMware.

### <a name="automatic-gateway-update-fail-when-updating-to-17-update-1"></a>Falha de atualização automática do Gateway ao atualizar para a versão 1.7 atualização 1

Ao atualizar do ATA 1.7 para o ATA 1.7 atualização 1, o processo de atualização automática do Gateway do ATA e a instalação manual dos Gateways usando o pacote do Gateway podem não funcionar conforme o esperado.
Esse problema ocorrerá se o certificado usado pelo Centro do ATA foi alterado antes de atualizar o ATA.
Para verificar esse problema, examine o **Microsoft.Tri.Gateway.Updater.log** no Gateway do ATA e procure as seguintes exceções: **System.Net.Http.HttpRequestException: Ocorreu um erro ao enviar a solicitação. ---> System.Net.WebException: A conexão subjacente estava fechada: Ocorreu um erro inesperado em um envio. ---> System.IdentityModel.Tokens.SecurityTokenValidationException: Falha ao validar a impressão digital do certificado**

![Bug de gateway da atualização do ATA](media/17update_gatewaybug.png)

Para resolver esse problema, depois de alterar o certificado em um prompt de comandos com privilégios elevados, navegue até o seguinte local: **%ProgramFiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** e execute o seguinte:

1. Mongo.exe ATA (ATA deve estar em letras maiúsculas) 

2. CenterThumbprint=db.SystemProfile.find({_t:"CenterSystemProfile"}).toArray()[0].Configuration.SecretManagerConfiguration.CertificateThumbprint;

3. db.SystemProfile.update({_t:"ServiceSystemProfile"},{$set:{"Configuration.ManagementClientConfiguration.ServerCertificateThumbprint":CenterThumbprint}}, {multi: true})

### <a name="export-suspicious-activity-details-to-excel-may-fail"></a>Exportar detalhes de atividade suspeita para o Excel pode falhar
Ao tentar exportar os detalhes de atividade suspeita para um arquivo do Excel, a operação pode falhar com o seguinte erro: *Erro [BsonClassMapSerializer`1] System.FormatException: Um erro ocorreu ao desserializar a propriedade Atividade da classe Microsoft.Tri.Common.Data.NetworkActivities.SuspiciousActivityActivity: Elemento 'ResourceIdentifier' não corresponde a nenhum campo ou propriedade de classe Microsoft.Tri.Common.Data.EventActivities.NtlmEvent. ---> System.FormatException: O Elemento 'ResourceIdentifier' não corresponde a nenhum campo ou propriedade da classe Microsoft.Tri.Common.Data.EventActivities.NtlmEvent.*

Para resolver esse problema, em um prompt de comandos com privilégios elevados, navegue até o seguinte local: **%ProgramFiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** e execute os seguintes comandos:
1.  `Mongo.exe ATA` (ATA deve estar em letras maiúsculas)
2.  `db.SuspiciousActivityActivity.update({ "Activity._t": "NtlmEvent" },{$unset: {"Activity.ResourceIdentifier": ""}}, {multi: true});`

## <a name="minor-changes"></a>Alterações secundárias

- Agora, o ATA está usando OWIN em vez de IIS para o Console de ATA.
- Se o serviço Centro de ATA estiver inativo, não será possível acessar o Console do ATA.
- As sub-redes de concessão de curto prazo não serão mais necessárias devido a alterações no NNR do ATA.

## <a name="see-also"></a>Confira Também
[Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Atualizar o ATA para a versão 1.7 — guia de migração](ata-update-1.7-migration-guide.md)

