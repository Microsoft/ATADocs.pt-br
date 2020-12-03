---
title: Suporte a várias florestas do Microsoft defender para identidade
description: Suporte para várias florestas Active Directory no Microsoft defender para identidade.
ms.date: 10/26/2020
ms.topic: conceptual
ms.openlocfilehash: 05cf574aa56f379cb636036c382cc87fb289990e
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2020
ms.locfileid: "96544548"
---
# <a name="product-long-multi-forest-support"></a>[!INCLUDE [Product long](includes/product-long.md)] suporte a várias florestas

## <a name="multi-forest-support-set-up"></a>Configuração de suporte a várias florestas

[!INCLUDE [Product long](includes/product-long.md)] o oferece suporte a organizações com várias florestas, oferecendo a você a capacidade de monitorar facilmente a atividade e os usuários de perfil entre as florestas.

As organizações normalmente têm várias florestas do Active Directory, geralmente usadas para finalidades diferentes, incluindo infraestrutura herdada de fusões e aquisições corporativas, distribuição geográfica e limites de segurança (florestas vermelhas). Você pode proteger várias florestas usando [!INCLUDE [Product short](includes/product-short.md)] o, fornecendo a capacidade de monitorar e investigar toda a rede por meio de um único painel de vidro.

A capacidade de dar suporte a várias florestas do Active Directory permite:

- Veja e investigue as atividades executadas pelos usuários em várias florestas usando um único painel de controle.
- Melhor detecção e redução de falsos positivos, fornecendo integração avançada do Active Directory e a resolução de conta.
- Maior controle e implantação facilitada. Alertas de integridade e relatórios aprimorados para cobertura entre organizações quando os controladores de domínio são todos monitorados de um único [!INCLUDE [Product short](includes/product-short.md)] console.

## <a name="product-short-detection-activity-across-multiple-forests"></a>[!INCLUDE [Product short](includes/product-short.md)] atividade de detecção em várias florestas

Para detectar atividades entre florestas, os [!INCLUDE [Product short](includes/product-short.md)] sensores consultam controladores de domínio em florestas remotas para criar perfis para todas as entidades envolvidas, (incluindo usuários e computadores de florestas remotas).

- [!INCLUDE [Product short](includes/product-short.md)] os sensores podem ser instalados em controladores de domínio em todas as florestas, mesmo em florestas sem confiança.
- Adicione credenciais adicionais na página serviços de diretório para dar suporte a florestas não confiáveis em seu ambiente.
  - Somente uma credencial é necessária para dar suporte a todas as florestas com uma relação de confiança bidirecional.
  - Credenciais adicionais só são necessárias para cada floresta com confiança não Kerberos ou sem confiança.
  - Há um limite padrão de 10 florestas não confiáveis por [!INCLUDE [Product short](includes/product-short.md)] instância. Fale com o suporte se sua organização tiver mais de dez florestas.

![Estágio 1 de boas-vindas do [!INCLUDE [Product short](includes/product-short.md)]](media/directory-services-add-no-trust-forests.png)

### <a name="requirements"></a>Requisitos

- O usuário que você configura no [!INCLUDE [Product short](includes/product-short.md)] console do em **serviços de diretório** deve ser confiável em todas as outras florestas e deve ter, pelo menos, permissão somente leitura para executar consultas LDAP nos controladores de domínio.
- Se [!INCLUDE [Product short](includes/product-short.md)] sensores autônomos forem instalados em computadores autônomos, em vez de diretamente nos controladores de domínio, verifique se os computadores têm permissão para se comunicar com todos os controladores de domínio de floresta remota usando LDAP.

- Para que o [!INCLUDE [Product short](includes/product-short.md)] se comunique com os [!INCLUDE [Product short](includes/product-short.md)] sensores e [!INCLUDE [Product short](includes/product-short.md)] sensores autônomos, abra as seguintes portas em cada computador em que o [!INCLUDE [Product short](includes/product-short.md)] sensor está instalado:

  |Protocolo|Transport|Porta|Para/De|Direção|
  |----|----|----|----|----|
  |**Portas de Internet**||||
  |SSL (*.atp.azure.com)|TCP|443|Serviço de nuvem do [!INCLUDE [Product short](includes/product-short.md)]|Saída|
  |**Portas internas**||||
  |LDAP|TCP e UDP|389|Controladores de domínio|Saída|
  |LDAP seguro (LDAPS)|TCP|636|Controladores de domínio|Saída|
  |LDAP para o Catálogo Global|TCP|3268|Controladores de domínio|Saída|
  |LDAPS para o Catálogo Global|TCP|3269|Controladores de domínio|Saída|

## <a name="multi-forest-support-network-traffic-impact"></a>Impacto do tráfego de rede no suporte a várias florestas

Quando [!INCLUDE [Product short](includes/product-short.md)] o mapeia suas florestas, ele usa um processo que afeta o seguinte:

- Depois [!INCLUDE [Product short](includes/product-short.md)] que o sensor estiver em execução, ele consultará as florestas de Active Directory remota e recuperará uma lista de usuários e dados do computador para a criação do perfil.
- A cada 5 minutos, cada [!INCLUDE [Product short](includes/product-short.md)] sensor consulta um controlador de domínio de cada domínio, de cada floresta, para mapear todas as florestas na rede.
- Cada [!INCLUDE [Product short](includes/product-short.md)] sensor mapeia as florestas usando o objeto "trustedDomain" no Active Directory, fazendo logon e verificando o tipo de confiança.
- Você também poderá ver o tráfego ad hoc quando o [!INCLUDE [Product short](includes/product-short.md)] sensor detectar a atividade entre florestas. Quando isso ocorrer, os [!INCLUDE [Product short](includes/product-short.md)] sensores enviarão uma consulta LDAP para os controladores de domínio relevantes a fim de recuperar as informações da entidade.

## <a name="known-limitations"></a>Limitações conhecidas

- Logons interativos executados por usuários em uma floresta para acessar recursos em outra floresta não são exibidos no [!INCLUDE [Product short](includes/product-short.md)] painel.

## <a name="see-also"></a>Consulte Também

- [Ferramenta de dimensionamento do [!INCLUDE [Product short](includes/product-short.md)]](https://aka.ms/aatpsizingtool)
- [Arquitetura do [!INCLUDE [Product short](includes/product-short.md)]](architecture.md)
- [Instalar o [!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [Confira o fórum do [!INCLUDE [Product short](includes/product-short.md)]!](https://aka.ms/MDIcommunity)
