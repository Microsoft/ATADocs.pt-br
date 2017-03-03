---
title: "Guia de migração de atualização do Advanced Threat Analytics para 1.6 | Microsoft Docs"
description: "Procedimentos para atualizar o ATA para a versão 1.6"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 0756ef64-3aef-4a69-8981-24fa8f285c6a
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: b1668f6d1d0c2107fc7116fb486d9e822552c852


---

# <a name="ata-update-to-16-migration-guide"></a>Guia de migração de atualização do ATA para 1.6
A atualização 1.6 do ATA fornece melhorias nas seguintes áreas:

-   Novas detecções

-   Aprimoramentos nas detecções existentes

-   O Gateway Lightweight do ATA

-   Atualizações automáticas

-   Melhor desempenho do Centro do ATA

-   Menos requisitos de armazenamento

-   Suporte ao IBM QRadar

## <a name="updating-ata-to-version-16"></a>Atualizando o ATA para a versão 1.6
> [!NOTE] 
> Se o ATA não estiver instalado em seu ambiente, baixe a versão completa do ATA que inclui a versão 1.6 e siga o procedimento de instalação padrão descrito em [Instalar o ATA](/advanced-threat-analytics/deploy-use/install-ata).

Se você já tiver a versão 1.5 do ATA implantada, esse procedimento explicará as etapas necessárias para atualizar sua implantação.

> [!NOTE] 
> Você não pode instalar o ATA versão 1.6 diretamente sobre o ATA versão 1.4. Instale primeiro o ATA versão 1.5. Se você tentar acidentalmente instalar o ATA 1.6 sem instalar o ATA 1.5, você obterá um erro informando que **Uma versão mais recente já está instalada no seu computador.** Desinstale os resíduos do ATA 1.6 que permanecerem no seu computador - mesmo que a instalação falhe - antes de instalar o ATA versão 1.5.

Execute estas etapas para atualizar para o ATA versão 1.6:

1. Para evitar problemas de atualização, lembre-se de seguir as etapas 8 a 10 de **Falha na migração ao atualizar para a versão 1.6 do ATA** descrito em [Novidades na versão 1.6 do ATA](whats-new-version-1.6.md).
2. Tenha certeza de que há espaço livre necessário para concluir a atualização. Você pode executar a instalação até a verificação de preparação para obter uma estimativa de quanto espaço livre é necessário e, em seguida, reiniciar a atualização depois de alocar o espaço em disco necessário.
1.  [Baixar a atualização 1.6](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
Nessa versão, o mesmo arquivo de instalação (Microsoft ATA Center Setup.exe) é usado para instalar uma nova implantação do ATA e para atualizar as implantações existentes.

2.  Atualize o Centro do ATA

3.  Baixe o pacote atualizado do Gateway do ATA

4.  Atualize os Gateways do ATA

    > [!IMPORTANT]
    > Atualize todos os Gateways do ATA para ter certeza de o ATA funciona corretamente.

### <a name="step-1-update-the-ata-center"></a>Etapa 1: Atualizar o Centro do ATA

1.  Faça backup do seu banco de dados: (opcional)

    -   Se a Central de ATA estiver sendo executada como uma máquina virtual e você quiser fazer um ponto de verificação, desligue a máquina virtual primeiro.

    -   Se a Central de ATA estiver em execução em um servidor físico, siga o procedimento recomendado para [fazer backup do MongoDB](https://docs.mongodb.org/manual/core/backups/).

2.  Execute o arquivo de instalação, Microsoft ATA Center Setup.exe, e siga as instruções na tela para instalar a atualização.

    1.  O ATA 1.6 exige o .Net Framework 4.6.1 instalado. Se ainda não estiver instalado, o ATA instalará o .NET Framework 4.6.1 como parte da configuração.
    
        > [!NOTE] 
        > A instalação do .Net Framework 4.6.1 pode exigir a reinicialização do servidor. A instalação do ATA continuará somente depois que o servidor for reiniciado.
    
    2.  Na página **Boas-vindas**, selecione seu idioma e clique em **Avançar**.

    3.  Leia o Contrato de Licença de Usuário Final e, se você aceitar os termos, clique em **Avançar**.

    4.  Agora é possível usar o Microsoft Update para manter o ATA atualizado.  Na página do Microsoft Update, selecione **Usar o Microsoft Update ao verificar se há atualizações (recomendado)**.
    ![Imagem Manter o ATA atualizado](media/ata_ms_update.png) Isso ajustará as configurações do Windows para habilitar atualizações para os outros produtos da Microsoft (incluindo o ATA), como visto aqui. 
     ![Imagem de atualização automática do Windows](media/ata_installupdatesautomatically.png)

    5.  Antes de iniciar a instalação, o ATA executará uma verificação de preparação. Examine os resultados da verificação para saber se os pré-requisitos foram configurados com êxito e se você tem pelo menos a quantidade mínima de espaço em disco. 
    ![Imagem de verificação de preparação do ATA](media/ata_install_readinesschecks.png)

    6.  Clique em **Atualizar**. Depois de clicar em Atualizar, o ATA ficará offline até que o procedimento de atualização seja concluído.

3.  Depois de atualizar a Central de ATA, os Gateways do ATA reportarão que agora estão desatualizados.

    ![Imagem de gateways desatualizados](media/ATA-center-outdated.png)

> [!IMPORTANT] 
> Atualize todos os Gateways do ATA para ter certeza de o ATA funciona corretamente.

### <a name="step-2-download-the-ata-gateway-setup-package"></a>Etapa 2. Baixe o pacote de instalação do Gateway do ATA
Após definir as configurações de conectividade do domínio, você poderá baixar o pacote de instalação do Gateway do ATA.

Para baixar o pacote do Gateway do ATA:

1.  Exclua todas as versões anteriores do pacote do Gateway do ATA baixado anteriormente.

2.  No computador do Gateway do ATA, abra um navegador e digite o endereço IP configurado no Centro do ATA para o Console do ATA. Quando o Console do ATA for aberto, clique no ícone de configurações e selecione **Configuração**.

    ![Ícone Definições de configuração](media/ATA-config-icon.JPG)

3.  Na guia **Gateways do ATA**, clique em **Baixar Instalação do Gateway do ATA**.

4.  Salve o pacote localmente.

O arquivo zip inclui o seguinte:

-   Instalador do Gateway do ATA

-   Arquivo de configurações com as informações necessárias para conectar-se à Central de ATA

### <a name="step-3-update-the-ata-gateways"></a>Etapa 3: Atualize os Gateways do ATA

1.  Em cada Gateway do ATA, extraia os arquivos do pacote do Gateway do ATA e execute o arquivo **Microsoft ATA Gateway Setup.exe**.

    > [!NOTE] 
    > Você também pode usar este pacote de Gateway do ATA para instalar novos Gateways do ATA.

2.  As configurações anteriores são preservadas, mas talvez demore alguns minutos até que o serviço seja reiniciado.

3.  Repita essa etapa para todos os outros Gateways do ATA implantados.

> [!NOTE] 
> Depois de atualizar um Gateway do ATA com êxito, a notificação desatualizada desse Gateway do ATA específico desaparecerá.

Você saberá que todos os Gateways do ATA foram atualizados com êxito quando todos os Gateways do ATA reportarem que foram sincronizados com êxito, e a mensagem de que um pacote do Gateway do ATA atualizado está disponível não será mais exibida.

![Imagem de gateways atualizados](media/ATA-gw-updated.png)


## <a name="see-also"></a>Consulte também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Feb17_HO1-->


