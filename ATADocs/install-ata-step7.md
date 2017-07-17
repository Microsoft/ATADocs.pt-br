---
title: "Instalação do Advanced Threat Analytics – Etapa 7 | Microsoft Docs"
description: "Na etapa final da instalação do ATA, configure o usuário Honeytoken."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/9/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 2b969089d8c4c2d861591342f7367e8cc5430b24
ms.sourcegitcommit: 3177d5894413fbd363b9aca8130f3f7a369223b8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*



# Instalação do ATA – Etapa 7
<a id="install-ata---step-7" class="xliff"></a>

>[!div class="step-by-step"]
[« Etapa 6](install-ata-step6.md)

## Etapa 7. Configurar as exclusões de endereço IP e o usuário Honeytoken
<a id="step-7-configure-ip-address-exclusions-and-honeytoken-user" class="xliff"></a>
O ATA permite a exclusão de endereços IP ou de usuários específicos de várias detecções. 

Por exemplo, uma **exclusão por Reconhecimento de DNS** poderia ser um verificador de segurança que usa o DNS como um mecanismo de verificação. A exclusão ajuda o ATA a ignorar esses verificadores. Um exemplo de uma exclusão por *Passagem de tíquete* é um dispositivo NAT.    

O ATA também permite a configuração de um usuário Honeytoken, que é usado como uma interceptação de atores mal-intencionados - qualquer autenticação associada à essa conta (normalmente inativa) disparará um alerta.

Para configurar os itens acima, execute estas etapas:

1.  No Console do ATA, clique no ícone de configurações e selecione **Configuração**.

    ![Definições de configurações do ATA](media/ATA-config-icon.png)

2.  Em **Detecção**, clique em **Geral**.

2. Em **Honeytoken accounts (Contas Honeytoken)** insira o nome da conta Honeytoken. O campo de contas Honeytoken é pesquisável e exibirá automaticamente entidades em sua rede.

   ![Honeytoken](media/honeytoken.png)

3. Clique em **Exclusões**. Para cada tipo de ameaça, insira uma conta de usuário ou endereço IP a ser excluído da detecção dessas ameaças e clique no sinal de *adição*. O campo **Adicionar entidade** (usuário ou computador) é pesquisável e será preenchido automaticamente com entidades na sua rede. Para obter mais informações, consulte [Excluindo entidades de detecções](excluding-entities-from-detections.md)

   ![Exclusões](media/exclusions.png)


  > [!NOTE]
  > Para localizar o SID de um usuário, pesquise o usuário no Console do ATA e clique na guia **Informações da Conta**. 

4.  Clique em **Salvar**.


Parabéns, você implantou com êxito o Microsoft Advanced Threat Analytics!

Verifique a linha de tempo do ataque para exibir atividades suspeitas detectadas e pesquisar por usuários ou computadores e exibir seus perfis.

O ATA iniciará a verificação de atividades suspeitas imediatamente. Algumas atividades, como algumas atividades de comportamento suspeito, não estarão disponíveis até que o ATA tenha tempo de criar perfis de comportamentos (três semanas, no mínimo).

Para verificar se ATA está funcionando e detectar violações em sua rede, é possível conferir o [manual de simulação de ataque ATA](https://docs.microsoft.com/enterprise-mobility-security/solutions/ata-attack-simulation-playbook).


>[!div class="step-by-step"]
[« Etapa 6](install-ata-step6.md)


## Consulte também
<a id="see-also" class="xliff"></a>

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)

