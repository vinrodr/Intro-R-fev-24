Documento Exemplo
================
Vinicius Rodrigues
February 27, 2024

# Produção de relatórios e análise de dados reproduzívies

Talvez se lembre dos primeiros encontros, quando disse que uma das
características mais louváveis da pesquisa científica e análise de dados
era que o binômio script + environment garantia a reprodutibilidade.
Pois, então: agora veremos ferramentas que ajudam a demonstrar que não
manipulamos os resultados de um paper ou de uma tarefa.

![](irreproducible.png)\<!../irreproducible.png\> BAKER, Monya. (2016)
“1,500 scientists lift the lid on reproducibility”. Nature, volume 533,
pages 452–454.

### 1. R Project - organizando sem problemas de ‘path’

Quando você foi se preparar para resolver o Desafio 1, precisou fazer
uso das funções *getwd()* e *setwd()* para ver o caminho (*path*) do seu
diretório. Isso por que, precisava substituir o meu endereço que estava
no exemplo do código, certo? A estrutura de pastas onde meu *working
directory* funcionava era diferente do seu. Mas eu tenho novidades. O R
permite que você envie o seu *script* para outra pessoa sem este
problema, que pode acabar sendo fonte de erros e perda de arquivos.

A ferramenta de ‘projetos em R’ resolve esse problema, pois salva uma
pasta que contém diversos arquivos. Essa pasta é do tipo **.Rproj**, que
o RStudio abre normalmente já com todos os scripts, arquivos de *input*
e todos os *outputs*. O que isso significa? Que caso queiramos abrir um
arquivo *.csv* dentro desta pasta, não será preciso especificar a
referência completa do arquivo, apenas seu nome. Na prática, o seu
*working directory* se converte automaticamente na pasta do seu
**.Rproj**. Por exemplo, podemos substituir o código:

> nova_pasta \<- “C:\User\Name\Projects\New\2024\Examples\\”
>
> path_meus_dados \<- file.path(nova_pasta, “meus_dados.txt”)
>
> tabela \<- read.table(meus_dados, header = T, sep = “,”)

pelo código:

> tabela \<- read.table(“meus_dados.txt”, header = T, sep = “,”)

Então, para que você abra um Projeto no R, basta que observe o caminho
na sua barra de tarefas (**File -\> New Project -\> New Directory -\>
New Project**), insira o nome da pasta do projeto e clique em **Create
Project**.

Mas veja: O arquivo **.Rproj** é apenas uma pasta, que automaticamente
converte-se no seu *working directory*. Por isso, quando você criar um
projeto, ainda é preciso que abra um script e o salve nesta mesma pasta,
certo? Igualmente, caso queira salvar seu *Global Environment* (.RData),
também precisa salvar seu arquivo na pasta do projeto.

Para que não reste dúvida: Ao optar pelo uso do R Project, você não
precisa mais utilizar a função *setwd()*, pois o R irá utilizar a pasta
que é seu projeto para ler e gravar arquivos.

### 2. Produzindo relatórios com RMarkdown (.Rmd)

Provavelmente quando você procurou este curso para aprender R, você
pretendia automatizar análises e rotinas. Devia imaginar que produziria
seus resultados, mas continuaria a escrever e preparar seus documentos
em Word-Microsoft/Writer-Broffice/Pages-IOS. Mas o R permite que você
produza documentos elegantes, que podem incluir, caso queira, seu
código\*\*\*\* e os resultados da sua análise: tabelas, gráficos, mapas,
páginas web, dashboards, livros, apresentações etc.

\*\*\*\*Bônus: Como o Rmarkdown é mantigo pelo RStudio, um IDLE que tem
buscado incorporar diferentes linguagens, você pode incorporar códigos
em R, Python, Markdown/LaTeX, HTML, CSS, SQL e outros num único arquivo.

O RMarkdown faz uso de funções muito similares ao LaTeX, que é comumente
utilizado para produção de relatórios científicos. Essa característica
permite que você incorpore fórmulas e símbolos de maneira relativamente
simples e com resultados esteticamente superiores.

