---
title: Avaliações de postura de segurança de identidade do spooler de impressão do Microsoft defender para identidade
description: Este artigo fornece uma visão geral do Microsoft defender para relatórios de avaliação de postura de segurança de identidade do spooler de impressão.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 3ce32384545ea3751966ba9a677348ac70fe266b
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93277477"
---
# <a name="security-assessment-domain-controllers-with-print-spooler-service-available"></a>Avaliação de segurança: Controladores de domínio com o serviço de spooler de impressão disponível

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

![Desabilitar o serviço de spooler de impressão](media/cas-isp-print-spooler-1.png)

## <a name="what-is-the-print-spooler-service"></a>O que é o serviço de **spooler de impressão** ?

O spooler de impressão é um serviço de software que gerencia processos de impressão. O spooler aceita trabalhos de impressão de computadores e garante que os recursos da impressora estejam disponíveis. O spooler também agenda a ordem em que os trabalhos de impressão são enviados para a fila de impressão. Nos primórdios dos PCs, os usuários precisavam esperar a impressão dos arquivos antes de executar outras ações. Graças aos spoolers de impressão modernos, imprimir tem um impacto mínimo na produtividade geral do usuário hoje em dia.

## <a name="what-risks-does-the-print-spooler-service-on-domain-controllers-introduce"></a>Quais riscos o serviço de **spooler de impressão** representam nos controladores de domínio?

Embora pareça inofensivo, qualquer usuário autenticado pode se conectar remotamente ao serviço de spooler de impressão de um controlador de domínio e solicitar uma atualização dos novos trabalhos de impressão. Além disso, os usuários podem dizer ao controlador de domínio para enviar a notificação ao sistema com [delegação irrestrita](cas-isp-unconstrained-kerberos.md). Essas ações testam a conexão e expõem a credencial da conta do computador do controlador de domínio (o **spooler de impressão** pertence ao SISTEMA).

Devido à possibilidade de exposição, os controladores de domínio e os sistemas de administração do Active Directory precisam ter o serviço de **spooler de impressão** desabilitado. Para fazer isso, é recomendável usar um GPO (Objeto de Política de Grupo).

Embora essa avaliação de segurança se concentre nos controladores de domínio, qualquer servidor tem a possibilidade de sofrer esse tipo de ataque.

   > [!NOTE]
   > Investigue suas configurações e dependências do **spooler de impressão** antes de desabilitar esse serviço e impedir fluxos de trabalho de impressão ativos.

## <a name="how-do-i-use-this-security-assessment"></a>Como usar a avaliação de segurança?

1. Use a tabela do relatório para descobrir quais controladores de domínio têm o serviço de **spooler de impressão** habilitado.

    ![Desabilitar a avaliação de segurança do serviço de spooler de impressão](media/cas-isp-print-spooler-2.png)
1. Tome as medidas adequadas em relação aos controladores de domínio em risco e remova ativamente o serviço de spooler de impressão manualmente, por meio do GPO ou outros tipos de comandos remotos.

> [!NOTE]
> Essa avaliação é atualizada quase em tempo real.

## <a name="remediation"></a>Remediação

Corrija esse problema específico desabilitando o serviço de spooler de impressão em todos os servidores que não o exigem.

## <a name="next-steps"></a>Próximas etapas

- [[!INCLUDE [Product short](includes/product-short.md)] filtragem de atividades no Cloud App Security](activities-filtering-mcas.md)
- [Confira o [!INCLUDE [Product short](includes/product-short.md)] Fórum!](https://aka.ms/MDIcommunity)
