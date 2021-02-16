---
title: Desinstalar o Microsoft defender para o sensor de identidade
description: Este artigo descreve como desinstalar o Microsoft defender para o sensor de identidade dos controladores de domínio.
ms.date: 12/22/2020
ms.topic: how-to
ms.openlocfilehash: 4d93637cabc0169efa0c3d62b4342578c4f006e1
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533334"
---
# <a name="uninstall-the-microsoft-defender-for-identity-sensor"></a>Desinstalar o sensor do Microsoft defender para identidade

Este artigo descreve como desinstalar o [!INCLUDE [Product long](includes/product-long.md)] sensor de controladores de domínio para os seguintes cenários:

1. Desinstalar um sensor de um controlador de domínio
1. Remover um sensor órfão
1. Remover um sensor duplicado

## <a name="uninstall-a-sensor-from-a-domain-controller"></a>Desinstalar um sensor de um controlador de domínio

As etapas a seguir descrevem como desinstalar um sensor de um controlador de domínio.

1. Entre no controlador de domínio com privilégios de administrador local.
1. No menu **Iniciar** do Windows, clique em **configurações**  >  **painel de controle**  >  **Adicionar/remover programas**.
1. Selecione a instalação do sensor, clique em **desinstalar** e siga as instruções para remover o sensor.

## <a name="remove-an-orphaned-sensor"></a>Remover um sensor órfão

Esse cenário pode ocorrer quando um controlador de domínio foi excluído sem primeiro desinstalar o sensor, e o sensor ainda aparece no [!INCLUDE [Product short](includes/product-short.md)] Portal.

1. No [!INCLUDE [Product short](includes/product-short.md)] portal, acesse **configuração** e, na seção **sistema** , selecione **sensores**.
1. Localize o sensor órfão e, no final da linha, clique em **excluir** (ícone de lixeira).

    ![Exclusão órfão [! INCLUIR sensor [produto curto] (inclui/produto-curto. MD)] da página sensores](media/delete-orphaned-sensor.png)

## <a name="remove-a-duplicate-sensor"></a>Remover um sensor duplicado

Esse cenário pode ocorrer após uma atualização do sensor in-loco e o sensor aparece duas vezes no [!INCLUDE [Product short](includes/product-short.md)] Portal.

1. No [!INCLUDE [Product short](includes/product-short.md)] portal, acesse **configuração** e, na seção **sistema** , selecione **sensores**.
1. Localize o sensor órfão e, no final da linha, clique em **excluir** (ícone de lixeira).

## <a name="see-also"></a>Consulte Também

- [Desinstalar o [!INCLUDE [Product short](includes/product-short.md)] sensor silenciosamente](silent-installation.md#silently-uninstall-sensor)
