---
title: Configurar exclusões de detecção e contas honeytoken da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Configuração de exclusões de detecção e contas de usuário honeytoken.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 1ad5e923-9bbd-4f56-839a-b11a9f387d4b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a538ce4596da106d11646e27aa65131bb47380d2
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48782974"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*


<<<<<<< HEAD
# <a name="configure-detection-exclusions-and-honeytoken-accounts"></a>Configurar exclusões de detecção e contas de honeytoken
=======

# <a name="install-azure-atp---step-7"></a>Instalar o Azure ATP – etapa 7

> [!div class="step-by-step"]
> [«Etapa 6](install-atp-step6-vpn.md)
> [Etapa 8»](install-atp-step8-samr.md)

## <a name="step-7-configure-detection-exclusions-and-honeytoken-accounts"></a>Etapa 7. Configurar exclusões de detecção e contas de honeytoken
>>>>>>> 209d7e7162816a4c9e6e0ec0ff8d02f771e12d04

O Azure ATP permite que endereços IP ou usuários específicos sejam excluídos de várias detecções. 

Por exemplo, uma **exclusão por Reconhecimento de DNS** poderia ser um verificador de segurança que usa o DNS como um mecanismo de verificação. A exclusão ajuda o Azure ATP a ignorar esses verificadores.  

O Azure ATP também permite a configuração de contas de honeytoken, usadas como interceptações de ações mal-intencionadas. Qualquer autenticação associada a essas contas de honeytoken (normalmente inativas) dispara um alerta.

Para configurar, execute estas etapas:

1.  No portal do Azure ATP, clique no ícone de configurações e selecione **Configuração**.

    ![Definições de configuração do Azure ATP](media/atp-config-menu.png)

2.  Em **Detecção**, clique em **Marcas de entidade**.

3. Em **Contas de honeytoken**, insira o nome da conta de honeytoken e clique no sinal **+**. O campo de contas Honeytoken é pesquisável e exibe automaticamente entidades em sua rede. Clique em **Salvar**.

   ![Honeytoken](media/honeytoken-sensitive.png)

4. Clique em **Exclusões**. Insira uma conta de usuário ou endereço IP a ser excluído da detecção, para cada tipo de ameaça. 
5. Clique no sinal *mais*. O campo **Adicionar entidade** (usuário ou computador) é pesquisável e será preenchido automaticamente com entidades na sua rede. Para obter mais informações, consulte [Excluindo entidades de detecções](excluding-entities-from-detections.md) e o [Guia de atividades suspeitas](suspicious-activity-guide.md).

   ![Exclusões](media/exclusions.png)

6.  Clique em **Salvar**.


Parabéns, você implantou a Proteção Avançada contra Ameaças do Azure!

Verifique a linha de tempo do ataque para exibir atividades suspeitas detectadas e pesquisar por usuários ou computadores e exibir seus perfis.

O Azure ATP iniciará imediatamente a verificação de atividades suspeitas. Algumas detecções, como Modificações de grupo anormais, requerem um período de aprendizado e não estão disponíveis imediatamente após a implantação do Azure ATP.


<a name="-head"></a><<<<<<< HEAD
=======

> [!div class="step-by-step"]
> [«Etapa 6](install-atp-step6-vpn.md)
> [Etapa 8»](install-atp-step8-samr.md)

>>>>>>> 209d7e7162816a4c9e6e0ec0ff8d02f771e12d04
## <a name="see-also"></a>Consulte Também
- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/aatpsizingtool)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Confira o fórum do Azure ATP!](https://aka.ms/azureatpcommunity)
