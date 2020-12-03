---
title: Avaliações de uso do Microsoft defender para identidade Microsoft LAPS
description: Este artigo fornece uma visão geral do relatório de avaliação da postura de segurança de identidade de uso do Microsoft defender para identidade do Microsoft LAPS.
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: d829636ac9659a19453db6f4cadfba54d129593d
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96543613"
---
# <a name="security-assessment-microsoft-laps-usage"></a>Avaliação de segurança: uso da LAPS da Microsoft

## <a name="what-is-microsoft-laps"></a>O que é LAPS da Microsoft?

A LAPS ("Solução de Senha de Administrador Local") da Microsoft oferece gerenciamento de senhas da conta de administrador local para computadores ingressados no domínio. As senhas são aleatórias e armazenadas no AD (Active Directory), protegidas por ACLs, portanto apenas usuários qualificados podem lê-las ou solicitar a redefinição delas.

## <a name="what-risk-does-not-implementing-laps-pose-to-an-organization"></a>Que risco a não implementação da LAPS apresenta para uma organização?

A LAPS fornece uma solução para o problema de usar uma conta local comum com uma senha idêntica em cada computador em um domínio. A LAPS resolve esse problema definindo uma senha aleatória alternada diferente para a conta de administrador local comum em todos os computadores no domínio.

A LAPS simplifica o gerenciamento de senha e ajuda os clientes a implementar outras defesas recomendadas contra ataques cibernéticos. Em particular, a solução reduz o risco de escalonamento lateral que ocorre quando os clientes usam a mesma combinação de conta local administrativa e senha nos computadores deles. A LAPS armazena a senha da conta de administrador local de cada computador no AD, protegida em um atributo confidencial no objeto do AD correspondente do computador. O computador pode atualizar os próprios dados da senha no AD e os administradores de domínio podem permitir acesso de leitura a usuários ou grupos autorizados, como administradores de senha da estação de trabalho.

## <a name="how-do-i-use-this-security-assessment"></a>Como usar a avaliação de segurança?

1. Use a tabela de relatório para descobrir quais de seus domínios têm alguns (ou todos os) dispositivos compatíveis com Windows que não estão protegidos por LAPS ou cuja senha gerenciada por LAPS não foi alterada nos últimos 60 dias.
1. Para domínios protegidos parcialmente, selecione a respectiva linha para ver a lista de dispositivos não protegidos por LAPS nesse domínio.
    ![Selecionar domínio com dispositivos LAPS](media/cas-isp-laps-1.png)
1. Execute a ação apropriada nesses dispositivos baixando, instalando e configurando ou solucionando problemas da [LAPS da Microsoft](https://go.microsoft.com/fwlink/?linkid=2104282) com a documentação fornecida no download.
    ![Corrigir dispositivo de LAPS](media/cas-isp-laps-2.png)

> [!NOTE]
> Essa avaliação é atualizada a cada 24 horas.

## <a name="see-also"></a>Consulte Também

- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
