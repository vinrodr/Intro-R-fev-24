Tutorial 3
================

# Tutorial 3

## Antes de avançar, um passo atrás

Vamos retomar de onde paramos e aproveitar para relembrar. Tínhamos
visto por cima o que seriam variáveis (colunas do date-frame e objetos)
e vetores (objetos) para o R, mas vamos melhorar isso um pouco.

O vetor é um termo polissêmico na linguagem R. Admintindo 3
significados:

- vetor atômico.
- objeto sem atributos.
- objeto que tem comprimento.

Assim, quando nos referirmos ao atomic vector estamos falando do
primeiro significado, mas abreviamos como vector para não ficar
enfadonho. Já para distinguir uma estrutura linear de uma matriz, também
falamos que se trata de um vector (ou seja, uma matriz de uma única
linha). Por fim, é o sentido literal da palavra que se aplica a todos
objetos: o que inclui listas, mas que se exclui do primeiro significado.
Em suma, com o tempo você se acostuma.

Certo, mas vamos relembrar isso: Um vetor atômico ( *atomic vector*) é o
tipo mais simples de dados com o qual você pode trabalhar no R. Conforme
aumentamos a dimensão (dim) do vetor, podemos incluir a mesma classe de
dados ou classes distintas.

``` r
x <- c(1,2,3,4)
x <- c(1, "dois", 3, TRUE)
```

Pois bem, vejamos então quais são os quatro principais tipos de
variáveis com os quais você deve estar familiarizado: **Obs.** Você pode
verificar a classe do objeto que está no seu environment de três formas.
Primeiro, há uma abreviatura da classe do objeto quando você repousar o
cursor do mouse sobre o objeto no Global Environment. A segunda maneira
é usando a função *str()*; e, por fim, usando *class()*.

• **Numérico** (*numeric*): Você deve estar familiarizado com a classe
dos numéricos (*numeric*), que é... bem, qualquer número. O R ainda
subclassifica os numéricos duplos (*doubles*) ou simples (*interger*),
que dizem respeito apenas a maneira pela qual o R irá armazenar e
representar estes números. Veja: um numérico pode incluir os decimais
(*double*); ou somente guardar a informar sem o fracionário
(*interger*). **Obs.** Note que há um falso cognato aqui! O número
inteiro no português é aquele número que admite fracionamento, enquanto
são os naturais são os que não admitem decimais.

• **Caractere** (*character*): são objetos que armazenam dados
alfanuméricos no formato de texto (*string*).

• **Lógico** (*logical*): são objetos que assumem valores de VERDADEIRO
ou FALSO. Da mesma maneira como um vetor da classe *character* assume
valores em texto (*string*), você pode entender que um vetor lógico
assume valores boleanos (*bolean*) de verdadeiro ou falso.

• **Fatores** (*factor*): Aqui você precisa abstrair novamente. Pense
nessa classe de objetos como uma variável categórica ordenada. Se você
não se lembra do que é isso, saiba que toda informação não numérica que
você pode ordenar é descrita como um factor ex. primeiro, segundo,
terceiro; ou, excelente, regular, péssimo. Assim, grosso modo, a classe
de objetos em R que lida com dados categóricos, sejam nominais ou
ordinais, são os *factors*.

Vamos tentar um exemplo para fixar melhor.

Imagine que você tem um vetor de texto que representa uma variável
categórica que pode receber valores “yes” e “no”.

``` r
resposta <- c("yes", "no", "no", "no", "yes", "no")
print(resposta)
class(resposta)
```

Vamos, então, usar a função factor() para ver o resultado:

``` r
resposta_f <- factor(resposta)
print(resposta_f)
```

**Perceba** que não há mais aspas nos valores “yes” e “no”. **Além
disso**, há uma nova informação: *levels* (níveis).

Com isso, você já pode perceber o porquê *factors* são vetores numéricos
cujos valores são associados a um rótulo (nível/level). Há um par de
informações nesta classe de dados, que é o numérico + rótulo.

Voltando à ideia de variável ordenada, cada ordem será chamada de
*level* pelo R. Agora, talvez você se pergunte o porquê de não serem
chamados de categorias, então?

