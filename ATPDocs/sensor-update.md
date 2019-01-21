---
title: Atualizar seus sensores da Azure ATP | Microsoft Docs
description: Descreve como atualizar e atrasar a atualização dos sensores do ATP do Azure.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/14/2019
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 603d9e09-a07d-4357-862f-d5682c8bc3dd
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f2df8f8f59edff7ebda3f86aae26b899913d57f8
ms.sourcegitcommit: e2daa0f93d97d552cfbf1577fbd05a547b63e95b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2019
ms.locfileid: "54314322"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*


# <a name="update-azure-atp-sensors"></a>Atualizar sensores da Azure ATP
É fundamental manter a Proteção Avançada contra Ameaças do Azure atualizada para garantir a melhor proteção possível para sua organização.

O serviço Azure ATP é atualizado algumas vezes ao mês com correções de bugs, melhorias de desempenho e novas detecções. Ocasionalmente, essas atualizações exigem uma atualização correspondente dos sensores. 

Se você não atualizar os sensores, talvez eles não consigam se comunicar com o serviço de nuvem Azure ATP, o que poderá resultar na degradação do serviço. 

A autenticação entre os sensores e o serviço de nuvem do Azure usa autenticação mútua forte baseada em certificado. 

Cada atualização é testada e validada em todos os sistemas operacionais compatíveis para causar o mínimo de impacto na rede e nas operações.

### <a name="azure-atp-sensor-update-types"></a>Tipos de atualização de sensor da Azure ATP   

Os sensores da Azure ATP são compatíveis com dois tipos de atualizações:
- Atualizações de versão secundárias: 
  - Frequentes 
  - Não exige nenhuma instalação de MSI e nenhuma alteração do Registro
  - Reinicializações do serviço de sensor da Azure ATP
  - Os controladores de domínio e o servidor não precisam ser reiniciados

- Atualizações de versão principais:
 - Raras
 - Podem exigir uma reinicialização dos controladores de domínio e dos servidores
 - Contêm alterações significativas 

> [!NOTE]
>- A reinicialização automática dos sensores (nas atualizações principais) pode ser controlada na página de configuração. 
> - O sensor da Azure ATP sempre preserva pelo menos 15% da memória e da CPU disponíveis. Se o serviço consumir uma quantidade muito grande de memória, ele será reiniciado automaticamente pelo serviço de atualizador de sensor da Azure ATP.

## <a name="delayed-sensor-update"></a>Atualização de sensor atrasada
Para que o processo de atualização seja mais gradual, a Azure ATP permite configurar um sensor como candidato à **Atualização atrasada**. 

Geralmente, os sensores são atualizados automaticamente quando o serviço de nuvem Azure ATP é atualizado. Os sensores configurados para a **Atualização atrasada** serão atualizados 24 horas após a atualização inicial do serviço de nuvem.

Assim, é possível selecionar sensores específicos nos quais a atualização ocorrerá automaticamente e atualizar o restante dos sensores de forma atrasada, somente depois que você verificar que a atualização inicial ocorreu sem problemas.

> [!NOTE]
> Se ocorrer algum erro e o sensor não for atualizado, abra um tíquete de suporte. Para proteger ainda mais seu proxy para comunicar-se somente com sua instância, confira [Configuração de proxy](configure-proxy.md).

Para configurar um sensor para atualização atrasada:

1. No portal do Azure ATP, clique no ícone de configurações e selecione **Configuração**.
2. Clique na guia **Atualizações**.
3. Na linha da tabela ao lado de cada sensor que você deseja atrasar, defina o controle deslizante **Atualização atrasada** para **Habilitado**.
4. Clique em **Salvar**.
 
## <a name="sensor-update-process"></a>Processo de atualização de sensor

A cada poucos minutos, os sensores da Azure ATP verificam se eles têm a versão mais recente. Depois que o serviço de nuvem Azure ATP é atualizado para uma versão mais recente, o serviço de sensor da Azure ATP inicia o processo de atualização:

1. O serviço de nuvem Azure ATP é atualizado para a versão mais recente.
2. O serviço de atualizador de sensor da Azure ATP reconhece que existe uma versão atualizada.
3. Os sensores que não estão definidos como **Atualização atrasada** começam o processo de atualização:
  1. O serviço de atualizador de sensor da Azure ATP recebe a versão atualizada do serviço de nuvem (em um formato de arquivo cab).
  2. O atualizador de sensor da Azure ATP valida a assinatura do arquivo.
  3. O serviço de atualizador de sensor da Azure ATP extrai o arquivo cab para uma nova pasta na pasta de instalação do sensor. Por padrão, ele será extraído para *C:\Arquivos de Programas\Sensor da Proteção Avançada contra Ameaças do Azure\<número de versão>*
  4. O serviço de atualizador de sensor da Azure ATP reinicia o serviço de sensor da Azure ATP.
  5. O serviço de sensor da Azure ATP aponta para os novos arquivos extraídos do arquivo cab.
  > [!NOTE]
  >Uma atualização secundária dos sensores não instala um MSI e não altera nenhum valor do Registro nem os arquivos do sistema. Nem mesmo uma reinicialização pendente afetará a atualização dos sensores. 
  6. Os sensores são executados com base na versão recém-atualizada.
  7. Um sensor recebe uma permissão do serviço de nuvem do Azure. Isso pode ser verificado na página **Atualizações**.
  8. O próximo sensor inicia o processo de atualização. 

4. 24 horas depois que o serviço de nuvem do ATP do Azure é atualizado, os sensores selecionados para **Atualização atrasada** começam o processo de atualização.

![atualização do sensor](./media/sensor-update.png)


Em caso de falha de atualização, se o sensor não concluir o processo de atualização, um alerta de monitoramento relevante será disparado e enviado como uma notificação.

![sensor desatualizado](./media/sensor-outdated.png)


## <a name="see-also"></a>Consulte Também

- [Configurar o encaminhamento de eventos](configure-event-forwarding.md)
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)