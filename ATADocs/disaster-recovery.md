---
title: Recuperação de desastre para o Advanced Threat Analytics | Microsoft Docs
description: Descreve como você pode recuperar rapidamente a funcionalidade do ATA após desastres
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/05/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 7620e171-76d5-4e3f-8b03-871678217a3a
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 10c87243e14ed9b2d4331abdbffcfa26f99b2ce2
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166537"
---
*Aplica-se a: Advanced Threat Analytics versão 1.9*



# <a name="ata-disaster-recovery"></a>Recuperação de desastre de ATA
Este artigo descreve como recuperar rapidamente seu Centro de ATA e restaurar a funcionalidade do ATA quando a funcionalidade do Centro de ATA for perdida, mas os Gateways de ATA ainda estiverem funcionando. 

>[!NOTE]
> O processo descrito não recupera atividades suspeitas detectadas anteriormente, mas retorna o Centro de ATA à funcionalidade completa. Além disso, o período de aprendizado necessário para algumas detecções comportamentais reiniciará, mas a maior parte da detecção que o ATA oferece estará funcionando depois que o Centro de ATA estiver restaurado. 

## <a name="back-up-your-ata-center-configuration"></a>Fazer backup da sua configuração do Centro de ATA

1. A configuração do Centro de ATA é armazenada em backup em um arquivo a cada quatro horas. Localize a última cópia de backup da configuração do Centro de ATA e salve-a em um computador à parte. Para obter uma explicação completa de como localizar esses arquivos, confira [Exportar e importar a configuração de ATA](ata-configuration-file.md). 
2. Exportação do certificado do Centro de ATA.
    1. No gerenciador de certificados, navegue até **Certificados (Computador Local)** -> **Pessoal** ->**Certificados** e selecione **Centro de ATA**.
    2. Clique com o botão direito do mouse em **Centro de ATA** e selecione **Todas as Tarefas** e, em seguida, **Exportar**. 
     ![Certificado do Centro de ATA](media/ata-center-cert.png)
    3. Siga as instruções para exportar o certificado, certificando-se de exportar também a chave privada.
    4. Faça o backup do arquivo de certificado exportado em um computador separado.

  > [!NOTE] 
  > Se você não puder exportar a chave privada, você deve criar um novo certificado e implantá-lo no ATA, conforme descrito em [Alteração do certificado do Centro de ATA](modifying-ata-center-configuration.md) e, em seguida, exportá-la. 

## <a name="recover-your-ata-center"></a>Recuperar seu Centro de ATA

1. Crie uma nova máquina do Windows Server usando o mesmo nome de computador e o endereço IP da máquina anterior do Centro de ATA.
2. Importe o certificado que você armazenou em backup anteriormente no novo servidor.
3. Siga as instruções para [Implantar o Centro de ATA](install-ata-step1.md) no Windows Server recém-criado. Não é necessário implantar os Gateways do ATA novamente. Quando for solicitado um certificado, forneça o certificado exportado durante o backup da configuração do Centro de ATA. 
![Restauração do Centro de ATA](media/disaster-recovery-deploymentss.png)
4. Interrompa o serviço do Centro ATA.
5. Importe a configuração do Centro de ATA armazenada em backup:
    1. Remova o documento padrão do Perfil do Sistema do Centro de ATA do MongoDB: 
        1. Acesse **C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**. 
        2. Execute `mongo.exe ATA` 
        3. Execute este comando para remover o perfil do sistema padrão: `db.SystemProfile.remove({})`
    2. Execute o comando: `mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert` usando o arquivo de backup da etapa 1.</br>
    Para obter uma explicação completa de como localizar e importar arquivos de backup, confira [Exportar e importar a configuração de ATA](ata-configuration-file.md). 
    3. Inicie o serviço do Centro ATA.
    4. Abra o Console do ATA. Você deverá ver todos os Gateways do ATA vinculados na guia Configuração/Gateways.
    5. Defina um [**Usuário de serviços de diretório**](install-ata-step2.md) e escolha um [**Sincronizador de controlador de domínio**](install-ata-step5.md). 






## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Planejamento da capacidade do ATA](ata-capacity-planning.md)
- [Configurar coleta de eventos](install-ata-step6.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-collection.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
