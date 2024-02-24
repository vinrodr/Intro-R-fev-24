Tutorial 6
================

O R base pode ter parecido um tanto desafiador e difícil para você. Mas,
a partir de agora, começaremos o uso mais comum (e potente) da
linguagem R. Vamos trabalhar com a manipulação de dados por meio da
biblioteca tidyverse - mais especificamente, o dplyr, que é um pacote
dentro da biblioteca do tidyverse.

Você já deve ter notado que há diversas formas de realizar uma mesma
tarefa, então iremos usar essa nova gramática para manipular dados. Até
agora vimos um pouco disso, mas o R base ainda é limitado em seu
alcance. Ainda bem que a comunidade é bem ativa e produtiva, e já
desenvolveu soluções diversas para importar, manipular, organizar,
extrair, salvar, transformar etc bases de dados.

``` r
install.packages('tidyverse')
```

Certo, agora seu computador tem a biblioteca `tidyverse` instalada (e
ela contém o `dplyr`). Mas isso não basta. Lembre-se de que precisamos
sempre carregar os pacotes que trouxemos para nossa biblioteca. Pense
que o *install.packages* é como ‘comprar um livro e levá-lo para sua
casa’, enquanto o *library()* é quando ‘você pega o livro da estante e
leva para sua mesa de trabalho’.

``` r
library(tidyverse)
# Talvez o R não carregue o dataset que iremos trabalhar. Por isso, indique especificamente o dplyr.
library(dplyr) 
```

**Rememorando:** Já vimos brevemente que o R é especialmente potente
para análise de dados. E também vimos que normalmente esta tarefa é
baseada em base de dados em formato tabular, particularmente em formato
**data frame**. Por este motivo, passamos rapidamente (e eu sei, de modo
árduo) pelo R base para ver aspectos básicos da linguagem, como elaborar
funções e executar loops, e indicamos que a partir deste encontro 4 as
coisas mudam. Um data frame é uma base de dados em formato tabular, onde
cada coluna representa uma variável (ou característica) de um dado
conjunto, enquanto cada linha representa uma observação deste conjunto.
No cruzamento de cada linha (observação) com cada coluna (variável)
temos o valor atribuído. Vejamos um exemplo:

| Indivíduo | Peso (kg) | Altura(cm) |
|-----------|----------:|-----------:|
| André     |      67,8 |        172 |
| Olga      |      58,5 |        165 |
| Caetano   |      95,3 |        205 |
| Dandara   |      62,7 |        170 |

Perceba que os elementos da linha são diferentes. Cada linha traz
valores em texto (*string* - nome do indivíduo), números com casas
decimais (*doubles* - peso) e números inteiros (*interger* - altura).
Por sua vez, cada coluna somente apresenta elementos de mesmo tipo, já
que cada variável só adimite registros de um único tipo.

Voltando…

Certo, prontos para começar. Neste tutorial, veremos as principais
funções (comandos) do `dplyr`. Este pacote fornece uma função específica
para cada ação que você precisar executar em um banco de dados tabular
(data.frame). Vejamos os principais deles, de maneira resumida.

## 1. Renomeando Variáveis/Colunas (rename)

Embora possa parecer uma função bem simples, se você já trabalhou com
banco de dados já abriu variáveis como “V1” ou “br52_lm_00”, vai
entender como esta transformação é importante. Cada coluna (variável) em
nossa tabela terá sempre um nome e que podemos trocar quando desejarmos.

Para inspecionar os nomes de nossas variáveis, podemos executar o nome
do objeto e o resultado aparecerá no console. Também podemos usar a
função **names()**. Vejamos um exemplo a partir do banco dados com dados
dos filmes de Guerra nas Estrelas, que vem na biblioteca “starwars” do
*dplyr*.

``` r
names(starwars)
```

Perceba que o R descreveu as posições das variáveis (índices) no banco
com números à esquerda dos nomes.

Certo, agora vamos tentar renomear uma variável usando *rename()*. Vamos
aplicar a função ao data.frame *starwars*, como abaixo.

``` r
starwars %>% rename(especies = species)
```

Mas espere, por que nosso objeto não mudou e não retornou nenhum erro?
Por que aplicar funções não salva as alterações no objeto. É preciso
“salvar” essa transformação em um novo objeto (ou no mesmo,
sobreescrevendo). Como o banco starwars não é um objeto de nosso *Global
Environment*, mas uma biblioteca do *dplyr*, temos que usar a seta de
atribuição (*assingment*) para isso: nomeiei de *starwars1*.

``` r
starwars1 <- starwars %>%
  rename(especies = species)
```

Veja que agora você tem um objeto em seu *Global Environment* e ele tem
a variável ‘especies’ - e não ‘species’. Mas há algo de novo neste
código, certo?!

### Operador Pipe

Neste pequeno código temos a sintaxe fundamental de manipulação de dados
no tidyverse. Primeiro temos o objeto (starwars) e depois aplicamos a
função/transformação que desejamos neste objeto (rename). A estrutura é
bem simples, não? Mas apareceu algo novo aqui. O chamado **operador pipe
%\>%**, que fez a revolução na linguagem R. Agora você pode encadear uma
série de comandos fazendo uso do pipe. O operador funciona conectando um
objeto a uma função. Traduzindo grosseiramente seria um “e depois” ou
“then” do inglês. Como no exemplo, “pegue o objeto starwars e renomeie a
variável species”.

