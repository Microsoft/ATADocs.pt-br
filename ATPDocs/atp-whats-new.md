---
title: Novidades no ATP do Azure (Proteção Avançada contra Ameaças do Azure) | Microsoft Docs
description: Este artigo é atualizado com frequência para que você conheça as novidades da versão mais recente do ATP do Azure (Proteção Avançada Contra Ameaças do Azure).
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/22/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 7d0f33db-2513-4146-a395-290e001f4199
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: d322c9b0352319e8511414e042d340acbbccd371
ms.sourcegitcommit: 4b89831dc3f17e594c0c824f94f6d2debb07c516
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2019
ms.locfileid: "71997561"
---
# <a name="whats-new-in-azure-advanced-threat-protection-azure-atp"></a>Novidades no ATP do Azure (Proteção Avançada contra Ameaças do Azure)

Este artigo é atualizado com frequência para mantê-lo informado das novidades na última versão do ATP do Azure.

RSS feed: receba uma notificação quando esta página for atualizada copiando e colando a seguinte URL em seu leitor de feeds: `https://docs.microsoft.com/api/search/rss?search=%22This+article+is+updated+frequently+to+let+you+know+what%27s+new+in+the+latest+release+of+Azure+ATP%22&locale=en-us`

Lançado em 6 de outubro de 2019
## <a name="azure-atp-release-297"></a>ATP do Azure versão 2.97

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.


Lançado em 22 de setembro de 2019
## <a name="azure-atp-release-296"></a>ATP do Azure versão 2.96

- **Dados de autenticação NTLM aprimorados usando o evento 8004 do Windows**<br>

Os sensores da ATP do Azure agora podem ler e enriquecer automaticamente as atividades de autenticações NTLM com seus dados de servidor acessados quando a auditoria NTLM está habilitada e o evento 8004 do Windows está ativado. A ATP do Azure analisa o evento 8004 do Windows para autenticações NTLM a fim de enriquecer os dados de autenticação NTLM usados para análise de ameaças e alertas da ATP do Azure. Esse recurso avançado fornece atividade de acesso a recursos sobre dados NTLM, bem como atividades de logon com falha aprimoradas, incluindo o computador de destino que o usuário tentou, mas falhou ao acessar.

