---
title: Perguntas frequentes sobre o ATA | Microsoft Advanced Threat Analytics
description: Fornece uma lista de perguntas frequentes sobre o ATA e as respostas associadas.
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: bb6bc2bf0d0df3112ecfdb33c8e9d6e41f183145


---

# Perguntas frequentes sobre o ATA
Este artigo fornece uma lista de perguntas frequentes sobre o ATA e também as respostas e outras informações.


## Como o ATA é licenciado?
Para obter informações sobre licenciamento, confira [How to buy Advanced Threat Analytics](https://www.microsoft.com/server-cloud/products/advanced-threat-analytics/Purchasing.aspx) (Como comprar o Advanced Threat Analytics)


## O que devo fazer se o Gateway do ATA não inicia?
Procure o erro mais recente no log de erros atual (No local onde o ATA está instalado, na pasta "Logs").
## Como posso testar o ATA?
Você pode simular atividades suspeitas, que é um teste de ponta a ponta, seguindo um destes procedimentos:

1.  Reconhecimento de DNS usando Nslookup.exe
2.  Execução remota usando psexec.exe


Isso deve ser executado remotamente no controlador de domínio que está sendo monitorado e não no Gateway do ATA.

## Como verificar o Encaminhamento de Eventos do Windows?
Você pode executar o seguinte em um prompt de comando no diretório:  **\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**:

        mongo ATA --eval "printjson(db.getCollectionNames())" | find /C "NtlmEvents"`
## O ATA funciona com tráfego criptografado?
O tráfego criptografado não será analisado (por exemplo: LDAPS, ESP IPSEC).
## O ATA funciona com Kerberos Armoring?
Há suporte para a habilitação do Kerberos Armoring, também conhecido como FAST (encapsulamento seguro de autenticação flexível), pelo ATA, com exceção da detecção de passagem pelo hash, que não funcionará.
## De quantos Gateways de ATA eu preciso?

Primeiro, é recomendável usar Gateways Lightweight do ATA em controladores de domínio que podem acomodá-los. Para determinar isso, confira [Dimensionamento do Gateway Lightweight do ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning#ata-lightweight-gateway-sizing). 

Se todos os controladores de domínio puderem ser abordados pelos Gateways Lightweight do ATA, não haverá a necessidade de Gateways do ATA.

Para controladores de domínio que não podem ser usados com Gateway Lightweight do ATA, considere o seguinte ao decidir quantos Gateways do ATA serão necessários:

 - A quantidade total de tráfego que os controladores de domínio produzem e a arquitetura de rede (para configurar o espelhamento de porta). Para ler mais sobre como determinar a quantidade de tráfego produzido por seus controladores de domínio, confira [Estimativa de tráfego do controlador de domínio](/advanced-threat-analytics/plan-design/ata-capacity-planning#Domain-controller-traffic-estimation).
 - As limitações operacionais do espelhamento de porta também determinam a quantidade de Gateways do ATA que você precisa para oferecer suporte a todos os controladores de domínio, por exemplo: por comutador, por datacenter, por região. Cada ambiente tem seus próprios aspectos. 

## Qual a quantidade de armazenamento necessária para o ATA?
Para cada dia inteiro com uma média de 1000 pacotes/s, você precisa de 0.3 GB de armazenamento.<br /><br />Para saber mais sobre consulte dimensionamento do Centro do ATA, confira [planejamento de capacidade do ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning).


## Por que certas contas são consideradas confidenciais?
Isso ocorre quando uma conta é membro de determinados grupos que podemos chamar de confidenciais (por exemplo: "Administradores do Domínio").

Para entender por que uma conta é confidencial, você pode examinar sua associação de grupo para entender a quais grupos confidenciais ela pertence (o grupo ao qual ela pertence também pode ser confidencial devido a outro grupo, portanto, o mesmo processo deve ser executado até que você localize o grupo confidencial de nível mais alto).

## Como monitorar o controlador de domínio virtual usando o ATA?
A maioria dos controladores de domínio virtuais pode ser abrangida pelo Gateway Lightweight do ATA. Para determinar se o Gateway Lightweight do ATA é apropriado para seu ambiente, confira [Planejamento de capacidade do ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning).

Se um controlador de domínio virtual não pode ser usado com Gateway Lightweight do ATA, você pode ter Gateways do ATA físicos ou virtuais conforme descrito em [Configurar o espelhamento de porta](/advanced-threat-analytics/deploy-use/configure-port-mirroring).  <br />A maneira mais fácil é ter um Gateway de ATA virtual em cada host no qual o controlador de domínio virtual exista.<br />Se os controladores de domínio virtuais se movimentarem entre os hosts, será necessário executar um destes procedimentos:

-   Quando o controlador de domínio virtual for movido para outro host, pré-configure o Gateway do ATA nesse host para receber o tráfego do controlador de domínio virtual movimentado recentemente.
-   Verifique se você afiliou o Gateway do ATA virtual ao controlador de domínio virtual, de modo que se ele for movido, o Gateway do ATA será movido com ele.
-   Há alguns comutadores virtuais que podem enviar o tráfego entre os hosts.

## Como fazer backup do ATA?
Há duas coisas das quais fazer backup:

-   O tráfego e os eventos armazenados pelo ATA, que podem sobre backup usando qualquer procedimento de backup de banco de dados com suporte, para saber mais, confira [Gerenciamento de banco de dados do ATA](/advanced-threat-analytics/deploy-use/ata-database-management). 
-   A configuração do ATA, que é armazenada no banco de dados e copiada em backup automaticamente a cada hora. 

## O que o ATA pode detectar?
O ATA detecta técnicas e ataques mal-intencionados e conhecidos, problemas de segurança e riscos.
Para obter a lista completa de detecções do ATA, confira [O que é o Microsoft Advanced Threat Analytics?](what-is-ata.md).

## Qual tipo de armazenamento eu preciso para o ATA?
Recomendamos o armazenamento rápido (discos de 7.200 RPM não são recomendados) com acesso ao disco de baixa latência (menos de 10 ms). A configuração de RAID deve dar suporte a cargas pesadas de gravação (RAID-5/6 e seus derivados não são recomendados).

## De quantos NICs o Gateway de ATA precisa?
O Gateway de ATA requer um mínimo de dois adaptadores de rede:<br>1. Uma NIC para se conectar à rede interna e à Central de ATA<br>2. Uma NIC que será usado para capturar o tráfego de rede do controlador de domínio por meio do espelhamento de porta.<br>* Isso não se aplica ao Gateway Lightweight do ATA, que usa nativamente todos os adaptadores de rede que o controlador de domínio usa.

## Que tipo de integração o ATA tem com o SIEMs?
O ATA tem uma integração bidirecional com o SIEMs, da seguinte maneira:

1. O ATA pode ser configurado para enviar um alerta de Syslog, no caso de uma atividade suspeita, para qualquer servidor SIEM usando o formato CEF.
2. O ATA pode ser configurado para receber mensagens do Syslog para cada evento do Windows com a ID 4776, destes [SIEMs](/advanced-threat-analytics/deploy-use/configure-event-collection#siem-support).

## O ATA pode monitorar controladores de domínio visualizados em sua solução IaaS?

Sim, você pode usar o Gateway Lightweight do ATA para monitorar controladores de domínio em qualquer solução IaaS.

## Isto é uma oferta local ou na nuvem?
O Microsoft Advanced Threat Analytics é um produto no local.

## Isto fará parte do Azure Active Directory ou do Active Directory local?
Esta solução é atualmente uma oferta autônoma; ela não faz parte do Azure Active Directory ou do Active Directory local.

## Você precisa escrever suas próprias regras e criar um limite/linha de base?
Com o Microsoft Advanced Threat Analytics, não é necessário criar regras, limites ou linhas de base e, em seguida, ajustar. O ATA analisa os comportamentos entre os usuários, dispositivos e recursos — bem como sua relação um com o outro — e pode detectar atividades suspeitas e ataques conhecidos rapidamente. Três semanas após a implantação, o ATA começa a detectar as atividades suspeitas do comportamento. Por outro lado, o ATA começará a detectar os ataques mal-intencionados conhecidos e os problemas de segurança imediatamente após a implantação.

## Se você já sofreu uma violação, o Microsoft Advanced Threat Analytics será capaz de identificar um comportamento anormal?
Sim, mesmo quando o ATA for instalado depois de você ter sofrido a violação, ainda poderá detectar atividades suspeitas do hacker. O ATA não está vendo apenas o comportamento do usuário, mas também os outros usuários no mapa de segurança da organização. Durante a análise inicial, se o comportamento do invasor for anormal, ele será identificado como uma "exceção" e o ATA continuará informando sobre o comportamento anormal. Além disso, o ATA poderá detectar uma atividade suspeita se o hacker tentar roubar outras credenciais dos usuários, como a Passagem de Tíquete, ou tentar realizar uma execução remota em um dos controladores de domínio.

## Isto aproveita apenas o tráfego do Active Directory?
Além de analisar o tráfego do Active Directory usando a tecnologia de inspeção profunda de pacotes, o ATA também pode coletar eventos relevantes das Informações de Segurança e do Gerenciamento de Eventos (SIEM), e criar perfis de entidade com base nas informações dos Serviços de Domínio do Active Directory. O ATA também poderá coletar eventos dos logs de eventos se a organização configurar o encaminhamento do Log de Eventos do Windows.

## O que é espelhamento de porta?
Também conhecido como SPAN (Switched Port Analyzer), o espelhamento de porta é um método de monitorar o tráfego da rede. Com o espelhamento de porta habilitado, a opção envia uma cópia de todos os pacotes de rede vistos em uma porta (ou uma VLAN inteira) para outra porta, onde o pacote pode ser analisado.

## O ATA monitora somente os dispositivos de domínio?
Não. O ATA monitora todos os dispositivos na rede que executam solicitações de autenticação e autorização no Active Directory, incluindo os dispositivos móveis e não Windows.

## O ATA monitora as contas de computador, bem como as contas de usuário?
Sim. Como as contas de computador (bem como quaisquer outras entidades) podem ser usadas para executar atividades mal-intencionadas, o ATA monitora todo o comportamento das contas de computador e todas as outras entidades no ambiente.

## O ATA pode dar suporte a vários domínios e várias florestas?
Na disponibilidade geral, o Microsoft Advanced Threat Analytics oferecerá suporte a vários domínios com o mesmo limite de floresta. A floresta propriamente dita é o verdadeiro "limite de segurança", de modo que dar suporte a vários domínios permitirá que os clientes tenham 100% de cobertura de seus ambientes com o ATA.

## Você pode ver a integridade geral da implantação?
Sim, é possível exibir a integridade geral da implantação, bem como os problemas específicos relacionados à configuração, conectividade, etc., e você será alertado quando ocorrerem.


## Consulte também
- [Pré-requisitos do ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planejamento da capacidade de ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurar coleta de eventos](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configuração do encaminhamento de eventos do Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#Configuring-Windows-Event-Forwarding)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Jun16_HO4-->


