---
# required metadata

title: Perguntas técnicas frequentes sobre o ATA | Microsoft Advanced Threat Analytics
description: Fornece uma lista de perguntas frequentes sobre o ATA e as respostas associadas.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Perguntas técnicas frequentes sobre o ATA
Este artigo fornece uma lista de perguntas frequentes sobre o ATA e também as respostas e outras informações.

## Perguntas frequentes sobre o ATA

|Pergunta|Resposta|
|------------|-----------------------------------|
|O Gateway do ATA não inicia, o que devo fazer?|Procure o erro mais recente no log de erros atual (No local onde o ATA está instalado, na pasta "Logs").|
|Como posso testar o ATA?|Você pode simular atividades suspeitas, que é um teste de ponta a ponta, seguindo um destes procedimentos:<br /><br />1.  Reconhecimento de DNS usando Nslookup.exe<br />2.  Execução remota usando psexec.exe<br /><br />Isso deve ser executado no controlador de domínio que está sendo monitorado e não no Gateway de ATA.|
|Como verificar o Encaminhamento de Eventos do Windows?|Você pode executar o seguinte em um prompt de comando no diretório:  **\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**:<br /><br />mongo ATA --eval "printjson(db.getCollectionNames())" &#124; find /C "NtlmEvents"`|
|O ATA funciona com tráfego criptografado?|O tráfego criptografado não será analisado (por exemplo: LDAPS, ESP IPSEC).|
|O ATA funciona com Kerberos Armoring?|Há suporte para a habilitação do Kerberos Armoring (também conhecido como FAST [encapsulamento seguro de autenticação flexível]) pelo ATA, com exceção da passagem de detecção de hash, que não funcionará.|
|De quantos Gateways de ATA eu preciso?|Há duas coisas a serem consideradas ao descobrir de quantos gateways você precisa:<br /><br />-   A quantidade total de tráfego produzida por seus controladores de domínio determina o número mínimo de Gateways de ATA dos quais você precisará para lidar com o ambiente do Active Directory, de uma perspectiva de desempenho.<br />    Para ler mais informações sobre como determinar a quantidade de tráfego produzido por seus controladores de domínio, confira [Planejamento de Capacidade de ATA](/advanced-threat-analytics/PlanDesign/ata-capacity-planning).<br />-   As limitações operacionais do espelhamento de porta também determinam a quantidade de Gateways de ATA que você precisa para oferecer suporte a todos os controladores de domínio, por exemplo: por comutador, por datacenter, por região. Cada ambiente tem seus próprios aspectos.|
|Qual a quantidade de armazenamento necessária para o ATA?|Para cada dia inteiro com uma média de 1000 pacotes/s, você precisa de 1,5 GB de armazenamento.<br /><br />Para saber mais, confira [Planejamento de capacidade de ATA](/advanced-threat-analytics/PlanDesign/ata-capacity-planning).|
|Por que determinadas contas são confidenciais?|Isso ocorre quando uma conta é membro de determinados grupos que podemos chamar de confidenciais (por exemplo: "Administradores do Domínio").<br />Para entender por que uma conta é confidencial, você pode examinar sua associação de grupo para entender a quais grupos confidenciais ela pertence (o grupo ao qual ela pertence também pode ser confidencial devido a outro grupo, portanto, o mesmo processo deve ser executado até que você localize o grupo confidencial de nível mais alto).|
|Como monitorar o controlador de domínio virtual?|Você pode ter Gateways de ATA físico ou virtual, conforme descrito em [Configurar o espelhamento da porta](/advanced-threat-analytics/PlanDesign/configure-port-mirroring).  <br />A maneira mais fácil é ter um Gateway de ATA virtual em cada host no qual o controlador de domínio virtual exista.<br />Se os controladores de domínio virtuais se movimentarem entre os hosts, será necessário executar um destes procedimentos:<br /><br />-   Quando o controlador de domínio virtual for movido para outro host, pré-configure o Gateway de ATA nesse host para receber o tráfego do controlador de domínio virtual movimentado recentemente.<br />-   Certifique-se de que você esteja afiliado ao Gateway de ATA virtual com o controlador de domínio virtual, de modo que se ele for movido, o Gateway de ATA será movido com ele.<br />-   Há alguns comutadores virtuais que podem enviar o tráfego entre os hosts.|
|Como fazer backup do ATA?|Há duas coisas das quais fazer backup:<br /><br />-   A configuração do ATA, que é armazenada no banco de dados e copiada em backup automaticamente a cada hora. <br />-   O tráfego e os eventos armazenados pelo ATA, que podem sobre backup usando qualquer procedimento de backup de banco de dados com suporte, para saber mais, confira [Gerenciamento de banco de dados do ATA](/advanced-threat-analytics/DeployUse/ata-database-management)|
|O que o ATA pode detectar?|Para obter a lista completa de detecções do ATA, confira [O que é o Microsoft Advanced Threat Analytics?](/advanced-threat-analytics/Understand/what-is-ata).|
|Qual tipo de armazenamento eu preciso para o ATA?|Recomendamos o armazenamento rápido (e não discos de 7.200 RPM) com números de baixa latência (menos de 10 ms) e uma configuração RAID que oferece suporte a cargas intensas de gravação (não o RAID-5/6 e seus derivados).|
|De quantos NICs o Gateway de ATA precisa?|O Gateway de ATA requer um mínimo de dois adaptadores de rede:<br>1. Uma NIC para se conectar à rede interna e à Central de ATA<br>2. Uma NIC para capturar o tráfego de rede do controlador de domínio por meio do espelhamento de porta.<br>* Isso não se aplica ao Gateway leve|
|Que tipo de integração o ATA tem com o SIEMs?|O ATA tem uma integração bidirecional com o SIEMs, da seguinte maneira:<br>
1. O ATA pode ser configurado para enviar um alerta de Syslog, no caso de uma atividade suspeita, para qualquer servidor SIEM que ofereça suporte ao formato CEF.<br>2. O ATA pode ser configurado para receber mensagens do Syslog para cada evento do Windows com a ID 4776, destes [SIEMs](/advanced-threat-analytics/PlanDesign/configure-event-collection#SIEMsupport).|


<!--HONumber=Apr16_HO2-->


