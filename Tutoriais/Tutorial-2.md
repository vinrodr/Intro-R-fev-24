Tutorial 2
================

## R Base

Lembremos que o R é uma linguagem funcional de alto nível direcionada a
objetos. E o que isso quer dizer? Vimos que é funcional por ser
implementada a partir de um roteiro de comandos (funções), mas o que
seria de alto nível? Isso diz respeito ao papel de intermediação que a
linguagem realiza com o sistema binário que o seu chip entende. Ao invés
de exigir que você reproduza uma linguagem binária, o R (como outras
linguagens) permite que você implemente uma linguagem acessível e ele
mesmo faz o trabalho pesado. Evidentemente, que isso não significa que o
R não tenha suas regras e estrutura, mas é muito mais simples que
aprender binário.

Certo, mas por que isso é relevante? Por que a linguagem tem funções
pré-configuradas (R base) e também está aberta a elaboração de outras
pelos desenvolvedores.

Assim, a linguagem é modular por que é composta por pacotes de
bibliotecas (packages) e um módulo básico com funcionalidade necessária
para análises estatísticas e matemáticas mais comuns. E se você acabou
de se perguntar a respeito dos demais pacotes, tenho uma ótima notícia:
existem **literalmente** milhares de bibliotecas (pacotes), que foram
construídas para os mais diversos fins e ramos científicos. A comunidade
R é vibrante e gigantesca.

Se ficou um pouco confuso: os Pacotes (packages) são conjuntos de
funções (ou seja, de comandos), que também podem guardar dados em
diferentes formatos. Normalmente, o início de nosso aprendizado fazemos
uso de *datasets* salvos em formato de pacote. São exemplos fictícios de
banco de dados, que o usuário carrega com o comando **library()** e
utiliza para testar/aprender os comandos mais usuais na linguagem R.

Vamos tentar? Carregue o pacote *datasets*, que contém diversos banco de
dados. Como o pacote já vem instalado com o R Base, basta tornar as
funções disponíveis *para uso nesta sessão específica* com o
comando/função *library()*:

``` r
library(datasets)
```

E como seria se o pacote não estivesse instalado? Neste caso, você
precisa usar a função *install.packages()* e, após a instalação,
utilizar a função *library()* para tornar as funções disponíveis. E a
resposta é sim! Você precisa carregar cada biblioteca/pacote sempre que
iniciar suas análises. Por este motivo, é usual que o cabeçalho do
script tenha todas as libraries que você irá precisar na sua análise.
Para praticar, tente você. Carregue o pacote *RColorBrewer* para uso.
Spoiler: Provavelmente, ele não está instalado na sua máquina.

``` r
library(RColorBrewer)
```

E por fim, voltando àquela definição: a linguagem é voltada a objetos. O
que é isso? Aqui é a referência de que a programação é orientada para
objetos, isto é, tudo o que é criado no ambiente do R (sejam gráficos,
análises, números, documentos, data-frames, funções, endereços web …)
são efetivamente objetos - e olha que facilidade: estarão todos no seu
global environment.

## O console

A linha de comando do R (painel abaixo à esquerda) só admite que o
usuário encaminhe um comando de cada vez. É o próprio software R
incorporado no R Studio. Ele aparece com o símbolo *\>* quando está
pronto para receber um comando. Há outras duas situações, que são de
execução e de espera.

Para a situação de execução, não há nenhum sinal na linha de comando e
não é possível inserir nenhum comando. Isso pode ser notado quando o
código demanda um esforço computacional relevante, que acaba demorando.
É bem simples de perceber esta situação, pois o R Studio cria um ícone
de **stop** em forma de placa de trânsito que surge no alto direito do
painel do console.

![](STOP.png)<!-- -->

Tente você colando este código no seu console (spoiler: ele tem um
erro):

``` r
for(n in 1:20000) prod(1:n)
```

Já o estado de espera ocorre quando o usuário envia um comando
**incompleto**. O R, então, retorna um símbolo de adição *+* na própria
linha de comando. Tente executar a primeira linha do código abaixo e
espere. Depois insira a segunda linha. O resultado será igual ao que
aparece na terceira linha.

``` r
> sqrt(
+ 2)
[1] 1.414214
> 
```

Quando inserimos uma função de raiz quadrada sem fechar o parênteses,
surge a inconsistência e o console retorna com o sinal de espera (+),
considerando que há algo incompleto. Caso você digite o parêntese
faltante e mande executar com a tecla enter, o resultado da raiz surge
como um número e a linha de comando volta a estar disponível como mostra
o sinal (\>) na última linha.

