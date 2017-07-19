---
title: "Investigando a elevação de privilégios usando ataques de dados de autorização forjados | Microsoft Docs"
description: "Este artigo descreve a elevação de privilégios usando ataques de dados de autorização forjados e fornece instruções de investigação quando essa ameaça é detectada na rede."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/4/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: f3db435e-9553-40a2-a2ad-278fad4f0ef5
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 842e9866c5fdb447f49600501c4486da6db902f2
ms.sourcegitcommit: 4118dd4bd98994ec8a7ea170b09aa301a4be2c8a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*

# <a name="investigating-privilege-escalation-using-forged-authorization-data-attacks"></a>Investigando a elevação de privilégios usando ataques de dados de autorização forjados

A Microsoft constantemente aprimora seus recursos de detecção de segurança e sua capacidade de fornecer inteligência acionável e quase em tempo real para analistas de segurança. O ATA (Advanced Threat Analytics) da Microsoft ajuda a conduzir esta mudança. Se o ATA detectar uma elevação de privilégios usando dados de autorização forjados suspeitos em sua rede e fornecer alertas sobre ela, este artigo o ajudará a compreendê-lo e investigá-lo.

## <a name="what-is-a-privileged-attribute-certificate-pac"></a>O que é um PAC (Certificado de Acesso Privilegiado)?

O PAC (Certificado de Atributos de Privilégio) é a estrutura de dados no Tíquete Kerberos que contém informações de autorização, incluindo associações de grupo, identificadores de segurança e informações de perfil do usuário. Em um domínio do Active Directory, isso permite que os dados de autorização fornecidos pelo DC (Controlador de Domínio) sejam transmitidos para outros servidores membro e estações de trabalho para fins de autenticação e autorização. Além das informações de associação, o PAC inclui informações de credencial adicionais, informações de perfil e política metadados de segurança de suporte. 

A estrutura de dados do PAC é usada pelos protocolos de autenticação (protocolos que verificam identidades) para transportar informações de autorização, que controlam o acesso aos recursos.

### <a name="pac-validation"></a>Validação de PAC

