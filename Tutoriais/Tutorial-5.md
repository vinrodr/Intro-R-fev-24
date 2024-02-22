Tutorial 5
================

# Introdução à programação em R (fev-24)

## Alfabetização em R base: Execução condicional e *loops*.

Aprendemos o uso dos operadores em R no último encontro, agora, fazendo
uso deste conhecimento, iremos construir cláusulas condicionais “if”,
“else” e “else if”. Elas são instrumentos fundamentais para a construção
de funções e algoritmos, já que controlam o fluxo de comandos de nosso
código!

Antes de mais nada, lembra-se que podemos usar a função *Help* para
esclarecer quaisquer dúvidas, certo? Para o caso da programação de
execuções condicionais, há ainda um resumo agregado que pode ser
acessado por meio do seguinte comando:

> ?Control

Certo, agora vejamos um exemplo simples para começar.

``` r
# imprima aprovado, a não ser que discente tenha valor menor que seis.
discente <- 4.5
if(discente > 6) {
  print("aprovado.")
} else {
  print("Discente não aprovado.")
}
```

A cláusula condicional *if* deve obedecer o comando que aparece entre os
(parênteses). Já o resultado, caso a (condição) seja satisfeita, dá-se
conforme a instrução colocada dentro das {chaves}. Ou seja, o comando
será atendido caso a cláusula seja verdadeira!!! (agora fica mais fácil
compreender por que razão há o operador lógico **!** \[“não”\], já que a
cláusula precisa ser verdadeira, quando desejamos a negativa desta
cláusula, fazemos uso do operador lógico negando. Por exemplo, x != 0 \|
x != z).

Uma boa prática a ser seguida é iniciar as chaves após fecharmos o
parênteses e fecharmos as chaves na linha seguinte ao fim das
instruções.

> if (condição) {
>
> instruções
>
> }

Outra boa prática é “identar” o código da cláusula, ou seja, desalinhar
o conteúdo das instruções do restante do seu código. Mas não se
preocupe, pois, diferentemente de outras linguagens (como é o caso do
Python e do HTML), **R não requer identação para funcionar**.

Spoiler: Se você pressionar a tecla “enter” após a abertura das chaves
ou ao término da instrução, o RStudio identará automaticamente seu
texto.

``` r
x  <- 10
z <- c(200, x, "meu texto")

if(x %in% z){
  print("está incluso")
} 
```

Vamos trabalhar com tranquilidade neste momento, não se preocupe. Outro
exemplo pode ajudar a tornar isso ainda mais claro. Imagine que você
está trabalhando novamente com os dados das eleições brasileiras de 2022
e precisa automatizar quais candidatos a deputado estadual foram eleitos
e quais não foram. Imaginando que fosse somente um o coeficiente, você
sabe qual é o número de votos necessários para ganhar uma cadeira, qual
seja: 15.000 votos.

Então você prepara este pequeno algoritmo.

``` r
votos <- 15000
if (votos > 15000){
  situacao <- "candidato eleito"
}

print(situacao)
```

Ok, você já consegue criar e preencher uma coluna com a informação dos
que foram eleitos. Mas, neste caso, não haveria nenhuma informação nas
células daqueles que não foram eleitos. Assim, você pode elaborar um
outro algortimo que dê conta dos casos em que a cláusula não foi
atendida.

``` r
votos <- 15000
if (votos > 15000){
  situacao <- "candidato eleito"
} else {
  situacao <- "candidato não eleito"
}

print(situacao)
```

Você percebeu o que fizemos? Usamos na sequência do comando *if*, o
comando *else*. Caso tenhamos somente uma condição (unidimensional
condition), só precisamos usar *if*. Caso desejemos também prever a
alternativa a esta condição, usamos o *else*.

``` r
if (condição){
  instrução
  } 
else{
  todas as alternativas
  }
```

**Obs.** Quero somente pontuar outra coisa. Você talvez se lembre, que
podemos alcançar um resultado de várias maneiras no R e que isso se deve
ao grande número de pacotes existentes. Pois bem, estamos aprendendo
aqui o *R base* e você ainda verá pacotes com maior celeridade na
análise computacional. Estes têm cláusulas condicionais com alguma
variação nesta estrutura - já que a regra é não ter mais de um comando
com o mesmo nome. No próximo encotro já veremos isso, no pacote
tidyverse. Neste momento, basta que saiba disso.

