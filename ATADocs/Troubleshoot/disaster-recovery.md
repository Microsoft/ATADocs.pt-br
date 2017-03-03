---
title: "Recuperação de desastre para o Advanced Threat Analytics | Microsoft Docs"
description: "Descreve como você pode recuperar rapidamente a funcionalidade do ATA após desastres"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 02/12/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 7620e171-76d5-4e3f-8b03-871678217a3a
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e3f763f7c1cce6c451a1cc969771b73543c76673
ms.openlocfilehash: 0669ccb78207dde1ede06a229af896bed0b19d28


---

*Aplica-se a: Advanced Threat Analytics versão 1.7*



# <a name="ata-disaster-recovery"></a>Recuperação de desastre de ATA
Este artigo descreve como recuperar rapidamente seu Centro de ATA e restaurar a funcionalidade do ATA quando a funcionalidade do Centro de ATA for perdida, mas os Gateways de ATA ainda estiverem funcionando. 

>[!NOTE]
> O processo descrito não recupera atividades suspeitas detectadas anteriormente, mas retorna o Centro de ATA à funcionalidade completa. Além disso, o período de aprendizado necessário para algumas detecções comportamentais reiniciará, mas a maior parte da detecção que o ATA oferece estará funcionando depois que o Centro de ATA estiver restaurado. 

## <a name="how-to-recover-your-ata-center-after-a-disaster"></a>Como recuperar o seu Centro de ATA após um desastre

1. A configuração do Centro de ATA é armazenada em backup em um arquivo a cada hora. Localize a última cópia de backup da configuração do Centro de ATA e salve-a em um computador à parte. Para obter uma explicação completa de como localizar esses arquivos, confira [Exportar e importar a configuração de ATA](/advanced-threat-analytics/deploy-use/ata-configuration-file). 
2. Exportação do certificado do Centro do ATA.
    1. No gerenciador de certificados, navegue até **Certificados (Computador Local)** -> **Pessoal** ->**Certificados** e selecione **Centro do ATA**.
    2. Clique com o botão direito em **Centro do ATA** e selecione **Todas as Tarefas** e, em seguida, **Exportar**. 
     ![Certificado do Centro do ATA](media/ata-center-cert.png)
    3. Siga as instruções para exportar o certificado, certificando-se de exportar também a chave privada.

    > [!NOTE] 
    > Se você não puder exportar a chave privada, você deve criar um novo certificado e implantá-lo no ATA, conforme descrito em [Alteração do certificado do Centro do ATA](/advanced-threat-analytics/deploy-use/modifying-ata-config-centercert) e, em seguida, exportá-la. 

    4. Faça o backup do arquivo de certificado exportado em um computador separado.
3. Crie uma nova máquina do Windows Server usando o mesmo nome de computador e o endereço IP da máquina anterior do Centro do ATA.
4. Importe o certificado que você armazenou em backup na etapa 2 ao novo servidor.
5. Siga as instruções para [Implantar o Centro do ATA](/advanced-threat-analytics/deploy-use/install-ata-step1) no Windows Server recém-criado. Não é necessário implantar os Gateways do ATA novamente. Quando um certificado for solicitado, forneça o certificado na etapa 2. 
![Restauração do Centro do ATA](media/ata-center-restore.png)
6. Importe a configuração do Centro do ATA armazenada em backup:
    1. Remova o documento padrão do Perfil do Sistema do Centro do ATA do MongoDB: 
        1. Acesse **C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**. 
        2. Execute `mongo.exe` 
        3. Execute o seguinte comando para remover o perfil do sistema padrão: `db.SystemProfile.remove({})`
    2. Execute o comando: `mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert` usando o arquivo de backup da etapa 1.</br>
    Para obter uma explicação completa de como localizar e importar arquivos de backup, confira [Exportar e importar a configuração de ATA](/advanced-threat-analytics/deploy-use/ata-configuration-file). 
    3. Após a importação, execute este comando para remover alguns dos perfis e detectores padrão (para redefini-los para o novo ambiente): `db.SystemProfile.remove({$or:[{"_t":"DetectorProfile"}, "_t":"DirectoryServicesSystemProfile"}]}) `
    4. Abra o Console do ATA. Você deverá ver todos os Gateways do ATA vinculados na guia Configuração/Gateways. 
    5. Defina um **Usuário de serviços de diretório** e escolha um **Sincronizador de controlador de domínio**. 






## <a name="see-also"></a>Consulte também
- [Pré-requisitos do ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planejamento da capacidade do ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurar coleta de eventos](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configuração do encaminhamento de eventos do Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Feb17_HO3-->


