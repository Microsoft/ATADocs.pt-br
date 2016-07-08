---
title: "Instalação do ATA - Etapa 5 | Microsoft Advanced Threat Analytics"
description: "A Etapa cinco da instalação do ATA ajuda você a definir as configurações de seu Gateway do ATA."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d6e7d7bef97bfc4ffde07959dd9256f0319d685f
ms.openlocfilehash: 6400a0eabefac91b418e00eb670b1329fa1b5fb5


---

# Instalação do ATA - Etapa 5

>[!div class="step-by-step"]
[« Etapa 4](install-ata-step4.md)
[Etapa 6 »](install-ata-step6.md)


## Etapa 5. Definir as configurações do Gateway do ATA
Após a instalação do Gateway do ATA, execute as etapas a seguir para definir as configurações do Gateway do ATA.

1.  No Console do ATA, clique em **Configuração** e selecione a página **Gateways do ATA**.

2.  Digite as seguintes informações.

  - **Descrição**: <br>Digite uma descrição do Gateway do ATA (opcional).
  - **Controladores de Domínio Espelhados da Porta (FQDN)** (obrigatórios para o Gateway do ATA; não podem ser definidos para o Gateway Lightweight do ATA): <br>Digite o FQDN completo de seu controlador de domínio e clique no sinal de adição para acrescentá-lo à lista. Por exemplo, **dc01.contoso.com**<br /><br />![Imagem de exemplo do FQDN](media/ATAGWDomainController.png)

As informações a seguir se aplicam aos servidores que você insere na lista **Controladores de Domínio**: -   Todos os controladores de domínio cujo tráfego está sendo monitorado por meio do espelhamento de porta pelo Gateway do ATA devem ser listados na lista **Controladores de Domínio**. Se um controlador de domínio não estiver listado em **Controladores de Domínio**, a detecção de atividades suspeitas pode não funcionar conforme o esperado.
-   Pelo menos um controlador de domínio na lista deve ser um servidor de catálogo global. Isso permitirá que o ATA resolva os objetos de usuário e computador em outros domínios na floresta.

 - **Capturar adaptadores de rede** (obrigatório):<br>
     - Para um Gateway do ATA em um servidor dedicado, selecione os adaptadores de rede que são configurados como a porta de espelho do destino. Eles receberão o tráfego do controlador de domínio espelhado.
     - Para um Gateway Lightweight do ATA, trata-se de todos os adaptadores de rede que são usados para comunicação com outros computadores da organização.

![Imagem de definição das configurações do gateway](media/ATA-Config-GW-Settings.jpg)

 - **Candidato ao sincronizador de domínio**<br>
Qualquer Gateway do ATA definido para ser um candidato ao sincronizador de domínio pode ser responsável pela sincronização entre o ATA e o domínio do Active Directory. Dependendo do tamanho do domínio, a sincronização inicial pode ser demorada e consumir muitos recursos. Por padrão, somente Gateways do ATA são definidos como candidatos ao sincronizador do domínio. <br>É recomendável impedir os Gateways do ATA do site remoto de serem candidatos ao sincronizador do domínio.<br>Se o controlador de domínio for somente leitura, não o defina como um candidato ao sincronizador do domínio. Para saber mais, confira [ATA architecture](/advanced-threat-analytics/plan-design/ata-architecture#ata-lightweight-gateway-features) (Arquitetura do ATA).

> [!NOTE] 
> Levará alguns minutos para que o serviço do Gateway do ATA inicie pela primeira vez, pois ele cria o cache dos analisadores de captura de rede.<br>
> As alterações de configuração serão aplicadas ao Gateway do ATA na próxima sincronização agendada entre o ele e o Centro do ATA.



    

3. Se desejar, é possível definir o [Ouvinte do syslog e o Conjunto de Encaminhamento de Eventos do Windows](configure-event-collection.md). 
4. Habilite **Atualizar Gateway do ATA automaticamente** para que nos lançamentos de versões futuras, quando você atualizar o Centro do ATA, esse Gateway do ATA seja atualizado automaticamente.
3.  Clique em **Salvar**.


## Validar instalações
Para validar a implantação bem-sucedida do Gateway do ATA, verifique o seguinte:

1.  Verifique se o serviço nomeado **Gateway do Microsoft Advanced Threat Analytics** está em execução. Depois de salvar as configurações do Gateway do ATA, talvez demore alguns minutos até que o serviço seja iniciado.

2.  Se o serviço não iniciar, examine o arquivo "Microsoft.Tri.Gateway-Errors.log" localizado na pasta padrão "%programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs".

3.  Confira a [Solução de problemas do ATA](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-known-errors) para obter ajuda.

4.  Se esse for o primeiro Gateway do ATA instalado, após alguns minutos, faça logon no Console do ATA e abra o painel de notificação deslizando para abrir o lado direito da tela. Você deverá ver uma lista de **Entidades Recentemente Aprendidas** na barra de notificação no lado direito do console.

5.  Na área de trabalho, clique no atalho do **Microsoft Advanced Threat Analytics** para se conectar ao Console do ATA. Faça logon com as mesmas credenciais de usuário que você usou para instalar o Centro do ATA.
6.  No console, procure algo na barra de pesquisa, por exemplo, um usuário ou um grupo em seu domínio.
7.  Abra o Monitor de Desempenho. Na árvore de Desempenho, clique em **Monitor de Desempenho** e clique no ícone de adição para **Adicionar um Contador**. Expanda **Gateway do Microsoft ATA** e role para baixo até **Mensagens Capturadas PEF do Ouvinte de Rede/s** e adicione-o. Em seguida, verifique se a atividade aparece no gráfico.

    ![Adicionar imagem dos contadores de desempenho](media/ATA-performance-monitoring-add-counters.png)


>[!div class="step-by-step"]
[« Etapa 4](install-ata-step4.md)
[Etapa 6 »](install-ata-step6.md)

## Consulte também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Jun16_HO4-->


