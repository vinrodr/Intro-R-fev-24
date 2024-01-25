Tutorial 3
================

Antes de avançar, um passo atrás
---
Vamos retomar de onde paramos e aproveitar para relembrar. Tínhamos
visto por cima o que seriam variáveis (colunas do date-frame e objetos)
e vetores (objetos) para o R, mas vamos melhorar isso um pouco.

O vetor é um termo polissêmico na linguagem R. Admintindo 3
significados: 
* vetor atômico.
* objeto sem atributos.
* objeto que tem comprimento.

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
variáveis com os quais você deve estar familiarizado:

• **Numérico** ( *numeric*): Você deve estar familiarizado com a classe
dos numéricos ( *numeric*), que é… bem, qualquer número. O R ainda
subclassifica os numéricos duplos ( *doubles*) ou simples ( *interger*),
que dizem respeito apenas a maneira pela qual o R irá armazenar e
representar estes números. Veja: um numérico pode incluir os decimais (
*double*); ou somente guardar a informar sem o fracionário (
*interger*). **Obs.** Note que há um falso cognato aqui! O número
inteiro no português é aquele número que admite fracionamento, enquanto
são os naturais que não admitem decimais.

• **Caractere** ( *character*): são objetos que armazenam dados
alfanuméricos no formato de texto ( *string*).

• **Lógico** ( *logical*): são objetos que assumem valores de VERDADEIRO
ou FALSO. Da mesma maneira como um vetor da classe *character* assume
valores em texto ( *string*), você pode entender que um vetor lógico
assume valores boleanos ( *bolean*) de verdadeiro ou falso.

• **Fatores** ( *factor*): Aqui você precisa abstrair novamente. Pense
nessa classe de objetos como uma variável categórica ordenada. Se você
não se lembra do que é isso, saiba que toda informação não numérica que
você pode ordenar é descrita como um factor ex. primeiro, segundo,
terceiro; ou, excelente, regular, péssimo. Cada ordem desta ordenação
será chamada de *level* pelo R. Talvez você se pergunte o porquê de não
serem chamados de categorias, então? A história é longa, mas basta
saberem da existência destas duas classes, pois, por vezes, a diferença
não importa. **Obs.** Veja que tanto os *character*, quanto os *factor*
admitem entradas em texto ( *string*), o que difere um do outro é que
não há ordenação na classe *character*. Evidentemente que é o R não
difere aprioristicamente um de outro, portanto, caso você crie uma
variável categórica ordinal ( *factor*), mas não diga ao R para
interpretá-la desta forma, mesmo que esteja c(“primeiro”, “segundo”,
“terceiro”), sua variável estará marcando como *character*. E para
transformar uma variável em outra, basta você informar ao R com os
comandos:

``` r
x <- c("primeiro", "segundo", "terceiro")
x <- as.factor(x)
```

**Obs.2** Você pode verificar a classe do objeto que está no seu
environment de três formas. Primeiro, há uma abreviatura da classe do
objeto quando você repousar o cursor do mouse sobre o objeto no Global
Environment. A segunda maneira é usando a função *str()*; e, por fim,
usando *class()*.

Objetos derivados: Listas
---
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
isso é chamada de **_subscripting_** e é realizada selecionando a posição do
valor na lista entre parênteses. Veja o exemplo abaixo:

``` r
curso[1]
nota <- curso[1]
```

Primeiro eu coloquei um comando para que o valor na primeira posição da lista fosse
mostrado. E o resultado foi o numeral 10. 

Na segunda linha, além de ordenar esta ação, eu guardei o resultado no objeto
nota que eu criei pelo **_assignment_**. 

**É importante perceber isso**: caso você não crie um objeto para guardar alguma 
informação, o R só irá executar a tarefa e mostrar seu resultado.

O caminho inverso ao *subscripting* é a **_indexação_**, que ocorre quando
eu atribuo um valor a uma posição de um objeto, por exemplo, quando eu
atribuo que a posição \[1,2\] da matriz valerá 300.

## Objetos derivados: Matriz

Uma matriz ( *matrix*) são objetos com dados dispostos de maneira
retangular. São estudadas na matemática amplamente por meio da algebra
linear, principalmente. Assim, matrizes são objetos (_vector_) que
apresentam em seu argumento as suas dimensões (largura e altura). A
dimensão (*length*) da matriz é o número de linhas pelo número de colunas.
Um exemplo de matriz é dado abaixo:

``` r
matrix(1:15, 5)
```

    ##      [,1] [,2] [,3]
    ## [1,]    1    6   11
    ## [2,]    2    7   12
    ## [3,]    3    8   13
    ## [4,]    4    9   14
    ## [5,]    5   10   15

Objetos derivados: Data-frame
---
Um data-frame é também um objeto com dados dispostos de maneira
retangular, mas diferentemente da matriz, pode apresentar valores de
classes diferentes em suas colunas. Por óbvio, a matriz só admite uma
classe de atomic vectors. Iremos ver como trabalhar com data-frames em
breve, por enquanto basta esta definição.

Funções também são objetos: Help (I)
---
O comando mais utilizado no R é a função help. Não se engane achando que
ela só vale para iniciantes! A quantidade de comandos e pacotes é tão
grande que se torna impraticável decorar tudo em seus detalhes. Lembre
de que existem milhares de pacotes e você mesma(o) poderá fazer um no
futuro.

Assim, qualquer objeto do R pode ter seu Vignettes (breve sumário)
aberto no painel de output pelo comando *help()* ou inserindo uma
interrogação antes daquilo que deseja conhecer, ex. ?srqt()

Funções também são objetos (II)
---
O R em sua forma mais básica pode ser uma calculadora, vamos relembrar
os operadores matemáticos:

|    Operadores     | Símbolos |  Exemplos   |
|:-----------------:|:--------:|:-----------:|
|      Adição       |    \+    |  5 + 3 = 8  |
|     Subtração     |    \-    |  5 - 2 = 3  |
|   Multiplicação   |    \*    | 2 \* 3 = 6  |
|      Divisão      |    /     | 10 / 5 = 2  |
|   Exponenciação   |    ^     |  2 ^ 3 = 8  |
| Divisão SEM resto |    %%    | 17 %% 3 = 5 |

    * Divisão sem resto: Caso você deseje obter somente o valor de uma divisão desconsiderando os valores decimais, basta usar os símbolos.

Na programação funcional, fazemos maior uso dos **Operadores lógicos**.
São extremamente úteis para aritmética e outras hipóteses, sempre
retornando um boleano ( *bolean*) TRUE ou FALSE.

|     Operadores      | Símbolos |
|:-------------------:|:--------:|
| estritamente maior  |    \>    |
|    maior e igual    |   \>=    |
| estritamente menor  |    \<    |
|    menor e igual    |   \<=    |
| exatamente igual a  |    ==    |
|    diferente de     |    !=    |
|       não é x       |    !x    |
|       x OU y        |  x \| y  |
|        x E y        |  x & y   |
| x está contido em y | x %in% y |

O operador lógico de contido em é extramente útil. Ele permite que você
verifique se alguma variável apresenta determinado valor em suas
observações.

``` r
 8 %in% c(2,3,4,5)
```

Funções também são objetos: Visualizar e Apagar objetos (III)
---
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

Errors and Warnings
---
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
