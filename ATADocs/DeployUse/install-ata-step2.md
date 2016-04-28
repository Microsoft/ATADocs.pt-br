---
# required metadata

title: Instalação do ATA - Etapa 2 | Microsoft Advanced Threat Analytics
description: A etapa dois da instalação do ATA ajuda você a definir as configurações de conectividade do domínio em seu servidor do Centro do ATA
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalação do ATA - Etapa 2

>[!div class="step-by-step"]
[« Etapa 1](install-ata-step1.md)
[Etapa 3 »](install-ata-step3.md)

## Etapa 2. Definição das configurações de conectividade de domínio do Gateway do ATA
As definições na seção de configurações de conectividade do domínio se aplicam a todos os Gateways do ATA gerenciados pelo Centro do ATA.

Para definir as configurações de conectividade do Domínio, faça o seguinte no servidor do Centro do ATA.

1.  Abra o Console do ATA e faça logon. Para obter instruções, confira [Como trabalhar com o Console do ATA](/advanced-threat-analytics/understand/working-with-ata-console).

2.  Na primeira vez que você faz logon no Console do ATA após a instalação do Centro do ATA, você será levado automaticamente à página de configuração de Gateways do ATA. Se você precisar modificar qualquer uma das configurações depois, clique no ícone Configurações e escolha **Configuração**.

    ![Definições de configuração do Gateway do ATA](media/ATA-config-icon.JPG)

3.  Na página **Gateways**, clique em **Configurações de conectividade do domínio**, insira as seguintes informações e clique em **Salvar**.

    |Campo|Comentários|
    |---------|------------|
    |**Nome de usuário** (obrigatório)|Insira o nome de usuário somente leitura, por exemplo: **usuário1**.|
    |**Senha** (obrigatório)|Digite a senha para o usuário somente leitura, por exemplo: **Lápis1**. **Observação:** certifique-se de que essa senha esteja correta. Se você salvar a senha incorreta, o Serviço do ATA interromperá a execução nos servidores de Gateway do ATA.|
    |**Domínio** (obrigatório)|Digite o domínio para o usuário somente leitura, por exemplo: **contoso.com**. **Observação:** é importante que você insira o FQDN completo do domínio onde o usuário está localizado. Por exemplo, se a conta do usuário estiver no domínio corp.contoso.com, você precisará inserir `corp.contoso.com` e não contoso.com|
    ![Imagem configurações de conectividade do Domínio do ATA](media/ATA-Domain-Connectivity-User.JPG)


>[!div class="step-by-step"]
[« Etapa 1](install-ata-step1.md)
[Etapa 3 »](install-ata-step3.md)


## Consulte também

- [Para obter suporte, confira nosso fórum!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurar coleta de eventos](/advanced-threat-analytics/plandesign/configure-event-collection)
- [Pré-requisitos do ATA](/advanced-threat-analytics/plandesign/ata-prerequisites)


<!--HONumber=Apr16_HO2-->


