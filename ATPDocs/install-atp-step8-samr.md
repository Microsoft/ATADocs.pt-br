---
title: Configurar SAM-R para habilitar a detecção de caminho de movimento lateral no Azure ATP | Microsoft Docs
description: Explica como configurar o Azure ATP para realizar chamadas remotas para SAM
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 12/02/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: db00eab0102a144c0cbf58fee10fbd1e672d1cbd
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56078163"
---
# <a name="configure-azure-atp-to-make-remote-calls-to-sam"></a>Configurar o Azure ATP para realizar chamadas remotas para SAM
A detecção de [caminho de movimento lateral](use-case-lateral-movement-path.md) do ATP do Azure baseia-se em consultas que identificam os administradores locais em computadores específicos. Essas consultas são executadas com o protocolo SAM-R usando a conta de serviço do Azure ATP criada durante a instalação do Azure ATP [Etapa 2. Conectar-se ao AD](install-atp-step2.md).

## <a name="configure-sam-r-required-permissions"></a>Configurar permissões necessárias do SAM-R
Para garantir que clientes e servidores Windows permitam que sua conta do Azure ATP execute o SAM-R, é necessário fazer uma modificação na **Política de Grupo** para adicionar a conta de serviço do Azure ATP, além das contas configuradas que aparecem na política de **Acesso de rede**.

1. Localize a política:

   - Nome da política: Acesso à rede – restringir clientes com permissão para efetuar chamadas remotas para SAM
   - Local: Configuração do computador, Configurações do Windows, Configurações de segurança, Políticas locais, Opções de segurança
  
   ![Localize a política](./media/samr-policy-location.png)

2. Adicione o serviço do Azure ATP à lista de contas aprovadas capazes de executar essa ação em seus sistemas modernos do Windows.
 
   ![Adicione o serviço](./media/samr-add-service.png)

3. Agora o **Serviço do AATP** (o serviço do Azure ATP criado durante a instalação) tem os privilégios necessários para executar o SAM-R no ambiente.

> [!NOTE]
> Antes de aplicar as novas políticas, certifique-se de que seu ambiente permaneça seguro, sem afetar a compatibilidade de aplicativos, ao permitir e verificar as alterações propostas no modo de auditoria.

Para saber mais sobre SAM-R e essa Política de Grupo, consulte [Acesso à rede: restringir clientes com permissão para efetuar chamadas remotas para SAM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).



## <a name="see-also"></a>Consulte Também
- [Investigando ataques de caminho de movimento lateral com o Azure ATP](use-case-lateral-movement-path.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)