Usamos um símbolo específico chamado **pipe** para ligar o objeto e a
função que desejamos aplicar a ele (A razão da escolha deste símbolo?
Não sei e não importa, na verdade). Mas o grande ganho no uso de pipes é
que podemos juntar vários deles para combinar funções diferentes e gerar
uma análise mais complexa. Por exemplo:

``` r
starwars %>% 
  rename() %>%
  filter() %>%
  outra_funcao() %>% # a função outra_funcao() não existe, é apenas para você ver que não importa qual seja.
  mais_outra_função() # a função mais_outra_função() idem.
```

**Obs.** Já vimos isso, mas acho bom relembrarmos. Se eu usasse
*starwars %\>% rename()*, sem indicar os atributos da função rename, não
aconteceria absolutamente nada. Já que uma função pode ter um ou mais
atributos, exigindo obrigatoriamente pelo menos um (a função *ls()*
mostra os objetos existentes no seu Global Environment e funciona sem
você colocar nenhum parâmetro dentro dos parênteses. Mas isso não
significa que o parâmetro não exista. O que ocorre é que o R compreende
sem você precisar lançar e usa o default). No último encontro, você
aprendeu a fazer suas próprias funções e nos exemplos que dei e pedi
para você, por exemplo *funtion(cubo)*, criamos funções com um único
parâmetro.

Talvez não tenha notado, mas a sintaxe dos atributos no rename() é
**“NOME_NOVO = NOME_VELHO”**, e, portanto, se você digitar o nome
original errado, a função não irá funcionar e o R retornará um erro.
**DICA**: nomear variáveis tem suas boas práticas, especialmente se você
não se habituou a preparar um documento README.txt com a legenda delas.
Assim, evite usar espaços em nomes compostos, prefira o uso de underline
“\_“. Além disso, não comece o nome com números.

Certo, mas você já deve estar se perguntando. E se eu quiser alterar o
nome de diversas variáveis ao mesmo tempo? Teria que repetir a função?

Poderíamos fazer isso, mas é muito mais eficiente rodar dentro da mesma
função rename(). Basta que você separe por vírgulas cada variável
renomeada. **DICA**: deixe cada variável renomeada em uma linha
separada, isso facilita a visualização do seu código e ajuda a corrigir
eventuais esquecimentos. Não é raro que demoremos muito a descobrir um
único erro de vírgula faltando.

``` r
starwars1 <- starwars %>% rename(especies = species,
                                 nome = name,
                                 cor_cabelo = hair_color)
```

Perceba o código: o operador pipe está transformando o objeto ‘starwars’
e não ‘starwars1’. Por este motivo, quando repeti a operação de renomear
a variável ‘species’, o R retornou com uma resposta válida. Caso eu
tivesse executado o pipe no objeto ‘starwars1’, o R retornaria com um
erro - já que não existiria variável ‘species’.

## 2. Selecionando Variáveis/Colunas (select)

Embora o nome sugira que a função *select()* serve para selecionar
variáveis, ela deve ser entendida em sentido mais amplo. Por meio deste
comando, você pode manipular as colunas (variáveis) da sua tabela, seja
para excluir, reposicionar ou selecionar visando outras operações.

Pode parecer bobagem agora, mas quando você for trabalhar com banco de
dados grandes e tiver apenas algumas variáveis de interesse, usar o
*select()* tonará sua vida bem mais fácil e ligeira. Tomemos um exemplo,
então:

``` r
starwars1 <- starwars1 %>%
  select(nome,cor_cabelo,especies)
```

Veja que escolhi somente as variáveis que já havíamos renomeado
anteriormente. **Obs**. Mas atenção: quando você excluir as colunas,
isso não pode ser desfeito. Para chegar a mesma etapa do seu código,
teria que rodar todo o script novamente até ali.

**DICA**: Por esta razão, é uma boa prática sempre deixar um arquivo
original salvo como objeto no seu *Global Environment*. Por exemplo,
quando você fizer o upload de um arquivo, deixe ele salvo como
“arquivo_original” ou “arquivo_download”, criando um novo objeto com o
qual irá trabalhar. Assim, caso você rode um comando errado, sempre
poderá voltar ao arquivo original preservado.

Vale dizer que você pode utilizar um rol de operadores lógicos com esta
função (e como veremos, com muitas outras). Assim, você pode ao invés de
nomear as variáveis, indicar as suas posições no objeto(lembra-se dos
números de índice que falamos ali em cima?) e usar dois pontos **:**
para selecionar um grupo de variáveis. Além disso, pode utilizar o não
**!** para criar um subset evitando certas variáveis. Os operadores
lógicos ‘and’ **&** e ‘or’ **\|** igualmente se aplicam. E, por fim,
caso seja um grupo de variáveis de índice não contínuo, você pode usar o
**c()** para indicar quais são.

**Pausa para funções importantes**: Há outra coisa que vai te ajudar
muito! Existem funções que foram desenhadas para trabalhar com grandes
bancos de dados. Por exemplo, você tem variáveis que começam com um
prefixo ou que contêm determinado *string* (por exemplo, “br” ou
“cod_ibge”). Para isso, você pode lançar mão cumulativamente das
funções: - **starts_with()** Inicie com o prefixo indicado. -
**ends_with()** Termine com o sufixo indicado. - **contains()** Contenha
literalmente o string. - **matches()** Coincida extamente com uma
expressão.

``` r
a <- starwars %>%
  rename("estetica" = ends_with("color")) #Perceba que renomeei e os nomes ganharam um índice
```

## 3. Transformando Variáveis (Mutate)

