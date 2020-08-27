---
title: O que há de novo na versão 1,4 do Advanced Threat Analytics
description: Lista as novidades na versão 1.4 do ATA e seus problemas conhecidos
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 01/23/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: cbea47f9-34c1-42b6-ae9e-6a472b49e1a5
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: cbe31a255a5b437852b6084fcea92556a04a6bd5
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88956679"
---
# <a name="what39s-new-in-ata-version-14"></a>Novidades na versão 1.4 do ATA
Essas notas de versão fornecem informações sobre problemas conhecidos na versão 1.4 da Advanced Threat Analytics.

## <a name="whats-new-in-this-version"></a>O que há de novo nesta versão?

- Suporte do Windows Event Forwarding (WEF) para enviar eventos diretamente dos controladores de domínio para o Gateway de ATA.

- Aprimoramentos na detecção de “Pass-The-Hash” em recursos corporativos, combinando DPI (inspeção profunda de pacote) e logs de eventos do Windows.

- Aprimoramentos para o suporte de dispositivos de domínio não unidos e dispositivos não Windows para detecção e visibilidade.

- Aprimoramentos de desempenho para oferecer suporte a mais tráfego por Gateway de ATA.

- Aprimoramentos de desempenho para oferecer suporte a mais Gateways de ATA por Centro de ATA.

- Um novo processo de resolução de nome automático foi adicionado, o que corresponde a nomes de computador e de endereços IP – este recurso exclusivo economiza um tempo precioso no processo de investigação e fornece provas sólidas para analistas de segurança

- Maior capacidade de coletar informações de usuários para ajustar automaticamente o processo de detecção.

- Detecção automática de dispositivos NAT.

- Failover automático quando os controladores de domínio não estão acessíveis.

- O monitoramento de integridade do sistema e as notificações agora fornecem o estado de integridade geral da implantação, assim como os problemas específicos relacionados à configuração e conectividade.

- Visibilidade de sites e os locais onde as entidades operam.

- Vários domínios.

- Suporte a domínios de rótulo único (SLD).

- Suporte para modificar o endereço IP e o certificado dos Gateways de ATA e o Centro de ATA.

- Telemetria para ajudar a melhorar a experiência do cliente.

## <a name="known-issues"></a>Problemas conhecidos
A seguir estão os problemas conhecidos existentes nesta versão.

### <a name="network-capture-software"></a>Software de captura de rede
No Gateway do ATA, o único software de captura de rede com suporte que pode ser instalado é o [Microsoft Network Monitor 3.4](https://www.microsoft.com/download/details.aspx?id=4865). Não instale o Microsoft Message Analyzer ou qualquer outro software de captura de rede. A instalação de outro software faz com que o Gateway de ATA pare de funcionar corretamente.

### <a name="installation-from-zip-file"></a>Instalação do arquivo Zip
Ao instalar o Gateway de ATA, certifique-se de extrair os arquivos do arquivo zip para um diretório local e instalá-lo de lá. Não instale o Gateway de ATA diretamente de dentro do arquivo zip ou a instalação falhará.

### <a name="uninstalling-previous-versions-of-ata"></a>Desinstalando versões anteriores de ATA
Se você instalou uma versão anterior do ATA, da Visualização Pública ou da Visualização Privada, você deve desinstalar o Centro de ATA e os Gateways de ATA antes de instalar esta versão do ATA.

Você também deve excluir os arquivos de banco de dados e arquivos de log. Os bancos de dados de versões anteriores do ATA não são compatíveis com a versão GA do ATA.

Se a instalação do ATA abrir em vez da desinstalação quando você tentar desinstalar o Centro de ATA ou o Gateway do ATA, será necessário adicionar a seguinte chave do Registro e, depois, desinstalar o ATA novamente.

**Centro do ATA**

- HKLM\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center

- Adicione um novo valor de cadeia de caracteres chamado `InstallationPath` com um valor de `C:\Program Files\Microsoft Advanced Threat Analytics\Center`. Esta é a pasta de instalação padrão. Se você tiver alterado a pasta de instalação, insira o caminho onde o ATA está instalado.

    ![Editor do registro para o caminho de instalação do Centro de ATA](media/ATA-uninstall-center-bug.jpg)

**Gateway do ATA**

- HKLM\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Gateway

- Adicione um novo valor de cadeia de caracteres chamado `InstallationPath` com um valor de `C:\Program Files\Microsoft Advanced Threat Analytics\Gateway`. Esta é a pasta de instalação padrão.  Se você tiver alterado a pasta de instalação, insira o caminho onde o ATA está instalado.

    ![Editor do registro para o caminho de instalação do Gateway de ATA](media/ATA-GW-uninstall-bug.jpg)

Após a desinstalação, exclua a pasta de instalação no Centro de ATA e no Gateway de ATA.  Se você instalou o banco de dados em uma pasta separada, exclua a pasta do banco de dados no Centro de ATA.

### <a name="health-alert---disconnected-ata-gateway"></a>Alerta de integridade – Gateway de ATA desconectado
Se você tiver mais de um Gateway de ATA e tiver desconectado os alertas de Gateway de ATA, a resolução automática funcionará em apenas um deles, deixando os restantes com status em aberto. Confirme manualmente que o Gateway de ATA está ativo e que o serviço está em execução, e resolva manualmente o alerta.

### <a name="kb-on-virtualization-host"></a>Base de dados de conhecimento sobre host de virtualização
Não instale a Base de dados de conhecimento 3047154 em um host de virtualização. Isso pode fazer com que o espelhamento de porta pare de funcionar corretamente.

## <a name="see-also"></a>Consulte Também

[Atualizar o ATA para a versão 1.6 — guia de migração](ata-update-1.6-migration-guide.md)

[Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)