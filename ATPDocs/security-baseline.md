---
title: Linha de base de segurança do Azure para Microsoft defender para identidade
description: A linha de base do Microsoft defender for Identity Security fornece diretrizes de procedimento e recursos para implementar as recomendações de segurança especificadas no benchmark de segurança do Azure.
author: msmbaldwin
ms.service: microsoft-defender-for-identity
ms.topic: conceptual
ms.date: 12/03/2020
ms.author: mbaldwin
ms.custom: subject-security-benchmark
ms.openlocfilehash: 37d46cd2a7810193990cc3143e69c9ea83c6afe2
ms.sourcegitcommit: 69339ed7712657427ee40af8cc3ac41e11ed2dd2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2020
ms.locfileid: "96597943"
---
# <a name="azure-security-baseline-for-microsoft-defender-for-identity"></a>Linha de base de segurança do Azure para Microsoft defender para identidade

Essa linha de base de segurança aplica diretrizes do [benchmark de segurança do Azure versão 2,0](https://docs.microsoft.com/azure/security/benchmarks/overview) para o Microsoft defender para identidade. O Azure Security Benchmark fornece recomendações sobre como você pode proteger suas soluções de nuvem no Azure. O conteúdo é agrupado pelos **controles de segurança** definidos pelo benchmark de segurança do Azure e pelas diretrizes relacionadas aplicáveis ao Microsoft defender for Identity. Os **controles** não aplicáveis ao Microsoft defender para identidade foram excluídos.

Para ver como o Microsoft defender for Identity é completamente mapeado para o benchmark de segurança do Azure, consulte o [arquivo completo de mapeamento de linha de base do Microsoft defender for Identity Security](https://github.com/MicrosoftDocs/SecurityBenchmarks/tree/master/Azure%20Offer%20Security%20Baselines).

## <a name="network-security"></a>Segurança de rede

*Para obter mais informações, confira o [Azure Security Benchmark: Segurança de Rede](/azure/security/benchmarks/security-controls-v2-network-security).*

### <a name="ns-6-simplify-network-security-rules"></a>NS-6: simplificar as regras de segurança de rede

**Diretrizes**: Use as marcas de serviço de rede virtual do Azure para definir os controles de acesso à rede nos grupos de segurança de rede ou no firewall do Azure configurados para seus recursos de identidade. Você pode usar marcas de serviço em vez de endereços IP específicos ao criar regras de segurança. Ao especificar o nome da marca de serviço (por exemplo: "AzureAdvancedThreatProtection") no campo de origem ou destino apropriado de uma regra, você pode permitir ou negar o tráfego para o serviço correspondente. A Microsoft gerencia os prefixos de endereço englobados pela marca de serviço e atualiza automaticamente a marca de serviço em caso de alteração de endereços.

- [Habilitar o acesso ao defender para URLs de serviço de identidade no servidor proxy](https://docs.microsoft.com/defender-for-identity/configure-proxy#enable-access-to--service-urls-in-the-proxy-server)

- [Entender e usar marcas de serviço](https://docs.microsoft.com/azure/virtual-network/service-tags-overview)

**Monitoramento da Central de Segurança do Azure**: Não aplicável

**Responsabilidade**: Cliente

## <a name="identity-management"></a>Gerenciamento de Identidades

*Para obter mais informações, confira o [Azure Security Benchmark: gerenciamento de identidades](/azure/security/benchmarks/security-controls-v2-identity-management).*

### <a name="im-1-standardize-azure-active-directory-as-the-central-identity-and-authentication-system"></a>IM-1: padronizar o Azure Active Directory como o sistema central de identidade e autenticação

**Diretrizes**: o defender for Identity usa Azure Active Directory (Azure AD) como o serviço de gerenciamento de identidade e acesso padrão. Você deve padronizar o Azure AD para controlar a identidade e o gerenciamento de acesso de sua organização no:

- Microsoft Cloud recursos, como o portal do Azure, o armazenamento do Azure, a máquina virtual do Azure (Linux e Windows), Azure Key Vault, PaaS e aplicativos SaaS.
- Os recursos da sua organização, como os aplicativos no Azure ou os recursos de rede corporativa.

A proteção do Azure AD deve ser uma prioridade alta na prática de segurança de nuvem da sua organização. O Azure AD fornece uma classificação de segurança de identidade para ajudar você a avaliar a postura de segurança de identidade em relação às recomendações de melhores práticas da Microsoft. Use a classificação para medir o alinhamento da sua configuração com as recomendações de melhores práticas e fazer aprimoramentos na sua postura de segurança.

Observação: o Azure AD dá suporte à identidade externa que permite aos usuários sem um conta Microsoft entrar em seus aplicativos e recursos com sua identidade externa.

- [Locatários no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/single-and-multi-tenant-apps) 

- [Como criar e configurar uma instância do Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-access-create-new-tenant) 

- [Usar provedores de identidade externos para o aplicativo](https://docs.microsoft.com/azure/active-directory/b2b/identity-providers) 

- [O que é a classificação de segurança de identidade no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/identity-secure-score)

**Monitoramento da Central de Segurança do Azure**: Não aplicável

**Responsabilidade**: Cliente

### <a name="im-4-use-strong-authentication-controls-for-all-azure-active-directory-based-access"></a>IM-4: usar controles de autenticação forte para todo o acesso baseado no Azure Active Directory

**Diretrizes**: o defender for Identity usa Azure Active Directory que dá suporte a controles de autenticação fortes por meio da autenticação multifator e métodos fortes de senha.

- Autenticação multifator – habilite a autenticação multifator do Azure AD e siga as recomendações de gerenciamento de acesso e identidade da central de segurança do Azure para obter algumas práticas recomendadas na configuração de autenticação multifator. A autenticação multifator pode ser imposta em todos, Selecionar usuários ou no nível por usuário com base nas condições de entrada e nos fatores de risco.
- Autenticação com senha-três opções de autenticação com senha estão disponíveis: Windows Hello para empresas, Microsoft Authenticator aplicativo e métodos de autenticação locais, como cartões inteligentes.

Para administradores e usuários privilegiados, verifique se o nível mais alto do método de autenticação forte é usado, seguido da distribuição da política de autenticação forte apropriada para outros usuários.

- [Como habilitar a autenticação multifator no Azure](https://docs.microsoft.com/azure/active-directory/authentication/howto-mfa-getstarted) 

- [Introdução às opções de autenticação sem senha do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/authentication/concept-authentication-passwordless) 

- [Política de senha padrão do Azure AD](https://docs.microsoft.com/azure/active-directory/authentication/concept-sspr-policy#password-policies-that-only-apply-to-cloud-user-accounts) 

- [Eliminar senhas inadequadas usando a proteção de senha do Azure AD](https://docs.microsoft.com/azure/active-directory/authentication/concept-password-ban-bad)

**Monitoramento da Central de Segurança do Azure**: Sim

**Responsabilidade**: Cliente

## <a name="privileged-access"></a>Acesso privilegiado

*Para obter mais informações, confira o [Azure Security Benchmark: acesso privilegiado](/azure/security/benchmarks/security-controls-v2-privileged-access).*

### <a name="pa-1-protect-and-limit-highly-privileged-users"></a>PA-1: proteger e limitar os usuários altamente privilegiados

**Diretrizes**: o defender for Identity tem as seguintes contas altamente privilegiadas: administrador global

Administrador de segurança

Limite o número de contas ou funções altamente privilegiadas e proteja essas contas em um nível elevado, pois os usuários com esse privilégio podem ler e modificar de forma direta ou indireta todos os recursos em seu ambiente do Azure.

Você pode habilitar o acesso privilegiado JIT (just-in-time) aos recursos do Azure e Azure Active Directory (Azure AD) usando Azure AD Privileged Identity Management (PIM). O JIT concede permissões temporárias para executar tarefas privilegiadas somente quando os usuários precisam dela. O PIM também pode gerar alertas de segurança quando há atividades suspeitas ou não seguras na sua organização do Azure AD.
- [Microsoft defender para grupos de funções de identidade](https://docs.microsoft.com/defender-for-identity/role-groups)

- [Permissões da função Administrador no Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) 

- [Usar os alertas de segurança do Azure Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-how-to-configure-security-alerts) 

- [Protegendo o acesso privilegiado para implantações de nuvem e híbridos no Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-admin-roles-secure)

**Monitoramento da Central de Segurança do Azure**: Sim

**Responsabilidade**: Cliente

### <a name="pa-2-restrict-administrative-access-to-business-critical-systems"></a>PA-2: restringir o acesso administrativo a sistemas críticos para os negócios

**Diretrizes**: o defender for Identity usa o Azure RBAC (controle de acesso baseado em função) para isolar o acesso a sistemas críticos de negócios, restringindo quais contas recebem acesso privilegiado às assinaturas e aos grupos de gerenciamento em que eles estão.

Certifique-se de também restringir o acesso aos sistemas de gerenciamento, identidade e segurança que têm acesso administrativo ao seu acesso crítico aos negócios, como controladores de Domínio do Active Directory (DCs), ferramentas de segurança e ferramentas de gerenciamento do sistema com agentes instalados em sistemas críticos para os negócios. Os invasores que comprometem esses sistemas de gerenciamento e segurança podem fazê-los imediatamente para comprometerem ativos críticos para os negócios.

Todos os tipos de controles de acesso devem ser alinhados à sua estratégia de segmentação corporativa para garantir o controle de acesso consistente.

- [Microsoft defender para grupos de funções de identidade](https://docs.microsoft.com/defender-for-identity/role-groups)

- [Componentes do Azure e modelo de referência](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#azure-components-and-reference-model-2151) 

- [Acesso ao grupo de gerenciamento](https://docs.microsoft.com/azure/governance/management-groups/overview#management-group-access) 

- [Administradores de assinatura do Azure](https://docs.microsoft.com/azure/cost-management-billing/manage/add-change-subscription-administrator)

**Monitoramento da Central de Segurança do Azure**: Sim

**Responsabilidade**: Cliente

### <a name="pa-3-review-and-reconcile-user-access-regularly"></a>PA-3: examinar e reconciliar regularmente o acesso do usuário

**Diretrizes**: o defender for Identity usa contas de Azure Active Directory para gerenciar seus recursos, examinar contas de usuário e acessar a atribuição regularmente para garantir que as contas e seus acessos sejam válidos. Você pode usar as revisões de acesso do Azure AD para revisar as associações de grupo, o acesso aos aplicativos empresariais e as atribuições de função. Os relatórios do AD do Azure podem fornecer logs para ajudar a descobrir contas obsoletas. Você também pode usar Azure AD Privileged Identity Management para criar um fluxo de trabalho de relatório de revisão de acesso para facilitar o processo de revisão.

Além disso, o Azure Privileged Identity Management também pode ser configurado para alertar quando um número excessivo de contas de administrador for criado e para identificar as contas de administrador que estão obsoletas ou configuradas incorretamente.

Observação: alguns serviços do Azure dão suporte a usuários e funções locais que não são gerenciados por meio do Azure AD. Você precisará gerenciar esses usuários separadamente.

- [Criar uma revisão de acesso das funções de recurso do Azure no Privileged Identity Management (PIM)](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-resource-roles-start-access-review) 

- [Como usar as revisões de identidade e acesso do Azure AD](https://docs.microsoft.com/azure/active-directory/governance/access-reviews-overvie)

**Monitoramento da Central de Segurança do Azure**: Sim

**Responsabilidade**: Cliente

### <a name="pa-6-use-privileged-access-workstations"></a>PA-6: usar estações de trabalho com acesso privilegiado

**Diretrizes**: estações de trabalho seguras e isoladas são extremamente importantes para a segurança de funções confidenciais, como administradores, desenvolvedores e operadores de serviços críticos. Use estações de trabalho de usuário altamente protegidas e/ou bastiões do Azure para tarefas administrativas. Use Azure Active Directory, Microsoft defender for Endpoint e/ou Microsoft Intune para implantar uma estação de trabalho de usuário segura e gerenciada para tarefas administrativas. As estações de trabalho protegidas podem ser gerenciadas de modo central para impor a configuração protegida, incluindo autenticação forte, linhas de base de software e hardware, acesso lógico restrito e de rede.

- [Entender as estações de trabalho com acesso privilegiado](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-managed-workstation) 
- [Implantar uma estação de trabalho com acesso privilegiado](https://docs.microsoft.com/azure/active-directory/devices/howto-azure-managed-workstation)

**Monitoramento da Central de Segurança do Azure**: Não aplicável

**Responsabilidade**: Cliente

## <a name="data-protection"></a>Proteção de dados

*Para obter mais informações, confira o [Azure Security Benchmark: proteção de dados](/azure/security/benchmarks/security-controls-v2-data-protection).*

### <a name="dp-2-protect-sensitive-data"></a>DP-2: proteger dados confidenciais

**Orientação**: o defender for Identity protege dados confidenciais restringindo o acesso usando funções do Azure Active Directory (Azure AD).

Para garantir um controle de acesso consistente, todos os tipos de controle de acesso devem ser alinhados à sua estratégia de segmentação corporativa. A estratégia de segmentação corporativa também deve ser informada pelo local de sistemas e dados confidenciais ou críticos para os negócios.

Quanto à plataforma subjacente, que é gerenciada pela Microsoft, a Microsoft trata todo o conteúdo do cliente como confidencial e fornece proteção contra a perda e a exposição de dados do cliente. Para garantir que os dados do cliente no Azure permaneçam seguros, a Microsoft implementa recursos e controles de proteção de dados padrão.
- [Funções do Azure AD com acesso ao Cloud App Security](https://docs.microsoft.com/cloud-app-security/manage-admins)

- [RBAC (controle de acesso baseado em função) do Azure](https://docs.microsoft.com/azure/role-based-access-control/overview) 

- [Entender a proteção de dados do cliente no Azure](https://docs.microsoft.com/azure/security/fundamentals/protection-customer-data)

**Monitoramento da Central de Segurança do Azure**: Não aplicável

**Responsabilidade**: Cliente

## <a name="asset-management"></a>Gerenciamento de Ativos

*Para obter mais informações, confira o [Azure Security Benchmark: gerenciamento de ativos](/azure/security/benchmarks/security-controls-v2-asset-management).*

### <a name="am-1-ensure-security-team-has-visibility-into-risks-for-assets"></a>AM-1: garantir que a equipe de segurança tenha visibilidade dos riscos de ativos

**Diretriz**: verifique se as equipes de segurança receberam as permissões Leitor de segurança no seu locatário e nas suas assinaturas do Azure, de modo que possam monitorar os riscos de segurança usando a Central de Segurança do Azure. 

Dependendo de como as responsabilidades da equipe de segurança são estruturadas, o monitoramento de riscos de segurança pode ser a responsabilidade de uma equipe de segurança central ou de uma equipe local. Dito isso, os insights e os riscos de segurança sempre precisam ser agregados de maneira centralizada em uma organização. 

As permissões de Leitor de segurança podem ser aplicadas amplamente a um locatário inteiro (grupo de gerenciamento raiz) ou terem como escopo grupos de gerenciamento ou assinaturas específicas. 

Observação: podem ser necessárias permissões adicionais a fim de obter visibilidade das cargas de trabalho e dos serviços. 

- [Visão geral da função Leitor de segurança](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#security-reader)

- [Visão geral dos grupos de gerenciamento do Azure](https://docs.microsoft.com/azure/governance/management-groups/overview)

**Monitoramento da Central de Segurança do Azure**: Não disponível no momento

**Responsabilidade**: Cliente

## <a name="logging-and-threat-detection"></a>Log e detecção de ameaças

*Para obter mais informações, confira o [Azure Security Benchmark: log e detecção de ameaças](/azure/security/benchmarks/security-controls-v2-logging-threat-protection).*

### <a name="lt-1-enable-threat-detection-for-azure-resources"></a>LT-1: habilitar a detecção de ameaças para recursos do Azure

**Diretrizes**: o defender for Identity pode notificá-lo quando detecta atividades suspeitas, enviando alertas de segurança e de integridade para o servidor syslog por meio de um sensor indicado.
Encaminhe todos os logs do defender para identidade para o SIEM, que pode ser usado para configurar as detecções de ameaças personalizadas. Verifique se você está monitorando diferentes tipos de ativos do Azure para possíveis ameaças e anomalias. Concentre-se em obter alertas de alta qualidade para reduzir os falsos positivos para os analistas classificarem. Os alertas podem ser originados de dados de log, agentes ou outros dados.

- [Como integrar com o syslog](https://docs.microsoft.com/defender-for-identity/setting-syslog)
- [Criar regras de análise personalizadas para detectar ameaças](https://docs.microsoft.com/azure/sentinel/tutorial-detect-threats-custom) 

- [Inteligência contra ameaças cibernéticos com o Azure Sentinel](https://docs.microsoft.com/azure/architecture/example-scenario/data/sentinel-threat-intelligence)

**Monitoramento da Central de Segurança do Azure**: Não aplicável

**Responsabilidade**: Cliente

### <a name="lt-2-enable-threat-detection-for-azure-identity-and-access-management"></a>LT-2: habilitar a detecção de ameaças para o gerenciamento de identidades e acesso do Azure

**Diretrizes**: Azure Active Directory (Azure AD) fornece os seguintes logs de usuário que podem ser exibidos no relatório do Azure ad ou integrados com Azure monitor, Azure Sentinel ou outras ferramentas de monitoramento/Siem para casos de uso de análise e monitoramento mais sofisticados:

- Entradas – O relatório de entradas fornece informações sobre o uso de aplicativos gerenciados e atividades de entrada do usuário.

- Logs de auditoria – Permitem o rastreio de todas as alterações feitas por vários recursos no Azure AD por meio de logs. Exemplos de logs de auditoria incluem alterações feitas em qualquer recurso no Azure AD, como adicionar ou remover usuários, aplicativos, grupos, funções e políticas.

- Entradas arriscadas - uma entrada arriscada é um indicador para uma tentativa de logon que pode ter sido realizada por alguém que não é o proprietário legítimo de uma conta de usuário.

- Usuários sinalizados para riscos - um usuário arriscado é um indicador de uma conta de usuário que pode ter sido comprometida.

A central de segurança do Azure também pode alertar sobre determinadas atividades suspeitas, como um número excessivo de tentativas de autenticação com falha, contas preteridas na assinatura. Além do monitoramento básico de higiene de segurança, o módulo de Proteção contra Ameaças da Central de Segurança do Azure também pode coletar alertas de segurança mais aprofundados de recursos de computação individuais do Azure (máquinas virtuais, contêineres, serviço de aplicativo), recursos de dados (BD SQL e armazenamento) e camadas de serviço do Azure. Essa funcionalidade permite que você veja anomalias de conta dentro dos recursos individuais.

- [Relatórios de atividades de auditoria no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-audit-logs) 

- [Habilitar o Azure Identity Protection](https://docs.microsoft.com/azure/active-directory/identity-protection/overview-identity-protection) 
- [Proteção contra ameaças na Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/threat-protection)

**Monitoramento da Central de Segurança do Azure**: Sim

**Responsabilidade**: Cliente

### <a name="lt-5-centralize-security-log-management-and-analysis"></a>LT-5: centralizar o gerenciamento e a análise do log de segurança

**Orientação**: Verifique se você está integrando os logs de atividades do Azure ao seu registro central. Os logs de ingestão por meio de Azure Monitor para agregar dados de segurança gerados por dispositivos de ponto de extremidade, recursos de rede e outros sistemas de segurança. No Azure Monitor, use espaços de trabalho do Log Analytics para consultar e executar análises e usar contas de armazenamento do Azure para armazenamento de longo prazo e arquivamento.

Além disso, habilite e integre dados ao Azure Sentinel ou a um SIEM de terceiros.

Muitas organizações optam por usar o Azure Sentinel para dados "quentes" que são usados com frequência e o armazenamento do Azure para dados "frios" que são usados com menos frequência.

O defender for Identity oferece para encaminhar todos os logs relacionados à segurança para o SIEM para gerenciamento centralizado.

- [Como coletar logs e métricas de plataforma com Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/platform/diagnostic-settings) 
- [Como integrar o Azure Sentinel](https://docs.microsoft.com/azure/sentinel/quickstart-onboard) 

- [Integrar o defender para identidade com o syslog](https://docs.microsoft.com/defender-for-identity/setting-syslog)

**Monitoramento da Central de Segurança do Azure**: Sim

**Responsabilidade**: Cliente

## <a name="incident-response"></a>Resposta a incidentes

*Para obter mais informações, confira o [Azure Security Benchmark: resposta a incidentes](/azure/security/benchmarks/security-controls-v2-incident-response).*

### <a name="ir-1-preparation--update-incident-response-process-for-azure"></a>IR-1: preparação – atualizar o processo de resposta a incidentes do Azure

**Diretriz**: verifique se a sua organização tem processos para responder a incidentes de segurança, atualizou esses processos para o Azure e está os exercendo regularmente para garantir a preparação.

- [Implementar a segurança em todo o ambiente empresarial](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud)

- [Guia de referência da resposta a incidentes](https://docs.microsoft.com/microsoft-365/downloads/IR-Reference-Guide.pdf)

**Monitoramento da Central de Segurança do Azure**: Não aplicável

**Responsabilidade**: Cliente

### <a name="ir-2-preparation--setup-incident-notification"></a>IR-2: preparação – configurar a notificação de incidentes

**Diretriz**: configure as informações de contato de incidentes de segurança na Central de Segurança do Azure. Essas informações de contato serão usadas pela Microsoft para entrar em contato com você se o MSRC (Microsoft Security Response Center) descobrir que os seus dados foram acessados por uma pessoa não autorizada ou ilegal. Você também tem opções para personalizar alertas de incidentes e notificações em diferentes serviços do Azure com base em suas necessidades de resposta a incidentes. 

- [Como definir o contato de segurança da Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-provide-security-contact-details)

**Monitoramento da Central de Segurança do Azure**: Sim

**Responsabilidade**: Cliente

### <a name="ir-3-detection-and-analysis--create-incidents-based-on-high-quality-alerts"></a>IR-3: detecção e análise – criar incidentes com base em alertas de alta qualidade

**Diretrizes**: verifique se você tem um processo para criar alertas de alta qualidade e medir a qualidade de alertas. Isso permite que você aprenda as lições dos últimos incidentes e priorize os alertas para os analistas, de modo a não perderem tempo em falsos positivos. 

Alertas de alta qualidade podem ser criados com base na experiência com incidentes passados, fontes de comunidade validadas e ferramentas projetadas para gerar e limpar alertas, focando e correlacionando várias fontes de sinal. 

A central de segurança do Azure (ASC) fornece alertas de alta qualidade em vários ativos do Azure. Use o conector de dados da ASC para transmitir os alertas para o Azure Sentinel. Com o Azure Sentinel, você pode criar regras de alertas avançadas a fim de gerar incidentes automaticamente para uma investigação. 

Exporte alertas e recomendações da Central de Segurança do Azure usando o recurso de exportação para ajudar a identificar os riscos para os recursos do Azure. Exporte os alertas e as recomendações de modo manual ou contínuo.

- [Como configurar a exportação](https://docs.microsoft.com/azure/security-center/continuous-export)

- [Como transmitir alertas para o Azure Sentinel](https://docs.microsoft.com/azure/sentinel/connect-azure-security-center)

**Monitoramento da Central de Segurança do Azure**: Não disponível no momento

**Responsabilidade**: Cliente

### <a name="ir-4-detection-and-analysis--investigate-an-incident"></a>IR-4: Detecção e análise – investigar um incidente

**Diretriz**: verifique se os analistas podem consultar e usar fontes de dados diversificadas à medida que investigam incidentes potenciais, para criar uma visão completa do que aconteceu. Logs diversificados devem ser coletados para acompanhar as atividades de um invasor potencial na cadeia de eliminação para evitar pontos cegos.  Você também deve garantir que os insights e os aprendizados sejam capturados para outros analistas e para referência histórica futura.  

As fontes de dados para investigação incluem as fontes de registro em log centralizadas que já estão sendo coletadas dos serviços dentro do escopo e sistemas em execução, mas também podem incluir:

- Dados de rede – Use os logs de fluxo dos grupos de segurança de rede, o Observador de Rede do Azure e o Azure Monitor para capturar logs de fluxo de rede e outras informações de análise. 

- Instantâneos dos sistemas em execução: 

    - Use a funcionalidade de instantâneo da máquina virtual do Azure para criar um instantâneo do disco do sistema em execução. 

    - Use a funcionalidade de despejo de memória nativa do sistema operacional para criar um instantâneo da memória do sistema em execução.

    - Use o recurso de instantâneo dos serviços do Azure ou a funcionalidade do seu software para criar instantâneos dos sistemas em execução.

O Azure Sentinel fornece ampla análise de dados em praticamente qualquer origem de log e um portal de gerenciamento de casos para gerenciar o ciclo de vida completo de incidentes. As informações de inteligência coletadas durante uma investigação podem ser associadas a um incidente para fins de rastreamento e relatório. 

- [Criar um instantâneo de disco de um computador Windows](https://docs.microsoft.com/azure/virtual-machines/windows/snapshot-copy-managed-disk)

- [Criar um instantâneo de disco de um computador Linux](https://docs.microsoft.com/azure/virtual-machines/linux/snapshot-copy-managed-disk)

- [Informações de diagnóstico e coleta de despejo de memória do Suporte do Microsoft Azure](https://azure.microsoft.com/support/legal/support-diagnostic-information-collection/) 

- [Investigar incidentes com o Azure Sentinel](https://docs.microsoft.com/azure/sentinel/tutorial-investigate-cases)

**Monitoramento da Central de Segurança do Azure**: Não aplicável

**Responsabilidade**: Cliente

### <a name="ir-5-detection-and-analysis--prioritize-incidents"></a>IR-5: detecção e análise – priorizar incidentes

**Diretriz**: forneça aos analistas o contexto dos incidentes nos quais eles devem se concentrar primeiro com base na severidade do alerta e na confidencialidade do ativo. 

A Central de Segurança do Azure atribui uma severidade a cada alerta para ajudar você a priorizar os alertas que devem ser investigados primeiro. A gravidade se baseia em quão confiante a central de segurança está na localização ou na análise usada para emitir o alerta, bem como o nível de confiança de que houve uma intenção mal-intencionada por trás da atividade que levou ao alerta.

Além disso, marque os recursos usando marcas e crie um sistema de nomenclatura para identificar e categorizar os recursos do Azure, em especial aqueles que processam dados confidenciais.  É sua responsabilidade priorizar a correção de alertas com base na criticalidade dos recursos do Azure e do ambiente em que o incidente ocorreu.

- [Alertas na Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-overview)

- [Usar marcas para organizar seus recursos do Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)

**Monitoramento da Central de Segurança do Azure**: Não disponível no momento

**Responsabilidade**: Cliente

### <a name="ir-6-containment-eradication-and-recovery--automate-the-incident-handling"></a>IR-6: confinamento, erradicação e recuperação – automatizar o tratamento de incidentes

**Diretriz**: automatize tarefas repetitivas manuais para acelerar o tempo de resposta e reduzir a carga dos analistas. As tarefas manuais demoram mais para serem executadas, atrasando cada incidente e reduzindo Quantos incidentes um analista pode manipular. Elas também aumentam a fadiga do analista, o que aumenta o risco de erros humanos que causam atrasos, prejudicando a capacidade dos analistas de se concentrarem efetivamente em tarefas complexas. Use os recursos de automação de fluxo de trabalho da Central de Segurança do Azure e do Azure Sentinel para disparar ações automaticamente ou executar um guia estratégico para responder aos alertas de segurança recebidos. O guia estratégico executa ações, como enviar notificações, desabilitar contas e isolar redes problemáticas. 

- [Configurar a automação de fluxo de trabalho na Central de Segurança](https://docs.microsoft.com/azure/security-center/workflow-automation)

- [Configurar respostas automatizadas a ameaças na Central de Segurança do Azure](https://docs.microsoft.com/azure/security-center/tutorial-security-incident#triage-security-alerts)

- [Configurar respostas de ameaças automatizadas no Azure Sentinel](https://docs.microsoft.com/azure/sentinel/tutorial-respond-threats-playbook)

**Monitoramento da Central de Segurança do Azure**: Não disponível no momento

**Responsabilidade**: Cliente

## <a name="posture-and-vulnerability-management"></a>Gerenciamento de postura e vulnerabilidades

*Para obter mais informações, confira o [Azure Security Benchmark: gerenciamento de postura e vulnerabilidades](/azure/security/benchmarks/security-controls-v2-vulnerability-management).*

### <a name="pv-8-conduct-regular-attack-simulation"></a>PV-8: realizar uma simulação de ataque regular

**Diretriz**: conforme necessário, realize testes de penetração ou atividades de equipe vermelhas nos seus recursos do Azure e garanta a correção de todas as conclusões de segurança críticas.
Siga as Regras de Participação no Teste de Penetração do Microsoft Cloud para garantir que os testes de penetração não violem as políticas da Microsoft. Use a estratégia da Microsoft, a execução de Equipes Vermelhas e os testes de penetração de sites online na infraestrutura, nos serviços e nos aplicativos de nuvem gerenciados pela Microsoft.

- [Teste de penetração no Azure](https://docs.microsoft.com/azure/security/fundamentals/pen-testing)

- [Regras de participação para testes de penetração](https://www.microsoft.com/msrc/pentest-rules-of-engagement?rtc=1) 

- [Equipes Vermelhas do Microsoft Cloud](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e)

**Monitoramento da Central de Segurança do Azure**: Não aplicável

**Responsabilidade**: Compartilhado

## <a name="governance-and-strategy"></a>Governança e estratégia

*Para obter mais informações, confira o [Azure Security Benchmark: governança e estratégia](/azure/security/benchmarks/security-controls-v2-governance-strategy).*

### <a name="gs-1-define-asset-management-and-data-protection-strategy"></a>GS-1: definir a estratégia de proteção de dados e gerenciamento de ativos 

**Diretriz**: documente e comunique uma estratégia clara para o monitoramento contínuo e a proteção de sistemas e dados. Priorize a descoberta, a avaliação, a proteção e o monitoramento de sistemas e dados comercialmente críticos. 

Essa estratégia deve incluir diretrizes documentadas, políticas e padrões para os seguintes elementos: 

-   Padrão de classificação de dados de acordo com os riscos de negócios

-   Visibilidade da organização de segurança dos riscos e do inventário de ativos 

-   Aprovação da organização de segurança dos serviços do Azure para uso 

-   Segurança de ativos por meio do ciclo de vida

-   Estratégia de controle de acesso obrigatório de acordo com a classificação de dados organizacionais

-   Uso de funcionalidades de proteção de dados de terceiros e nativas do Azure

-   Requisitos de criptografia de dados para casos de uso em trânsito e em repouso

-   Padrões de criptografia apropriados

Para saber mais, consulte as referências a seguir:
- [Recomendação da arquitetura de segurança do Azure – Armazenamento, dados e criptografia](https://docs.microsoft.com/azure/architecture/framework/security/storage-data-encryption?toc=/security/compass/toc.json&amp;bc=/security/compass/breadcrumb/toc.json)

- [Conceitos básicos de segurança do Azure – Segurança, criptografia e armazenamento de dados do Azure](https://docs.microsoft.com/azure/security/fundamentals/encryption-overview)

- [Cloud Adoption Framework – Melhores práticas de segurança e criptografia de dados do Azure](https://docs.microsoft.com/azure/security/fundamentals/data-encryption-best-practices?toc=/azure/cloud-adoption-framework/toc.json&amp;bc=/azure/cloud-adoption-framework/_bread/toc.json)

- [Azure Security Benchmark – Gerenciamento de ativos](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-asset-management)

- [Azure Security Benchmark – Proteção de dados](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-data-protection)

**Monitoramento da Central de Segurança do Azure**: Não aplicável

**Responsabilidade**: Cliente

### <a name="gs-2-define-enterprise-segmentation-strategy"></a>GS-2: definir uma estratégia de segmentação corporativa 

**Diretriz**: estabeleça uma estratégia de toda a empresa para segmentar o acesso aos ativos usando uma combinação de identidade, rede, aplicativo, assinatura, grupo de gerenciamento e outros controles.

Equilibre cuidadosamente a necessidade de separação de segurança com a necessidade de habilitação da operação diária dos sistemas que precisam se comunicar entre si e acessar dados.

Certifique-se de que a estratégia de segmentação seja implementada consistentemente nos tipos de controle, incluindo segurança de rede, identidade e modelos de acesso, além de permissões de aplicativo/modelos de acesso e controles de processos humanos.

- [Diretrizes sobre a estratégia de segmentação no Azure (vídeo)](https://docs.microsoft.com/security/compass/microsoft-security-compass-introduction#azure-components-and-reference-model-2151)

- [Diretrizes sobre a estratégia de segmentação no Azure (documento)](https://docs.microsoft.com/security/compass/governance#enterprise-segmentation-strategy)

- [Alinhar a segmentação de rede com a estratégia de segmentação corporativa](https://docs.microsoft.com/security/compass/network-security-containment#align-network-segmentation-with-enterprise-segmentation-strategy)

**Monitoramento da Central de Segurança do Azure**: Não aplicável

**Responsabilidade**: Cliente

### <a name="gs-3-define-security-posture-management-strategy"></a>GS-3: definir uma estratégia de gerenciamento de postura de segurança

**Diretriz**: Meça e atenue continuamente os riscos para seus ativos individuais e o ambiente no qual eles estão hospedados. Priorize os ativos de alto valor e as superfícies de ataque altamente expostas, como aplicativos publicados, pontos de entrada e saída de rede, os pontos de extremidade de usuário e administrador, etc.

- [Azure Security Benchmark – Gerenciamento de postura e vulnerabilidade](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-posture-vulnerability-management)

**Monitoramento da Central de Segurança do Azure**: Não aplicável

**Responsabilidade**: Cliente

### <a name="gs-4-align-organization-roles-responsibilities-and-accountabilities"></a>GS-4: alinhar funções e responsabilidades da organização

**Diretriz**: documente e comunique uma estratégia clara para funções e responsabilidades na sua organização de segurança. Priorize o fornecimento de responsabilidade clara por decisões de segurança, educando todos no modelo de responsabilidade compartilhada e instrua equipes técnicas sobre a tecnologia usada para proteger a nuvem.

- [Melhor prática de segurança do Azure 1 – Pessoas: educar as equipes na jornada de segurança na nuvem](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#1-people-educate-teams-about-the-cloud-security-journey)

- [Melhor prática de segurança do Azure 2 – Pessoas: educar as equipes na tecnologia de segurança na nuvem](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#2-people-educate-teams-on-cloud-security-technology)

- [Melhor prática de segurança do Azure 3 – Processo: atribuir responsabilidade por decisões de segurança na nuvem](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud)

**Monitoramento da Central de Segurança do Azure**: Não aplicável

**Responsabilidade**: Cliente

### <a name="gs-5-define-network-security-strategy"></a>GS-5: definir uma estratégia de segurança de rede

**Diretriz**: estabeleça uma abordagem de segurança de rede do Azure como parte da estratégia geral de controle de acesso de segurança da sua organização.  

Essa estratégia deve incluir diretrizes documentadas, políticas e padrões para os seguintes elementos: 

-   Gerenciamento de rede centralizado e responsabilidade pela segurança

-   Modelo de segmentação de rede virtual alinhado com a estratégia de segmentação corporativa

-   Estratégia de correção em diferentes cenários de ameaças e ataques

-   Estratégia de entrada e saída e borda da Internet

-   Estratégia de interconectividade local e de nuvem híbrida

-   Artefatos de segurança de rede atualizados (por exemplo, diagramas de rede, arquitetura de rede de referência)

Para saber mais, consulte as referências a seguir:
- [Melhor prática de segurança do Azure 11 – Arquitetura: uma estratégia de segurança unificada](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#11-architecture-establish-a-single-unified-security-strategy)

- [Azure Security Benchmark – Segurança de rede](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-network-security)

- [Visão geral da segurança de rede do Azure](https://docs.microsoft.com/azure/security/fundamentals/network-overview)

- [Estratégia de arquitetura de rede corporativa](https://docs.microsoft.com/azure/cloud-adoption-framework/ready/enterprise-scale/architecture)

**Monitoramento da Central de Segurança do Azure**: Não aplicável

**Responsabilidade**: Cliente

### <a name="gs-6-define-identity-and-privileged-access-strategy"></a>GS-6: definir uma estratégia de identidade e acesso privilegiado

**Diretriz**: estabeleça abordagens de identidade e acesso privilegiado do Azure como parte da estratégia geral de controle de acesso de segurança da sua organização.  

Essa estratégia deve incluir diretrizes documentadas, políticas e padrões para os seguintes elementos: 

-   Um sistema de identidade e autenticação centralizado e a interconectividade dele com outros sistemas de identidade internos e externos

-   Métodos de autenticação forte em diferentes casos de uso e condições

-   Proteção de usuários altamente privilegiados

-   Monitoramento e tratamento de atividades de usuário de anomalias  

-   Processo de revisão de acesso e reconciliação e identidade do usuário

Para saber mais, consulte as referências a seguir:

- [Azure Security Benchmark – Gerenciamento de identidades](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-identity-management)

- [Azure Security Benchmark – Acesso privilegiado](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-privileged-access)

- [Melhor prática de segurança do Azure 11 – Arquitetura: uma estratégia de segurança unificada](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#11-architecture-establish-a-single-unified-security-strategy)

- [Visão geral da segurança de gerenciamento de identidade do Azure](https://docs.microsoft.com/azure/security/fundamentals/identity-management-overview)

**Monitoramento da Central de Segurança do Azure**: Não aplicável

**Responsabilidade**: Cliente

### <a name="gs-7-define-logging-and-threat-response-strategy"></a>GS-7: definir uma estratégia de log e resposta a ameaças

**Diretriz**: estabeleça uma estratégia de log e resposta a ameaças para detectar e corrigir as ameaças rapidamente, atendendo aos requisitos de conformidade. Priorize o fornecimento de alertas de alta qualidade e experiências perfeitas aos analistas para que eles possam se concentrar em ameaças em vez de etapas manuais e de integração. 

Essa estratégia deve incluir diretrizes documentadas, políticas e padrões para os seguintes elementos: 

-   A função e as responsabilidades da organização de SecOps (operações de segurança) 

-   Um processo de resposta a incidentes bem definido, alinhando-se ao NIST ou a outra estrutura do setor 

-   Captura e retenção de log para dar suporte às necessidades de conformidade, detecção de ameaças e resposta a incidentes

-   Visibilidade centralizada das ameaças e informações de correlação sobre elas por meio do SIEM, de funcionalidades nativas do Azure e de outras fontes 

-   Plano de comunicação e notificação com seus clientes, fornecedores e partes públicas interessadas

-   Uso de plataformas nativas e de terceiros do Azure para tratamento de incidentes, como log e detecção de ameaças, análise forense, além de correção e erradicação de ataques

-   Processos para tratamento de incidentes e atividades pós-incidente, como lições aprendidas e retenção de evidências

Para saber mais, consulte as referências a seguir:

- [Azure Security Benchmark – Log e detecção de ameaças](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-logging-threat-detection)

- [Azure Security Benchmark – Resposta a incidentes](https://docs.microsoft.com/azure/security/benchmarks/security-benchmark-v2-incident-response)

- [Melhor prática de segurança do Azure 4 – Processo: atualizar processos de resposta a incidentes para a nuvem](https://docs.microsoft.com/azure/cloud-adoption-framework/security/security-top-10#4-process-update-incident-response-ir-processes-for-cloud)

- [Guia de log, de decisão de relatórios e do Adoption Framework do Azure](https://docs.microsoft.com/azure/cloud-adoption-framework/decision-guides/logging-and-reporting/)

- [Escala empresarial, gerenciamento e monitoramento do Azure](https://docs.microsoft.com/azure/cloud-adoption-framework/ready/enterprise-scale/management-and-monitoring)

**Monitoramento da Central de Segurança do Azure**: Não aplicável

**Responsabilidade**: Cliente

## <a name="next-steps"></a>Próximas etapas

- Confira a [Visão geral do Azure Security Benchmark V2](/azure/security/benchmarks/overview)
- Saiba mais sobre a [Linhas de base de segurança do Azure](/azure/security/benchmarks/security-baselines-overview)