Certo, e como faria se quisesse criar novas variáveis na minha tabela?
Isso é bem razoável, afinal você que vai trabalhar com análise de dados
irá, com toda certeza, criar relações a partir de informações já
disponíveis para você. Então, vejamos um exemplo bem simples: Caso eu
quisesse calcular o PIB (produto interno bruto) per capita? Pegaria o
valor do PIB e dividiria pela população. Para fazer isso no R, você
teria que usar a função/comando *mutate()*.

Ela permite que você combine, usando a operação matemática que você
desejar, as colunas **que já existem** no banco de dados (se queremos
trazer dados que ainda não estão no nosso tibble/data.frame, usaremos
uma outra função *join()* que veremos em outro momento).

Então, vamos a prática? A gramática do *dplyr* é a mesma dos exemplos
anteriores: primeiro o objeto, depois o pipe e depois a função/comando
(com seus atributos/parâmetros).

Dentro dos parâmetros da função *mutate()* (use o help!!), iremos
especificar o cálculo a ser realizado fazendo uso dos nomes das
colunas/variáveis atuais, e indicaremos o nome da nova variável/coluna
em que devemos guardar o resultado do cálculo. Por exemplo, eu quero
triplicar o valor de ‘height’.

``` r
starwars1 <- starwars1 %>% 
  mutate(height_triplo = height*3)
```

A nova variável está onde? Toda variável que você criar vai ser colocada
ao final (à direita) da sua tabela. Caso queira visualizar, use *View()*
(a letra V é maiúscula - e sim, esquecemos disso sempre, já que é algo
raro em nomes de funções de R), ou *names()* para ver a nova variável
incluída.

Agora, podemos fazer muito mais que isso. Vamos combinar diversas
variáveis para alcançar cálculos mais complexos. Por exemplo, vejamos a
metade da soma entre ‘height’ e ‘mass’:

``` r
starwars1 <- starwars1 %>% 
  mutate(calculo = (height + mass)/2)
```

Uma outra facilidade do *mutate()* é que ele pode reconfigurar a
variável **sem a necessidade** de criar uma nova. Por vezes, queremos só
aplicar uma correção nos nossos dados (por exemplo, quando alguém
corrige preços pela inflação mensal)… e criar uma nova variável, para
depois excluir a antiga e reposicionar a nova onde a outra estava
(lembre-se que as variáveis criadas são jogadas para o final da sua
tabela) daria muito trabalho. Para fazer isso, basta que você
sobrescreva o conteúdo original pelo resultado do cálculo que irá
realizar. Assim, o nome da ‘nova coluna/variável’ vai ser idêntico ao da
variável/coluna que já existe. Veja o exemplo:

``` r
starwars1 <- starwars1 %>%
  mutate(mass = mass * 100)
```

E, por fim (e mais legal!), você poderá usar outras funções por dentro
da função *mutate()* e não apenas operadores matemáticos (da mesma forma
que você fez com *select*). Mais pra frente, isso vai abrir um mundo de
possibilidades de análise para você. Por enquanto, vamos aplicar uma
função que muda todos os *strings* da variável texto para minúsculas.

``` r
starwars1 <- starwars1 %>% 
  mutate(name = tolower(name))
```

## Linhas

Talvez você tenha percebido já, ou ainda tenha surgido a dúvida de como
realizar operações com as linhas da tabela como parâmetros. Afinal, até
agora só vimos comandos/funções que trabalharam com as
variáveis/colunas. Pois bem, é o que veremos agora.

## 4. Cortar/Selecionar observações (slice)

Tenha em mente que as observações de seu banco de
dados/tabela/data.frame são seus indíviduos de interesse, que assumem
valores específicos para cada variável. Por exemplo, no censo, cada
linha corresponderia a um indivíduo que teria valores específicos para
cada resposta (variável/coluna). Caso você queira selecionar um conjunto
de indivíduos/observações a partir de **critérios de posição**, você
usaria a função *slice()*.

Tornando mais claro, vamos ver um exemplo.

``` r
starwars1 <- starwars %>%
  slice(1:10)
```

Mas você deve se lembrar que no R base poderíamos usar o comando
X\[1:10, \] e chegar ao mesmo resultado!!! Qual a vantagem do slice,
então? A aplicação no ambiente *dplyr* permite uma encadenação de
comandos (que veremos já já!) e tem duas variantes interessantes para
quem vai fazer uso de base de dados públicas!

É bem comum que os dados que você escolha para trabalhar venham com
ruído, lacunas ou erros. O problema mais recorrente é a existência de um
cabeçalho ou um rodapé nos dados. Uma explicação ou autoria que é
indicada e que difere do formato da tabela. Infelizmente, não é raro que
isso aconteça, pois o hábito de fazer arquivos do tipo README.txt para
acompanhar o banco de dados não é disseminado como deveria. Pois bem, há
casos em que você terá que abrir o arquivo em algum leitor de planilhas
(libreoffice, excel, numbers etc) e corrigir o problema. Mas há
situações que o banco de dados é tão grande que você não consegue abrir
nestes programas e, portanto, deve desenvolver uma solução no seu
código. Para isso há comandos como:

- **slice_head()** e **slice_tail()** Permitem que você escolha um certo
  número de linhas para retirar do início/final do seu data.frame. Você
  ainda pode usar as funções **slice_min()** e **slice_max()** para
  selecionar apenas o menor ou o maior valor.

``` r
starwars %>%
  slice_head(n = 5)

starwars %>%
  slice_tail(n = 3)
```

