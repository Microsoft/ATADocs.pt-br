---
title: Resolução de nomes de rede da proteção avançada contra ameaças do Azure
description: Este artigo fornece uma visão geral dos usos e da funcionalidade avançada de resolução de nomes de rede do ATP do Azure.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/22/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1ac873fc-b763-41d7-878e-7c08da421cb5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4c98696b11ba329b6b907003b86cc5bd3d111cdf
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912708"
---
# <a name="what-is-network-name-resolution"></a>O que é a Resolução de nomes de rede?

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

A resolução de nomes de rede (NNR) é um componente principal da funcionalidade do Azure ATP. O ATP do Azure captura atividades com base no tráfego de rede, nos eventos do Windows e no ETW, atividades que normalmente contêm dados de IP.

Usando o NNR, o Azure ATP pode correlacionar entre atividades brutas (que contêm endereços IP) e os computadores relevantes envolvidos em cada atividade. Com base nas atividades brutas, o ATP do Azure cria perfis de entidades, incluindo computadores, e gera alertas de segurança de atividades suspeitas.

Para resolver os endereços IP para nomes do computador, os sensores do ATP do Azure pesquisam os endereços IP usando os seguintes métodos:

- NTLM sobre RPC (porta TCP 135)
- NetBIOS (porta UDP 137)
- RDP (porta TCP 3389): apenas o primeiro pacote do **Client hello**
- Consultas ao servidor DNS usando a pesquisa de DNS reverso do endereço IP (UDP 53)

Recomendamos o uso de todos os métodos para obter os melhores resultados. Se isso não for possível, você deverá usar o método de pesquisa de DNS e pelo menos um dos outros métodos.

> [!NOTE]
> Nenhuma autenticação é realizada em quaisquer das portas.

O ATP do Azure avalia e determina o sistema operacional do dispositivo com base no tráfego de rede. Depois de recuperar o nome do computador, o sensor do ATP do Azure verifica o Active Directory e usa impressões digitais de TCP para ver se há um objeto de computador correlacionado com o mesmo nome do computador. O uso de impressões digitais de TCP ajuda a identificar dispositivos não registrados e não Windows, auxiliando em seu processo de investigação.
Quando o sensor do ATP do Azure encontra a correlação, ele associa esse IP ao objeto de computador.

Nos casos em que nenhum nome é recuperado, um **perfil de computador não resolvido por IP** é criado com o IP e a atividade relevante detectada.

![Perfil de computador não resolvido](media/unresolved-computer-profile.png)

Os dados da NNR são cruciais para a detecção das seguintes ameaças:

- Suspeita de roubo de identidade (Pass-the-Ticket)
- Suspeita de ataque de DCSync (replicação de serviços de diretório)
- Reconhecimento de mapeamento de rede (DNS)

Para melhorar a capacidade de determinar se um alerta é um **Verdadeiro Positivo (TP)** ou um **Falso Positivo (FP)**, a ATP do Azure inclui o grau de certeza de resolução do nome do computador na evidência de todos os alertas de segurança.

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

Para ter certeza de que o Azure ATP está funcionando de forma ideal e que o ambiente está configurado corretamente, o Azure ATP verifica o status de resolução de cada sensor e emite um alerta de integridade por método, fornecendo uma lista dos sensores do Azure ATP com baixa taxa de êxito da resolução de nome ativa usando cada método.

> [!NOTE]
> Abra uma chamada de suporte para desabilitar um método NNR opcional no ATP do Azure para atender às necessidades do seu ambiente.

Cada alerta de integridade fornece detalhes específicos do método, sensores, a política problemática, bem como recomendações de configuração.

![Alerta de baixa taxa de sucesso da Resolução de Nomes de Rede (NNR)](media/atp-nnr-success-rate.png)

### <a name="configuration-recommendations"></a>Recomendações de configuração

- NTLM sobre RPC:
  - verifique se a porta TCP 135 está aberta para a comunicação de entrada de sensores do ATP do Azure em todos os computadores no ambiente.
  - Verifique todas as configurações de rede (firewalls), pois isso pode impedir a comunicação com as portas relevantes.

- NetBIOS:
  - verifique se a porta UDP 137 está aberta para a comunicação de entrada de sensores do ATP do Azure em todos os computadores no ambiente.
  - Verifique todas as configurações de rede (firewalls), pois isso pode impedir a comunicação com as portas relevantes.
- RDP
  - Verifique se a porta TCP 3389 está aberta para a comunicação de entrada de sensores do Azure ATP em todos os computadores no ambiente.
  - Verifique todas as configurações de rede (firewalls), pois isso pode impedir a comunicação com as portas relevantes.
- DNS inverso:
  - O Sensor deve ser capaz de alcançar o servidor DNS e as Zonas de Pesquisa Inversa devem estar habilitadas.

## <a name="see-also"></a>Consulte Também

- [Pré-requisitos do Azure ATP](prerequisites.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)
