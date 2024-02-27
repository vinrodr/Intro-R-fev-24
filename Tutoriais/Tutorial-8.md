Tutorial 8
================

# Organizando seus dados

Agora, vamos ver como o R pode produzir resumos estatísticos de seus
dados, que são extremamente úteis quando você tem que realizar
descrições de bancos de muitas variáveis e/ou linhas. Lembre-se que
quanto maior é a informação que precisará explicar ao seu leitor, mais
difícil é fazer isso sem medidas de resumo como média, mediana, desvio
etc.

A função/comando *summarize()* fará isso para nós. E veja que bom,
também funciona dentro da sintaxe do tidyverse com o operador pipe.
Contudo, é importante perceber que este comando gerará um novo objeto
(tabela/data.frame) que conterá apenas as medidas de resumo solicitadas.

``` r
# Carregando os pacotes que usaremos
library("nycflights13")
library("tidyverse")

# Pedindo pela média da distância percorrida
flights %>%
  summarize(media_atraso = mean(distance))
```

A sintaxe é composta por três elementos, um primeiro que informa o nome
da(s) variável(eis) que será(ão) criada(s); um segundo que é(são) a(s)
função(ões) que pretendo usar como medida de resumo - no nosso exemplo
foi a função *mean()*; e, por fim, a(s) variável(eis) que será(ão)
resumida(s). Bem simples. E *summarize()* é equivalente a *summarise()*.
Para qualquer função estatística do R base ou outro pacote desenhado
para isso, você poderá calcular estatísticas de seu interesse.

Agora, tente você com os exemplos abaixo.

| Medida estatística |           Função no R  |
|--------------------|-----------------------:|
| Média              |                mean()  |
| Mediana            |              median()  |
| Desvio Padrão      |                  sd()  |
| Quartil (25%)      | quantile( ,probs=0.25) |
| Mínimo             |                 min()  |
| Máximo             |                 max()  |

Caso queira, você pode agregar diversas medidas resumo no bloco de
código separando os argumentos por vírgulas. Veja o exemplo:

``` r
flights %>% summarize(distancia_media = mean(distance),
                      distancia_mediana = median(distance),
                      distancia_desvio = sd(distance))
```

Talvez você tenha tentado outras variáveis para fazer seu cálculo e o R
retornou **NA** como resultados. Estou certo? Primeiro, parabéns, pois é
assim mesmo que caminhamos no aprendizado. Segundo, você sempre precisa
**estar atenta(o) aos valores faltantes (missing values)** na hora de
pedir ao R para calcular estatísticas.

O R sempre irá retornar **NA** quando você solicitar o cálculo da
estatística de uma variável que tem pelo menos 1 NA. Difícil? Isso é
ótimo, na verdade. Com esse resultado o R nos permite investigar nossos
dados e encontrar lacunas e erros. Certo, mas o que fazemos então? Vamos
usar o atributo **na.rm = TRUE** nas funções. Isso fará com que o R
ignore os valores faltantes!

``` r
flights %>% summarize(atraso_decolagem_media = mean(dep_delay, na.rm = TRUE),
                      atraso_decolagem_mediana = median(dep_delay, na.rm = T),
                      atraso_decolagem_desvio = sd(dep_delay, na.rm = T))
```

## Reunindo os dados em grupos *group_by()* e *ungroup()*

Frequentemente, as informações apresentam padrões conforme se distribuem
nas variáveis e nos levar a refletir quais seriam as estatísticas
considerando certo agrupamento/subgrupo do meu banco de dados. E, neste
caso, como faríamos para mensurar? Seria preciso criar uma nova variável
com *mutate()*, recodificando os valores de cada grupo, por exemplo,
valor1 = grupoA, valor2 = grupoA…? Não, o R tem sua própria função para
agrupar os dados, sem haver a necessidade de modificar nada seu banco
original.

Claro que você pode criar um novo objeto que traga os grupos
descriminados, mas isso não é preciso.

``` r
# Criando objeto com database agrupada conforme aeroporto de destino
destino_voo <- flights %>% group_by(dest)
```

Surpresa! Os objetos ‘destino_voo’ e ‘flights’ são quase que inteiramente
iguais. Então, o que aconteceu? Ocorre que a função *group_by()*
**sozinha não irá alterar nada do seu banco original**. Caso você
escreva ‘destino_voo’ no seu console, para verificar o objeto, verá que
linhas e colunas são iguais, mas apareceu uma nova linha \> dest \[105\]
que não existia. Isso é o R te contando que o objeto está agrupado
conforme a variável ‘dest’ e tem 105 grupos.

Então, para ser útil, precisamos combinar o *group_by()* com outras
funções. Veja o exemplo que calcula a média do atraso na aterrissagem para
cada um dos 105 aeroportos da variável ‘dest’:

