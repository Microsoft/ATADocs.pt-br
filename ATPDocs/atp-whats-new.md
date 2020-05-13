---
title: Novidades no ATP do Azure (Proteção Avançada contra Ameaças do Azure)
description: Este artigo é atualizado com frequência para que você conheça as novidades da versão mais recente do ATP do Azure (Proteção Avançada Contra Ameaças do Azure).
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 04/23/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: 178175373153ce162042cee3228628a9ca9ab2c8
ms.sourcegitcommit: 2d1bdcc3adee8452aef7259a99c9aaa2f87c31cd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82886540"
---
# <a name="whats-new-in-azure-advanced-threat-protection-azure-atp"></a>Novidades no ATP do Azure (Proteção Avançada contra Ameaças do Azure)

Este artigo é atualizado com frequência para manter você informado sobre as novidades nas últimas versões do ATP do Azure.

Para obter detalhes das versões anteriores do ATP do Azure até (e incluindo) a versão 2.55, confira a [referência de versão do ATP do Azure](atp-release-reference.md).

Feed RSS: Receba uma notificação quando esta página for atualizada copiando e colando a seguinte URL em seu leitor de feed: `https://docs.microsoft.com/api/search/rss?search=%22This+article+is+updated+frequently+to+let+you+know+what%27s+new+in+the+latest+release+of+Azure+ATP%22&locale=en-us`

## <a name="azure-atp-release-2113"></a>ATP do Azure versão 2.113

Lançado em 5 de maio de 2020

- **Aprimoramento do recurso: Atividade enriquecida de acesso a recursos com o NTLMv1**  
Desta versão em diante, o ATP do Azure fornece informações para atividades de acesso a recursos que mostram se o recurso usa a autenticação NTLMv1. Essa configuração de recurso não é segura e representa um risco de que atores mal-intencionados possam forçar o aplicativo para vantagem deles. Para obter mais informações sobre o risco, confira [Uso de protocolos herdados](atp-cas-isp-legacy-protocols.md).

- **Aprimoramento do recurso: Alerta de suspeita de ataque de força bruta (Kerberos, NTLM)**  
O ataque de força bruta é usado por invasores para obter acesso à sua organização. Ele é um método-chave para a descoberta de ameaças e de riscos no ATP do Azure. A fim de ajudar você a se concentrar nos riscos críticos para os usuários, essa atualização torna mais fácil e rápido analisar e corrigir riscos, limitando e priorizando o volume de alertas.

## <a name="azure-atp-release-2112"></a>ATP do Azure versão 2.112

Lançado em 15 de março de 2020

- **Novas instâncias do ATP do Azure são integradas automaticamente com o Microsoft Cloud App Security**  
Ao criar uma instância do ATP do Azure (anteriormente workspace), a integração com o Microsoft Cloud App Security é habilitada por padrão. Para saber mais sobre a integração, confira [Usar o ATP do Azure com o Microsoft Cloud App Security](atp-mcas-integration.md).

- **Novas atividades monitoradas**  
Os seguintes monitores de atividade agora estão disponíveis:
  - Logon interativo com certificado
  - Falha no logon com certificado
  - Acesso de recurso delegado

    Saiba mais sobre quais [atividades o ATP do Azure monitora](monitored-activities.md) e como [filtrar e pesquisar atividades monitoradas](atp-activities-search.md) no portal.

- **Aprimoramento do recurso: Atividade de acesso a recursos aprimorados**  
A partir desta versão, o ATP do Azure fornece informações para atividades de acesso a recursos que mostram se o recurso é confiável para delegação irrestrita. Essa configuração de recurso não é segura e representa um risco de que atores mal-intencionados possam forçar o aplicativo para vantagem deles. Para saber mais sobre o risco, confira [Avaliação de segurança: delegação de Kerberos não segura](atp-cas-isp-unconstrained-kerberos.md).

