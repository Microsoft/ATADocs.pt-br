---
title: Recuperação de desastre para a análise avançada de ameaças
description: Descreve como você pode recuperar rapidamente a funcionalidade do ATA após desastres
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 05/02/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 7620e171-76d5-4e3f-8b03-871678217a3a
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: eeb4a87ed3983af7e6452849ab35edc7ee15f369
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88954724"
---
# <a name="ata-disaster-recovery"></a>Recuperação de desastre de ATA

*Aplica-se a: Advanced Threat Analytics versão 1.9*

Este artigo descreve como recuperar rapidamente seu Centro de ATA e restaurar a funcionalidade do ATA quando a funcionalidade do Centro de ATA for perdida, mas os Gateways de ATA ainda estiverem funcionando. 

>[!NOTE]
> O processo descrito não recupera atividades suspeitas detectadas anteriormente, mas retorna o Centro de ATA à funcionalidade completa. Além disso, o período de aprendizado necessário para algumas detecções comportamentais reiniciará, mas a maior parte da detecção que o ATA oferece estará funcionando depois que o Centro de ATA estiver restaurado. 

## <a name="back-up-your-ata-center-configuration"></a>Fazer backup da sua configuração do Centro de ATA

1. A configuração do Centro de ATA é armazenada em backup em um arquivo a cada quatro horas. Localize a última cópia de backup da configuração do Centro de ATA e salve-a em um computador à parte. Para obter uma explicação completa de como localizar esses arquivos, confira [Exportar e importar a configuração de ATA](ata-configuration-file.md). 
1. Exportação do certificado do Centro de ATA.
    1. No Gerenciador de certificados, navegue até **certificados (computador local)**  ->  **Personal**  -> **certificados**pessoais e selecione **centro do ATA**.
    2. Clique com o botão direito do mouse em **Centro de ATA** e selecione **Todas as Tarefas** e, em seguida, **Exportar**. 
     ![Certificado do Centro de ATA](media/ata-center-cert.png)
    3. Siga as instruções para exportar o certificado, certificando-se de exportar também a chave privada.
    4. Faça o backup do arquivo de certificado exportado em um computador separado.

   > [!NOTE] 
   > Se você não puder exportar a chave privada, você deve criar um novo certificado e implantá-lo no ATA, conforme descrito em [Alteração do certificado do Centro do ATA](modifying-ata-center-configuration.md) e, em seguida, exportá-la. 

## <a name="recover-your-ata-center"></a>Recuperar seu Centro de ATA

1. Crie uma nova máquina do Windows Server usando o mesmo nome de computador e o endereço IP da máquina anterior do Centro do ATA.
1. Importe o certificado que você armazenou em backup anteriormente no novo servidor.
1. Siga as instruções para [Implantar o Centro do ATA](install-ata-step1.md) no Windows Server recém-criado. Não é necessário implantar os Gateways do ATA novamente. Quando for solicitado um certificado, forneça o certificado exportado durante o backup da configuração do Centro de ATA. 
![Restauração do Centro do ATA](media/disaster-recovery-deploymentss.png)
1. Interrompa o serviço do Centro ATA.
1. Importe a configuração do Centro de ATA armazenada em backup:
    1. Remova o documento padrão do Perfil do Sistema do Centro de ATA do MongoDB: 
        1. Acesse **C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**. 
        2. Execute `mongo.exe ATA` 
        3. Execute este comando para remover o perfil do sistema padrão: `db.SystemProfile.remove({})`
        4. Deixe o shell do Mongo e retorne ao prompt de comando, digitando: `exit`
    2. Execute o comando: `mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert` usando o arquivo de backup da etapa 1.</br>
    Para obter uma explicação completa de como localizar e importar arquivos de backup, confira [Exportar e importar a configuração de ATA](ata-configuration-file.md). 
    3. Inicie o serviço do Centro ATA.
    4. Abra o Console do ATA. Você deverá ver todos os Gateways do ATA vinculados na guia Configuração/Gateways.
    5. Certifique-se de definir um [**usuário de serviços de diretório**](install-ata-step2.md) e escolher um [**sincronizador de controlador de domínio**](install-ata-step5.md). 






## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Planejamento da capacidade do ATA](ata-capacity-planning.md)
- [Configurar coleta de eventos](install-ata-step6.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-collection.md)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
