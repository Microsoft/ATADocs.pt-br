---
title: Avaliações de uso da LAPS da Microsoft da Proteção Avançada contra Ameaças do Azure
description: Este artigo fornece uma visão geral do relatório de avaliação da postura de segurança da identidade de uso da LAPS da Microsoft do ATP do Azure.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f9e322e831b2c5e7b9852ce0889aafff6dffde8f
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90827954"
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
    ![Selecionar domínio com dispositivos LAPS](media/atp-cas-isp-laps-1.png)
1. Execute a ação apropriada nesses dispositivos baixando, instalando e configurando ou solucionando problemas da [LAPS da Microsoft](https://go.microsoft.com/fwlink/?linkid=2104282) com a documentação fornecida no download.
    ![Corrigir dispositivo de LAPS](media/atp-cas-isp-laps-2.png)

> [!NOTE]
> Essa avaliação é atualizada a cada 24 horas.

## <a name="see-also"></a>Consulte Também

- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
