---
title: Configurar SAM-R para habilitar a detecção de caminho de movimento lateral no ATP do Azure
description: Explica como configurar o Azure ATP para realizar chamadas remotas para SAM
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 05/16/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d752b23fb339bfdcbd1b202716c97a027f5b86dc
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912926"
---
# <a name="configure-azure-atp-to-make-remote-calls-to-sam"></a>Configurar o Azure ATP para realizar chamadas remotas para SAM

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

A detecção de [caminho de movimento lateral](use-case-lateral-movement-path.md) do ATP do Azure baseia-se em consultas que identificam os administradores locais em computadores específicos. Essas consultas são executadas com o protocolo SAM-R usando a conta de serviço do Azure ATP criada durante a instalação do Azure ATP [Etapa 2. Conectar-se ao AD](install-step2.md).

## <a name="configure-sam-r-required-permissions"></a>Configurar permissões necessárias do SAM-R

Para garantir que clientes e servidores Windows permitam que sua conta do Azure ATP execute o SAM-R, é necessário fazer uma modificação na **Política de Grupo** para adicionar a conta de serviço do Azure ATP, além das contas configuradas que aparecem na política de **Acesso de rede**. Lembre-se de aplicar as políticas de grupo a todos os computadores, exceto aos controladores de domínio.

> [!Note]
> Antes de aplicar novas políticas como essa, é fundamental garantir que o ambiente permaneça seguro e que nenhuma alteração afete a compatibilidade do aplicativo. Para isso, primeiro habilite e verifique a compatibilidade das alterações propostas no modo de auditoria antes de fazer alterações no ambiente de produção.

1. Localize a política:

   - Nome da política: Acesso à rede – restringir clientes com permissão para efetuar chamadas remotas para SAM
   - Localização: Configuração do computador, Configurações do Windows, Configurações de segurança, Políticas locais, Opções de segurança

    ![Localize a política](media/samr-policy-location.png)

1. Adicione o serviço do Azure ATP à lista de contas aprovadas capazes de executar essa ação em seus sistemas modernos do Windows.

    ![Adicione o serviço](media/samr-add-service.png)

3. Agora o **Serviço do AATP** (o serviço do Azure ATP criado durante a instalação) tem os privilégios necessários para executar o SAM-R no ambiente.

Para saber mais sobre SAM-R e essa Política de Grupo, consulte [Acesso à rede: restringir clientes com permissão para efetuar chamadas remotas para SAM](/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).

## <a name="see-also"></a>Consulte Também

- [Investigando ataques de caminho de movimento lateral com o Azure ATP](use-case-lateral-movement-path.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)