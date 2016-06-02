---
# required metadata

title: Instalação do ATA - Etapa 1 | Microsoft Advanced Threat Analytics
description: A primeira etapa da instalação do ATA envolve baixar e instalar o Centro do ATA em seu servidor escolhido.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalação do ATA - Etapa 1

>[!div class="step-by-step"]

[Etapa 2 »](install-ata-step2.md)

## Etapa 1. Baixar e instalar o Centro do ATA
Depois de verificar que o servidor atende aos requisitos, você pode prosseguir com a instalação do Centro do ATA.

Execute as seguintes etapas no servidor do Centro do ATA.

1.  Baixe o ATA do [Microsoft Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx) ou do [Centro de avaliação TechNet](http://www.microsoft.com/en-us/evalcenter/) ou do [MSDN](https://msdn.microsoft.com/en-us/subscriptions/downloads).

2.  Entre no computador no qual você está instalando o Centro do ATA como um usuário que seja membro do grupo Administradores local.

3.  Execute **Microsoft ATA Center Setup.EXE** e siga o assistente de instalação.

4.  Se o Microsoft .NET Framework não estiver instalado, você precisará instalá-lo ao iniciar a instalação. Você pode ter que reinicializar após a instalação do .NET Framework.
5.  Na página de **Boas-vindas**, selecione o idioma a ser usado nas telas de instalação do ATA e clique em **Avançar**.

6.  Leia os Termos de licença de software da Microsoft e, se aceitá-los, clique na caixa de seleção e em **Próximo**.

7.  É recomendável que você defina o ATA para atualizar automaticamente. Se o Windows não estiver configurado para fazer isso no seu computador, você verá a tela **Utilizar o Microsoft Update para ajudar a manter seu computador protegido e atualizado**. 
    ![Imagem Mantenha o ATA atualizado](media/ata_ms_update.png)

8. Selecione **Usar o Microsoft Update ao verificar atualizações (recomendado)** Isso ajustará as configurações do Windows para habilitar atualizações para outros produtos da Microsoft (incluindo o ATA), como visto aqui. 
    ![Imagem de atualização automática do Windows](media/ata_installupdatesautomatically.png)

8.  Na página **Configuração do Centro do ATA**, insira as informações abaixo com base em seu ambiente:

    |Campo|Descrição|Comentários|
    |---------|---------------|------------|
    |Caminho da Instalação|Esse é o local onde o Centro do ATA será instalado. Por padrão, é %programfiles%\Microsoft Advanced Threat Analytics\Center|Mantenha o valor padrão|
    |Caminho de Dados do Banco de Dados|Esse é o local onde os arquivos de banco de dados do MongoDB estarão localizados. Por padrão, é %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|Altere o local para um local onde você tem espaço para crescer com base em seu tamanho. **Observação:** <ul><li>Em ambientes de produção, você deve usar uma unidade que tenha espaço suficiente com base em um planejamento de capacidade.</li><li>Para implantações de grande porte, o banco de dados deve estar em um disco físico separado.</li></ul>Confira [Planejamento de capacidade do ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning) para obter informações sobre dimensionamento.|
    |Endereço IP do Serviço do Centro do ATA: Porta|Esse é o endereço IP que o serviço do Centro do ATA escutará a comunicação dos Gateways do ATA.<br /><br />**Porta padrão:** 443|Clique na seta para baixo para selecionar o endereço IP a ser usado pelo serviço do Centro do ATA.<br /><br />O endereço IP e a porta do serviço do Centro do ATA não podem ser iguais ao endereço IP e à porta do Console do ATA. Altere a porta do Console do ATA.|
    |Certificado SSL do Serviço do Centro do ATA|Esse é o certificado que será usado pelo serviço do Centro do ATA.|Clique no ícone de chave para selecionar um certificado instalado ou verificar o certificado autoassinado durante a implantação em um ambiente de laboratório.|
    |Endereço IP do Console do ATA|Esse é o endereço IP que será usado pelo IIS para o Console do ATA.|Clique na seta para baixo para selecionar o endereço IP a ser usado pelo Console do ATA. **Observação:** anote esse endereço IP para facilitar o acesso ao Console do ATA do Gateway do ATA.|
    |Certificado SSL do Console do ATA|Este é o certificado a ser usado pelo IIS.|Clique no ícone de chave para selecionar um certificado instalado ou verificar o certificado autoassinado durante a implantação em um ambiente de laboratório.|

    ![Imagem de configuração do Centro do ATA](media/ATA-Center-Configuration.JPG)

10.  Clique em **Instalar** para instalar o Centro do ATA e seus componentes.
    Os seguintes componentes serão instalados e configurados durante a instalação do Centro do ATA:

    -   Serviços de Informações da Internet (IIS)

    -   Site do serviço do Centro do ATA e IIS do Console do ATA

    -   MongoDB

    -   Conjunto de coleta de dados do Monitor de Desempenho Personalizado

    -   Certificados autoassinados (se tiver sido selecionado durante a instalação)

11.  Após a conclusão da instalação, clique em **Iniciar** para se conectar ao Console do ATA.
Neste ponto, você será levado automaticamente para a página de configuração **Geral** a fim de continuar a configuração e a implantação dos Gateways do ATA.
Como você está entrando no site usando um endereço IP, recebe um aviso relacionado ao certificado; isso é normal. Clique em **Continuar neste site**.

### Validar a instalação

1.  Verifique se o serviço chamado **Central do Microsoft Advanced Threat Analytics** está em execução.
2.  Na área de trabalho, clique no atalho do **Microsoft Advanced Threat Analytics** para se conectar ao Console do ATA. Faça logon com as mesmas credenciais de usuário que você usou para instalar o Centro do ATA.



>[!div class="step-by-step"]
[« Pré-instalação](preinstall-ata.md)
[Etapa 2 »](install-ata-step2.md)

## Consulte também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=May16_HO1-->