**DICA:** Caso você tenha curiosidade, já conhecendo ou não o LaTeX,
deixo aqui uma ferramenta que facilita e muito o mundo da produção de
artigos científicos. No endereço <https://pt.overleaf.com/> você pode
escrever seus documentos cheios de fórmulas com uma gramática
*friendly*. Com estas duas ferramentas (RMarkdown e overleaf) já pode
abandonar o LaTeX.

#### Começando

Como já vimos, o *script* do R produz um arquivo do tipo **.R**, que
pode ser lido num bloco de notas ou abrir diretamente no seu RStudio. Os
arquivos produzidos no RMarkdown são do tipo **.Rmd**, mas você pode
produzir um PDF, Documento Word ou um site HTML simplesmente alterando
uma opção.

Talvez tenha ficado confuso, como um **.Rmd** vai virar um documento
**.doc**? Acontece que para rodar em seu ambiente RStudio, o arquivo tem
terminação **.Rmd**, mas em qualquer momento você poderá solicitar ao R
que transforme este arquivo em um arquivo, por exemplo, Documento Word
(.doc).

Certo, entendido isso, vamos instalar a biblioteca do RMarkdown.

``` r
# Instalando a biblioteca
install.packages("rmarkdown")

# Carregando a biblioteca
library(rmarkdown)
```

Agora, vamos abrir um arquivo RMarwdown. Dois caminhos: O ícone abaixo
de “File” da barra de tarefas. Você já havia utilizado para criar um
*script*, agora vai abrir um arquivo RMarkdown. A segunda forma, você
segue o caminho da barra de tarefas (**File -\> New File -\> R
Markdown**).

Apareceu uma janela para você, certo? Nesta janela você escolherá o
título do documento, o autor e um formato *default* para o *output*. Das
opções das janelas à esquerda, mantenha como “documento”. Embora você
tenha feito tais escolhas, você poderá alterar a qualquer tempo.

> {r setup, include = TRUE} knitr::opts_chunk\$set(echo = TRUE)

Além do que está aí em cima, há um conteúdo gerado por *default*, sempre
que você cria um arquivo **.Rmd**. É como um manual pequeno de como
funciona e você pode ler se quiser. Mas feito isso, apague. NÃO TUDO!
Pode apagar tudo para baixo do primeiro *chunck* - que é o nome que
damos para estes pedaços do arquivo que aceitam código.

O cabeçalho e este primeiro *chunck* devem estar em todo e qualquer
arquivo RMarkdown que você criar. A razão do cabeçalho é um pouco
autoevidente, embora você possa deixar ‘author’ e ‘date’ em branco. Já o
primeiro *chunck* serve para você estabelecer o padrão para todos os
demais - por exemplo, caso queira que todos os meus códigos fiquem
ocultos e o documento gerado apresente só os resultados da análise, devo
criar um argumento **‘include = FALSE’**.

São inúmeras possibilidades, que você vai se acostumando conforme
utiliza o pacote, mas saiba que como na escolha do cabeçalho, você pode
mudar a configuração padrão que estabeleceu no primeiro *chunck* - seja
para todos os demais, seja individualmente fazendo diferente dos demais.
Isso é bem lógico, já que você pode ter a necessidade de mostrar seu
código em alguma parte do seu relatório e não em outro.

Certo, vamos fazer um teste. Tente inserir um *chunck*. De novo, duas
maneiras: Ou você usa o ícone na barra de tarefas **da sua aba .Rmd**,
que é um quadrado verde com um “c” no meio e um símbolo de soma + … Se
tiver difícil de achar, do lado direito há uma seta pra cima, uma para
baixo e o atalho para executar o código –\> RUN. Ao clicar neste ícone
vai abrir uma lista, escolha a primeira opção: R. Outra maneira de
inserir um *chunck* em seu arquivo .Rmd é usar o atalho **Ctrl+Alt+I**.

Nos dois casos, aparecerá uma caixa cinza, onde você poderá escrever seu
código.