Mas veja, dificilmente nós optamos por inserir a informação faltante
diretamente no console, já que o script permaneceria errado. Assim,
quando surgir o sinal de espera, use a tecla *esc* para sair da espera e
corrija o código.

## Criando objetos no R: Sintaxe básica de comandos

- Há algumas regras na estrutura da linguagem R.

  - todas as funções precedem parênteses *ex. read.csv()*

  - todos os objetos são criados nomeando à esquerda do símbolo *\<-* ,
    que é uma seta formada pelo símbolo de menor e um hífen. **Tente
    criar um objeto com seu nome**:

``` r
unifesp <- c(10)
unifesp
```

Neste exemplo, ao utilizar a função conjunto, eu criei um objeto chamado
unifesp que vai guardar o valor numérico 10. Não se preocupe com os
valores, somente perceba a estrutura, pois ela que irá se repetir. Após,
a segunda linha de comando pede para o R informar o conteúdo do objeto
unifesp e o resultado é o numeral 10.

Perceba, você pode dar qualquer nome para o conjunto com o numeral 10!!!
Eu pedi que usasse seu nome para perceber que qualquer palavra ou texto
que venha antes de \<- é o nome do objeto que foi criado e está guardado
no seu global environment. Esta ação de criar um objeto no global
environment é chamada de *assignment*.

**Obs.** Você também poderá criar objetos (assignment) usando o símbolo
de igual (=), entretanto, é recomendável que não faça. Pode gerar muita
confusão no seu código e no seu desenvolvimento posterior, pois o
símbolo de igual *=* é utilizado para atribuir valores aos argumentos
das funções.

**Obs.2** Você não deve utilizar as chamadas *reserved words* para
nomear seus objetos. Isso por que o R reserva uma série de nomes para
suas próprias funções e argumentos ex. você não poderá criar um objeto
chamado NULL, NA, false, if, else, repeat, for, function …. Há uma lista
delas, que você encontra executando o código abaixo - mas não se
preocupe que não precisa decorar.

``` r
help(reserved)
?reserved
```

``` r
?reserved
```

As funções (algoritmos) apresentam argumentos dos mais diferentes,
conforme a finalidade para a qual elas foram construídas. Um exemplo
tornará isso claro:

``` r
sqrt(x = 2)
sqrt(2)

log(x = 8, base = 2)
log(8,2)
```

A função de cálculo da raiz quadrada só dispõe de um argumento, que é o
valor ao qual desejamos calcular e vem representado por x. Como só há um
argumento, é desnecessário escrevermos x = 2, por exemplo; basta sqrt(2)
para termos o resultado.

Já a função logaritmo tem dois argumentos, a base e o logaritmando.
Também não haveria necessidade de escrevermos *x =* e *base =*, bastando
manter a ordenação dos argumentos na função e separando os argumentos
por vírgula, que o R entenderá. Entretanto, as melhores práticas
recomendam que indique os nomes dos argumentos na função. Isso se torna
mais comum, pois existem funções com dezenas de argumentos!

E lembre-se, a função help() trará o *vignette* com a descrição de todos
os argumentos da função que deseja conhecer! Viu como você irá usar com
frequência!? Em suma, podemos perceber uma estrutura de sintaxe básica
como:

> **função (argumento1 = valor, argumento2 = valor, …)**.
>
> **qualquer_nome \<- atributos_do_objeto_criado**

## Mas espere, de onde o R armazena e de onde ele pega seus arquivos?

Quando você der o comando *q()*, o R irá iniciar o fechamento do
programa. Mas isso nos ajuda a entender conceitos importantes: a área
virtual, a sessão e o diretório de trabalho ( *workspace*).

Ao iniciar o R, você irá iniciar uma sessão. E o diretório de trabalho é
aquele endereço (local ou externo) onde o R irá buscar ou armazenar
arquivos. Para verificar qual é o seu diretório de trabalho você pode
usar o comando:

> getwd()

Caso queira alterar este diretório, use a função:

> setwd()

Dessa maneira, a sessão sempre será iniciada vinculada a um *workspace*!
Sempre tenha isso em mente ao salvar seus arquivos ou buscá-los. Tudo o
que você fizer: de cálculos e análises estatísticas a gráficos, imagens
e banco de dados tudo estará no seu *working directory* (wd)

