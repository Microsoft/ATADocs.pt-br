---
title: Instalação do Advanced Threat Analytics – Etapa 8 | Microsoft Docs
description: Na etapa final da instalação do ATA, configure o usuário Honeytoken.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 6/14/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b237ce62e3828e1dced51a05d6d5a2977bf11285
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56076548"
---
# <a name="install-ata---step-8"></a>Instalação do ATA - Etapa 8

*Aplica-se a: Advanced Threat Analytics versão 1.9*

> [!div class="step-by-step"]
> [« Etapa 7](vpn-integration-install-step.md)
> [Etapa 9 »](install-ata-step9-samr.md)

## <a name="step-8-configure-ip-address-exclusions-and-honeytoken-user"></a>Etapa 8. Configurar as exclusões de endereço IP e o usuário Honeytoken

O ATA permite a exclusão de endereços IP ou de usuários específicos de várias detecções. 

Por exemplo, uma **exclusão por Reconhecimento de DNS** poderia ser um verificador de segurança que usa o DNS como um mecanismo de verificação. A exclusão ajuda o ATA a ignorar esses verificadores. Um exemplo de uma exclusão por *Passagem de tíquete* é um dispositivo NAT.    

O ATA também permite a configuração de um usuário Honeytoken, que é usado como uma interceptação de atores mal-intencionados - qualquer autenticação associada à essa conta (normalmente inativa) dispara um alerta.

Para configurar isso, execute estas etapas:

1.  No Console do ATA, clique no ícone de configurações e selecione **Configuração**.

    ![Definições de configurações do ATA](media/ATA-config-icon.png)

2.  Em **Detecção**, clique em **Marcas de entidade**.

2. Em **Honeytoken accounts (Contas Honeytoken)** insira o nome da conta Honeytoken. O campo de contas Honeytoken é pesquisável e exibe automaticamente entidades em sua rede.

   ![Honeytoken](media/honeytoken.png)

3. Clique em **Exclusões**. Para cada tipo de ameaça, insira uma conta de usuário ou endereço IP a ser excluído da detecção dessas ameaças e clique no sinal de *adição*. O campo **Adicionar entidade** (usuário ou computador) é pesquisável e será preenchido automaticamente com entidades na sua rede. Para obter mais informações, consulte [Excluindo entidades de detecções](excluding-entities-from-detections.md)

   ![Exclusões](media/exclusions.png)

4.  Clique em **Salvar**.


Parabéns, você implantou com êxito o Microsoft Advanced Threat Analytics!

Verifique a linha de tempo do ataque para exibir atividades suspeitas detectadas e pesquisar por usuários ou computadores e exibir seus perfis.

O ATA inicia a verificação de atividades suspeitas imediatamente. Algumas atividades, como atividades de comportamento suspeito, não ficam disponíveis até que o ATA tenha tempo de criar perfis de comportamentos (três semanas, no mínimo).

Para verificar se ATA está funcionando e detectar violações em sua rede, é possível conferir o [manual de simulação de ataque ATA](https://docs.microsoft.com/enterprise-mobility-security/solutions/ata-attack-simulation-playbook).


> [!div class="step-by-step"]
> [« Etapa 7](vpn-integration-install-step.md)
> [Etapa 9 »](install-ata-step9-samr.md)


## <a name="related-videos"></a>Vídeos Relacionados
- [Visão geral da implantação do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Como escolher o tipo certo de Gateway do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Consulte Também
- [Guia de implantação da POC (prova de conceito) do ATA](http://aka.ms/atapoc)
- [Ferramenta de dimensionamento do ATA](http://aka.ms/atasizingtool)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)

