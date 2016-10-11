---
title: Instalar o ATA | Microsoft ATA
description: "Na etapa final da instalação do ATA, configure o usuário Honeytoken."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 09/20/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d47d9e7be294c68d764710c15c4bb78539e42f62
ms.openlocfilehash: 9ee2f36d8f0b7eae061873e8735139ccc4da00d1


---

*Aplica-se a: Advanced Threat Analytics versão 1.7*



# Instalação do ATA - Etapa 6

>[!div class="step-by-step"]
[« Etapa 5](install-ata-step5.md)

## Etapa 6. Configurar as exclusões de endereço IP e o usuário Honeytoken
O ATA permite a exclusão de endereços IP específicos e sub-redes de IP a partir de dois tipos de detecções: **Reconhecimento de DNS** e **Passagem de tíquete**. 

Por exemplo, uma **exclusão por Reconhecimento de DNS** poderia ser um verificador de segurança que usa o DNS como um mecanismo de verificação. A exclusão ajuda o ATA a ignorar esses verificadores. Um exemplo de uma exclusão por *Passagem de tíquete* é um dispositivo NAT.    

O ATA também permite a configuração de um usuário Honeytoken, que é usado como uma interceptação de atores mal-intencionados - qualquer autenticação associada à essa conta (normalmente inativa) disparará um alerta.

Para configurar os itens acima, execute estas etapas:

1.  No Console do ATA, clique no ícone de configurações e selecione **Configuração**.

    ![Definições de configurações do ATA](media/ATA-config-icon.JPG)

2.  Em **Exclusões de detecção**, insira o seguinte para os endereços IP de *Reconhecimento de DNS* ou *Passagem de tíquete*. Use o formato CIDR, por exemplo: `192.168.1.0/24` e clique no sinal de *adição*.

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


## Consulte também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Sep16_HO4-->


