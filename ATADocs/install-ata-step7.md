---
title: Instalar o Advanced Threat Analytics – etapa 8
description: Na etapa final da instalação do ATA, configure o usuário Honeytoken.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 6/14/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 81145cd89246e4274b90a9524c995a32690f18c1
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90911254"
---
# <a name="install-ata---step-8"></a>Instalação do ATA - Etapa 8

[!INCLUDE [Banner for top of topics](includes/banner.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

> [!div class="step-by-step"]
> [«Etapa 7](vpn-integration-install-step.md) 
>  [Etapa 9»](install-ata-step9-samr.md)

## <a name="step-8-configure-ip-address-exclusions-and-honeytoken-user"></a>Etapa 8. Configurar as exclusões de endereço IP e o usuário Honeytoken

O ATA permite a exclusão de endereços IP ou de usuários específicos de várias detecções.

Por exemplo, uma **exclusão por Reconhecimento de DNS** poderia ser um verificador de segurança que usa o DNS como um mecanismo de verificação. A exclusão ajuda o ATA a ignorar esses verificadores. Um exemplo de uma exclusão por *Passagem de tíquete* é um dispositivo NAT.

O ATA também permite a configuração de um usuário Honeytoken, que é usado como uma interceptação de atores mal-intencionados - qualquer autenticação associada à essa conta (normalmente inativa) dispara um alerta.

Para configurar isso, execute estas etapas:

1. No console do ATA, clique no ícone configurações e selecione **configuração**.

    ![Definições de configurações do ATA](media/ATA-config-icon.png)

1. Em **Detecção**, clique em **Marcas de entidade**.

1. Em **Honeytoken accounts (Contas Honeytoken)** insira o nome da conta Honeytoken. O campo de contas Honeytoken é pesquisável e exibe automaticamente entidades em sua rede.

    ![Captura de tela mostrando a entrada de nome de conta do Honeytoken](media/honeytoken.png)

1. Clique em **Exclusões**. Para cada tipo de ameaça, insira uma conta de usuário ou endereço IP a ser excluído da detecção dessas ameaças e clique no sinal de *adição*. O campo **Adicionar entidade** (usuário ou computador) é pesquisável e será preenchido automaticamente com entidades na sua rede. Para obter mais informações, consulte [Excluindo entidades de detecções](excluding-entities-from-detections.md)

    ![Captura de tela mostrando a exclusão de entidades da detecção](media/exclusions.png)

1. Clique em **Save** (Salvar).

Parabéns, você implantou com êxito o Microsoft Advanced Threat Analytics!

Verifique a linha de tempo do ataque para exibir atividades suspeitas detectadas e pesquisar por usuários ou computadores e exibir seus perfis.

O ATA inicia a verificação de atividades suspeitas imediatamente. Algumas atividades, como atividades de comportamento suspeito, não ficam disponíveis até que o ATA tenha tempo de criar perfis de comportamentos (três semanas, no mínimo).

Para verificar se ATA está funcionando e detectar violações em sua rede, é possível conferir o [manual de simulação de ataque ATA](/enterprise-mobility-security/solutions/ata-attack-simulation-playbook).

> [!div class="step-by-step"]
> [«Etapa 7](vpn-integration-install-step.md) 
>  [Etapa 9»](install-ata-step9-samr.md)

## <a name="related-videos"></a>Vídeos Relacionados

- [Visão geral da implantação do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Como escolher o tipo certo de Gateway do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>Consulte Também

- [Guia de implantação da POC (prova de conceito) do ATA](https://aka.ms/atapoc)
- [Ferramenta de dimensionamento do ATA](https://aka.ms/atasizingtool)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)
