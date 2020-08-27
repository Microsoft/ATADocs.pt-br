---
title: Perguntas frequentes sobre a análise avançada de ameaças
description: Fornece uma lista de perguntas frequentes sobre o ATA e as respostas associadas.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/07/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: df882d70067dd3408bd4dee6ad5f3d7ac1a24618
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88953823"
---
# <a name="ata-frequently-asked-questions"></a>Perguntas frequentes sobre o ATA

*Aplica-se a: Advanced Threat Analytics versão 1.9*

Este artigo fornece uma lista de perguntas frequentes sobre o ATA e também as respostas e outras informações.

## <a name="where-can-i-get-a-license-for-advanced-threat-analytics-ata"></a>Onde posso obter uma licença para o ATA (Advanced Threat Analytics)?

Se você tiver um Enterprise Agreement ativo, poderá baixar o software do VLSC (Centro de Licenciamento por Volume da Microsoft).

Se você adquiriu uma licença para o Enterprise Mobility + Security (EMS) diretamente pelo portal Microsoft 365 ou por meio do modelo de licença do CSP(Cloud Solution Partner) e não tiver acesso ao ATA por meio do Microsoft VLSC (Volume Licensing Center), entre em contato com o atendimento ao cliente da Microsoft para obter o processo para ativar o ATA (Advanced Threat Analytics).

## <a name="what-should-i-do-if-the-ata-gateway-wont-start"></a>O que devo fazer se o gateway do ATA não for iniciado?

Procure o erro mais recente no log de erros atual (No local onde o ATA está instalado, na pasta "Logs").

## <a name="how-can-i-test-ata"></a>Como posso testar o ATA?

Você pode simular atividades suspeitas, que é um teste de ponta a ponta, seguindo um destes procedimentos:

1. Reconhecimento de DNS usando Nslookup.exe
1. Execução remota usando psexec.exe

Isso deve ser executado remotamente no controlador de domínio que está sendo monitorado e não no Gateway do ATA.

## <a name="which-ata-build-corresponds-to-each-version"></a>Qual build do ATA corresponde a cada versão?

Para obter informações de atualização de versão, consulte [Caminho de atualização do ATA](upgrade-path.md).

## <a name="what-version-should-i-use-to-upgrade-my-current-ata-deployment-to-the-latest-version"></a>Qual versão devo usar para atualizar a implantação atual do ATA para a versão mais recente?

Para obter a matriz de atualização de versão do ATA, consulte [Caminho de atualização do ATA](upgrade-path.md).

## <a name="how-does-the-ata-center-update-its-latest-signatures"></a>Como o Centro do ATA atualiza suas assinaturas mais recentes?

O mecanismo de detecção do ATA é aprimorado quando uma nova versão é instalada no Centro do ATA. É possível atualizar o Centro usando o MU (Microsoft Update) ou manualmente, baixando a nova versão do Centro de Download ou do Site de Licenças por Volume.

## <a name="how-do-i-verify-windows-event-forwarding"></a>Como verificar o Encaminhamento de Eventos do Windows?

Você pode inserir o código a seguir em um arquivo e, em seguida, executá-lo em um prompt de comando no diretório:  **\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** da seguinte maneira:

nome do arquivo ATA mongo.exe

```
db.getCollectionNames().forEach(function(collection) {
    if (collection.substring(0,10)=="NtlmEvent_") {
        if (db[collection].count() > 0) {
            print ("Found "+db[collection].count()+" NTLM events") 
        }
    }
});
```

## <a name="does-ata-work-with-encrypted-traffic"></a>O ATA funciona com tráfego criptografado?

O ATA se baseia na análise de vários protocolos de rede, bem como em eventos coletados do SIEM ou por meio de Encaminhamento de Eventos do Windows. Detecções com base em protocolos de rede com tráfego criptografado (por exemplo, LDAPS e IPSEC) não serão analisadas.

## <a name="does-ata-work-with-kerberos-armoring"></a>O ATA funciona com Kerberos Armoring?

Há suporte para a habilitação do Kerberos Armoring, também conhecido como FAST (encapsulamento seguro de autenticação flexível), pelo ATA, com exceção da detecção de passagem pelo hash, que não funcionará.

## <a name="how-many-ata-gateways-do-i-need"></a>De quantos Gateways de ATA eu preciso?