É possível alocar uma cláusula dentro de outra, estabelecendo uma árvore
de condições. Não é raro que você queira criar variáveis a partir de
condições relacionadas e costuma fazer isso no papel sulfite. Assim, não
precisa se preocupar, pois com o tempo você irá fazer algoritmos cada
vez mais complexos. Lembre-se que isso é mais uma questão de lógica do
que saber como programar em R - caso tenha dificuldade, faça uso do
papel e depois copie para a estrutura do R base.

Vejamos agora o *else if*, que é utilizado quando queremos colocar
**duas ou mais** condições intercaladas. Você pode usar uma série de
*else if* concatenados com **um** *if* e **um** *else*.

``` r
votos <- 250
if (votos > 15000){
  situacao <- "candidato eleito"
} else if (votos > 8000  & votos <= 15000){
  situacao <- "candidato suplente"
} else {
  situacao <- "candidato não eleito"
}

print(situacao)
```

Perceba o que fizemos. Agora usamos três cláusulas condicionais
intercaladas, onde a primeira *if* traz a condição inicial, a segunda
*else if* uma segunda condição e para a terceira cláusula *else* ficam
todos os demais casos não previstos nas duas primeiras. Lembre-se disso:
*else* será utilizado para abarcar todas as situações não abarcadas
pelas cláusulas *if* e *else if*.

Considere outro exemplo:

``` r
numero <- 100

if(numero <= 100) {
  print("menor ou igual a 100")
  } else if(numero < 999) {
    print("menor que 999")
}
```

Neste exemplo, o *else* não será executado, já que o *if* já teve sua
condição satisfeita. Grosso modo, entende o *else* como um “do
contrário”. Resumindo, os blocos de *else* e *else if* só irão ser
executados pelo R, caso não tiverem tido condições anteriores
antendidas. Olhe o oposto, para fixar melhor.

``` r
numero <- 100
if(numero <= 100){
  print("menor ou igual a 100")
  } 
if(numero < 999) {
  print("menor que 999");
}
```

Veja que com dois *if*, o R irá executar ambos os comandos. Isso, pois,
são duas condições **independentes**.

### Tente você

- Tente se lembrar quantas horas você dormiu na noite passada. Crie uma
  variável ‘sono’ para guardar esta informação.
- Crie sua própria condicional, a partir da regra: caso tenha dormido
  mais que oito horas, imprima “repouso”. Do contrário, imprima
  “cansaço”.

## Repetindo tarefas - *Loops* explícitos: “while” e “for”.

Agora que você já viu a ferramenta de programação condicional, vamos ver
como o R trabalha com repetição de tarefas.

Especialmente no começo, você copiará e colará partes do seu código com
um pequeno ajuste de cada vez. Mas saiba que você irá abandonar este
procedimento gradativamente - e na velocidade com que se torna mais
familiarizado com os *loops*. Nós evitamos copiar e colar um mesmo
trecho do código mais do que duas vezes - esta é outra boa prática que
ajuda você a evitar:

- a tarefa irritante de escrever código para um “n” de elementos muito
  grande
- a dificuldade de se alterar o código mais tarde, caso seja necessário
- a propensão a erros e bugs.

Ao invés disso, portanto, procure sempre fazer uso de *loops* de
repetição. Mesmo que você não consiga no começo, ter essa meta facilita
sua trajetória. Em pouco tempo terá um código enxuto e elegante.

Pois bem, então invés de repetir uma tarefa até alcançar determinada
condição (como aprendemos antes), você queira repetir uma tarefa por um
número já conhecido de vezes. Por exemplo, você queira colocar lançar na
planilha do RH, 900 reais de vale alimentação para os 30 funcionários de
sua empresa; ou você queira lançar um dado 30 vezes e obter o resultado.
Em todos estes casos, uma alternativa é utilizar a função *for* para
criar um loop.

Diferentemente das cláusulas condicionais, que funcionam como: “enquanto
ocorrer x, faça y”; agora as ideias de loop funcionam como: “para todo
elemento de a (todo i em a), faça algo até b”. O *for loop* é uma
ferramenta simples que funciona por meio da **iteração** (*iteration*),
que nada mais é que a repetição de um mesmo código para diferentes
valores de entrada armazenados numa variável (vetor/objeto) de entrada.

Veja como ficaria no exemplo abaixo:

``` r
# Para todo número k entre 1 e 5, imprima este número. Ou lendo de outra maneira, "para cada k de 1 até 5, faça"
for (k in 1:5){
  print(k)
}
```

