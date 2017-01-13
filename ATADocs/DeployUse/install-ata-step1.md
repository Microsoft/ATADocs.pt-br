---
title: "Instalar o ATA – Etapa 1 | Microsoft Docs"
description: "A primeira etapa da instalação do ATA envolve baixar e instalar o Centro do ATA em seu servidor escolhido."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b73fb769438a7290053c27766c233010079dca78
ms.openlocfilehash: 313ae02742d4acc68c52d5481fdc24c0aa508681


---

*Aplica-se a: Advanced Threat Analytics versão 1.7*



# <a name="install-ata---step-1"></a>Instalação do ATA - Etapa 1

>[!div class="step-by-step"]
[Etapa 2 »](install-ata-step2.md)

O procedimento de instalação fornece instruções para executar uma nova instalação do ATA 1.7. Para saber mais sobre como atualizar uma implantação do ATA existente de uma versão anterior, confira [Guia de migração do ATA versão 1.7](/advanced-threat-analytics/understand-explore/ata-update-1.7-migration-guide).

> [!IMPORTANT] 
> Se você estiver usando o Windows 2012 R2, instale o KB2934520 no servidor da Central do ATA e nos servidores do Gateway do ATA antes de começar a instalação, caso contrário a instalação do ATA instalar essa atualização e exigirá uma reinicialização no meio do processo.

## <a name="step-1-download-and-install-the-ata-center"></a>Etapa 1. Baixar e instalar o Centro do ATA
Depois de verificar que o servidor atende aos requisitos, você pode prosseguir com a instalação do Centro do ATA.

Execute as seguintes etapas no servidor do Centro do ATA.

1.  Baixe o ATA no [Centro de Serviços de Licenciamento por Volume da Microsoft](https://www.microsoft.com/Licensing/servicecenter/default.aspx), no [Centro de avaliação do TechNet](http://www.microsoft.com/evalcenter/) ou no [MSDN](https://msdn.microsoft.com/subscriptions/downloads).

2.  Entre no computador no qual você está instalando o Centro do ATA como um usuário que seja membro do grupo Administradores local.

3.  Execute **Microsoft ATA Center Setup.EXE** e siga o assistente de instalação.

> [!NOTE]   
> Certifique-se de executar o arquivo de instalação de uma unidade local e não de um arquivo ISO montado para evitar problemas, caso uma reinicialização seja necessária como parte da instalação.   

4.  Se o Microsoft .NET Framework não estiver instalado, você precisará instalá-lo ao iniciar a instalação. Você pode ter que reinicializar após a instalação do .NET Framework.
5.  Na página de **Boas-vindas**, selecione o idioma a ser usado nas telas de instalação do ATA e clique em **Avançar**.

6.  Leia os Termos de Licença para Software Microsoft e, se aceitá-los, clique na caixa de seleção e em **Avançar**.

7.  É recomendável que você defina o ATA para atualizar automaticamente. Se o Windows não estiver configurado para fazer isso no seu computador, você verá a tela **Utilizar o Microsoft Update para ajudar a manter seu computador protegido e atualizado**. 
    ![Imagem Manter o ATA atualizado](media/ata_ms_update.png)

8. Selecione **Usar o Microsoft Update ao verificar atualizações (recomendado)** Isso ajustará as configurações do Windows para habilitar atualizações para outros produtos da Microsoft (incluindo o ATA), como visto aqui. 
    ![Imagem de atualização automática do Windows](media/ata_installupdatesautomatically.png)

8.  Na página **Configuração do Centro do ATA**, insira as informações abaixo com base em seu ambiente:

    |Campo|Descrição|Comentários|
    |---------|---------------|------------|
    |Caminho da Instalação|Esse é o local onde o Centro do ATA será instalado. Por padrão, é %programfiles%\Microsoft Advanced Threat Analytics\Center|Mantenha o valor padrão|
    |Caminho de Dados do Banco de Dados|Esse é o local onde os arquivos de banco de dados do MongoDB estarão localizados. Por padrão, é %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|Altere o local para um local onde você tem espaço para crescer com base em seu tamanho. **Observação:** <ul><li>Em ambientes de produção, você deve usar uma unidade que tenha espaço suficiente com base em um planejamento de capacidade.</li><li>Para implantações de grande porte, o banco de dados deve estar em um disco físico separado.</li></ul>Confira [Planejamento de capacidade do ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning) para obter informações sobre dimensionamento.|
    |Endereço IP do Serviço da Central: Porta|Esse é o endereço IP que o serviço do Centro do ATA escutará a comunicação dos Gateways do ATA.<br /><br />**Porta padrão:** 443|Clique na seta para baixo para selecionar o endereço IP a ser usado pelo serviço do Centro do ATA.<br /><br />O endereço IP e a porta do serviço do Centro do ATA não podem ser iguais ao endereço IP e à porta do Console do ATA. Altere a porta do Console do ATA.|
    |Certificado SSL do Serviço da Central|Esse é o certificado que será usado pelo serviço da Central do ATA e pelo Console do ATA.|Clique no ícone de chave para selecionar um certificado instalado ou verificar o certificado autoassinado durante a implantação em um ambiente de laboratório.|
    |Endereço IP do Console|Esse é o endereço IP que será usado para o Console do ATA.|Clique na seta para baixo para selecionar o endereço IP a ser usado pelo Console do ATA. **Observação:** anote esse endereço IP para facilitar o acesso ao Console do ATA do Gateway do ATA.|
    
    ![Imagem de configuração do Centro do ATA](media/ATA-Center-Configuration.png)

10.  Clique em **Instalar** para instalar o Centro do ATA e seus componentes.
    Os seguintes componentes serão instalados e configurados durante a instalação do Centro do ATA:

    -   Serviço da Central do ATA

    -   MongoDB

    -   Conjunto de coleta de dados do Monitor de Desempenho Personalizado

    -   Certificados autoassinados (se tiver sido selecionado durante a instalação)

11.  Após a conclusão da instalação, clique em **Iniciar** para se conectar ao Console do ATA.
Neste ponto, você será levado automaticamente para a página de configuração **Geral** a fim de continuar a configuração e a implantação dos Gateways do ATA.
Como você está fazendo logon no site usando um endereço IP, você recebe um aviso relacionado ao certificado e isso é normal. Clique em **Continuar neste site**.

### <a name="validate-installation"></a>Validar a instalação

1.  Verifique se o serviço chamado **Central do Microsoft Advanced Threat Analytics** está em execução.
2.  Na área de trabalho, clique no atalho do **Microsoft Advanced Threat Analytics** para se conectar ao Console do ATA. Faça logon com as mesmas credenciais de usuário que você usou para instalar o Centro do ATA.



>[!div class="step-by-step"]
[« Pré-instalação](configure-port-mirroring.md)
[Etapa 2 »](install-ata-step2.md)

## <a name="see-also"></a>Consulte Também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Jan17_HO2-->


