---
title: Perguntas frequentes sobre o Microsoft defender para identidade
description: Fornece uma lista de perguntas frequentes sobre o Microsoft defender para identidade e as respostas associadas
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b677512817fc910c5845fa7e1544003bfec60593
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848934"
---
# <a name="product-long-frequently-asked-questions"></a>[!INCLUDE [Product long](includes/product-long.md)] perguntas frequentes

Este artigo fornece uma lista de perguntas e respostas frequentes sobre [!INCLUDE [Product long](includes/product-long.md)] dividida nas seguintes categorias:

- [O que é [!INCLUDE [Product short](includes/product-short.md)]](#what-is-azure-atp)
- [Licenciamento e privacidade](#licensing-and-privacy)
- [Implantação](#deployment)
- [Operações](#operation)
- [Solução de problemas](#troubleshooting)

<a name="what-is-azure-atp"></a>

## <a name="what-is-product-short"></a>O que é o [!INCLUDE [Product short](includes/product-short.md)]?

### <a name="what-can-product-short-detect"></a>O que pode [!INCLUDE [Product short](includes/product-short.md)] detectar?

[!INCLUDE [Product short](includes/product-short.md)] detecta ataques maliciosos e técnicas, problemas de segurança e riscos conhecidos em sua rede.
Para obter a lista completa de [!INCLUDE [Product short](includes/product-short.md)] detecções, consulte [quais detecções o [!INCLUDE [Product short](includes/product-short.md)] executa?](suspicious-activity-guide.md).

### <a name="what-data-does-product-short-collect"></a>Quais dados são [!INCLUDE [Product short](includes/product-short.md)] coletados?

[!INCLUDE [Product short](includes/product-short.md)] coleta e armazena informações de seus servidores configurados (controladores de domínio, servidores membros, etc.) em um banco de dados específico para o serviço para fins de administração, rastreamento e relatório. As informações coletadas incluem o tráfego de rede dos controladores de domínio (como autenticação Kerberos, autenticação NTLM, consultas DNS), logs de segurança (como eventos de segurança do Windows), informações do Active Directory (estrutura, sub-redes, sites) e informações de entidade (como nomes, endereços de email e números de telefone).

A Microsoft usa esses dados para:

- Identificar proativamente IOAs (indicadores de ataque) em sua organização
- Gerar alertas se um possível ataque for detectado
- Forneça a suas operações de segurança uma visão das entidades relacionadas aos sinais de ameaça de sua rede, permitindo que você investigue e explore a presença de ameaças à segurança na rede.

A Microsoft não explora seus dados para fornecer anúncios ou para qualquer outra finalidade que não seja fornecer o serviço.

### <a name="how-many-directory-service-credentials-does-product-short-support"></a>Quantas credenciais de serviço de diretório [!INCLUDE [Product short](includes/product-short.md)] dão suporte?

[!INCLUDE [Product short](includes/product-short.md)] Atualmente, o dá suporte à adição de até 10 credenciais de serviço de diretório diferentes para dar suporte a ambientes Active Directory com florestas não confiáveis. Se você precisar de mais contas, abra um tíquete de suporte.

### <a name="does-product-short-only-leverage-traffic-from-active-directory"></a>O [!INCLUDE [Product short](includes/product-short.md)] só aproveita o tráfego de Active Directory?

Além de analisar o tráfego de Active Directory usando a tecnologia de inspeção profunda de pacotes, [!INCLUDE [Product short](includes/product-short.md)] o também coleta eventos relevantes do Windows do controlador de domínio e cria perfis de entidade com base nas informações de Active Directory Domain Services. [!INCLUDE [Product short](includes/product-short.md)] também dá suporte ao recebimento de estatísticas RADIUS de logs de VPN de vários fornecedores (Microsoft, Cisco, F5 e Checkpoint).

### <a name="does-product-short-monitor-only-domain-joined-devices"></a>O [!INCLUDE [Product short](includes/product-short.md)] monitora somente dispositivos ingressados no domínio?

Não. [!INCLUDE [Product short](includes/product-short.md)] monitora todos os dispositivos na rede que executam solicitações de autenticação e autorização em relação a Active Directory, incluindo dispositivos não Windows e móveis.

### <a name="does-product-short-monitor-computer-accounts-as-well-as-user-accounts"></a>O [!INCLUDE [Product short](includes/product-short.md)] monitora contas de computador, bem como contas de usuário?

Sim. Como as contas de computador (bem como outras entidades) podem ser usadas para executar atividades mal-intencionadas, o [!INCLUDE [Product short](includes/product-short.md)] monitora todo o comportamento de contas de computador e todas as outras entidades no ambiente.

### <a name="what-is-the-difference-between-advanced-threat-analytics-ata-and-product-short"></a>Qual é a diferença entre o ATA (Advanced Threat Analytics) e o [!INCLUDE [Product short](includes/product-short.md)] ?

O ATA é uma solução local autônoma com vários componentes, como o ATA Center que requer hardware dedicado local.

[!INCLUDE [Product short](includes/product-short.md)] o é uma solução de segurança baseada em nuvem que aproveita seus sinais do Active Directory (Azure AD) locais. A solução é altamente escalonável e é atualizada frequentemente.

A versão final do ATA está [disponível para o público geral](https://support.microsoft.com/help/4568997/update-3-for-microsoft-advanced-threat-analytics-1-9). O ATA terminará o suporte base em 12 de janeiro de 2021. O suporte estendido continuará até janeiro de 2026. Para obter mais informações, leia [nosso blog](https://techcommunity.microsoft.com/t5/microsoft-security-and/end-of-mainstream-support-for-advanced-threat-analytics-january/ba-p/1539181).

Ao contrário do sensor do ATA, o [!INCLUDE [Product short](includes/product-short.md)] sensor também usa fontes de dados, como a habilitação do ETW (rastreamento de eventos para Windows) [!INCLUDE [Product short](includes/product-short.md)] para fornecer detecções adicionais.

[!INCLUDE [Product short](includes/product-short.md)]as atualizações frequentes do incluem os seguintes recursos e funcionalidades:

- **Suporte para [ambientes de várias florestas](multi-forest.md)** : fornece visibilidade às organizações nas florestas do AD.

- **[Avaliações da Postura de Segurança de Identidade](isp-overview.md)** : identifica configurações incorretas e componentes exploráveis comuns, além de fornecer caminhos de correção para reduzir a superfície de ataque.

- **[Funcionalidades do UEBA](/cloud-app-security/tutorial-ueba)** : insights sobre o risco do usuário individual por meio da pontuação de prioridade de investigação do usuário. A pontuação pode auxiliar a SecOps nas investigações dela e ajudar analistas a entenderem atividades incomuns do usuário e da organização.

- **Integrações nativas**: integra-se com o Microsoft Cloud App Security e o Azure AD Identity Protection para fornecer uma exibição híbrida do que está ocorrendo em ambientes híbridos e locais.

- **Contribui para o Microsoft 365 defender**: contribui com dados de alerta e ameaça para o Microsoft 365 defender. O Microsoft 365 defender aproveita o portfólio de segurança de Microsoft 365 (identidades, pontos de extremidade, dados e aplicativos) para analisar automaticamente os dados de ameaças entre domínios, criando uma imagem completa de cada ataque em um único painel. Com essa amplitude e profundidade de clareza, os defensores podem se concentrar em ameaças críticas e procurar por violações sofisticadas, confiando que a automação avançada do Microsoft 365 defender interrompe os ataques em qualquer lugar da cadeia de Kill e retorna a organização a um estado seguro.

## <a name="licensing-and-privacy"></a>Licenciamento e privacidade

### <a name="where-can-i-get-a-license-for-product-long"></a>Para onde posso obter uma licença [!INCLUDE [Product long](includes/product-long.md)] ?

[!INCLUDE [Product short](includes/product-short.md)] está disponível como parte do Enterprise Mobility + Security 5 Suite (EMS E5) e como uma licença autônoma. Você pode adquirir uma licença diretamente no [Portal do Microsoft 365](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing) ou por meio do CSP (Parceiro de Soluções na Nuvem).

### <a name="does-product-short-need-only-a-single-license-or-does-it-require-a-license-for-every-user-i-want-to-protect"></a>O [!INCLUDE [Product short](includes/product-short.md)] precisa de uma única licença ou requer uma licença para cada usuário que desejo proteger?

Para obter informações sobre [!INCLUDE [Product short](includes/product-short.md)] os requisitos de licenciamento, consulte [ [!INCLUDE [Product short](includes/product-short.md)] diretrizes de licenciamento](/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance/microsoft-365-security-compliance-licensing-guidance#azure-advanced-threat-protection).

### <a name="is-my-data-isolated-from-other-customer-data"></a>Meus dados são isolados de outros dados do cliente?

Sim, seus dados são isolados por meio da autenticação de acesso e da diferenciação lógica com base nos identificadores do cliente. Cada cliente pode acessar somente dados coletados de sua própria organização e dados genéricos fornecidos pela Microsoft.

### <a name="do-i-have-the-flexibility-to-select-where-to-store-my-data"></a>É tenho flexibilidade para selecionar onde armazenar meus dados?

Não. Quando sua [!INCLUDE [Product short](includes/product-short.md)] instância é criada, ela é armazenada automaticamente no país Data Center mais próximo da localização geográfica do seu locatário do AAD. [!INCLUDE [Product short](includes/product-short.md)] os dados não podem ser movidos depois que sua [!INCLUDE [Product short](includes/product-short.md)] instância é criada para um Data Center diferente.

### <a name="how-does-microsoft-prevent-malicious-insider-activities-and-abuse-of-high-privilege-roles"></a>Como a Microsoft impede atividades internas mal-intencionadas e abuso de funções de alto privilégio?

Os administradores e desenvolvedores da Microsoft, por design, recebem privilégios suficientes para realizar as tarefas atribuídas a eles para operar e desenvolver o serviço. A Microsoft implanta combinações de controles preventivos, investigativos e reativos, incluindo os seguintes mecanismos para ajudar a proteger contra atividades administrativas e/ou de desenvolvedor não autorizadas:

- Controle de acesso total a dados confidenciais
- Combinações de controles que melhoram muito a detecção independente de atividades mal-intencionadas
- Vários níveis de monitoramento, registro em log e relatórios

Além disso, a Microsoft realiza verificações de histórico de determinados funcionários de operações e limita o acesso a aplicativos, sistemas e infraestrutura de rede proporcionalmente ao nível da verificação de histórico. A equipe de operações segue um processo formal quando precisa acessar a conta de um cliente ou informações relacionadas ao desempenho de suas tarefas.

## <a name="deployment"></a>Implantação

### <a name="how-many-product-short-sensors-do-i-need"></a>De quantos [!INCLUDE [Product short](includes/product-short.md)] sensores eu preciso?

Cada controlador de domínio no ambiente deve ser coberto por um sensor [!INCLUDE [Product short](includes/product-short.md)] ou sensor autônomo. Para obter mais informações, consulte [ [!INCLUDE [Product short](includes/product-short.md)] dimensionamento de sensor](capacity-planning.md#sizing).

### <a name="does-product-short-work-with-encrypted-traffic"></a>[!INCLUDE [Product short](includes/product-short.md)]Funciona com tráfego criptografado?

Os protocolos de rede com tráfego criptografado (por exemplo, AtSvc e WMI) não são descriptografados, mas são analisados pelos sensores.

### <a name="does-product-short-work-with-kerberos-armoring"></a>[!INCLUDE [Product short](includes/product-short.md)]Funciona com a proteção Kerberos?

A habilitação da proteção Kerberos, também conhecida como FAST (encapsulamento seguro de autenticação flexível), é suportada pelo [!INCLUDE [Product short](includes/product-short.md)] , com a exceção de passar a detecção de hash, que não funciona com a proteção Kerberos.

### <a name="how-do-i-monitor-a-virtual-domain-controller-using-product-short"></a>Como fazer monitorar um controlador de domínio virtual usando [!INCLUDE [Product short](includes/product-short.md)] ?

A maioria dos controladores de domínio virtuais pode ser coberta pelo [!INCLUDE [Product short](includes/product-short.md)] sensor, para determinar se o [!INCLUDE [Product short](includes/product-short.md)] sensor é apropriado para seu ambiente, consulte [ [!INCLUDE [Product short](includes/product-short.md)] planejamento de capacidade](capacity-planning.md).

Se um controlador de domínio virtual não puder ser coberto pelo [!INCLUDE [Product short](includes/product-short.md)] sensor, você poderá ter um sensor autônomo virtual ou físico, [!INCLUDE [Product short](includes/product-short.md)] conforme descrito em [Configurar o espelhamento de porta](configure-port-mirroring.md).  
A maneira mais fácil é ter um [!INCLUDE [Product short](includes/product-short.md)] sensor autônomo virtual em cada host onde existe um controlador de domínio virtual.  
Se os controladores de domínio virtuais se movimentarem entre os hosts, será necessário executar uma destas etapas:

- Quando o controlador de domínio virtual é movido para outro host, pré-configurar o [!INCLUDE [Product short](includes/product-short.md)] sensor autônomo nesse host para receber o tráfego do controlador de domínio virtual recentemente movido.
- Certifique-se de associar o [!INCLUDE [Product short](includes/product-short.md)] sensor autônomo virtual ao controlador de domínio virtual para que, se ele for movido, o [!INCLUDE [Product short](includes/product-short.md)] sensor autônomo se mova com ele.
- Há alguns comutadores virtuais que podem enviar o tráfego entre os hosts.

### <a name="how-do-i-configure-the-product-short-sensors-to-communicate-with-product-short-cloud-service-when-i-have-a-proxy"></a>Como fazer configurar os [!INCLUDE [Product short](includes/product-short.md)] sensores para se comunicar com o [!INCLUDE [Product short](includes/product-short.md)] serviço de nuvem quando eu tiver um proxy?

Para seus controladores de domínio se comunicarem com o serviço de nuvem, você deve abrir: *. atp.azure.com porta 443 em seu firewall/proxy. Para obter instruções sobre como fazer isso, consulte [configurar seu proxy ou firewall para habilitar a comunicação com [!INCLUDE [Product short](includes/product-short.md)] sensores](configure-proxy.md).

### <a name="can-product-short-monitored-domain-controllers-be-virtualized-on-your-iaas-solution"></a>[!INCLUDE [Product short](includes/product-short.md)]Os controladores de domínio monitorados podem ser virtualizados em sua solução IaaS?

Sim, você pode usar o [!INCLUDE [Product short](includes/product-short.md)] sensor para monitorar controladores de domínio que estão em qualquer solução de IaaS.

### <a name="can-product-short-support-multi-domain-and-multi-forest"></a>Pode [!INCLUDE [Product short](includes/product-short.md)] dar suporte a vários domínios e várias florestas?

[!INCLUDE [Product short](includes/product-short.md)] dá suporte a ambientes de vários domínios e a várias florestas. Confira mais informações e requisitos de confiança em [Suporte a várias florestas](multi-forest.md).

### <a name="can-you-see-the-overall-health-of-the-deployment"></a>Você pode ver a integridade geral da implantação?

Sim, você pode exibir a integridade geral da implantação, bem como problemas específicos relacionados à configuração, conectividade, etc., e você é alertado conforme eles ocorrem com [!INCLUDE [Product short](includes/product-short.md)] alertas de integridade.

## <a name="operation"></a>Operação

### <a name="what-kind-of-integration-does-product-short-have-with-siems"></a>Que tipo de integração [!INCLUDE [Product short](includes/product-short.md)] tem com Siems?

[!INCLUDE [Product short](includes/product-short.md)] pode ser configurado para enviar um alerta de syslog para qualquer servidor SIEM usando o formato CEF, para alertas de integridade e quando um alerta de segurança é detectado. Consulte a [referência de log do SIEM](cef-format-sa.md) para obter mais informações.

### <a name="why-are-certain-accounts-considered-sensitive"></a>Por que certas contas são consideradas confidenciais?

Isso ocorre quando uma conta é membro de grupos designados como confidenciais (por exemplo: "Administradores do Domínio").

Para entender por que uma conta é confidencial, você pode examinar sua associação de grupo para entender a quais grupos confidenciais ela pertence (o grupo ao qual ela pertence também pode ser confidencial devido a outro grupo, portanto, o mesmo processo deve ser executado até que você localize o grupo confidencial de nível mais alto). Você também pode [marcar contas como confidenciais](sensitive-accounts.md) manualmente.

### <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>Você precisa escrever suas próprias regras e criar um limite/linha de base?

Com o [!INCLUDE [Product short](includes/product-short.md)] , não é necessário criar regras, limites ou linhas de base e, em seguida, ajustar. [!INCLUDE [Product short](includes/product-short.md)] analisa os comportamentos entre usuários, dispositivos e recursos, bem como sua relação entre si, e pode detectar atividades suspeitas e ataques conhecidos rapidamente. Três semanas após a implantação, [!INCLUDE [Product short](includes/product-short.md)] começa a detectar atividades suspeitas comportamentais. Por outro lado, o [!INCLUDE [Product short](includes/product-short.md)] começará a detectar ataques mal-intencionados conhecidos e problemas de segurança imediatamente após a implantação.

### <a name="which-traffic-does-product-short-generate-in-the-network-from-domain-controllers-and-why"></a>Qual tráfego [!INCLUDE [Product short](includes/product-short.md)] gera na rede de controladores de domínio e por quê?

[!INCLUDE [Product short](includes/product-short.md)] gera o tráfego de controladores de domínio para computadores na organização em um dos três cenários:

1. **Resolução de Nomes de Rede**  
[!INCLUDE [Product short](includes/product-short.md)] captura tráfego e eventos, aprendizado e criação de perfil de usuários e atividades de computador na rede. Para aprender e criar o perfil de atividades de acordo com os computadores da organização, o [!INCLUDE [Product short](includes/product-short.md)] precisa resolver IPS para contas de computador. Para resolver os IPs para os sensores de nomes de computador, [!INCLUDE [Product short](includes/product-short.md)] solicite o endereço IP para o nome do computador *por trás* do endereço IP.

    As solicitações são feitas com um dos quatro métodos a seguir:
    - NTLM sobre RPC (porta TCP 135)
    - NetBIOS (porta UDP 137)
    - RDP (TCP porta 3389)
    - Consulta ao servidor DNS usando a pesquisa de DNS reverso do endereço IP (UDP 53)

    Depois de obter o nome do computador,  [!INCLUDE [Product short](includes/product-short.md)] os sensores passam a verificar os detalhes em Active Directory para ver se há um objeto de computador correlacionado com o mesmo nome de computador. Se encontrarem a correspondência, é feita uma associação entre o endereço IP e o objeto do computador correspondido.
2. **LMP (caminho de movimento lateral)**  
Para criar possíveis LMPs para usuários confidenciais, [!INCLUDE [Product short](includes/product-short.md)] o requer informações sobre os administradores locais em computadores. Nesse cenário, o [!INCLUDE [Product short](includes/product-short.md)] sensor usa Sam-R (TCP 445) para consultar o endereço IP identificado no tráfego de rede, a fim de determinar os administradores locais do computador. Para saber mais sobre o [!INCLUDE [Product short](includes/product-short.md)] e o Sam-r, confira [configurar permissões necessárias do Sam-r](install-step8-samr.md).

3. **Consulta ao Active Directory usando o LDAP** sobre dados de entidades  
[!INCLUDE [Product short](includes/product-short.md)] os sensores consultam o controlador de domínio do domínio ao qual a entidade pertence. Pode ser no mesmo sensor ou em outro controlador de domínio daquele domínio.

|Protocolo|Serviço|Porta|Origem| Direção|
|---------|---------|---------|---------|--------|
|LDAP|TCP e UDP|389|Controladores de domínio|Saída|
|LDAP seguro (LDAPS)|TCP|636|Controladores de domínio|Saída|
|LDAP para o Catálogo Global|TCP|3268|Controladores de domínio|Saída|
|LDAPS para o Catálogo Global|TCP|3269|Controladores de domínio|Saída|

### <a name="why-dont-activities-always-show-both-the-source-user-and-computer"></a>Por que as atividades sempre mostram o computador e o usuário da origem?

[!INCLUDE [Product short](includes/product-short.md)] captura atividades em vários protocolos diferentes. Em alguns casos, [!INCLUDE [Product short](includes/product-short.md)] o não recebe os dados do usuário de origem no tráfego. [!INCLUDE [Product short](includes/product-short.md)] Tenta correlacionar a sessão do usuário à atividade e, quando a tentativa é bem-sucedida, o usuário de origem da atividade é exibido. Caso as tentativas de correlação do usuário falhem, apenas o computador de origem será exibido.

## <a name="troubleshooting"></a>Solução de problemas

### <a name="what-should-i-do-if-the-product-short-sensor-or-standalone-sensor-doesnt-start"></a>O que devo fazer se o [!INCLUDE [Product short](includes/product-short.md)] sensor ou sensor autônomo não for iniciado?

Examine o erro mais recente no [log](troubleshooting-using-logs.md) de erros atual (onde [!INCLUDE [Product short](includes/product-short.md)] é instalado na pasta "logs").

## <a name="see-also"></a>Consulte Também

- [Pré-requisitos do [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Planejamento de capacidade do [!INCLUDE [Product short](includes/product-short.md)]](capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md)
- [Solução de problemas](troubleshooting-known-issues.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
