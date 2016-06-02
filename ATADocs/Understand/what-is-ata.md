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
ATA (Microsoft Advanced Threat Analytics) é uma solução líder na análise comportamental de usuários e entidades que ajuda os profissionais de TI a proteger sua organização contra APTs (ataques direcionados avançados) e ameaças internas. Ao analisar, aprender e identificar automaticamente comportamentos (usuário, dispositivos e recursos) normais e anômalos da entidade usando tecnologia de aprendizado de máquina avançada, o ATA ajuda a identificar ataques mal-intencionados e técnicas, problemas de segurança e riscos conhecidos. Usando informações e inteligência de pesquisadores de segurança de classe mundial, esta tecnologia inovadora destina-se a ajudar empresas a focar na identificação de violações de segurança antes elas que causem danos.

## O que o ATA faz?
O ATA detecta:

  - Ameaças avançadas persistentes (APTs) no início da cadeia de extermínio do ataque, antes que elas causem danos

  - Ameaças internas

O ATA ajuda a separar atividades suspeitas de pistas falsas, para se concentrar no que é crítico.

O mecanismo de detecção do ATA aproveita o aprendizado de máquina, as inspeções profundas de pacote de entidade contextuais, a análise de log e as informações do AD (Active Directory) para analisar o comportamento do usuário e da entidade.

O ATA executa uma análise em profundidade do tráfego da sua organização e aproveita o aprendizado de máquina para criar um mapa de como atividades normais, tráfego e uso aparecem em sua organização. Em seguida, o ATA inspeciona e notifica quando situações anormais acontecem. Isso é feito com a execução de tecnologia DPI (deep packet inspection), que permite a inspeção de pacotes de entidade contextual de um nível mais profundo de análise de tráfego de rede, permitindo que o ATA analise todos os níveis de seu tráfego de rede.

O ATA também coleta eventos relevantes dos sistemas SIEM e dos controladores de domínio. Após a análise, o ATA cria uma exibição dinâmica e continuamente atualizada de todas as pessoas, dispositivos e recursos em uma organização. Usando essa visão abrangente, o ATA é capaz de detectar ataques mal-intencionados, como passagem de hash, passagem de tíquete, ataques de reconhecimento e outros, além de procurar anormalidades no comportamento de entidades na sua rede.

Quando uma atividade suspeita é detectada, o ATA emite um alerta – minimizando o número de falsos positivos que receber usando algoritmos avançados para agregação e verificação de contexto.



## Que tipos de ameaças o ATA procura?

O ATA fornece detecção para as seguintes várias fases de ataque avançado: reconhecimento, comprometimento de credenciais, movimentação lateral, elevação de privilégios, predominância de domínio e outros. Essas detecções visam detectar ataques avançados e ameaças internas antes que eles possam causar danos à sua organização.

A detecção de cada fase resulta em várias atividades suspeitas relevantes para a fase em questão, em que cada atividade suspeita se correlaciona com diferentes tipos de ataques possíveis.

### Reconhecimento
O ATA fornece diversas detecções de reconhecimento. Essas detecções incluem:

-   **Reconhecimento de enumeração de conta**<br>Detecta tentativas de invasores usando o protocolo Kerberos para descobrir a existência de um usuário, mesmo que a atividade não tenha sido registrada como um evento no controlador de domínio.
-   **Enumeração da sessão Net**<br>
Como parte da fase de reconhecimento, os invasores podem consultar o DC de todas as sessões SMB ativas no servidor, o que permite que eles obtenham acesso a todos os usuários e endereços IP associados a essas sessões SMB. A enumeração da sessão SMB pode ser usada pelos invasores para acessar contas confidenciais, o que os ajuda a se mover lateralmente na rede.
-   **Reconhecimento usando DNS**<br>
Informações de DNS na rede de destino geralmente são informações de reconhecimento muito úteis. As informações de DNS contêm uma lista de todos os servidores e, muitas vezes, de todos os clientes, e o mapeamento para seus endereços IP. A exibição de informações de DNS pode fornecer aos invasores uma visão detalhada dessas entidades no seu ambiente, permitindo que eles concentrem seus esforços em entidades relevantes para a campanha.