Mas veja, quando você sai do R (comando q() ou pelo Idle Rstudio) será
questionado se deseja gravar o seu *working directory*. Ainda que não
tenha produzido arquivos .jpeg, .xls, .csv, .txt etc, você pode salvar
os objetos que guardam seus avanços na análise. Ou seja, é possível
gravar todos os objetos do seu *Global Environment* em um arquivo do
tipo *.RData*. Você poderá carregar este arquivo a qualquer momento que
desejar e continuar suas análises.

Note que o *Script* só é um arquivo texto com comandos em disposição
sequencial. Portanto, não guarda nenhum dos objetos que você trabalhou.
Repetindo para fixar: O script (arquivo no formato .R) e o Global
Environment (arquivo no formato .RData) devem ser salvos separadamente!

## Funções também são objetos: Visualizar e Apagar objetos

Por vezes você terá muitos objetos em seu environment e ao invés de
ficar procurando na barra de rolagem do painel, usará a função:

> ls()

Outra função são recorrente quanto help() é a utilizada para apagar
objetos do seu environment. Para isso você deve usar:

> rm()

**Obs.** Lembre-se que ao criar os objetos, você não gravou o workspace
em seu disco rígido! Esta tudo na memória RAM e desaparece
automaticamente caso você feche sem salvar (inclusive, crash por falta
de memória ou mesmo chutar uma tomada!). Por este motivo é importante
gravar periodicamente seu workspace.

> save.image() \# grava o workspace como “.RData”
>
> save.image(file=“qualquer_nome.RData”) \# gravará o workspace com nome
> dado “qualquer_nome.RData”

Mais um lembrete! Caso não dê um nome, possivelmente o arquivo ficará em
sua pasta de arquivos ocultos!

## Errors and Warnings

Retomamos a ideia de linguagem aqui, para diferenciar dos idiomas
humanos. Enquanto um pequeno erro não costuma gerar grandes problemas de
compreensão para uma conversa entre amigos, caso você cometa um pequeno
equívoco na linguagem R, sua mensagem será incompreensível (ou
compreendida de maneira diversa da pretendida) pelo software.

Mas nem tudo são problemas! O R retorna uma mensagem de erro sempre que
acontecer isso. E basta que você leia (embora seja mais comum que copiar
o erro e colar na barra de busca do google) para identificar onde errou.
Tente copiar os exemplos abaixo em seu R Studio para ver os resultados.

``` r
logaritmo(5)
```

``` r
log(5))
```

``` r
log(5, basse=50)
```

``` r
log(5, base=50)
```

Há outros casos em que o R retorna um resultado, mas possivelmente não
era o que você esperaria. Nestes casos, o console retorna um resultado
com uma (ou mais) mensagem de alerta (warning).

``` r
log(-5)
```

    ## Warning in log(-5): NaNs produzidos

    ## [1] NaN

## Linguagem voltada a objetos

**O R aceita uma grande quantidade de tipos de objetos e isso é uma das
forças da linguagem**. Mas acaba sendo difícil apresentar cada um dos
tipos por este mesmo motivo.

Mas vejamos alguns tipos mais comuns:

## Operações matemáticas e vetores atômicos

Caso você não soubesse nada a respeito da sintaxe do R, muito
provavelmente não teria dificuldade em usar seu console como uma
calculadora para operações matemáticas simples.

O R em sua forma mais básica pode ser uma calculadora, obedecendo os
seguintes operadores:

|    Operadores     | Símbolos |  Exemplos   |
|:-----------------:|:--------:|:-----------:|
|      Adição       |    \+    |  5 + 3 = 8  |
|     Subtração     |    \-    |  5 - 2 = 3  |
|   Multiplicação   |    \*    | 2 \* 3 = 6  |
|      Divisão      |    /     | 10 / 5 = 2  |
|   Exponenciação   |    ^     |  2 ^ 3 = 8  |
| Divisão SEM resto |    %%    | 17 %% 3 = 5 |

**Obs**. Divisão sem resto: Caso você deseje obter somente o valor de
uma divisão desconsiderando os valores decimais, basta usar os símbolos.

Bom, mas caso você usasse o R só como calculadora, não iria atribuir um
nome ao resultado da operação matemática (ou seja, não iria criar um
objeto).