``` r
flights %>% group_by(dest) %>% 
  summarize(atraso_medio_aterrissagem = mean(arr_delay), na.rm = T)
```

Ué?! Um monte de NA, mas eu pedi que o R ignorasse os *missing values*.
O que aconteceu? Fiz isso para você perceber que quando combinamos
funções, podemos acabar confundindo onde o atributo deveria estar.
Lembre-se que ‘na.rm = T’ deveria ser um atributo da função que calcula
a estatística - para nós, da função *mean()*. Mas o atributo está fora,
portanto, funcionando como um argumento de *summarize()*. E qual seria a
sintaxe desta função? na.rm seria o nome da variável que receberia o
valor TRUE para as observações. Então, vamos corrigir o código.

``` r
flights1 <- flights %>% group_by(dest) %>% 
  summarize(atraso_medio_decolagem = mean(arr_delay, na.rm = T))
```

Legal, né? Agora você tem uma ferramenta potente para investigar seu
*data frame*. E ela pode agrupar os seus dados por mais variáveis!!!
Veja só o cálculo da média do atraso de aterrissagem para o binômio
origem-destino.

``` r
flights %>% group_by(origin, dest) %>% 
  summarize(atraso_medio_aterrissagem = mean(arr_delay, na.rm = T))
```

Apareceu uma advertência, certo? O R deve ter te contado que:
*summarise() has grouped output by ‘dest’. You can override using the
.groups argument.\>“*. Usei este exemplo para te contar a parte que
acabamos esquecendo no uso do *group_by()*, que é a necessidade de
‘desagrupar’ seu objeto depois que você fez suas análises. Lembra que lá
atrás o seu console adicionou uma linha ‘origin \[105\]’? E você não tinha
feito absolutamente nada além de usar o *group_by()*?!

Pois é. A ação de agrupar um objeto é permanente, demandando que você
use o **ungroup()** (sem nenhum argumento) para retornar o objeto a
condição anterior. E, inclusive, você não precisa salvar o resultado do
*group_by()* em um objeto para que ele esteja agrupado e demande
desagrupar! Veja que flights não teve seu resultado salvo, no código
anterior! O que você pode concluir disso? Que *group_by()* é uma função
que orienta o R a maneira pela qual deve olhar para determinado objeto e
não uma operação nos seus dados - que, inclusive, continuam iguais.

Mas veja: Para o nosso último exemplo, entretanto, o R roda o que
pedimos. Até pouco tempo o R não retornaria um ‘warning’ para você, mas
sim faria todas as ações subsequentes com o agrupamento ativo. Como isso
gerava enormes problemas nas diversas operações que você acaba fazendo
com seus dados, acrescentaram o argumento **.add = TRUE** para que a
função *grou_by()* sobrescreva o agrupamento anterior como *default*.

> When FALSE, the default, group_by() will override existing groups. To
> add to the existing groups, use .add = TRUE.

Então, qual foi o problema que ainda restou para o uso de *group_by()* e
que exige que façamos nosso *ungroup()*? Para todos os demais casos em
que você não irá fazer novo agrupamento. Ou seja, se o *group_by()*
resolveu seu problema para novos agrupamento, ela não resolveu para os
casos em que você fizer operações agrupadas e voltar para fazer
operações desagrupadas. Por este motivo, recomendo sempre usar o
*ungroup()* ao final do bloco de código, pois evita que você se esqueça
que seu *data frame* estava agrupado quando rodar análises
posteriormente do seu banco inteiro.

Tudo isso numa frase: fique atenta(o) em sempre desagrupar *ungroup()* -
é simples e necessário.

``` r
# Reagrupando
flights %>%
  group_by(dest) %>%
  summarize(atraso_medio_aterrissagem = mean(arr_delay, na.rm = T)) #%>%
  ungroup() # desagrupando
```

### Agora faça você mesmo

Usando o objeto flights, pré-carregado em seu R, calcule:

- A duração média do tempo de vôo (air_time) de cada companhia área
  (carrier).

- A duração média do tempo de vôo de cada companhia, mas agora
  informando por mês.

- Você consegue dizer qual o aeroporto de destino (dest) tem a pior
  média de atraso? Dica: Use group_by() e top_n() ou arrange()

- Agora, informe qual é a companhia aérea menos pontual (carrier).

### Agrupamento para criar novas variáveis *group_by()* + *mutate()*

Você acabou de trabalhar com agrupamento e produção de estatísticas de
resumo, certo? Mas acabou gerando uma nova tabela que colapsava todos os
dados originais em alguma medida de resumo menor. Entretanto, você
também pode usar o *group_by()* para construir novas colunas em seu
banco original, bastando que use o *mutate()*.

