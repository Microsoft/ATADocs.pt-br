---
title: Suporte a várias florestas da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Suporte para várias florestas do Active Directory no Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/24/2019
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7eccccc520d97e38c001f509d851912126d8fc17
ms.sourcegitcommit: 19ff0ed88e450506b5725bbcbb0d0bd2f0c5e4bb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/27/2019
ms.locfileid: "55085394"
---
# <a name="azure-advanced-threat-protection-multi-forest-support"></a>Suporte para várias florestas da Proteção Avançada contra Ameaças do Azure


## <a name="multi-forest-support-set-up"></a>Configuração de suporte a várias florestas 

O ATP do Azure dá suporte a organizações com várias florestas, permitindo monitorar a atividade e criar perfis de usuários facilmente entre as florestas. 

As organizações normalmente têm várias florestas do Active Directory, geralmente usadas para finalidades diferentes, incluindo infraestrutura herdada de fusões e aquisições corporativas, distribuição geográfica e limites de segurança (florestas vermelhas). Você pode proteger várias florestas usando o ATP do Azure, com a capacidade de monitorar e investigar a rede inteira usando um único painel de controle.

A capacidade de dar suporte a várias florestas do Active Directory permite:
-   Veja e investigue as atividades executadas pelos usuários em várias florestas usando um único painel de controle. 
-   Melhor detecção e redução de falsos positivos, fornecendo integração avançada do Active Directory e a resolução de conta. 
-   Maior controle e implantação facilitada. Alertas de monitoramento aprimorados e relatórios para cobertura entre organizações quando os controladores do domínio forem todos monitorados de um único console do Azure ATP.


## <a name="azure-atp-detection-activity-across-multiple-forests"></a>Atividade de detecção do ATP do Azure entre várias florestas 

Para detectar atividades entre florestas, os sensores do ATP do Azure consultam os controladores de domínio nas florestas remotas para criar perfis para todas as entidades envolvidas (incluindo usuários e computadores em florestas remotas). 

- Os sensores do ATP do Azure podem ser instalados em todas as florestas, até mesmo em florestas não confiáveis.
- Adicione credenciais na página Serviços de diretório para todas as florestas em seu ambiente. 
    - Uma credencial é necessária para cada floresta com relação de confiança bidirecional. 
    - Credenciais adicionais são necessárias para cada floresta sem a confiança Kerberos ou não confiáveis. 

![Estágio 1 de boas-vindas do Azure ATP](media/directory-services-add-no-trust-forests.png)

### <a name="requirements"></a>Requisitos 

- O usuário que você configura no console do ATP do Azure em **Serviços de diretório** precisa ser confiável em todas as outras florestas e ter pelo menos permissão somente leitura para executar consultas LDAP nos controladores de domínio.
- Se os sensores autônomos do Azure ATP estiverem instalados em computadores autônomos, em vez de diretamente nos controladores de domínio, os computadores devem ter permissão para se comunicar com todos os controladores de domínio da floresta remota usando o LDAP. 

- Para que o ATP do Azure se comunique com os sensores e sensores autônomos dele, abra as seguintes portas em cada computador no qual o sensor do ATP do Azure está instalado:
 
  |Protocolo|Transport|Porta|Para/De|Direção|
  |----|----|----|----|----|
  |**Portas de Internet**||||
  |SSL (*.atp.azure.com)|TCP|443|Serviço de nuvem do Azure ATP|Saída|
  |**Portas internas**||||           
  |LDAP|TCP e UDP|389|Controladores de domínio|Saída|
  |LDAP seguro (LDAPS)|TCP|636|Controladores de domínio|Saída|
  |LDAP para o Catálogo Global|TCP|3268|Controladores de domínio|Saída|
  |LDAPS para o Catálogo Global|TCP|3269|Controladores de domínio|Saída|


## <a name="multi-forest-support-network-traffic-impact"></a>Impacto do tráfego de rede no suporte a várias florestas 

Quando o Azure ATP mapeia suas florestas, ele usa um processo que afeta o seguinte:

-   Depois que o sensor do Azure ATP está em execução, ele consulta as florestas remotas do Active Directory e recupera uma lista de usuários e dados de máquinas para a criação de perfil.
-   A cada cinco minutos, cada sensor do Azure ATP consulta um controlador de domínio de cada domínio, de cada floresta, para mapear todas as florestas na rede.
-   Cada sensor do Azure ATP mapeia as florestas usando o objeto "trustedDomain" no Active Directory, efetuando logon e verificando o tipo de relação de confiança.
-   Você também pode ver o tráfego ad hoc quando o sensor do Azure ATP detecta atividade entre florestas. Quando isso ocorre, os sensores do Azure ATP enviarão uma consulta LDAP para os respectivos controladores de domínio para recuperar informações da entidade. 

## <a name="known-limitations"></a>Limitações conhecidas
-   Os logons interativos executados por usuários em uma floresta para acessar recursos em outra floresta não são exibidos no painel do Azure ATP.



## <a name="see-also"></a>Consulte Também
- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/aatpsizingtool)
- [Arquitetura do Azure ATP](atp-architecture.md)
- [Instalar o Azure ATP](install-atp-step1.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)

