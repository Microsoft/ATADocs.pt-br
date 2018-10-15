---
title: Perguntas frequentes sobre a Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Fornece uma lista de perguntas frequentes sobre o Azure ATP e as respostas associadas
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/4/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 6a9b5273-eb26-414e-9cdd-f64406e24ed8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 07c5d67804eb4c74df678e8752a2516af5c52cc7
ms.sourcegitcommit: bbbe808c08ce703a314c82b46aedaae79ab256a3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2018
ms.locfileid: "48848500"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*

# <a name="azure-atp-frequently-asked-questions"></a>Perguntas frequentes sobre o Azure ATP
Este artigo fornece uma lista de perguntas frequentes sobre o Azure ATP e dividido nas seguintes categorias: 
- [O que é o Azure ATP](#What-is-Azure-ATP)
- [Licenciamento e privacidade](#Licensing-and-privacy)
- [Implantação](#Deployment)
- [Operações](#Operations)
- [Solução de problemas](#Troubleshooting)

## <a name="what-is-azure-atp"></a>O que é o Azure ATP?

### <a name="what-can-azure-atp-detect"></a>O que pode o Azure ATP pode detectar?

O Azure ATP detecta técnicas e ataques mal-intencionados e conhecidos, problemas de segurança e riscos.
Para obter a lista completa das detecções do Azure ATP, consulte [Quais detecções são realizadas pelo Azure ATP?](suspicious-activity-guide.md).

### <a name="what-data-does-azure-atp-collect"></a>Quais dados o Azure ATP coleta? 
O Azure ATP coleta e armazena informações de seus servidores configurados (controladores de domínio, servidores membro etc.) em um banco de dados específico para o serviço para fins de administração, rastreamento e relatório. As informações coletadas incluem o tráfego de rede dos controladores de domínio (como autenticação Kerberos, autenticação NTLM, consultas DNS), logs de segurança (como eventos de segurança do Windows), informações do Active Directory (estrutura, sub-redes, sites) e informações de entidade (como nomes, endereços de email e números de telefone). 

A Microsoft usa esses dados para: 

-   Identificar proativamente IOAs (indicadores de ataque) em sua organização 
-   Gerar alertas se um possível ataque for detectado 
-   Forneça a suas operações de segurança uma visão das entidades relacionadas aos sinais de ameaça de sua rede, permitindo que você investigue e explore a presença de ameaças à segurança na rede. 

A Microsoft não explora seus dados para fornecer anúncios ou para qualquer outra finalidade que não seja fornecer o serviço. 

### <a name="does-azure-atp-only-leverage-traffic-from-active-directory"></a>O Azure ATP aproveita apenas tráfego do Active Directory?
Além de analisar o tráfego do Active Directory usando a tecnologia de inspeção profunda de pacotes, o Azure ATP também coleta eventos do Windows relevantes do controlador de domínio e cria perfis de entidade com base nas informações do Active Directory Domain Services. O Azure ATP também dá suporte ao recebimento contabilidade RADIUS de logs VPN de vários fornecedores (Microsoft, Cisco, F5 e Checkpoint).

### <a name="does-azure-atp-monitor-only-domain-joined-devices"></a>O Azure ATP monitora somente dispositivos ingressados em domínio?
Não. O Azure ATP monitora todos os dispositivos na rede que executam solicitações de autenticação e autorização no Active Directory, incluindo dispositivos móveis e que não são do Windows.

### <a name="does-azure-atp-monitor-computer-accounts-as-well-as-user-accounts"></a>O Azure ATP monitora as contas de computador, bem como as contas de usuário?
Sim. Como as contas computador (bem como quaisquer outras entidades) podem ser usadas para executar atividades mal-intencionadas, o Azure ATP monitora todo o comportamento das contas de computador e todas as outras entidades no ambiente.

## <a name="licensing-and-privacy"></a>Licenciamento e privacidade 
### <a name="where-can-i-get-a-license-for-azure-advanced-threat-protection-atp"></a>Onde posso obter uma licença do Azure ATP (Proteção Avançada contra Ameaças)?

Você pode adquirir uma licença do Enterprise Mobility + Security 5 (EMS E5) diretamente por meio do [Portal do Office 365](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing) ou do modelo de licenciamento do Parceiro de Soluções na Nuvem (CSP).  

### <a name="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory"></a>Isto fará parte do Azure Active Directory ou do Active Directory local?
Atualmente, esta solução é uma oferta autônoma. Ela não faz parte do Azure Active Directory ou do Active Directory local.

### <a name="is-my-data-isolated-from-other-customer-data"></a>Meus dados são isolados de outros dados do cliente? 

Sim, seus dados são isolados por meio da autenticação de acesso e da lógica de diferenciação com base no identificador do cliente. Cada cliente pode acessar somente dados coletados de sua própria organização e dados genéricos fornecidos pela Microsoft.

### <a name="do-i-have-the-flexibility-to-select-where-to-store-my-data"></a>É tenho flexibilidade para selecionar onde armazenar meus dados? 

Ao criar o espaço de trabalho do Azure ATP, você pode optar por armazenar seus dados em data centers do Microsoft Azure nos Estados Unidos ou na Europa. Após configurar, você não pode alterar o local onde os dados são armazenados. A Microsoft não transfere os dados do local especificado.                

### <a name="how-does-microsoft-prevent-malicious-insider-activities-and-abuse-of-high-privilege-roles"></a>Como a Microsoft impede atividades internas mal-intencionadas e abuso de funções de alto privilégio? 

Os administradores e desenvolvedores da Microsoft, por design, recebem privilégios suficientes para realizar as tarefas atribuídas a eles para operar e desenvolver o serviço. A Microsoft implanta combinações de controles preventivos, investigativos e reativos, incluindo os seguintes mecanismos para ajudar a proteger contra atividades administrativas e/ou de desenvolvedor não autorizadas: 

-   Controle de acesso total a dados confidenciais 
-   Combinações de controles que melhoram muito a detecção independente de atividades mal-intencionadas 
-   Vários níveis de monitoramento, registro em log e relatórios 

Além disso, a Microsoft realiza verificações de histórico de determinados funcionários de operações e limita o acesso a aplicativos, sistemas e infraestrutura de rede proporcionalmente ao nível da verificação de histórico. A equipe de operações segue um processo formal quando precisa acessar a conta de um cliente ou informações relacionadas ao desempenho de suas tarefas. 

## <a name="deployment"></a>Implantação
### <a name="how-many-azure-atp-sensors-do-i-need"></a>De quantos sensores do Azure ATP eu preciso?

Cada controlador de domínio no ambiente deve ser coberto por um sensor ou sensor autônomo do ATP. Para obter mais informações, confira [Azure ATP sensor sizing](atp-capacity-planning.md#sizing) (Dimensionamento do sensor do Azure ATP). 

### <a name="does-azure-atp-work-with-encrypted-traffic"></a>O Azure ATP funciona com tráfego criptografado?
Os protocolos de rede com tráfego criptografado (por exemplo, LDAPS e IPSEC) não são descriptografados, mas são analisados pelos sensores.

### <a name="does-azure-atp-work-with-kerberos-armoring"></a>O Azure ATP funciona com Kerberos Armoring?
Há suporte para a habilitação do Kerberos Armoring, também conhecido como FAST (Flexible Authentication Secure Tunneling), pelo Azure ATP, com exceção da detecção de passagem pelo hash, que não funciona com o Kerberos Armoring.

### <a name="how-do-i-monitor-a-virtual-domain-controller-using-azure-atp"></a>Como monitorar um controlador de domínio virtual usando o Azure ATP?
A maioria dos controladores de domínio virtuais pode ser coberta pelo sensor do Azure ATP. Para determinar se o sensor do Azure ATP é apropriado para seu ambiente, consulte [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md).

Se um controlador de domínio virtual não puder ser coberto pelo sensor do Azure ATP, você pode ter um sensor autônomo do Azure ATP físico ou virtual, conforme descrito em [Configurar o espelhamento de porta](configure-port-mirroring.md).  <br />A maneira mais fácil é ter um sensor autônomo do Azure ATP virtual em cada host no qual o controlador de domínio virtual existe.<br />Se os controladores de domínio virtuais se movimentarem entre os hosts, será necessário executar uma destas etapas:

-   Quando o controlador de domínio virtual for movido para outro host, pré-configure o sensor autônomo do Azure ATP nesse host para receber o tráfego do controlador de domínio virtual movimentado recentemente.
-   Não deixe de afiliar o sensor autônomo do Azure ATP virtual ao controlador de domínio virtual, de modo que se ele for movido, o sensor autônomo do Azure ATP será movido com ele.
-   Há alguns comutadores virtuais que podem enviar o tráfego entre os hosts.

### <a name="how-do-i-configure-the-azure-atp-sensors-to-communicate-with-azure-atp-cloud-service-when-i-have-a-proxy"></a>Como posso configurar os sensores do Azure ATP para se comunicar com o serviço de nuvem do Azure ATP quando tiver um proxy?

Para seus controladores de domínio se comunicarem com o serviço de nuvem, você deve abrir: *. atp.azure.com porta 443 em seu firewall/proxy. Para obter instruções de como fazer isso, consulte [Configurar seu proxy ou firewall para habilitar a comunicação com sensores do Azure ATP](configure-proxy.md).

### <a name="can-azure-atp-monitor-domain-controllers-be-virtualized-on-your-iaas-solution"></a>Os controlador de domínio de monitor do Azure ATP podem ser virtualizados em sua solução IaaS?
Sim, você pode usar o sensor do Azure ATP para monitorar controladores de domínio em qualquer solução IaaS.

### <a name="can-azure-atp-support-multi-domain-and-multi-forest"></a>O Azure ATP pode dar suporte a vários domínios e várias florestas?
A Proteção Avançada contra Ameaças do Azure dá suporte a ambientes com vários domínios e com várias florestas. Este recurso está em visualização pública no momento. Confira mais informações e limitações conhecidas em [Suporte a várias florestas](atp-multi-forest.md).

### <a name="can-you-see-the-overall-health-of-the-deployment"></a>Você pode ver a integridade geral da implantação?
Sim, é possível exibir a integridade geral da implantação, bem como os problemas específicos relacionados à configuração, conectividade, etc., e você recebe um alerta quando ocorrerem.

## <a name="operation"></a>Operação

### <a name="what-kind-of-integration-does-azure-atp-have-with-siems"></a>Que tipo de integração o Azure ATP tem com SIEMs?
O Azure ATP pode ser configurado para enviar um alerta de Syslog para qualquer servidor SIEM usando o formato CEF para alertas de integridade e caso uma atividade suspeita seja detectada. Consulte a [referência de log do SIEM](cef-format-sa.md) para obter mais informações.

### <a name="why-are-certain-accounts-considered-sensitive"></a>Por que certas contas são consideradas confidenciais?
Isso ocorre quando uma conta é membro de grupos designados como confidenciais (por exemplo: "Administradores do Domínio").

Para entender por que uma conta é confidencial, você pode examinar sua associação de grupo para entender a quais grupos confidenciais ela pertence (o grupo ao qual ela pertence também pode ser confidencial devido a outro grupo, portanto, o mesmo processo deve ser executado até que você localize o grupo confidencial de nível mais alto). Você também pode [marcar contas como confidenciais manualmente](sensitive-accounts.md).

### <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>Você precisa escrever suas próprias regras e criar um limite/linha de base?
Com a Proteção Avançada contra Ameaças do Azure, não é necessário criar regras, limites ou linhas de base e, em seguida, ajustar. O Azure ATP analisa os comportamentos entre os usuários, dispositivos e recursos — bem como sua relação um com o outro — e pode detectar atividades suspeitas e ataques conhecidos rapidamente. Três semanas após a implantação, o Azure ATP começa a detectar as atividades suspeitas do comportamento. Por outro lado, o Azure ATP começará a detectar os ataques mal-intencionados conhecidos e os problemas de segurança imediatamente após a implantação.

## <a name="troubleshooting"></a>Solução de problemas
### <a name="what-should-i-do-if-the-azure-atp-sensor-or-standalone-sensor-doesnt-start"></a>O que devo fazer se o sensor ou o sensor autônomo do Azure ATP não for iniciado?
Procure o erro mais recente no [log](troubleshooting-atp-using-logs.md) de erros atual (onde o Azure ATP está instalado, na pasta "Logs").

### <a name="how-can-i-test-azure-atp"></a>Como posso testar o Azure ATP?
Você pode simular atividades suspeitas como um teste de ponta a ponta. No cenário a seguir, o reconhecimento DNS é simulado:

1.  Verifique se os sensores do Azure ATP estão instalados e configurados nos controladores de domínio (ou se os sensores autônomos e o espelhamento de porta relacionado estão instalados e configurados)
2.  Abra o CMD
3.  Execute o seguinte comando: nslookup -<DC iP address>
    -   Pressione Enter
    -   Digite: Is -d <FQDN>
    -   Dependendo da configuração do ambiente, as respostas irão variar de "Consulta recusada" para uma lista dos registros DNS. 
4. Exiba o alerta relacionado ao reconhecimento de DNS simulado no portal do Azure ATP. 

## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Solução de problemas](troubleshooting-atp-known-issues.md)
- [Confira o fórum do Azure ATP!](https://aka.ms/azureatpcommunity)