O funcionamento do *for* loop é variar o elemento “k” a cada iteração do
código - **de acordo com a ordem estabelecida**. Veja como fica o mesmo
código, agora com a ordem invertida.

``` r
# Para todo número k entre 1 e 5, imprima este número. Ou lendo de outra maneira, "para cada k de 1 até 5, faça"
for (k in 1:-5){
  print(k)
}
```

Certo, vamos tornar as coisas um pouco mais úteis agora. Imagine que
você deseja calcular a média de diferentes variáveis de um certo banco
de dados (data.frame). Como sabemos, as variáveis estão nas colunas
deste banco de dados e cada linha é um indivíduo/observação. Assim,
vamos fazer uso de um banco de dados que o R já tem pré-carregado para
que seja utilizado para fins didáticos. E vamos supor que desejamos
saber a média total de homicídios, a média populacional e a média da
taxa de homicídios (todas calculadas abaixo).

``` r
install.packages("dslabs")
library(dslabs) # carregando a biblioteca já instalada
data(murders) # executando a função data, para o objeto murders

#selecionando algumas colunas para minha análise. Boa prática: renomear o objeto original.
murders2 <- cbind(murders, taxa = murders$total / murders$population * 100000) 

mean(murders2$total)

mean(murders2$population)

mean(murders2$taxa)
```

Qual é o problema com esse código? Aparentemente nenhum, já que
conseguimos os resultados. Mas agora imagine repetir o cálculo da média
para 15 variáveis diferentes. Pois é por isso que fazemos uso dos
*loops*. E, novamente: mesmo que você tenda a executar um código mais
longo e repetitivo no começo, com o tempo vai produzir seus próprios
*loops*.

``` r
numeric_cols = c("total", "population", "taxa")
for(var in numeric_cols) {  # para todo elemento do objeto "var"
  print(mean(murders[[var]])) # imprima a sua média
}
```

### for + condição

Agora, vamos associar um *for loop* a uma condição.

``` r
# Para cada i elemento de 1 até 42, desde que i seja ímpar, imprima i.
for (i in 1:25){
  if((i %% 2) != 0){ # caso o resto da divisão de i por 2 não seja 0, temos um número ímpar 
    print(i)
  }
}
```

Embora tenhamos trabalhado com vetores numéricos até agora, o *for loop*
pode ser executado também com outras classes de vetores. Basta colocar
após o “in” dentro do parênteses o vector que desejar. Vejamos um
exemplo:

``` r
# Para cada i elemento de 1 até 42, desde que i seja ímpar, imprima i.
cores <- c("roxo", "vermelho", "verde", "azul", "amarelo")

for (aquarela in cores){
  print(aquarela)
  }
```

Veja outra coisa. A estrutura do *for* ppermite que você nomeie o termo
que precede o “in” como bem entender. No caso de elemento numérico,
costumamos usar uma letra. Para o exemplo acima, para fins didáticos dei
o nome de aquarela para o objeto.

**Em suma**, *loops* resolvem problemas onde devemos repetir
procedimentos variando apenas um índice. Com o tempo você aprenderá a
usar os *loops* com maior facilidade e agilidade. Eles economizam um
tempo precioso, já que conseguimos automatizar tarefas ou deixamos o
script mais enxuto quando deixamos de repetir o mesmo comando inúmeras
vezes.

## While loop

Quando quisermos utilizar uma regra condicional e um *loop* de
repetição, podemos fazer uso de uma ferramenta ainda mais simples. O
*while loop* realiza uma série de repetições, conforme uma condição e a
partir de um estado inicial. Assim, a estrutura se encerra com a
instrução para que o R realize uma repetição enquanto a condição estiver
satisfeita.

Vamos tentar traduzir essa sintaxe agora para a linguagem R. Preciso que
o R compreenda que ele deve “imprimir” o número que desejo, sempre
somado de uma unidade, partindo de 1 até 27. Portanto, minha condição
será: enquanto houver variável no registro inferior a 27, realize a
soma. Note bem que eu determinei o início do *loop* por meio da
indicação do objeto registro valendo 1, antes do *while loop*.

``` r
# determino o início
registro <- 1

# começa o while
while (registro <= 27) {
  print(registro)
  registro <- registro + 1
}
```

Fazendo a tradução para o idioma português: *enquanto* o registro for
menor ou igual a 27, imprima e some uma unidade. Neste sentido, a
estrutura de um *while loop* é sempre:

