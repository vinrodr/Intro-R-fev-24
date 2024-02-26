Tutorial 7
================

# Organizando seus dados

Hoje vamos ver um pouco mais das ferramentas que o *tidyverse* nos
concede para trabalhar com *data frames*. Se no encontro passado vimos
funções/comandos para manipular ora colunas, ora linhas; agora veremos
como podemos organizar nossos dados, quando precisamos mexer nas
informações das células. Vamos aproveitar este encontro também para
aprender como produzir estatísticas resumidas de nossos dados com poucos
comandos. Para isso, o Tutorial 7 vai ensinar como unir/separar
variáveis, identificar valores repetidos, completar dados faltantes e
recodificar variáveis.

## Dividindo variáveis (*separate*)

É bem comum que você precise separar alguma informação que está unida em
uma única variável. Por exemplo, imagine que a variável data esteja
codificada como “fevereiro_2023”, mas você precisa de uma variável mês e
outra ano. Como faria, neste caso?

**DICA:** Saiba que é um princípio da análise e manipulação de dados que
cada informação merece ser individualizada. Dito de outra forma, prefira
organizar seus dados com cada variável de interesse dentro de uma coluna
diferente - no nosso exemplo, uma coluna mês e outra ano.

Para separar as informações presentes de uma coluna em duas, usaremos a
função *separate()* do *tidyr* (outro pacote do *tidyverse*), que
permite que usemos tanto a posição de um caractere, quanto seu próprio
símbolo como critério de divisão. Não entendeu, né?

``` r
# Carregando biblioteca
library(tidyverse)

# Criando uma tabela 
meus_dados <- tibble(ID = 1:3,
                      mes_ano = c("abr2005","jan2010","nov2015")) 
```

Imagine que num primeiro caso você tem as três primeiras letras do nome
do mês seguido pelo ano (jan_2023, fev_2023, mar_2023 …). Neste caso,
você poderia indicar dentro do parâmetro da função *separate()* que a
divisão deveria ocorrer a partir do 4 caractere, certo? Mas imagine um
segundo caso, em que o nome dos meses estivesse completo (janeiro_2023,
fevereiro_2023, marco_2023 … ). Para este, já não funcionaria indicar a
posição do caractere (que muda conforme a observação), sendo que
deveríamos usar outro critério. Por isso, o *separate()* também aceita
que você indique o próprio caractere “\_“.

A sintaxe desta função pede os argumentos: (I) *col* = nome da variável
que desejamos dividir; (II)*into* = os nomes que você dará para as duas
novas colunas. Mas atenção aqui: como você irá criar duas novas colunas,
precisa usar a função *c()* para isso; e (III) *sep* = qual a
posição/caractere que usamos como separador - a divisão se dará
**depois** desta posição/caractere. (IV) Você pode ou não excluir a
coluna original, para excluir deve colocar o atributo *remove* = TRUE.
**Obs.** Há outros atributos, veja com *help()*.

``` r
# Separando informações em duas variáveis
meus_dados <- meus_dados %>% 
  separate(mes_ano, c("mes","ano"), 3) # Após o terceiro caractere
```

Você percebeu que não precisei colocar o nome dos atributos da função
para que o R compreendesse. Bastou que deixasse as informações na
posição *default* esperada pela estrutura original da função. Com o
tempo você se habituará, mas no começo, use os nomes dos
parâmetros/atributos no interior dos parênteses.

Certo, agora veja o exemplo que pede ao R para buscar o caractere
específico para fazer a separação.

``` r
# Criando uma nova tabela

meus_dados2 <- tibble(ID = 1:3,
                      mes_ano = c("setembro_2001", "dezembro_2002", "julho_2013"))

# Separando informações em duas variáveis

meus_dados2 %>% separate(mes_ano, c("mes","ano"), "_") # Usando o underline como referência

meus_dados2
```

Ué?! Por que não funcionou? Será que erramos no código? Lembre-se que ao
dar o comando para separar as informações, você não pediu que o R
armazenasse o resultado em lugar nenhum. Então, o resultado está somente
no seu console e não no seu *global environment*. Caso quisesse
sobrescrever, deveria ter usado a seta de *assingment*, certo? De igual
forma, caso desejasse criar um novo objeto.

