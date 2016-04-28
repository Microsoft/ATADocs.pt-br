---
# required metadata

title: Alteração da configuração do ATA - nome do adaptador de captura de rede | Microsoft Advanced Threat Analytics
description: Descreve como alterar o nome do adaptador de rede configurado como um Adaptador de captura de rede sem encerrar a conectividade de Gateway do ATA
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 3225a81e-0395-43ca-9a48-0cbe7171e5de

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Alteração da configuração do ATA - nome do adaptador de captura de rede

>[!div class="step-by-step"]
[« Senha de conectividade do domínio](modifying-ata-config-dcpassword.md)

## Alteração do nome do adaptador de captura de rede do Gateway do ATA
Se você alterar o nome do adaptador de rede configurado como adaptador de captura de rede, o servidor de Gateway do ATA não será iniciado. Para alterar o nome sem encerrar a conectividade do Gateway do ATA, siga este processo:

1.  Na página de configuração do Gateway do ATA, desmarque o adaptador de rede que você deseja renomear e selecione outro adaptador de rede como o adaptador de captura de rede. Pode ser um adaptador de rede temporário ou até mesmo o adaptador de rede de gerenciamento. Durante esse tempo, o ATA não capturará o tráfego espelhado pela porta do controlador de domínio. Salve a nova configuração.

2.  No Gateway do ATA, renomeie o adaptador de rede abrindo o Painel de Controle e selecionando Conexões de Rede.

3.  Depois, volte à página de configuração do Gateway do ATA do Console do ATA . Talvez seja necessário atualizar a página para poder ver o adaptador de rede com o novo nome na lista. Desmarque o adaptador selecionado na etapa 1 e selecione o adaptador recém-renomeado. Por fim, salve a nova configuração.

Se você renomeou o adaptador de rede sem seguir esse processo, seu Gateway do ATA não será iniciado e você receberá esse erro no Gateway do ATA, no arquivo de log Microsoft.Tri.Gateway-Errors.log. No exemplo a seguir, **Capture** seria o nome original do adaptador de rede definido por você:

`Error [NetworkListener] Microsoft.Tri.Infrastructure.ExtendedException: Unavailable network adapters [UnavailableCaptureNetworkAdapterNames=Capture]`

Para corrigir esse problema, renomeie o adaptador de rede usando o nome original durante a configuração do ATA e, depois, percorra o processo descrito acima para alterar o nome.

>[!div class="step-by-step"]
[« Senha de conectividade do domínio](modifying-ata-config-dcpassword.md)


## Consulte também
- [Trabalhando com o Console do ATA](/advanced-threat-analytics/understand/working-with-ata-console)
- [Instalar o ATA](install-ata.md)
- [Para obter suporte, confira nosso fórum!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


