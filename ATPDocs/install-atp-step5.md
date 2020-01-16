---
title: Descrição conceitual das configurações do sensor do ATP do Azure | Microsoft Docs
description: A etapa cinco da instalação do Azure ATP ajuda a definir as configurações do sensor autônomo do Azure ATP.
author: shsagir
ms.author: shsagir
ms.date: 09/15/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b50dc7247e17831c3b083090787b85c228c13a77
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2020
ms.locfileid: "75907762"
---
# <a name="configure-azure-atp-sensor-settings"></a>Definir as configurações do sensor do ATP do Azure

Neste artigo, você aprenderá a definir corretamente as configurações do sensor do ATP do Azure para começar a ver os dados. Você precisará fazer configurações e integrações adicionais para aproveitar as funcionalidades completas do ATP do Azure.  

## <a name="prerequisites"></a>Pré-requisitos

- Uma [instância do ATP do Azure](install-atp-step1.md)[conectada ao Active Directory](install-atp-step2.md).
- Uma cópia baixada de seu [pacote de instalação do sensor do ATP](install-atp-step3.md) e a chave de acesso.

## <a name="configure-sensor-settings"></a>Definir as configurações do sensor

Após a instalação do sensor do ATP do Azure, faça o seguinte para definir as configurações do sensor do ATP do Azure.

1. Clique em **Iniciar** para abrir o navegador e entrar no portal do ATP do Azure.

1.  No portal do ATP do Azure, acesse **Configuração** e, na seção **Sistema**, selecione **Sensores**.
   
    ![Imagem de definição das configurações do sensor](media/atp-sensor-config.png)


1. Clique no sensor que deseja configurar e insira as seguintes informações:

   ![Imagem de definição das configurações do sensor](media/atp-sensor-config-2.png)

   - **Descrição**: Insira uma descrição para o sensor do ATP do Azure (opcional).
   - **Controladores de domínio (FQDN)** (necessário para o sensor autônomo do ATP do Azure, não pode ser alterado para o sensor do ATP do Azure): Digite o FQDN completo de seu controlador de domínio e clique no sinal de adição para acrescentá-lo à lista. Por exemplo, **dc01.contoso.com**

     As informações a seguir se aplicam aos servidores digitados na lista **Controladores de Domínio**:
     - Todos os controladores de domínio cujo tráfego está sendo monitorado por meio do espelhamento de porta pelo sensor autônomo do Azure ATP devem estar na lista **Controladores de Domínio**. Se um controlador de domínio não estiver listado em **Controladores de Domínio**, a detecção de atividades suspeitas pode não funcionar conforme o esperado.
     - Pelo menos um controlador de domínio na lista deve ser um catálogo global. Isso permite que o Azure ATP resolva os objetos de usuário e computador em outros domínios na floresta.

   - **Capturar adaptadores de rede** (obrigatório):
   
    - Para os sensores do ATP do Azure, todos os adaptadores de rede usados para comunicação com outros computadores da organização.
    - Para um sensor autônomo do ATP do Azure em um servidor dedicado, selecione os adaptadores de rede configurados como a porta de espelho de destino. Esses adaptadores de rede recebem o tráfego do controlador de domínio espelhado.

 
1. Clique em **Salvar**.


## <a name="validate-installations"></a>Validar instalações
Para validar a implantação bem-sucedida do sensor do Azure ATP, verifique o seguinte:

1. Verifique se o serviço chamado **Sensor de Proteção Avançada contra Ameaças do Azure** está em execução. Após você salvar as configurações do sensor do Azure ATP, talvez demore alguns minutos até que o serviço seja iniciado.

1. Se o serviço não iniciar, examine o arquivo “Microsoft.Tri.sensor-Errors.log” localizado na pasta padrão a seguir “%programfiles%\Azure Advanced Threat Protection sensor\Version X\Logs”.
 
   >[!NOTE]
   > A versão do ATP do Azure é atualizada com frequência. Para verificar a versão mais recente, no portal do ATP do Azure, vá em **Configuração** e, em seguida, **Sobre**. 

1. Acesse a URL da instância do ATP do Azure. No portal do ATP do Azure, pesquise algo na barra de pesquisa, como um usuário ou um grupo em seu domínio.

1. Verifique a conectividade do ATP em qualquer dispositivo de domínio usando as seguintes etapas:
    1. Abra um prompt de comando
    1. Digite ```nslookup```
    1. Digite **server**, depois o endereço IP ou FQDN do controlador de domínio no qual o sensor do ATP está instalado. Por exemplo, ```server contosodc.contoso.azure```
        - Substitua contosodc.contoso.azure e contoso.azure pelo FQDN do sensor e do nome domínio do ATP do Azure, respectivamente.
    1. Digite ```ls -d contoso.azure```
    1. Repita as etapas 3 e 4 para cada sensor que você quer testar.  
    1. No console do ATP do Azure, abra o perfil de entidade do computador a partir do qual você executou o teste de conectividade. 
    1. Verifique a atividade lógica relacionada e confirme a conectividade. 

    > [!NOTE] 
    >Se o controlador de domínio que você quer testar for o primeiro sensor implantado, aguarde pelo menos 15 minutos para permitir que o back-end do banco de dados conclua a implantação inicial dos microsserviços necessários antes de tentar verificar a atividade lógica relacionada desse controlador de domínio.

## <a name="next-steps"></a>Próximas etapas

- [Configuração de proxy](configure-proxy.md)
- [Política de auditoria avançada](atp-advanced-audit-policy.md)
- [Configurar o Azure ATP para realizar chamadas remotas para SAM](install-atp-step8-samr.md)


## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o ATP do Azure e a segurança relacionada com outras pessoas? Participe da [Comunidade do ATP do Azure](https://aka.ms/azureatpcommunity) hoje mesmo!