Certo, agora fica simples falar da função que executa a operação
inversa: *unite()*. Mas fica a advertência dada anteriormente, isso
acaba sendo bem mais raro. De toda maneira, imagine que você tem um
banco de dados que codificou nome e sobrenome de indivíduos em duas
colunas distintas, e para fazer um relatório quer uní-los.

``` r
# Criando tabela de nomes
meus_dados3 <- tibble(ID = 1:3, 
                      nome = c("João", "Maria", "José"),
                      sobrenome = c("Silva", "Ferreira", "Alves"))

# Unindo variáveis nome e sobrenome

meus_dados3 <- meus_dados3 %>%
  unite("nome", c(nome, sobrenome))
```

Algumas coisas importantes aqui. Primeiro, por *default* a função
*unite()* irá inserir um underline “\_” entre o conteúdo unido. Você
pode mudar isso por meio do parâmetro/argumento **sep** da função. E
sim, você pode utilizar o espaço como separador - para isso, sep = ” “.
E sim, também. Você pode usar mais de um caractere para isso, por
exemplo, uma vírgula seguida de espaço”, ”

``` r
# Recriando as informações separadas
meus_dados3 <- tibble(ID = 1:3, 
                      nome = c("João", "Maria", "José"),
                      sobrenome = c("Silva", "Ferreira", "Alves"))

# Unindo e inserindo um espaço entre os nomes
meus_dados3 <- meus_dados3 %>%
  unite("nome", c(nome, sobrenome), sep = " ")
```

Uma segunda coisa importante é o uso de aspas em informações de texto no
R. A esta altura você talvez esteja um pouco confusa(o), especialmente
vendo o código acima com a variável nome, ora com aspas e ora sem aspas.

O R tem se tornado cada vez mais tolerante com essas coisas, por
exemplo, não aceitava aspas nos nomes dos objetos que desejasse remover
com a função *rm()*, mas agora já aceita. De toda forma, para evitar
problemas, há três regras do uso das aspas para texto no seu código.

- Usamos **sem aspas** para nos referirmos a um **objeto que já existe**
  no *global environment* ou uma **coluna que já existe** num
  *tibble/data.frame*.

- Por isso, as aspas são para nos referirmos a um nome que estamos
  ‘gerando’ naquele momento, seja objeto, seja coluna de um objeto.

- Quando você está se referindo ao **conteúdo em texto uma célula**,
  sempre **usamos aspas**.

Por isso, no nosso exemplo do *unite()*, a nova variável apresenta-se
entre aspas e as colunas antigas não se apresentam entre aspas.

## Recodificando Variáveis (mutate, case_when, arrange, top_n, top_frac)

Bom, para recodificar um banco de dados temos diversos caminhos,
conforme o problema que seja colocado. Vamos começar pelo mais simples,
que seja substituir o valor inteiramente.

``` r
# Limpando seu global environment
rm(meus_dados, meus_dados2, meus_dados3)

# Criando um novo banco
meus_dados4 <- tibble(ID = 1:4,
                        mes = c("janeiro", "março", "april", "novembro"),
                        ano = c(2001, 2012, 2015, 2018))
```

Para corrigir devemos **identificar** a informação que desejamos alterar
(e apenas ela); e **especificar** o novo valor.

Como você viu no encontro passado, caso queira **alterar** ou **criar**
uma variável, deve usar a função *mutate()*. Entretanto, você viu que
ela acaba mudando todos os valores da coluna e não é o que queremos
aqui! Por isso, temos que combinar a função *mutate()* com a função
*case_when()*, que restringirá os casos em que a recodificação irá
ocorrer.

``` r
meus_dados4 <- meus_dados4 %>%
  mutate(mes = case_when(mes == "april" ~ "abril")) 
```

Perceba o que fizemos. Corrigimos o valor que estava grafado errado,
sobrescrevendo a variável ‘mes’ que já existia. O *case_when()* admite
que você empilhe várias condições como você faz com o *filter()*, mas no
nosso exemplo usamos só um. A sintaxe, então, primeiro identifica a
variável/coluna que queremos recodificar e usando o operador lógico
(“==” equivalante à) colocamos “VALOR_ERRADO” ~ “VALOR_CORRETO”.