### Credenciais comprometidas

Para fornecer detecção de credenciais comprometidas, o ATA aproveita a análise de comportamento baseado em aprendizado de máquina, assim como a de ataques mal-intencionados conhecidos e detecção de técnicas.

Usando a análise comportamental e o aprendizado de máquina, o ATA é capaz de detectar atividades suspeitas como logons, acesso a recursos e horas de trabalho anômalas. o que poderia indicar um comprometimento de credenciais.
Para proteger contra credenciais comprometidas, o ATA detecta os ataques mal-intencionados e técnicas conhecidos a seguir:
:

 - **Força bruta** <br>Em ataques de força bruta, os invasores tentam adivinhar as credenciais do usuário tentando vários usuários e emparelhando-os com várias tentativas de senha. Os invasores geralmente usam algoritmos complexos ou dicionários para tentar todos os valores permitidos por um sistema.

- **Conta confidenciais expostas na autenticação de texto sem formatação**<br>
Se as credenciais de conta com alto privilégio forem enviadas em texto sem formatação, o ATA envia um alerta para que você possa atualizar a configuração do computador.

- **Serviço que expõe contas na autenticação de texto sem formatação** <br>
Se um serviço em um computador estiver enviando várias credenciais da conta em texto sem formatação, o ATA envia um alerta para que você possa atualizar a configuração do serviço.

- **Atividades suspeitas de conta Honey Token**<br>
As contas Honey Token são contas fictícias configuradas para interceptar, identificar e rastrear atividades mal-intencionadas que tentam usar essas contas fictícias. O ATA alertas sobre todas as atividades entre essas contas Honey Tokens.
-   **Implementação de protocolo incomum**<br>
As solicitações de autenticação (Kerberos ou NTLM) normalmente são executadas usando um conjunto normal de protocolos e métodos. No entanto, para autenticar com êxito, a solicitação só deve atender a um conjunto específico de requisitos. Os invasores podem implementar esses protocolos com pequenos desvios da implementação normal no ambiente. Esses desvios podem indicar a presença de um invasor tentando ou efetivamente se aproveitando de credenciais comprometidas.
-   **Solicitação de informações privadas para proteção contra dados mal-intencionados**<br>
A DPAPI (API de Proteção de Dados) é um serviço de proteção de dados baseado em senha. Esse serviço de proteção é usado por vários aplicativos que armazenam segredos do usuário, como senhas de site e as credenciais de compartilhamento de arquivos. Para dar suporte a cenários de perda de senha, os usuários poderão descriptografar os dados protegidos usando uma chave de recuperação que não envolva a senha deles. Em um ambiente de domínio, os invasores podem roubar a chave de recuperação remotamente e usá-la para descriptografar os dados protegidos em todos os computadores ingressados no domínio.
-   **Comportamento anômalo**<br>
Muitas vezes em casos de ameaças internas e de ataques avançados, as credenciais da conta podem ser comprometidas usando métodos de engenharia social ou métodos e técnicas novos e ainda não conhecidos. O ATA é capaz de detectar esses tipos de comprometimento, analisar o comportamento da entidade e detectar e alertar anomalias nas operações executadas pela entidade.

### Movimentação lateral
Para fornecer detecção de movimentação lateral, quando os usuários se aproveitarem de credenciais que fornecem acesso a alguns recursos para obter recursos de acesso que eles não deveriam acessar, o ATA usa a análise de comportamento baseada em aprendizado de máquina e detecção de técnicas e ataques mal-intencionados.

Usando análise comportamental e aprendizado de máquina, o ATA detecta o acesso anormal aos recursos, dispositivos anômalos usados e outros indicadores que evidenciam a movimentação lateral.

Além disso, o ATA é capaz de detectar movimentação lateral por meio das técnicas usadas pelos invasores para realizar a movimentação lateral, como:

