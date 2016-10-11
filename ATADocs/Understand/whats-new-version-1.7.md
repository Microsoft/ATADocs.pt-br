---
title: "Novidades na versão 1.7 do ATA | Microsoft ATA"
description: "Lista as novidades na nova versão 1.7 do ATA e seus problemas conhecidos"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 09/20/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 
ms.reviewer: 
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d47d9e7be294c68d764710c15c4bb78539e42f62
ms.openlocfilehash: 62f2aadc978547647a1dc3c27ed3453f7ed15828


---

# Novidades na versão 1.7 do ATA
Estas notas de versão fornecem informações sobre problemas conhecidos nesta versão da Advanced Threat Analytics.

## Quais são as novidades na atualização 1.7 do ATA?
A atualização 1.7 do ATA fornece melhorias nas seguintes áreas:

-   Detecções novas e atualizadas

-   Controle de acesso baseado em função

-   Compatível com Windows Server 2016 e o Windows Server Core

-   Aprimoramentos da experiência do usuário

-   Alterações secundárias


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

 > [!IMPORTANT]
 Não há suporte para a renovação automática de certificados para os certificados usados pelo ATA. O uso desses certificados pode fazer com que o ATA deixe de funcionar quando o certificado é renovado automaticamente. 

### Não há suporte do navegador para codificação JIS
**Sintomas:** o Console ATA podem não funcionar conforme o esperado em navegadores que usam a codificação JIS **Solução:** alterar a codificação do navegador Unicode UTF-8.
 
## Alterações secundárias

- Agora, o ATA está usando OWIN em vez de IIS para o Console de ATA.
- Se o serviço Centro de ATA estiver inativo, você não poderá acessar o Console do ATA.
- As sub-redes de concessão de curto prazo não serão mais necessárias devido a alterações no NNR do ATA.

## Consulte também
[Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Atualizar o ATA para a versão 1.7 — guia de migração](ata-update-1.7-migration-guide.md)




<!--HONumber=Sep16_HO4-->