Certo, mas se você abriu o objeto ‘meus_dados4’, percebeu um
probleminha. Onde foi parar o resto das informações que queria que
permanecessem? Como o *mutate()* altera a variável inteira, é preciso
que a sintaxe do *case_when()* informe todas as condições se aplicam.
Você pode pensar aqui como aquela cláusula condicional que aprendemos no
encontro 3, onde você devia cobrir todas as alternativas para ela
funcionar (fossem duas “if else”, ou mais “if elseif elseif… else).

Para completar todos as condições, então, usamos o valor boleano TRUE. É
como se dissesse ao R, “mude case_when”; e ele me perguntasse, “mantenho
o resto?”, e eu respondesse: “TRUE”. Ok, vamos ver como isso ficaria.

``` r
meus_dados4 <- meus_dados4 %>% 
  mutate(mes = case_when(mes == "april" ~ "abril",
                                        TRUE ~ mes))
```

Fiz esse exercício para que você fixe isso: *case_when()* precisa de uma
linha completando as condições **TRUE ~ NOME_VARIAVEL**. Mas, de toda
maneira, esta função/comando admite que você ‘empilhe’ várias condições
definindo novos valores em suas células. Veja só abaixo:

``` r
meus_dados4 <- meus_dados4 %>% 
  mutate(nova_variavel = case_when( ano <= 2013 ~ "nao",
                                    ano > 2013 & mes == "abril" ~ "nao",
                                    ano > 2013 & mes == "novembro" ~ "sim"))
```

Por que não temos a linha com o valor TRUE? Por que, agora, cobrimos
todas as condições possíveis!!! Talvez agora esteja mais claro.

- Você deve construir suas condições **completando** todas as
  possibilidades.
- E as condições devem ser **mutualmente exclusivas**!
- A ordem em que as condições aparecem **não** importa.

Vamos exercitar um pouco, agora trabalhando com um *database* um pouco
maior, mas que já está pré-carregada no pacote *nycflights13* (vamos
trabalhar agora com 336776 linhas/observações).

``` r
## Instale o pacote
install.packages("nycflights13")

## Carregue a biblioteca
library(nycflights13)

## Salve o data.frame em seu global environment
flights1 <- flights

## Insira seu código nos trechos abaixo para responder ao que se pede

# 1) Crie uma nova variável que traga a data em formato "ano-mes-dia"

# 2) Separe a variável 'time_hour', criando duas novas variáveis e apagando a original

# 3) Recodifique a variável arr_delay (arrive_delay) para binário, sendo 1 para atrasado e 0 para sem atraso. Obs. Valores menores que zero significa chegada antes do previsto.
```

### Ordenando variáveis *arrange()*

Já citamos esta função no Tutorial 6, mas agora vamos ver alguns
exemplos. Não precisamos ordenar nossas colunas conforme os valores que
cada linha assuma; mas, por vezes, queremos organizar para uma tabela de
mais fácil visualização e apresentação. Imagine, por exemplo, que
tenhamos dados de datas apresentados desorganizadamente.

``` r
# Criando uma tabela
 meus_dados5 <- tibble(ID = 1:10,
                     ano = c(2008, 2005, 2009, 2006, 2006, 2007, 2008, 2005, 2008, 2005),
                     mes = c("Abril","Novembro","Julho","Março","Novembro","Fevereiro",
                           "Junho","Novembro","Janeiro","Outubro"),
                     temperatura = c(18.5, 32.4, 20.1, 22.5, 29, 34.5, 25.9, 28.8, 33.7, 23.8))
```

Caso queira ordenar conforme o ano e temperatura, como ficaria? Ou seja,
primeiro os dados seriam ordenados por ano e, dentro de cada ano,
ordenados por temperatura. Perceba que o primeiro bloco de código ordena
de modo crescente e o segundo de modo descrescente (basta usar o hífen
como ‘menos’).

``` r
# Organizando de modo crescente, por ano e temperatura
meus_dados5 <- meus_dados5 %>%
  arrange(ano, temperatura)

# Organizando de modo decrescente, por ano e temperatura
meus_dados5 <- meus_dados5 %>%
  arrange(-ano, -temperatura)
```

