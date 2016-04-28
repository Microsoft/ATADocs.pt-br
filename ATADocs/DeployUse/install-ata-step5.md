---
# required metadata

title: Instalação do ATA - Etapa 5 | Microsoft Advanced Threat Analytics
description: A Etapa cinco da instalação do ATA ajuda você a definir as configurações de seu Gateway do ATA.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalação do ATA - Etapa 5

>[!div class="step-by-step"]
[« Etapa 4](install-ata-step4.md)
[Etapa 6 »](install-ata-step6.md)


## Etapa 5. Definir as configurações do Gateway do ATA
Após a instalação do Gateway do ATA, execute as etapas a seguir para definir as configurações do Gateway do ATA.

1.  No computador do Gateway do ATA, no Console do ATA, clique em **Configuração** e escolha a página **Gateways do ATA**.

2.  Digite as seguintes informações.



  - **Descrição**: <br>Digite uma descrição do Gateway do ATA (opcional).
  - **Controladores de domínio** (obrigatório): <br>Saiba mais sobre a lista de controladores logo abaixo.<br>Digite o FQDN completo de seu controlador de domínio e clique no sinal de adição para acrescentá-lo à lista. Por exemplo, **dc01.contoso.com**<br /><br />![Imagem de exemplo de FQDN](media/ATAGWDomainController.png)<br>Os objetos no primeiro controlador de domínio da lista serão sincronizado por meio de consultas LDAP. Dependendo do tamanho do domínio, isso pode demorar um pouco.<br>
  **Observação:** <br>Certifique-se de que o primeiro controlador de domínio **não** seja somente leitura. Controladores de domínio somente leitura devem ser adicionados somente após a conclusão da sincronização inicial.<br>


 - **Capturar adaptadores de rede** (obrigatório):<br>Selecione os adaptadores de rede que estão conectados ao comutador e configurados como a porta de espelho de destino para receber o tráfego do controlador de domínio. | Selecione Capturar adaptador de rede.
    ![Imagem de Definir as configurações do gateway](media/ATA-Config-GW-Settings.jpg)

3.  Clique em **Salvar**.

    > [!NOTE]
    > Vai demorar alguns minutos até que o serviço do Gateway do ATA seja iniciado pela primeira vez, pois ele cria o cache dos analisadores de captura de rede usados pelo Gateway do ATA.

As informações a seguir se aplicam aos servidores digitados na lista **Controladores de Domínio**.

-   O primeiro controlador de domínio na lista será usado pelo Gateway do ATA para sincronizar os objetos no domínio por meio de consultas LDAP. Dependendo do tamanho do domínio, isso pode demorar um pouco.

-   Todos os controladores de domínio cujo tráfego esteja sendo monitorado por meio do espelhamento de porta pelo Gateway do ATA devem estar na lista **Controladores de Domínio**. Se um controlador de domínio não estiver listado em **Controladores de Domínio**, a detecção de atividades suspeitas pode não funcionar conforme o esperado.

-   Certifique-se de que o primeiro controlador de domínio **não** seja um RODC (controlador de domínio somente leitura).

    Controladores de domínio somente leitura devem ser adicionados somente após a conclusão da sincronização inicial.

-   Pelo menos um controlador de domínio na lista deve ser um servidor de catálogo global. Isso permitirá que o ATA resolva os objetos de usuário e computador em outros domínios na floresta.

As alterações de configuração serão aplicadas ao Gateway do ATA na próxima sincronização agendada entre o ele e o Centro do ATA.

### Validar a instalação:
Para validar a implantação bem-sucedida do Gateway do ATA, verifique o seguinte:

1.  Verifique se o serviço Gateway do Microsoft Advanced Threat Analytics está em execução. Depois de salvar as configurações do Gateway do ATA, talvez demore alguns minutos até que o serviço seja iniciado.

2.  Se o serviço não iniciar, examine o arquivo "Microsoft.Tri.Gateway-Errors.log" localizado na seguinte pasta padrão, "%programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs”, e procure por entradas com "transfer" ou "service start".

3.  Verifique os seguintes contadores de desempenho do Gateway do Microsoft ATA:

    -   **Mensagens Capturadas de NetworkListener / s**: este contador controla quantas mensagens estão sendo capturadas por segundo pelo ATA. O valor deve estar entre 150 e 1000, dependendo do número de controladores de domínio que está sendo monitorado e o quanto cada controlador de domínio está ocupado. Valores de dígito único ou duplo podem indicar um problema com a configuração de espelhamento de porta.

    -   **Transferências de Atividade de EntityTransfer /s**: esse valor deve estar na faixa intervalo de algumas centenas a cada alguns segundos.

4.  Se esse for o primeiro Gateway do ATA instalado, após alguns minutos, faça logon no Console do ATA e abra o painel de notificação deslizando para abrir o lado direito da tela. Você deverá ver uma lista de **Entidades Recentemente Aprendidas** na barra de notificação no lado direito do console.

5.  Para validar se a instalação foi concluída com êxito:

    No console, procure algo na barra de pesquisa, por exemplo, um usuário ou um grupo em seu domínio.

    Abra o Monitor de Desempenho. Na árvore de Desempenho, clique em **Monitor de Desempenho** e clique no ícone de adição para **Adicionar um Contador**. Expanda **Gateway do Microsoft ATA** e role para baixo até **Mensagens Capturadas pelo Ouvinte de Rede por Segundo** e adicione-o. Em seguida, verifique se a atividade aparece no gráfico.

    ![Adicionar imagem dos contadores de desempenho](media/ATA-performance-monitoring-add-counters.png)


>[!div class="step-by-step"]
[« Etapa 4](install-ata-step4.md)
[Etapa 6 »](install-ata-step6.md)

## Consulte também

- [Para obter suporte, confira nosso fórum!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurar coleta de eventos](/advanced-threat-analytics/plandesign/configure-event-collection)
- [Pré-requisitos do ATA](/advanced-threat-analytics/plandesign/ata-prerequisites)


<!--HONumber=Apr16_HO2-->