**Atenção aqui**: Haverá dois usos para o termo variável. O primeiro
deles será um sinônimo para *coluna* em um *data frame*. Isso fica mais
claro se você lembrar que as linhas de um banco de dados fazem
referência aos valores de cada observação. Por exemplo, caso eu deseje
construir um banco de dados com as respostas do CENSO 2022. Serão
milhões de linhas correspondendo cada uma a um entrevistado. As colunas
deste mesmo *data frame* serão as variáveis de interesse (ou seja, as
perguntas feitas pelo CENSO). As células em que há o match da linha com
a coluna, obviamente, serão preenchidas com o conjunto de respostas de
cada cidadão às perguntas feitas pelo entrevistador, por exemplo, a
primeira coluna poderia ser a variável “idade”, a segunda “renda”, e
assim por diante. Ainda iremos nos reverir à variável enquanto objeto no
R. Iremos cambiar entre os significados, mas não se preocupe que com o
tempo você se acostumará.

Vamos dar mais um passo e abandonar a calculadora. O R também permite o
armazenamento de valores como ‘objetos’, descritos por um nome. Uma vez
criado, o objeto fica disponível para o restante do script e fica no
Environment. Então, vamos criar uma variável (objeto) e atribuir um
valor a ele. Criando a variável “U”, eu atribui (\<-) o valor numérico
100. Neste exemplo, eu crei um vetor atômico (*atomic vector*), pois ele
tem tamanho unitário.

``` r
U <- 100
```

Podemos ‘imprimir’ o conteúdo de uma variável no console, meramente
digitando seu nome e teclando enter:

``` r
U
```

Outra opção é utilizar a função *print*, que existe em diversas
linguagens, para imprimir:

``` r
print(U)
```

Se você se perguntou quando usar cada opção, a resposta é um pouco
esquiva. Você verá no futuro que a depender do caso é preciso explicitar
a função *print* para que o código funcione. O exemplo mais corriqueiro
é a ação de chamar a variável dentro de funções ou encadeamentos. Mas,
por enquanto, só tenha em mente que existem ambas possibilidades.

- E se você usasse os objetos para realizar operações?

Talvez você tenha se perguntado, será que conseguiria somar objetos?
Ótima notícia, sim. Dentro da sintaxe aceita, você pode indicar os nomes
das variáveis ao invés de lançar valores. Veja o exemplo:

``` r
R <- 5
U <- 100

R + U
R - U
R / U
R * U
```

Vamos deixar as coisas mais interessantes. Podemos intercalar objetos e
valores em operações diversas, e armazenar seu resultado em uma nova
variável. Veja os exemplos:

``` r
V1 <- 100 / 5
V2 <- R + U
V3 <- ((V2 / 5 ) * 8) + 23
```

**Obs**. Observe a variável (objeto) “V3”. Há diversos parênteses,
certo? Talvez você já tenha se dado conta, mas as regras para uso de
parênteses no R em operações matemáticas é similar às da aritmética do
lápis e borracha. Ou seja, primeiro são executados os comandos internos
e depois os mais externos. A execução é “de fora para dentro”. E bônus
track: A regra vale para qualquer operação do seu script! Ou seja,
aplicação para quaisquer funções e não somente operações matemáticas.

Certo, até agora trabalhamos com vetores atômicos (*atomic vector*), que
são objetos que têm tamanho unitário (e, portanto, também assumem só uma
classe). Para os fins desta aula introdutória, vale citar os exemplos de
vetores atômicos numéricos (*numeric*), lógicos (*logical*) ou de
caracteres (*character*). Tente criar objetos destes tipos.

``` r
unifesp <- 10
unifesp <- TRUE
unifesp <- "universidade"
unifesp
```

Perceba que ao final do seu código, unifesp assumiu um valor em *string*
(character): “universidade”. Mas e os vetores numérico e lógico que você
acabou de criar? Onde foram parar?

