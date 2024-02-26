Desafio 1
================

Você deverá exercitar o que aprendemos até aqui. Não se preocupe, não será difícil. Apenas serve para que volte aos conteúdos e faça você mesmo.

Vamos utilizar dados tabulares do arquivo “desafio1_data” que você deve baixar [aqui](Data/desafio1_data.csv). 
- **Atenção:** Você pode usar seu teclado para fazer o download, segurando: Crtl + Shift + S
- **Atenção:** Lembre-se de verificar se o arquivo está na mesma pasta do seu *working directory*. Use *getwd()* para consultar e *setwd()* para alterar. Aos usuários de windows, lembrem-se das barras duplas invertidas.


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

**4.** Envie seu *script* (**.R**) e seu *Global Environment* (**.RData**) no email do curso: <extensao.curso.r@gmail.com>

Viu só, era simples.

Parabéns, em quatro encontros você já sabe por onde tem
que caminhar com o R!


Sugestões de solução
================

#####################################################################
###                                                               ###
###                       Código Exemplo                          ###
###                                                               ###
#####################################################################

# Carregando Biblioteca

if (!require(tidyverse)) install.packages('tidyverse')
library(tidyverse)

# Verificando meu working directory
getwd()

# Fixando meu working directory
setwd(dir = "\\Users\\vinicius.anaue\\Documents")

# Usando R base para carregar o arquivo .csv no environment
meus_dados <- read.delim(file = "desafio1_data.csv", header = TRUE, sep = ";")
# ou
meus_dados <- read.csv2(file = "desafio1_data.csv", header = TRUE)

# Usando dplyr para carregar o arquivo .csv no environment
meus_dados <- read_delim(file = "desafio1_data.csv", delim = ";")
# ou
meus_dados <- read_csv2(file = "desafio1_data.csv")

# Acessando informações do data.frame pela linha de comando
head(meus_dados)
names(meus_dados)
dim(meus_dados)
str(meus_dados)

##### 3.1 Select columns
  # R base
meus_dados1 <- meus_dados[ , 1:4]
# ou
meus_dados1 <- meus_dados[ , c("age","sex","educ","income")]
# e
meus_dados1 <- meus_dados[ , c(1,2,4,11)]
meus_dados1 <- meus_dados[ , c("age","sex","income","economy")]

  ## Dplyr
meus_dados1 <- meus_dados %>%
  select(age, sex, educ, income)
# ou
meus_dados1 <- meus_dados %>%
  select(1:4)
# e
meus_dados1 <- meus_dados %>%
  select(1,2,4,11)
# ou
meus_dados1 <- meus_dados %>%
  select(age, sex, income, economy)

 
##### 3.2. Slice rows
  # R base
meus_dados2 <- meus_dados[1:10, ]
# e
meus_dados2 <- meus_dados[21:30, ]

  # Dplyr
meus_dados2 <- meus_dados %>%
  slice_head(n = 10)
# e
meus_dados2 <- meus_dados %>%
  slice_tail(n = 10)

##### 3.3. Mutate columns
  # R base
meus_dados$income <- as.numeric(meus_dados$income) # income era character
meus_dados$nova_coluna <- (meus_dados$age * meus_dados$income)
# e
meus_dados$nova_coluna <- (meus_dados$age / meus_dados$income)
rm(meus_dados)

  # Dplyr
meus_dados <- read_delim(file = "desafio1_data.csv", delim = ";")
meus_dados <- meus_dados %>%
  mutate(nova_variavel = as.numeric(income) * age)
# e
meus_dados <- meus_dados %>%
  mutate(nova_variavel = nova_variavel / age)

##### 3.4. Filter rows
  # R base
meus_dados4 <- meus_dados[which(meus_dados$turnout == "Yes"), ]
# ou
meus_dados4 <- subset(meus_dados, turnout == "Yes")

  # Dplyr
meus_dados4 <- meus_dados %>%
  filter(turnout == "Yes")

##### 3.5.
  # R base
meus_dados5 <- meus_dados
colnames(meus_dados5) <- c("idade", "sexo", "educacao",
                           "renda", "poupanca", "casamento",
                           "filhos", "partido", "adesao",
                           "historia_voto", "economia",
                           "incumbente", "candidato")
# Ou
names(meus_dados5)[1:13] <- c("idade", "sexo", "educacao",
                             "renda", "poupanca", "casamento",
                             "filhos", "partido", "adesao",
                             "historia_voto", "economia",
                             "incumbente", "candidato")

  # Dplyr
meus_dados5 <- meus_dados %>%
  rename(idade = age,
          sexo = sex,
          educacao = educ,
          renda = income,
          poupanca = savings,
          casamento = marriage,
          filhos = kids,
          partido = party,
          adesao = turnout,
          historia_voto = vote_history,
          economia = economy,
          incumbente = incumbent,
          candidato = candidate)
	