**Obs.**Veja uma coisa importante: Há inúmeras funções dentre de
inúmeros pacotes. Você pode ter que encontrar uma solução para seus
dados que não está neste tutorial. Tenha isso em mente. Você vai evoluir
na linguagem e buscar por soluções aos problemas que irá se deparar. Por
isso há a indicação de várias ferramentas no README deste curso. Acima
de tudo e a de acesso mais fácil e rápido: *help()* - você usou
*help(slice)*? Deveria, já que é uma função nova para você.

Voltando…

Claro que pode parecer sem utilidade agora, mas fará mais sentido à
frente. Especialmente, caso você use a função *slice()*
concomitantemente com um parâmetro que você guardou em um objeto
previamente. Veja o exemplo:

``` r
linhas_desejadas <- c(1,2,4,5,10)

starwars1 <- starwars %>%
  slice(linhas_desejadas)
```

O R irá substituir o objeto ‘linhas_desejadas’ pelos números indicados e
devolverá um *tibble* das 5 linhas desejadas. É possível também fazer a
operação pelo seu inverso, ou seja, usar o *slice()* para excluir
linhas. Para isso, adicionamos um hífen **-** antes da numeração.

``` r
starwars1 <- starwars %>%
  slice(-1)

starwars1 <- starwars %>%
  slice(-linhas_desejadas)
```

**Obs**. Quando você exclui linhas, as restantes têm seu índice
renumerado para manter a ordem sempre sem saltos.

Há ainda a hipótese de excluir observações/linhas não sequenciais, mas
que obedecem a alguma regularidade. Por exemplo, as linhas das dezenas
(a cada dez linhas) até a linha 100. Vejamos:

``` r
starwars1 <- starwars %>%
  slice(seq(from=0,
                      to=100,
                      by=10))
```

