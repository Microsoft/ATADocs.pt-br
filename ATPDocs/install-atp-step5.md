---
title: Instalar a Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: A etapa cinco da instalação do Azure ATP ajuda a definir as configurações do sensor autônomo do Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: d7c95f8c-04f8-4946-9bae-c27ed362fcb0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2bdfd0fe41ed6dc5f489784c2095cefd2032d135
ms.sourcegitcommit: f4f2a1b2c674c4dba7a46ece0624f5ea10c4865e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2018
ms.locfileid: "52744345"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*



# <a name="install-azure-atp---step-5"></a>Instalar o Azure ATP – etapa 5

> [!div class="step-by-step"]
> [« Etapa 4](install-atp-step4.md)
> [Etapa 6 »](install-atp-step6-vpn.md)



## <a name="step-5-configure-the-azure-atp-sensor-settings"></a>Etapa 5. Definir configurações do sensor do Azure ATP
Após a instalação do sensor do Azure ATP, execute as etapas a seguir para definir as configurações do sensor do Azure ATP.

1.  No portal do ATP do Azure, vá em **Configuração** e, em **Sistema**, selecione **sensor**.
   
     ![Imagem de definição das configurações do sensor](media/atp-sensor-config.png)


2.  Clique no sensor que deseja configurar e insira as seguintes informações:

    ![Imagem de definição das configurações do sensor](media/atp-sensor-config-2.png)

  - **Descrição**: insira uma descrição para o sensor do Azure ATP (opcional).
  - **Controladores de Domínio (FQDN)** (obrigatório para o sensor autônomo do Azure ATP, não pode ser alterado para o sensor do Azure ATP): insira o FQDN completo de seu controlador de domínio e clique no sinal de adição para adicioná-lo à lista. Por exemplo, **dc01.contoso.com**

      As informações a seguir se aplicam aos servidores digitados na lista **Controladores de Domínio**:
      - Todos os controladores de domínio cujo tráfego está sendo monitorado por meio do espelhamento de porta pelo sensor autônomo do Azure ATP devem estar na lista **Controladores de Domínio**. Se um controlador de domínio não estiver listado em **Controladores de Domínio**, a detecção de atividades suspeitas pode não funcionar conforme o esperado.
      - Pelo menos um controlador de domínio na lista deve ser um catálogo global. Isso permite que o Azure ATP resolva os objetos de usuário e computador em outros domínios na floresta.

  - **Capturar adaptadores de rede** (obrigatório):
   
     - Para um sensor do Azure ATP, trata-se de todos os adaptadores de rede usados para comunicação com outros computadores da organização.
    - Para um sensor autônomo do Azure ATP em um servidor dedicado, selecione os adaptadores de rede que estão configurados como a porta de espelho do destino. Eles recebem o tráfego do controlador de domínio espelhado.

    - **Candidato ao sincronizador de domínio**: por padrão, os sensores do Azure ATP não são candidatos ao sincronizador do domínio, embora os sensores autônomos do ATP do Azure sejam. Para selecionar manualmente um sensor do ATP do Azure como um candidato de sincronizador do domínio, alterne a opção **Candidato a sincronizador de domínio** para **LIGADO** na tela de configuração. 
    
        O sincronizador de domínio é responsável pela sincronização entre o Azure ATP e o domínio do Active Directory. Dependendo do tamanho do domínio, a sincronização inicial pode ser demorada e consumir muitos recursos. 
   É recomendável desabilitar que os sensores do Azure ATP do site remoto sejam candidatos a sincronizador de domínio.
   Se o controlador de domínio for somente leitura, não o defina como um candidato ao sincronizador do domínio. Para obter mais informações sobre a sincronização de domínio do Azure ATP, veja [arquitetura do Azure ATP](atp-architecture.md#azure-atp-sensor-features)
  
3. Clique em **Salvar**.


## <a name="validate-installations"></a>Validar instalações
Para validar a implantação bem-sucedida do sensor do Azure ATP, verifique as seguintes etapas:

1.  Verifique se o serviço chamado **Sensor de Proteção Avançada contra Ameaças do Azure** está em execução. Após você salvar as configurações do sensor do Azure ATP, talvez demore alguns minutos até que o serviço seja iniciado.

2.  Se o serviço não iniciar, examine o arquivo "Microsoft.Tri.sensor-Errors.log" localizado na pasta padrão a seguir "%programfiles%\Azure Advanced Threat Protection sensor\Version X\Logs".
 
 >[!NOTE]
 > A versão do ATP do Azure é atualizada com frequência. Para verificar a versão mais recente, no portal do ATP do Azure, vá em **Configuração** e, em seguida, **Sobre**. 

3.  Acesse a URL da instância do ATP do Azure. No portal do ATP do Azure, pesquise algo na barra de pesquisa, como um usuário ou um grupo em seu domínio.



> [!div class="step-by-step"]
> [« Etapa 4](install-atp-step4.md)
> [Etapa 6 »](install-atp-step6-vpn.md)



## <a name="see-also"></a>Consulte Também

- [Ferramenta de dimensionamento do Azure ATP](http://aka.ms/aatpsizingtool)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
