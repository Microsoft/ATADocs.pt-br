---
# required metadata

title: Instalação do ATA - Etapa 4 | Microsoft Advanced Threat Analytics
description: A Etapa quatro da instalação do ATA ajuda você a instalar o Gateway do ATA.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalação do ATA - Etapa 4

>[!div class="step-by-step"]
[« Etapa 3](install-ata-step3.md)
[Etapa 5 »](install-ata-step5.md)

## Etapa 4. Instalar o Gateway do ATA
Antes de instalar o Gateway do ATA, verifique se o espelhamento de porta está configurado corretamente, e se o Gateway do ATA pode ver o tráfego chegando e saindo dos controladores de domínio. Confira [Validar o espelhamento de porta](/advanced-threat-analytics/plandesign/validate-port-mirroring) para saber mais.

> [!IMPORTANT]
> Verifique se o [KB2919355](http://support.microsoft.com/kb/2919355/) foi instalado.  Execute o seguinte cmdlet do PowerShell para verificar se o hotfix foi instalado:
>
> `Get-HotFix -Id kb2919355`

Execute as seguintes etapas no servidor do Gateway do ATA.

1.  Extraia os arquivos do arquivo zip.

2.  Em um prompt de comando elevado, execute o arquivo Microsoft ATA Gateway Setup.exe e siga o assistente de instalação.

3.  Na página **Boas-vindas**, selecione seu idioma e clique em **Avançar**.

4.  Na página **Configuração do Gateway do ATA** insira as informações a seguir com base em seu ambiente:

    ![Imagem da configuração do gateway de ATA](media/ATA-Gateway-Configuration.JPG)

    |Campo|Descrição|Comentários|
    |---------|---------------|------------|
    |Caminho da Instalação|Esse é o local onde o Gateway do ATA será instalado. Por padrão, é %programfiles%\Microsoft Advanced Threat Analytics\Gateway|Mantenha o valor padrão|
    |Certificado SSL do Serviço do Gateway do ATA|Esse é o certificado que será usado pelo Gateway do ATA.|Use um certificado autoassinado apenas para ambientes de laboratório.|
    |Registro de Gateway do ATA|Digite o Nome de Usuário e a Senha do administrador do ATA.|Para o Gateway do ATA registrar-se no Centro do ATA, digite o nome de usuário e a senha do usuário que instalou o Centro do ATA. Esse usuário deve ser membro de um dos seguintes grupos locais no Centro do ATA.<br /><br />-   Administradores<br />-   Administradores do Microsoft Advanced Threat Analytics **Observação:** essas credenciais são usadas apenas para registro e não são armazenadas no ATA.|
    Os componentes a seguir serão instalados e configurados durante a instalação do Gateway do ATA:

    -   KB 3047154

        > [!IMPORTANT]
        > -   Não instale a Base de dados de conhecimento 3047154 em um host de virtualização. Isso pode fazer com que o espelhamento de porta pare de funcionar corretamente.
        > -   Não instale o Message Analyzer, o Wireshark ou qualquer outro software de captura de rede no Gateway do ATA. Se você precisa capturar o tráfego de rede, instale e use o Microsoft Network Monitor 3.4.

    -   Serviço do Gateway do ATA

    -   Microsoft Visual C++ 2013 Redistributable

    -   Conjunto de coleta de dados do Monitor de Desempenho Personalizado

5.  Após a conclusão da instalação, clique em **Iniciar** para abrir o navegador e faça logon Console do ATA.


>[!div class="step-by-step"]
[« Etapa 3](install-ata-step3.md)
[Etapa 5 »](install-ata-step5.md)

## Consulte também

- [Para obter suporte, confira nosso fórum!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Configurar coleta de eventos](/advanced-threat-analytics/plandesign/configure-event-collection)
- [Pré-requisitos do ATA](/advanced-threat-analytics/plandesign/ata-prerequisites)


<!--HONumber=Apr16_HO2-->


