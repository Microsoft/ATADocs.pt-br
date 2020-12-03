---
title: Atualizar os sensores do Microsoft Defender para Identidade
description: Descreve como atualizar e atrasar atualizações de sensores no Microsoft Defender para Identidade.
ms.date: 10/27/2020
ms.topic: how-to
ms.openlocfilehash: 6db4db087f64431812a3998f2c79f066dfb09ea2
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96542389"
---
# <a name="update-product-long-sensors"></a>Atualizar sensores do [!INCLUDE [Product long](includes/product-long.md)]

Para fornecer a melhor proteção possível para sua organização, mantenha os sensores do [!INCLUDE [Product long](includes/product-long.md)] atualizados.

O serviço do [!INCLUDE [Product long](includes/product-long.md)] é atualizado algumas vezes por mês com novas detecções, recursos e melhorias de desempenho. Essas atualizações normalmente exigem uma atualização menor correspondente nos sensores. Os sensores do [!INCLUDE [Product short](includes/product-short.md)] e as atualizações correspondentes nunca têm permissões de gravação nos controladores de domínio. Os pacotes de atualização do sensor controlam apenas o sensor do [!INCLUDE [Product short](includes/product-short.md)] e recursos de detecção de sensor.

## <a name="product-short-sensor-update-types"></a>Tipos de atualização dos sensores do [!INCLUDE [Product short](includes/product-short.md)]

Os sensores do [!INCLUDE [Product short](includes/product-short.md)] dão suporte a dois tipos de atualizações:

- Atualizações de versão secundárias:
  - Frequentes
  - não exige nenhuma instalação de MSI e nenhuma alteração do Registro
  - Reiniciado: serviços de sensor do [!INCLUDE [Product short](includes/product-short.md)]
  - Sem reinicialização: serviços de controlador de domínio e sistema operacional de servidor

- Atualizações de versão principais:
  - Raras
  - Contém alterações significativas
  - Reiniciado: serviços de sensor do [!INCLUDE [Product short](includes/product-short.md)]
  - Possível reinicialização necessária: serviços de controlador de domínio e sistema operacional de servidor

> [!NOTE]
>
> - Controle as reinicializações automáticas de sensor (para atualizações **principais**) na página de configuração do portal do [!INCLUDE [Product short](includes/product-short.md)].
> - O sensor do [!INCLUDE [Product short](includes/product-short.md)] reserva sempre pelo menos 15% da memória e da CPU disponíveis no controlador de domínio no qual está instalado. Se o serviço do [!INCLUDE [Product short](includes/product-short.md)] consumir uma quantidade muito grande de memória, ele será automaticamente interrompido e reiniciado pelo serviço do atualizador de sensor do [!INCLUDE [Product short](includes/product-short.md)].

## <a name="delayed-sensor-update"></a>Atualização de sensor atrasada

Dada a velocidade rápida de atualizações contínuas de desenvolvimento e lançamento do [!INCLUDE [Product short](includes/product-short.md)], você pode decidir definir um grupo de subconjuntos em seus sensores como um grupo de atualização com atraso, permitindo um processo de atualização gradual dos sensores. O [!INCLUDE [Product short](includes/product-short.md)] permite que você escolha como os sensores serão atualizados e defina cada sensor como um candidato à **Atualização atrasada**.

Os sensores não selecionados para atualização atrasada serão atualizados automaticamente sempre que o serviço do [!INCLUDE [Product short](includes/product-short.md)] for atualizado. Os sensores definidos como **Atualização atrasada** são atualizados com um atraso de 72 horas após o lançamento oficial de cada atualização de serviço.

A opção **Atualização atrasada** permite que você selecione sensores específicos como um grupo de atualização automática, no qual todas as atualizações são distribuídas automaticamente, e que você defina o restante de seus sensores para atualizar em atraso, proporcionando tempo para confirmar que o sensores automaticamente atualizados foram bem-sucedidos.

