---
title: Investigando o reconhecimento usando DNS | Microsoft Docs
description: "Este artigo descreve o reconhecimento usando o DNS e fornece instruções de investigação quando essa ameaça é detectada pelo ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 5ec554b303a19a6e7b12cd788755604f1aaf43db
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*

# <a name="investigating-reconnaissance-using-dns"></a>Investigando o reconhecimento usando DNS

Se o ATA detectar o **Reconhecimento usando DNS** na sua rede e alertá-lo sobre isso, use esse artigo para ajudá-lo a investigar o alerta e entender como corrigir o problema.

## <a name="what-is-reconnaissance-using-dns"></a>O que é o reconhecimento usando DNS?

O alerta de **Reconhecimento usando DNS** indica que consultas DNS (Sistema de Nomes de Domínio) suspeitas estão sendo feitas de um host incomum para executar o reconhecimento na rede interna.

O DNS (Sistema de Nomes de Domínio) é um serviço implementado como um banco de dados hierárquico e distribuído que fornece a resolução de nomes de host e nomes de domínio. Os nomes em um banco de dados DNS formam uma estrutura de árvore hierárquica chamada de namespace de domínio.
Para um adversário, o DNS contém informações importantes para o mapeamento de uma rede interna, incluindo uma lista de todos os servidores e geralmente todos os clientes mapeados para seus endereços IP. Além disso, essa informação é valiosa porque ela lista os nomes de host que geralmente são descritivos em um determinado ambiente de rede. Ao recuperar essas informações, um adversário pode priorizar melhor seus esforços nas entidades relevantes durante uma campanha. Ferramentas como [Nmap](https://nmap.org/), [Fierce](https://github.com/mschwager/fierce) e ferramentas internas como [Nslookup](https://technet.microsoft.com/library/cc725991(v=ws.11).aspx) fornecem recursos para a descoberta de host usando o reconhecimento de DNS.
A detecção de reconhecimento usando consultas DNS de um host interno é causa de preocupação e um indicativo da possibilidade de um comprometimento de host existente, um comprometimento de rede mais amplo ou a possibilidade de uma ameaça interna.

## <a name="dns-query-types"></a>Tipos de consulta DNS

Há vários tipos de consulta no protocolo DNS. O ATA detecta as solicitações AXFR (transferência) e cria um alerta quando elas são vistas. Esse tipo de consulta deve vir apenas de servidores DNS.

## <a name="discovering-the-attack"></a>Descoberta do ataque

Quando um invasor tenta realizar o reconhecimento usando DNS, o ATA o detecta e o marca com a severidade média.

![O ATA detecta o reconhecimento de DNS](./media/dns-recon.png)
 
O ATA exibe o nome do computador de origem, bem como os detalhes adicionais sobre a consulta DNS real que foi executada. Por exemplo, pode haver várias tentativas feitas do mesmo host.

## <a name="investigating"></a>Investigação

Para investigar o reconhecimento usando DNS, primeiro você precisa determinar a causa das consultas. Elas podem ser identificadas em uma das categorias a seguir: 
-   Verdadeiros positivos – há um invasor ou malware mal-intencionado na rede. Isso pode ser um invasor que violou o perímetro da rede ou uma ameaça interna.
-   Verdadeiros positivos benignos – podem ser alertas disparados por testes de penetração, atividade da equipe vermelha, scanners de segurança, firewall de última geração ou administradores de TI realizando atividades sancionadas.
-   Falsos positivos – você poderá receber alertas que ocorrem devido a um erro de configuração, por exemplo, se a porta UDP 53 está bloqueada entre o Gateway do ATA e o servidor DNS (ou qualquer outro problema de rede).

O gráfico a seguir ajuda a determinar quais etapas de investigação você deve executar:

![Resolvendo o reconhecimento de DNS com o ATA](./media/dns-recon-diagram.png)
 
1.  A primeira etapa é identificar o computador do qual o alerta é originado, conforme descrito na tela a seguir:
 
    ![Exibir atividades suspeitas de reconhecimento de DNS no ATA](./media/dns-recon.png)
2.  Identifique o que este computador é. É uma estação de trabalho, um servidor, uma estação de trabalho de administração, um teste de penetração etc.?
3.  Se o computador for um servidor DNS e tiver direitos legítimos para solicitar uma cópia secundária da zona, ele será um falso positivo. Quando você encontrar um falso positivo, use a opção **Excluir** para que não receba mais esse alerta específico para esse computador.
4. Verifique se a porta UDP 53 está aberta entre o Gateway do ATA e o servidor DNS.
4.  Se o computador for usado para o trabalho de administração ou teste de penetração, será um verdadeiro positivo benigno e o computador envolvido também pode ser configurado como uma exceção.
5.  Se ele não for usado para testes de penetração, verifique se o computador está executando um scanner de segurança ou um firewall de última geração, que pode emitir solicitações DNS do tipo AXFR.
6.  Por fim, se nenhum desses critérios for atendido, é possível que o computador esteja comprometido e deverá ser totalmente investigado. 
7.  Se as consultas forem isoladas para computadores específicos e for determinado que não são benignas, as etapas a seguir deverão ser tratadas:
    1.  Examine as origens de log disponíveis. 
    2.  Conduza a análise baseada em host. 
    3.  Se a atividade não for de um usuário suspeito, deverá ser realizada a análise forense no computador para determinar se ele foi comprometido com malware.

## <a name="post-investigation"></a>Investigação de postagem

O malware usado para comprometer o host pode incluir cavalos de troia com recursos de backdoor. Em casos em que a movimentação lateral bem-sucedida foi identificada do host comprometido, as ações de correção devem se estender a esses hosts, incluindo alterar senhas e credenciais usadas no host e em qualquer host incluído na movimentação lateral. 

Em casos em que o host vítima não pode ser confirmado como limpo após as etapas de correção ou não é possível identificar a causa raiz do comprometimento, a Microsoft recomenda fazer backup de dados críticos e recriar o computador host. Além disso, os hosts novos ou recriados devem ser protegidos antes de serem colocados na rede para evitar uma nova infecção. 

A Microsoft recomenda consultar uma equipe profissional de Resposta a Incidentes e Recuperação, que pode ser contatada por meio da Equipe de contas da Microsoft, para ajudar a detectar se um invasor implantou métodos de persistência em sua rede.

## <a name="mitigation"></a>Atenuação

A proteção de um servidor DNS interno para impedir que o reconhecimento usando DNS ocorra pode ser obtida desabilitando ou restringindo as transferências de zona apenas para endereços IP específicos. Para obter mais informações sobre como restringir transferências de zona, confira [Restringir transferências de zona](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx). As transferências de zona podem ser bloqueadas [protegendo as transferências de zona com IPsec](https://technet.microsoft.com/library/ee649192(v=ws.10).aspx). A modificação de transferências de zona é uma tarefa entre uma lista de verificação deve ser resolvida para [proteger seus servidores DNS contra ataques internos e externos](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx).



## <a name="see-also"></a>Consulte também
- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