- **Suspeita de manipulação de pacote SMB (exploração de CVE-2020-0796) – (versão prévia)**  
O alerta de segurança de [Suspeita de manipulação de pacote SMB](atp-lateral-movement-alerts.md#suspected-smb-packet-manipulation-cve-2020-0796-exploitation-external-id-2406) do ATP do Azure está agora em versão prévia pública. Nessa detecção, é disparado um alerta de segurança do ATP do Azure quando um pacote SMBv3 suspeito de explorar a vulnerabilidade de segurança [CVE-2020-0796](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2020-0796) invade um controlador de domínio na rede.

## <a name="azure-atp-release-2111"></a>ATP do Azure versão 2.111

Lançado em 1º de março de 2020

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.

## <a name="azure-atp-release-2110"></a>ATP do Azure versão 2.110

Lançado em 23 de fevereiro de 2020

- **Nova avaliação de segurança: controladores de domínio não monitorados**  
As avaliações de segurança do ATP do Azure agora incluem um relatório sobre controladores de domínio não monitorados, servidores sem um sensor, para ajudá-lo a gerenciar a cobertura total do seu ambiente. Para saber mais, confira [Controladores de domínio não monitorados](atp-cas-isp-unmonitored-domain-controller.md).

## <a name="azure-atp-release-2109"></a>ATP do Azure versão 2.109

Lançado em 16 de fevereiro de 2020

- **Aprimoramento do recurso: entidades confidenciais**  
A partir desta versão (2.109), os computadores identificados como servidores DNS, DHCP ou Autoridade Certificada pelo ATP do Azure serão marcados automaticamente como **Confidenciais**.

## <a name="azure-atp-release-2108"></a>ATP do Azure versão 2.108

Lançado em 9 de fevereiro de 2020

- **Novo recurso: suporte para Contas de Serviço Gerenciado de Grupo**  
O ATP do Azure agora dá suporte ao uso de gMSA (Contas de Serviço Gerenciado de Grupo) para aumentar a segurança ao conectar sensores do ATP do Azure às suas florestas do AD (Azure Active Directory). Para saber mais sobre como usar a gMSA com sensores do ATP do Azure, confira [Conectar à sua floresta do Active Directory](install-atp-step2.md#prerequisites).

- **Aprimoramento do recurso: relatório agendado com muitos dados**  
Quando um relatório agendado tem muitos dados, o email agora informa sobre o fato, exibindo o seguinte texto: havia dados em excesso durante o período especificado para gerar um relatório. Isso substitui o comportamento anterior de apenas descobrir o fato depois de clicar no link do relatório no email.

- **Aprimoramento do recurso: lógica de cobertura do controlador de domínio atualizada**  
Atualizamos nossa lógica do relatório de cobertura do controlador de domínio para incluir informações adicionais do Azure AD, resultando em uma exibição mais precisa dos controladores de domínio sem sensores neles. Essa nova lógica também deve ter um efeito positivo no Microsoft Secure Score correspondente.

## <a name="azure-atp-release-2107"></a>ATP do Azure versão 2.107

Lançado em 3 de fevereiro de 2020

- **Nova atividade monitorada: Alteração do histórico de SID**  
A alteração do histórico de SID agora é uma atividade monitorada e filtrável. Saiba mais sobre quais [atividades o ATP do Azure monitora](monitored-activities.md) e como [filtrar e pesquisar atividades monitoradas](atp-activities-search.md) no portal.

- **Aprimoramento do recurso: Alertas fechados ou suprimidos não são mais reabertos**  
Depois que um alerta é fechado ou suprimido no portal da ATP do Azure, se a mesma atividade for detectada novamente em um curto período, um novo alerta será aberto. Anteriormente, sob as mesmas condições, o alerta era reaberto.

- **Necessário o TLS 1.2 para acesso ao portal e aos sensores**  
Agora o TLS 1.2 é necessário para usar os sensores do ATP do Azure e o serviço de nuvem. O acesso ao portal do ATP do Azure não será mais possível usando navegadores que não são compatíveis com TLS 1.2.

## <a name="azure-atp-release-2106"></a>Versão 2.106 do Azure ATP

Lançado em 19 de janeiro de 2020

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.

## <a name="azure-atp-release-2105"></a>ATP do Azure versão 2.105

Lançado em 12 de janeiro de 2020

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.

## <a name="azure-atp-release-2104"></a>Versão 2.104 do ATP do Azure

Lançado em 23 de dezembro de 2019

- **Expirações de versão do sensor eliminadas**  
A implantação do sensor do ATP do Azure e os pacotes de instalação do sensor não expiram mais após várias versões e agora são atualizados apenas uma vez. O resultado desse recurso é que os pacotes de instalação do sensor baixados anteriormente agora podem ser instalados mesmo que sejam mais antigos do que nosso número máximo de versões expiradas.

- **Confirmar comprometimento**  
Agora você pode confirmar o comprometimento de usuários específicos do Office 365 e definir o nível de risco deles para **alto**. Esse fluxo de trabalho permite que suas equipes de operações de segurança tenham outro recurso de resposta para reduzir os limites de tempo para resolver incidentes de segurança. Saiba mais sobre [como confirmar o comprometimento](https://docs.microsoft.com/cloud-app-security/tutorial-ueba?branch=pr-en-us-1204#phase-4-protect-your-organization) usando o ATP do Azure e o Cloud App Security.

- **Faixa da nova experiência**  
Nas páginas do portal do ATP do Azure em que uma nova experiência está disponível no portal do Cloud App Security, são exibidas novas faixas que descrevem o que está disponível nos links de acesso.

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-2103"></a>ATP do Azure versão 2.103

Lançado em 15 de dezembro de 2019

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.

## <a name="azure-atp-release-2102"></a>ATP do Azure versão 2.102

Lançado em 8 de dezembro de 2019

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.

## <a name="azure-atp-release-2101"></a>ATP do Azure versão 2.101

Lançado em 24 de novembro de 2019

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.

## <a name="azure-atp-release-2100"></a>ATP do Azure versão 2.100

Lançado em 17 de novembro de 2019

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.

## <a name="azure-atp-release-299"></a>ATP do Azure versão 2.99

Lançado em 3 de novembro de 2019

- **Aprimoramento do recurso:  A notificação da interface do usuário da disponibilidade do portal do Cloud App Security foi adicionada ao portal do ATP do Azure**  
Para garantir que todos os usuários estejam cientes da disponibilidade dos recursos aprimorados no portal do Cloud App Security, uma notificação foi adicionada ao portal na linha do tempo de alertas do ATP do Azure.

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.

## <a name="azure-atp-release-298"></a>ATP do Azure versão 2.98

Lançado em 27 de outubro de 2019

- **Aprimoramento do recurso: Alerta de suspeita de ataque de força bruta**  
Melhoria do alerta de [SMB (suspeita de ataque de força bruta)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033) usando análise adicional, e melhoria da lógica de detecção para reduzir resultados de alerta **B-TP (verdadeiro positivo benigno)** e **FP (falso positivo)** .

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.

## <a name="azure-atp-release-297"></a>ATP do Azure versão 2.97

Lançado em 6 de outubro de 2019

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.

## <a name="azure-atp-release-296"></a>ATP do Azure versão 2.96

Lançado em 22 de setembro de 2019

- **Dados de autenticação NTLM aprimorados usando o evento 8004 do Windows**  
Os sensores da ATP do Azure agora podem ler e enriquecer automaticamente as atividades de autenticações NTLM com seus dados de servidor acessados quando a auditoria NTLM está habilitada e o evento 8004 do Windows está ativado. A ATP do Azure analisa o evento 8004 do Windows para autenticações NTLM a fim de enriquecer os dados de autenticação NTLM usados para análise de ameaças e alertas da ATP do Azure. Esse recurso avançado fornece atividade de acesso a recursos sobre dados NTLM, bem como atividades de logon com falha aprimoradas, incluindo o computador de destino que o usuário tentou, mas falhou ao acessar.

    Saiba mais sobre as atividades de autenticação NTLM [usando o evento 8004 do Windows](configure-windows-event-collection.md#ntlm-authentication-using-windows-event-8004).

- A versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-295"></a>ATP do Azure versão 2.95

Lançado em 15 de setembro de 2019

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.

## <a name="azure-atp-release-294"></a>ATP do Azure versão 2.94

Lançado em 8 de setembro de 2019

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.

## <a name="azure-atp-release-293"></a>ATP do Azure versão 2.93

Lançado em 1º de setembro de 2019

-   Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.

## <a name="azure-atp-release-292"></a>ATP do Azure versão 2.92

Lançado em 25 de agosto de 2019

-   Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.

## <a name="azure-atp-release-291"></a>ATP do Azure versão 2.91

Lançado em 18 de agosto de 2019

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.

## <a name="azure-atp-release-290"></a>ATP do Azure versão 2.90

Lançado em 11 de agosto de 2019

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.

## <a name="azure-atp-release-289"></a>ATP do Azure versão 2.89

Lançado em 4 de agosto de 2019

- **Aprimoramentos do método do sensor**  
Para evitar o excesso de geração de tráfego NTLM na criação de avaliações de LMP (Caminho de Movimento Lateral) precisas, foram feitas melhorias nos métodos do sensor do ATP do Azure para confiar menos no uso do NTLM e fazer um uso mais significativo do Kerberos.

- **Melhoria de alerta: uso suspeito do Golden Ticket (conta inexistente)**  
Foram adicionadas alterações de nome SAM aos tipos de evidência de suporte listados neste tipo de alerta. Para saber mais sobre o alerta, incluindo como evitar e corrigir esse tipo de atividade, confira [Uso suspeito do Golden Ticket (conta inexistente)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027).

- **Disponibilidade geral: suspeita de violação da autenticação NTLM**  
O alerta de [Suspeita de violação da autenticação NTLM](atp-lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039) não está mais no modo de versão prévia e agora está disponível para o público em geral.

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.

## <a name="azure-atp-release-288"></a>ATP do Azure versão 2.88

Lançado em 28 de julho de 2019

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-287"></a>ATP do Azure versão 2.87

Lançado em 21 de julho de 2019

- **Aprimoramento do recurso: Coleta de eventos de syslog automatizada para sensores autônomos do ATP do Azure**  
As conexões de syslog de entrada para sensores autônomos do ATP do Azure agora são totalmente automatizadas, enquanto a opção de alternância é removida da tela de configuração. Essas alterações não têm nenhum efeito nas conexões de syslog de saída.

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-286"></a>ATP do Azure versão 2.86

Lançado em 14 de julho de 2019

- **Novo alerta de segurança: suspeita de violação da autenticação NTLM (ID externa 2039)**  
O novo alerta de segurança de [suspeita de violação de autenticação do NTLM](atp-lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039) do ATP do Azure agora está em versão prévia pública.    Nessa detecção, um alerta de segurança do ATP do Azure é disparado quando há suspeita de que o uso de um ataque man-in-the-middle tenha ignorado com êxito a MIC (verificação de integridade da mensagem) do NTLM, uma vulnerabilidade de segurança detalhada no Microsoft [CVE-2019-040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040). Esses tipos de ataques tentam fazer downgrade dos recursos de segurança do NTLM e se autenticam com êxito, com a meta final de fazer movimentos laterais bem-sucedidos.

- **Aprimoramento do recurso: Identificação do sistema operacional do dispositivo aprimorado**  
Até agora, o ATP do Azure forneceu informações do sistema operacional do dispositivo de entidade com base no atributo disponível no Active Directory. Anteriormente, se as informações do sistema operacional não estavam disponíveis no Active Directory, elas também não ficavam disponíveis nas páginas de entidade do ATP do Azure. Desta versão em diante, graças ao uso dos métodos de identificação de sistema operacional de dispositivo aprimorado, o ATP do Azure agora fornece essas informações para dispositivos em que o Active Directory não tem as informações ou que não estão registrados no Active Directory.

    A adição dos dados de identificação de sistema operacional de dispositivo aprimorado ajuda a identificar dispositivos não registrados e não Windows, auxiliando simultaneamente em seu processo de investigação. Para saber mais sobre a resolução de nomes de rede no ATP do Azure, confira [Noções básicas sobre a NRR (resolução de nomes de rede)](atp-nnr-policy.md).  

- **Novo recurso: Proxy autenticado – versão prévia**  
O ATP do Azure agora é compatível com proxy autenticado. Especifique a URL do proxy usando a linha de comando do sensor e especifique o nome de usuário/senha para usar proxies que exigem autenticação. Para obter mais informações sobre como usar o proxy autenticado, confira [Configurar o proxy](https://docs.microsoft.com/azure-advanced-threat-protection/configure-proxy#configure-the-proxy).

- **Aprimoramento do recurso: Processo sincronizador de domínio automatizado**  
O processo de designação e marcação de controladores de domínio como candidatos do sincronizador de domínio durante a instalação e a configuração contínua agora é totalmente automatizado. A opção de alternância para selecionar manualmente os controladores de domínio como candidatos do sincronizador de domínio foi removida.

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-285"></a>ATP do Azure versão 2.85

Lançado em 7 de julho de 2019

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-284"></a>ATP do Azure versão 2.84

Lançado em 1º de julho de 2019

- **Suporte a novo local: data center do Azure no Reino Unido**  
Agora as instâncias do ATP do Azure são compatíveis com o data center do Azure no Reino Unido. Para saber mais como criar instâncias do ATP do Azure e seus locais de data center correspondentes, confira a [Etapa 1 da instalação do ATP do Azure](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step10).

- **Aprimoramento do recurso: novo nome e recursos para o alerta Adições suspeitas a grupos confidenciais (ID externa 2024)**  
O alerta **Adições suspeitas a grupos confidenciais** era denominado alerta **Modificações suspeitas modificações em grupos confidenciais**. A ID externa do alerta (ID 2024) permanece a mesma. A alteração do nome descritivo reflete com maior precisão a finalidade dos alertas em adições aos seus grupos **confidenciais**. O alerta aprimorado também conta com novas evidências e descrições aprimoradas. Para saber mais, confira [Adições suspeitas a grupos confidenciais](https://docs.microsoft.com/azure-advanced-threat-protection/atp-domain-dominance-alerts#suspicious-additions-to-sensitive-groups-external-id-2024).  

- **Nova documentação: guia para migrar do Advanced Threat Analytics para o ATP do Azure**  
Este novo artigo inclui pré-requisitos, diretrizes de planejamento e etapas de configuração e verificação para migrar do ATA para o serviço de ATP do Azure. Para saber mais, confira [Migrar do ATA para o ATP do Azure](https://docs.microsoft.com/azure-advanced-threat-protection/ata-atp-move-overview).

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-283"></a>ATP do Azure versão 2.83

Lançado em 23 de junho de 2019

- **Aprimoramento do recurso: alerta Criação de serviço suspeito (ID externa 2026)**  
Este alerta agora conta com uma página de alerta aprimorada com evidência adicional e uma nova descrição. Para saber mais, confira [Alerta de segurança da criação de serviço suspeito](https://docs.microsoft.com/azure-advanced-threat-protection/atp-domain-dominance-alerts#suspicious-service-creation-external-id-2026).

- **Suporte à nomenclatura de instância: suporte adicionado para prefixo de domínio de apenas dígitos**  
Suporte adicionado para criação de instâncias do ATP do Azure usando prefixos de domínio inicial que contêm apenas dígitos. Por exemplo, agora há suporte ao uso de prefixos de domínio inicial de apenas dígitos como 123456.contoso.com.

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-282"></a>ATP do Azure versão 2.82

Lançado em 18 de junho de 2019

- **Nova versão prévia pública**  
A experiência de investigação de ameaça de identidade do ATP do Azure agora está em **Versão prévia pública** e está disponível para todos os locatários protegidos do ATP do Azure. Confira [Experiência de investigação do Microsoft Cloud App Security do ATP do Azure](atp-mcas-integration.md) para saber mais.

- **Disponibilidade geral**  
O suporte do ATP do Azure para florestas não confiáveis está agora em disponibilidade geral. Confira [Várias florestas do ATP do Azure](atp-multi-forest.md) para saber mais.

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-281"></a>Azure ATP versão 2.81

Lançado em 10 de junho de 2019

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-280"></a>ATP do Azure versão 2.80

Lançado em 2 de junho de 2019

- **Aprimoramento do recurso: Alerta de conexão VPN suspeita**  
Esse alerta agora inclui evidência aprimorada e textos para melhor utilização. Para obter mais informações sobre os recursos de alerta e as etapas de correção e prevenção sugeridas, confira a [Descrição do alerta de conexão VPN suspeita](atp-compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025).

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-279"></a>Azure ATP versão 2.79

Lançado em 26 de maio de 2019

- **Disponibilidade geral: Reconhecimento de entidade de segurança (LDAP) (ID 2038 externa)**

    Esse alerta já está em disponibilidade geral. Para obter mais informações sobre o alerta, os recursos do alerta e a correção e prevenção sugeridas, confira a [descrição do alerta Reconhecimento de entidade de segurança (LDAP)](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-278"></a>ATP do Azure versão 2.78

Lançado em 19 de maio de 2019

- **Aprimoramento do recurso: entidades confidenciais**  
Marcação Confidencial Manual para Servidores Exchange

    Agora você pode marcar manualmente entidades como Servidores Exchange durante a configuração.

    Para marcar manualmente uma entidade como um Servidor Exchange:
    1. No portal do ATP do Azure, acesse o menu **Configuração**.
    2. Em **Detecção**, escolha **Marcas de entidade** e, em seguida, escolha **Confidencial**.
    3. Escolha **Exchange Servers** e, em seguida, adicione a entidade que você deseja marcar.

    Depois de marcar um computador como um Exchange Server, ele será marcado como Confidencial e exibirá que foi marcado como um Servidor Exchange.  A marcação Confidencial será exibida no perfil da entidade do computador, e o computador será analisado em todas as detecções baseadas em contas confidenciais e Caminhos de Movimentação Lateral.

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-277"></a>ATP do Azure versão 2.77

Lançado em 12 de maio de 2019

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-276"></a>ATP do Azure versão 2.76

Lançada em 6 de maio de 2019

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-275"></a>ATP do Azure versão 2.75

Lançada em 28 de abril de 2019

- **Aprimoramento do recurso: entidades confidenciais**  
A partir desta versão (2.75), os computadores identificados como servidores do Exchange pelo ATP do Azure serão marcados automaticamente como **Confidenciais**.  

    As entidades marcadas automaticamente como **Confidenciais** por funcionarem como servidores do Exchange listam essa classificação como o motivo pelo qual são marcadas.

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-274"></a>ATP do Azure versão 2.74

Lançamento em 14 de abril de 2019

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-273"></a>ATP do Azure versão 2.73

Lançado em 10 de abril de 2019

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-272"></a>ATP do Azure, versão 2.72

Lançada em 31 de março de 2019

- **Aprimoramento do recurso: profundidade com escopo do LMP (caminho de movimento lateral)**  
Os LMPs (caminhos de movimento lateral) são um método fundamental para a descoberta de ameaças e riscos no ATP do Azure. Para ajudar a manter o foco em riscos críticos para os usuários mais confidenciais, essa atualização torna mais fácil e rápido analisar e corrigir riscos para esses usuários em cada LMP, limitando o escopo e a profundidade de cada gráfico exibido.

    Confira os [caminhos de movimento lateral](use-case-lateral-movement-path.md) para saber mais sobre como a ATP do Azure usa os LMPs para expor riscos de acesso a cada entidade em seu ambiente.

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-271"></a>ATP do Azure versão 2.71

Lançado em 24 de março de 2019

- **Aprimoramento do recurso: Alertas de integridade da Resolução de nomes de rede (NNR)**  
Os alertas de integridade foram adicionados para níveis de confiança associados aos alertas de segurança do ATP do Azure que se baseiam na NNR. Cada alerta de integridade inclui recomendações detalhadas e acionáveis para ajudar a resolver as baixas taxas de sucesso da NNR.

    Saiba mais sobre como o ATP do Azure usa a NNR e por que ela é importante para a precisão do alerta em [O que é a Resolução de nomes da rede](atp-nnr-policy.md).

- **Suporte do servidor: suporte adicionado para o Server 2019 com uso de KB4487044**  
Suporte adicionado para o uso do Windows Server 2019, com um nível de patch de KB4487044. Não há suporte para o uso do Server 2019 sem o patch, que é bloqueado a partir desta atualização.

- **Aprimoramento do recurso: exclusão de alerta com base no usuário**  
As opções estendidas de exclusão de alerta agora permitem a exclusão de usuários específicos de alertas específicos. As exclusões podem ajudar a evitar situações em que o uso ou a configuração de certos tipos de software interno disparavam repetidamente alertas de segurança benignos.

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-270"></a>ATP do Azure versão 2.70

Lançado em 17 de março de 2019

- **Aprimoramento do recurso: Adição do nível de confiança NNR (Resolução de Nomes de Rede) a vários alertas** A NNR ou a Resolução de Nomes de Rede é usada para ajudar a identificar de maneira positiva a identidade da entidade de origem dos ataques suspeitos. Adicionando os níveis de confiança de NNR às listas de evidências de alerta do ATP do Azure, agora você pode avaliar e compreender instantaneamente o nível de confiança de NNR relacionado às possíveis origens identificadas e aplicar as correções adequadas.

    A evidência no nível de confiança de NNR foi adicionada aos seguintes alertas:
  - [Reconhecimento de mapeamento de rede (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)
  - [Suspeita de roubo de identidade (Pass-the-Ticket)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)
  - [Suspeita de ataque de retransmissão de NTLM (conta do Exchange) — versão prévia](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)
  - [Suspeita de ataque de DCSync (replicação de serviços de diretório)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)

- **Cenário adicional de alerta de integridade: falha ao iniciar o serviço do sensor do ATP do Azure**  
Agora, quando o sensor do ATP do Azure não pode ser iniciado devido a um problema de driver de captura de rede, um alerta de integridade do sensor é disparado. Confira [Solução de problemas do sensor do ATP do Azure com logs do ATP do Azure](troubleshooting-atp-using-logs.md), para obter mais informações sobre os logs do ATP do Azure e como usá-los.

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-269"></a>ATP do Azure versão 2.69

Lançada em 10 de março de 2019

- **Aprimoramento do recurso: Alerta de suspeita de roubo de identidade (Pass-the-Ticket)** Este alerta agora apresenta uma nova evidência que mostra os detalhes das conexões feitas por meio do protocolo RDP. A evidência adicionada facilita a correção do problema conhecido de alertas benignos verdadeiro positivo (B-TP) causado pelo uso da credencial da Credential Guard remota através de conexões de RDP.

- **Aprimoramento do recurso: Alerta de execução remota de código sobre DNS**  
Esse alerta agora apresenta nova evidência mostrando ao seu controlador de domínio as atualizações de status de segurança, informando quando atualizações são necessárias.

- **Nova documentação: Alerta de segurança do MITRE ATT & CK Matrix&trade;** do ATP do Azure  
Para explicar e facilitar o mapeamento da relação entre alertas de segurança do ATP do Azure e o MITRE ATT & CK Matrix conhecido, adicionamos as técnicas MITRE relevantes para listagens de alertas de segurança do ATP do Azure. Essa referência adicional facilita o reconhecimento da técnica de ataque suspeito potencialmente em uso quando um alerta de segurança do ATP do Azure é acionado. Saiba mais sobre o [guia de alerta de segurança do ATP do Azure](suspicious-activity-guide.md).  

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-268"></a>Azure ATP versão 2.68

Lançada em 3 de março de 2019

- **Aprimoramento do recurso: Alerta de suspeita de LDAP (ataque de força bruta)**  
Foram feitas melhorias de usabilidade consideráveis nesse alerta de segurança, incluindo uma descrição revisada, fornecimento de informações de origem adicionais e detalhes da tentativa de adivinhação para correção mais ágil.  
Saiba mais sobre alertas de segurança de [Suspeita de LDAP (ataque de força bruta)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004).

- **Nova documentação: Laboratório de alerta de segurança**  
Para explicar o poder do ATP do Azure na detecção de ameaças reais ao seu ambiente de trabalho, adicionamos um novo **Laboratório de alerta de segurança** a esta documentação. O **Laboratório de alerta de segurança** ajuda você a configurar rapidamente um laboratório ou ambiente de teste, e explica a melhor postura de defesa contra ataques e ameaças comuns e reais.  

    O [laboratório passo a passo](atp-playbook-lab-overview.md) foi projetado para garantir que você gaste o mínimo de tempo criando e o máximo de tempo aprendendo sobre o panorama de ameaças e os alertas e proteção disponíveis no ATP do Azure. Estamos ansiosos para receber seus comentários.

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-267"></a>ATP do Azure versão 2.67

Lançado em 24 de fevereiro de 2019

- **Novo alerta de segurança: Reconhecimento de entidade de segurança (LDAP) - (versão prévia)**  
O alerta de segurança de [Reconhecimento de entidade de segurança (LDAP) – versão prévia](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038) do ATP do Azure está agora em versão prévia pública.    Nessa detecção, um alerta de segurança do ATP do Azure é disparado quando o reconhecimento de entidade de segurança é usado pelos invasores para obter informações essenciais sobre o ambiente de domínio. Estas informações ajudam os invasores a mapear a estrutura de domínio, bem como identificar contas privilegiadas para uso em etapas posteriores em sua cadeia de encerramento do ataque.

    O protocolo LDAP (Lightweight Directory Access Protocol) é um dos métodos mais populares usados para fins legítimos e mal-intencionados para consultar o Active Directory Domain Services. O reconhecimento de entidade de segurança focada no LDAP é normalmente usado como a primeira fase de um ataque Kerberoasting. Os ataques de Kerberoasting são usados para obter uma lista de destino de SPNs (nome da entidade de serviço), que os invasores tentam, então, obter tíquetes do TGS (servidor de concessão de tíquete).

- **Aprimoramento do recurso: Alerta de reconhecimento de enumeração de conta (NTLM)**  
Alerta aprimorado de **reconhecimento de enumeração de conta (NTLM)** usando a análise adicional e a lógica de detecção aprimorada para reduzir os resultados de alertas **B-TP** e **FP**.

- **Aprimoramento do recurso: Alerta de reconhecimento de mapeamento de rede (DNS)**  
Novos tipos de detecções adicionados aos alertas de reconhecimento de mapeamento de rede (DNS). Além de detectar solicitações suspeitas de AXFR, agora o ATP do Azure detecta tipos de suspeitos de solicitações originadas de servidores não DNS usando uma quantidade excessiva de solicitações.

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-266"></a>ATP do Azure versão 2.66

Lançado em 17 de fevereiro de 2019

- **Aprimoramento do recurso: alerta Suspeita de ataque de DCSync (replicação de serviços de diretório)**  
Foram feitas melhorias de usabilidade nesse alerta de segurança, inclusive uma descrição revisada, fornecimento de informações de origem adicionais, novo infográfico e mais evidências.
Saiba mais sobre os alertas de segurança [Suspeita de ataque de DCSync (replicação de serviços de diretório)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006).

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-265"></a>ATP do Azure versão 2.65

Lançado em 10 de fevereiro de 2019

- **Novo alerta de segurança: Suspeita de ataque de retransmissão de NTLM (conta do Exchange) — (versão prévia)**  
O alerta de segurança [Suspeita de ataque de retransmissão de NTLM (conta do Exchange) — versão prévia](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037) do ATP do Azure agora está na versão prévia pública.    Nessa detecção, um alerta de segurança do ATP do Azure é disparado quando o uso de credenciais de conta do Exchange de uma fonte suspeita é identificado. Esses tipos de ataques tentam utilizar técnicas de retransmissão do NTLM para obter privilégios do Exchange do controlador de domínio e são conhecidos como **ExchangePriv**. Saiba mais sobre a técnica **ExchangePriv** do [comunicado ADV190007](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/ADV190007) publicado pela primeira vez em 31 de janeiro de 2019 e a [resposta do alerta do ATP do Azure](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/How-to-win-the-latest-security-race-over-NTLM-relay/ba-p/334511).  

- **Disponibilidade geral: Execução remota de código sobre DNS**  
Esse alerta já está em disponibilidade geral. Confira mais informações e recursos de alerta na [página de descrição do alerta Execução remota de código sobre DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036).

- **Disponibilidade geral: Exportação de dados por SMB**  
Esse alerta já está em disponibilidade geral. Confira mais informações e recursos de alerta na [página de descrição do alerta Exportação de dados por SMB](atp-exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030).

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-264"></a>ATP do Azure, lançamento 2.64

Lançado em 4 de fevereiro de 2019

- **Disponibilidade geral: Suspeita de uso de Golden Ticket (anomalia de tíquete)**  
Esse alerta já está em disponibilidade geral. Confira mais informações e recursos de alerta na [página de descrição do alerta Suspeita de uso de Golden Ticket (anomalia de tíquete)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032).

- **Aprimoramento do recurso: Reconhecimento de mapeamento de rede (DNS)**  
A lógica de detecção de alerta aprimorada foi implantada para este alerta para reduzir falsos positivos e ruído de alerta. Agora, esse alerta tem um período de aprendizado de oito dias, antes que ele seja disparado pela primeira vez. Para saber mais sobre esse alerta, confira a [página de descrição do alerta "Reconhecimento de mapeamento de rede (DNS)"](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007).

    **Devido ao aprimoramento desse alerta, o método nslookup não deve mais ser usado para testar a conectividade do ATP do Azure durante a configuração inicial.**

- **Aprimoramento do recurso:**  
Esta versão inclui páginas de alerta reprojetadas e novas evidências, fornecendo uma melhor investigação de alertas.
  - [Suspeita de ataque de força bruta (SMB)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)
  - [Página de descrição do alerta Suspeita de uso de Golden Ticket (anomalia de tempo)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)
  - [Suspeita de ataque de Overpass-the-Hash (Kerberos)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)
  - [Suspeita de uso da estrutura de hacker Metasploit](atp-compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)
  - [Suspeita de ataque do ransomware WannaCry](atp-compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-263"></a>ATP do Azure versão 2.63

Lançado em 27 de janeiro de 2019

- **Novo recurso: suporte para floresta não confiável – (versão prévia)**  
O suporte do ATP do Azure para sensores em florestas não confiáveis agora está em versão prévia pública.
Na página **Serviços de diretório** do portal do ATP do Azure, defina conjuntos de credenciais adicionais para permitir que os sensores do ATP do Azure se conectem a diferentes florestas do Active Directory e relatem ao serviço do ATP do Azure. Confira [Várias florestas do ATP do Azure](atp-multi-forest.md) para saber mais.

- **Novo recurso: cobertura do controlador de domínio**  
O ATP do Azure agora fornece informações de cobertura para controladores de domínio monitorados do ATP do Azure.  
Na página **Sensores** do portal do ATP do Azure, veja o número de controladores de domínio não monitorados e monitorados detectados pelo ATP do Azure em seu ambiente. Baixe a lista de controladores de domínio monitorados para análise posterior e para a criação de um plano de ação. Confira o guia de instruções [Monitoramento de controlador de domínio](atp-sensor-monitoring.md) para saber mais.

- **Aprimoramento do recurso: reconhecimento de enumeração de conta**  
Agora, a detecção de reconhecimento de enumeração de conta do ATP do Azure detecta e emite alertas de tentativas de enumeração usando o Kerberos e o NTLM. Antes, a detecção funcionava apenas para tentativas que usavam o Kerberos. Confira [Alertas de reconhecimento do ATP do Azure](atp-reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003) para saber mais.

- **Aprimoramento do recurso: alerta de tentativa de execução remota de código**
  - Todas as atividades de execução remota, como a criação de serviços, a execução de WMI e a nova execução **PowerShell**, foram adicionadas à linha do tempo do perfil do computador de destino. O computador de destino é o controlador de domínio no qual o comando foi executado.
  - A execução do **PowerShell** foi adicionada à lista de atividades de execução remota de código listadas na linha do tempo de alerta do perfil da entidade.
  - Confira [Tentativa de execução remota de código](atp-domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019) para saber mais.  

- **Problema do LSASS do Windows Server 2019 e do ATP do Azure**  
Em resposta aos comentários dos clientes sobre o uso do ATP do Azure com controladores de domínio que executam o Windows Server 2019, esta atualização inclui uma lógica adicional para evitar que o comportamento relatado nos computadores Windows Server 2019 seja disparado. O suporte completo para o sensor do ATP do Azure no Windows Server 2019 está planejado para uma atualização futura do ATP do Azure, no entanto, **não** há suporte para a instalação e a execução do ATP do Azure nos Windows Servers 2019 no momento. Confira [Requisitos do sensor do ATP do Azure](atp-prerequisites.md#azure-atp-sensor-requirements) para saber mais.

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-262"></a>ATP do Azure versão 2.62

Lançado em 20 de janeiro de 2019

- **Novo alerta de segurança: Execução remota de código com DNS – (versão prévia)**  
O alerta de segurança [Execução remota de código sobre DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036) do ATP do Azure está agora na versão prévia pública.    Nessa detecção, um alerta de segurança do ATP do Azure é disparado quando as consultas DNS suspeitas de explorar a vulnerabilidade de segurança [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626) são feitas em um controlador de domínio na rede.

- **Aprimoramento do recurso: Atualização de sensor atrasada por 72 horas**  
Opção alterada para adiar atualizações de sensor, em sensores selecionados por 72 horas (em vez do adiamento anterior de 24 horas), após cada atualização de lançamento do ATP do Azure. Ver [atualização do sensor do ATP do Azure](sensor-update.md) para obter instruções de configuração.

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-261"></a>ATP do Azure versão 2.61

Lançado em 13 de janeiro de 2019

- **Novo alerta de segurança: Exportação de dados por SMB – (versão prévia)**  
O alerta de segurança [Exportação de dados por SMB](atp-exfiltration-alerts.md) do ATP do Azure está agora na versão prévia pública. Os invasores com direitos de administrador de domínio podem comprometer a conta KRBTGT. Usando a conta KRBTGT, os invasores podem criar um TGT (tíquete de concessão de tíquetes) Kerberos que fornece autorização para qualquer recurso.

- **Aprimoramento do recurso: alerta de segurança Tentativa de execução remota de código**  
Uma nova descrição de alerta e uma evidência adicional foram adicionadas para facilitar a compreensão do alerta e melhorar os fluxos de trabalho de investigação.

- **Aprimoramento do recurso: atividades lógicas de consulta DNS**  
Tipos de consulta adicionais foram adicionados às [atividades monitoradas pelo ATP do Azure](monitored-activities.md) incluindo: **TXT**, **MX**, **NS**, **SRV**, **ANY**, **DNSKEY**.

- **Aprimoramento do recurso: suspeita de uso de Golden Ticket (anomalia de tíquete) e suspeita de uso de Golden Ticket (conta inexistente)**  
Uma lógica de detecção aprimorada foi aplicada a ambos os alertas para reduzir o número de alertas FP e entregar resultados mais precisos.

- **Aprimoramento do recurso: documentação de alertas de segurança do ATP do Azure**  
A documentação de alertas de segurança do ATP do Azure foi aprimorada e expandida para incluir descrições de alerta melhores, classificações de alerta mais precisas e explicações de evidência, correção e prevenção. Familiarize-se com o novo design da documentação de alertas de segurança usando os links a seguir:
  - [Alertas de segurança do ATP do Azure](suspicious-activity-guide.md)
  - [Entender os alertas de segurança](understanding-security-alerts.md)
    - [Alertas de fase de reconhecimento](atp-reconnaissance-alerts.md)
    - [Alertas de fase de credencial comprometida](atp-compromised-credentials-alerts.md)
    - [Alertas de fase de movimento lateral](atp-lateral-movement-alerts.md)
    - [Alertas de fase de comprometimento de domínio](atp-domain-dominance-alerts.md)
    - [Alertas da fase de exportação](atp-exfiltration-alerts.md)
  - [Investigar um computador](investigate-a-computer.md)
  - [Investigar um usuário](investigate-a-user.md)

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-260"></a>ATP do Azure versão 2.60

Lançado em 6 de janeiro de 2019

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-259"></a>ATP do Azure versão 2.59

Lançado em 16 de dezembro de 2018

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-258"></a>ATP do Azure versão 2.58

Lançado em 9 de dezembro de 2018

- **Aprimoramento do alerta de segurança: Divisão do alerta da Implementação de Protocolo Incomum**  
A série de alertas de segurança de Implementação de Protocolo Incomum do ATP do Azure que anteriormente compartilhava uma externalId (2002), agora está dividida em quatro alertas distintos, com uma ID externa exclusiva correspondente.

### <a name="new-alert-externalids"></a>Novas externalIds de alerta

> [!div class="mx-tableFixed"]
> |Novo nome do alerta de segurança|Antigo nome do alerta de segurança|ID externa exclusiva|
> |---------|----------|---------|
> |Suspeita de ataque de força bruta (SMB)|Implementação de protocolo incomum (possível uso de ferramentas mal-intencionadas, como a Hydra)|2033
> |Suspeita de ataque de Overpass-the-Hash (Kerberos)|Implementação incomum de protocolo Kerberos (possível ataque de overpass-the-hash)|2002|
> |Suspeita de uso da estrutura de hacker Metasploit|Implementação de protocolo incomum (possível uso das ferramentas de invasão Metasploit)|2034
> |Suspeita de ataque do ransomware WannaCry|Implementação de protocolo incomum (possível ataque do ransomware WannaCry)|2035
> |

- **Nova atividade monitorada: cópia de arquivo pelo SMB**  
A cópia de arquivos usando o SMB agora é uma atividade monitorada e filtrável. Saiba mais sobre quais [atividades o ATP do Azure monitora](monitored-activities.md) e como [filtrar e pesquisar atividades monitoradas](atp-activities-search.md) no portal.

- **Aprimoramento de imagem do caminho de movimento lateral grande**  
Ao visualizar grandes caminhos de movimento lateral, o ATP do Azure agora destaca apenas os nós conectados a uma entidade escolhida, em vez de desfocar os outros nós. Essa alteração apresenta uma melhoria significativa na velocidade de renderização de um LMP grande.

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-257"></a>ATP do Azure versão 2.57

Lançado em 2 de dezembro de 2018

- **Novo alerta de segurança: suspeita de uso de Golden Ticket - anomalia de tíquete (versão prévia)**  
O alerta de segurança [Suspeita de uso de Golden Ticket – anomalia de tíquete](suspicious-activity-guide.md) do ATP do Azure agora está na versão prévia pública.    Os invasores com direitos de administrador de domínio podem comprometer a conta KRBTGT. Usando a conta KRBTGT, os invasores podem criar um TGT (tíquete de concessão de tíquete) Kerberos que fornece autorização para qualquer recurso.

    Esse TGT forjado é chamado de "Golden Ticket" porque permite que os invasores obtenham uma persistência duradoura na rede. Os Golden Tickets forjados desse tipo têm características exclusivas que essa detecção foi projetada para identificar.

- **Aprimoramento do recurso: criação automatizada de instância (workspace) do ATP do Azure**  
A partir de hoje, os *workspaces* do ATP do Azure foram renomeados para *instâncias* do ATP do Azure. O ATP do Azure agora dá suporte a uma instância do ATP do Azure por conta do ATP do Azure. As instâncias de novos clientes são criadas usando o assistente de criação de instância no [portal do ATP do Azure](https://portal.atp.azure.com). Os workspaces existentes do ATP do Azure são convertidos automaticamente em instâncias do ATP do Azure com essa atualização.  

  - Criação de instância simplificada para acelerar a implantação e a proteção usando [Criar sua instância do ATP do Azure](install-atp-step1.md).
  - Todos os aspectos de [conformidade e privacidade de dados](atp-privacy-compliance.md) permanecem iguais.

  Para saber mais sobre as instâncias do ATP do Azure, confira [Criar sua instância do ATP do Azure](install-atp-step1.md).

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-256"></a>ATP do Azure versão 2.56

Lançado em 25 de novembro de 2018

- **Aprimoramento do recurso: caminhos de movimento lateral (LMPs)**  
Mais dois recursos foram adicionados para melhorar as funcionalidades de LMP (caminho de movimento Lateral) do ATP do Azure:

  - O histórico de LMP agora é salvo e pode ser descoberto por entidade e ao usar os relatórios de LMP.
  - Siga uma entidade em um LMP por meio da linha do tempo da atividade e investigue o uso de evidência adicional fornecida para a descoberta de possíveis caminhos de ataque.

  Confira [Caminhos de movimento lateral do ATP do Azure](use-case-lateral-movement-path.md) para saber mais sobre como usar e investigar com LMPs aprimorados.

- **Aprimoramentos de documentação: caminhos de movimento lateral, nomes de alertas de segurança**  
Foram feitas adições e atualizações nos artigos do ATP do Azure que contêm descrições e recursos dos caminhos de movimento lateral. Foi adicionado o mapeamento de nomes para todas as instâncias, dos antigos nomes de alertas de segurança para os novos nomes e externalIds.
  - Confira [Caminhos de movimento lateral do ATP do Azure](use-case-lateral-movement-path.md), [Investigar caminhos de movimento lateral](investigate-lateral-movement-path.md) e [Guia de alerta de segurança](suspicious-activity-guide.md) para saber mais.

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

Para obter detalhes de cada versão anterior do ATP do Azure até (e incluindo) a versão 2.55, confira a [referência de versão do ATP do Azure](atp-release-reference.md).

## <a name="see-also"></a>Consulte Também

- [O que é o Azure Advanced Threat Protection?](what-is-atp.md)
- [Perguntas frequentes](atp-technical-faq.md)
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
