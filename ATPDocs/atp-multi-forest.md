---
title: Suporte a várias florestas da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Como configurar o suporte para várias florestas do Active Directory no Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/20/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ad120cfe3e736935a557f66417794cd531fa5b2e
ms.sourcegitcommit: b283bf66e63d76e6dba4564a229e804792794c6d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/29/2018
ms.locfileid: "47454081"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*

# <a name="install-azure-atp---step-9"></a>Instalar o Azure ATP – etapa 9

> [!div class="step-by-step"]
> [« Etapa 8](install-atp-step8-samr.md)

## <a name="step-9--set-up-azure-advanced-threat-protection-multi-forest-support"></a>Etapa 9.  Configurar o suporte para várias florestas da Proteção Avançada contra Ameaças do Azure

O Azure ATP pode dar suporte a organizações com várias florestas, permitindo monitorar com facilidade a atividade e os perfis de usuário entre florestas de um único painel de controle. 

As organizações normalmente têm várias florestas do Active Directory, geralmente usadas para finalidades diferentes, incluindo infraestrutura herdada de fusões e aquisições corporativas, distribuição geográfica e limites de segurança (florestas vermelhas). Você pode proteger várias florestas usando o Azure ATP, tendo a capacidade de monitorar e investigar por meio de um único painel de controle.

A capacidade de dar suporte a várias florestas do Active Directory permite:
-   Exiba e investigue as atividades executadas pelos usuários em várias florestas de um único painel de controle. 
-   Melhor detecção e redução de falsos positivos, fornecendo integração avançada do Active Directory e a resolução de conta. 
-   Maior controle e implantação facilitada. Alertas de monitoramento aprimorados e relatórios para cobertura entre organizações quando os controladores do domínio forem todos monitorados de um único console do Azure ATP.


## <a name="how-azure-atp-detects-activities-across-multiple-forests"></a>Como o Azure ATP detecta atividades entre várias florestas 

Para detectar atividades entre florestas, os sensores do Azure ATP consultam os controladores de domínio em florestas remotas para criar perfis para todas as entidades envolvidas, incluindo usuários e computadores em florestas remotas. 

> [!NOTE]
> - Sensores do Azure ATP podem ser instalados em todas as florestas (se existir uma relação de confiança unidirecional mínima).
> - O usuário que você configura no console do Azure ATP em **Serviços de diretório** devem ser confiáveis em todas as outras florestas.


Mesmo que você tenha florestas sem nenhum sensor do Azure ATP instalado, o Azure ATP ainda pode exibir e monitorar as atividades provenientes dessas florestas. Os sensores do ATP instalados podem consultar todos os controladores de domínio da floresta remota conectados para resolver os usuários e computadores, e criar perfis para cada um deles. 

## <a name="installation-requirements"></a>Requisitos de instalação 

-   Se os sensores autônomos do Azure ATP estiverem instalados em computadores autônomos, em vez de diretamente nos controladores de domínio, os computadores devem ter permissão para se comunicar com todos os controladores de domínio da floresta remota usando o LDAP. 
- O usuário que você configurar no console do Azure ATP em **Serviços de diretório** deve ser de confiança em todas as outras florestas e deve ter pelo menos permissão de leitura para executar consultas LDAP dos controladores de domínio.

- Para que o Azure ATP se comunique com os sensores do ATP e com os sensores autônomos do ATP, abra as seguintes portas em cada computador no qual o sensor do ATP esteja instalado:

 
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
-   Você também poderá ver tráfego ad hoc quando o sensor do ATP detectar atividade de diferentes florestas. Quando isso ocorre, os sensores do ATP enviam uma consulta LDAP para os controladores de domínio relevantes para recuperar informações da entidade. 

## <a name="known-limitations"></a>Limitações conhecidas
-   Os logons interativos executados por usuários em uma floresta para acessar recursos em outra floresta não são exibidos no painel do Azure ATP.


> [!div class="step-by-step"]
> [« Etapa 8](install-atp-step8-samr.md)


## <a name="see-also"></a>Consulte Também
- [Ferramenta de dimensionamento do ATP](http://aka.ms/aatpsizingtool)
- [Arquitetura do ATP](atp-architecture.md)
- [Instalar o ATP](install-atp-step1.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)

