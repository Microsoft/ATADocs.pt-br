---
# required metadata

title: [TÍTULO DO ARTIGO | NOME DO SERVIÇO]
description:
keywords:
author: [GITHUB USERNAME]
manager: [ALIAS]
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: [GET ONE FROM guidgenerator.com]

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer: [ALIAS]
#ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Modelo de markdown e de metadados

Esse modelo docs.ms contém exemplos de sintaxe de redução e orientações sobre como definir os metadados. Ele está disponível no diretório raiz de cada repositório EM piloto (por exemplo, ~/Azure-RMSDocs-pr /template.md) e deve ser lido como um arquivo de redução, embora você possa consultar [a versão publicada](https://stage.docs.microsoft.com/en-us/rights-management/template) para ver como os exemplos de redução foram processados.

Ao criar uma um arquivo de markdown, copie o modelo em um novo arquivo, preencha metadados conforme especificado abaixo, defina o cabeçalho H1 acima como o título do artigo e exclua o conteúdo. 


## Metadados 

O bloco de metadados completo está acima, dividido nos campos necessários e opcionais. Consulte as [anotações de referência de metadados OPS](https://ppe.msdn.microsoft.com/en-us/ce-csi-docs/ops/ops-onboarding/managing-content/content-meta-data) para obter mais detalhes. Algumas observações importantes:

- Você **precisa** ter um espaço entre os dois-pontos (:) e o valor de um elemento de metadados.
- Se um elemento de metadados opcional não tiver um valor, remova o comentário do elemento com um # (não deixe em branco ou use "na"). Se você estiver adicionando um valor a um elemento que teve o comentário removido, não deixe de remover o #.
- Dois-pontos em um valor (por exemplo, um título) interrompem o analisador de metadados. Em seu lugar, use a codificação HTML &#58; (por exemplo, "title: Azure Rights Management& #58; noções básicas | Azure RMS").
- **title**: esse título aparecerá nos resultados da pesquisa. O título deve terminar com uma barra vertical (|) seguida do nome do serviço (por exemplo, veja acima). O título não precisa (e provavelmente não deve) ser idêntico ao título do seu cabeçalho H1. Ele deve ter aproximadamente 65 caracteres (incluindo | NOME DO SERVIÇO)
- **author**, **manager**, **reviewer**: o campo author deve conter o **nome de usuário Github** do autor, não seu alias.  Por outro lado, os campos "manager" e "reviewer" devem conter aliases. ms.reviewer especifica o nome do PM associado ao artigo ou serviço.
- **ms.assetid**: esse é o GUID do artigo do CAPS. Ao criar um novo arquivo de markdown, obtenha um GUID em [https://www.guidgenerator.com](https://www.guidgenerator.com). 
- **ms.prod**, **ms.service**, **ms.technology**, **ms.devlang**, **ms.topic**, **ms.tgt_pltfrm**: os valores possíveis para esses elementos podem ser encontrados [aqui](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default).

## GFM e markdown básico

Todos os markdowns básicos e GFM têm suporte. Para saber mais sobre estas configurações, confira:

- [Sintaxe de markdown de linha de base](https://daringfireball.net/projects/markdown/syntax)
- [Documentação do GFM (Github-flavored markdown)](https://guides.github.com/features/mastering-markdown)

## Títulos

Acima, temos exemplos de cabeçalhos de primeiro e segundo nível. 

Somente um cabeçalho de primeiro nível **pode** existir no seu tópico, que será exibido como o título na página.  

Títulos de segundo nível irão gerar o Sumário na página que aparece na seção "Neste artigo" embaixo do título da página.

### Cabeçalho de terceiro nível
#### Cabeçalho de quarto nível
##### Cabeçalho de quinto nível
###### Cabeçalho de sexto nível

## Estilo do texto

*Itálico* 

**Negrito** 

~~Tachado~~



## Links

Para vincular a um arquivo de markdown no mesmo repositório, use [links relativos](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2). 

- Exemplo: [o que é o Azure Rights Management?](./understand-explore/what-is-azure-rights-management.md)

Para vincular a um cabeçalho no mesmo arquivo de markdown, exiba o código-fonte do artigo publicado, localize a ID de cabeçalho (por exemplo, `id="blockquote"`) e vincule usando # + ID (por exemplo, `#blockquote`).

- Exemplo: [Blockquotes](#blockquote)

Para vincular a um cabeçalho em um arquivo de markdown no mesmo repositório, use link relativo + link de hashtag.

- Exemplo: [visão técnica do processo de inscrição](./understand-explore/rms-for-individuals-user-signup.md#technical-overview-of-the-sign-up-process)

Para vincular a um arquivo externo, use a URL completa como o link.

- Exemplo: [Github](http://www.github.com)

Se aparecer uma URL em um arquivo de markdown, ela será transformada em um link clicável.

- Exemplo: http://www.github.com

## Listas

### Listas ordenadas

1. Isso 
1. É
1. Um
1. Ordenado
1. Lista  


#### Lista ordenada com uma lista incorporada

1. Aqui
1. vem
1. um
1. inserido
    1. Srta. Rosa
    1. Professor Black
1. ordenado
1. lista


### Listas não ordenadas

- Isso
- é
- a
- com marcadores
- lista


##### Lista não ordenada com uma lista incorporada

- Isso 
- com marcadores 
- lista
    - Dona Violeta
    - Sr. Marinho
- contém  
- outro
    1. Coronel Mostarda
    1. Dona Branca
- listas


## Régua horizontal

---

## Tabelas

| Tabelas        | São           | Legais  |
| ------------- |:-------------:| -----:|
| a col. 3 está      | alinhada à direita | R$ 1600 |
| a col. 2 está      | centralizada      |   R$ 12 |
| a coluna 1 é, por padrão, | alinhada à esquerda     |    R$ 1 |


## Código

### Codeblock

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }

### Código em linha

Este é um exemplo de `in-line code`.

## Blockquotes

> A seca já durava dez milhões de anos, e o reino dos terríveis lagartos havia terminado há tempos. Aqui no Equador, no continente que um dia seria conhecido como África, a batalha pela sobrevivência atingiu um novo clímax de ferocidade, e o vencedor ainda não era conhecido. Nesta terra estéril e desértica, apenas os pequenos, os velozes ou os selvagens poderiam prosperar, ou mesmo ter esperança de sobreviver.

## Imagens

### Imagem Estática

![este é o texto alternativo](./media/AzRMS_elements.png)

### Imagem Vinculada

[![aTexto de longo prazo para imagem vinculada](./media/AzRMS_elements.png)](https://azure.microsoft.com) 

### Gif animado

![gif animado](./media/hololens.gif)

## Alertas

### Observação

> [!NOTE] Isso é OBSERVAÇÃO

### Aviso

> [!WARNING] Isso é um AVISO

### Dica

> [!TIP] Isso é uma DICA

### Importante

> [!IMPORTANT] Isso é IMPORTANTE

## Vídeos

### Channel 9

<iframe src="http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>


### Youtube

<iframe width="420" height="315" src="https://www.youtube.com/embed/R6_eWWfNB54" frameborder="0" allowfullscreen></iframe>

## docs.ms extentions
Estas são as extensões disponíveis:

### Botão

> [!div class="button"] [links de botão](/rights-management)

### Seletor

> [!div class="op_single_selector"]
- [foo](/rights-management/template.md)
- [bar](/rights-management/scratch.md)

### Passo a passo

>[!div class="step-by-step"] [Voltar](https://www.example.com)
[Avançar](https://www.example.com)

<!--HONumber=May16_HO3-->