A validação de PAC é um recurso de segurança para impedir que um invasor obtenha acesso não autorizado a um sistema ou seus recursos com um ataque a intermediários, especialmente em aplicativos em que a representação do usuário é utilizada. A representação envolve uma identidade confiável, como uma conta de serviço, que recebe privilégios elevados para acessar recursos e executar tarefas. A validação de PAC reforça um ambiente de autorização mais seguro nas configurações de autenticação de Kerberos em que ocorre a representação. A [validação de PAC](https://blogs.msdn.microsoft.com/openspecification/2009/04/24/understanding-microsoft-kerberos-pac-validation/) garante que um usuário apresente os dados de autorização exatamente como foram concedidos no Tíquete Kerberos e que os privilégios do tíquete não sejam modificados.

Quando a validação de PAC ocorre, o servidor codifica uma mensagem de solicitação que contém o tipo e o comprimento da assinatura de PAC e os transmite para o DC. O DC decodifica a solicitação e extrai a soma de verificação do servidor e os valores da soma de verificação do KDC. Se a conferência da soma de verificação for bem-sucedida, o DC retornará um código de êxito para o servidor. Um código de retorno de falha indica que o PAC foi alterado. 

O conteúdo do PAC Kerberos é assinado duas vezes: 
- Uma vez com a chave mestra do KDC, para impedir que serviços mal intencionados do servidor alterem os dados de autorização
- Uma vez com a chave mestra da conta do servidor de recurso de destino, para impedir que um usuário modifique o conteúdo do PAC e adicione seus próprios dados de autorização

### <a name="pac-vulnerability"></a>Vulnerabilidade de PAC
Os boletins de segurança [MS14-068](https://technet.microsoft.com/library/security/MS14-068.aspx) e [MS11-013](https://technet.microsoft.com/library/security/ms11-013.aspx) apontam as vulnerabilidades no KDC Kerberos que podem permitir que um invasor manipule o campo PAC em um Tíquete Kerberos válido, concedendo privilégios adicionais a si mesmo.

## <a name="privilege-escalation-using-forged-authorization-data-attack"></a>Elevação de privilégios usando ataques de dados de autorização forjada

Um ataque de elevação de privilégios usando dados de autorização forjados é uma tentativa de um invasor tirar proveito das vulnerabilidades do PAC para elevar seus privilégios no seu Domínio ou Floresta do Active Directory. Para realizar esse ataque, o invasor deve:
-   Ter credenciais para um usuário de domínio.
-   Ter conectividade de rede com um Controlador de Domínio que pode ser usado para autenticar as credenciais de domínio comprometidas.
-   Ter as ferramentas certas. O PyKEK (Kit de Exploração de Kerberos do Python) é uma ferramenta conhecida que forjará os PACs.

Se o invasor tiver as credenciais e a conectividade necessárias, ele poderá modificar ou forjar o PAC (Certificado de Atributo Privilegiado) de um token de logon do usuário (TGT) Kerberos existente. O invasor altera a declaração de associação de grupo para incluir um grupo de privilégios elevados (por exemplo, "Administradores de domínio" ou "Administradores de empresa"). O invasor, então, inclui o PAC modificado no Tíquete Kerberos. Esse Tíquete Kerberos, em seguida, é usado para solicitar um Tíquete de serviço do DC (Controlador de Domínio) sem patch, dando ao invasor permissões elevadas no domínio e autorização para executar ações que não deveria. Um invasor pode apresentar o token de logon do usuário (TGT) modificado para acessar qualquer recurso no domínio, solicitando tokens de acesso do recurso (TGS). Isso significa que um invasor pode ignorar todas as ACLs de recursos configuradas que limitam o acesso na rede por meio da falsificação dos dados de autorização (PAC) de qualquer usuário no Active Directory.

## <a name="discovering-the-attack"></a>Descoberta do ataque
Quando o invasor tenta elevar seus privilégios, o ATA o detectará e marcará como um alerta de gravidade alta.

![Atividades suspeitas de PAC forjado](./media/forged-pac.png)

O ATA indicará no alerta de atividade suspeita independentemente de a elevação de privilégios usando dados de autorização forjados ter êxito ou falhar. Tanto os alertas de êxito quanto os de falha devem ser investigados, pois as tentativas frustradas ainda podem indicar a presença de um invasor em seu ambiente.

## <a name="investigating"></a>Investigação
Depois de receber o alerta de elevação de privilégios usando o alerta de dados de autorização no ATA, você precisa determinar o que deve ser feito para mitigar o ataque. Para fazer isso, primeiro você deve classificar o alerta como um dos seguintes: 
-   Verdadeiro positivo: uma ação mal intencionada detectada pelo ATA
-   Falso positivo: um alerta falso – a elevação de privilégios usando dados de autorização forjados não ocorreu na verdade (esse é um evento que o ATA confundiu com um ataque de elevação de privilégios usando dados de autorização forjados)
-   Verdadeiro positivo benigno: uma ação detectada pelo ATA que é real, mas não é mal intencionada, como um teste de penetração

O gráfico a seguir ajuda a determinar quais etapas você deve executar:

![Diagrama de PAC forjado](./media/forged-pac-diagram.png)

1. Primeiro, verifique o alerta no cronograma de ataque do ATA para conferir se a tentativa de autorização forjada teve êxito, falhou ou foi pretendida (os ataques pretendidos também são ataques com falha). As tentativas com êxito e com falha podem resultar em um Positivo Verdadeiro, mas com gravidades diferentes no ambiente.
 
 ![Atividades suspeitas de PAC forjado](./media/forged-pac-sa.png)


2.  Se o ataque de Elevação de privilégios usando dados de autorização forjados tiver tido êxito:
    -   Se o DC no qual o alerta foi gerado corretamente for corrigido, ele será um falso positivo. Nesse caso, você deve ignorar o alerta e enviar um email notificando a equipe do ATA em ATAEval@microsoft.com para melhorar continuamente nossa detecções. 
    -   Se o controlador de domínio no alerta não estiver devidamente corrigido:
        -   Se o serviço listado no alerta não tiver seu próprio mecanismo de autorização, isso será um verdadeiro positivo e você deverá executar o processo de RI (Resposta de Incidente) da sua organização. 
        -   Se o serviço listado no alerta tiver um mecanismo interno de autorização que solicita dados de autorização, ele poderá ser falsamente identificado como um ataque de elevação de privilégios usando dados de autorização forjados. 

3.  Se o ataque detectado tiver falhado:
    -   Se o sistema operacional ou o aplicativo for conhecido por modificar o PAC, esse provavelmente será um verdadeiro positivo benigno e você deverá trabalhar com o proprietário do aplicativo ou do sistema operacional para corrigir esse comportamento.

    -   Se o sistema operacional ou o aplicativo não for conhecido por modificar o PAC: 

        -   Se o serviço listado não tiver seu próprio serviço de autorização, isso será um verdadeiro positivo e você deverá executar o processo de RI (Resposta de Incidente) da sua organização. Mesmo que o invasor não tenha êxito ao elevar seus privilégios no domínio, você pode assumir que há um invasor em sua rede e vai querer localizá-lo assim que possível, antes que ele tente outros ataques persistentes avançados conhecidos para elevar seus privilégios. 
        -   Se o serviço listado no alerta tiver seu próprio mecanismo de autorização que solicita dados de autorização, ele poderá ser falsamente identificado como um ataque de elevação de privilégios usando dados de autorização forjados.

## <a name="post-investigation"></a>Investigação de postagem
A Microsoft recomenda consultar uma equipe profissional de Resposta a Incidentes e Recuperação, que pode ser contatada por meio da Equipe de contas da Microsoft, para ajudar a detectar se um invasor implantou métodos de persistência em sua rede.


## <a name="mitigation"></a>Atenuação

Aplicar os boletins de segurança [MS14-068](https://technet.microsoft.com/library/security/MS14-068.aspx) e [MS11-013](https://technet.microsoft.com/library/security/ms11-013.aspx) que resolvem as vulnerabilidades no KDC do Kerberos. 


## <a name="see-also"></a>Consulte também
- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
