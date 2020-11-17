---
title: Alterar configuração do Advanced Threat Analytics-senha de conectividade do domínio
description: Descreve como alterar a Senha de conectividade do domínio no Gateway do ATA.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: d310ec8659fcb2fa2a128f24b9b243939dc438eb
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690373"
---
# <a name="change-ata-configuration---domain-connectivity-password"></a>Alteração da configuração do ATA - senha de conectividade do domínio

[!INCLUDE [Banner for top of topics](includes/banner.md)]

## <a name="change-the-domain-connectivity-password"></a>Alterar a senha de conectividade do domínio

Se você modificar a senha de conectividade do domínio, certifique-se de que a senha digitada esteja correta. Se não estiver, o serviço do Gateway do ATA deixará de ser executado em Gateways do ATA.

Se você suspeitar que isso aconteceu, no Gateway do ATA, examine o arquivo Microsoft.Tri.Gateway-Errors.log em busca dos seguintes erros: `The supplied credential is invalid.`

Para corrigir isso, siga este procedimento e atualize a Senha de conectividade do domínio na Central do ATA:

1. Abra o Console do ATA na Central do ATA.

1. Selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

    ![Ícone Definições de configuração do ATA](media/ATA-config-icon.png)

1. Selecione **Serviços de Diretório**.

    ![Imagem da mudança de senha no Gateway do ATA](media/ATA-GW-change-DC-password.png)

1. Em **Senha**, altere a senha.

    Se o Centro do ATA tiver conectividade com o domínio, use o botão **Testar Conexão** para validar as credenciais

1. Clique em **Save** (Salvar).

1. Depois de alterar a senha, verifique manualmente se o serviço do Gateway do ATA está em execução nos servidores do Gateway do ATA.



## <a name="see-also"></a>Consulte Também
- [Trabalhando com o Console do ATA](working-with-ata-console.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