Você poderá utilizar estes *chunck* para incluir toda e qualquer função,
de qualquer pacote. O RMarkdown será a integração entre o seu software
editor de texto e sua ferramenta de análise de dados - como já havia
adiantado lá em cima.

Então, agora talvez esteja mais claro. **TUDO** o que você escrever fora
destes *chuncks* será considerado como texto e tudo que estiver dentro
do *chunck* será considerado código - para inclusive, executar os
comandos/funções e apresentar os resultados (imagens, tabelas, mapas
etc). Mas se lembre que os *chuncks* serão executados na ordem em que
aparecem no documento!!!! Não adinta você executar um código do
tidyverse, sem antes ter carregado esse pacote com *library()* neste
*chunck* ou em outro anterior.

Percebeu a facilidade? Como trabalhamos com diversos tipos de conteúdo
no nosso cotidiano, integrar os arquivos e informações não será mais um
problema. Seu código, seu texto, suas tabelas geradas pelo código, seus
gráficos idem, suas fórmulas e equações…. tudo isso no mesmo lugar!

Assim, dentro do seu arquivo **.Rmd**:

- 1)  No corpo do script ficará seu texto, onde poderá escrever como se
      estivesse em seu editor de texto (ex. Microsoft Word). Apenas
      observando as regras do LaTeX para formatação e estilo.

- 2)  Nos *chunks* (caixas cinzas) ficará seu código, onde poderá
      escrever como se estivesse usando um *script* do tipo **.R**.

|     Digite no corpo |      Digite no *chunk* |
|--------------------:|-----------------------:|
|           Seu texto |            Código de R |
| Equações (em Latex) | Tabelas, gráficos, etc |

#### Formatação de texto básico

Certo, nem tudo são flores! É bem mais *friendly* escrever num editor de
textos, mas o RMarkdown tem a vantegem de, uma vez aprendido, não
precisará mais usar botões. Por aqui, o funcionamento é baseado em
caracteres, que indicam a formatação do texto que os seguem. Talvez você
já tenha usado negrito, itálico … no seu Whatsapp. Se sim, é a mesma
coisa.

Resumidamente:

- para itálico (*Italic*), use \* ou \_ (ao começo e ao final do seu
  texto).

- para negrito (**Bold**), use \*\* ou \_\_ (ao começo e ao final do seu
  texto).

- Os títulos são sempre antecedidos de \# (hashtag), e quanto maior o
  número de \####… menor será o tamanho deste título. Ou seja, caso você
  use apenas um \#, isso significa que é o principal. \# Big Header \##
  Sub-Header \### Sub-Sub-Header \#### Sub-Sub-Sub-Header \#####
  Sub-Sub-Sub-Sub-Header …

- Os links devem ser escritos dentro de (parênteses), sendo que o nome
  que permanece no hyperlink antecede envolto por colchetes –\> []()
  [link que te leva para o google](http:\\www.google.com)

- Para que você abra um parágrafo, você precisa (i) ou inserir dois
  espaços; (ii) inserir uma linha com ‘enter’.

- Para abrir uma lista de itens, você pode usar: (i) hífen **-**,
  ou (ii) asterísco \*, ou numerais.

- Para que você crie sub-itens, é preciso que insira quatro espaços,
  sempre na linha inferior e inserir um símbolo de soma +

- Bullets

  - Sub-Bullets

1.  Numbered List
2.  Numbered List
    - 2.1. Sub-Numbered List

