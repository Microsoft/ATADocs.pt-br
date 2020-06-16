---
title: Configurar SAM-R para habilitar a detecção de caminho de movimento lateral na análise avançada de ameaças
description: Descreve como configurar o SAM-R para habilitar a detecção de caminho de movimento lateral no ATA (Advanced Threat Analytics)
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/08/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 7597ed25-87f5-472c-a496-d5f205c9c391
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4804717d489a68380f78292d8ee8e89910bf7435
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2020
ms.locfileid: "84775056"
---
# <a name="install-ata---step-9"></a>Instalar o ATA – Etapa 9

*Aplica-se a: Advanced Threat Analytics versão 1.9*

> [!div class="step-by-step"]
> [« Etapa 8](install-ata-step7.md)

> [!NOTE]
> Antes de impor qualquer nova política, sempre certifique-se de que seu ambiente permaneça seguro, sem afetar a compatibilidade do aplicativo, primeiro Habilitando e verificando as alterações propostas no modo de auditoria. 

## <a name="step-9-configure-sam-r-required-permissions"></a>Etapa 9. Configurar permissões necessárias do SAM-R

A detecção de [caminho de movimento lateral](use-case-lateral-movement-path.md) se baseia em consultas que identificam os administradores locais em computadores específicos. Essas consultas são executadas usando o protocolo SAM-R, por meio da conta de serviço do ATA criada na [etapa 2. Conecte-se ao AD](install-ata-step2.md).
 
Para garantir que clientes e servidores Windows permitam que a conta de serviço do ATA execute essa operação SAM-R, é necessário fazer uma modificação na **política de grupo** que adicione a conta de serviço do ATA, além das contas configuradas listadas na política de **Acesso de rede**. Essa política de grupo deve ser aplicada para cada dispositivo em sua organização. 

1. Localize a política:

   - Nome da política: Acesso à rede – restringir clientes com permissão para efetuar chamadas remotas para SAM
   - Local: Configuração do computador, Configurações do Windows, Configurações de segurança, Políticas locais, Opções de segurança
  
   ![Localize a política](./media/samr-policy-location.png)

2. Adicione o serviço do ATA à lista de contas aprovadas que podem executar essa ação em seus sistemas modernos do Windows.
 
   ![Adicione o serviço](./media/samr-add-service.png)

3. Agora, o **Serviço do ATA** (o serviço do ATA criado durante a instalação) tem os privilégios apropriados para executar o SAM-R no ambiente.

 Saiba mais sobre SAM-R e Política de Grupo em [Acesso à rede: restringir clientes com permissão para efetuar chamadas remotas para SAM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls).


> [!div class="step-by-step"]
> [« Etapa 8](install-ata-step7.md)

## <a name="see-also"></a>Consulte Também
- [Guia de implantação da POC (prova de conceito) do ATA](https://aka.ms/atapoc)
- [Ferramenta de dimensionamento do ATA](https://aka.ms/atasizingtool)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)
