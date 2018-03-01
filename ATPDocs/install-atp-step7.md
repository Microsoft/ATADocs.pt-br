---
title: "Instalar a Proteção Avançada contra Ameaças do Azure – etapa 7 | Microsoft Docs"
description: "Na etapa final da instalação do Azure ATP, você configura o usuário Honeytoken."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 1ad5e923-9bbd-4f56-839a-b11a9f387d4b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: bef13d0f4799a4483eda6604a8ed96befaa13508
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2018
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*



# <a name="install-azure-atp---step-7"></a>Instalar o Azure ATP – etapa 7

>[!div class="step-by-step"]
[«Etapa 6](install-atp-step6-vpn.md)
[Etapa 8»](install-atp-step8-samr.md)

## <a name="step-7-configure-detection-exclusions-and-honeytoken-user"></a>Etapa 7. Configurar exclusões de detecção e o usuário Honeytoken

O Azure ATP permite que endereços IP ou usuários específicos sejam excluídos de várias detecções. 

Por exemplo, uma **exclusão por Reconhecimento de DNS** poderia ser um verificador de segurança que usa o DNS como um mecanismo de verificação. A exclusão ajuda o Azure ATP a ignorar esses verificadores.  

O Azure ATP também permite a configuração de um usuário Honeytoken, que é usado como uma interceptação de atores mal-intencionados – qualquer autenticação associada a essa conta (normalmente inativa) dispara um alerta.

Para configurar isso, execute estas etapas:

1.  No portal de espaço de trabalho do Azure ATP, clique no ícone de configurações e selecione **Configuração**.

    ![Definições de configuração do Azure ATP](media/atp-config-menu.png)

2.  Em **Detecção**, clique em **Marcas de entidade**.

3. Em **Contas Honeytoken**, insira o nome da conta Honeytoken e clique no sinal **+**. O campo de contas Honeytoken é pesquisável e exibe automaticamente entidades em sua rede. Clique em **Salvar**.

   ![Honeytoken](media/honeytoken-sensitive.png)

4. Clique em **Exclusões**. Para cada tipo de ameaça, insira uma conta de usuário ou endereço IP a ser excluído da detecção dessas ameaças e clique no sinal de *adição*. O campo **Adicionar entidade** (usuário ou computador) é pesquisável e será preenchido automaticamente com entidades na sua rede. Para obter mais informações, consulte [Excluindo entidades de detecções](excluding-entities-from-detections.md) e o [Guia de atividades suspeitas](suspicious-activity-guide.md).

   ![Exclusões](media/exclusions.png)

5.  Clique em **Salvar**.


Parabéns, você implantou com êxito a Proteção Avançada contra Ameaças do Azure!

Verifique a linha de tempo do ataque para exibir atividades suspeitas detectadas e pesquisar por usuários ou computadores e exibir seus perfis.

O Azure ATP inicia a verificação de atividades suspeitas imediatamente. Alguns detecções, como Modificações de grupo anormais, requerem um período de aprendizado e não ficam disponíveis imediatamente após a implantação do Azure ATP.



>[!div class="step-by-step"]
[«Etapa 6](install-atp-step6-vpn.md)
[Etapa 8»](install-atp-step8-samr.md)

## <a name="see-also"></a>Consulte Também
- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/aatpsizingtool)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)