Para mais detalhes, veja o
[cheatsheet](https://www.rstudio.com/wp-content/uploads/2015/02/rmarkdown-cheatsheet.pdf)
do RMarkdown - aquele mapa mental com as funções do pacote.

#### Para inserir equações/fórmulas

Como adiantei, podemos escrever fórmulas e equações (como fazemos com o
LaTeX) aqui no RMarkdown. Se você já tentou inserir uma simples fórmula
de somatória no Word sabe do que estou falando. Pois bem, por aqui a
inclusão deste tipo de informação é muito mais bonita e estilosa.

Para inserir uma equação qualquer no corpo do seu texto, até mesmo
dentro de uma frase, basta que você use **cifrões \$** em volta da
equação que pretende escrever. Como você fez acima com o itálico. Caso
você deseje inserir a equação centralizada no corpo do seu texto e
separada das demais frases, basta inserir a equação entre **dois pares
de cifrões \$\$**, como você fez com o negrito ali acima.

Vamos usar o exemplo de α2+β2=χ2. A sintaxe, entre duplas de cifrões é
assim: ^2 + ^2 = ^2

$$\alpha^2 + \beta^2 = \chi^2$$ Bonito, não? Mais um exemplo:
1–√2∗a2b=a4b. Ficaria assim: \* =

$$\frac{\sqrt{1}}{2} * \frac{a}{2b} = \frac{a}{4b}$$

E para não deixar a somatória de lado, ficaria assim: \_0^{10} x = …

$$\sum_0^{10} x = ...$$ De novo, você vê todos os caracteres e códigos
na documentação do pacote. Mas vai aí uma facilidade, onde você escreve
sua fórmula e o editor online retorna como seria o código
[aqui](https://latex.codecogs.com/eqneditor/editor.php?lang=pt-br). De
toda maneira, vou lembrar você que podem fazer uso do
[OverLeaf](https://www.overleaf.com/).

#### Parâmetros do *chunck*

Lá atrás eu havia advertido sobre o primeiro *chunck* que funciona como
*setup* dos demais. Além disso, disse que poderia alterar a qualquer
tempo o *default* ou cada *chunck* individualmente. Mas não disse quais
seriam os parâmetros de mais relevância. Acho que vale a pena pontuar
alguns - para todos os demais, veja
[aqui](https://yihui.org/knitr/options/#chunk-options).

> \`\`{r, echo = FALSE}

Vai impedir que o código ‘bruto’ apareça no seu relatório
gerado/documento final.

> \`\`{r, eval = FALSE}

Este atributo preveni a **execução** do seu código! Suponha que queira
elaborar um tutorial de R e precise que o código permaneça ali sem
rodar? Pois então, foi assim que eu fiz.

> \`\`{r, warning = FALSE, message = FALSE}

Como nesta altura você já deve ter instalado um pacote no R, já viu
também aquelas mensagens de ‘warning’ e ‘conflict’ que aparecem as
vezes. Pois bem, quando você coloca estes atributos, previne que o R
coloque estas informações poluindo seu relatório final.

Por fim, caso queira alterar o *setup* do seu *default*, você deve usar
o atalho abaixo:

``` r
knitr::opts_chunk$set(echo = F, warning=F, message=F)
```

E, por fim, acho que vale a pena o parâmetro que controla o tamanho dos
gráficos, tabelas e figuras gerados. Para que seus resultados não fiquem
deslocados do seu texto.

> {r, out.width = “100%”}

#### Código na linha (‘in line code’): inserindo valores no seu texto

Outra coisa legal do RMarkdown é que você pode reservar um espaço no seu
texto para exibir um valor simples, mas que depende da execução de um
código. Por exemplo, caso você queira colocar o valor da área construída
de um edifício, mas precise efetuar alguns cálculos e não tenha o valor
na mão.

Para inserir o resultado que é o valor do objeto ‘area’ do código acima,
basta que você escreva *r area* entre duas crases **\`**.

> A área construída do edifício é exatamente 1256.6370614.

#### Produzindo um documento final (*output*)

Certo, agora que você já tem uma base, deve estar querendo saber como
produz o seu documento final. É bem simples. Basta que você vá na barra
de tarefas da aba do seu arquivo **.Rmd**, no ícone que tem um novelo de
lã com a palavra **Knit**.

Ao clicar no **Knit** abrirá uma lista de opções para você, sendo que a
primeira será o *default* que escolheu ao criar seu arquivo **.Rmd** e
consta lá no seu cabeçalho na linha ‘output:’.

Alguns detalhes sobre isso. Para criar outputs em Word ou HTML não há
segredo, basta que escolha estas opções. Entretanto, para criar arquivos
do tipo pdf, precisará instalar também o [LATEX for Windows
Complete](https://miktex.org/download).