Veja que tanto os *character*, quanto os *factor* admitem entradas em
texto (*string*), **o que difere um do outro** é que não há ordenação na
classe *character*. Evidentemente que é o R não difere aprioristicamente
um de outro, portanto, caso você crie uma variável categórica ordinal (
*factor*), mas não diga ao R para interpretá-la desta forma, mesmo que
esteja c(“primeiro”, “segundo”, “terceiro”), sua variável estará
marcando como *character*. E para transformar uma variável em outra,
basta você informar ao R com os comandos:

Além disso, se tentarmos transformar um vetor factor em um vetor
numérico, teremos um **grande problema**. Veja só:

```r
resposta_f <- as.numeric(resposta_f)
```

As saídas 1 e 2 que apareceram são os códigos automaticamente gerados
pelo R para “yes” e “no”. O **critério** para atribuir os valores foi a
**ordem alfabética** do texto que transformamos em fatores.

Agora, caso queiramos descobrir os níveis (levels) de um vetor de
fatores, usamos a função *levels()*:

``` r
levels(resposta_f)
```

Por serem informações do rótulo, também podemos alterar os nomes dos
níveis da mesma maneira que fazemos com os nomes dos elementos de um
vetor:

``` r
levels(resposta_f) <- c("SIM", "no")
print(resposta_f)
```

Voltando à criação da variável ordenada com os níveis “primeiro”,
“segundo”, “terceiro”. Lembre-se que falamos que o R não reconhece esta
informação como factor, salvo se você dizer para ele. Mas se lembre,
também, que a ordenação é dada por default por ordem alfabética!

Então, para que o vetor de fatores c(“primeiro”, “segundo”, “terceiro”)
mantivesse esta ordem, é preciso indicarmos ao R qual ordem é essa! De
novo: O default é a ordenação nominal!!!

Vejamos um exemplo:

``` r
altura <- c("baixo", "medio", "medio", "baixo", "alto", "baixo", "alto")
altura_f <- factor(altura)
print(altura_f)
```

O que aconteceu? Dado o default de ordenamento alfabético, o número 1
ficou associado ao rótulo “alto”, o número 2 a “baixo” e o 3 a “medio”.
Assim, para corrigir isso e evitar equívocos na análise, temos que
informar alguns parâmetros adicionais ao criar um factor!

- Order
- Levels

Veja o exemplo abaixo:

``` r
altura_f <- factor(altura, ordered = T, levels <- c("baixo", "medio", "alto"))
altura_f
```

A informação dos níveis (levels) agora está em consonância com a ideia
ordenada de baixo, medio e alto. As comparações que fazem uso de
operadores lógicos entre os níveis agora fazem sentido!

Falamos bastante de *factors* por que é uma classe de vetores em R que
costuma gerar erros no código, que por vezes não são percebidos até a
revisão por um terceiro. Imagine você classificar nominalmente um vetor
e inverter os resultados que buscava? Fique atento a isso, pois é um
elemento costumeiro de erro.

**Para reforçar: Diversas vezes, quando importamos bases de dados (data
frames) para nosso global environment, o R considera variáveis character
como factors.** Para evitarmos este problema, usamos o argumento
***stringAsFactors = F*** em diferentes funções de importação. Tudo isso
será revisitado nos próximos encontros, quando aprenderemos a importar
dados, mas fique aqui a advertência de que factors, ao lado de missing
values e enconding são os pontos de maior confusão em R.

### Para Fixação

- Crie seu vetor de texto com elementos não ordenáveis.
- Crie agora um objeto de fatores a partir do anterior e ordene conforme
  queira.
- Agora, crie um objeto texto com níveis ordenáveis.
- E a partir dele, um vetor de fatores.
- Usando operadores lógicos, compare dois elementos de um dos vetores
  que você criou.

## Objetos derivados: Listas

As listas são objetos formados por conjuntos de valores de tipos
diferentes. É um caso específico de conjunto e é bem útil para raspagem
de páginas web e iteração em funções.

