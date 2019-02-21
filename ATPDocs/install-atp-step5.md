---
title: Início rápido para definir as configurações do sensor do ATP do Azure | Microsoft Docs
description: A etapa cinco da instalação do Azure ATP ajuda a definir as configurações do sensor autônomo do Azure ATP.
author: mlottner
ms.author: mlottner
ms.date: 02/06/2018
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 381cf39f29edb36c704ce2de7f6c2aca31d4f19d
ms.sourcegitcommit: c48db18274edb2284e281960c6262d97f96e01d2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56263338"
---
# <a name="quickstart-configure-azure-atp-sensor-settings"></a>Início Rápido: Definir as configurações do sensor do ATP do Azure

Neste início rápido, você vai definir as configurações do sensor do ATP do Azure para começar a ver os dados. Você precisará fazer configurações e integrações adicionais para aproveitar os recursos do ATP do Azure.  

## <a name="prerequisites"></a>Pré-requisitos

- Uma [instância do ATP do Azure](install-atp-step1.md) [conectada ao Active Directory](install-atp-step2.md).
- Uma cópia baixada de seu [pacote de instalação do sensor do ATP](install-atp-step3.md) e a chave de acesso.

## <a name="configure-sensor-settings"></a>Definir as configurações do sensor

Após a instalação do sensor do ATP do Azure, execute as etapas a seguir para definir as configurações do sensor do ATP do Azure.

1.  No portal do ATP do Azure, acesse **Configuração** e, na seção **Sistema**, selecione **Sensores**.
   
    ![Imagem de definição das configurações do sensor](media/atp-sensor-config.png)


2. Clique no sensor que deseja configurar e insira as seguintes informações:

   ![Imagem de definição das configurações do sensor](media/atp-sensor-config-2.png)

   - **Descrição**: Insira uma descrição para o sensor do ATP do Azure (opcional).
   - **Controladores de domínio (FQDN)** (necessário para o sensor autônomo do ATP do Azure, não pode ser alterado para o sensor do ATP do Azure): Digite o FQDN completo de seu controlador de domínio e clique no sinal de adição para acrescentá-lo à lista. Por exemplo, **dc01.contoso.com**

     As informações a seguir se aplicam aos servidores digitados na lista **Controladores de Domínio**:
     - Todos os controladores de domínio cujo tráfego está sendo monitorado por meio do espelhamento de porta pelo sensor autônomo do Azure ATP devem estar na lista **Controladores de Domínio**. Se um controlador de domínio não estiver listado em **Controladores de Domínio**, a detecção de atividades suspeitas pode não funcionar conforme o esperado.
     - Pelo menos um controlador de domínio na lista deve ser um catálogo global. Isso permite que o Azure ATP resolva os objetos de usuário e computador em outros domínios na floresta.

   - **Capturar adaptadores de rede** (obrigatório):
   
    - Para os sensores do ATP do Azure, todos os adaptadores de rede usados para comunicação com outros computadores da organização.
    - Para um sensor autônomo do ATP do Azure em um servidor dedicado, selecione os adaptadores de rede configurados como a porta de espelho de destino. Esses adaptadores de rede recebem o tráfego do controlador de domínio espelhado.

  - **Candidato ao sincronizador de domínio**: 
    
    - O sincronizador de domínio é responsável pela sincronização entre o Azure ATP e o domínio do Active Directory. Dependendo do tamanho do domínio, a sincronização inicial pode ser demorada e consumir muitos recursos. O ATP do Azure recomenda a configuração de pelo menos um controlador de domínio como o candidato a sincronizador de domínio por domínio. Se pelo menos um controlador de domínio não for selecionado como o candidato a sincronizador de domínio, o ATP do Azure verificará a rede apenas passivamente e poderá não ser capaz de coletar todas as alterações e os detalhes de entidade do Active Directory. Pelo menos um **candidato a sincronizador de domínio** designado por domínio garante que o ATP do Azure sempre esteja verificando ativamente a rede e seja capaz de coletar todas as alterações e os valores de entidade do Active Directory.
  
    - Por padrão, os sensores do ATP do Azure não são candidatos ao sincronizador do domínio, embora os sensores autônomos do ATP do Azure sejam. Para definir manualmente um sensor do ATP do Azure como um candidato a sincronizador de domínio, mude a opção **Candidato a sincronizador de domínio** para **HABILITADO** na tela de configuração.
        
    - É recomendável desabilitar que os sensores do ATP do Azure do site remoto sejam candidatos a sincronizador de domínio.
   
    - Não defina os controladores de domínio somente leitura como candidatos a sincronizador de domínio. Para obter mais informações sobre a sincronização de domínio do ATP do Azure, confira [Arquitetura do ATP do Azure](atp-architecture.md#azure-atp-sensor-features).
  
3. Clique em **Salvar**.


## <a name="validate-installations"></a>Validar instalações
Para validar a implantação bem-sucedida do sensor do Azure ATP, verifique as seguintes etapas:

1. Verifique se o serviço chamado **Sensor de Proteção Avançada contra Ameaças do Azure** está em execução. Após você salvar as configurações do sensor do Azure ATP, talvez demore alguns minutos até que o serviço seja iniciado.

2. Se o serviço não iniciar, examine o arquivo “Microsoft.Tri.sensor-Errors.log” localizado na pasta padrão a seguir “%programfiles%\Azure Advanced Threat Protection sensor\Version X\Logs”.
 
   >[!NOTE]
   > A versão do ATP do Azure é atualizada com frequência. Para verificar a versão mais recente, no portal do ATP do Azure, vá em **Configuração** e, em seguida, **Sobre**. 

3. Acesse a URL da instância do ATP do Azure. No portal do ATP do Azure, pesquise algo na barra de pesquisa, como um usuário ou um grupo em seu domínio.

## <a name="next-steps"></a>Próximas etapas

- [Configuração de proxy](configure-proxy.md)
- [Política de auditoria avançada](atp-advanced-audit-policy.md)
- [Configurar o Azure ATP para realizar chamadas remotas para SAM](install-atp-step8-samr.md)


## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o ATP do Azure e a segurança relacionada com outras pessoas? Participe da [Comunidade do ATP do Azure](https://aka.ms/azureatpcommunity) hoje mesmo!
