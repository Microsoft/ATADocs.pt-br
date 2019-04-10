---
title: Verificação de política de auditoria avançada da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Este artigo fornece uma visão geral da verificação de política de auditoria avançada da ATP do Azure.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 04/07/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: ab1e8dd9-a6c2-4c68-89d5-343b8ec56142
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4d3bac024e94f0aec2fb01f827fb5456527c5356
ms.sourcegitcommit: 4072bb8accd439590412f1380694f19aeaaa7a28
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59233319"
---
# <a name="azure-atp-advanced-audit-policy-check"></a>Verificação de política de auditoria avançada da ATP do Azure

A detecção da ATP do Azure depende de Logs de Eventos do Windows para obter visibilidade em determinados cenários, tais como logons de NTLM, modificações de grupos de segurança e eventos semelhantes. Para que os eventos corretos sejam auditados e incluídos no Log de Eventos do Windows, seus controladores de domínio exigem configurações precisas de política de auditoria avançada. Configurações de política de auditoria avançada incorretas fazem com que eventos críticos fiquem de fora de seus logs e resultam em uma cobertura incompleta da ATP do Azure.

Para facilitar a verificação do status atual de cada uma das políticas de auditoria avançada do controlador de domínio, a ATP do Azure verifica automaticamente as políticas de auditoria avançadas existentes e emite alertas de integridade para as configurações de política que exigem modificação. Cada alerta de integridade fornece detalhes específicos sobre o controlador de domínio e a política que apresenta problemas, bem como sugestões de correção.

![Alerta de Integridade da política de auditoria avançada](media/atp-health-alert-audit.png)


A Política de Auditoria de Segurança Avançada é habilitada por meio do GPO de **Política de Controladores de Domínio Padrão**. Esses eventos de auditoria são registrados nos Eventos do Windows do controlador de domínio. 

## <a name="modify-audit-policies"></a>Modificar políticas de auditoria 

Modifique as políticas de auditoria avançadas do seu controlador de domínio usando as instruções a seguir:

1. Faça logon no servidor como **administrador do domínio**.
2. Carregue o Editor de Gerenciamento de Política de Grupo de **Gerenciador do Servidor** > **Ferramentas** > **Gerenciamento de Política de Grupo**. 
3. Expanda as **Unidades organizacionais de controladores de domínio**, clique com o botão direito do mouse em **Política de controladores de domínio padrão** e selecione **Editar**. 

    ![Editar política de controlador de domínio](media/atp-advanced-audit-policy-check-step-1.png)

4. Na janela que é aberta, vá para **Configuração do computador** > **Políticas** > **Configurações do Windows** > **Configurações de segurança** > **Configuração de política de auditoria avançada**.

    ![Configuração da política de auditoria avançada](media/atp-advanced-audit-policy-check-step-2.png)

5. Vá para Logon na conta, clique duas vezes em **Validação de credenciais de auditoria** e selecione **Configurar estes eventos de auditoria**, tanto para eventos de êxito quanto para os de falha. 

    ![Validação de credenciais](media/atp-advanced-audit-policy-check-step-3.png)

6. Vá para Gerenciamento da Conta, clique duas vezes em **Gerenciamento do Grupo de Segurança de Auditoria** e selecione **Configurar estes eventos de auditoria**, tanto para eventos de êxito quanto para os de falha.

    ![Auditoria de gerenciamento do grupo de distribuição](media/atp-advanced-audit-policy-check-step-4.png)

    > [!NOTE]
    > Se você optar por usar a política local, adicione os logs de auditoria de **Logon da Conta** e **Gerenciamento de Conta** em sua política local. Se você estiver configurando a política de auditoria avançada, force a [subcategoria de política de auditoria](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/audit-force-audit-policy-subcategory-settings-to-override).
    
    > [!NOTE] 
    > Se você usar uma política diferente da política do controlador de domínio padrão para aplicar configurações da política de auditoria avançada, pode ser que o alerta de integridade resultante do ATP do Azure seja ignorado. 

7. Após a aplicação por meio do GPO, os novos eventos ficam visíveis nos **Logs de Eventos do Windows**.

## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