``` r
i <- c(8192, "Universidade")
curso <- c(10, "UNIFESP", TRUE, i)
```

É importante notar que a lista aceita todo tipo de objetos, tanto
valores atômicos, quanto outras listas/conjuntos/outros objetos.

Além disso, a lista é um conjunto ordenado de valores. Assim, como no
conjunto, cada valor assume uma posição na lista e é a partir desta
informação que podemos utilizar/controlar a lista. A ação utilizada para
isso é chamada de ***subscripting*** e é realizada selecionando a
posição do valor na lista entre parênteses. Veja o exemplo abaixo:

``` r
curso[1]
nota <- curso[1]
```

Primeiro eu coloquei um comando para que o valor na primeira posição da
lista fosse mostrado. E o resultado foi o numeral 10. Na segunda linha,
além de ordenar esta ação, eu guardei o resultado no objeto nota que eu
criei pelo ***assignment***. É importante perceber isso: caso você não
crie um objeto para guardar alguma informação, o R só irá executar a
tarefa e mostrar seu resultado.

Veremos mais abaixo a ideia de subconjunto, que faz uso da técnica desta
técnica de ***subscripting***.

Já o caminho inverso ao *subscripting* é a ***indexação***, que ocorre
quando eu atribuo um valor a uma posição de um objeto, por exemplo,
quando eu atribuo que a posição \[1,2\] da matriz será 300.

``` r
a <- matrix(1:15, 5)
a

a[1,2] <- 300
a
```

## Objetos derivados: Matriz

Durante nossos encontros, iremos nos focar nos dados em formato de data
frames, que é um caso específico de matriz. Por esta razão, só iremos
pontuar a existência de matrizes e alguns pontos que facilitam o
aprendizado dos data frames.

Matrizes (*matrix*) são objetos com dados dispostos de maneira
retangular. Lembre-se que para a matemática, matrizes são objetos de
álgebra própria e que as operações matemáticas neste campo seguem as
determinações da álgebra linear.

Assim, matrizes são objetos (*vector*) que apresentam em seu argumento
as suas dimensões (largura e altura). A dimensão (*length*) da matriz é
o número de linhas pelo número de colunas. Para preenchermos os valores
de cada elemento da matriz, podemos adotar dois procedimentos: Ou por
meio de indicação das linhas (“byrow = T”), ou por meio das colunas
(“byrow = F”). Veja o exemplo abaixo e tente compreender o
funcionamento:

``` r
matrix(1:15, byrow = T, 5)
```

    ##      [,1] [,2] [,3]
    ## [1,]    1    2    3
    ## [2,]    4    5    6
    ## [3,]    7    8    9
    ## [4,]   10   11   12
    ## [5,]   13   14   15

``` r
matrix(1:15, byrow = F, 5)
```

    ##      [,1] [,2] [,3]
    ## [1,]    1    6   11
    ## [2,]    2    7   12
    ## [3,]    3    8   13
    ## [4,]    4    9   14
    ## [5,]    5   10   15

Agora, vamos criar um vetor de matriz a partir de três vetores. Abaixo
temos as notas das cinco disciplinas semestrais de estudantes da
unifesp.

``` r
dandara <- c(10, 7, 8, 9, 10)
lamarca <- c(2, 6, 7, 6, 5)
olga <- c(9, 8, 4, 8, 9)
```

Iremos juntar todos os indivíduos em um só vetor.

``` r
vetor_discentes <- c(dandara, lamarca, olga)
```

E, depois, criar um vetor matriz com 5 linhas e 3 colunas, denominando
turma:

``` r
turma <- matrix(vetor_discentes, byrow = FALSE, nrow = 5)
turma
```

    ##      [,1] [,2] [,3]
    ## [1,]   10    2    9
    ## [2,]    7    6    8
    ## [3,]    8    7    4
    ## [4,]    9    6    8
    ## [5,]   10    5    9

Note que as colunas (variáveis) não têm nomes. Aqui utilizamos as
funções **rownames()** e **colnames()** para dar nome às observações e
às variáveis, respectivamente.

## Uma observação antes de prosseguir