Como o seu script é uma sequência ordenada de ordens, quando você
atribuiu novos valores nas linhas subsequentes, o objeto unifesp foi
reescrito. **Lembre-se**: O R irá processar exatamente tudo que está em
seu script, linha por linha, palavra por palavra. A única exceção é
quando uma parte do código está precedida pelo símbolo de hashtag (#).
Como vimos, trata-se de um “comentário”, que deve ser feito para
documentar as razões do que está ali naquela linha.

## Aqui ficam duas lições importantes!

(I). Você pode verificar a classe de um objeto ao repousar o cursor do
mouse sobre a variável no “Global Environment”, mas se acostume a
utilizar a função *class()*. Há diferença quando você deseja saber e
quando você precisa informar ao código para executar algum comando
somente em uma classe específica de objetos.

(II). **A linguagem é case sensitive!!!**. Um objeto chamado “B” é
diferente de um objeto chamado “b”. Noutras palavras, caso desejássemos
guardar os valores 10, TRUE e “universidade” no nosso Environment, seria
preciso nomear diferentemente. A *contrario sensu*, portanto, poderíamos
alterar somente um caractere da palavra unifesp para mantermos todos os
valores armazenados.

``` r
unifesp <- 10
Unifesp <- TRUE
uniFESP <- "universidade"

unifesp
Unifesp
uniFESP
```

Agora você terá três objetos diferentes! Em poucas palavras, unifesp é
um objeto e Unifesp é outro, uniFESP é outro ainda. Parece evidente, mas
este é um dos principais motivos de erro nos primeiros scripts que você
mandar executar.

Tente ver a classe de cada vetor atômico criado. É auto-explicativo.

``` r
class(unifesp)
class(Unifesp)
class(uniFESP)
```

## Trabalhando com *NULL*, *NA* e *NaN*

Por vezes precisamos criar um objeto vazio, que receberá informações em
alguma reiteração de comandos. É bem comum criarmos um objeto vazio, que
irá receber linhas de maneira repetida e formarão um data-frame ao
final. Veremos isso mais a frente com calma, por enquanto saibam que
existe e que é útil.

``` r
UNIFESP <- NULL
```

Note que o comando **NULL** difere dos outros dois, pois para ele não há
nenhum valor assinalado. Já para NA ou NaN pode até existir um valor
atribuído, mas este não é *“usável”*. Vejamos alguns exemplos:

``` r
y <- NULL
y > 4
#logical(0)

y <- 0/0
y
# NaN
```

Em suma, o *NA (not avaliable)* geralmente aponta para um valor faltante
*missing value*, admitindo diversas formas conforme a classe do dado,
por exemplo, NA_interger, NA_real, NA_string etc. No exemplo do código
abaixo, eu criei um objeto y, com valores atribuídos de 1 e 2. Quando
solicito para o R me retornar o terceiro elemento do conjunto, ele dará
como resposta *Not Avaliable*, já que não existe este terceiro elemento.

``` r
y <- c(1,2)
y[3]
```

Ao passo que o *NaN (Not A Number)* geralmente tem propósitos
algébricos. Assim, NaN é a resposta do R a operações inexistentes para
números reais, por exemplo, divisão de zero por zero. Já a divisão de um
número qualquer por zero, retorna o resultado de *infinito (Inf)*

``` r
a <- 1/0
a
```

## Mais um pouco sobre vetores: Conjunto

Além de vetores com um único valor, por óbvio, você poderá criar vetores
com tamanho não unitário. Ou seja, agora iremos criar um conjunto, que é
a função que permite atribuir vários valores a um objeto, sejam eles
numéricos, lógicos, caracteres …

Para isso, usamos a função *c()*

``` r
unifesp <- c(10, 100, 3.72, 500, 0, 200.10)
Unifesp <- c(TRUE, FALSE, TRUE, F, T)
uniFESP <- c("universidade", "federal", "1000")

unifesp
Unifesp
uniFESP
```

Caso você execute novamente a função class(), vai perceber que os
objetos mantiveram suas classes. Mas há alguns detalhes que merecem sua
atenção:

- Para o vetor numérico, não importa se usamos números com ou sem casas
  decimais, entretanto, o R irá usar a vírgula (comma) como separador de
  atributos e não como casa decimal. Para indicar uma casa decimal
  deverá ser utilizado o ponto. **Obs**. Este, inclusive, é uma das
  principais dificuldades na limpeza e manipulação de banco de dados. Há
  fontes com padrão em vírgulas, outros com ponto, outros ainda com
  separação regular …. Mas deixemos este problema para o momento
  oportuno.
- No caso de vetores do tipo “character”, não importa se você digitou um
  número ou letras dentro das aspas, tudo ali será considerado como
  texto.
- Para lógicos, o uso dos termos FALSE e TRUE são cambiáveis com a
  primeira letra destas palavras em caixa alta. O R vai entender o que
  você quis dizer: seja FALSE ou F, seja TRUE ou T. Mas se lembre:
  SEMPRE USE MAIÚSCULAS.

## Paramos por aqui hoje.

Amanhã continuamos com mais sobre objetos em R: Lembre-se, a linguagem
direcionada a objetos! Vamos falar de outros objetos que derivam dos
vetores atômicos, especialmente de *data-frames*. Falaremos também sobre
algunmas *funções* que são importantes recursos para o programador.