O número de Gateways do ATA depende de seu layout de rede, do volume de pacotes e do volume de eventos capturados pelo ATA. Para determinar o número exato, consulte [Dimensionamento do Gateway Lightweight do ATA](ata-capacity-planning.md#ata-lightweight-gateway-sizing). 

## <a name="how-much-storage-do-i-need-for-ata"></a>Qual a quantidade de armazenamento necessária para o ATA?

Para cada dia inteiro com uma média de 1000 pacotes/s, você precisa de 0.3 GB de armazenamento. Para saber mais sobre consulte dimensionamento do Centro do ATA, confira [planejamento de capacidade do ATA](ata-capacity-planning.md).

## <a name="why-are-certain-accounts-considered-sensitive"></a>Por que certas contas são consideradas confidenciais?

Isso ocorre quando uma conta é membro de determinados grupos que podemos chamar de confidenciais (por exemplo: "Administradores do Domínio").

Para entender por que uma conta é confidencial, você pode examinar sua associação de grupo para entender a quais grupos confidenciais ela pertence (o grupo ao qual ela pertence também pode ser confidencial devido a outro grupo, portanto, o mesmo processo deve ser executado até que você localize o grupo confidencial de nível mais alto).

Além disso, você pode marcar manualmente um usuário, um grupo ou um computador como confidencial. Para obter mais informações, veja [Marcar contas confidenciais](tag-sensitive-accounts.md).

## <a name="how-do-i-monitor-a-virtual-domain-controller-using-ata"></a>Como monitorar o controlador de domínio virtual usando o ATA?

A maioria dos controladores de domínio virtuais pode ser abrangida pelo Gateway Lightweight do ATA. Para determinar se o Gateway Lightweight do ATA é apropriado para seu ambiente, confira [Planejamento de capacidade do ATA](ata-capacity-planning.md).

Se um controlador de domínio virtual não pode ser usado com Gateway Lightweight do ATA, você pode ter Gateway do ATA físico ou virtual conforme descrito em [Configurar o espelhamento de porta](configure-port-mirroring.md).  

A maneira mais fácil é ter um Gateway de ATA virtual em cada host no qual o controlador de domínio virtual exista. Se os controladores de domínio virtuais se movimentarem entre os hosts, será necessário executar uma destas etapas:

- Quando o controlador de domínio virtual for movido para outro host, pré-configure o Gateway do ATA nesse host para receber o tráfego do controlador de domínio virtual movimentado recentemente.
- Verifique se você afiliou o Gateway do ATA virtual ao controlador de domínio virtual, de modo que se ele for movido, o Gateway do ATA será movido com ele.
- Há alguns comutadores virtuais que podem enviar o tráfego entre os hosts.

## <a name="how-do-i-back-up-ata"></a>Como fazer backup do ATA?

Consulte [Recuperação de desastre de ATA](disaster-recovery.md)

## <a name="what-can-ata-detect"></a>O que o ATA pode detectar?

O ATA detecta técnicas e ataques mal-intencionados e conhecidos, problemas de segurança e riscos.
Para obter a lista completa das detecções do ATA, consulte [Quais detecções são realizadas pelo ATA?](ata-threats.md).

## <a name="what-kind-of-storage-do-i-need-for-ata"></a>Qual tipo de armazenamento eu preciso para o ATA?

Recomendamos o armazenamento rápido (discos de 7200 RPM não são recomendados) com acesso ao disco de baixa latência (menos de 10 ms). A configuração de RAID deve dar suporte a cargas pesadas de gravação (RAID-5/6 e seus derivados não são recomendados).

## <a name="how-many-nics-does-the-ata-gateway-require"></a>De quantos NICs o Gateway de ATA precisa?

O Gateway de ATA requer um mínimo de dois adaptadores de rede:<br>1. uma NIC para se conectar à rede interna e ao centro do ATA<br>2. uma NIC que é usada para capturar o tráfego de rede do controlador de domínio por meio do espelhamento de porta.<br>* Isso não se aplica ao Gateway Lightweight do ATA, que usa nativamente todos os adaptadores de rede que o controlador de domínio usa.

## <a name="what-kind-of-integration-does-ata-have-with-siems"></a>Que tipo de integração o ATA tem com o SIEMs?

O ATA tem uma integração bidirecional com o SIEMs, da seguinte maneira:

1. O ATA pode ser configurado para enviar um alerta de Syslog a qualquer servidor SIEM usando o formato CEF no caso de uma atividade suspeita.
1. O ATA pode ser configurado para receber mensagens do Syslog eventos do Windows [destes SIEMs](install-ata-step6.md).

## <a name="can-ata-monitor-domain-controllers-virtualized-on-your-iaas-solution"></a>O ATA pode monitorar controladores de domínio visualizados em sua solução IaaS?

Sim, você pode usar o Gateway Lightweight do ATA para monitorar controladores de domínio em qualquer solução IaaS.

## <a name="is-this-an-on-premises-or-in-cloud-offering"></a>Isto é uma oferta local ou na nuvem?

O Microsoft Advanced Threat Analytics é um produto no local.

## <a name="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory"></a>Isto fará parte do Azure Active Directory ou do Active Directory local?

Esta solução é atualmente uma oferta autônoma; ela não faz parte do Azure Active Directory ou do Active Directory local.

## <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>Você precisa escrever suas próprias regras e criar um limite/linha de base?

Com o Microsoft Advanced Threat Analytics, não é necessário criar regras, limites ou linhas de base e, em seguida, ajustar. O ATA analisa os comportamentos entre os usuários, dispositivos e recursos — bem como sua relação um com o outro — e pode detectar atividades suspeitas e ataques conhecidos rapidamente. Três semanas após a implantação, o ATA começa a detectar as atividades suspeitas do comportamento. Por outro lado, o ATA começará a detectar os ataques mal-intencionados conhecidos e os problemas de segurança imediatamente após a implantação.

## <a name="if-you-are-already-breached-can-microsoft-advanced-threat-analytics-identify-abnormal-behavior"></a>Se você já sofreu uma violação, o Microsoft Advanced Threat Analytics será capaz de identificar um comportamento anormal?

Sim, mesmo quando o ATA for instalado depois de você ter sofrido a violação, ainda poderá detectar atividades suspeitas do hacker. O ATA não apenas examina o comportamento do usuário, mas também em relação aos outros usuários no mapa de segurança da organização. Durante o tempo de análise inicial, se o comportamento do invasor for anormal, ele será identificado como uma "exceção" e o ATA manterá relatórios sobre o comportamento anormal. Além disso, o ATA poderá detectar uma atividade suspeita se o hacker tentar roubar outras credenciais dos usuários, como a Passagem de Tíquete, ou tentar realizar uma execução remota em um dos controladores de domínio.

## <a name="does-this-only-leverage-traffic-from-active-directory"></a>Isto aproveita apenas o tráfego do Active Directory?

Além de analisar o tráfego do Active Directory usando a tecnologia de inspeção profunda de pacotes, o ATA também pode coletar eventos relevantes das Informações de Segurança e do Gerenciamento de Eventos (SIEM), e criar perfis de entidade com base nas informações dos Serviços de Domínio do Active Directory. O ATA também poderá coletar eventos dos logs de eventos se a organização configurar o encaminhamento do Log de Eventos do Windows.

## <a name="what-is-port-mirroring"></a>O que é espelhamento de porta?

Também conhecido como SPAN (Switched Port Analyzer), o espelhamento de porta é um método de monitorar o tráfego da rede. Com o espelhamento de porta habilitado, a opção envia uma cópia de todos os pacotes de rede vistos em uma porta (ou uma VLAN inteira) para outra porta, onde o pacote pode ser analisado.

## <a name="does-ata-monitor-only-domain-joined-devices"></a>O ATA monitora somente os dispositivos de domínio?

Não. O ATA monitora todos os dispositivos na rede que executam solicitações de autenticação e autorização no Active Directory, incluindo os dispositivos móveis e não Windows.

## <a name="does-ata-monitor-computer-accounts-as-well-as-user-accounts"></a>O ATA monitora as contas de computador, bem como as contas de usuário?

Sim. Como as contas de computador (bem como quaisquer outras entidades) podem ser usadas para executar atividades mal-intencionadas, o ATA monitora todo o comportamento das contas de computador e todas as outras entidades no ambiente.

## <a name="can-ata-support-multi-domain-and-multi-forest"></a>O ATA pode dar suporte a vários domínios e várias florestas?

O Microsoft Advanced Threat Analytics oferece suporte a ambientes com vários domínios dentro dos mesmos limites de floresta. Várias florestas exigem uma implantação do ATA para cada floresta.

## <a name="can-you-see-the-overall-health-of-the-deployment"></a>Você pode ver a integridade geral da implantação?

Sim, é possível exibir a integridade geral da implantação, bem como os problemas específicos relacionados à configuração, conectividade, etc., e você recebe um alerta quando ocorrerem.

## <a name="see-also"></a>Consulte Também

- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Planejamento da capacidade do ATA](ata-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-collection.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