### Filtrando as maiores/menores observações *top_n()* e *top_frac()*

Um tipo de *filter()* específico seleciona as maiores/menores
observações de acordo com uma coluna/variável. Até poderíamos alcançar o
mesmo resultado usando *filter()*, bastando que ranqueássemos os valores
de uma variável e filtrássemos por um limite absoluto (por exemplo,
temperatura acima de 22.5) ou relativo (por exemplo, os 30% maiores
valores). Mas já existem funções que automatizam e economizam linhas de
código.

As funções *top_n()* e *top_frac()* só requer que você indique o número
de observações/linhas desejadas e de qual variável você tem interesse.
Veja os exemplos:

``` r
# Selecionando o mês com maior temperatura
maior <- meus_dados5 %>%
  top_n(n = 1, temperatura) # perceba, não precisava indicar o nome do argumento

# Selecionando 30% dos meses com maiores temperaturas
maiores30 <- meus_dados5 %>%
  top_frac(0.3, temperatura)

# Selecionando o mês de menor temperatura da amostra
menor <- meus_dados5 %>%
  top_n(n = -1, temperatura) # perceba, não precisava indicar o nome do argumento
```

## Identificando observações idênticas e valores únicos *distinct()*

Dificilmente bancos de dados são bem acabados e não trazem erros. Por
este motivo, talvez você encontre observações duplicadas. Quando for
resolver este problema, poderá fazer uso de uma função do *tidyverse*
que produz valores únicos dentro de uma ou mais variáveis, ou seja, que
funciona retirando tudo o que está duplicado.

Mas veja, você especifica nos argumentos quais são as variáveis que
deseja considerar. Por isso, talvez acabe perdendo observações que
trazem dados distintos em outras colunas. Fique atenta(o) a isso, caso
deseje incluir todas as variáveis de seu banco.

``` r
# Vamos verificar todos os trechos existentes
trechos <- flights1 %>%
  distinct(origin, dest) # neste caso, mantém somente duas variáveis

trechos_all <- flights1 %>%
  distinct(origin, dest, .keep_all = TRUE) # neste caso, mantém as demais - atenção para a sintaxe
```

Veja que *distinct()* vai te ajudar a analisar seu banco de dados, se há
informações duplicadas que podem indicar erros e prejudicar suas
inferências posteriores. Usando a mesma ferramenta com o R base,
bastaria usarmos a função *duplicated* precedida do operador lógico
negativo **!**. Aqui é uma escolha que você deve fazer, pois se
*distinct()* tem uma sintaxe mais permissiva, *duplicated()* pode
indicar para você quais são as linhas duplicadas - já que pode retornar
um vetor lógico. Além disso, o tempo de processamento de cada função é
diferente, o que implica em opções para trabalhar com grandes bases de
dados.

``` r
# Utilizando todas variáveis de parâmetro
trechos1 <- flights1[!duplicated(flights1), ]

# Utilizando a variável 'origin' de parâmetro
trechos2 <- flights1[!duplicated(flights1$origin), ]

# Utilizando duas variáveis de parâmetro
trechos3 <- flights1[!duplicated(flights1[c("origin", "dest")]), ]
```

Há uma função bem interessante do pacote R base que permite comparar
dois objetos e verificar se são iguais. Ela é particularmente boa para
quando você tem que atualizar algum banco de dados com frequência, caso
alguma nova informação seja publicada. Por exemplo, imagine que todo dia
uma instituição solta uma tabela com índices e valores vigentes, e você
precisa saber se houve alguma alteração com as informações do dia
anterior. Você vai ler linha por linha de cada tabela para descobrir?
Não! Deixe que o R faz isso pra você em alguns segundos.

Vamos então aproveitar para comparar os objetos ‘trechos_all’ e
‘trechos3’, que foram construídos com funções que deveriam ter feito a
mesma ação.

``` r
setdiff(trechos_all, trechos3)
```

Legal né? De maneira rápida você pode deixar o R trabalhar por você,
identificando diferenças e atualizações.

Paramos por aqui.
