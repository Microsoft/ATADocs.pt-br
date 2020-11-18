---
title: Relatório de avaliação da postura de segurança de identidade de codificação fraca do Microsoft defender para identidade
description: Este artigo fornece uma visão geral do relatório de avaliação de postura de segurança de identidade de codificação fraca da identidade do Microsoft defender.
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
ms.openlocfilehash: a27d972e95c2c6b4ed4d87ebad747ef14ac0f24d
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848696"
---
# <a name="security-assessment-weak-cipher-usage"></a>Avaliação de segurança: Uso de criptografia fraca

## <a name="what-are-weak-ciphers"></a>O que é criptografia fraca?

A criptografia depende da codificação para criptografar dados. Por exemplo, o RC4 (Rivest Cipher 4, também conhecido como ARC4 ou ARCFOUR, que significa Alleged RC4) é um deles. Embora o RC4 seja notável por sua simplicidade e velocidade, várias vulnerabilidades foram descobertas desde sua versão original, tornando-o inseguro. O RC4 é especialmente vulnerável quando o início do fluxo de chave de saída não é descartado ou quando chaves relacionadas ou não aleatórias são usadas.

## <a name="how-do-i-use-this-security-assessment-to-improve-my-organizational-security-posture"></a>Como usar esta avaliação de segurança para aprimorar minha situação de segurança organizacional?

1. Analise a avaliação de segurança do uso de criptografia fraca.
    ![Analisar a avaliação do uso da criptografia fraca](media/cas-isp-weak-cipher-2.png)
1. Pesquise o motivo para os clientes e os servidores identificados usarem criptografias fracas.
1. Corrija os problemas e desabilite o uso do RC4 e/ou outras criptografias fracas (como DES/3DES).
1. Para saber mais sobre como desabilitar o RC4, confira o [Microsoft Security Advisory](https://support.microsoft.com/help/2868725/microsoft-security-advisory-update-for-disabling-rc4).

> [!NOTE]
> Essa avaliação é atualizada quase em tempo real.

## <a name="remediation"></a>Remediação

Desabilite os clientes e os servidores que você não quer que usem os pacotes de criptografia do RC4 configurando as seguintes chaves do Registro. Após desabilitar, qualquer servidor ou cliente que se comunique com outro cliente ou servidor que exija o uso do RC4 poderá impedir que a conexão ocorra. Os clientes, onde essa configuração for implantada, não poderão se conectar a sites que exigem RC4, e os servidores que implantarem essa configuração não poderão atender a clientes que exigem o uso de RC4.

> [!NOTE]
> Não se esqueça de testar as seguintes configurações em um ambiente controlado antes de habilitá-las na produção.
>
> - [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128]   "Enabled"=dword:00000000
> - [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128]   "Enabled"=dword:00000000
> - [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128]   "Enabled"=dword:00000000

Para saber mais sobre como baixar e atualizar as edições do Registro, confira o [Microsoft Security Advisory](/security-updates/SecurityAdvisories/2013/2868725).

## <a name="next-steps"></a>Próximas etapas

- [[!INCLUDE [Product short](includes/product-short.md)] filtragem de atividades no Cloud App Security](activities-filtering-mcas.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