Caso tivéssemos um vetor de dimensão unitária ao invés de uma matriz,
usaríamos a função **names()**. Vejamos com o exemplo abaixo.

Teremos gastos diários armazenados nos objetos (*vector*)
*gastos_semana* e *gastos_semana2*. Além disso, vamos criar um vetor com
os nomes dos dias da semana.

``` r
gastos_semana <- c(34, 20, 15, 25, 16, 18, 30)
gastos_semana2 <- c(28, 32, 10, 15, 30, 26, 28)
dias_semana <- c("segunda", "terça", "quarta", "quinta", "sexta", "sábado", "domingo")
```

Agora, usamos a função *names()*. Vejamos:

``` r
names(gastos_semana) <- dias_semana 
names(gastos_semana2) <- dias_semana
```

Você pode ter se perguntado, e se eu criasse uma tabela (data.frame)?

``` r
df <- rbind(dias_semana, gastos_semana, gastos_semana2)
df

rm(df)
```

Mas, neste caso, teríamos um data.frame com células organizadas, mas os
nomes das variáveis seriam “V1”, “V2” …“V7” - que são default.

Então, se quisermos um data.frame com variáveis nomeadas, usamos a
função names() para nomear cada item do dos vetores gastos_semana e
gastos_semana2, posteriormente unimos os vetores com a função rbind()
(rool bind, na tradução livre junção de linhas).

\*\*Obs.(!) Você pode usar a função names() para verificar os nomes
dados a cada variável do data.frame ou do item (no caso de um vetor de
dimensão única). Veja abaixo a diferença:

``` r
names(gastos_semana)
gastos_semana

names(gastos_semana) <- c("V1", "V2", "V3", "V4", "V5", "V6", "V7")
gastos_semana
```

Você terá problemas com a função rbind() caso deseje unir vetores de
dimensões diferentes. Veja, um data.frame é um banco de dados com
largura e altura fixas. Além disso, a função rbind coloca os vetores um
sobre o outro, na ordem em que colocamos os objetos nos atributos da
função. Ou seja, rbind(gastos_semana2, gastos_semana) fará um data.frame
diferente de rbind(gastos_semana, gastos_semana2).

## Voltando às Matrizes

Estávamos nomeando as observações e variáveis da matriz com as funções
rownames() e colnames(). Mas como no caso dos vetores, temos que criar
um vetor com os nomes que serão atribuídos. Veja abaixo:

``` r
disciplinas <- c("Matemática", "História", "Geografia", "Português", "Física") 
discentes <- c("dandara", "lamarca", "olga")

rownames(turma) <- disciplinas
colnames(turma) <- discentes
turma
```

    ##            dandara lamarca olga
    ## Matemática      10       2    9
    ## História         7       6    8
    ## Geografia        8       7    4
    ## Português        9       6    8
    ## Física          10       5    9

Há ainda a possibilidade de nomear as observações e variáveis no momento
em que criamos a Matriz. Para isso, a função matrix() tem o atributo
*dimnames*. Veja abaixo:

``` r
turma <- matrix(vetor_discentes, byrow = F, nrow = 5, dimnames = list(disciplinas, discentes))
turma
```

    ##            dandara lamarca olga
    ## Matemática      10       2    9
    ## História         7       6    8
    ## Geografia        8       7    4
    ## Português        9       6    8
    ## Física          10       5    9

Menos linhas de código, não é mesmo? Mas conhecer as diferentes funções
permitem a você editar seus objetos e cria repertório nas soluções de
programação que irá possuir. Lembre-se: Normalmente há mais de um modo
de fazer algo.

E se você inverter linhas e colunas? O que aconteceria? Bom, o R
informaria um erro, pois o vetor disciplinas é maior que o número de
colunas. O mesmo vale para o caso das linhas, em que o número de
discentes passa a ser inferior.

> Error in dimnames(x) \<- dn: comprimento de ‘dimnames’ \[1\] não é
> igual ao tamanho do array

Outras funções interessantes para trabalhar com matrizes são *rowSums* e
*colSums*. Os nomes das funções são autoexplicativas.

``` r
rowSums(turma)

colSums(turma)
```

