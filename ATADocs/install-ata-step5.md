---
title: "Instalação do Advanced Threat Analytics – Etapa 5 | Microsoft Docs"
description: "A Etapa cinco da instalação do ATA ajuda você a definir as configurações de seu Gateway do ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/20/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ff0de9755c4023d0245c6af8b7a29d505b4f4664
ms.sourcegitcommit: 129bee06ff89b72d21b64f9aa0d1a29f66bf9153
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*



# <a name="install-ata---step-5"></a>Instalação do ATA - Etapa 5

>[!div class="step-by-step"]
[« Etapa 4](install-ata-step4.md)
[Etapa 6 »](install-ata-step6.md)


## <a name="step-5-configure-the-ata-gateway-settings"></a>Etapa 5. Definir as configurações do Gateway do ATA
Após a instalação do Gateway do ATA, execute as etapas a seguir para definir as configurações do Gateway do ATA.

1.  No Console do ATA, acesse **Configuração** e, em **Sistema**, selecione **Gateways**.
   
     ![Imagem de definição das configurações do gateway](media/ata-gw-config-1.png)


2.  Clique no Gateway que você deseja configurar e insira as seguintes informações:

    ![Imagem de definição das configurações do gateway](media/ATA-Gateways-config-2.png)

  - **Descrição**: insira uma descrição para o Gateway do ATA (opcional).
  - **Controladores de Domínio com porta espelhada (FQDN)** (exigidos para o Gateway do ATA, isso não pode ser alterado para o Gateway Lightweight do ATA): insira o FQDN completo de seu controlador de domínio e clique no sinal de adição para adicioná-lo à lista. Por exemplo, **dc01.contoso.com**

      As informações a seguir se aplicam aos servidores digitados na lista **Controladores de Domínio**:
      - Todos os controladores de domínio cujo tráfego esteja sendo monitorado por meio do espelhamento de porta pelo Gateway do ATA devem estar na lista **Controladores de Domínio**. Se um controlador de domínio não estiver listado em **Controladores de Domínio**, a detecção de atividades suspeitas pode não funcionar conforme o esperado.
      - Pelo menos um controlador de domínio na lista deve ser um catálogo global. Isso permitirá que o ATA resolva os objetos de usuário e computador em outros domínios na floresta.

  - **Capturar adaptadores de rede** (obrigatório):
  - Para um Gateway do ATA em um servidor dedicado, selecione os adaptadores de rede que são configurados como a porta de espelho do destino. Eles receberão o tráfego do controlador de domínio espelhado.
  - Para um Gateway Lightweight do ATA, trata-se de todos os adaptadores de rede que são usados para comunicação com outros computadores da organização.


  - **Candidato ao sincronizador de domínio**: qualquer Gateway do ATA definido para ser um candidato ao sincronizador de domínio pode ser responsável pela sincronização entre o ATA e o domínio do Active Directory. Dependendo do tamanho do domínio, a sincronização inicial pode ser demorada e consumir muitos recursos. Por padrão, somente Gateways do ATA são definidos como Candidatos ao sincronizador do domínio.
   É recomendável impedir os Gateways do ATA do site remoto de serem candidatos ao sincronizador do domínio.
   Se o controlador de domínio for somente leitura, não o defina como um candidato ao sincronizador do domínio. Para saber mais, confira [Arquitetura do ATA](ata-architecture.md#ata-lightweight-gateway-features).

  > [!NOTE] 
  > Levará alguns minutos para que o serviço do Gateway do ATA inicie pela primeira vez após a instalação, pois ele cria o cache dos analisadores de captura de rede.
  > As alterações de configuração serão aplicadas ao Gateway do ATA na próxima sincronização agendada entre o ele e o Centro do ATA.

3. Se desejar, é possível definir o [Ouvinte do syslog e o Conjunto de Encaminhamento de Eventos do Windows](configure-event-collection.md). 
4. Habilite **Atualizar Gateway do ATA automaticamente** para que nos lançamentos de versões futuras, quando você atualizar o Centro do ATA, esse Gateway do ATA seja atualizado automaticamente.

5. Clique em **Salvar**.


## <a name="validate-installations"></a>Validar instalações
Para validar a implantação bem-sucedida do Gateway do ATA, verifique o seguinte:

1.  Verifique se o serviço nomeado **Gateway do Microsoft Advanced Threat Analytics** está em execução. Depois de salvar as configurações do Gateway do ATA, talvez demore alguns minutos até que o serviço seja iniciado.

2.  Se o serviço não iniciar, examine o arquivo "Microsoft.Tri.Gateway-Errors.log" localizado na pasta padrão "%programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs" e confira [Solução de problemas do ATA](troubleshooting-ata-known-errors.md) para obter ajuda.

3.  Se esse for o primeiro Gateway do ATA instalado, após alguns minutos, faça logon no Console do ATA e abra o painel de notificação deslizando para abrir o lado direito da tela. Você deverá ver uma lista de **Entidades Recentemente Aprendidas** na barra de notificação no lado direito do console.

4.  Na área de trabalho, clique no atalho do **Microsoft Advanced Threat Analytics** para se conectar ao Console do ATA. Faça logon com as mesmas credenciais de usuário que você usou para instalar o Centro do ATA.
5.  No console, procure algo na barra de pesquisa, por exemplo, um usuário ou um grupo em seu domínio.
6.  Abra o Monitor de Desempenho. Na árvore de Desempenho, clique em **Monitor de Desempenho** e clique no ícone de adição para **Adicionar um Contador**. Expanda **Gateway do Microsoft ATA** e role para baixo até **Mensagens Capturadas PEF do Ouvinte de Rede/s** e adicione-o. Em seguida, verifique se a atividade aparece no gráfico.

    ![Adicionar imagem dos contadores de desempenho](media/ATA-performance-monitoring-add-counters.png)


>[!div class="step-by-step"]
[« Etapa 4](install-ata-step4.md)
[Etapa 6 »](install-ata-step6.md)



## <a name="related-videos"></a>Vídeos Relacionados
- [Como escolher o tipo certo de Gateway do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Consulte também
- [Guia de implantação da POC (prova de conceito) do ATA](http://aka.ms/atapoc)
- [Ferramenta de dimensionamento do ATA](http://aka.ms/atasizingtool)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)