Na verdade, como já deve ter percebido, no R (e, particularmente, no
*tidyverse*) você pode associar funções/comandos para alcançar uma
solução para seu problema. Assim, Iremos usar o *group_by()* associado a
inúmeras funções, embora as principais sejam ‘summarize’, ‘mutate’ e
‘ggplot’. Como veremos daqui a alguns encontros, para a produção de
gráficos, o *group_by()* é extremamente potente.

Certo, então vamos imaginar que agora você queira construir uma nova
variável com a média do tempo de atraso para cada aeroporto de origem.
Perceba que a medida resumirá a média para cada aeroporto de origem,
repetindo valores para todos os vôos partindo dali.

``` r
flights4 <- flights %>% 
  group_by(origin) %>%
  mutate(atraso_medio = mean(dep_time, na.rm=TRUE)) %>%
  ungroup()
```

### Resumindo inúmeras variáveis *across()*

Por que normalmente pedimos estatística resumo de inúmeras variáveis, o
pessoal que construiu o *tidyverse* facilitou nossa vida. Há uma função
que permite que você escreva menos código nos argumentos de
*summarize()*.

A sintaxe da função é diferentona, pois aplicamos combinando
‘summarize()’ e a ‘estatística’ que desejamos, mas esta fica como um
argumento de ‘across()’ Veja como fica:

``` r
flights %>% summarize(across(c(air_time, arr_delay), # informando para quais variáveis
                             mean, # informando a estatística que quero calcular
                             na.rm=TRUE)) # lembrando de ignorar eventuais NA's
```

Vamos deixar o código mais enxuto ainda e entregando mais análises? Que
tal se incluíssemos outras estatísticas? Como estas passam a ser um
argumento da função *across()*, poderia criar um objeto com os nomes de
todas as funções que desejo executar. Veja como ficaria:

``` r
flights_stats <- flights %>%
  summarize(across(c(air_time, distance),      # informando para quais variáveis
            list(mean, median, sd, max, min),  # informando a estatística que quero calcular
            na.rm=TRUE))                       # lembrando de ignorar eventuais NA's
```

As colunas terminadas em “\_1” do novo objeto ‘flights_stats’ fazem
referência às estatísticas listadas da primeira variável ‘air_time’,
enquanto as terminadas em “\_2” fazem referência à variável ‘distance’.

Por fim, vale uma última função *everything()*. Você aplica ela de
maneira combinada com as outras duas e evita ter de escrever o nome de
todas as variáveis. Mas evidentemente que as colunas com variáveis texto
(character ou factor), não haverá cálculo algum destas estatísticas e
serão inseridos NA’s. Veja como ficaria:

``` r
flights_stats <- flights %>%
  summarize(across(everything(),               # informando que são todas as variáveis
            list(mean, median, sd, max, min),  # informando a estatística que quero calcular
            na.rm=TRUE))                       # informando para ignorar NA's
```

Há um procedimento que é bemmmmm comum para pesquisa quantitativa e você
já deve ter enfrentado. Trata-se da padronização de uma variável, que é
alcançada subtraindo-se a média e dividindo pelo desvio padrão. Você
poderia construir esse cálculo e aplicar para cada variável, não é
mesmo? Mas se lembra que falamos que toda ação repetitiva e que ocorre
muito provavelmente já tem uma função/algoritmo/comando desenhado pela
comunidade do R? E neste caso não é diferente, já que padronizar
variáveis é uma das atividades mais corriqueiras da estatística.

Para isso, então, usamos a função *scale()*. Vejamos como ficaria na
combinação com *across()*:

``` r
flights %>% mutate(across(everything(), 
                          scale))
```

Apareceu um erro, não é mesmo? O ‘x’ deve ser numérico. O que o R está
nos dizendo aí? Que a sintaxe de *across()* não é tão flexível assim.
Quando ele encontrou a primeira variável que não era numérica, parou de
executar o código e informou você. No nosso exemplo, parou em ‘carrier’
que é a variável dos nomes das companhias.

Certo, então precisamos de uma solução que permita: ou pular as colunas
que não são numéricas, ou que permita selecionar as colunas que
queremos. Para o primeiro caso, precisamos do *select()* e ir
manualmente selecionando antes de rodar o *mutate(across())* - como já
fizemos antes.

flights %\>% mutate(across(c(year, month, day, dep_time, sched_dep_time,
dep_delay, arr_time, sched_arr_time, arr_delay, flight, air_time,
distance, hour, minute), scale))

Funciona, mas a depender do seu banco de dados vai ser bem cansativo
digitar tudo isso. Então, para a segunda alternativa, usamos uma
variação do ‘across’, que é a função *where()*. Como queremos só as
variáveis numéricas no nosso exemplo, usamos também a função do gênero
**is.** para contar ao R para aplicar só onde as colunas são numéricas.
Veja como fica:

``` r
flights %>%
    mutate(across(where(is.numeric), scale))
```

Duas linhas e você padronizou todas as suas variáveis!!! Que tal isso?!

Ficamos por aqui.
