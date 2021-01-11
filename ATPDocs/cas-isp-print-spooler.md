---
title: Avaliações de postura de segurança de identidade do spooler de impressão do Microsoft defender para identidade
description: Este artigo fornece uma visão geral do Microsoft defender para relatórios de avaliação de postura de segurança de identidade do spooler de impressão.
ms.date: 01/11/2021
ms.topic: how-to
ms.openlocfilehash: dc380efcff1353203786a91b481d1e091e860071
ms.sourcegitcommit: 57dd3e4663346db3542cf9e755dac135c5e75125
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98062511"
---
# <a name="security-assessment-domain-controllers-with-print-spooler-service-available"></a>Avaliação de segurança: Controladores de domínio com o serviço de spooler de impressão disponível

![Desabilitar o serviço de spooler de impressão](media/cas-isp-print-spooler-1.png)

## <a name="what-is-the-print-spooler-service"></a>O que é o serviço de **spooler de impressão**?

O spooler de impressão é um serviço de software que gerencia processos de impressão. O spooler aceita trabalhos de impressão de computadores e garante que os recursos da impressora estejam disponíveis. O spooler também agenda a ordem em que os trabalhos de impressão são enviados para a fila de impressão. Nos primórdios dos PCs, os usuários precisavam esperar a impressão dos arquivos antes de executar outras ações. Graças aos spoolers de impressão modernos, imprimir tem um impacto mínimo na produtividade geral do usuário hoje em dia.

## <a name="what-risks-does-the-print-spooler-service-on-domain-controllers-introduce"></a>Quais riscos o serviço de **spooler de impressão** representam nos controladores de domínio?

Embora pareça inofensivo, qualquer usuário autenticado pode se conectar remotamente ao serviço de spooler de impressão de um controlador de domínio e solicitar uma atualização dos novos trabalhos de impressão. Além disso, os usuários podem dizer ao controlador de domínio para enviar a notificação ao sistema com [delegação irrestrita](cas-isp-unconstrained-kerberos.md). Essas ações testam a conexão e expõem a credencial da conta do computador do controlador de domínio (o **spooler de impressão** pertence ao SISTEMA).

Devido à possibilidade de exposição, os controladores de domínio e os sistemas de administração do Active Directory precisam ter o serviço de **spooler de impressão** desabilitado. Para fazer isso, é recomendável usar um GPO (Objeto de Política de Grupo).

Embora essa avaliação de segurança se concentre nos controladores de domínio, qualquer servidor tem a possibilidade de sofrer esse tipo de ataque.

> [!NOTE]
>
> - Investigue suas configurações e dependências do **spooler de impressão** antes de desabilitar esse serviço e impedir fluxos de trabalho de impressão ativos.
> - A função de controlador de domínio [adiciona um thread ao serviço de spooler](https://docs.microsoft.com/windows-server/security/windows-services/security-guidelines-for-disabling-system-services-in-windows-server#print-spooler) que é responsável por executar a remoção de impressão – removendo os objetos de fila de impressão obsoletos do Active Directory. Portanto, a recomendação de segurança para desabilitar o serviço **spooler de impressão** é uma compensação entre a segurança e a capacidade de realizar a remoção de impressão. Para resolver o problema, você deve considerar a remoção periódica de objetos de fila de impressão obsoletos, manualmente ou usando um script de automação.

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
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
