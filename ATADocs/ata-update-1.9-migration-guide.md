---
title: Guia de migração de atualização do Advanced Threat Analytics para 1.9 | Microsoft Docs
description: Procedimentos para atualizar o ATA para a versão 1.9
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 03/25/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b970f5e8472c58fa87a078d8b8612a4dbc86e388
ms.sourcegitcommit: 0f3ee3241895359d5cecd845827cfba1fdca9317
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/29/2019
ms.locfileid: "75543789"
---
# <a name="updating-ata-to-version-19"></a>Atualizando o ATA para a versão 1.9

> [!NOTE] 
> Se o ATA não estiver instalado em seu ambiente, baixe a versão completa do ATA que inclui a versão 1.9 e siga o procedimento de instalação padrão descrito em [Instalar o ATA](install-ata-step1.md).

Se você já tiver a versão 1.8 do ATA implantada, esse procedimento explicará as etapas necessárias para atualizar sua implantação.

> [!NOTE] 
>  Somente o ATA versão 1.8 (1.8.6645) e o ATA 1.8 atualização 1 (1.8.6765) podem ser atualizados para a versão 1.9 do ATA. Nenhuma outra versão anterior do ATA poderá ser atualizada diretamente para a versão 1.9.

Siga estas etapas para atualizar para o ATA versão 1.9:

1.  [Baixe a versão de atualização do ATA 1.9 no Centro de Download](https://www.microsoft.com/download/details.aspx?id=56725) ou a versão completa no [Centro de Avaliação](https://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).<br>
Na versão de migração, o arquivo pode ser usado apenas para a atualização do ATA 1.8. Na versão do Centro de Avaliação, o mesmo arquivo de instalação (Microsoft ATA Center Setup.exe) é usado para instalar uma nova implantação do ATA e para atualizar as implantações existentes.

2.  Atualize o Centro do ATA

4.  Atualize os Gateways do ATA

    > [!IMPORTANT]
    > Atualize todos os Gateways do ATA para ter certeza de o ATA funciona corretamente.

### <a name="step-1-update-the-ata-center"></a>Etapa 1: Atualizar o Centro do ATA

1. Faça backup do seu banco de dados: (opcional)

   -   Se a Central de ATA estiver sendo executada como uma máquina virtual e você quiser fazer um ponto de verificação, desligue a máquina virtual primeiro.

   -   Se o Centro do ATA estiver em execução em um servidor físico, consulte o artigo sobre [recuperação de desastre](disaster-recovery.md) para obter informações sobre como fazer backup do banco de dados.

2. Execute o arquivo de instalação, **Microsoft ATA Center Setup.exe**, e siga as instruções na tela para instalar a atualização.

   - Na página **Boas-vindas**, escolha seu idioma e clique em **Avançar**.

   - Se você não tiver habilitado as atualizações automáticas na versão 1.8, será necessário definir o ATA para usar o Microsoft Update para que ele permaneça atualizado.  Na página do Microsoft Update, selecione **Usar o Microsoft Update ao verificar se há atualizações (recomendado)** .
     ![Imagem Manter o ATA atualizado](media/ata_ms_update.png)
     
     Isso ajusta as configurações do Windows para habilitar as atualizações para o ATA. 
    
   - A tela **Migração parcial de dados** permite que você saiba se os dados capturados anteriormente relacionados ao tráfego de rede, aos eventos, às entidades e à detecção foram excluídos. Todas as detecções funcionam de maneira imediata, com exceção da detecção de comportamento anormal, da modificação anormal de grupo, do reconhecimento usando os serviços de diretório (SAM-R) e das detecções de downgrade de criptografia, que demoram até três semanas para a criação de um perfil completo após o tempo de aprendizado necessário. 
     
     ![Migração parcial do ATA](media/partial-migration.png)

   - Clique em **Atualizar**. Depois de clicar em Atualizar, o ATA ficará offline até que o procedimento de atualização seja concluído.

3. Após a conclusão da atualização do Centro do ATA, clique em **Iniciar** para abrir a tela **Atualizar** no console do ATA para os Gateways do ATA.

    ![Tela de sucesso da atualização](media/migration-center-success.png)

4. Na tela **Atualizações**, se você já tiver configurado seus Gateways do ATA para atualizarem automaticamente, eles serão atualizados agora, caso contrário, clique em **Atualizar** ao lado de cada Gateway do ATA.
  
    ![Imagem de atualização dos gateways](media/migration-update-gw.png)

  
> [!IMPORTANT] 
> Atualize todos os Gateways do ATA para ter certeza de o ATA funciona corretamente.
 
> [!NOTE] 
> Para instalar novos gateways do ATA, acesse a tela **gateways** e clique em **baixar a instalação do gateway** para obter o pacote de instalação do gateway 1,9 do ATA e siga as instruções para nova instalação do gateway, conforme descrito na [etapa 4. Instale o gateway do ATA](install-ata-step4.md).


## <a name="see-also"></a>Confira Também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