Saiba mais sobre as atividades de autenticação NTLM [usando o evento 8004 do Windows](configure-windows-event-collection.md##ntlm-authentication-using-windows-event-8004).

- A versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.


Lançado em 15 de setembro de 2019
## <a name="azure-atp-release-295"></a>ATP do Azure versão 2.95

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.


Lançado em 8 de setembro de 2019

## <a name="azure-atp-release-294"></a>ATP do Azure versão 2.94

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.


Lançado em 1º de setembro de 2019

## <a name="azure-atp-release-293"></a>ATP do Azure versão 2.93

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.

Lançado em 25 de agosto de 2019

## <a name="azure-atp-release-292"></a>ATP do Azure versão 2.92

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.

Lançado em 18 de agosto de 2019

## <a name="azure-atp-release-291"></a>ATP do Azure versão 2.91

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.

Lançado em 11 de agosto de 2019

## <a name="azure-atp-release-290"></a>ATP do Azure versão 2.90

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.

Lançado em 4 de agosto de 2019

## <a name="azure-atp-release-289"></a>ATP do Azure versão 2.89

- **Aprimoramentos do método do sensor**<br>Para evitar o excesso de geração de tráfego NTLM na criação de avaliações de LMP (Caminho de Movimento Lateral) precisas, foram feitas melhorias nos métodos do sensor do ATP do Azure para confiar menos no uso do NTLM e fazer um uso mais significativo do Kerberos.  

- **Melhoria de alerta: uso suspeito do Golden Ticket (conta inexistente)**<br>Foram adicionadas alterações de nome SAM aos tipos de evidência de suporte listados neste tipo de alerta. Para saber mais sobre o alerta, incluindo como evitar e corrigir esse tipo de atividade, confira [Uso suspeito do Golden Ticket (conta inexistente)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027).

- **Disponibilidade geral: suspeita de violação da autenticação NTLM**<br> O alerta de [Suspeita de violação da autenticação NTLM](atp-lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039) não está mais no modo de versão prévia e agora está disponível para o público em geral. 

- Essa versão inclui melhorias e correções de bugs da infraestrutura do sensor interno.


Lançado em 28 de julho de 2019

## <a name="azure-atp-release-288"></a>ATP do Azure versão 2.88 

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

Lançado em 21 de julho de 2019

## <a name="azure-atp-release-287"></a>ATP do Azure versão 2.87 

- **Aprimoramento do recurso: Coleta de eventos de syslog automatizada para sensores autônomos do ATP do Azure**<br> As conexões de syslog de entrada para sensores autônomos do ATP do Azure agora são totalmente automatizadas, enquanto a opção de alternância é removida da tela de configuração. Essas alterações não têm nenhum efeito nas conexões de syslog de saída. 

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-286"></a>ATP do Azure versão 2.86 

Lançado em 14 de julho de 2019

- **Novo alerta de segurança: suspeita de violação da autenticação NTLM (ID externa 2039)**<br>
O novo alerta de segurança de [suspeita de violação de autenticação do NTLM](atp-lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039) do ATP do Azure agora está em versão prévia pública. <br> Nessa detecção, um alerta de segurança do ATP do Azure é disparado quando há suspeita de que o uso de um ataque man-in-the-middle tenha ignorado com êxito a MIC (verificação de integridade da mensagem) do NTLM, uma vulnerabilidade de segurança detalhada no Microsoft [CVE-2019-040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040). Esses tipos de ataques tentam fazer downgrade dos recursos de segurança do NTLM e se autenticam com êxito, com a meta final de fazer movimentos laterais bem-sucedidos. 

- **Aprimoramento do recurso: Identificação do sistema operacional do dispositivo aprimorado**<br> Até agora, o ATP do Azure forneceu informações do sistema operacional do dispositivo de entidade com base no atributo disponível no Active Directory. Anteriormente, se as informações do sistema operacional não estavam disponíveis no Active Directory, elas também não ficavam disponíveis nas páginas de entidade do ATP do Azure. Desta versão em diante, graças ao uso dos métodos de identificação de sistema operacional de dispositivo aprimorado, o ATP do Azure agora fornece essas informações para dispositivos em que o Active Directory não tem as informações ou que não estão registrados no Active Directory. 
 
    A adição dos dados de identificação de sistema operacional de dispositivo aprimorado ajuda a identificar dispositivos não registrados e não Windows, auxiliando simultaneamente em seu processo de investigação. Para saber mais sobre a resolução de nomes de rede no ATP do Azure, confira [Noções básicas sobre a NRR (resolução de nomes de rede)](atp-nnr-policy.md).  

- **Novo recurso: Proxy autenticado – versão prévia**<br> O ATP do Azure agora é compatível com proxy autenticado. Especifique a URL do proxy usando a linha de comando do sensor e especifique o nome de usuário/senha para usar proxies que exigem autenticação. Para obter mais informações sobre como usar o proxy autenticado, confira [Configurar o proxy](https://docs.microsoft.com/azure-advanced-threat-protection/configure-proxy#configure-the-proxy).

- **Aprimoramento do recurso: Processo sincronizador de domínio automatizado**<br> O processo de designação e marcação de controladores de domínio como candidatos do sincronizador de domínio durante a instalação e a configuração contínua agora é totalmente automatizado. A opção de alternância para selecionar manualmente os controladores de domínio como candidatos do sincronizador de domínio foi removida. 

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-285"></a>ATP do Azure versão 2.85

Lançado em 7 de julho de 2019

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-284"></a>ATP do Azure versão 2.84

Lançado em 1º de julho de 2019

- **Suporte a novo local: data center do Azure no Reino Unido**<br>
    Agora as instâncias do ATP do Azure são compatíveis com o data center do Azure no Reino Unido. Para saber mais como criar instâncias do ATP do Azure e seus locais de data center correspondentes, confira a [Etapa 1 da instalação do ATP do Azure](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step10).

- **Aprimoramento do recurso: novo nome e recursos para o alerta Adições suspeitas a grupos confidenciais (ID externa 2024)**<br> 
    O alerta **Adições suspeitas a grupos confidenciais** era denominado alerta **Modificações suspeitas modificações em grupos confidenciais**. A ID externa do alerta (ID 2024) permanece a mesma. A alteração do nome descritivo reflete com maior precisão a finalidade dos alertas em adições aos seus grupos **confidenciais**. O alerta aprimorado também conta com novas evidências e descrições aprimoradas. Para saber mais, confira [Adições suspeitas a grupos confidenciais](https://docs.microsoft.com/azure-advanced-threat-protection/atp-domain-dominance-alerts#suspicious-additions-to-sensitive-groups-external-id-2024).  

- **Nova documentação: guia para migrar do Advanced Threat Analytics para o ATP do Azure**<br>
    Este novo artigo inclui pré-requisitos, diretrizes de planejamento e etapas de configuração e verificação para migrar do ATA para o serviço de ATP do Azure. Para saber mais, confira [Migrar do ATA para o ATP do Azure](https://docs.microsoft.com/azure-advanced-threat-protection/ata-atp-move-overview).   

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-283"></a>ATP do Azure versão 2.83

Lançado em 23 de junho de 2019

- **Aprimoramento do recurso: alerta Criação de serviço suspeito (ID externa 2026)**<br> 
    Este alerta agora conta com uma página de alerta aprimorada com evidência adicional e uma nova descrição. Para saber mais, confira [Alerta de segurança da criação de serviço suspeito](https://docs.microsoft.com/azure-advanced-threat-protection/atp-domain-dominance-alerts#suspicious-service-creation-external-id-2026).

-  **Suporte à nomenclatura de instância: suporte adicionado para prefixo de domínio de apenas dígitos**<br>
    Suporte adicionado para criação de instâncias do ATP do Azure usando prefixos de domínio inicial que contêm apenas dígitos. Por exemplo, agora há suporte ao uso de prefixos de domínio inicial de apenas dígitos como 123456.contoso.com. 

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.


## <a name="azure-atp-release-282"></a>ATP do Azure versão 2.82

Lançado em 18 de junho de 2019

- **Nova versão prévia pública**<br>
A experiência de investigação de ameaça de identidade do ATP do Azure agora está em **Versão prévia pública** e está disponível para todos os locatários protegidos do ATP do Azure. Confira [Experiência de investigação do Microsoft Cloud App Security do ATP do Azure](atp-mcas-integration.md) para saber mais. 

- **Disponibilidade geral**<br>
O suporte do ATP do Azure para florestas não confiáveis está agora em disponibilidade geral. Confira [Várias florestas do ATP do Azure](atp-multi-forest.md) para saber mais. 

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-281"></a>Azure ATP versão 2.81

Lançado em 10 de junho de 2019

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-280"></a>ATP do Azure versão 2.80

Lançado em 2 de junho de 2019

- **Aprimoramento do recurso: Alerta de conexão VPN suspeita**<br>
   Esse alerta agora inclui evidência aprimorada e textos para melhor utilização. Para obter mais informações sobre os recursos de alerta e as etapas de correção e prevenção sugeridas, confira a [Descrição do alerta de conexão VPN suspeita](atp-compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025).

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-279"></a>Azure ATP versão 2.79
Lançado em 26 de maio de 2019

- **Disponibilidade geral: Reconhecimento de entidade de segurança (LDAP) (ID 2038 externa)**

    Esse alerta já está em disponibilidade geral. Para obter mais informações sobre o alerta, os recursos do alerta e a correção e prevenção sugeridas, confira a [descrição do alerta Reconhecimento de entidade de segurança (LDAP)](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-278"></a>ATP do Azure versão 2.78

Lançado em 19 de maio de 2019

- **Aprimoramento do recurso: entidades confidenciais**<br> Marcação Confidencial Manual para Servidores Exchange

    Agora você pode marcar manualmente entidades como Servidores Exchange durante a configuração.

    Para marcar manualmente uma entidade como um Servidor Exchange:
    1. No portal do ATP do Azure, acesse o menu **Configuração**.
    2. Em **Detecção**, escolha **Marcas de entidade** e, em seguida, escolha **Confidencial**.
    3. Escolha **Exchange Servers** e, em seguida, adicione a entidade que você deseja marcar.

    Depois de marcar um computador como um Exchange Server, ele será marcado como Confidencial e exibirá que foi marcado como um Servidor Exchange.  A marcação Confidencial será exibida no perfil da entidade do computador e o computador será analisado em todas as detecções baseadas em contas confidenciais e Caminhos de Movimentação Lateral.

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-277"></a>ATP do Azure versão 2.77

Lançado em 12 de maio de 2019

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-276"></a>ATP do Azure versão 2.76

Lançada em 6 de maio de 2019

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-275"></a>ATP do Azure versão 2.75

Lançada em 28 de abril de 2019

- **Aprimoramento do recurso: entidades confidenciais**<br> A partir desta versão (2.75), os computadores identificados como servidores do Exchange pelo ATP do Azure serão marcados automaticamente como **Confidenciais**.  

    As entidades marcadas automaticamente como **Confidenciais** por funcionarem como servidores do Exchange listam essa classificação como o motivo pelo qual são marcadas. 

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-274"></a>ATP do Azure versão 2.74

Lançamento em 14 de abril de 2019

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-273"></a>ATP do Azure versão 2.73

Lançamento em 10 de abril de 2019

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-272"></a>ATP do Azure, versão 2.72

Lançada em 31 de março de 2019

- **Aprimoramento do recurso: profundidade com escopo do LMP (caminho de movimento lateral)**<br>
Os LMPs (caminhos de movimento lateral) são um método fundamental para a descoberta de ameaças e riscos no ATP do Azure. Para ajudar a manter o foco em riscos críticos para os usuários mais confidenciais, essa atualização torna mais fácil e rápido analisar e corrigir riscos para esses usuários em cada LMP, limitando o escopo e a profundidade de cada gráfico exibido.   

    Confira os [caminhos de movimento lateral](use-case-lateral-movement-path.md) para saber mais sobre como a ATP do Azure usa os LMPs para expor riscos de acesso a cada entidade em seu ambiente.   

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-271"></a>ATP do Azure versão 2.71

Lançado em 24 de março de 2019

- **Aprimoramento do recurso: Alertas de monitoramento da Resolução de nomes de rede (NNR)**<br>
Os alertas de monitoramento foram adicionados para níveis de confiança associados aos alertas de segurança do ATP do Azure que se baseiam na NNR. Cada alerta de monitoramento inclui recomendações detalhadas e acionáveis para ajudar a resolver as baixas taxas de sucesso da NNR. 

    Saiba mais sobre como o ATP do Azure usa a NNR e por que ela é importante para a precisão do alerta em [O que é a Resolução de nomes da rede](atp-nnr-policy.md). 

- **Suporte do servidor: suporte adicionado para o Server 2019 com uso de KB4487044**<br>
Suporte adicionado para o uso do Windows Server 2019, com um nível de patch de KB4487044. Não há suporte para o uso do Server 2019 sem o patch, que é bloqueado a partir desta atualização. 

- **Aprimoramento do recurso: exclusão de alerta com base no usuário**<br>
As opções estendidas de exclusão de alerta agora permitem a exclusão de usuários específicos de alertas específicos. As exclusões podem ajudar a evitar situações em que o uso ou a configuração de certos tipos de software interno disparavam repetidamente alertas de segurança benignos.

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-270"></a>ATP do Azure versão 2.70
Lançado em 17 de março de 2019

- **Aprimoramento do recurso: nível de confiança de NNR (Resolução de Nomes de Rede) adicionado a vários alertas**<br> A NNR (Resolução de Nomes de Rede) é usada para ajudar a identificar positivamente a identidade da entidade de origem das suspeitas de ataque. Adicionando os níveis de confiança de NNR às listas de evidências de alerta do ATP do Azure, agora você pode avaliar e compreender instantaneamente o nível de confiança de NNR relacionado às possíveis origens identificadas e aplicar as correções adequadas. 

    A evidência no nível de confiança de NNR foi adicionada aos seguintes alertas:
  - [Reconhecimento de mapeamento de rede (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)
  - [Suspeita de roubo de identidade (Pass-the-Ticket)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018) 
  - [Suspeita de ataque de retransmissão de NTLM (conta do Exchange) — versão prévia](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)
  - [Suspeita de ataque de DCSync (replicação de serviços de diretório)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)

- **Cenário adicional de alerta de integridade: falha ao iniciar o serviço do sensor do ATP do Azure**<br>Agora, quando o sensor do ATP do Azure não pode ser iniciado devido a um problema de driver de captura de rede, um alerta de integridade do sensor é disparado. Confira [Solução de problemas do sensor do ATP do Azure com logs do ATP do Azure](troubleshooting-atp-using-logs.md), para obter mais informações sobre os logs do ATP do Azure e como usá-los. 
  
- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-269"></a>ATP do Azure versão 2.69
Lançada em 10 de março de 2019

- **Aprimoramento do recurso: Alerta de suspeita de roubo de identidade (Pass-the-Ticket)**<br> Esse alerta agora apresenta nova evidência mostrando os detalhes das conexões feitas usando o protocolo RDP (Área de Trabalho Remota). A evidência adicionada facilita a correção do problema conhecido de alertas benignos verdadeiro positivo (B-TP) causado pelo uso da credencial da Credential Guard remota através de conexões de RDP. 

- **Aprimoramento do recurso: Alerta de execução remota de código sobre DNS**<br> Esse alerta agora apresenta nova evidência mostrando ao seu controlador de domínio as atualizações de status de segurança, informando quando atualizações são necessárias.   

- **Nova documentação: Alerta de segurança do MITRE ATT & CK Matrix™ do ATP do Azure**<br>

    Para explicar e facilitar o mapeamento da relação entre alertas de segurança do ATP do Azure e o MITRE ATT & CK Matrix conhecido, adicionamos as técnicas MITRE relevantes para listagens de alertas de segurança do ATP do Azure. Essa referência adicional facilita o reconhecimento da técnica de ataque suspeito potencialmente em uso quando um alerta de segurança do ATP do Azure é acionado. Saiba mais sobre o [guia de alerta de segurança do ATP do Azure](suspicious-activity-guide.md).  

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-268"></a>Azure ATP versão 2.68
Lançada em 3 de março de 2019

- **Aprimoramento do recurso: Alerta de suspeita de LDAP (ataque de força bruta)**<br>
Foram feitas melhorias de usabilidade consideráveis nesse alerta de segurança, incluindo uma descrição revisada, fornecimento de informações de origem adicionais e detalhes da tentativa de adivinhação para correção mais ágil. Saiba mais sobre alertas de segurança de [Suspeita de LDAP (ataque de força bruta)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004). 

- **Nova documentação: Laboratório de alerta de segurança**<br>

    Para explicar o poder do ATP do Azure na detecção de ameaças reais ao seu ambiente de trabalho, adicionamos um novo **Laboratório de alerta de segurança** a esta documentação. O **Laboratório de alerta de segurança** ajuda você a configurar rapidamente um laboratório ou ambiente de teste, e explica a melhor postura de defesa contra ataques e ameaças comuns e reais.  

    O [laboratório passo a passo](atp-playbook-lab-overview.md) foi projetado para garantir que você gaste o mínimo de tempo criando e o máximo de tempo aprendendo sobre o panorama de ameaças e os alertas e proteção disponíveis no ATP do Azure. Estamos ansiosos para receber seus comentários.

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-267"></a>ATP do Azure versão 2.67
Lançado em 24 de fevereiro de 2019

- **Novo alerta de segurança: Reconhecimento de entidade de segurança (LDAP) - (versão prévia)**<br>

    O alerta de segurança de [Reconhecimento de entidade de segurança (LDAP) – versão prévia](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038) do ATP do Azure está agora em versão prévia pública. <br> Nessa detecção, um alerta de segurança do ATP do Azure é disparado quando o reconhecimento de entidade de segurança é usado pelos invasores para obter informações essenciais sobre o ambiente de domínio. Estas informações ajudam os invasores a mapear a estrutura de domínio, bem como identificar contas privilegiadas para uso em etapas posteriores em sua cadeia de encerramento do ataque. 

    O protocolo LDAP (Lightweight Directory Access Protocol) é um dos métodos mais populares usados para fins legítimos e mal-intencionados para consultar o Active Directory Domain Services. O reconhecimento de entidade de segurança focada no LDAP é normalmente usado como a primeira fase de um ataque Kerberoasting. Os ataques de Kerberoasting são usados para obter uma lista de destino de SPNs (nome da entidade de serviço), que os invasores tentam, então, obter tíquetes do TGS (servidor de concessão de tíquete).

- **Aprimoramento do recurso: Alerta de reconhecimento de enumeração de conta (NTLM)** <br> 
    Alerta aprimorado de **reconhecimento de enumeração de conta (NTLM)** usando a análise adicional e a lógica de detecção aprimorada para reduzir os resultados de alertas **B-TP** e **FP**. 
 
- **Aprimoramento do recurso: Alerta de reconhecimento de mapeamento de rede (DNS)** <br>
    Novos tipos de detecções adicionados aos alertas de reconhecimento de mapeamento de rede (DNS). Além de detectar solicitações suspeitas de AXFR, agora o ATP do Azure detecta tipos de suspeitos de solicitações originadas de servidores não DNS usando uma quantidade excessiva de solicitações.

 - Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-266"></a>ATP do Azure versão 2.66
Lançado em 17 de fevereiro de 2019

- **Aprimoramento do recurso: alerta Suspeita de ataque de DCSync (replicação de serviços de diretório)**<br>
Foram feitas melhorias de usabilidade nesse alerta de segurança, inclusive uma descrição revisada, fornecimento de informações de origem adicionais, novo infográfico e mais evidências. Saiba mais sobre os alertas de segurança [Suspeita de ataque de DCSync (replicação de serviços de diretório)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006). 

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-265"></a>ATP do Azure versão 2.65
Lançado em 10 de fevereiro de 2019

- **Novo alerta de segurança: Suspeita de ataque de retransmissão de NTLM (conta do Exchange) — (versão prévia)**<br>
O alerta de segurança [Suspeita de ataque de retransmissão de NTLM (conta do Exchange) — versão prévia](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037) do ATP do Azure agora está na versão prévia pública. <br> Nessa detecção, um alerta de segurança do ATP do Azure é disparado quando o uso de credenciais de conta do Exchange de uma fonte suspeita é identificado. Esses tipos de ataques tentam utilizar técnicas de retransmissão do NTLM para obter privilégios do Exchange do controlador de domínio e são conhecidos como **ExchangePriv**. Saiba mais sobre a técnica **ExchangePriv** do [comunicado ADV190007](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/ADV190007) publicado pela primeira vez em 31 de janeiro de 2019 e a [resposta do alerta do ATP do Azure](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/How-to-win-the-latest-security-race-over-NTLM-relay/ba-p/334511).  

- **Disponibilidade geral: Execução remota de código sobre DNS**<br>
Esse alerta já está em disponibilidade geral. Confira mais informações e recursos de alerta na [página de descrição do alerta Execução remota de código sobre DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036). 

- **Disponibilidade geral: Exportação de dados por SMB**<br>
Esse alerta já está em disponibilidade geral. Confira mais informações e recursos de alerta na [página de descrição do alerta Exportação de dados por SMB](atp-exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030).


- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-264"></a>ATP do Azure, lançamento 2.64
Lançado em 4 de fevereiro de 2019

- **Disponibilidade geral: Suspeita de uso de Golden Ticket (anomalia de tíquete)**<br>
Esse alerta já está em disponibilidade geral. Confira mais informações e recursos de alerta na [página de descrição do alerta Suspeita de uso de Golden Ticket (anomalia de tíquete)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032). 

- **Aprimoramento do recurso: Reconhecimento de mapeamento de rede (DNS)**<br>
A lógica de detecção de alerta aprimorada foi implantada para este alerta para reduzir falsos positivos e ruído de alerta. Agora, esse alerta tem um período de aprendizado de oito dias, antes que ele seja disparado pela primeira vez. Para saber mais sobre esse alerta, confira a [página de descrição do alerta "Reconhecimento de mapeamento de rede (DNS)"](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007). 

    **Devido ao aprimoramento desse alerta, o método nslookup não deve mais ser usado para testar a conectividade do ATP do Azure durante a configuração inicial.** 

- **Aprimoramento do recurso:**<br>
Esta versão inclui páginas de alerta reprojetadas e novas evidências, fornecendo uma melhor investigação de alertas. 
    - [Suspeita de ataque de força bruta (SMB)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)
    - [Página de descrição do alerta Suspeita de uso de Golden Ticket (anomalia de tempo)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)
    - [Suspeita de ataque de Overpass-the-Hash (Kerberos)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)
    - [Suspeita de uso da estrutura de hacker Metasploit](atp-compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)
    - [Suspeita de ataque do ransomware WannaCry](atp-compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.


## <a name="azure-atp-release-263"></a>ATP do Azure versão 2.63
Lançado em 27 de janeiro de 2019

- **Novo recurso: suporte para floresta não confiável – (versão prévia)**<br>
O suporte do ATP do Azure para sensores em florestas não confiáveis agora está em versão prévia pública. Na página **Serviços de diretório** do portal do ATP do Azure, defina conjuntos de credenciais adicionais para permitir que os sensores do ATP do Azure se conectem a diferentes florestas do Active Directory e relatem ao serviço do ATP do Azure. Confira [Várias florestas do ATP do Azure](atp-multi-forest.md) para saber mais. 

- **Novo recurso: cobertura do controlador de domínio**<br>
O ATP do Azure agora fornece informações de cobertura para controladores de domínio monitorados do ATP do Azure.  
Na página **Sensores** do portal do ATP do Azure, veja o número de controladores de domínio não monitorados e monitorados detectados pelo ATP do Azure em seu ambiente. Baixe a lista de controladores de domínio monitorados para análise posterior e para a criação de um plano de ação. Confira o guia de instruções [Monitoramento de controlador de domínio](atp-sensor-monitoring.md) para saber mais. 

- **Aprimoramento do recurso: reconhecimento de enumeração de conta**<br>
Agora, a detecção de reconhecimento de enumeração de conta do ATP do Azure detecta e emite alertas de tentativas de enumeração usando o Kerberos e o NTLM. Antes, a detecção funcionava apenas para tentativas que usavam o Kerberos. Confira [Alertas de reconhecimento do ATP do Azure](atp-reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003) para saber mais. 

- **Aprimoramento do recurso: alerta de tentativa de execução remota de código**<br>
    - Todas as atividades de execução remota, como a criação de serviços, a execução de WMI e a nova execução **PowerShell**, foram adicionadas à linha do tempo do perfil do computador de destino. O computador de destino é o controlador de domínio no qual o comando foi executado. 
    - A execução do **PowerShell** foi adicionada à lista de atividades de execução remota de código listadas na linha do tempo de alerta do perfil da entidade.
    - Confira [Tentativa de execução remota de código](atp-domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019) para saber mais.  

- **Problema do LSASS do Windows Server 2019 e do ATP do Azure**<br>
Em resposta aos comentários dos clientes sobre o uso do ATP do Azure com controladores de domínio que executam o Windows Server 2019, esta atualização inclui uma lógica adicional para evitar que o comportamento relatado nos computadores Windows Server 2019 seja disparado. O suporte completo para o sensor do ATP do Azure no Windows Server 2019 está planejado para uma atualização futura do ATP do Azure, no entanto, **não** há suporte para a instalação e a execução do ATP do Azure nos Windows Servers 2019 no momento. Confira [Requisitos do sensor do ATP do Azure](atp-prerequisites.md#azure-atp-sensor-requirements) para saber mais. 

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.


## <a name="azure-atp-release-262"></a>ATP do Azure versão 2.62
Lançado em 20 de janeiro de 2019

- **Novo alerta de segurança: Execução remota de código com DNS – (versão prévia)**<br>
O alerta de segurança [Execução remota de código sobre DNS ](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036) do ATP do Azure está agora na versão prévia pública. <br> Nessa detecção, um alerta de segurança do ATP do Azure é disparado quando as consultas DNS suspeitas de explorar a vulnerabilidade de segurança [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626) são feitas em um controlador de domínio na rede.

- **Aprimoramento do recurso: Atualização de sensor atrasada por 72 horas** <br> Opção alterada para adiar atualizações de sensor, em sensores selecionados por 72 horas (em vez do adiamento anterior de 24 horas), após cada atualização de lançamento do ATP do Azure. Ver [atualização do sensor do ATP do Azure](sensor-update.md) para obter instruções de configuração. 


- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-261"></a>ATP do Azure versão 2.61
Lançado em 13 de janeiro de 2019

- **Novo alerta de segurança: Exportação de dados por SMB – (versão prévia)**<br>
O alerta de segurança [Exportação de dados por SMB](atp-exfiltration-alerts.md) do ATP do Azure está agora na versão prévia pública. <br> Os invasores com direitos de administrador de domínio podem comprometer a conta KRBTGT. Usando a conta KRBTGT, os invasores podem criar um TGT (tíquete de concessão de tíquetes) Kerberos que fornece autorização para qualquer recurso. 


- **Aprimoramento do recurso: alerta de segurança Tentativa de execução remota de código** <br> Uma nova descrição de alerta e uma evidência adicional foram adicionadas para facilitar a compreensão do alerta e melhorar os fluxos de trabalho de investigação. 


- **Aprimoramento do recurso: atividades lógicas de consulta DNS** <br>Tipos de consulta adicionais foram adicionados às [atividades monitoradas pelo ATP do Azure](monitored-activities.md) incluindo: **TXT**, **MX**, **NS**, **SRV**, **ANY**, **DNSKEY**. 

- **Aprimoramento do recurso: suspeita de uso de Golden Ticket (anomalia de tíquete) e suspeita de uso de Golden Ticket (conta inexistente)** <br>
Uma lógica de detecção aprimorada foi aplicada a ambos os alertas para reduzir o número de alertas FP e entregar resultados mais precisos.

- **Aprimoramento do recurso: documentação de alertas de segurança do ATP do Azure** <br>
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

- **Aprimoramento do alerta de segurança: Divisão do alerta da Implementação de Protocolo Incomum**<br>
A série de alertas de segurança de Implementação de Protocolo Incomum do ATP do Azure que anteriormente compartilhava uma externalId (2002), agora está dividida em quatro alertas distintos, com uma ID externa exclusiva correspondente. 

### <a name="new-alert-externalids"></a>Novas externalIds de alerta

> [!div class="mx-tableFixed"] 

|Novo nome do alerta de segurança|Antigo nome do alerta de segurança|ID externa exclusiva|
|---------|----------|---------|
|Suspeita de ataque de força bruta (SMB)|Implementação de protocolo incomum (possível uso de ferramentas mal-intencionadas, como a Hydra)|2033
|Suspeita de ataque de Overpass-the-Hash (Kerberos)|Implementação incomum de protocolo Kerberos (possível ataque de overpass-the-hash)|2002|
|Suspeita de uso da estrutura de hacker Metasploit|Implementação de protocolo incomum (possível uso das ferramentas de invasão Metasploit)|2034
|Suspeita de ataque do ransomware WannaCry|Implementação de protocolo incomum (possível ataque do ransomware WannaCry)|2035
|

- **Nova atividade monitorada: cópia de arquivo pelo SMB**<br>
A cópia de arquivos usando o SMB agora é uma atividade monitorada e filtrável. Saiba mais sobre quais [atividades o ATP do Azure monitora](monitored-activities.md) e como [filtrar e pesquisar atividades monitoradas](atp-activities-search.md) no portal. 

- **Aprimoramento de imagem do caminho de movimento lateral grande**<br>
Ao visualizar grandes caminhos de movimento lateral, o ATP do Azure agora destaca apenas os nós conectados a uma entidade escolhida, em vez de desfocar os outros nós. Essa alteração apresenta uma melhoria significativa na velocidade de renderização de um LMP grande. 

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-257"></a>ATP do Azure versão 2.57
Lançado em 2 de dezembro de 2018

- **Novo alerta de segurança: suspeita de uso de Golden Ticket - anomalia de tíquete (versão prévia)**<br>
O alerta de segurança [Suspeita de uso de Golden Ticket – anomalia de tíquete](suspicious-activity-guide.md) do ATP do Azure agora está na versão prévia pública. <br> Os invasores com direitos de administrador de domínio podem comprometer a conta KRBTGT. Usando a conta KRBTGT, os invasores podem criar um TGT (tíquete de concessão de tíquete) Kerberos que fornece autorização para qualquer recurso. 
<br>Esse TGT forjado é chamado de "Golden Ticket" porque permite que os invasores obtenham uma persistência duradoura na rede. Os Golden Tickets forjados desse tipo têm características exclusivas que essa detecção foi projetada para identificar. 


- **Aprimoramento do recurso: criação automatizada de instância (workspace) do ATP do Azure** <br>
A partir de hoje, os *workspaces* do ATP do Azure foram renomeados para *instâncias* do ATP do Azure. O ATP do Azure agora dá suporte a uma instância do ATP do Azure por conta do ATP do Azure. As instâncias de novos clientes são criadas usando o assistente de criação de instância no [portal do ATP do Azure](https://portal.atp.azure.com). Os workspaces existentes do ATP do Azure são convertidos automaticamente em instâncias do ATP do Azure com essa atualização.  

  - Criação de instância simplificada para acelerar a implantação e a proteção usando [Criar sua instância do ATP do Azure](install-atp-step1.md). 
  - Todos os aspectos de [conformidade e privacidade de dados](atp-privacy-compliance.md) permanecem iguais. 

  Para saber mais sobre as instâncias do ATP do Azure, confira [Criar sua instância do ATP do Azure](install-atp-step1.md). 

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-256"></a>ATP do Azure versão 2.56
Lançado em 25 de novembro de 2018


- **Aprimoramento do recurso: caminhos de movimento lateral (LMPs)** <br>
Mais dois recursos foram adicionados para melhorar as funcionalidades de LMP (caminho de movimento Lateral) do ATP do Azure:

  - O histórico de LMP agora é salvo e pode ser descoberto por entidade e ao usar os relatórios de LMP. 
  - Siga uma entidade em um LMP por meio da linha do tempo da atividade e investigue o uso de evidência adicional fornecida para a descoberta de possíveis caminhos de ataque. 

  Confira [Caminhos de movimento lateral do ATP do Azure](use-case-lateral-movement-path.md) para saber mais sobre como usar e investigar com LMPs aprimorados. 

- **Aprimoramentos de documentação: caminhos de movimento lateral, nomes de alertas de segurança**<br> Foram feitas adições e atualizações nos artigos do ATP do Azure que contêm descrições e recursos dos caminhos de movimento lateral. Foi adicionado o mapeamento de nomes para todas as instâncias, dos antigos nomes de alertas de segurança para os novos nomes e externalIds. 
  - Confira [Caminhos de movimento lateral do ATP do Azure](use-case-lateral-movement-path.md), [Investigar caminhos de movimento lateral](investigate-lateral-movement-path.md) e [Guia de alerta de segurança](suspicious-activity-guide.md) para saber mais.   

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-255"></a>ATP do Azure versão 2.55
Lançado em 18 de novembro de 2018

- **Alerta de segurança: comunicação suspeita sobre DNS - disponibilidade geral**<br>
O alerta de segurança de [comunicação suspeita sobre DNS](suspicious-activity-guide.md) da Proteção Avançada contra Ameaças do Azure já está em disponibilidade geral. <br> Normalmente, o protocolo DNS não é monitorado na maioria das organizações e raramente é bloqueado para atividades mal-intencionadas. Isso permite que um invasor em um computador comprometido abuse do protocolo DNS. A comunicação mal-intencionada por DNS pode ser usada para extração, comando e controle de dados e/ou fuga de restrições de rede corporativa.

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-254"></a>ATP do Azure versão 2.54
Lançado em 11 de novembro de 2018

- **Aprimoramento do recurso: exclusões de domínio padrão adicionadas ao alerta de Comunicação suspeita por DNS**<br>   Nova adição de três domínios populares à lista de exclusões de domínio padrão. A lista de exclusões permanece totalmente personalizável. Para saber mais, veja [Excluindo entidades de detecções](excluding-entities-from-detections.md). 

- **Aprimoramentos de documentação: atualização de log do SIEM, diretrizes de problemas conhecidos**<br>    Mapeamento de externalId e explicações adicionais foram adicionados a descrições de log do SIEM. Para saber mais, veja [referência de log do SIEM](cef-format-sa.md). <br>Um artigo adicional para obter diretrizes de problemas conhecidos atualmente não resolvidos foi adicionado. Para saber mais, veja [Problemas conhecidos do ATP do Azure](known-issues.md).  

- Essa versão inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-253"></a>ATP do Azure versão 2.53
Lançado em 4 de novembro de 2018

- **Aprimoramento do alerta de segurança: falhas de autenticação suspeitas**<br>
O [alerta de segurança de falha de autenticação suspeita](suspicious-activity-guide.md) da Proteção Avançada contra Ameaças do Azure agora inclui o monitoramento para detecção de ataques de força bruta de pulverização de senhas.
Em um ataque típico de **pulverização de senhas**, depois de enumerar com êxito uma lista de usuários válidos do controlador de domínio, os invasores tentam UMA senha cuidadosamente concebida em TODAS as contas de usuário conhecidas (uma senha para várias contas). Quando a pulverização de senhas inicial não tem êxito, eles tentam novamente utilizando uma senha diferente cuidadosamente concebida, normalmente após aguardar 30 minutos entre as tentativas. Esse tempo de espera permite que os invasores evitem disparar a maioria dos limites de bloqueio de conta que se baseiam no tempo. A pulverização de senhas tornou-se rapidamente uma técnica de preferência entre os invasores e testadores de intrusão. Os ataques de pulverização de senhas se mostraram eficazes na conquista de uma entrada na organização e por fazer movimentos laterais posteriores, tentando aumentar os privilégios. 

- **Aprimoramento do recurso: enviar uma mensagem de teste do Syslog**<br>   Nova funcionalidade de envio de mensagem de Syslog de teste durante o processo de configuração do SIEM. Saiba mais em [Integração com o Syslog](setting-syslog.md). 

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-252"></a>ATP do Azure versão 2.52
Lançado em 28 de outubro de 2018


- **Aprimoramento do alerta de segurança: tentativa de execução remota de código**<br>
O [alerta de segurança de tentativa de execução remota de código](suspicious-activity-guide.md) do ATP do Azure agora inclui monitoramento para tentativas suspeitas de execução remota de código do PowerShell em seus controladores de domínio. O PowerShell Remoto é um método comum para a execução de comandos administrativos válidos, mas é com frequência usado maliciosamente em uma tentativa de executar scripts em pontos de extremidade remotos. 

- **Aprimoramento do recurso: definir o agendamento de relatórios**
<br>Agora você pode definir uma hora específica para agendar seus relatórios do ATP do Azure usando a função [relatórios](reports.md#). 

- **Adição de configuração: RBAC (Controle de Acesso Baseado em Função)**
<br>Configure as funções de segurança do seu locatário no Centro de administração do AAD (Azure Active Directory) diretamente do novo link de administrador no Portal do ATP do Azure. 

- **Estrutura e conteúdo de documentação revisados**
<br>As recentes alterações de conteúdo para a documentação do ATP do Azure incluem novos artigos, fornecendo uma lista completa de todas as atividades monitoradas do ATP do Azure, instruções de filtragem de atividade, bem como uma reformulação da estrutura de site de documentação para melhor capacidade de utilização:
  - [Atividades monitoradas do ATP do Azure](monitored-activities.md) 
  - [Filtragem de atividades do ATP do Azure](atp-activities-search.md) 
  - [Documentação do ATP do Azure](https://docs.microsoft.com/azure-advanced-threat-protection/)  

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-251"></a>ATP do Azure versão 2.51
Lançado em 21 de outubro de 2018

- Você pode agora habilitar/desabilitar a **integração WD-ATP** na tela [Configuração](integrate-wd-atp.md#how-to-integrate-azure-atp-with-windows-defender-atp) do portal do ATP do Azure. (Para acessar essa funcionalidade, o usuário do ATP do Azure deve ser um Administrador de segurança ou Global no locatário do AAD).

- Essa versão também inclui aprimoramentos e correções de bug da infraestrutura do sensor interno.

## <a name="azure-atp-release-250"></a>Azure ATP versão 2.50
Lançado em 14 de outubro de 2018
- Essa versão inclui correções e melhorias para vários problemas.


## <a name="azure-atp-release-249"></a>Azure ATP versão 2.49
Lançado em 7 de outubro de 2018
-   **Novas detecções: comunicação suspeita de DNS** (versão prévia)<br>Nova detecção adicionada para ajudar a proteger contra ataques de comunicação suspeita de DNS:

    -   Essa detecção ajuda a detectar ataques contra o protocolo DNS. Na maioria das organizações, o protocolo DNS não é monitorado e raramente é bloqueado para atividade mal-intencionada. Permitir que um invasor em um computador comprometido abuse do protocolo DNS. A comunicação mal-intencionada por DNS pode ser usada para extração, comando e controle de dados e/ou fuga de restrições de rede corporativa.

- **Nova funcionalidade** <br>**Função de usuário** do Azure ATP aprimorada com as seguintes funcionalidades:
  - Alterar o status de alertas de segurança (abrir novamente, fechar, excluir, suprimir)
  - Definir relatórios agendados
  - Definir marcas de entidade (confidenciais e honeytoken)
  - Exclusão de detecção
  - Alterar idioma
  - Definir notificações por email ou syslog


- Um aumento temporário no **Reconhecimento usando os alertas de segurança das consultas de serviços de diretório** que ocorreu em 16 de setembro de 2018 foi identificado e resolvido. 

- Essa versão também inclui correções e melhorias para vários problemas.


## <a name="azure-atp-release-248"></a>Azure ATP versão 2.48
Lançado em 16 de setembro de 2018
- **Alerta de segurança:** Reconhecimento usando consultas de serviços de diretório

  Esse alerta de segurança melhorou os infográficos e as evidências. 

- **Excluir entidades de detecções** 

  Para reduzir os falsos positivos, você pode optar por excluir entidades das seguintes detecções: 
  - Conexão VPN suspeita (exclusão de usuário)
  - Promoção do controlador de domínio suspeito (possível ataque DCShadow)
  - Solicitação de replicação suspeita (possível ataque DCShadow)

- Essa versão também inclui correções e melhorias para vários problemas.


## <a name="azure-atp-release-247"></a>ATP do Azure versão 2.47
Lançado em 2 de setembro de 2018

- **Verificação de política de auditoria avançada da ATP do Azure**
 
A Proteção Avançada contra Ameaças agora verifica as políticas de auditoria avançadas existentes de seu controlador de domínio e recomenda alterações de política para fornecer a máxima cobertura do serviço de ATP do Azure para sua organização. 

**Essa nova verificação permite que você:**
  -  Identifique eventos ausentes de seus Logs de Eventos do Windows que atualmente são excluídos da sua cobertura da ATP do Azure.
  -  Verifique se as configurações são as ideais e faça alterações de acordo com as recomendações de alerta de integridade fornecidas.
  -  Será emitido um único alerta de integridade agregado para todos os controladores de domínio, incluindo sugestões de correção (se/conforme necessário).

Revise como [Configurar políticas de auditoria avançadas](atp-advanced-audit-policy.md) para garantir que seu sistema esteja configurado corretamente. 
- Essa versão também inclui correções e melhorias para vários problemas.

## <a name="azure-atp-release-246"></a>Azure ATP versão 2.46

Lançado em 26 de agosto de 2018

- Essa versão inclui correções e melhorias para vários problemas.

## <a name="azure-atp-release-245"></a>Azure ATP versão 2.45

Lançado em 19 de agosto de 2018

- **O Azure ATP adiciona o ETW (Rastreamento de Eventos para Windows) como uma fonte de dados adicional**  <br> O ETW (Rastreamento de Eventos para Windows) é adicionado como fonte de dados adicional, além do tráfego de rede existente e dos eventos do Windows. O ETW fornece detecções de atividades suspeitas adicionais, incluindo: promoções do controlador de domínio suspeitas e solicitações de replicação do controlador de domínio suspeitas (ambas são possíveis ataques DCShadow). <br>
Somente sensores do ATP instalados em controladores de domínio têm suporte detecções baseadas no ETW. As detecções do ETW não têm suporte nos sensores autônomos do ATP. <br>  

- **Quatro novas detecções agora em disponibilidade geral** <br>
  - Conexão de VPN suspeita
  - Golden Ticket do Kerberos – conta não existente 
  - Promoção do controlador de domínio suspeita (possível ataque DcShadow) – detecção baseada no ETW, só disponível nos sensores do ATP 
  - Solicitação de replicação do controlador de domínio suspeita (possível ataque DcShadow) – detecção baseada no ETW, só disponível nos sensores do ATP

- Essa versão também inclui correções e melhorias para vários problemas.


## <a name="azure-atp-release-244"></a>Azure ATP versão 2.44

Lançado em 12 de agosto de 2018

- Essa versão inclui correções e melhorias para vários problemas.
- Os arquivos de log criados no computador do sensor não incluem o log de "Estatística de Exceção".


## <a name="azure-atp-release-243"></a>Azure ATP versão 2.43

Lançamento de 5 de agosto de 2018

- Essa versão inclui correções e melhorias para vários problemas.



## <a name="azure-atp-release-242"></a>Azure ATP versão 2.42

Lançado em 29 de julho de 2018

- Essa versão inclui correções e melhorias para vários problemas. 


## <a name="azure-atp-release-241"></a>Azure ATP versão 2.41

Lançado em 22 de julho de 2018

- **O suporte de várias florestas do Azure ATP está sendo distribuído gradualmente (visualização)** <br> Agora, o ATP do Azure pode dar suporte a organizações com várias florestas, permitindo monitorar a atividade e os perfis de usuário entre florestas. Essa nova funcionalidade permite que você:

  - Exiba e investigue as atividades executadas pelos usuários em várias florestas de um único painel de controle.
  - Melhore a detecção e reduza os falsos positivos, fornecendo integração avançada do Active Directory e a resolução de conta.
  - Obtenha melhores alertas de monitoramento e emissão de relatórios para cobertura entre organizações.


-   **Novas detecções: DCShadow**<br>Duas novas detecções foram adicionadas para ajudar a proteger contra ataques de sombra do controlador de domínio (DCShadow):

    -   Promoção do controlador de domínio suspeito (possível ataque DCShadow) – essa detecção ajuda a detectar ataques nos quais uma máquina representa um controlador de domínio e tenta usar a replicação para propagar alterações em outros controladores de domínio em seu domínio.

    -   Solicitação de replicação suspeita (possível ataque DCShadow) – essa detecção ajuda a proteger contra ataques que tentam executar a promoção DC dos computadores que não são controladores de domínio para alterar objetos do directory.

-   **Informações aprimoradas de downgrade de criptografia**<br>Agora a detecção de downgrade de criptografia fornece mais informações sobre o tipo específico de ataque detectado: overpass-the-hash, golden ticket e skeleton key. Além disso, esses alertas foram agregados para permitir uma investigação mais fácil.
- Essa versão inclui correções e melhorias para vários problemas. 


## <a name="azure-atp-release-240"></a>Azure ATP versão 2.40

Lançado em 15 de julho de 2018

- A detecção de pass-the-ticket agora inclui uma seção de evidências na página de detalhes do alerta. Isso fornece informações adicionais para a investigação do alerta.

- Os sinalizadores de controle de acesso do usuário, que podem ser encontrados no perfil de um usuário nos Dados do diretório, agora incluem uma legenda para permitir um melhor entendimento dos atributos que estão habilitados e desativados.  

## <a name="azure-atp-release-239"></a>Azure ATP versão 2.39

Lançado em 5 de julho de 2018
-   **Nova detecção adicionada: Golden Ticket do Kerberos – conta não existente** (versão prévia)<br>Essa nova detecção ajuda a proteger sua organização contra ataques em que um golden ticket é criado para uma conta que não existe no seu domínio. Para saber mais, confira o [Guia de atividades suspeitas da Proteção Avançada contra Ameaças do Azure](suspicious-activity-guide.md)

- Essa versão inclui correções e melhorias para vários problemas. 


## <a name="azure-atp-release-238"></a>Azure ATP versão 2.38

Lançado em 1º de julho de 2018

- Esta versão inclui correções e aprimoramentos para vários problemas, bem como os aprimoramentos do portal do Azure ATP.

## <a name="azure-atp-release-237"></a>Azure ATP versão 2.37

Lançado em 24 de junho de 2018

- Essa versão inclui correções e melhorias para vários problemas. 

## <a name="azure-atp-release-236"></a>Azure ATP versão 2.36

Lançado em 17 de junho de 2018

- Essa versão inclui correções e melhorias para vários problemas. 


## <a name="azure-atp-release-235"></a>Azure ATP versão 2.35

Lançamento em 10 de junho de 2018
 
- **Novas detecções de versão prévia**<br></br>De agora em diante, a Azure ATP aproveitará o fato de que é um serviço de nuvem, no qual novos recursos podem ser entregues em ciclos rápidos, e fornecerá novas detecções com a maior rapidez possível. Essas novas detecções serão marcadas como "versão prévia" quando forem lançadas pela primeira vez. Normalmente, uma nova detecção passa de versão prévia para disponibilidade geral em poucas semanas. Por padrão, você verá as detecções de versão prévia. Para obter informações de como recusar, confira [detecções de versão prévia](working-with-suspicious-activities.md#preview-detections).
 
- **Detecção de VPN suspeita**<br></br>Esta versão apresenta uma versão prévia da detecção de VPN suspeita. A Azure ATP aprende o comportamento de VPN do usuário, incluindo os computadores aos quais os usuários se conectam e as localizações de onde eles se conectam e alerta você quando há algum desvio do comportamento esperado. Para obter mais informações, confira [Detecção de VPN suspeita](suspicious-activity-guide.md).

- **Atualização atrasada**<br></br>Agora existe a opção de configurar os sensores da Azure ATP para serem atualizados mais tarde, sempre que a Azure ATP for atualizada. Agora é possível configurar cada sensor da Azure ATP para **Atualização atrasada**, para que ele seja atualizado 24 horas depois que o serviço de nuvem Azure ATP for atualizado. Esse recurso permite que você teste a atualização em sensores de teste específicos e apenas atualize os sensores de produção mais tarde. Se você descobrir algum problema durante o primeiro ciclo de atualização, abra um tíquete de suporte. Para obter mais informações, confira [Atualizar sensores da Azure ATP](sensor-update.md).

- **A detecção de implementação de protocolo incomum foi atualizada**<br></br>A detecção de implementação de protocolo incomum agora fornece mais informações. Agora você pode ver qual ferramenta de possível ataque a Azure ATP suspeita que esteja ativa em sua rede. Para obter mais informações, confira o [Guia de atividades suspeitas](suspicious-activity-guide.md).
 
- **Alerta de sensor desatualizado**<br></br>A Azure ATP inclui um novo alerta de monitoramento para informar se um sensor está mais de três versões desatualizado. Se esse alerta aparecer, você deverá atualizar o sensor ou investigar por que o sensor não está sendo atualizado automaticamente. Se o alerta persistir, desinstale e reinstale o sensor.

- Essa versão inclui correções e melhorias para vários problemas. 

## <a name="azure-atp-release-234"></a>Azure ATP versão 2.34

Lançado em 3 de junho de 2018
 
- Essa versão inclui correções e melhorias para vários problemas. 

 
## <a name="azure-atp-release-233"></a>Azure ATP versão 2.33

Lançamento: 27 de maio de 2018

- Recurso de versão prévia: o ATP do Azure agora é compatível com novos idiomas e 13 novas localidades:
    - Tcheco
    - Húngaro
    - Italiano
    - Coreano
    - Holandês
    - Polonês
    - Português (Brasil)
    - Português (Portugal)
    - Rússia
    - Sueco
    - Turco
    - Chinês (China)
    - Chinês (Taiwan)


## <a name="azure-atp-release-232"></a>Azure ATP versão 2.32

Lançado em 13 de maio de 2018
 
- Essa versão inclui correções e melhorias para vários problemas. 

## <a name="azure-atp-release-231"></a>Azure ATP versão 2.31

Lançamento em 6 de maio de 2018
 
- Foram feitas melhorias na resolução de nome. Como parte desse esforço, além da resolução ativa RPC e NetBIOS, o sensor pode emitir um pacote Client Hello TLS para a porta RDP (3389) do ponto de extremidade. 
- Essa versão inclui correções e melhorias para vários problemas. 

## <a name="azure-atp-release-230"></a>Azure ATP versão 2.30

Lançado em 29 de abril de 2018
 
- Agora, as atividades suspeitas de downgrade de criptografia incluem uma seção de evidências que descreve os sintomas detectados pelo Azure ATP e que fazem com que ele suspeite de uma atividade de downgrade de criptografia. 
-   Agora, o Azure ATP usa o Azure Email Orchestrator para todos os emails enviados do Azure ATP, inclusive atividades suspeitas, alertas de monitoramento e relatórios. Você verá que essas notificações de email agora seguem um formato consistente para facilitar o uso e que arquivos do Excel terão um link para download no console.
 
 
## <a name="azure-atp-release-229"></a>Azure ATP versão 2.29

Lançado em 22 de abril de 2018
 
- Essa versão inclui correções e melhorias para vários problemas. 
 
 
## <a name="azure-atp-release-228"></a>Azure ATP versão 2.28

Lançado em 15 de abril de 2018
 
-   Os usuários que são membros dos grupos de funções Usuários do Azure ATP e Visualizadores do Azure ATP agora têm permissões para ver alertas de monitoramento.
- Essa versão inclui correções e melhorias para vários problemas. 


## <a name="azure-atp-release-227"></a>Azure ATP versão 2.27

Lançado em 8 de abril de 2018

- Agora você tem a capacidade de fornecer comentários do usuário na barra de navegação superior. Clicar no Smiley na barra de menu habilita você a enviar um email à equipe da Proteção Avançada contra Ameaças do Azure com seus comentários.

- Essa versão inclui correções e melhorias para vários problemas. 
 

## <a name="azure-atp-release-226"></a>Azure ATP versão 2.26

Lançado em 25 de março de 2018

- Quando o ATP do Azure alerta sobre uma atividade suspeita que você identifica como um positivo benigno (uma ação legítima que não é uma atividade suspeita), você tem a opção de excluir computadores e endereços IP de mais detecções, como: downgrade de criptografia, força bruta de LDAP, PAC forjado, força bruta e Pass-the-hash.
-   O desempenho do sensor do Azure ATP foi aprimorado.
-   Uma nova região foi adicionada para a implantação do Workspace. Agora é possível implantar um workspace na Ásia. 


## <a name="azure-atp-release-225"></a>Azure ATP versão 2.25

Lançada em 18 de março de 2018

- Agora há compatibilidade com a MFA (Autenticação Multifator) no Azure ATP. Os locatários usando MFA agora podem entrar no portal do Azure ATP.
- O Azure ATP agora tem uma página [**Status do sistema**](https://health.atp.azure.com/) para fornecer informações sobre se o Portal de Gerenciamento do workspace está funcionando e ativo, se há problemas com as detecções e se o sensor pode enviar tráfego para a nuvem. Você pode acessar o **Status do sistema** na barra de menus do Azure ATP.


## <a name="azure-atp-release-224"></a>Versão 2.24 do Azure ATP

Lançada em 11 de março de 2018

**Detecções novas e atualizadas**
  - Criação de serviços suspeitos – invasores tentam executar serviços suspeitos na sua rede. Agora, o Azure ATP gera um alerta ao identificar que um novo serviço que parece suspeito está sendo executado por uma pessoa em um computador específico. Essa detecção se baseia em eventos (e não no tráfego de rede) e ocorre em qualquer controlador de domínio da rede que esteja encaminhando o evento 7045 para o Azure ATP. Para saber mais, consulte o [Guia de atividades suspeitas](suspicious-activity-guide.md).

**Investigação aprimorada**
  - O Azure ATP tem um [perfil de entidade](entity-profiles.md) aperfeiçoado. O perfil de entidade oferece uma plataforma projetada para investigações aprofundadas das atividades do usuário – como os recursos acessados, computadores em que fizeram logon, e muito mais. O perfil de entidade também fornece os dados de diretório e permite identificar possíveis caminhos de movimentação lateral de/para a entidade. Assim, é possível saber mais sobre violações em potencial na sua organização.

  - Com o ATP, é possível marcar manualmente as entidades como *confidenciais*, a fim de aperfeiçoar as detecções e o monitoramento. Essa marcação afeta diversas detecções do Azure ATP, como a detecção de modificação de grupos confidenciais e o [caminho de movimentação lateral](use-case-lateral-movement-path.md), que dependem de entidades consideradas confidenciais.

**Novos relatórios para ajudá-lo a investigar**
  - O [relatório de senhas expostas em texto não criptografado](reports.md) permite detectar quando os serviços enviam credenciais de conta em texto sem formatação. Assim, é possível investigar os serviços e aprimorar o nível de segurança da rede. Esse relatório substitui os alertas de atividade suspeita em texto não criptografado.
  - O [relatório de caminhos de movimento lateral para contas confidenciais](reports.md) lista as contas confidenciais que estão expostas por meio de caminhos de movimentação lateral. Dessa forma, é possível reduzir esses caminhos e fortalecer sua rede a fim de minimizar o risco de superfície de ataque. Assim, você pode impedir a movimentação lateral, para que os invasores não se movimentem entre usuários e computadores ao longo da rede até encontrarem o prêmio máximo da segurança virtual: suas credenciais de conta do administrador.

- Agora, é possível acessar facilmente a documentação em um link fornecido com um alerta de atividade suspeita, a fim de exibir as [etapas de investigação a serem seguidas](suspicious-activity-guide.md). 

**Melhorias de desempenho**
 -  A infraestrutura do sensor do Azure ATP teve seu desempenho aprimorado: a exibição agregada do tráfego permite otimizar a CPU e o pipeline de pacotes. Além disso, reutiliza soquetes para os controladores de domínio minimizarem as sessões de SSL para o DC.

## <a name="see-also"></a>Consulte Também
- [O que é o Azure Advanced Threat Protection?](what-is-atp.md)
- [Perguntas frequentes](atp-technical-faq.md)
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
