---
title: Instalar o Advanced Threat Analytics-etapa 5
description: A Etapa cinco da instalação do ATA ajuda você a definir as configurações de seu Gateway do ATA.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 6bcb99a86cfab977ec6a1ab590313a7878e9e4e2
ms.sourcegitcommit: 5bf0c6a204b71126306a0c64108eaf9cb7fc042f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/18/2021
ms.locfileid: "101097480"
---
# <a name="install-ata---step-5"></a>Instalação do ATA - Etapa 5

[!INCLUDE [Banner for top of topics](includes/banner.md)]

> [!div class="step-by-step"]
> [«Etapa 4](install-ata-step4.md) 
>  [Etapa 6»](install-ata-step6.md)

## <a name="step-5-configure-the-ata-gateway-settings"></a>Etapa 5. Definir as configurações do Gateway do ATA

Após a instalação do Gateway do ATA, execute as etapas a seguir para definir as configurações do Gateway do ATA.

1. No Console do ATA, acesse **Configuração** e, em **Sistema**, selecione **Gateways**.

    ![Definir configurações de gateway fase 1](media/ata-gw-config-1.png)

1. Clique no Gateway que você deseja configurar e insira as seguintes informações:

    ![Definir configurações de gateway fase 2](media/ATA-Gateways-config-2.png)

    - **Descrição**: insira uma descrição para o Gateway do ATA (opcional).
    - **Controladores de Domínio com porta espelhada (FQDN)** (exigidos para o Gateway do ATA, isso não pode ser alterado para o Gateway Lightweight do ATA): insira o FQDN completo de seu controlador de domínio e clique no sinal de adição para adicioná-lo à lista. Por exemplo, **dc01.contoso.com**

    As informações a seguir se aplicam aos servidores digitados na lista **Controladores de Domínio**:

    - Todos os controladores de domínio cujo tráfego esteja sendo monitorado por meio do espelhamento de porta pelo Gateway do ATA devem estar na lista **Controladores de Domínio**. Se um controlador de domínio não estiver listado em **Controladores de Domínio**, a detecção de atividades suspeitas pode não funcionar conforme o esperado.
    - Pelo menos um controlador de domínio na lista deve ser um catálogo global. Isso permite que o ATA resolva os objetos de usuário e computador em outros domínios na floresta.

    - **Capturar adaptadores de rede** (obrigatório):
    - Para um Gateway do ATA em um servidor dedicado, selecione os adaptadores de rede que são configurados como a porta de espelho do destino. Eles recebem o tráfego do controlador de domínio espelhado.
    - Para um Gateway Lightweight do ATA, trata-se de todos os adaptadores de rede que são usados para comunicação com outros computadores da organização.

    - **Candidato ao sincronizador de domínio**: qualquer Gateway do ATA definido para ser um candidato ao sincronizador de domínio pode ser responsável pela sincronização entre o ATA e o domínio do Active Directory. Dependendo do tamanho do domínio, a sincronização inicial pode ser demorada e consumir muitos recursos. Por padrão, somente Gateways do ATA são definidos como Candidatos ao sincronizador do domínio.
    É recomendável impedir que os Gateways do ATA do site remoto sejam candidatos ao Sincronizador de domínio.
    Se o controlador de domínio for somente leitura, não o defina como um candidato ao sincronizador do domínio. Para obter mais informações, consulte [arquitetura do ATA](ata-architecture.md#ata-lightweight-gateway-features).

    > [!NOTE]
    > Levará alguns minutos para que o serviço do Gateway do ATA inicie pela primeira vez após a instalação, pois ele cria o cache dos analisadores de captura de rede.
    > As alterações de configuração são aplicadas ao Gateway do ATA na próxima sincronização agendada entre o ele e o Centro do ATA.

1. Se desejar, é possível definir o [Ouvinte do syslog e o Conjunto de Encaminhamento de Eventos do Windows](configure-event-collection.md).
1. Habilite **Atualizar Gateway do ATA automaticamente** para que nos lançamentos de versões futuras, quando você atualizar o Centro do ATA, esse Gateway do ATA seja atualizado automaticamente.

1. Clique em **Salvar**.

## <a name="validate-installations"></a>Validar instalações

Para validar a implantação bem-sucedida do Gateway do ATA, verifique as seguintes etapas:

1. Verifique se o serviço nomeado **Gateway do Microsoft Advanced Threat Analytics** está em execução. Depois de salvar as configurações do Gateway do ATA, talvez demore alguns minutos até que o serviço seja iniciado.

1. Se o serviço não for iniciado, examine o arquivo "Microsoft. Tri. gateway-Errors. log" localizado na seguinte pasta padrão, "%programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs" e verifique a [solução de problemas do ATA](troubleshooting-ata-known-errors.md) para obter ajuda.

1. Se esse for o primeiro Gateway do ATA instalado, após alguns minutos, faça logon no Console do ATA e abra o painel de notificação deslizando para abrir o lado direito da tela. Você deverá ver uma lista de **Entidades Recentemente Aprendidas** na barra de notificação no lado direito do console.

1. Na área de trabalho, clique no atalho do **Microsoft Advanced Threat Analytics** para conectar-se ao console do ATA. Faça logon com as mesmas credenciais de usuário que você usou para instalar o Centro do ATA.
1. No console, procure algo na barra de pesquisa, por exemplo, um usuário ou um grupo em seu domínio.
1. Abra o Monitor de Desempenho. Na árvore de Desempenho, clique em **Monitor de Desempenho** e clique no ícone de adição para **Adicionar um Contador**. Expanda **Gateway do Microsoft ATA** e role para baixo até **Mensagens Capturadas PEF do Ouvinte de Rede/s** e adicione-o. Em seguida, verifique se a atividade aparece no gráfico.

    ![Adicionar imagem dos contadores de desempenho](media/ATA-performance-monitoring-add-counters.png)

### <a name="set-anti-virus-exclusions"></a>Definir as exclusões de antivírus

Depois de instalar o gateway do ATA, exclua o diretório do ATA de ser continuamente examinado por seu aplicativo antivírus. O local padrão no banco de dados é: **c:\Arquivos de Programas\microsoft Advanced \* Threat Analytics*.

Certifique-se também de excluir os seguintes processos da verificação de AV:

**Processos**  
Microsoft.Tri.Gateway.exe  
Microsoft.Tri.Gateway.Updater.exe

Se você instalou o ATA em um diretório diferente, não deixe de alterar os caminhos de pasta de acordo com a sua instalação.

> [!div class="step-by-step"]
> [«Etapa 4](install-ata-step4.md) 
>  [Etapa 6»](install-ata-step6.md)

## <a name="related-videos"></a>Vídeos Relacionados

- [Visão geral da implantação do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Como escolher o tipo certo de Gateway do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>Consulte Também

- [Guia de implantação da POC (prova de conceito) do ATA](/samples/browse/?redirectedfrom=TechNet-Gallery)
- [Ferramenta de dimensionamento do ATA](https://aka.ms/atasizingtool)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)