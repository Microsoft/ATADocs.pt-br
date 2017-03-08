---
title: "Instalação do Advanced Threat Analytics – Etapa 6 | Microsoft Docs"
description: "Na etapa final da instalação do ATA, configure o usuário Honeytoken."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 70b8c4886f1c7459412eafc0646abfe1cc5d37d3
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*Aplica-se a: Advanced Threat Analytics versão 1.7*



# <a name="install-ata---step-6"></a>Instalação do ATA - Etapa 6

>[!div class="step-by-step"]
[« Etapa 5](install-ata-step5.md)

## <a name="step-6-configure--ip-address-exclusions-and-honeytoken-user"></a>Etapa 6. Configurar as exclusões de endereço IP e o usuário Honeytoken
O ATA permite a exclusão de endereços IP específicos de dois tipos de detecção: **Reconhecimento de DNS** e **Passagem de tíquete**. 

Por exemplo, uma **exclusão por Reconhecimento de DNS** poderia ser um verificador de segurança que usa o DNS como um mecanismo de verificação. A exclusão ajuda o ATA a ignorar esses verificadores. Um exemplo de uma exclusão por *Passagem de tíquete* é um dispositivo NAT.    

O ATA também permite a configuração de um usuário Honeytoken, que é usado como uma interceptação de atores mal-intencionados - qualquer autenticação associada à essa conta (normalmente inativa) disparará um alerta.

Para configurar os itens acima, execute estas etapas:

1.  No Console do ATA, clique no ícone de configurações e selecione **Configuração**.

    ![Definições de configurações do ATA](media/ATA-config-icon.JPG)

2.  Em **Exclusões de detecção**, insira um endereço IP para *Reconhecimento de DNS* ou *Passagem de tíquete* e clique no sinal de *mais*.

    ![Guardar alterações](media/ATA-exclusions.png)

3.  Em **Configurações da detecção**, insira os SIDs da conta Honeytoken e clique no sinal de adição. Por exemplo: `S-1-5-21-72081277-1610778489-2625714895-10511`.

    ![Definições de configurações do ATA](media/ATA-honeytoken.png)

    > [!NOTE]
    > Para localizar o SID de um usuário, pesquise o usuário no Console do ATA e clique na guia **Informações da Conta**. 

4.  Clique em **Salvar**.


Parabéns, você implantou com êxito o Microsoft Advanced Threat Analytics!

Verifique a linha de tempo do ataque para exibir atividades suspeitas detectadas e pesquisar por usuários ou computadores e exibir seus perfis.

O ATA iniciará a verificação de atividades suspeitas imediatamente. Algumas atividades, como algumas atividades de comportamento suspeito, não estarão disponíveis até que o ATA tenha tempo de criar perfis de comportamentos (três semanas, no mínimo).


>[!div class="step-by-step"]
[« Etapa 5](install-ata-step5.md)


## <a name="see-also"></a>Consulte também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)

