---
# required metadata

title: Instalação do ATA | Microsoft Advanced Threat Analytics
description: Na etapa final da instalação do ATA, configure as sub-redes de concessão de curto prazo e o usuário Honeytoken.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalação do ATA - Etapa 6

>[!div class="step-by-step"]
[« Etapa 5](install-ata-step5.md)

## Etapa 6. Configurar as sub-redes de concessão de curto prazo e o usuário Honeytoken
Sub-redes de concessão de curto prazo são sub-redes nas quais a atribuição de endereço IP muda muito rapidamente, em questão de segundos ou minutos. Por exemplo, endereços IP usados para suas VPNs endereços IP de Wi-Fi . Para inserir a lista de sub-redes de concessão de curto prazo usadas em sua organização, execute estas etapas:

1.  No Console do ATA no computador do Gateway do ATA, clique no ícone de configurações e escolha **Configuração**.

    ![Definições de configurações do ATA](media/ATA-config-icon.JPG)

2.  Em **Detecção**, digite o seguinte para as sub-redes de concessão de curto prazo. Insira as sub-redes de concessão de curto prazo usando o formato de notação de barra, por exemplo: `192.168.0.0/24` e clique no sinal de adição.

3.  Para os SIDs da conta do Honeytoken, insira o SID da conta de usuário que não terá qualquer atividade de rede e clique no sinal de adição. Por exemplo: `S-1-5-21-72081277-1610778489-2625714895-10511`.

    > [!NOTE]
    > Para localizar o SID de um usuário, pesquise o usuário no Console do ATA e clique na guia **Informações da Conta**. 

4.  Configurar exclusões: você pode configurar os endereços IP a serem excluídos de atividades suspeitas específicas. Confira [Como trabalhar com configurações de detecção do ATA](working-with-detection-settings.md) para saber mais.

5.  Clique em **Salvar**.

![Guardar alterações](media/ATA-VPN-Subnets.JPG)

Parabéns, você implantou com êxito o Microsoft Advanced Threat Analytics!

Verifique a linha de tempo do ataque para exibir atividades suspeitas detectadas e pesquisar por usuários ou computadores e exibir seus perfis.

O ATA iniciará a verificação de atividades suspeitas imediatamente. Algumas atividades, como algumas atividades de comportamento suspeito, não estarão disponíveis até que o ATA tenha tempo de criar perfis de comportamentos (três semanas, no mínimo).


>[!div class="step-by-step"]
[« Etapa 5](install-ata-step5.md)


## Consulte também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=May16_HO1-->