Parecia bobagem, certo? Mas combinando as funções… temos as margens da
tabela criada. Vejamos:

``` r
total_col_turma <- colSums(turma)
turma2 <- rbind(turma, total_col_turma)

total_lin_turma <- rowSums(turma2)
turma2 <- cbind(turma2, total_lin_turma)
print(turma2)
```

Já estamos encerrando este tutorial. Mas vamos ao que mais importa
agora: a **criação de subconjuntos de matrizes**.

Lembre-mos que usamos colchetes \[\] para produzirmos subconjuntos dos
vetores (conjuntos).

``` r
vetor_unitário <- c(3,10,"meu texto", TRUE)
subconjunto_vetor_unitário <- vetor_unitário[3]

subconjunto_vetor_unitário
```

A boa notícia que o mesmo se aplica para as matrizes. A diferença é que
agora os colchetes devem trazer as informações de coluna e linha. Quase
como naquele jogo de batalha naval! Para matrizes (e, portanto, também
para os data frames) para extrairmos um subconjunto precisamos primeiro
a linha e depois a coluna, separadas por uma vírgula. Veja você:

``` r
notas_história <- turma[2, ] #selecionar somente as notas da disciplina de História, não indico a coluna
notas_dandara <- turma[ ,1] #selecionar somente as notas de dandara
nota_mat_olga <- turma[1,3] #selecionar a nota de matemática de olga

notas_mat_hist <- turma[1:2,3] #selecionar notas de matemática e história da olga
```

O símbolo de dois pontos indica um intervalo. Na última linha do
exemplo, vocês selecionaram da linha 1 até a linha 2, além de restringir
à coluna 3 (olga). Mas e se quisesse selecionar as notas de matemática e
geografia, mas não de história? Ai usaríamos a função *combine* “c()”,
veja só:

``` r
turma[c(1,3,5), 3]
```

Perceba que a função *combine* está no lugar onde devemos indicar as
linhas que desejamos selecionar. Caso quiséssemos selecionar dandara e
olga, neste caso, a função *combine* deve ficar após a vírgula.

Ao invés de indicar a posição dos elementos na matriz, podemos ainda
trazer o próprio valor do elemento. Veja o exemplo abaixo:

``` r
turma[ ,c("dandara", "olga")]
```

Para os exemplos dados, parecem ser extremamente trabalhosos para um
resultado ruim. Mas pense por um minuto em outro exemplo. Imagine que
você deseja aferir o gasto de campanha de TODOS os **candidatos** nas
últimas eleições (deputados estaduais, deputados federais, governadores,
senadores e presidentes). Talvez seja uma centena de milhar de
observações! É neste particular que o R te traz escalabilidade e
velocidade para suas análises. Poderíamos criar um subconjunto com os
candidatos acima ou abaixo de determinado valor.

### Para fixação

Crie um subconjunto diferente da matriz “turma” com a qual trabalhamos.

Ok. Acho que já está pegando o jeito. Agora, imagine se você quisesse
criar um subconjunto a partir de uma claúsula condicional? Por exemplo,
selecionar o subconjunto de notas superiores à média de aprovação? Neste
caso, não precisaríamos olhar item por item para filtrar indicando sua
posição na matriz.

Para isso, usamos os operadores lógicos!!! Iremos falar deles no próximo
tutorial. Por agora, basta encerrar falando um pouco sobre data frames.

## Objetos derivados: Data-frame

A grande capacidade analítica está em realizar cálculos no interior de
um banco de dados correlacionado, procurando causalidades, tendências e
fazendo previsões. Para isso, devemos criar variáveis e montar um
data.frame.

Um data-frame é também um objeto com dados dispostos de maneira
retangular, mas diferentemente da matriz, pode apresentar valores de
classes diferentes em suas colunas. Por óbvio, a matriz só admite uma
classe de atomic vectors. Iremos ver como trabalhar com data-frames em
breve, por enquanto basta esta definição.

## Paramos por aqui.

Você provavelmente conseguiu fixar melhor o conteúdo que foi colocado
anteriormente. Então, paramos por aqui.