- **Passagem de tíquete (Pass the ticket)** <br>
Em ataques de passagem de tíquete, os invasores roubam um tíquete Kerberos de um computador e usam-no para obter acesso a outro computador, representando uma entidade em sua rede.
- **Passagem de hash (Pass the hash)** <br>
Em ataques de passagem de hash, os invasores roubam o hash NTLM de uma entidade e usam-na para autenticar com NTLM e representar a entidade para obter acesso aos recursos da rede.
- **Excesso de passagem de hash (Over-pass the hash)**<br>
Excesso de passagem de hash são ataques em que o invasor usa um hash NTLM roubado para autenticar com o Kerberos e obter um tíquete TGT de Kerberos válido que é usado para autenticar como um usuário válido e obter acesso aos recursos da rede.
-   **Comportamento anômalo**<br>
A movimentação lateral é uma técnica normalmente usada pelos invasores para mover entre dispositivos e áreas na rede da vítima a fim de obter acesso a credenciais com altos privilégios ou informações confidenciais de interesse ao invasor. O ATA é capaz de detectar movimentação lateral analisando o comportamento dos usuários, o dispositivos e suas relações dentro da rede corporativa, e de detectar padrões de acesso anômalos que podem indicar movimentação lateral executada por um invasor.

### Elevação de privilégios
O ATA detecta tentativas e efetivos ataques de elevação de privilégio, nos quais os invasores tentam aumentar privilégios existentes e usá-los várias vezes para finalmente obter controle total sobre o ambiente da vítima. 

O ATA habilita a detecção de escalonamento de privilégio combinando com análise comportamental para detectar comportamentos anômalos de contas privilegiadas e detectar técnicas e ataques conhecidos e mal-intencionados que geralmente são usados para escalonar privilégios, como:

- **Exploração de MS14-068 (PAC forjado)**<br>
PAC forjado é um tipo de ataque em que o invasor planta dados de autorização em seu tíquete TGT válido na forma de um cabeçalho de autorização forjado que lhe dá permissões adicionais que não foram dadas pela organização. Neste cenário, o invasor se aproveita de credenciais comprometidas anteriormente ou credenciais coletadas durante as operações de movimentação lateral.
- **Exploração de MS11-013 (Silver PAC)**<br>
Os ataques de exploração de MS11-013 são uma vulnerabilidade na elevação de privilégio no Kerberos que permite que determinados aspectos de um tíquete do serviço Kerberos sejam forjados. Um usuário mal-intencionado ou um invasor que explorasse com êxito essa vulnerabilidade poderia obter um token com privilégios elevados no controlador de domínio. Neste cenário, o invasor se aproveita de credenciais comprometidas anteriormente ou credenciais coletadas durante as operações de movimentação lateral.

### Predominância de domínio
O ATA detecta invasores tentando ou efetivamente conseguindo obter dominância e controle total sobre o ambiente da vítima pela execução de detecção de técnicas conhecidas usadas pelos invasores, que incluem:

- **Malware Skeleton key**<br>
Em ataques de Skeleton key, o malware está instalado em seu controlador de domínio, permitindo que os invasores autentiquem como qualquer usuário, enquanto ainda permite que os usuários legítimos façam logon.
- **Golden ticket**<br>
Em ataques de golden ticket, um invasor rouba as credenciais do KBTGT, o tíquete de ouro do Kerberos. Esse tíquete permite que o invasor crie um tíquete TGT offline, que será usado novamente para acessar recursos na rede.
- **Execução remota**<br>
Os invasores podem tentar controlar sua rede executando códigos remotamente em seu controlador de domínio.
-   **Solicitações de replicação mal-intencionada**
Em ambientes do AD (Active Directory), a replicação ocorre regularmente entre Controladores de Domínio. Um invasor pode falsificar uma solicitação de replicação do AD (às vezes representando um Controlador de Domínio), permitindo que o invasor recupere os dados armazenados no AD, incluindo hashes de senha, sem utilizar técnicas mais invasivas como a Cópia de Sombra de Volume.

## Novidades

-   Para saber mais sobre como o ATA se adapta à sua rede: [Arquitetura do ATA](/advanced-threat-analytics/plan-design/ata-architecture)

-   Para começar a implantar o ATA: [Instalar o ATA](/advanced-threat-analytics/deploy-use/install-ata)

## Consulte também
[Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


