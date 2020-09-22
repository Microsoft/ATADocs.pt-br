---
title: Atualização do Advanced Threat Analytics para o guia de migração 1,5
description: Procedimentos para atualizar o ATA para a versão 1.5
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 01/23/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: fb65eb41-b215-4530-93a2-0b8991f4e980
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: dae94f42ee4b4be200a3cf2ac299561efe0ddbb1
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90908779"
---
# <a name="ata-update-to-15-migration-guide"></a>Guia de migração de atualização do ATA para 1.5

[!INCLUDE [Rebranding notice](includes/rebranding.md)]
A atualização 1.5 do ATA fornece melhorias nas seguintes áreas:

- Tempo de detecção mais rápido

- Algoritmo de detecção automática avançado para os dispositivos NAT (conversão de endereços de rede)

- Processo de resolução de nomes avançado para dispositivos não associados a um domínio

- Suporte para a migração de dados durante as atualizações de produto

- Melhor capacidade de resposta da interface do usuário para atividades suspeitas com milhares de entidades envolvidas

- Resolução automática de alertas de integridade aprimorada

- Contadores de desempenho adicionais para monitoramento e solução de problemas avançados

## <a name="updating-ata-to-version-15"></a>Atualização do ATA para a versão 1.5
> [!NOTE]
> Se o ATA não estiver instalado em seu ambiente, baixe a versão completa do ATA, que inclui a versão 1,5 e siga o procedimento de instalação padrão descrito em [instalar o ATA](install-ata-step1.md).

Se você já tiver a versão 1.4 do ATA implantada, esse procedimento explicará as etapas necessárias para atualizar sua instalação.

Execute estas etapas para atualizar para o ATA versão 1.5:

1. Baixe o ATA v1.5 do VLSC ou MSDN.
      > [!NOTE]
      > Você também pode usar a versão atualizada completa do ATA para executar a atualização para a versão 1.5.


1. Atualize o Centro do ATA

1. Baixe o pacote atualizado do Gateway do ATA

1. Atualize os Gateways do ATA

    > [!IMPORTANT]
    > Atualize todos os Gateways do ATA para ter certeza de o ATA funciona corretamente.

### <a name="step-1-update-the-ata-center"></a>Etapa 1: Atualizar o Centro do ATA

1. Faça backup do seu banco de dados: (opcional)

    - Se a Central de ATA estiver sendo executada como uma máquina virtual e você quiser fazer um ponto de verificação, desligue a máquina virtual primeiro.

    - Se o centro do ATA estiver em execução em um servidor físico, siga o procedimento recomendado para [fazer backup do MongoDB](https://docs.mongodb.org/manual/core/backups/).

1. Execute o arquivo de atualização, Microsoft ATA Center Update.exe, e siga as instruções na tela para instalar a atualização.

    1.  Na página **Boas-vindas**, selecione seu idioma e clique em **Avançar**.

    2.  Leia o Contrato de Licença de Usuário Final e, se você aceitar os termos, clique na caixa de seleção **Avançar**.

    3.  Selecione se você quer executar a migração parcial ou completa (padrão).

        ![Escolha a migração completa ou parcial](media/ATA-center-fullpartial.png)

        - Se você selecionar a migração **Parcial**, qualquer tráfego de rede coletado e eventos do Windows encaminhados analisados pelo ATA serão excluídos e os perfis comportamentais do usuário terão que ser aprendidos novamente; isso levará no mínimo três semanas. Se você estiver com pouco espaço em disco, será útil executar uma migração **Parcial**.

        - Se você executar uma migração **Completa**, será necessário adicionar espaço em disco, conforme calculado para você na página de atualização, e a migração poderá demorar mais, dependendo do tráfego de rede. A migração completa retém todos os dados coletados anteriormente e os perfis comportamentais do usuário serão mantidos, o que significa que não demorará mais tempo para o ATA aprender os perfis de comportamento, e comportamentos anormais poderão ser detectados imediatamente após a atualização.

1. Clique em **Atualizar**. Depois de clicar em Atualizar, o ATA ficará offline até que o procedimento de atualização seja concluído.

1. Depois de atualizar a Central de ATA, os Gateways do ATA reportarão que agora estão desatualizados.

    ![Imagem de gateways desatualizados](media/ATA-center-outdated.png)

> [!IMPORTANT]
> - Atualize todos os Gateways do ATA para ter certeza de o ATA funciona corretamente.

### <a name="step-2-download-the-ata-gateway-setup-package"></a>Etapa 2. Baixe o pacote de instalação do Gateway do ATA
Após definir as configurações de conectividade do domínio, você poderá baixar o pacote de instalação do Gateway do ATA.

Para baixar o pacote do Gateway do ATA:

1. Exclua todas as versões anteriores do pacote do Gateway do ATA baixado anteriormente.

1. No computador do Gateway do ATA, abra um navegador e digite o endereço IP configurado no Centro do ATA para o Console do ATA. Quando o console do ATA for aberto, clique no ícone de configurações e selecione **configuração**.

    ![Ícone Definições de configuração](media/ATA-config-icon.png)

1. Na guia **gateways do ATA** , clique em **baixar a instalação do gateway do ATA**.

1. Salve o pacote localmente.

O arquivo zip inclui os seguintes arquivos:

- Instalador do Gateway do ATA

- Arquivo de configurações com as informações necessárias para conectar-se à Central de ATA

### <a name="step-3-update-the-ata-gateways"></a>Etapa 3: Atualize os Gateways do ATA

1. Em cada Gateway do ATA, extraia os arquivos do pacote do Gateway do ATA e execute o arquivo de Configuração do Gateway do Microsoft ATA.

    > [!NOTE]
    > Você também pode usar este pacote de Gateway do ATA para instalar novos Gateways do ATA.

1. As configurações anteriores são preservadas, mas talvez demore alguns minutos até que o serviço seja reiniciado.

1. Repita essa etapa para todos os outros Gateways do ATA implantados.

> [!NOTE]
> Depois de atualizar com êxito um Gateway do ATA, a notificação desatualizada para o Gateway do ATA específico desaparecerá.

Você saberá que todos os Gateways do ATA foram atualizados com êxito quando todos os Gateways do ATA reportarem que foram sincronizados com êxito, e a mensagem de que um pacote do Gateway do ATA atualizado está disponível não será mais exibida.

![Imagem de gateways atualizados](media/ATA-gw-updated.png)

## <a name="see-also"></a>Consulte Também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
