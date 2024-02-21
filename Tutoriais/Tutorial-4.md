Tutorial 4
================

## Relembrando

Você já viu que qualquer operação ou transformação em R ocorre por meio
de um comando, ou seja, por meio de uma função. Também já viu que
qualquer a estrutura básica das funções, qual seja,
**“aqui_uma_funcao(aqui_seus_atributos/insumos)”**.

Agora, como há alguns milhares de pacotes em R, as vezes que se propõem
a fazer a mesma coisa de modo diferente, ou mesmo atualizam e
aperfeiçoam, pequenas variações no nome são comuns. P.ex: col_names,
colnames e col.names. E isso é relevante, pois cada função DEVE ter um
nome único e você já sabe que há as *reserved words*. Entretanto,
existem sim funções de mesmo nome! O R gera um warning (*conflicts*) no
seu sistema quando percebe que instalou pacotes com funções de mesmo
nome.

> ── Conflicts ─────────────────────────────────── tidyverse_conflicts()
> ──
>
> ✖ dplyr::filter() masks plotly::filter(), stats::filter()
>
> ✖ dplyr::lag() masks stats::lag()

Caso estejamos usando dois ou mais pacotes que possuam funções de mesmo
nome, a solução é anteceder o nome da função do nome do pacote seguido
do símbolo de dois pontos repetido uma vez. Veja:

> dplyr::filter()

Ok, precisamos lembrar também que cada função aceita insumo(s) (*input*)
e gera um ou mais produtos produto (*output*). E, ainda que a função não
exija nenhum *input*, sua estrutura básica exige seu comando ser seguido
de parênteses. Por exemplo, a função Sys.Date(), que retorna a data de
hoje.

``` r
Sys.Date()
```

## Funções também são objetos: Help

O comando mais utilizado no R é a função help. Não se engane achando que
ela só vale para iniciantes! A quantidade de comandos e pacotes é tão
grande que se torna impraticável decorar tudo em seus detalhes. Lembre
de que existem milhares de pacotes e você mesma(o) poderá fazer um no
futuro.

Assim, qualquer objeto do R pode ter seu *Vignettes* (breve sumário)
aberto no painel de output pelo comando **help()** ou inserindo uma
interrogação antes daquilo que deseja conhecer, ex. ?srqt()

## Operadores matemáticos e operadores lógicos

O R em sua forma mais básica pode ser uma calculadora, vamos relembrar
os operadores matemáticos:

|    Operadores     | Símbolos |  Exemplos   |
|:-----------------:|:--------:|:-----------:|
|      Adição       |    \+    |  5 + 3 = 8  |
|     Subtração     |    \-    |  5 - 2 = 3  |
|   Multiplicação   |    \*    | 2 \* 3 = 6  |
|      Divisão      |    /     | 10 / 5 = 2  |
|   Exponenciação   |    ^     |  2 ^ 3 = 8  |
| Divisão SEM resto |    %/%   | 17 %% 3 = 5 |
| RESTO da divisão  |    %%    | 17 %% 3 = 2 |

    * Divisão sem resto: Caso você deseje obter somente o valor de uma divisão desconsiderando os valores decimais, basta usar os símbolos.

Na programação funcional, fazemos maior uso dos **Operadores relacionais
e lógicos**. São extremamente úteis para aritmética e outras hipóteses,
sempre retornando um boleano (*bolean*) TRUE ou FALSE. Uma das melhores
capacidade de processamento é verificar se uma proposição é falsa ou
verdadeira. **Operadores relacionais e lógicos** funcionam para aferir
se objetos são iguais, diferentes, maiores ou menores; agrupando,
incluindo/excluindo ou alternando entre elementos. Vejamos os símbolos
na tabela abaixo:

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
|         Não         |    !     |

**Obs.** O operador lógico de contido (%in%) em é extramente útil. Ele
permite que você verifique se alguma variável apresenta determinado
valor em suas observações.

``` r
 8 %in% c(2,3,4,5)
```

## Vamos praticar um pouco

Copie uma linha de cada vez e execute no seu console. Veja os
resultados.

``` r
# Execute um grupo de comandos de cada vez e veja o resultado.
# Note que há diferença entre executar um comando e guardar seu resultado como um objeto no Global Environment
45 - 13
13 * 3
10 ^ 10
17 %% 3
a <- 45 - 13
b <- 13 * 3
c <- 10 ^ 10
d <- 17 %% 3
f <- a + b - c
pi <- 3.14
escrito <- "meu texto"
verd <- TRUE

# Confira a classe dos objetos que acabou de criar
class(pi)
class(escrito)
class(a)
class(f)
class(verd)

# Operações com vetores e objetos
vetor_numeric <- c(a, c, f, pi, 300, 200, 450.2, 100)
vetor_numeric
class(vetor_numeric)

vetor_string <- c(escrito, "meu texto", )
vetor_string
class(vetor_string)

vetor_logico <- c(T, F, T, F, F)
vetor_logico
class(vetor_logico)

lista_diversa <- c(vetor_logico, vetor_numeric, 200, "vermelho", "dois", 2, "2")
class(lista_diversa)

k <- a > b
class(k)

a == 32
a != 32
isTRUE(a != 32)

# O operador relacional é distinto do operador matemático/símbolo de atribuição

1 = 1
1 == 1

# Podemos usar objetos e números nos cálculos

temp_celsius <- c(-7, -10, 5, 12, 21)
farenheit <- ((temp_celsius / 5) * 9) + 32
farenheit

# Operadores relacionais também vale para textos

"meu texto" == "meu texto"
"meu texto" = "meu texto"
"meu texto" == "Meu texto"
"meu texto" != "Meu texto"

# Objetos string também podem ser ordenados. Lembre-se que os factors são ordenados alfabeticamente por default.

"a" > "b"
"a" < "b"
"A" < "b"
"A" > "a"

# O mesmo vale para palavras ou frases!

"Olga" < "Olga Benário Prestes"
"cores frias" > "cores quentes"

# E os valores boleanos? Dica: Lembre-se do binário.

TRUE == 1
FALSE == 0
TRUE > FALSE 

# Comparar objetos a partir dos valores que armazenam

a <- 4
b <- 3
a > b

# Operadores relacionais e vetores

gastos2024 <- c(1020, 800, 990, 345, 203, 3035)
gastos2024 >= 500

# A comparação entre dois vetores

gastos2023 <- c(1000,900,897,458,200,2200)
gastos2023 > gastos2024

# Obs. Os elementos são comparados par a par de acordo com sua posição no vetor. E o vetor resultante tem o mesmo tamanho!

# Operadores relacionais + Lógicos (Booleanos)
# Embora a primeira condição permitisse que o último elemento 2200 fosse TRUE, quando coloco o operador lógico E (&) para uma nova condição: ser diferente de 2200, todos os elementos retornam como FALSE.

gastos2023 > 1000 & gastos2023 !=2200

# O operador lógico "não" reverte uma proposição. 

!TRUE
!(4 > 2)
!(gastos2023 > 1000 & gastos2023 <= 300)
```

## Paramos por aqui
