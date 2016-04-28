---
# required metadata

title: O que é o Microsoft Advanced Threat Analytics (ATA)? | Microsoft Advanced Threat Analytics
description: Explica o que é o Microsoft Advanced Threat Analytics (ATA) e os tipos de atividades suspeitas que ele pode detectar
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


## O que é ATA?
O Microsoft Advanced Threat Analytics (ATA) é uma solução de segurança que ajuda profissionais de segurança de TI a proteger suas empresas contra ataques direcionados e ameaças internas. O ATA automaticamente analisa, aprende e identifica o comportamento normal e anormal de entidades (usuário, dispositivos e recursos) para identificar ataques mal-intencionados conhecidos, assim como técnicas, problemas de segurança e riscos. Usando informações e inteligência de pesquisadores de segurança de classe mundial, esta tecnologia inovadora destina-se a ajudar empresas a focar na identificação de violações de segurança antes elas que causem danos.

## O que o ATA faz?
O ATA detecta:

  - Ameaças avançadas persistentes (APTs) no início da cadeia de extermínio do ataque, antes que elas causem danos

  - Ameaças internas

  O ATA também permite que você separe o sinal do ruído para se concentrar no que é crítico.

O ATA tem um mecanismo de detecção que aproveita o aprendizado de máquina, as inspeções profundas de pacote de entidade contextuais, a análise de log e as informações do Active Directory (AD) para analisar o comportamento do usuário e da entidade.
O ATA analisa o tráfego em profundidade e aproveita o aprendizado de máquina para criar um mapa de como atividades normais, tráfego e uso aparecem em sua organização. Em seguida, o ATA inspeciona e notifica quando situações anormais acontecem. Esse resultado é realizado usando a tecnologia de inspeção profunda de pacotes da Microsoft (DPI). Essa tecnologia permite a inspeção de pacotes de entidade contextual de um nível mais profundo de análise de tráfego de rede, permitindo que o ATA analise todos os níveis de seu tráfego de rede.

O ATA também coleta eventos relevantes dos sistemas SIEM e dos controladores de domínio. Após a análise, o ATA cria uma exibição dinâmica e continuamente atualizada de todas as pessoas, dispositivos e recursos em uma organização. Usando essa visão abrangente, o ATA é capaz de detectar ataques mal-intencionados conhecidos como passagem de hash, passagem de tíquete, ataques de reconhecimento e outros. O ATA também procura qualquer anomalia no comportamento das entidades em sua rede.  

Quando uma atividade suspeita é detectada, o ATA emite um alerta – minimizando o número de falsos positivos que receber usando algoritmos avançados para agregação e verificação de contexto.


## Que tipos de ameaças o ATA procura?

O ATA fornece detecção para as várias fases de ataque avançado a seguir: reconhecimento, comprometimento de credenciais, movimentação lateral, elevação de privilégios, predominância de domínio e outros. Essas detecções visam detectar ataques avançados e ameaças internas antes que eles possam prejudicar sua organização.

A detecção de cada fase resulta em várias atividades suspeitas relevantes para a fase em questão. Cada atividade suspeita se correlaciona com diferentes tipos de ataques possíveis.


### Reconhecimento
O ATA fornece diversas detecções de reconhecimento. Por exemplo, a atividade suspeita de **Reconhecimento usando a enumeração de conta** detecta tentativas de invasores usando o protocolo Kerberos para descobrir a existência de um usuário, mesmo que a atividade não tenha sido registrada como um evento no controlador de domínio.

### Comprometimento de credenciais

Para fornecer detecção de credenciais comprometidas, o ATA aproveita a análise de comportamento baseado em aprendizado de máquina, assim como a de ataques mal-intencionados conhecidos e detecção de técnicas.  

Usando a análise comportamental e o aprendizado de máquina, o ATA é capaz de detectar atividades suspeitas como logons, acesso a recursos e horas de trabalho anormais. Qualquer uma dessas atividades suspeitas indicam um potencial comprometimento de credenciais.

Para proteger contra credenciais comprometidas, o ATA detecta os ataques mal-intencionados e técnicas conhecidos a seguir:

 - **Força bruta** – em ataques de força bruta, os invasores tentam adivinhar as credenciais do usuário tentando vários usuários e emparelhando-os com várias tentativas de senha. Os invasores geralmente usam algoritmos complexos ou dicionários para tentar todos os valores permitidos por um sistema.

