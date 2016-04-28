---
# required metadata

title: Alteração da configuração do ATA - Certificado do Centro do ATA | Microsoft Advanced Threat Analytics
description: Descreve o processo de dois estágios para renovar ou substituir o certificado no repositório de computador local no servidor do Centro do ATA. 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: c8855287-de3b-4cdd-be8f-2128f48a6f27

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Alteração da configuração do ATA - Certificado do Centro do ATA

>[!div class="step-by-step"]
[« Endereço IP de servidor do Centro do ATA](modifying-ata-config-centerip.md)
[Endereço IP do Console do ATA »](modifying-ata-config-consoleip.md)

## Alteração do certificado do Centro do ATA
Se os seus certificados expiram e precisam ser renovados ou substituídos após a instalação do novo certificado no repositório de computador local no servidor do Centro do ATA, substitua o certificado com este processo em dois estágios:

-   Primeiro estágio – Atualizar o certificado que você deseja que o serviço do Centro do ATA use. Neste ponto, o serviço do Centro do ATA ainda está associado ao certificado original. Quando os Gateways do ATA sincronizarem suas configurações, terão dois possíveis certificados que serão válidos para autenticação mútua. Contanto que o Gateway do ATA possa se conectar usando o certificado original, ele não tentará o novo.

-   Segundo estágio – Após a sincronização de todos os Gateways do ATA com a configuração atualizada, você poderá ativar o novo certificado ao qual o serviço do Centro do ATA está associado. Quando você ativar o novo certificado, o serviço do Centro do ATA fará uma associação com o novo certificado. Os Gateways do ATA não serão capazes de autenticar mutuamente de forma correta o serviço do Centro do ATA, e tentarão autenticar o segundo certificado. Após a conexão com o serviço do Centro do ATA, o Gateway do ATA obterá a configuração mais recente e terá um único certificado para o Centro do ATA. (A menos que você tenha iniciado o processo novamente.)

> [!NOTE]
> -   Se um Gateway do ATA estava offline durante o primeira estágio e nunca recebeu a configuração atualizada, será necessário atualizar manualmente o arquivo de configuração JSON no Gateway do ATA.
> -   O certificado que você está usando deve ser de confiança dos Gateways do ATA.
> -   Se você precisar implantar um novo Gateway do ATA depois de ativar o novo certificado, será necessário baixar o pacote de Instalação do Gateway do ATA novamente.

1.  Abra o Console do ATA.

2.  Selecione a opção de configurações na barra de ferramentas e escolha **Configuração**.

    ![Ícone Definições de configuração do ATA](media/ATA-config-icon.JPG)

3.  Selecione **Centro do ATA**.

4.  Em **Certificado**, escolha um dos certificados na lista.

5.  Clique em **Salvar**.

6.  Você verá uma notificação indicando quantos Gateways do ATA foram sincronizados com a configuração mais recente.

7.  Após a sincronização de todos os Gateways do ATA, clique em **Ativar** para ativar o novo certificado.

8.  Verifique se todos os Gateways do ATA são capazes de sincronizar suas configurações após a ativação da alteração.

>[!div class="step-by-step"]
[« Endereço IP de servidor do Centro do ATA](modifying-ata-config-centerip.md)
[Endereço IP do Console do ATA »](modifying-ata-config-consoleip.md)

## Consulte também
- [Trabalhando com o Console do ATA](/advanced-threat-analytics/understand/working-with-ata-console)
- [Instalar o ATA](install-ata.md)
- [Para obter suporte, confira nosso fórum!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


