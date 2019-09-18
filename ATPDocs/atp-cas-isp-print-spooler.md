---
title: Avaliações de situação de segurança de identidade de spooler de impressão da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Neste artigo, você tem uma visão geral dos relatórios de avaliação de situação de segurança de identidade de spooler de impressão da ATP do Azure.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1a7d9525-8923-4dae-af51-02a68aa61644
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fd2b795d7bb7973e24a5457237ff98a4bd1315f5
ms.sourcegitcommit: 939c098dd02a1f4191c528d10d69d059a62042b2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2019
ms.locfileid: "71005011"
---
# <a name="security-assessment-domain-controllers-with-print-spooler-service-available---preview"></a>Avaliação de segurança: Controladores de domínio com o Serviço de Spooler de Impressão disponível – versão prévia

![Desabilitar o serviço de spooler de impressão](media/atp-cas-isp-print-spooler-1.png)
 
## <a name="what-is-the-print-spooler-service"></a>O que é o serviço de **spooler de impressão**? 

O spooler de impressão é um serviço de software que gerencia processos de impressão. O spooler aceita trabalhos de impressão de computadores e garante que os recursos da impressora estejam disponíveis. O spooler também agenda a ordem em que os trabalhos de impressão são enviados para a fila de impressão. Nos primórdios dos PCs, os usuários precisavam esperar a impressão dos arquivos antes de executar outras ações. Graças aos spoolers de impressão modernos, hoje, imprimir tem um impacto mínimo na produtividade do usuário.

## <a name="what-risks-does-the-print-spooler-service-on-domain-controllers-introduce"></a>Quais riscos o serviço de **spooler de impressão** representam nos controladores de domínio? 

Embora pareça inofensivo, qualquer usuário autenticado pode se conectar remotamente ao serviço de spooler de impressão de um controlador de domínio e solicitar uma atualização dos novos trabalhos de impressão. Além disso, os usuários podem fazer com que o controlador de domínio envie a notificação para o sistema com a [delegação irrestrita](atp-cas-isp-unconstrained-kerberos.md). Essas ações testam a conexão e expõem a credencial da conta do computador do controlador de domínio (o **spooler de impressão** pertence ao SISTEMA). 

Devido à possibilidade de exposição, os controladores de domínio e os sistemas de administração do Active Directory precisam ter o serviço de **spooler de impressão** desabilitado. Para fazer isso, é recomendável usar um GPO (Objeto de Política de Grupo). 

Embora essa avaliação de segurança se concentre nos controladores de domínio, qualquer servidor tem a possibilidade de sofrer esse tipo de ataque.

## <a name="how-do-i-use-this-security-assessment"></a>Como usar a avaliação de segurança? 
1. Use a tabela do relatório para descobrir quais controladores de domínio têm o serviço de **spooler de impressão** habilitado.   
    <br>![Desabilitar a avaliação de segurança do serviço de spooler de impressão](media/atp-cas-isp-print-spooler-2.png)
1. Tome as medidas adequadas em relação aos controladores de domínio em risco e remova ativamente o serviço de spooler de impressão manualmente, por meio do GPO ou outros tipos de comandos remotos.

## <a name="remediation"></a>Remediação

Corrija este problema específico desabilitando o serviço de spooler de impressão em todos os servidores que não o exigem e verifique se não há contas com a delegação irrestrita configurada.
  

## <a name="next-steps"></a>Próximas etapas
- [Filtrar atividades da ATP do Azure no Cloud App Security](atp-activities-filtering-mcas.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)