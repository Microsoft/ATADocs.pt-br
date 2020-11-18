---
title: Resolução de nomes de rede do Microsoft defender para identidade
description: Este artigo fornece uma visão geral do Microsoft defender para a funcionalidade de resolução de nome de rede avançada da identidade e usa o.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9b9688031ea9916a09b8beaa2ce5c67633fd935f
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94847234"
---
# <a name="what-is-network-name-resolution"></a>O que é a Resolução de nomes de rede?

A resolução de nomes de rede (NNR) é um componente principal da  [!INCLUDE [Product long](includes/product-long.md)] funcionalidade. [!INCLUDE [Product short](includes/product-short.md)] captura atividades com base no tráfego de rede, eventos do Windows e ETW-essas atividades normalmente contêm dados IP.

Usar NNR, [!INCLUDE [Product short](includes/product-short.md)] pode correlacionar entre atividades brutas (contendo endereços IP) e os computadores relevantes envolvidos em cada atividade. Com base nas atividades brutas, [!INCLUDE [Product short](includes/product-short.md)] entidades de perfis, incluindo computadores, e gera alertas de segurança para atividades suspeitas.

Para resolver os endereços IP para nomes do computador, os sensores do [!INCLUDE [Product short](includes/product-short.md)] pesquisam os endereços IP usando os seguintes métodos:

- NTLM sobre RPC (porta TCP 135)
- NetBIOS (porta UDP 137)
- RDP (porta TCP 3389): apenas o primeiro pacote do **Client hello**
- Consultas ao servidor DNS usando a pesquisa de DNS reverso do endereço IP (UDP 53)

Recomendamos o uso de todos os métodos para obter os melhores resultados. Se isso não for possível, você deverá usar o método de pesquisa de DNS e pelo menos um dos outros métodos.

> [!NOTE]
> Nenhuma autenticação é realizada em quaisquer das portas.

[!INCLUDE [Product short](includes/product-short.md)] avalia e determina o sistema operacional do dispositivo com base no tráfego de rede. Depois de recuperar o nome do computador, o [!INCLUDE [Product short](includes/product-short.md)] sensor verifica Active Directory e usa as impressões digitais TCP para ver se há um objeto de computador correlacionado com o mesmo nome de computador. O uso de impressões digitais de TCP ajuda a identificar dispositivos não registrados e não Windows, auxiliando em seu processo de investigação.
Quando o [!INCLUDE [Product short](includes/product-short.md)] sensor encontra a correlação, o sensor associa o IP ao objeto de computador.

Nos casos em que nenhum nome é recuperado, um **perfil de computador não resolvido por IP** é criado com o IP e a atividade relevante detectada.

![Perfil de computador não resolvido](media/unresolved-computer-profile.png)

Os dados da NNR são cruciais para a detecção das seguintes ameaças:

- Suspeita de roubo de identidade (Pass-the-Ticket)
- Suspeita de ataque de DCSync (replicação de serviços de diretório)
- Reconhecimento de mapeamento de rede (DNS)

Para melhorar sua capacidade de determinar se um alerta é um **verdadeiro positivo (TP)** ou **falso positivo (FP)**, [!INCLUDE [Product short](includes/product-short.md)] inclui o grau de certeza da resolução de nomes de computadores na evidência de cada alerta de segurança.

Por exemplo, quando os nomes dos computadores são resolvidos com **certeza alta**, ela aumenta a confiança no resultado do alerta de segurança como um **Verdadeiro Positivo** ou **TP**.

A evidência inclui a hora, o IP e o nome do computador para o qual o IP foi resolvido. Quando a certeza de resolução for **baixa**, use essas informações para investigar e verificar qual dispositivo era a fonte verdadeira do IP nesse momento.
Depois de confirmar o dispositivo, você poderá determinar se o alerta é um **Falso Positivo** ou **FP**, semelhante aos exemplos a seguir:

- Suspeita de roubo de identidade (pass-the-ticket) – o alerta foi disparado para o mesmo computador.
- Suspeita de ataque DCSync (replicação de serviços de diretório) – o alerta foi disparado de um controlador de domínio.
- Reconhecimento de mapeamento de rede (DNS), o alerta foi disparado de um servidor DNS.

    ![Certeza da evidência](media/nnr-high-certainty.png)

### <a name="prerequisites"></a>Pré-requisitos

|Protocolo|Transport|Porta|Dispositivo|Direção|
|--------|--------|------|-------|------|
|NTLM via RPC *|TCP|135|Todos os dispositivos na rede|Entrada|
|Output|UDP|137|Todos os dispositivos na rede|Entrada|
|RDP|TCP|3389|Todos os dispositivos na rede|Entrada|
|DNS|UDP|53|Controladores de domínio|Saída|

\* Um desses métodos é necessário, mas é recomendável usar todos eles.

Para ter certeza [!INCLUDE [Product short](includes/product-short.md)] de que está funcionando idealmente e o ambiente está configurado corretamente, [!INCLUDE [Product short](includes/product-short.md)] o verifica o status de resolução de cada sensor e emite um alerta de integridade por método, fornecendo uma lista dos [!INCLUDE [Product short](includes/product-short.md)] sensores com baixa taxa de êxito da resolução de nome ativa usando cada método.

> [!NOTE]
> Para desabilitar um método NNR opcional no [!INCLUDE [Product short](includes/product-short.md)] para atender às necessidades do seu ambiente, abra uma chamada de suporte.

Cada alerta de integridade fornece detalhes específicos do método, sensores, a política problemática, bem como recomendações de configuração.

![Alerta de baixa taxa de sucesso da Resolução de Nomes de Rede (NNR)](media/nnr-success-rate.png)

### <a name="configuration-recommendations"></a>Recomendações de configuração

- NTLM sobre RPC:
  - Verifique se a porta TCP 135 está aberta para comunicação de entrada de [!INCLUDE [Product short](includes/product-short.md)] sensores, em todos os computadores do ambiente.
  - Verifique todas as configurações de rede (firewalls), pois isso pode impedir a comunicação com as portas relevantes.

- NetBIOS:
  - Verifique se a porta UDP 137 está aberta para a comunicação de entrada de [!INCLUDE [Product short](includes/product-short.md)] sensores, em todos os computadores do ambiente.
  - Verifique todas as configurações de rede (firewalls), pois isso pode impedir a comunicação com as portas relevantes.
- RDP
  - Verifique se a porta TCP 3389 está aberta para comunicação de entrada de [!INCLUDE [Product short](includes/product-short.md)] sensores, em todos os computadores do ambiente.
  - Verifique todas as configurações de rede (firewalls), pois isso pode impedir a comunicação com as portas relevantes.
- DNS inverso:
  - O Sensor deve ser capaz de alcançar o servidor DNS e as Zonas de Pesquisa Inversa devem estar habilitadas.

## <a name="see-also"></a>Consulte Também

- [Pré-requisitos do [!INCLUDE [Product short](includes/product-short.md)]](prerequisites.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
