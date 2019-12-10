---
title: Tutorial de alertas de exportação do ATP do Azure | Microsoft Docs
d|Description: This article explains the Azure ATP alerts issued when attacks typically part of exfiltration phase efforts are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 02/11/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 452d951c-5f49-4a21-ae10-9fb38c3de302
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 704e372952d1b02fdcf6564bad26ebc4c7d184f2
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "65196868"
---
# <a name="tutorial-exfiltration-alerts"></a>Tutorial: Alertas de exfiltração  

Normalmente, os ataques cibernéticos são lançados contra alguma entidade acessível, como um usuário com poucos privilégios e, em seguida, se movem lateralmente com rapidez até que o invasor obtenha acesso a ativos valiosos. Os ativos valiosos podem ser contas confidenciais, administradores de domínio ou dados altamente confidenciais. O ATP do Azure identifica essas ameaças avançadas na origem ao longo de toda a cadeia de ataque e classifica-as nas seguintes fases:

1. [Reconhecimento](atp-reconnaissance-alerts.md)
2. [Credenciais comprometidas](atp-compromised-credentials-alerts.md)
3. [Movimentos laterais](atp-lateral-movement-alerts.md)
4. [Comprometimento de domínio](atp-domain-dominance-alerts.md)
5. **Exportação**

Para entender melhor a estrutura e os componentes comuns de todos os alertas de segurança do ATP do Azure, confira [Entendendo os alertas de segurança](understanding-security-alerts.md)

Os alertas de segurança a seguir ajudam você a identificar e corrigir atividades suspeitas da fase de **Exportação** detectadas pelo ATP do Azure em sua rede. Neste tutorial, aprenda como entender, classificar, evitar e corrigir os ataques a seguir:

> [!div class="checklist"]
> * Comunicação suspeita por DNS (ID 2031 externa)
> * Exportação de dados por SMB (ID 2030 externa)

## <a name="suspicious-communication-over-dns-external-id-2031"></a>Comunicação suspeita por DNS (ID 2031 externa) 

*Nome anterior*: Comunicação suspeita por DNS

**Descrição**

Normalmente, na maioria das organizações, o protocolo DNS não é monitorado e raramente é bloqueado para atividade mal-intencionada. Isso permite que um invasor entre em um computador comprometido abusando do protocolo DNS. A comunicação mal-intencionada por DNS pode ser usada para extração, comando e controle de dados e/ou fuga de restrições de rede corporativa.

**TP, B-TP ou FP?**
 
Algumas empresas usam o DNS legitimamente para a comunicação regular. Para determinar o status do alerta de segurança:

1. Verifique se o domínio de consulta registrado pertence a uma fonte confiável, como o provedor de antivírus.  
    - Considere-a uma atividade **B-TP** se o domínio for conhecido e confiável e se as consultas DNS forem permitidas. *Feche* o alerta de segurança e exclua o domínio de futuros alertas.  
    - Se o domínio de consulta registrado não for confiável, identifique o processo de criação da solicitação no computador de origem. Use o [Process Monitor](https://docs.microsoft.com/sysinternals/downloads/procmon) para auxiliar com essa tarefa.

**Entender o escopo da violação**

1. No computador de destino, que deve ser um servidor DNS, verifique os registros do domínio em questão.
    - A qual IP ele está correlacionado?
    - Quem é o proprietário do domínio?
    - Onde está o IP?
1. Investigue os [computadores de origem e de destino](investigate-a-computer.md).

**Correção sugerida e etapas de prevenção**

1. Contenha o computador de origem.
    - Encontre a ferramenta que realizou o ataque e remova-a.
    - Procure por usuários que estavam conectados em horário próximo àquele da atividade, pois eles também podem estar comprometidos. Redefina as senhas e habilite o MFA.
2. Se, após a investigação, o domínio de consulta registrado for considerado não confiável, recomendamos que você bloqueie o domínio de destino para evitar todas as comunicações futuras.

> [!NOTE]
> Os alertas de segurança da *comunicação suspeita em DNS* listam o domínio suspeito. Novos domínios, ou domínios recentemente adicionados que ainda não sejam conhecidos nem reconhecidos pelo Azure ATP, mas que fazem parte ou são conhecidos por fazer parte de sua organização podem ser fechados.

## <a name="data-exfiltration-over-smb-external-id-2030"></a>Exportação de dados por SMB (ID 2030 externa)

**Descrição** Os controladores de domínio têm os dados organizacionais mais confidenciais. Para a maioria dos invasores, uma das principais prioridades é obter acesso de controlador de domínio, para roubar seus dados mais confidenciais. Por exemplo, a exportação do arquivo Ntds.dit, armazenado no controlador de domínio, permite que um invasor falsifique o TGT (tíquetes que concedem tíquete) Kerberos fornecendo autorização para qualquer recurso. Os TGTs Kerberos forjados permite que o invasor defina a expiração do tíquete para qualquer momento arbitrário. Um alerta de **Exportação de dados por SMB** do ATP do Azure é disparado quando transferências de dados suspeitas são observadas em seus controladores de domínio monitorados.

**TP, B-TP ou FP**
1. Esses usuários devem copiar esses arquivos para este computador?  
    - Se a resposta à pergunta anterior for **sim**, **feche** o alerta de segurança e exclua o computador como uma atividade **B-TP**.

**Entender o escopo da violação**
1. Investigue os [usuários de origem](investigate-a-user.md).  
2. Investigue os [computadores de origem e de destino](investigate-a-computer.md) das cópias. 

**Correção sugerida e etapas de prevenção**
1. Redefina a senha dos usuários de origem e habilite a MFA.
2. Contenha o computador de origem.
    - Encontre a ferramenta que realizou o ataque e remova-a.
    - Localize os arquivos que foram copiados e remova-os. 
    <br>Verifique se houve outras atividades nesses arquivos. Eles foram transferidos para outro lugar? Verifique se eles foram transferidos para fora da rede da organização? 
    - Procure por usuários que estavam conectados em horário próximo àquele da atividade, pois eles também podem estar comprometidos. Redefina as senhas e habilite o MFA.
3. Se um dos arquivos for o **ntds.dit**:
    - Altere o Tíquete de concessão de tíquete Kerberos (KRBTGT) duas vezes de acordo com as diretrizes em [Scripts de redefinição de senha da conta KRBTGT disponíveis agora para clientes](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) usando a [ferramenta Redefinir chaves/senha da conta KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51). 
    - A redefinição dupla do KRBTGT invalida todos os tíquetes Kerberos nesse domínio. A invalidação de todos os tíquetes Kerberos no domínio significa que **todos** os serviços serão interrompidos e não funcionarão novamente até que sejam renovados ou em alguns casos, que o serviço seja reiniciado.

    - **Planeje cuidadosamente antes de executar a redefinição dupla do KRBTGT. A redefinição dupla do KRBTGT afeta todos os computadores, servidores e usuários no ambiente.**

   - Feche todas as sessões existentes dos controladores de domínio. 

## <a name="see-also"></a>Consulte Também

- [Investigar um computador](investigate-a-computer.md)
- [Trabalhando com alertas de segurança](working-with-suspicious-activities.md)
- [Trabalhando com caminhos de movimento lateral](use-case-lateral-movement-path.md)
- [Alertas de reconhecimento](atp-reconnaissance-alerts.md)
- [Alertas de credencial comprometida](atp-compromised-credentials-alerts.md)
- [Alertas de movimento lateral](atp-lateral-movement-alerts.md)
- [Alertas de predominância de domínio](atp-domain-dominance-alerts.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