> [!NOTE]
> Se ocorrer algum erro e o sensor não for atualizado, abra um tíquete de suporte. Para proteger ainda mais seu proxy para comunicar-se somente com sua instância, confira [Configuração de proxy](configure-proxy.md).
A autenticação entre os sensores e o serviço de nuvem do Azure usa autenticação mútua forte baseada em certificado.

Cada atualização é testada e validada em todos os sistemas operacionais compatíveis para causar o mínimo de impacto na rede e nas operações.

Para configurar um sensor para atualização atrasada:

1. No portal do [!INCLUDE [Product short](includes/product-short.md)], clique no ícone de engrenagem e selecione **Configuração**.
1. Clique na guia **Atualizações**.
1. Na linha da tabela ao lado de cada sensor que você deseja atrasar, defina o controle deslizante **Atualização atrasada** para **Habilitado**.
1. Clique em **Salvar**.

## <a name="sensor-update-process"></a>Processo de atualização de sensor

A cada poucos minutos, os sensores do [!INCLUDE [Product short](includes/product-short.md)] verificam se eles têm a versão mais recente. Depois que o serviço de nuvem do [!INCLUDE [Product short](includes/product-short.md)] é atualizado para a versão mais recente, o serviço de sensor do [!INCLUDE [Product short](includes/product-short.md)] inicia o processo de atualização:

1. O serviço de nuvem do [!INCLUDE [Product short](includes/product-short.md)] é atualizado para a versão mais recente.
1. O serviço de atualizador de sensor do [!INCLUDE [Product short](includes/product-short.md)] reconhece que existe uma versão atualizada.
1. Os sensores que não estejam definidos com **Atualização atrasada** começam o processo de atualização em uma base de sensor a sensor:
    1. O serviço de atualizador de sensor do [!INCLUDE [Product short](includes/product-short.md)] recebe a versão atualizada do serviço de nuvem (no formato de arquivo cab).
    1. O atualizador de sensor do [!INCLUDE [Product short](includes/product-short.md)] valida a assinatura do arquivo.
    1. O serviço de atualizador de sensor do [!INCLUDE [Product short](includes/product-short.md)] extrai o arquivo cab para uma nova pasta na própria pasta de instalação do sensor. Por padrão, ele será extraído em *C:\Arquivos de Programas\Sensor da Proteção Avançada contra Ameaças do Azure\<version number>*
    1. O serviço de sensor do [!INCLUDE [Product short](includes/product-short.md)] aponta para os novos arquivos extraídos do arquivo cab.
    1. O serviço de atualizador de sensor do [!INCLUDE [Product short](includes/product-short.md)] reinicia o serviço de sensor do [!INCLUDE [Product short](includes/product-short.md)].
        > [!NOTE]
        > Os sensores de atualizações menores não instalam o MSI e não alteram nenhum valor de registro ou os arquivos do sistema. Até mesmo uma reinicialização pendente não tem impacto sobre uma atualização do sensor.
    1. Os sensores são executados com base na versão recém-atualizada.
    1. O sensor recebe uma permissão do serviço de nuvem do Azure. Você pode verificar o status do sensor na página **Atualizações**.
    1. O próximo sensor inicia o processo de atualização.

1. Em 72 horas após a atualização do serviço de nuvem do [!INCLUDE [Product short](includes/product-short.md)], os sensores selecionados para a **Atualização atrasada** iniciam seu processo de atualização de acordo com o mesmo processo dos sensores atualizados automaticamente.

![Atualização do sensor](media/sensor-update.png)

Se algum sensor não concluir o processo de atualização, o alerta de integridade relevante será disparado e enviado como uma notificação.

![Falha na atualização do sensor](media/sensor-outdated.png)

## <a name="see-also"></a>Consulte Também

- [Configurar o encaminhamento de eventos](configure-event-forwarding.md)
- [Pré-requisitos do [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
