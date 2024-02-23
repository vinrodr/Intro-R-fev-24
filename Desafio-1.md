Desafio 1
================

Você deverá exercitar o que aprendemos até aqui. Não se preocupe, não
será difícil. Apenas serve para que volte aos conteúdos e faça você
mesmo.

Vamos utilizar dados tabulares do arquivo “desafio1_data” que você deve
baixar [aqui](../Data).

**1.** Abra o arquivo e guarde em um objeto no seu *Global Environmet*

**2.** Use as funções que vimos nos últimos dias para examinar os dados
sem precisar usar View(). Tente usar as funções *head()*, *names()*,
*dim()* e *str()*. Feito isso, responda quantas observações há nos
dados? Quantas variáveis? Quais os valores assumidos por cada variável -
quais as classes das colunas?

Para o próximo exercício, quero que você se lembre da função do cifrão
(**\$**) para objetos do tipo tibble/data.frame. Usamos o cifrão após o
nome para que possamos fazer referência a uma única variável do nosso
objeto. Assim, a sintaxe seria

``` r
NOME_OBJETO$NOME_VARIAVEL
```

Também para o próximo exercício, lembre-se de que objetos do tipo
tibble/data.frame podem criar *subsets* a partir do uso de colchetes,
obedecendo à sintaxe ‘NOME_OBJETO\[LINHAS , COLUNAS\]’. Não é preciso
para o exercício proposto, mas se lembre que também podemos selecionar
um elemento de um objeto lista usando colchetes. E, neste caso, a
sintaxe seria ‘LISTA\[NUMERO_POSIÇÃO_DO_ELEMENTO_NA_LISTA\]’.

``` r
NOME_OBJETO[LINHAS , COLUNAS]

NOME_LISTA[POSICAO]
```

**3.** Usando tanto R base, quanto o dplyr.

- Crie um novo objeto em seu *working directory* que tenha somente as
  colunas ‘age’, ‘sex’, ‘education’ e ‘income’. Depois, outro objeto que
  traga somente as colunas ‘age’, ‘sex’, ‘income’, ‘savings’ e
  ‘economy’.

- Crie um novo objeto em seu *working directory*, selecionando somente
  as 10 primeiras linhas. E outro, com somente as últimas 10.

- Crie um novo objeto em seu *working directory*, criando uma variável
  nova a partir de alguma correlação entre as variáveis que já existem.
  Depois, sobrescreva esta variável realizando alguma operação
  matemática.

- Crie um novo objeto em seu *working directory*, filtrando somente as
  observações em que a variável ‘turnout’ assuma o valor “Yes”. E
  depois, crie um novo objeto em que ‘turnout’ assuma o valor “Yes”,
  ‘age’ seja inferior a 35 e ‘income’ seja superior a 2500.

- Crie um novo objeto em seu *working directory*, renomeando as
  variáveis para o idioma português. Dica: Não vimos isso no R base, mas
  faça uso do *help(recode)* e *help(replace)*.

Viu só, era simples. Parabéns, em quatro dias você já sabe por onde tem
que caminhar com o R!