**LEMBRANDO**: Perceba que você usou os nomes de cada
argumento/parâmetro (‘from’, ‘to’, ‘by’) seguido por um símbolo de igual
e o seu valor desejado. Mas estes argumentos têm uma ordem fixa dentro
da função, e se você souber essa ordem não é preciso que escreva os
nomes dos atributos. Isso evita que você perca tempo (no futuro!!!
Agora, enquanto está aprendendo, é importante que deixe tudo bem
inteligível para você! E se você não está usando os comentários do
código \#, você deveria!). O código abaixo é idêntico ao código acima:

``` r
starwars1 <- starwars %>% 
  slice(seq(1,100,10))
```

E se você nomeasse os atributos e alterasse a ordem prévia da função? O
R iria aceitar, pois no caso de você nominar os atributos não importa a
ordem que os valores aparecerão!!! A regra da ordem fixa só vale para o
*default*, quando você não nomeia os valores que coloca entre os
parênteses (como no exemplo anterior).

**LEMBRANDO 2**. E como podemos saber os nomes e ordem dos argumentos,
mesmo? Use a função *help()* ou o ponto de interrogação antes do nome da
função: *help(slice)* ou *?slice*.

## 5. Filtrando as observações/linhas (filter)

É mais comum que não seja a posição de uma linha/observação seu critério
de seleção de uma observação/linha do seu banco. Na verdade, na análise
de dados, é mais comum que nos interessemos pelo valor que a observação
assume em uma dada variável/coluna. Queremos filtrar somente os
indivíduos maiores de 65 anos, que vivem na periferia das regiões
metropolitanas do Brasil; ou as reações positivas em amostras de
interação de moléculas de aminoácidos; ou as bases de controle
metereológico que indicaram valores superiores de temperatura à média
histórica ao longo do ano …

Para isso, usamos a função *filter()*, especificando as **condições**
que queremos encontrar nos valores de cada variável. O R vai avaliar se
o parâmetro de cada observação é verdadeiro ou falso (TRUE ou FALSE),
armazenando apenas as observações ‘verdadeiras’.

Vamos testar em nosso exemplo. Vamos selecionar apenas os
indivíduos/observações que não têm cabelo. E como fazemos isso?
Precisamos de três elementos:

- Nome da variável/coluna - para nós, ‘hair_color’.
- Espécie/tipo de comparação que iremos realizar - para nós, queremos
  selecionar as observações com ‘hair_color’, então vamos precisar do
  operador lógico de igualdade **==**. Sim, lembre-se que são dois
  iguais juntos!
- Critério - aqui seria o valor que esperamos que as observações/os
  indivíduos assumam naquela variável. Para nós, ‘none’.

``` r
starwars %>%
  filter(hair_color == "none") 
#lembre-se: trata-se de uma variável texto, em que os valores nas células estão em *string* - por isso as aspas no valor.
```

E veja só, você fará uso agregado dos operadores lógicos e matemáticos
aqui. Vejamos um exemplo, a partir do banco de dados `starwars` (que já
vem com o R base), que seleciona somente os indivíduos que tenham
skin_color == ‘light’ e eye_color == ‘brown’.

``` r
starwars2 <- starwars %>% 
  filter(skin_color == "light", 
         eye_color == "brown")
```

Agora, se você foi atento, percebeu que eu salvei o resultado da minha
seleção em um novo objeto. Como você já deve saber a esta altura, você
pode ou não salvar o resultado, e pode ou não fazê-lo sobreescrevendo o
objeto anterior. Eu criei um novo objeto, pois ele é menor que o
anterior e para você memorizar que normalmente deixamos o banco original
salvo e criamos um banco só das observações que iremos trabalhar.
Lembre-se: Aqui nossos exemplos são didáticos e pequenos, mas quando
você estiver lidando com grandes bases de dados, a capacidade de
processamento será crucial para a velocidade e alcance dos seus
resultados.

Por fim, vamos usar operadores lógicos concomitantemente com o
*filter()*.

``` r
starwars3 <- starwars %>% 
  filter(sex == "feminine" | mass > 50 & mass < 100)
```

Uma última coisa. Talvez a seleção de linhas precise excluir ou manter
observações com *NA* (missing values), para isso usamos a função
*is.na()*. Por exemplo, caso você queira excluir todas as observações
cuja cor do cabelo é desconhecida ‘hair_color’ (o sinal de exclamação,
lembre-se, serve para inverter a operação. O **!** é o operador lógico
de negação, lembra?).

``` r
starwars1 <- starwars %>% 
  filter(!is.na(hair_color))
```

**DICA**: A escolha de excluir as observações com *missing values* faz
parte do desenho de pesquisa que você adotar. Há ganhos e perdas em
fazê-lo, mas se lembre que não importa qual base de dados você irá
trabalhar, os *missing values* estarão presentes em maior ou menor grau.

## 6. Outras funções menos usadas

- **arrange()** Altera a ordem das linhas conforme critério escolhido.
  Grosso modo, é aquele filtro automático da sua planilha excel, em que
  você reordena suas linhas a partir da distribuição de valores em uma
  ou mais colunas.

``` r
starwars %>% 
  arrange(height, name) #veja que funciona com variáveis numéricas e strings!
```

- **desc()** Podemos usar o arrange associado com o comendo desc(), de
  modo a organizar uma coluna em ordem descrescente.

``` r
starwars %>% 
  arrange(desc(mass))
```

## Combinando Manipulações usando o Operador Pipe %\>%

O operador **pipe** altera a cadeia de operações (‘pipeline’), que passa
a permitir que apliquemos uma série de funções/comandos a um objeto sem
a necessidade de repertirmos o seu nome diversas vezes. A economia aqui
não é só de linhas no seu código, mas também de capacidade de
processamento.

``` r
starwars4 <- starwars %>% 
  rename(sexo = sex) %>%  # por que não há aspas aqui? Por que é o nome da variável(objeto) e não os valores assumidos na variável. Se quisesse selecionar "Obi-Wan", ai sim usaria as aspas.
  mutate(mass = mass*100) %>%
  filter(sexo == "none"  & gender == "feminine") %>% 
  select(height, name, gender, species, sexo) 
```

Duas coisas importantes: - Perceba que como renomeei a variável como
primeira operação do bloco do pipe, então as próximas operações já devem
ser realizadas considerando tal alteração. Por isso, para filtrar as
linhas e selecionar as colunas (na terceira e quarta linhas do bloco
acima), devo usar o novo nome da variável: “sexo”, e não “sex”. -
Perceba também que aproveitei para reordenar as colunas, jogando a
variável sexo para o final do meu *subset*. Abra o objeto e veja que só
há uma única observação/indivíduo que atende aos requisitos que
estabeleci no bloco de código acima.

É importante, portanto, que você perceba que mesmo que o código seja
executado em bloco, cada ação/comando atualiza o objeto para a próxima
ação. Uma sendo resultado da outra. Então, caso você colocasse
filter(sex == …), o R retornaria um erro. Para um grande conjunto de
dados e um bloco de pipe complexo, a dica é rodar uma linha de cada vez
previamente, testando e identificando eventuais erros, para depois
executar o código por inteiro.

Agora, tente você. (Para cada operação, use o dataset original)

- Quais são os humanos referidos no dataset starwars?
- Restrinja seu banco de dados original, selecionando somente
  características físicas dos indivíduos.
- Quais personagens masculinos estão com sobrepeso? (IMC = Peso / Altura
  ² )

|          Resultado |               Situação |
|-------------------:|-----------------------:|
|       Abaixo de 17 |   Muito abaixo do peso |
|   Entre 17 e 18,49 |         Abaixo do peso |
| Entre 18,5 e 24,99 |            Peso normal |
|   Entre 25 e 29,99 |          Acima do peso |
|   Entre 30 e 34,99 |            Obesidade I |
|   Entre 35 e 39,99 |   Obesidade II(severa) |
|        Acima de 40 | Obesidade III(mórbida) |

## 7. Abrindo dados (input)

Ok, estas primeiras funções do dplyr optei por usar um *dataset*
previamente carregado no seu R. Mas vamos ver como abrir seus próprios
arquivos. O que quer dizer, tornar arquivos externos em objetos do seu
*Global Environment*.

Assim, o primeiro passo é contar para o R qual é o diretório da sua
máquina que ele deve buscar os arquivos. Para isso, vamos relembrar duas
funções importantes.

Ao iniciar o R, você irá iniciar uma sessão. E o diretório de trabalho é
aquele endereço (local ou externo) onde o R irá buscar ou armazenar
arquivos. Para verificar qual é o seu diretório de trabalho você pode
usar o comando:

    getwd()

Caso queira alterar este diretório, use a função:

    setwd()

Dessa maneira, a sessão sempre será iniciada vinculada a um *workspace*!
Sempre tenha isso em mente ao salvar seus arquivos ou buscá-los. Tudo o
que você fizer: de cálculos e análises estatísticas a gráficos, imagens
e banco de dados tudo estará no seu working directory (wd). O *default*
para o wd costuma ser a pasta “Meus Documentos” ou “Documentos” do seu
diretório raiz. Caso deseje alterar e não saiba como, abra a pasta que
começará a receber os arquivos e vá em propriedades com seu mouse atrás
da informação “path”, ou “caminho”, “diretório”, ou ainda “pasta pai”.
Copie essa informação e cole na sua função *setwd()* usando as aspas,
por exemplo, “/home/user/documents”. (Use help para ver os nomes dos
atributos de setwd).

Dica: Se você usa windows, um bug para você se lembrar. Por que alá
quis, você **talvez** tenha que usar as barras invertidas e aos pares
para indicar o caminho **\\**. Por exemplo, “\home\user\documents”.

**Importante**: Não use *setwd()* em scripts compartilhados. Definir o
diretório de trabalho é uma das poucas exceções à regra de que você
sempre deve escrever todo o seu código em scripts. - O diretório de
trabalho de outra pessoa será diferente do seu! - Você deseja que seu
código seja portável.

Lembre-se: quando você sai do R (comando q() ou pelo Idle Rstudio) será
questionado se deseja gravar o seu working directory. Ainda que não
tenha produzido arquivos .jpeg, .xls, .csv, .txt etc, você pode salvar
os objetos que guardam seus avanços na análise. Ou seja, é possível
gravar todos os objetos do seu Global Environment em um arquivo do tipo
**.RData**. Você poderá carregar este arquivo a qualquer momento que
desejar e continuar suas análises. Já o seu *script* é salvo
separadamente em um arquivo **.R**, que tem formato texto. Em suma,
salvar um não significa salvar o outro e vice-versa.

### Dados em arquivos texto (.txt, .csv, .tsv)

Primeiro vale dizer que existem inúmeras funções para abrir arquivos de
dados, de diferentes formatos, mas dado que este é um curso intensivo,
vamos focar nos mais comuns e que são arquivos que trazem informações em
formato ‘retangular’ (colunas x linhas).

**Obs.** Talvez não devesse, mas só para que você saiba que existe: há
um botão para abrir arquivos no R. Mas veja, se você decidiu aprender a
programar, provavelmente quer substituir seu tempo perdido pelo tempo da
máquina trabalhando em seu lugar. E por isso estamos aprendendo a
escrever *scripts* que não substituam do começo ao fim das tarefas que
devemos executar. Dito isso, vamos lá:Lá na janela do seu *Global
Environmet* há um botão (ao lado do botão de salvar) com o nome “import
dataset”. Clicando nele você terá a opção de importar arquivos de texto
com duas bibliotecas diferentes ‘base’ e ‘readr’(esta é o pacote de
abertura de dados do tidyverse), além disso, de dados em outros formatos
como excel e softwares de análise estatística SPSS, SAS, Stata. Quando
você selecionar sua opção, irá aparecer um espaço para que indique uma
pasta local ou URL, insira e clique em ‘Update’. No campo ‘Name’, você
dá o nome do seu objeto a ser criado. E veja que ao lado há um “Code
Preview” — melhor, não?

Embora já saiba, vale dizer que você pode executar uma tarefa de
diferentes maneiras no R - especialmente, em diferentes
pacotes/bibliotecas que têm as mesmas funcionalidades. Por isso, você
encontra no R base variações das funções de importação que veremos aqui
no *tidyverse*. Para o R, as funções do tipo “read” são as que funcionam
para abertura de dados. Experimente digitar *read* no seu *script* e
veja o que o RStudio te sugere. Veja que o próprio *Rbase* traz funções
do tipo *read* para diferentes tipos de arquivos.

Provavelmente a função mais utilizada para importar arquivos seja a
*read_csv()*, que como o nome já mostra, abre arquivos do tipo .csv
(separado por vírgulas “comma”). Talvez você já tenha salvo uma planilha
do seu excel (.xls) e notou que ele aceitava também .csv e .txt. Pois
bem, estes são formatos enxutos, que ao invés de manter a estrutura da
tabela, usa vírgulas (.csv) ou tabulação (.tsv) para delimitar os
valores das células, e entende que a primeira linha do arquivo será a
designação das suas variáveis. Por isso, você pode abrir um arquivo .csv
num bloco de notas ou no próprio Excel/CalcBrOffice que irá funcionar.

Mas como vamos trabalhar juntos no mesmo arquivo, faça o download para
sua máquina [aqui](../Data) e vamos tentar abrir os arquivos.

``` r
# ATENÇÃO: o caminho entre aspas faz referência ao meu wd. Veja o seu e substitua.

dados1 <- read_csv(file = "/home/vinicius/Área de Trabalho/Curso R - Data/amostra_hp.csv")
dados2 <- read_csv(file = "/home/vinicius/Área de Trabalho/Curso R - Data/amostra_ht.csv")
dados3 <- read_csv(file = "/home/vinicius/Área de Trabalho/Curso R - Data/amostra_hv.csv")
```

Agora veja lá no *Global Environment* (não precisa abrir o arquivo!),
“dados1” e “dados2” só têm uma única coluna/variável, enquanto “dados3”
tem cinco variáveis/colunas. Por que isso? O que aconteceu? (Agora você
pode abrir o arquivo com um duplo clique sobre o nome do objeto lá no
*Global Environment*).

Percebeu que o R colocou todas as informações numa única coluna para os
dois primeiros exemplos? Isso aconteceu, pois a função “read_csv” admite
como separador a vírgula “,” e esses objetos eram delimitados por
tabulação e por ponto e vírgula. Faça o seguinte: Abra os arquivos que
você baixou para sua máquina no bloco de notas. Veja a estrutura do
arquivo e volte aqui.

Aqui apresentei a você outra grande fonte de erro no R. Saber quais são
os parâmetros que os arquivos foram salvos. Há funções mais flexíveis
para abrir dados, como é o caso da função *read_delim()*, que permite
que você especifique qual o caractere utilizado para separar as colunas.

``` r
dados1 <- read_delim(file = "Curso R - Data/amostra_hp.csv",
           delim = ";")

dados2 <- read_delim(file = "Curso R - Data/amostra_ht.csv",
           delim = "\t") #aqui \t significa tabulação, já que não poderíamos só 'dar um tab'.
```

Pronto! Agora você tem os seus dados certos!

Agora, o padrão da função “read” é importar os dados com a primeira
linha fazendo referência aos nomes das variáveis. Mas existe bancos de
dados que não trazem as colunas com rótulo. Neste caso, o R retornaria
uma tabela com várias colunas e cada uma nomeada com os valores
assumidos pela primeira observação.

``` r
dados_sem_header <- read_delim(file = "Curso R - Data/amostra_nv.csv",
                    delim = ",")
```

Para evitar que isso aconteça, precisamos indicar no
parâmetro/argumento/atributo **col_names** da função *read_delim()* deve
ser igual a “FALSE” ou “F” (lembre-se: O R aceita ambos maiúsculos).
Atenção: este parâmetro **col_names** não é exclusivo desta função. Esta
‘funcionalidade’ é encontrada em outras funções do tipo *read* - o que
pode ocorrer é que o nome deste atributo seja diferente.

Com isso, são criados rótulos em que um “X” antecede um índice conforme
a posição da coluna. Dito de outra forma, caso seus dados não tiverem um
**header** (cabeçalho), a primeira linha deles serão convertidos
necessariamente como nomes/rótulos das colunas, salvo se você indicar
que seu dados não possuem **header** por meio do parâmetro **col_names =
FALSE**, mas ao fazer isso, o R cria os nomes.

``` r
dados_sem_header <- read_delim(file = "Curso R - Data/amostra_nv.csv",
                    col_names = F, 
                    delim = ",")
```

Mas você ainda pode nomear as colunas! Ao invés de criar um índice de
“X1”, “X2”, “X3”… você pode usar o parâmetro/atributo **col_names** para
corrigir seus dados.

``` r
dados_com_header <- read_delim(file = "Curso R - Data/amostra_nv.csv", 
                    col_names = c("estado", "municipio_cod", "municipio_nome",
                                  "NIS", "transferido"),
                    delim = ",")
```

As vezes, poderá ser de seu interesse definir as classes das variáveis
‘a priori’. Isso evita que o R aplique transformações em seus dados no
momento em que importá-los. Assim, usamos o parâmetro/atributo
**col_types** e criamos um conjunto conforme a sequência das variáveis
nos seus dados. Aí, para abreviar: “c” = “character” (texto), “d” =
“double” (números com decimais), “i” = integer (números sem decimais),
“l” = “logical” (booleanos).

``` r
dados_com_header <- read_delim(file = "Curso R - Data/amostra_nv.csv", 
           delim = ",", 
           col_types = "cicid")
```

Certo, mas agora imagine um banco de dados que tenha o separador de
casas numéricas como a vírgula (como é no Brasil) e também tenha
escolhido a vírgula como separador entre células. Vai ficar uma bagunça!
As funções *read* tentarão identificar automaticamente. Mas calma, você
consegue arrumar isso, temos só que especificar no argumento **locale**
essas diferenças.

**Dica**: No Brasil, usamos o ponto e vírgula (**;**) como caractere
separador de colunas e a vírgula (**,**) de separador decimal.

``` r
dados <- read_delim(file = "Curso R - Data/amostra_hv.csv", 
                    delim = ",", 
                    locale = locale(decimal_mark=",",grouping_mark="."))
```

**Obs.** Este atributo também é utilizado para informar o formato que
horas (12h, 24h, com ou sem segundos etc) e datas (DIA/MES/ANO não é
universal!) estão escritas nos seus dados.

### Arquivos Excel (.xls e .xlsx)

Normalmente o primeiro contato com análise e manipulação de base de
dados, seja de pesquisadores ou profissionais, é feita por meio de
editores de planilha. Infelizmente, organizações ainda disponibilizam
seus dados no formato do software pago Excel (.xls ou .xlsx), fazendo
com que muitos pesquisadores ainda adotem esta ferramenta para construir
e analisar seus dados. Então, vamos ver como subir arquivos deste tipo e
depois exportá-los em formato texto (com tamanho no disco infinitamente
menor, inclusive!).

Para isso, precisamos da biblioteca **readxl**. Não é preciso instalar,
pois ela faz parte do *tidyverse*, mas você já sabe que precisa chamar
ela para sua mesa de trabalho.

``` r
library(readxl)
```

Nosso exemplo vai buscar um arquivo na base do IBGE (Pesquisa Perfil dos
Municípios Brasileiros de 2005 - aka ‘MUNIC’). Faça o
[download](https://ftp.ibge.gov.br/Perfil_Municipios/2005//base_MUNIC_2005.zip)
e descompacte (“Base 2005.xls”) lá na pasta que escolheu como seu
*working directory*.

A essa altura você já deve ter percebido que o R permite que você
navegue e selecione arquivos/objetos de endereços diferentes do seu
*working directory*. E deve estar se perguntando, então por que raios eu
preciso usar o *setwd()*. Pois bem, há um ganho imenso quando estamos em
um projeto e não precisamos ficar escrevendo um endereço inteiro a cada
vez que ‘upamos’ ou ‘salvamos’ um arquivo. Basta que digitemos o nome do
arquivo e o R acessará tudo que está na pasta do seu *working
directory*.

Certo, voltando…

Use a função **excel_sheets()** para examinar quais são as
abas/planilhas do seu arquivo excel.

``` r
excel_sheets("Base 2005.xls")
```

Apareceram ‘só’ 11 abas diferentes. Além de algumas mensagens de erro,
certo? A aba dicionário não são dados, mas quase como um README com
informações espalhadas nas células sobre a pesquisa. Todas as outras
estão em formato ‘retangular tabular’ (‘tibble’). Então, agora, importe
a planilha ‘Variáveis externas’ do arquivo. Você poderá fazer isso de
duas formas:

``` r
# Primeira colocando o nome da planilha
MUNIC_EXT <- read_excel("Base 2005.xls", "Variáveis externas")

# Segunda colocando a posição da planilha 
MUNIC_EXT <- read_excel("Base 2005.xls", 11)
```

A função read_excel aceita os argumentos “col_names” e “col_types” tal
como as funções de importação do pacote readr. Observe que o R não se
importa e não lembra como o arquivo foi aberto - quando aberto por
read_csv ou read_excel ou outra função, o tibble em R é idêntico.

### SPSS, Stata e SAS

Veja só. Se você é do campo das ciências econômicas já deve ter
usado/escutado/visto arquivos em formato Stata. Que é um software
estatístico pago utilizado com relativa frequência por universidades e
institutos de pesquisa. Caso seja das ciências humanas ou biológicas,
pode ter trabalhado com SPSS ou SAS em algum momento dos longíquos anos
90 e 2000.

Pois bem, o R é uma ferramenta tão poderosa que importa arquivos
produzidos por estes softwares pagos e permite que você trabalhe num
ambiente de software livre!!!! Para isso, há alguns pacotes, mas indico
um que faz parte do *tidyverse*, o pacote *haven*. Como já sabem, peguem
o livro na estante e coloquem sobre sua mesa de trabalho. Você o
comprou, quando saiu para comprar o *tidyverse*.

``` r
library(haven)
```

Esta biblioteca traz cinco comandos/funções de importação de dados: -
Para dados SAS, **read_sas()** - Para dados SPSS, **read_sav()** e
**read_por()**, conforme o dado gerado pelo software - Para dados Stata,
**read_stata()** e **read_dta()**, também conforme o formato dos
arquivos gerados pelo software.

Vamos tentar? Entrem no site do
[Latinobarômetro](https://www.latinobarometro.org/latContents.jsp), que
traz versões de seus dados em SAS, Stata e SPSS. Baixe manualmente e
extraia os arquivos do ano de 2015 para seu *working directory*, como
fizemos antes. Feito isso, veja como é simples:

``` r
# Dados em formato SPSS
dados_spss <- read_spss("Latinobarometro_2015_Eng.sav")

# Dados em formato Stata
dados_stata <- read_stata("Latinobarometro_2015_Eng.dta")
```

Atenção: Existe critérios para converter variáveis categóricas, rótulos
de variáveis, delimitadores etc… tudo isso será manipulado pelo R ao
importar arquivos de outras linguagens. Mas agora, você já consegue
descobrir isso sozinha/o. Lembre-se: help(), stackoverflow, readme do
nosso curso.

### Encoding

Para terminar essa aula, que já está longa, vamos ver outro ponto chave
de erros/problemas no R.

Quando queremos abrir arquivos que contenham caracteres especiais,
normalmente você irá passar por isso. E aqui não estou falando de
símbolos estranhos, basta uma cedilha (ç) ou um acento para seus
problemas começarem. Há diferentes maneiras por meio das quais o PC
interpreta caracteres. O *encoding* de cada arquivo irá variar conforme
o **sistema operacional de seu computador** e **software utilizado na
geração do arquivo.**

Agora talvez você se lembre daquela boa prática: escreva nomes sem
caracteres especiais!

``` r
dados <- read_delim(file = "Curso R - Data/amostra_hv.csv", 
                    delim = ",", 
                    locale = locale(encoding='latin1'))
```

Outras funções, seja de importação, seja de escrita (salvar), também tem
esta funcionalidade. Evidente que você precisa ver o nome do
parâmetro/atributo em cada uma delas.

**DICA:** Não há uma bala de prata para resolver problemas de *encoding*
e por isso é um ponto chave de problemas. Por vezes, quem gera o arquivo
não fornece informações sobre como se produziu aquele dado, e você terá
que ir por tentativa e erro. Os mais comuns no Brasil são: ‘latin1’,
‘latin2’, ‘utf8’ e ‘WINDOWS-1252’ - mas há inúmeros outros, e por isso
valorizamos tanto quando há um arquivo README acompanhando os dados que
iremos trabalhar. Caso seu arquivo não tenha caracteres especiais, não é
preciso fazer nada, pois o R já vai abrí-lo/salvá-lo de maneira
acertada.

**DICA2:** O formato mais universal e flexível para se trabalhar é o
UTF-8 (utf8). Caso tenha curiosidade sobre *enconding*, como isso surgiu
e como se pretende criar parâmetros de transformação e comparação
universais [veja
aqui](https://www.ime.usp.br/~pf/algoritmos/apend/unicode.html)

## Ficamos por aqui

Tente começar a resolver o Desafio 1 em sala, se tiver tempo.