> “enquanto” (condição), “faça” (instrução).

Resumindo, então, a estrutura do *while*: - estado inicial - condição
(‘regra de quebra’) - instrução

Agora, podemos pontuar um elemento fundamental de todo *loop*: o uso do
comando *break*. Na medida em que o R obedece aos nossos comandos, caso
ordenemos que ele realize uma iteração em que a condição nunca será
satisfeita, o programa não irá cessar. Por isso, duas práticas são
aconselhadas:

1)  Especificar as ‘regras de quebra’: o critério de parada (condição
    entre parênteses) deve ser atendido em algum ponto do processamento
    do seu algoritmo (*while loop*) para que haja a interrupção.

2)  Ficar atenta(o) ao especificar as regras, pois enunciar errado uma
    regra/condição que nunca se encerra, pode acarretar com que o R
    feche a sessão por falta de memória (‘out of memory’).

**Obs.** Um erro comum desta espécie é esquecer que a condição inicial
será alterada a cada iteração (a palavra é sem o “n”)!

**\[condicional + while\]** Agora, vamos colocar uma cláusula
condicional aninhada com o *while loop*. E faremos isso repetindo o que
fizemos antes para o *for*, para armazenarmos somente os números
ímpares.

``` r
# determino o início
registro <- 1

# Começa o while
while (registro <= 15) {
  
  if ((registro %% 2) != 0){
    print(registro)
  }
  registro <- registro + 1
}
```

Como antes, agora o código está todo integrado, já que o condicional
está no interior do *loop*. Repetindo o que havia dito: Este é mais um
problema de lógica do que de sintaxe da linguagem de programação. Faça
no papel antes de passar à linha de comando. Você verá que em breve fará
seus scripts com bastante elegância, robustez e velocidade
computacional.

## Funções Customizadas

Nós já discutimos a ideia de função em outro encontro. Falamos que
função deve ser entendida como uma série de comandos/regras, ou seja, um
“passo a passo” para o R executar. Vimos também que as funções em R
obedecem à estrutura “nome_da_função(atributos_da_função)”, bem como,
apresentamos algumas funções do R base.

Agora, vamos aprender como criar nossas próprias funções/algoritmos, que
podem ser extremamente úteis no desenvolvimento de nossas
pesquisas/análises. Vamos começar com algo simples.

``` r
potenciacao <- function(cubo){
  z <- cubo^3
  return(z)
}
```

Neste primeiro exemplo, eu desenhei um algoritmo chamado “potenciacao”,
que irá solicitar um número de entrada e irá oferecer o seu resultado
elevado ao cubo. O exemplo é simples para que percebam a sintaxe da
expressão. Para criarmos uma função customizada, temos o comando
*function*. Este irá exigir três informações: 1) dentro dos parênteses
será a informação que irá ser avaliada e, portanto, muda a cada
iteração; 2) dentro das chaves estará ‘o que a função faz’. 3) Além
disso, precisamos colocar ao final do código, dentro das chaves, o
argumento **return()**: que define qual o resultado da função. Vejamos
outro exemplo:

``` r
calcular_z = function(coordenada) {
  z = (coordenada - mean(coordenada)) / sd(coordenada)
  return(z)
}
```

Neste exemplo, a função “calcular_z” foi desenhada para aplicar o
cálculo de normalização de variáveis. Dentro das chaves, a variável
“coordenada” é subtraída de sua média e dividida por seu desvio padrão.

Perceba que, em ambos os casos, a função poderá ser aplicada em qualquer
variável, uma vez que tenha sido criada como um objeto do R. Ao invés de
ter que redigir toda a fórmula “cubo” ou “calcular_z” a cada vez que
queira utilizar, agora posso simplesmente utilizar as funções
customizadas que criei: potenciacao() e calcular_z().

Evidentemente que estamos trabalhando com algoritmos simples para que
entendam a lógica e estrutura da função customizada. Mas saibam que
conforme suas análises apresentem repetições e encadeamentos excessivos,
você poderá desenhar um algoritmo que atenda as suas necessidades.

### Tente você

Para terminar, tente você:

- Crie um vetor numérico e, depois, crie uma função que calcule a média.
- Crie uma função que faça a conversão de temperatura de Celsius para
  Farenheit. Para isso, incorpore a fórmula de Celsius =
  (farenheit - 32) \* 5/9.
- Crie um conversor monetário, que transforme reais em dólares na
  cotação de 5 para 1.
