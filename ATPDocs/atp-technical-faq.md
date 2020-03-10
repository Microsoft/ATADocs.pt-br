---
title: Perguntas frequentes sobre a Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Fornece uma lista de perguntas frequentes sobre o Azure ATP e as respostas associadas
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 03/01/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 6a9b5273-eb26-414e-9cdd-f64406e24ed8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b8db17d50269463dda6340496463ac673a053462
ms.sourcegitcommit: c8b1e584ef42559a40afd62dac1b5ca9056c5602
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2020
ms.locfileid: "78926502"
---
# <a name="azure-atp-frequently-asked-questions"></a>Perguntas frequentes sobre o Azure ATP

Este artigo fornece uma lista de perguntas frequentes e respostas sobre o ATP do Azure, divididas nas seguintes categorias:

- [O que é o Azure ATP](#what-is-azure-atp)
- [Licenciamento e privacidade](#licensing-and-privacy)
- [Implantação](#deployment)
- [Operações](#operation)
- [Solução de problemas](#troubleshooting)

## <a name="what-is-azure-atp"></a>O que é o Azure ATP?

### <a name="what-can-azure-atp-detect"></a>O que pode o Azure ATP pode detectar?

O ATP do Azure detecta técnicas e ataques mal-intencionados conhecidos, problemas de segurança e riscos na rede.
Para obter a lista completa das detecções do Azure ATP, consulte [Quais detecções são realizadas pelo Azure ATP?](suspicious-activity-guide.md).

### <a name="what-data-does-azure-atp-collect"></a>Quais dados o Azure ATP coleta?

O Azure ATP coleta e armazena informações de seus servidores configurados (controladores de domínio, servidores membro etc.) em um banco de dados específico para o serviço para fins de administração, rastreamento e relatório. As informações coletadas incluem o tráfego de rede dos controladores de domínio (como autenticação Kerberos, autenticação NTLM, consultas DNS), logs de segurança (como eventos de segurança do Windows), informações do Active Directory (estrutura, sub-redes, sites) e informações de entidade (como nomes, endereços de email e números de telefone).

A Microsoft usa esses dados para:

- Identificar proativamente IOAs (indicadores de ataque) em sua organização
- Gerar alertas se um possível ataque for detectado
- Forneça a suas operações de segurança uma visão das entidades relacionadas aos sinais de ameaça de sua rede, permitindo que você investigue e explore a presença de ameaças à segurança na rede.

A Microsoft não explora seus dados para fornecer anúncios ou para qualquer outra finalidade que não seja fornecer o serviço.

### <a name="does-azure-atp-only-leverage-traffic-from-active-directory"></a>O Azure ATP aproveita apenas tráfego do Active Directory?

Além de analisar o tráfego do Active Directory usando a tecnologia de inspeção profunda de pacotes, o Azure ATP também coleta eventos do Windows relevantes do controlador de domínio e cria perfis de entidade com base nas informações do Active Directory Domain Services. O Azure ATP também dá suporte ao recebimento contabilidade RADIUS de logs VPN de vários fornecedores (Microsoft, Cisco, F5 e Checkpoint).

### <a name="does-azure-atp-monitor-only-domain-joined-devices"></a>O Azure ATP monitora somente dispositivos ingressados em domínio?

Não. O Azure ATP monitora todos os dispositivos na rede que executam solicitações de autenticação e autorização no Active Directory, incluindo dispositivos móveis e que não são do Windows.

### <a name="does-azure-atp-monitor-computer-accounts-as-well-as-user-accounts"></a>O Azure ATP monitora as contas de computador, bem como as contas de usuário?

Sim. Como as contas computador (bem como quaisquer outras entidades) podem ser usadas para executar atividades mal-intencionadas, o Azure ATP monitora todo o comportamento das contas de computador e todas as outras entidades no ambiente.

### <a name="what-is-the-difference-between-advanced-threat-analytics-ata-and-azure-atp"></a>Qual é a diferença entre o ATA (Advanced Threat Analytics) e o ATP do Azure?

O ATA é uma solução autônoma, instalada no local. O ATP do Azure, com sua conectividade em nuvem, possui atualizações contínuas de recursos, incluindo novas detecções, recursos de UEBA, avaliações de segurança e uma experiência de investigação em soluções da Segurança do Microsoft 365.

Recursos adicionais do ATP do Azure:

- O ATP do Azure detecta mais ataques avançados e comportamentos suspeitos no local do que o ATA e fornece relatórios de **avaliação de segurança de identidade**.
- Sensor reformulado com fontes de dados adicionais (como **Rastreamento de Eventos para Windows**).
- O ATP do Azure protege ambientes de várias florestas.

O ATP do Azure faz parte da Segurança do Microsoft 365 – protegendo a organização híbrida:

- O ATP do Azure, junto com o MCAS (Microsoft Cloud App Security) e o Azure AD Identity Protection, proporciona uma experiência de investigação unificada para atividades do usuário, locais e na nuvem, e fornece detecções aprimoradas de UEBA (Análise de Comportamento de Usuários e Entidades).
- O ATA não tem integração com outras soluções de segurança online da Microsoft

Escalonável e seguro, aproveitando o potencial da nuvem:

- O ATP do Azure permite que os clientes aproveitem os benefícios de uma solução baseada em nuvem, sem limitações de dimensionamento e com atualizações contínuas.
- O ATA é baseado em um servidor de gerenciamento central local que exige um hardware dedicado para que o centro de gerenciamento seja implantado no local e, normalmente, recebe uma ou duas atualizações de versão por ano.

## <a name="licensing-and-privacy"></a>Licenciamento e privacidade

### <a name="where-can-i-get-a-license-for-azure-advanced-threat-protection-atp"></a>Onde posso obter uma licença do Azure ATP (Proteção Avançada contra Ameaças)?

O ATP do Azure está disponível no pacote Enterprise Mobility + Security 5 (EMS E5) e como uma licença autônoma. Você pode adquirir uma licença diretamente no [Portal do Microsoft 365](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing) ou por meio do CSP (Parceiro de Soluções na Nuvem).

### <a name="does-azure-atp-need-only-a-single-license-or-does-it-require-a-license-for-every-user-i-want-to-protect"></a>O ATP do Azure precisa de uma única licença ou requer uma licença para cada usuário que desejo proteger?

O ATP do Azure requer licenciamento para cada usuário.

### <a name="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory"></a>Isto fará parte do Azure Active Directory ou do Active Directory local?

A solução ATP do Azure é uma oferta autônoma no momento. Ela não faz parte do Azure Active Directory ou do Active Directory local.

### <a name="is-my-data-isolated-from-other-customer-data"></a>Meus dados são isolados de outros dados do cliente?

Sim, seus dados são isolados por meio da autenticação de acesso e da diferenciação lógica com base nos identificadores do cliente. Cada cliente pode acessar somente dados coletados de sua própria organização e dados genéricos fornecidos pela Microsoft.

### <a name="do-i-have-the-flexibility-to-select-where-to-store-my-data"></a>É tenho flexibilidade para selecionar onde armazenar meus dados?

Não. Quando sua instância do ATP do Azure é criada, ela é armazenada automaticamente no data center nacional mais próximo da localização geográfica do seu locatário do AAD. Os dados do ATP do Azure não podem ser movidos depois que sua instância do ATP do Azure é criada em um data center diferente.

### <a name="how-does-microsoft-prevent-malicious-insider-activities-and-abuse-of-high-privilege-roles"></a>Como a Microsoft impede atividades internas mal-intencionadas e abuso de funções de alto privilégio?

Os administradores e desenvolvedores da Microsoft, por design, recebem privilégios suficientes para realizar as tarefas atribuídas a eles para operar e desenvolver o serviço. A Microsoft implanta combinações de controles preventivos, investigativos e reativos, incluindo os seguintes mecanismos para ajudar a proteger contra atividades administrativas e/ou de desenvolvedor não autorizadas:

- Controle de acesso total a dados confidenciais
- Combinações de controles que melhoram muito a detecção independente de atividades mal-intencionadas
- Vários níveis de monitoramento, registro em log e relatórios

Além disso, a Microsoft realiza verificações de histórico de determinados funcionários de operações e limita o acesso a aplicativos, sistemas e infraestrutura de rede proporcionalmente ao nível da verificação de histórico. A equipe de operações segue um processo formal quando precisa acessar a conta de um cliente ou informações relacionadas ao desempenho de suas tarefas.

## <a name="deployment"></a>Implantação

### <a name="how-many-azure-atp-sensors-do-i-need"></a>De quantos sensores do Azure ATP eu preciso?

Cada controlador de domínio no ambiente deve ser coberto por um sensor ou sensor autônomo do ATP. Para obter mais informações, confira [Azure ATP sensor sizing](atp-capacity-planning.md#sizing) (Dimensionamento do sensor do Azure ATP).

### <a name="does-azure-atp-work-with-encrypted-traffic"></a>O Azure ATP funciona com tráfego criptografado?

Os protocolos de rede com tráfego criptografado (por exemplo, AtSvc e WMI) não são descriptografados, mas são analisados pelos sensores.

### <a name="does-azure-atp-work-with-kerberos-armoring"></a>O Azure ATP funciona com Kerberos Armoring?

Há suporte para a habilitação do Kerberos Armoring, também conhecido como FAST (Flexible Authentication Secure Tunneling), pelo Azure ATP, com exceção da detecção de passagem pelo hash, que não funciona com o Kerberos Armoring.

### <a name="how-do-i-monitor-a-virtual-domain-controller-using-azure-atp"></a>Como monitorar um controlador de domínio virtual usando o Azure ATP?

A maioria dos controladores de domínio virtuais pode ser coberta pelo sensor do Azure ATP. Para determinar se o sensor do Azure ATP é apropriado para seu ambiente, consulte [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md).

Se um controlador de domínio virtual não puder ser coberto pelo sensor do Azure ATP, você pode ter um sensor autônomo do Azure ATP físico ou virtual, conforme descrito em [Configurar o espelhamento de porta](configure-port-mirroring.md).

A maneira mais fácil é ter um sensor autônomo do Azure ATP virtual em cada host no qual o controlador de domínio virtual existe.

Se os controladores de domínio virtuais se movimentarem entre os hosts, será necessário executar uma destas etapas:

- Quando o controlador de domínio virtual for movido para outro host, pré-configure o sensor autônomo do Azure ATP nesse host para receber o tráfego do controlador de domínio virtual movimentado recentemente.
- Não deixe de afiliar o sensor autônomo do Azure ATP virtual ao controlador de domínio virtual, de modo que se ele for movido, o sensor autônomo do Azure ATP será movido com ele.
- Há alguns comutadores virtuais que podem enviar o tráfego entre os hosts.

### <a name="how-do-i-configure-the-azure-atp-sensors-to-communicate-with-azure-atp-cloud-service-when-i-have-a-proxy"></a>Como posso configurar os sensores do Azure ATP para se comunicar com o serviço de nuvem do Azure ATP quando tiver um proxy?

Para seus controladores de domínio se comunicarem com o serviço de nuvem, você deve abrir: *. atp.azure.com porta 443 em seu firewall/proxy. Para obter instruções de como fazer isso, consulte [Configurar seu proxy ou firewall para habilitar a comunicação com sensores do Azure ATP](configure-proxy.md).

### <a name="can-azure-atp-monitored-domain-controllers-be-virtualized-on-your-iaas-solution"></a>Os controladores de domínio monitorados do ATP do Azure podem ser virtualizados em sua solução de IaaS?

Sim, você pode usar o sensor do Azure ATP para monitorar controladores de domínio em qualquer solução IaaS.

### <a name="can-azure-atp-support-multi-domain-and-multi-forest"></a>O Azure ATP pode dar suporte a vários domínios e várias florestas?

A Proteção Avançada contra Ameaças do Azure dá suporte a ambientes com vários domínios e com várias florestas. Confira mais informações e requisitos de confiança em [Suporte a várias florestas](atp-multi-forest.md).

### <a name="can-you-see-the-overall-health-of-the-deployment"></a>Você pode ver a integridade geral da implantação?

Sim, é possível exibir a integridade geral da implantação, bem como os problemas específicos relacionados à configuração, à conectividade e a outros aspectos. Você recebe alertas de integridade do ATP do Azure conforme eles ocorrem.

## <a name="operation"></a>Operação

### <a name="what-kind-of-integration-does-azure-atp-have-with-siems"></a>Que tipo de integração o Azure ATP tem com SIEMs?

O Azure ATP pode ser configurado para enviar um alerta de Syslog para qualquer servidor SIEM usando o formato CEF para alertas de integridade e caso uma atividade suspeita seja detectada. Consulte a [referência de log do SIEM](cef-format-sa.md) para obter mais informações.

### <a name="why-are-certain-accounts-considered-sensitive"></a>Por que certas contas são consideradas confidenciais?

Isso ocorre quando uma conta é membro de grupos designados como confidenciais (por exemplo: "Administradores do Domínio").

Para entender por que uma conta é confidencial, você pode examinar sua associação de grupo para entender a quais grupos confidenciais ela pertence (o grupo ao qual ela pertence também pode ser confidencial devido a outro grupo, portanto, o mesmo processo deve ser executado até que você localize o grupo confidencial de nível mais alto). Você também pode [marcar contas como confidenciais](sensitive-accounts.md) manualmente.

### <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>Você precisa escrever suas próprias regras e criar um limite/linha de base?

Com a Proteção Avançada contra Ameaças do Azure, não é necessário criar regras, limites ou linhas de base e, em seguida, ajustar. O ATP do Azure analisa os comportamentos entre os usuários, dispositivos e recursos, bem como o relacionamento entre eles, e pode detectar atividades suspeitas e ataques conhecidos rapidamente. Embora algumas detecções incluam um período de aprendizado, para muitas detecções, o ATP do Azure começará a detectar os ataques mal-intencionados conhecidos e os problemas de segurança imediatamente após a implantação. Todos os períodos de aprendizado estão documentados nos tópicos de alerta relevantes listados no [Guia de alertas de segurança](suspicious-activity-guide.md).

### <a name="which-traffic-does-azure-atp-generate-in-the-network-from-domain-controllers-and-why"></a>Qual tráfego o ATP do Azure gera na rede dos controladores de domínio e por quê?

O ATP do Azure gera tráfego dos controladores de domínio para os computadores da organização em um dos três cenários:

1. **Resolução de Nomes de Rede**  
   O ATP do Azure captura o tráfego e os eventos, aprendendo e criando perfis para usuários e atividades de computadores na rede. Para aprender e criar perfis das atividades de acordo com os computadores da organização, o ATP do Azure precisa resolver os IPs de acordo com as contas dos computadores. Para resolver IPs dos nomes dos computadores, os sensores do ATP do Azure solicitam o endereço IP do nome do computador *por trás* do endereço IP.

   As solicitações são feitas com um dos quatro métodos a seguir:
    - NTLM sobre RPC (porta TCP 135)
    - NetBIOS (porta UDP 137)
    - RDP (TCP porta 3389)
    - Consulta ao servidor DNS usando a pesquisa de DNS reverso do endereço IP (UDP 53)

    Depois de obter o nome do computador, os sensores do ATP do Azure executam uma verificação cruzada dos detalhes no Active Directory para ver se há um objeto de computador correlacionado com o mesmo nome do computador. Se encontrarem a correspondência, é feita uma associação entre o endereço IP e o objeto do computador correspondido.
2. **LMP (caminho de movimento lateral)**  
    Para criar LMPs potenciais para usuários confidenciais, o ATP do Azure requer informações sobre os administradores locais nos computadores. Neste cenário, o sensor do ATP do Azure usa SAM-R (TCP 445) para consultar o endereço IP identificado no tráfego de rede a fim de determinar os administradores locais do computador. Para saber mais sobre o ATP do Azure e SAM-R, confira [Configurar permissões necessárias do SAM-R](install-atp-step8-samr.md).

3. **Consulta ao Active Directory usando o LDAP** sobre dados de entidades  
    Os sensores do ATP do Azure consultam o controlador de domínio a partir do domínio ao qual a entidade pertence. Pode ser no mesmo sensor ou em outro controlador de domínio daquele domínio.

|Protocolo|Serviço|Porta|Origem| Direção|
|---------|---------|---------|---------|--------|
|LDAP|TCP e UDP|389|Controladores de domínio|Saída|
|LDAP seguro (LDAPS)|TCP|636|Controladores de domínio|Saída|
|LDAP para o Catálogo Global|TCP|3268|Controladores de domínio|Saída|
|LDAPS para o Catálogo Global|TCP|3269|Controladores de domínio|Saída|
|

### <a name="why-dont-activities-always-show-both-the-source-user-and-computer"></a>Por que as atividades sempre mostram o computador e o usuário da origem?

O ATP do Azure captura as atividades de vários protocolos diferentes. Em alguns casos, o ATP do Azure não recebe os dados do usuário de origem no tráfego. O ATP do Azure tenta correlacionar a sessão do usuário com a atividade e, quando a tentativa for bem-sucedida, o usuário de origem da atividade será exibido. Caso as tentativas de correlação do usuário falhem, apenas o computador de origem será exibido.

## <a name="troubleshooting"></a>Solução de problemas

### <a name="what-should-i-do-if-the-azure-atp-sensor-or-standalone-sensor-doesnt-start"></a>O que devo fazer se o sensor ou o sensor autônomo do Azure ATP não for iniciado?

Procure o erro mais recente no [log](troubleshooting-atp-using-logs.md) de erros atual (onde o Azure ATP está instalado, na pasta "Logs").

## <a name="see-also"></a>Consulte Também

- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md)
- [Solução de problemas](troubleshooting-atp-known-issues.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
