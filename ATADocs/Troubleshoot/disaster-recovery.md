---
title: "Recuperação de desastre para o Advanced Threat Analytics | Microsoft Docs"
description: "Descreve como você pode recuperar rapidamente a funcionalidade do ATA após desastres"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 02/28/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 7620e171-76d5-4e3f-8b03-871678217a3a
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: e315e9731fa9715c3b41b9292349ee5aca13fbce
ms.sourcegitcommit: 4f5927f30089655e3984d69623ea4439b7c36845
translationtype: HT
---
*Aplica-se a: Advanced Threat Analytics versão 1.7*



# <a name="ata-disaster-recovery"></a>Recuperação de desastre de ATA
Este artigo descreve como recuperar rapidamente seu Centro de ATA e restaurar a funcionalidade do ATA quando a funcionalidade do Centro de ATA for perdida, mas os Gateways de ATA ainda estiverem funcionando. 

>[!NOTE]
> O processo descrito não recupera atividades suspeitas detectadas anteriormente, mas retorna o Centro de ATA à funcionalidade completa. Além disso, o período de aprendizado necessário para algumas detecções comportamentais reiniciará, mas a maior parte da detecção que o ATA oferece estará funcionando depois que o Centro de ATA estiver restaurado. 

## <a name="back-up-your-ata-center-configuration"></a>Fazer backup da sua configuração do Centro de ATA

1. A configuração do Centro de ATA é armazenada em backup em um arquivo a cada hora. Localize a última cópia de backup da configuração do Centro de ATA e salve-a em um computador à parte. Para obter uma explicação completa de como localizar esses arquivos, confira [Exportar e importar a configuração de ATA](/advanced-threat-analytics/deploy-use/ata-configuration-file). 
2. Exportação do certificado do Centro de ATA.
    1. No gerenciador de certificados (`certlm.msc`), navegue até **Certificados (Computador Local)** -> **Pessoal** ->**Certificados** e selecione **Centro de ATA**.
    2. Clique com o botão direito em **Centro de ATA** e selecione **Todas as Tarefas** e, em seguida, **Exportar**. 
     ![Certificado do Centro de ATA](media/ata-center-cert.png)
    3. Siga as instruções para exportar o certificado, certificando-se de exportar também a chave privada.
    4. Faça o backup do arquivo de certificado exportado em um computador separado.

  > [!NOTE] 
  > Se você não puder exportar a chave privada, você deve criar um novo certificado e implantá-lo no ATA, conforme descrito em [Alteração do certificado do Centro de ATA](/advanced-threat-analytics/deploy-use/modifying-ata-config-centercert) e, em seguida, exportá-la. 

## <a name="recover-your-ata-center"></a>Recuperar seu Centro de ATA

1. Crie uma nova máquina do Windows Server usando o mesmo nome de computador e o endereço IP da máquina anterior do Centro de ATA.
4. Importe o certificado que você armazenou em backup acima para o novo servidor.
5. Siga as instruções para [Implantar o Centro de ATA](/advanced-threat-analytics/deploy-use/install-ata-step1) no Windows Server recém-criado. Verifique se você selecionou o mesmo endereço IP e porta do centro antigo. Não é necessário implantar os Gateways do ATA novamente. Quando for solicitado um certificado, forneça o certificado exportado durante o backup da configuração do Centro de ATA. 
![Restauração do Centro de ATA](media/ata-center-restore.png)
6. Importe a configuração do Centro de ATA armazenada em backup:
    1. Remova o documento padrão do Perfil do Sistema do Centro de ATA do MongoDB: 
        1. Acesse **C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**. 
        2. Execute `mongo.exe ATA` 
        3. Execute este comando para remover o perfil do sistema padrão: `db.SystemProfile.remove({})`
    2. Execute o comando: `mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert` usando o arquivo de backup da etapa 1.</br>
    Para obter uma explicação completa de como localizar e importar arquivos de backup, confira [Exportar e importar a configuração de ATA](/advanced-threat-analytics/deploy-use/ata-configuration-file). 
    3. Após a importação, execute este comando para remover alguns dos perfis do sistema padrão (para redefini-los para o novo ambiente): `db.SystemProfile.remove({$or:[{"_t":"DetectorProfile"}, "_t":"DirectoryServicesSystemProfile"}]}) `
    4. Abra o Console do ATA. Você deverá ver todos os Gateways do ATA vinculados na guia Configuração/Gateways. 
    5. Defina um [**Usuário de serviços de diretório**](/advanced-threat-analytics/deploy-use/install-ata-step2) e escolha um [**Sincronizador de controlador de domínio**](/advanced-threat-analytics/deploy-use/install-ata-step5). 






## <a name="see-also"></a>Consulte também
- [Pré-requisitos do ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planejamento da capacidade do ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurar coleta de eventos](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configuração do encaminhamento de eventos do Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
