---
title: Atualizar sensores do ATP do Azure
description: Descreve como atualizar e atrasar a atualização dos sensores do ATP do Azure.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 12/24/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 603d9e09-a07d-4357-862f-d5682c8bc3dd
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0e2a5c24b2dac7675f55e2279ccaa11897e154ef
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/21/2020
ms.locfileid: "90826627"
---
# <a name="update-azure-atp-sensors"></a>Atualizar sensores da Azure ATP

Manter a Proteção Avançada contra Ameaças do Azure atualizada garante a melhor proteção possível para sua organização.

O serviço ATP do Azure é atualizado algumas vezes ao mês com novas detecções, recursos e melhorias de desempenho. Essas atualizações normalmente exigem uma atualização menor correspondente nos sensores. Os sensores do ATP do Azure e as atualizações correspondentes nunca têm permissões de gravação nos controladores de domínio. Os pacotes de atualização do sensor controlam apenas o sensor do ATP do Azure e recursos de detecção de sensor. 

### <a name="azure-atp-sensor-update-types"></a>Tipos de atualização de sensor da Azure ATP    

Os sensores do ATP do Azure são compatíveis com dois tipos de atualizações:
- Atualizações de versão secundárias: 
    - Frequentes 
    - não exige nenhuma instalação de MSI e nenhuma alteração do Registro
    - Com reinicialização: serviços do sensor do ATP do Azure 
    - Sem reinicialização: serviços de controlador de domínio e sistema operacional de servidor

- Atualizações de versão principais:
    - Raras
    - Contém alterações significativas 
    - Com reinicialização: serviços do sensor do ATP do Azure
    - Possível reinicialização necessária: serviços de controlador de domínio e sistema operacional de servidor

> [!NOTE]
>- Controle as reinicializações automáticas de sensor (para atualizações **principais**) na página de configuração do portal do ATP do Azure. 
> - O sensor do ATP do Azure reserva sempre pelo menos 15% da memória e da CPU disponíveis no controlador de domínio no qual está instalado. Se o serviço do ATP do Azure consumir uma quantidade muito grande de memória, ele será automaticamente interrompido e reiniciado pelo serviço do atualizador de sensor do ATP do Azure.

## <a name="delayed-sensor-update"></a>Atualização de sensor atrasada

Dada a velocidade rápida de atualizações contínuas de desenvolvimento e lançamento do ATP do Azure, você pode decidir definir um grupo de subconjuntos em seus sensores como um grupo de atualização com atraso, permitindo um processo de atualização gradual de sensores. O ATP do Azure permite que você escolha como os sensores são atualizados e defina cada sensor como um candidato a **Atualização atrasada**.  

Os sensores não selecionados para atualização atrasada são atualizados automaticamente sempre que o serviço do ATP do Azure for atualizado. Os sensores definidos como **Atualização atrasada** são atualizados com um atraso de 72 horas após o lançamento oficial de cada atualização de serviço. 

A opção **Atualização atrasada** permite que você selecione sensores específicos como um grupo de atualização automática, no qual todas as atualizações são distribuídas automaticamente, e que você defina o restante de seus sensores para atualizar em atraso, proporcionando tempo para confirmar que o sensores automaticamente atualizados foram bem-sucedidos.

> [!NOTE]
> Se ocorrer algum erro e o sensor não for atualizado, abra um tíquete de suporte. Para proteger ainda mais seu proxy para comunicar-se somente com sua instância, confira [Configuração de proxy](configure-proxy.md).
A autenticação entre os sensores e o serviço de nuvem do Azure usa autenticação mútua forte baseada em certificado. 

Cada atualização é testada e validada em todos os sistemas operacionais compatíveis para causar o mínimo de impacto na rede e nas operações.


Para configurar um sensor para atualização atrasada:

1. No portal do Azure ATP, clique no ícone de configurações e selecione **Configuração**.
1. Clique na guia **Atualizações**.
1. Na linha da tabela ao lado de cada sensor que você deseja atrasar, defina o controle deslizante **Atualização atrasada** para **Habilitado**.
1. Clique em **Salvar**.
 
## <a name="sensor-update-process"></a>Processo de atualização de sensor

A cada poucos minutos, os sensores da Azure ATP verificam se eles têm a versão mais recente. Depois que o serviço de nuvem Azure ATP é atualizado para uma versão mais recente, o serviço de sensor da Azure ATP inicia o processo de atualização:

1. O serviço de nuvem do ATP do Azure é atualizado para a versão mais recente.
1. O serviço de atualizador de sensor do ATP do Azure reconhece que existe uma versão atualizada.
1. Os sensores que não estejam definidos com **Atualização atrasada** começam o processo de atualização em uma base de sensor a sensor:
   1. O serviço de atualizador de sensor do ATP do Azure recebe a versão atualizada do serviço de nuvem (no formato de arquivo cab).
   2. O atualizador de sensor do ATP do Azure valida a assinatura do arquivo.
   3. O serviço de atualizador de sensor do ATP do Azure extrai o arquivo cab para uma nova pasta na própria pasta de instalação do sensor. Por padrão, ele será extraído em *C:\Arquivos de Programas\Sensor da Proteção Avançada contra Ameaças do Azure\<version number>*
   4. O serviço de sensor do ATP do Azure aponta para os novos arquivos extraídos do arquivo cab.    
   5. O serviço de atualizador de sensor do ATP do Azure reinicia o serviço de sensor do ATP do Azure.
       > [!NOTE]
      >Os sensores de atualizações menores não instalam o MSI e não alteram nenhum valor de registro ou os arquivos do sistema. Até mesmo uma reinicialização pendente não tem impacto sobre uma atualização do sensor. 
   6. Os sensores são executados com base na versão recém-atualizada.
   7. O sensor recebe uma permissão do serviço de nuvem do Azure. Você pode verificar o status do sensor na página **Atualizações**.
   8. O próximo sensor inicia o processo de atualização. 

1. Em 72 horas após a atualização do serviço de nuvem do ATP do Azure, os sensores selecionados para a **Atualização atrasada** iniciam seu processo de atualização de acordo com o mesmo processo de atualização dos sensores atualizados automaticamente.

![Atualização do sensor](media/sensor-update.png)


Se algum sensor não concluir o processo de atualização, o alerta de integridade relevante será disparado e enviado como uma notificação.

![Falha na atualização do sensor](media/sensor-outdated.png)


## <a name="see-also"></a>Consulte Também

- [Configurar o encaminhamento de eventos](configure-event-forwarding.md)
- [Pré-requisitos do Azure ATP](prerequisites.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