- **Conta confidencial exposta na autenticação de texto sem formatação** – se as credenciais da conta com alto privilégio forem enviadas em texto sem formatação, o ATA envia um alerta para que você possa atualizar a configuração do computador.

- **Serviço expondo contas na autenticação de texto sem formatação** – se um serviço em um computador estiver enviando várias credenciais da conta em texto sem formatação, o ATA envia um alerta para que você possa atualizar a configuração do serviço.

- **Atividades suspeitas da conta Honey Token** – As contas Honey Token são contas fictícias configuradas para interceptar, identificar e rastrear atividades mal-intencionadas que tentam usar essas contas fictícias.

### Movimentação lateral
A movimentação lateral ocorre quando os usuários aproveitam as credenciais que fornecem acesso a alguns recursos para acessar outros recursos que eles não deveriam acessar. O ATA aproveita a análise de comportamento baseado em aprendizado de máquina, assim como a de ataques mal-intencionados conhecidos e detecção de técnicas para identificar essas movimentações laterais.  

O ATA detecta o acesso anormal aos recursos, dispositivos anormais usados e outros indicadores que evidenciam a movimentação lateral. Além disso, o ATA é capaz de detectar movimentação lateral por meio das técnicas usadas pelos invasores para realizar a movimentação lateral, como:
- **Passagem de tíquete** – em ataques de passagem de tíquete, os invasores roubam um tíquete Kerberos de um computador e usam-no para obter acesso a outro computador, representando uma entidade em sua rede.
- **Passagem de hash** – em ataques de passagem de hash, os invasores roubam o hash NTLM de uma entidade e usam-na para autenticar com NTLM e representar a entidade para obter acesso aos recursos da rede.
- **Excesso de passagem de hash** – excesso de passagem de hash são ataques em que o invasor usa um hash NTLM roubado para autenticar com o Kerberos e obter um tíquete TGT de Kerberos válido que é usado para autenticar como um usuário válido e obter acesso aos recursos da rede.

### Elevação de privilégios
Um ataque de elevação de privilégio ocorre quando os invasores tentam aumentar privilégios existentes e usá-los várias vezes para finalmente obter controle total sobre o ambiente da vítima. O ATA detecta ataques de elevação de privilégio bem-sucedidos e tentativas. O ATA usa análise comportamental para detectar comportamento anômalo de contas privilegiadas. O ATA também detecta ataques mal-intencionados conhecidos e as técnicas que geralmente são usadas para elevar privilégios, tais como:
- **Exploração de MS14-068 (PAC forjado)** – PAC forjado são ataques em que o invasor planta dados de autorização em seu tíquete TGT válido na forma de um cabeçalho de autorização forjado. Com essa técnica, o invasor obtém permissões que sua organização não lhe concedeu.
- O uso de credenciais anteriormente comprometidas ou de credenciais coletadas durante as operações de movimentação lateral.

### Predominância de domínio
A predominância de domínio ocorre quando os invasores tentam ou conseguem alcançar o controle total e a predominância sobre o ambiente da vítima. O ATA detecta essas tentativas procurando técnicas conhecidas usadas por invasores, que incluem:
- **Malware de chave de esqueleto** – em ataques de chave de esqueleto, o malware está instalado em seu controlador de domínio, permitindo que os invasores autentiquem como qualquer usuário, enquanto ainda permite que os usuários legítimos façam logon.
- **Tíquete de ouro** – em ataques de tíquete de ouro, um invasor rouba as credenciais do KBTGT, o tíquete de ouro do Kerberos. Esse tíquete permite que o invasor crie um tíquete TGT offline, que será usado novamente para acessar recursos na rede.
- **Execução remota** – os invasores podem tentar controlar sua rede executando códigos remotamente em seu controlador de domínio.


## O que fazer em seguida?

-   Para mais informações sobre como o ATA se adapta à sua rede, consulte: [Arquitetura de ATA](ata-architecture.md)

-   Para começar a implantar o ATA: [Instalar o ATA](/advanced-threat-analytics/DeployUse/install-ata)

## Consulte também
[Para obter suporte sobre o ATA, confira nosso fórum!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


