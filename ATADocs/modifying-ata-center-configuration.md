---
title: Alterar a configuração do Centro do ATA do Advanced Threat Analytics | Microsoft Docs
description: Descreve como alterar o endereço IP, a porta, a URL do console ou o certificado de seu Centro do ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 80f96966a1ba9e62b23311cc19ed8fc5a8210bba
ms.sourcegitcommit: 56065ee43dac299203871cd6f025315520750b3b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47233857"
---
*Aplica-se a: Advanced Threat Analytics versão 1.9*



# <a name="modifying-the-ata-center-configuration"></a>Modificar a configuração do Centro do ATA


Após a implantação inicial, as modificações no Centro do ATA deverão ser feitas com cuidado. Use os procedimentos a seguir ao atualizar a URL do console e o certificado.

## <a name="the-ata-console-url"></a>A URL do Console do ATA

A URL é usada nos seguintes cenários:

-   Essa é a URL usada pelos Gateways do ATA para a comunicação com o Centro do ATA.

- Instalação de Gateways do ATA – Quando um Gateway do ATA é instalado, ele registra ai próprio no Centro do ATA. Esse processo de registro é realizado pela conexão com o Console do ATA. Se você digitar um FQDN para a URL do Console do ATA, garanta que o Gateway do ATA possa resolver o FQDN para o endereço IP associado ao Console do ATA.

-   Alertas – Quando o ATA envia um SIEM ou alerta de email, ele inclui um link para a atividade suspeita. A parte de host do link é a configuração de URL do Console do ATA.

-   Se você tiver instalado um certificado de sua Autoridade de Certificação (CA) interna, corresponda à URL para o nome da entidade no certificado. Isso impede que os usuários obtenham uma mensagem de aviso ao se conectarem ao Console do ATA.

-   O uso de um FQDN para a URL do Console do ATA permite que você modifique o endereço IP usado pelo Console do ATA sem dividir os alertas anteriores ou baixar o pacote de Gateway do ATA novamente. Você precisa apenas atualizar o DNS com o novo endereço IP.

1. Verifique se a nova URL que você deseja usar é resolvida para o endereço IP do Console do ATA.

2. Nas configurações do ATA, em **Centro**, digite a nova URL. Neste ponto, o serviço do Centro do ATA ainda usa a URL original. 

 ![Alteração da configuração do ATA](media/change-center-config.png)

  > [!NOTE]
  > Se você tiver inserido um endereço IP personalizado, não poderá clicar em **Ativar** até que tenha instalado o endereço IP no Centro do ATA.
    
3. Aguarde a sincronização dos Gateways do ATA. Agora eles têm duas URLs potenciais por meio das quais acessam o Console do ATA. Contanto que o Gateway do ATA possa se conectar usando a URL original, ele não tentará a nova.

4. Depois que todos os Gateways do ATA forem sincronizados com a configuração atualizada, na página de configuração central, clique no botão **Ativar** para ativar a nova URL. Quando você ativar a nova URL, os Gateways do ATA usarão a nova URL para acessar o centro do ATA. Após a conexão com o serviço do Centro do ATA, o Gateway do ATA obterá a configuração mais recente e terá somente a nova URL do Console do ATA. 
5. 
 ![Ativar o certificado](media/center-activation.png)

> [!NOTE]
> -   Se um Gateway do ATA estava offline durante a ativação da nova URL, e portanto nunca recebeu a configuração atualizada, atualize manualmente o arquivo JSON de configuração no Gateway do ATA.
> -   Se você precisar implantar um novo Gateway do ATA depois de ativar a nova URL, será necessário baixar o pacote de Instalação do Gateway do ATA novamente.


## <a name="the-ata-center-certificate"></a>O certificado do Centro do ATA

> [!WARNING]
> - Não há suporte para o processo de renovação de um certificado existente. A única maneira de renovar um certificado é criando um novo certificado e configurando o ATA para usar o novo certificado.


Substitua o certificado seguindo este processo:

1. Antes da expiração do certificado atual, crie um novo certificado e verifique se ele está instalado no servidor do Centro do ATA. <br></br>É recomendável escolher um certificado de uma autoridade de certificação interna, mas também é possível criar um novo certificado autoassinado. Para saber mais, confira [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).

2. Nas configurações do ATA, em **Centro**, selecione este certificado recém-criado. Neste ponto, o serviço do Centro do ATA ainda está associado ao certificado original. 

 ![Alteração da configuração do ATA](media/change-center-config.png)

3. Aguarde a sincronização dos Gateways do ATA. Agora eles têm dois possíveis certificados que são válidos para autenticação mútua. Contanto que o Gateway do ATA possa se conectar usando o certificado original, ele não tentará o novo.

4. Após a sincronização de todos os Gateways do ATA com a configuração atualizada, ative o novo certificado ao qual o serviço do Centro do ATA está associado. Quando você ativar o novo certificado, o serviço do Centro do ATA se associará ao novo certificado. Agora, os Gateways do ATA usam o novo certificado para autenticar no Centro do ATA. Após a conexão com o serviço do Centro do ATA, o Gateway do ATA obterá a configuração mais recente e terá somente o novo certificado para o Centro do ATA. 

> [!NOTE]
> -   Se um Gateway do ATA estava offline durante a ativação do novo certificado, e portanto nunca recebeu a configuração atualizada, será necessário atualize manualmente o arquivo de configuração JSON no Gateway do ATA.
> -   O certificado que você está usando deve ser de confiança dos Gateways do ATA.
> -   O certificado também é usado para o Console do ATA, portanto, ele deve corresponder ao endereço do Console do ATA a fim de evitar avisos do navegador.
> -   Se você precisar implantar um novo Gateway do ATA depois de ativar o novo certificado, será necessário baixar o pacote de Instalação do Gateway do ATA novamente.



 
## <a name="see-also"></a>Consulte Também
- [Trabalhando com o Console do ATA](working-with-ata-console.md)
- [Confira o fórum do ATA!](https://aka.ms/ata-forum)
