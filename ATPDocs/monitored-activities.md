---
title: Atividades de domínio monitoradas do ATP do Azure|Microsoft Docs
description: Descreve cada tipo de atividade monitorado pela Proteção Avançada contra Ameaças do Azure
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 01/19/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 37d1a032-65e7-4a89-be0b-c3f9cc2bacdb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: cce0cfab66410b1e13f20a9837b7c55472f4cb3d
ms.sourcegitcommit: 450295f4ee87db835c9921d2595ae9d291f727c5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/20/2020
ms.locfileid: "76281739"
---
# <a name="azure-atp-monitored-activities"></a>Atividades monitoradas do ATP do Azure

> [!NOTE]
> Os recursos do ATP do Azure explicados nesta página também podem ser acessados usando o novo [portal](https://portal.cloudappsecurity.com).

A Proteção Avançada contra Ameaças do Azure monitora informações geradas do Active Directory e das atividades de rede e de eventos da sua organização para detectar atividades suspeitas. As informações de atividades monitoradas permitem que o ATP do Azure ajude a determinar a validade de cada possível ameaça e a realizar a triagem e a responder corretamente.

No caso de uma ameaça válida ou de **verdadeiro positivo**, o ATP do Azure permite que você descubra o escopo da violação de cada incidente, investigue quais entidades estão envolvidas e determine como corrigi-las.

As informações monitoradas pelo ATP do Azure são apresentadas na forma de atividades. O ATP do Azure atualmente dá suporte ao monitoramento dos seguintes tipos de atividade:

> [!NOTE]
>
> - Este artigo é relevante para todos os tipos de sensor do ATP do Azure.
> - As atividades monitoradas do ATP do Azure aparecem na página de perfil do computador e do usuário.

## <a name="monitored-user-activities-user-account-ad-attribute-changes"></a>Atividades do usuário monitoradas: alterações de atributo do AD da conta do usuário

|Atividade monitorada|Descrição|
|---------------------|------------------|
|Estado da Delegação Restrita da Conta Alterado|O estado da conta agora está habilitado ou desabilitado para delegação.|
|SPNs de delegação restrita de conta alterados|A delegação restrita restringe os serviços nos quais um determinado servidor pode agir em nome do usuário.|
|Conta Desabilitada Alterada|Indica se uma conta está desabilitada ou habilitada.|
|Conta Expirada|Data em que a conta expira.|
|Hora da Expiração da Conta Alterada|Alteração na data em que a conta expira.|
|Conta Bloqueada Alterada|Alteração na data em que a conta expira.|
|Senha da Conta Alterada|O usuário alterou a senha.|
|Senha da Conta Expirada|Senha do usuário expirada.|
|Senha da Conta Nunca Expira Alterada|Senha de usuário alterada para nunca expirar.|
|Senha Não Obrigatória da Conta Alterada|A conta de usuário foi alterada e permite fazer logon com uma senha em branco.|
|Cartão Inteligente Obrigatório da Conta Alterada|A conta é alterada para exigir que os usuários façam logon em um dispositivo usando um cartão inteligente.|
|Tipos de Criptografia com Suporte da Conta Alterados|Tipos de criptografia compatíveis com Kerberos foram alterados (tipos: Des, AES 129, AES 256)|
|Nome Upn de Conta Alterado|O nome de entidade do usuário foi alterado.|
|Associação do Grupo Alterada|O usuário adicionou/removeu, de/para um grupo, por outro usuário ou por si só.|
|Email de Usuário Alterado|O atributo de email de usuários foi alterado.|
|Gerenciador de Usuários Alterado|O atributo do gerenciador de usuários foi alterado.|
|Número de Telefone do Usuário Alterado|O número de telefone do usuário foi alterado.|
|Título do Usuário Alterado|O atributo de título do usuário foi alterado.|

<!-- Rollback
|SID-History Changed|Account's SID-History attribute was changed.|
-->

## <a name="monitored-user-activities-ad-security-principal-operations"></a>Atividades do usuário monitoradas: Operações da entidade de segurança do AD

|Atividade monitorada|Descrição|
|---------------------|------------------|
|Entidade de Segurança Criada|A conta foi criada (usuário e computador).|
|Entidade de Segurança Excluída Alterada|A conta foi excluída/restaurada (usuário e computador).|
|Nome de Exibição da Entidade de Segurança Alterado|O nome de exibição da conta foi alterado de X para Y.|
|Nome da Entidade de Segurança Alterado|O atributo de nome da conta foi alterado.|
|Caminho da Entidade de Segurança Alterado|O nome diferenciado da conta foi alterado de X para Y.|
|Nome SAM da Entidade de Segurança Alterado|Nome SAM alterado (SAM é o nome de logon usado para dar suporte a clientes e servidores que executam versões anteriores do sistema operacional).|

## <a name="monitored-user-activities-domain-controller-based-user-operations"></a>Atividades do usuário monitoradas: controlador de domínio com base em operações de usuário

|Atividade monitorada|Descrição|
|---------------------|------------------|
|Replicação do Serviço de Diretório|O usuário tentou replicar o serviço de diretório.|
|Consulta DNS|Tipo de usuário de consulta executado no controlador de domínio (**AXFR**, **TXT**, **MX**, **NS**, **SRV**, **ANY**, **DNSKEY**).|
|Recuperação de Dados Particular|O usuário tentou/conseguiu consultar dados particulares usando o protocolo LSARPC.|
|Criação de Serviço|O usuário tentou criar remotamente de um serviço específico para um computador remoto.|
|Enumeração da Sessão SMB|O usuário tentou enumerar todos os usuários com sessões SMB abertas nos controladores de domínio.|
|Cópia de arquivos SMB|O usuário copiou arquivos usando SMB|
|Consulta SAMR|O usuário executou uma consulta SAMR.|
|Agendamento de Tarefas|O usuário tentou agendar a tarefa X remotamente para um computador remoto.|
|Execução WMI|O usuário tentou executar remotamente um método WMI.|

## <a name="monitored-user-activities-login-operations"></a>Atividades do usuário monitoradas: Operações de logon

|Tipo de logon|Atividade monitorada|Descrição|
|---------------------|---------------------|------------------|
|Tipo de logon 2|Validação de Credenciais|Evento de autenticação de conta de domínio usando os métodos de autenticação NTLM e Kerberos.|
|Tipo de logon 2|Logon interativo|Usuário recebeu acesso à rede ao inserir um nome de usuário e senha (método de autenticação Kerberos).|
|Tipo de logon 2|Conexão VPN|Usuário conectado por VPN – Autenticação usando o protocolo RADIUS.|
|Tipo de logon 3|Acesso de Recurso|O usuário acessou um recurso usando a autenticação Kerberos.|
|Tipo de logon 8|Texto não criptografado LDAP|O usuário autenticou usando o LDAP com uma senha com texto não criptografado (autenticação simples).|
|Tipo de logon 10|Área de Trabalho Remota|O usuário executou uma sessão RDP em um computador remoto usando a autenticação Kerberos.|
|---|Falha no Logon|Falha na tentativa de autenticação da conta de domínio (via NTLM e Kerberos) porque a seguinte conta estava desabilitada/expirada/bloqueada ou usou um certificado não confiável ou devido a horas de logon inválidas/senha antiga/senha expirada/senha errada.|

## <a name="monitored-machine-activities-machine-account"></a>Atividades da máquina monitoradas: conta do computador

|Atividade monitorada|Descrição|
|---------------------|------------------|
|Sistema Operacional do Computador Alterado|Alteração no sistema operacional do computador.

## <a name="see-also"></a>Consulte Também

- [Gerenciando alertas de segurança](working-with-suspicious-activities.md)
- [Guia de alertas de segurança](suspicious-activity-guide.md)
- [Investigar entidades](investigate-entity.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
