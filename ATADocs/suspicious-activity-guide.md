---
title: Guia de atividades suspeitas do ATA | Microsoft Docs
d|Description: This article provides a list of the suspicious activities ATA can detect and steps for remediation.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/2/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1fe5fd6f-1b79-4a25-8051-2f94ff6c71c1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 8c93f4485998bbb1b2b440f01fed8d96ad4e2842
ms.sourcegitcommit: 7bc04eb4d004608764b3ded1febf32bc4ed020be
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/02/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*


# <a name="introduction"></a>Introdução

O ATA fornece detecção para as várias fases de ataque avançado a seguir: reconhecimento, comprometimento de credenciais, movimentação lateral, elevação de privilégios, predominância de domínio e outros.

As fases na cadeia de extermínio, nas quais o ATA fornece atualmente as detecções, estão realçadas neste diagrama.

![O ATA se concentra na atividade lateral da cadeia de extermínio do ataque](media/attack-kill-chain-small.jpg)

Este artigo fornece detalhes sobre cada atividade suspeita por fase.


## <a name="reconnaissance-using-account-enumeration"></a>Reconhecimento de enumeração de conta

> [!div class="mx-tableFixed"]
|Descrição|Investigação|Recomendação|Severidade|
|------|----|------|----------|
| Ataque de enumeração de conta é uma técnica que os invasores usam para adivinhar nomes de conta diferentes, usando as tentativas de autenticação Kerberos, para descobrir se um usuário existe na rede. Contas adivinhadas com êxito podem ser usadas nas etapas seguintes do ataque. | Examine o computador em questão e tente determinar se há um motivo legítimo pelo qual ele iniciaria tantos processos de autenticação Kerberos. Esses são os processos que tentaram e falham em descobrir várias contas, pois o usuário não existe (erro Client_Principal_Unknown) e tiveram pelo menos uma tentativa de acesso com êxito. <br></br>**Exceções:** essa detecção se baseia em encontrar várias contas não existentes e tentar a autenticação de um único computador. Se um usuário cometer um erro ao digitar manualmente um nome de usuário ou um domínio, a tentativa de autenticação será vista como uma tentativa de fazer logon em uma conta não existente. Servidores de terminal que exigem que muitos usuários façam logon podem ter, legitimamente, uma grande quantidade de tentativas de logon incorretas. |Investigue o processo responsável por gerar essas solicitações.  Para obter ajuda sobre como identificar os processos com base na porta de origem, consulte [Have you ever wanted to see which Windows process sends a certain packet out to network?](https://blogs.technet.microsoft.com/nettracer/2010/08/02/have-you-ever-wanted-to-see-which-windows-process-sends-a-certain-packet-out-to-network/) (Você já tentou ver qual processo do Windows envia um determinado pacote para fora da rede?)|Média|

## <a name="reconnaissance-using-directory-services-enumeration-sam-r"></a>Reconhecimento usando enumeração de serviços de diretório (SAM-R)

> [!div class="mx-tableFixed"]
|Descrição|Investigação|Recomendação|Severidade|
|------|----|------|----------|
O reconhecimento de serviços de diretório é uma técnica usada pelos invasores para mapear a estrutura de diretório e visar contas com privilégios para as etapas posteriores do ataque. O protocolo SAM-R (Remoto do Gerenciador de Conta de Segurança) é um dos métodos usados para consultar o diretório. | Entenda por que o computador em questão está executando o Gerenciador de Contas de Segurança –Remoto (MS-SAMR). Ele está sendo executado de forma anormal, provavelmente consultando entidades confidenciais. <br></br>**Exceções:** essa detecção depende da criação de perfil do comportamento normal dos usuários que fazem consultas do SAM-R e do alerta quando uma consulta anormal é observada. Usuários confidenciais que fazem logon em computadores que não são de sua propriedade podem disparar uma consulta SAM-R que será detectada como anormal, mesmo se for parte do processo de trabalho normal. Normalmente, isso pode acontecer com os membros da equipe de TI. Se isso for marcado como suspeito, mas foi o resultado do uso normal, é porque o comportamento não foi observado anteriormente pelo ATA. | Nesse caso, é recomendável ter um período mais longo de aprendizado e melhor cobertura do ATA no domínio, por floresta do Active Directory.<br></br>[Baixe e execute a ferramenta “SAMRi10”](https://gallery.technet.microsoft.com/SAMRi10-Hardening-Remote-48d94b5b). A ferramenta SAMRi10 foi lançada pela equipe do ATA, que protege seu ambiente contra consultas SAM-R. | Média|

## <a name="reconnaissance-using-dns"></a>Reconhecimento usando DNS


> [!div class="mx-tableFixed"]
|Descrição|Investigação|Recomendação|Severidade|
|------|----|------|----------|
| O servidor DNS contém um mapa de todos os computadores, endereços IP e serviços em sua rede. Essas informações são usadas pelos invasores para mapear sua estrutura de rede e visar computadores interessantes para etapas posteriores no ataque. | Entenda por que o computador em questão está executando uma consulta de zona de transferência completa (AXFR) para obter todos os registros no domínio DNS. <br></br>**Exceções:** essa detecção identifica os servidores não DNS que emitem solicitações de transferência de zona DNS. Há várias soluções de scanner de segurança conhecidas para emitir esses tipos de solicitações para servidores DNS. <br></br>Além disso, verifique se o ATA é capaz de se comunicar através da porta 53 dos Gateways do ATA para os servidores DNS para evitar cenários de falsos positivos.| Limite a transferência de zona escolhendo cuidadosamente quais hosts podem solicitá-la. Para obter mais detalhes, consulte [Protegendo o DNS](https://technet.microsoft.com/library/cc770474(v=ws.11).aspx) e [Lista de verificação: proteger o seu servidor DNS](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx). |Média|

## <a name="reconnaissance-using-smb-session-enumeration"></a>Reconhecimento usando a enumeração da sessão SMB


> [!div class="mx-tableFixed"]
|Descrição|Investigação|Recomendação|Severidade|
|------|----|------|----------|
| A enumeração do protocolo SMB permite que um invasor obtenha informações sobre de quais endereços IP os usuários na rede se conectaram recentemente. Depois que um invasor tiver essas informações, ele poderá usá-la para visar contas específicas e se mover lateralmente na rede. | Entenda por que o computador em questão está executando enumerações de sessão SMB.<br></br>**Exceções:** essa detecção se baseia na suposição de que a enumeração da sessão SMB não tem nenhum uso legítimo em uma rede corporativa, mas algumas soluções de scanner de segurança (como Websense) emitem tais solicitações. | [Use a ferramenta de interromper a rede para proteger seu ambiente](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b) | Média   |

## <a name="brute-force-ldap-kerberos-ntlm"></a>Força bruta (LDAP, Kerberos, NTLM)


> [!div class="mx-tableFixed"]
|Descrição|Investigação|Recomendação|Severidade|
|------|----|------|----------|
| Em um ataque de força bruta, o invasor tenta muitas senhas, esperando eventualmente adivinhar corretamente. O invasor sistematicamente verifica todas as senhas possíveis (ou um grande conjunto de possíveis senhas) até encontrar a correta. Depois que um invasor adivinha a senha correta, ele pode fazer logon na rede como se fosse o usuário. Atualmente o ATA dá suporte à força bruta horizontal (várias contas) usando o protocolo NTLM ou Kerberos e horizontal e vertical (única conta, várias tentativas de senha) usando a associação LDAP simples. | Entenda por que o computador em questão pode estar falhando em autenticar várias contas de usuário (com aproximadamente o mesmo número de tentativas de autenticação para vários usuários) ou por que houve uma grande quantidade de falhas de autenticação para um único usuário. <br></br>**Exceções:** essa detecção depende da criação de perfil do comportamento normal de contas que se autenticarem em diferentes recursos e o alerta é disparado quando um padrão anormal é observado. Esse padrão não é incomum em scripts que autenticam automaticamente, mas podem usar credenciais desatualizadas (ou seja, nome de usuário ou senha errada). | Senhas complexas e longas fornecem o primeiro nível necessário de segurança contra ataques de força bruta. | Média   |

## <a name="sensitive-account-exposed-in-plain-text-authentication-and-service-exposing-accounts-in-plain-text-authentication"></a>Conta confidencial exposta na autenticação de texto sem formatação e serviço que expõe contas na autenticação de texto sem formatação


> [!div class="mx-tableFixed"]
|Descrição|Investigação|Recomendação|Severidade|
|------|----|------|----------|
| Alguns serviços em um computador enviam credenciais de conta em texto sem formatação, mesmo para contas confidenciais. Os invasores monitorando o tráfego podem capturar essas credenciais para fins mal-intencionados. Qualquer senha de texto não criptografado de uma conta confidencial disparará um alerta. | Localize o computador perpetrador e descubra por que ele está usando associações LDAP simples. | Verifique a configuração nos computadores de origem e certifique-se de não usar a associação LDAP simples. Em vez de usar as associações LDAP simples, use LDAP SALS ou LDAPS. Siga a estrutura em camadas de segurança e restrinja o acesso entre as camadas para evitar a elevação de privilégios. | Baixa para serviços expondo, média para contas confidencias |

## <a name="honey-token-account-suspicious-activities"></a>Atividades suspeitas de conta Honey Token


> [!div class="mx-tableFixed"]
|Descrição|Investigação|Recomendação|Severidade|
|------|----|------|----------|
| As contas Honey Token são contas fictícias configuradas para interceptar, identificar e rastrear atividades mal-intencionadas na rede que envolvem essas contas. Essas são contas que não estão em uso e estão inativas em sua rede e se houver atividade repentina de uma conta de honey token, isso pode indicar que um usuário mal-intencionado está tentando usá-la. | Entenda por que uma conta honey token pode estar realizando a autenticação desse computador. | Percorra as páginas de perfil do ATA de outras contas confidenciais (privilegiadas) em seu ambiente para ver se há atividades potencialmente suspeitas. | Média   |

## <a name="unusual-protocol-implementation"></a>Implementação de protocolo incomum


> [!div class="mx-tableFixed"]
|Descrição|Investigação|Recomendação|Severidade|
|------|----|------|----------|
|Os invasores podem usar as ferramentas que implementam protocolos SMB/Kerberos de determinadas maneiras que permite que eles obtenham recursos pela rede. Isso é uma indicação de técnicas mal-intencionadas usadas para ataques over-pass-the-hash ou de força bruta. | Entenda por que o computador em questão usaria um protocolo de autenticação ou SMB de maneira incomum. <br></br>Para determinar se este é um ataque WannaCry, faça o seguinte:<br></br> 1.    Baixe a exportação do Excel da atividade suspeita.<br></br>2.    Abra a guia de atividade de rede e vá para o campo "Json" para copiar os JSONs Smb1SessionSetup e Ntlm relacionados<br></br>3.   Se o Smb1SessionSetup.OperatingSystem for "Windows 2000 2195" e o Smb1SessionSetup.IsEmbeddedNtlm for "true" e se Ntlm.SourceAccountId for "null", então trata-se de um ataque WannaCry.<br></br><br></br>**Exceções:** essa detecção poderá ser disparada em casos raros, quando as ferramentas legítimas são usadas para implementar os protocolos de uma maneira não padrão. Alguns aplicativos de teste de penetração são conhecidos por fazer isso. | Capture o tráfego de rede e identifique o processo que está gerando o tráfego com a implementação de protocolo incomum.| Média|

## <a name="malicious-data-protection-private-information-request"></a>Solicitação de informações privadas para proteção contra dados mal-intencionados


> [!div class="mx-tableFixed"]
|Descrição|Investigação|Recomendação|Severidade|
|------|----|------|----------|
|A DPAPI (API de Proteção de Dados) é usada por vários componentes do Windows para armazenar senhas, chaves de criptografia e outros dados confidencias de forma segura. Os controladores de domínio têm uma chave mestra de backup que pode ser usada para descriptografar todos os segredos criptografados com DPAPI por computadores Windows ingressados no domínio. Os invasores podem usar a chave mestra de backup do domínio do DPAPI para descriptografar todos os segredos nos computadores ingressados no domínio (senhas de navegador, arquivos criptografados etc.).| Entenda por que o computador fez uma solicitação usando essa chamada à API não documentada para a chave mestra da DPAPI.|Leia mais sobre DPAPI em [Windows Data Protection](https://msdn.microsoft.com/library/ms995355.aspx) (Proteção de Dados do Windows).|Alta|

## <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>Suspeita de roubo de identidade com base no comportamento anormal


> [!div class="mx-tableFixed"]
|Descrição|Investigação|Recomendação|Severidade|
|------|----|------|----------|
| Depois de criar um modelo de comportamento (são necessárias pelo menos 50 contas ativas ao longo de três semanas para criar um modelo de comportamento), qualquer comportamento anormal disparará um alerta. O comportamento que não coincide com o modelo criado para uma conta de usuário específica pode apontar para roubo de identidade. | Entenda por que o usuário em questão pode estar se comportando de forma diferente. <br></br>**Exceções:** se o ATA tem apenas parcial cobertura (nem todos os controladores de domínio são roteados para um Gateway do ATA), somente a atividade parcial é aprendida para um usuário específico. Se repentinamente, depois de mais de três semanas, o ATA começar a abranger todo o tráfego, toda a atividade do usuário pode causar o disparo de um alerta. | Verifique se o que ATA está implantado em todos os controladores de domínio. <br></br>1.  Verifique se o usuário tem um novo cargo na organização.<br></br>2.  Verifique se o usuário é um trabalhador sazonal.<br></br>3.  Verifique se o usuário simplesmente retornou após uma ausência longa.| Média para todos os usuários e Alta para usuários confidenciais |


## <a name="pass-the-ticket"></a>Passagem de tíquete (Pass the ticket)


> [!div class="mx-tableFixed"]
|Descrição|Investigação|Recomendação|Severidade|
|------|----|------|----------|
| Um ataque Pass-the-Ticket é uma técnica de movimento lateral em que os invasores roubam um tíquete Kerberos de um computador e usam-no para obter acesso a outro computador, representando uma entidade em sua rede. | Essa detecção depende do uso dos mesmos tíquetes Kerberos em dois ou mais computadores diferentes. Em alguns casos, se seus endereços IP forem alterados rapidamente, o ATA não poderá determinar se os endereços IP diferentes são usados pelo mesmo computador ou por computadores diferentes. Esse é um problema comum pools DHCP subdimensionados (VPN, WiFi etc.) e endereços IP compartilhados (dispositivos NAT). | Siga a estrutura em camadas de segurança e restrinja o acesso entre as camadas para evitar a elevação de privilégios. | Alta     |

## <a name="pass-the-hash"></a>Passagem de hash (Pass the hash)


> [!div class="mx-tableFixed"]
|Descrição|Investigação|Recomendação|Severidade|
|------|----|------|----------|
| Em um ataque Pass the Hash, o invasor se autentica em um servidor remoto ou serviço usando o hash NTLM subjacente da senha de um usuário, em vez da senha de texto sem formatação associada como normalmente é o caso. | Veja se a conta executou alguma atividade anormal no período próximo a esse alerta. | Implemente as recomendações descritas em [Pass the Hash](http://aka.ms/PtH). Siga a estrutura em camadas de segurança e restrinja o acesso entre as camadas para evitar a elevação de privilégios. | Alta|

## <a name="over-pass-the-hash"></a>Excesso de passagem de hash (Over-pass the hash)


> [!div class="mx-tableFixed"]
|Descrição|Investigação|Recomendação|Severidade|
|------|----|------|----------|
| Um ataque Over Pass the Hash explora uma vulnerabilidade da implementação no protocolo de autenticação Kerberos, em que um hash NTLM é usado para criar um tíquete Kerberos, permitindo que um invasor se autentique em serviços na rede sem a senha do usuário. | Downgrade de criptografia: entenda por que a conta em questão pode estar usando RC4 no Kerberos depois que ele aprendeu a usar AES. <br></br>**Exceções:** essa detecção depende da criação de perfil dos métodos de criptografia usados no domínio e do alerta se um método anormal e mais fraco for observado. Em alguns casos, será usado um método de criptografia mais fraco e o ATA o detectará como anormal, embora possa ser parte do processo de trabalho normal (embora raro). Isso pode acontecer quando esse comportamento não foi observado anteriormente pelo ATA. A cobertura melhor do ATA no domínio ajudará. | Implemente as recomendações descritas em [Pass the Hash](http://aka.ms/PtH). Siga a estrutura em camadas de segurança e restrinja o acesso entre as camadas para evitar a elevação de privilégios. | Alta     |

## <a name="privilege-escalation-using-forged-authorization-data-ms14-068-exploit-forged-pac--ms11-013-exploit-silver-pac"></a>Elevação de privilégios usando dados de autorização forjados (exploração de MS14-068 (PAC forjado) / exploração de MS11-013 (PAC Prata))


> [!div class="mx-tableFixed"]
|Descrição|Investigação|Recomendação|Severidade|
|------|----|------|----------|
| As vulnerabilidades conhecidas em versões mais antigas do Windows Server permitem que os invasores manipulem o PAC (Certificado de Atributo Privilegiado), um campo no tíquete Kerberos que contém os dados de autorização do usuário (no Active Directory essa é a associação de grupo), concedendo ao invasor privilégios adicionais. | Verifique se há um serviço especial em execução no computador afetado que pode usar um método de autorização que não seja PAC. <br></br>**Exceções:** em alguns cenários específicos, os recursos implementam seu próprio mecanismo de autorização e podem disparar um alerta no ATA. | Verifique se todos os controladores de domínio com sistemas operacionais até o Windows Server 2012 R2 estão instalados com o [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege) e todos os servidores membros e controladores de domínio até 2012 R2 estão atualizados com o KB2496930. Para obter mais informações, consulte [PAC Prata](https://technet.microsoft.com/library/security/ms11-013.aspx) e [PAC Forjado](https://technet.microsoft.com/library/security/ms14-068.aspx). | Alta     |

## <a name="abnormal-sensitive-group-modification"></a>Modificação anormal de grupo confidencial


> [!div class="mx-tableFixed"]
|Descrição|Investigação|Recomendação|Severidade|
|------|----|------|----------|
|Como parte da fase de elevação de privilégio, os invasores modificam grupos com altos privilégios para obter acesso a recursos confidenciais.| Valide que a alteração do grupo é legítima. <br></br>**Exceções:** a detecção depende da criação de perfil do comportamento normal dos usuários que modificam grupos confidenciais e alertando quando uma alteração anormal é observada. Alterações legítimas podem disparar um alerta quando esse comportamento não foi observado anteriormente pelo ATA. Um período de aprendizado maior e uma melhor cobertura do ATA no domínio ajudarão. | Certifique-se de minimizar o grupo de pessoas que estão autorizadas a modificar grupos confidenciais. Use permissões Just-I-Time, se possível. | Média   |

## <a name="encryption-downgrade---skeleton-key-malware"></a>Downgrade de criptografia – Malware Skeleton Key


> [!div class="mx-tableFixed"]
|Descrição|Investigação|Recomendação|Severidade|
|------|----|------|----------|
| O Skeleton Key é um malware que é executado nos controladores de domínio e permite a autenticação no domínio com qualquer conta sem saber sua senha. Este malware geralmente usa algoritmos de criptografia mais fracos para codificação de senhas do usuário no controlador de domínio. | Downgrade de criptografia: entenda por que a conta em questão pode estar usando RC4 no Kerberos depois que ele aprendeu a usar AES. <br></br>**Exceções:** essa detecção depende da criação de perfil dos métodos de criptografia usados no domínio. Em alguns casos, será usado um método de criptografia mais fraco e o ATA o detectará como anormal, embora seja parte do processo de trabalho normal (embora raro). | Você pode verificar se a Skeleton Key afetou os controladores de domínio usando [o scanner gravado pela equipe do ATA](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73). | Alta |

## <a name="golden-ticket"></a>Golden ticket


> [!div class="mx-tableFixed"]
|Descrição|Investigação|Recomendação|Severidade|
|------|----|------|----------|
| Se um invasor tiver direitos de administrador de domínio, ele pode criar um TGT (Tíquete de Concessão de Tíquete) Kerberos que fornece autorização para todos os recursos na rede e define o tempo de expiração do tíquete para quando escolher. Isso permite que os invasores obtenham persistência na rede. | Downgrade de criptografia: entenda por que a conta em questão pode estar usando RC4 no Kerberos depois que ele aprendeu a usar AES. <br></br>**Exceções:** essa detecção depende da criação de perfil dos métodos de criptografia usados no domínio e do envio de um alerta quando um método anormal e mais fraco for observado. Em alguns casos, será usado um método de criptografia mais fraco e o ATA o detectará como anormal, mesmo que seja parte do processo de trabalho normal (embora raro). Isso pode acontecer quando esse comportamento não foi observado anteriormente pelo ATA. Verifique se que o ATA tem cobertura completa do seu domínio. | Mantenha a chave mestra do Tíquete de Concessão de Tíquete Kerberos da chave mestra (KRBTGT) o mais segura possível, das seguintes maneiras:<br></br>1.  Segurança física<br></br>2.  Segurança física para máquinas virtuais<br></br>3. Execute a proteção do controlador de domínio<br></br>4.  Credential Guard/Isolamento de LSA (Autoridade de Segurança Local)<br></br>Se forem detectados golden tickets, será necessário realizar uma investigação mais profunda para avaliar se a recuperação tática será necessária.<br></br>Altere o Tíquete de Concessão de Tíquete Kerberos da chave mestra (KRBTGT) duas vezes regularmente de acordo com as diretrizes no [Blog da Microsoft, KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (Agora os scripts de redefinição de senha de conta KRBTGT estão disponíveis para clientes), usando a [ferramenta Reset the krbtgt account password/keys](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). <br></br>Implemente essas [recomendações de pass the hash](http://aka.ms/PtH). | Média   |



## <a name="remote-execution"></a>Execução remota


> [!div class="mx-tableFixed"]
|Descrição|Investigação|Recomendação|Severidade|
|------|----|------|----------|
| Os invasores que comprometeram credenciais de administrador podem executar comandos remotos no controlador de domínio. Isso pode ser usado para obter a persistência, coletar informações, ataques DOS (negação de serviço) ou qualquer outro motivo. | Descubra se a conta em questão tem permissão para realizar essa execução remota em seu controlador de domínio. <br></br>**Exceções:** usuários legítimos que, às vezes, executam comandos no controlador de domínio podem disparar esse alerta, embora isso faça parte do processo normal de administração. Isso é mais comum para membros da equipe de TI ou contas de serviço que executam tarefas administrativas nos controladores de domínio. | Restrinja o acesso remoto aos controladores de domínio de computadores que não são da camada 0. Exclua todos os arquivos e pastas suspeitos, obsoletos e desnecessários. Implemente políticas de UAC (Controle de Conta de Usuário) fortes. Implemente [PAW](https://technet.microsoft.com/en-us/windows-server-docs/security/securing-privileged-access/securing-privileged-access) para permitir que apenas computadores protegidos se conectem aos controladores de domínio para administração. | Baixo      |

## <a name="malicious-replication-requests"></a>Solicitações de replicação mal-intencionada


> [!div class="mx-tableFixed"]
|Descrição|Investigação|Recomendação|Severidade|
|------|----|------|----------|
| A replicação do Active Directory é o processo pelo qual as alterações feitas em um controlador de domínio são sincronizadas com todos os outros controladores de domínio no domínio ou floresta que armazenam cópias dos mesmos dados. Dada a permissão apropriada, um invasor pode iniciar uma solicitação de replicação como se fosse um controlador de domínio, permitindo que o invasor recupere os dados armazenados no Active Directory, incluindo hashes de senha. | Entenda por que o computador pode estar usando a API de replicação do controlador de domínio. Essa detecção depende do ATA usar a partição de configuração da floresta do diretório para entender se um computador é um controlador de domínio. <br></br>**Exceções:** a sincronização de diretório do Azure AD pode fazer com que esse alerta seja disparado. | Valide as seguintes permissões: – Replicar alterações de diretório <br></br>– Replicar todas as alterações de diretório<br></br>Para obter mais informações, consulte [Conceder permissões do Active Directory Domain Services para sincronização de perfil no SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx)<br></br>Você pode utilizar o [Scanner ACL do AD](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) ou criar um script do PowerShell para determinar quem no domínio tem essas permissões. | Média   |



## <a name="broken-trust-between-domain-and-computers"></a>Confiança quebrada entre domínio e computadores


> [!div class="mx-tableFixed"]
|Descrição|Investigação|Recomendação|Severidade|
|------|----|------|----------|
| Confiança quebrada significa que os requisitos de segurança do Active Directory podem não estar em vigor. Isso é geralmente considerado uma falha de conformidade e segurança de linha de base e um alvo fácil para os invasores. Isso disparará um alerta no ATA se mais de cinco falhas de autenticação do Kerberos consecutivas forem observadas de uma conta de computador no período de 24 horas. Como o computador não está se comunicando com o controlador de domínio, (1) não tem uma política de grupo atualizada e (2) o logon é limitado às credenciais em cache. | Verifique se a confiança do computador com o domínio está íntegra verificando os logs de eventos. | Ingresse o computador no domínio se necessário ou redefina a senha do computador. | Baixo      |

## <a name="massive-object-deletion"></a>Exclusão de objeto grande


> [!div class="mx-tableFixed"]
|Descrição|Investigação|Recomendação|Severidade|
|------|----|------|----------|
| O ATA gera esse alerta quando mais de 5% de todas as contas são excluídas. Isso requer o acesso de leitura para o contêiner do item excluído. | Entenda por que 5% de todas as suas contas foram excluídas repentinamente. | Remova as permissões para usuários que podem excluir contas no Active Directory. Para obter mais detalhes, consulte [View or Set Permissions on a Directory Object](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx) (Exibir ou definir permissões em um objeto de diretório). | Baixo |

## <a name="see-also"></a>Consulte Também
- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Investigando ataques de PAC forjado](use-case-forged-pac.md)
- [Solução de erros conhecidos do ATA](troubleshooting-ata-known-errors.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
