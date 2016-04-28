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
[« Pré-instalação](install-ata-preinstall.md)
[Etapa 2 »](install-ata-step2.md)

## Etapa 1. Baixar e instalar o Centro do ATA
Depois de verificar que o servidor atende aos requisitos, você pode prosseguir com a instalação do Centro do ATA.

Execute as seguintes etapas no servidor do Centro do ATA.

1.  Baixe o ATA do [TechNet Evaluation Center](http://www.microsoft.com/en-us/evalcenter/).

2.  Faça logon com um usuário membro do grupo de administradores locais.

3.  Em um prompt de comando elevado, execute o arquivo Microsoft ATA Center Setup.EXE e siga o assistente de instalação.

4.  Na página **Boas-vindas**, selecione seu idioma e clique em **Avançar**.

5.  Leia o Contrato de Licença de Usuário Final e, se você aceitar os termos, clique em **Avançar**.

6.  Na página **Configuração do Centro** insira as informações a seguir com base em seu ambiente:

    |Campo|Descrição|Comentários|
    |---------|---------------|------------|
    |Caminho da Instalação|Esse é o local onde o Centro do ATA será instalado. Por padrão, é %programfiles%\Microsoft Advanced Threat Analytics\Center|Mantenha o valor padrão|
    |Caminho de Dados do Banco de Dados|Esse é o local onde os arquivos de banco de dados do MongoDB estarão localizados. Por padrão, é %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|Altere o local para um local onde você tem espaço para crescer com base em seu tamanho. **Observação:** <ul><li>Em ambientes de produção, você deve usar uma unidade que tenha espaço suficiente com base em um planejamento de capacidade.</li><li>Para implantações de grande porte, o banco de dados deve estar em um disco físico separado.</li></ul>Confira [Planejamento de capacidade de ATA](/advanced-threat-analytics/PlanDesign/ata-capacity-planning) para obter informações de dimensionamento.|
    |Caminho de Diário do Banco de Dados|Esse é o local onde os arquivos de diário do banco de dados estarão localizados. Por padrão, é %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data\journal|Para implantações maiores, o Diário de Banco de Dados deve estar em um disco físico separado do banco de dados e da unidade do sistema. Altere o local para um local onde você tem espaço para seu Diário de Banco de Dados.|
    |Endereço IP do Serviço do Centro do ATA: Porta|Esse é o endereço IP que o serviço do Centro do ATA escutará a comunicação dos Gateways do ATA.<br /><br />**Porta padrão:** 443|Clique na seta para baixo para selecionar o endereço IP a ser usado pelo serviço do Centro do ATA.<br /><br />O endereço IP e a porta do serviço do Centro do ATA não podem ser iguais ao endereço IP e à porta do Console do ATA. Altere a porta do Console do ATA.|
    |Certificado SSL do Serviço do Centro do ATA|Esse é o certificado que será usado pelo serviço do Centro do ATA.|Clique no ícone de chave para selecionar um certificado instalado ou verificar o certificado autoassinado durante a implantação em um ambiente de laboratório.|
    |Endereço IP do Console do ATA|Esse é o endereço IP que será usado pelo IIS para o Console do ATA.|Clique na seta para baixo para selecionar o endereço IP a ser usado pelo Console do ATA. **Observação:** anote esse endereço IP para facilitar o acesso ao Console do ATA do Gateway do ATA.|
    |Certificado SSL do Console do ATA|Este é o certificado a ser usado pelo IIS.|Clique no ícone de chave para selecionar um certificado instalado ou verificar o certificado autoassinado durante a implantação em um ambiente de laboratório.|
    ![Imagem de configuração do Centro do ATA](media/ATA-Center-Configuration.JPG)

7.  Clique em **Instalar** para instalar o ATA e seus componentes e criar a conexão entre o Centro do ATA e o Console do ATA.

8.  Após a conclusão da instalação, clique em **Iniciar** para se conectar ao Console do ATA.

    Os seguintes componentes serão instalados e configurados durante a instalação do Centro do ATA:

    -   Serviços de Informações da Internet (IIS)

    -   MongoDB

    -   Site do serviço do Centro do ATA e IIS do Console do ATA

    -   Conjunto de coleta de dados do Monitor de Desempenho Personalizado

    -   Certificados autoassinados (se tiver sido selecionado durante a instalação)

> [!NOTE]
> Para ajudar na solução de problemas e aprimoramento do produto, recomendamos a instalação do MongoVue e qualquer outro suplemento do MongoDB, ou qualquer outra ferramenta de terceiros de sua escolha. O MongoVue exige o .Net Framework 3.5 instalado.

### Validar a instalação

1.  Verifique se o serviço Centro do Microsoft Advanced Threat Analytics está em execução.

2.  Na área de trabalho, clique no atalho do Microsoft Advanced Threat Analytics para se conectar ao Console do ATA. Faça logon com as mesmas credenciais de usuário que você usou para instalar o Centro do ATA. Na primeira vez que você efetuar logon no Console do ATA, será levado automaticamente para a página **Configurações de conectividade do domínio** para continuar a configuração e a implantação dos Gateways do ATA.

3.  Examine o arquivo de erro no arquivo **Microsoft.Tri.Center-Errors.log** que pode ser encontrado no seguinte local padrão: %programfiles%\Microsoft Advanced Threat Analytics\Center\Logs.

>[!div class="step-by-step"]
[« Pré-instalação](install-ata-preinstall.md)
[Etapa 2 »](install-ata-step2.md)

## Consulte também

- [Para obter suporte, confira nosso fórum!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurar coleta de eventos](/advanced-threat-analytics/plandesign/configure-event-collection)
- [Pré-requisitos do ATA](/advanced-threat-analytics/plandesign/ata-prerequisites)


<!--HONumber=Apr16_HO2-->


