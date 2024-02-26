Tutorial 1
================

## Ambiente de programação

## Software R

**ATENÇÃO**: não iremos reinstalar o R nestes computadores, pois o
ambiente já está configurado e o R deixou de oferecer suporte para a
versão de windows que temos aqui.

O software R tem uma nova versão e duas a três atualizações menores
anualmente. É uma ótima prática manter o R e seus pacotes atualizados.
Por mais que a atualização possa ser chata, já que a melhor maneira é
desinstalar e reinstalar o R e seus pacotes, adiar só irá deixar as
coisas piores.

Para baixar R, vá para [CRAN](https://cloud.r-project.org/) e siga as
seguintes etapas: 
* Clique no botão CRAN no lado esquerdo.
* Selecione um espelho que seja próximo, ou seja, brasileiro. O espelho da USP ou da UFPR são ótimos. 
* Selecione qual tipo de máquina você possui (Windows, Linux ou MacOS X). 
* Caso tenha algum problema, você pode consultar o guia de instalação e administração do R [aqui](http://cran.r-project.org/doc/manuals/R-admin.html).

Mas vamos esclarecer o que você acabou de fazer. O CRAN (comprehensive R
archive network) é formado por uma série de servidores espelho
distribuídos ao redor do mundo, que são utilizados para distribuir os
*pacotes* e o software R.

Um jeito simples de atualizar, caso use sistema windows, é usar o pacote
updateR diretamente no R Studio. Conforme segue o exemplo:

``` r
# Instalar o pacote 'installr', caso não esteja instalado
if (!requireNamespace("installr", quietly = TRUE)) {
  install.packages("installr")
}

# Carregue a biblioteca 
library(installr)

# Update R
updateR()
```

Por último, caso os pacotes (bibliotecas) estejam desatualizados, o R envia
um alerta na linha de comando ao carregá-los. Você poderá executar a
atualização por meio do install.packages() da linha de comando ou por
meio da barra de menu: Tools \> check for packages update.

## Software R Studio

**ATENÇÃO**: Da mesma maneira que o software R, não iremos reinstalar o
R Studio. Veja onde você pode encontrá-lo e os passos para instalá-lo em
sua própria máquina. É bem simples, baixe em
<http://www.rstudio.com/download> e instale. O RStudio é atualizado
algumas vezes por ano e sempre avisa quando há uma nova versão
disponível.

O fato de instalarmos dois softwares para
programar pode gerar algum estranhamento, mas isso acontece por que enquanto o **R** é o software de
processamento, o **R Studio** é a interface do usuário que lhe permitirá
usar e salvar seu código mais facilmente. O R Studio, assim, é o
ambiente que *‘roda sobre o R’*. Um jeito que ajuda a entender é pensar
o R como o motor de um carro e o R Studio como o conjunto de volante,
acelerador e embreagem.

De toda maneira, há duas formas de rodar uma linha de código: (I) digite
seu comando diretamente no ‘console’ e dê *Enter* para executar; (II)
selecione a(s) linha(s) de seu código que deseja executar e clique
simulteneamente as teclas *Crtl + Enter* (alternativamente, pode usar o
ícone ‘Run’ na aba do painel do script). Na prática, raramente fazeremos
uso da primeira opção de executar diretamente no R console. Isso pois, o
R console só aceita um comando de cada vez! Cada linha de código é
executada para que outra possa ser inserida, e é por esta razão que o
IDE facilita muito o seu trabalho!

Como você irá descobrir nos próximos dias, a ordem de execução das
linhas de código é determinante para o resultado que você obtém do
processamento. O R seguirá suas ordens de comando e é um excelente
trabalhador para atividades repetitivas e chatas. Entretanto, sempre
haverá um grande risco em executar os seus códigos na ordenação
equivocada. O script, dessa maneira, é um instrumento robusto para dar
unidade e deixar a sua análise clara. Na eventualidade de você ficar
confusa(o) com as operações que já foram executadas, basta que você
limpe o seu environment (ícone da vassoura na aba do painel) e reinicie
os comandos do script.

Nesse sentido, o R Studio é um ambiente de desenvolvimento integrado (ou
IDE - Integrated Development Environment) para programação em R - e está
disponível para os sistemas operacionais Windows, macOS e Linux. Da
mesma maneira como em outras linguagens de programação, com o uso de IDE
no R você poderá gravar o seu trabalho em scripts. Estes podem ser
alterados a qualquer tempo, bem como, executados de maneira fácil, seja
parcialmente, seja integralmente. Isso é possível, pois um script é um
registro das análises que você realizou (um passo a passo). Em termos
técnicos, isso revela que a linguagem R é funcional: ela implementa
ações e análises a partir de funções (regras, comandos), ou seja,
algoritmos. Lembre que um algoritmo é uma sequência funcional de
comandos ou instruções, que devem ser realizados de maneira sistemática
para resolver um problema ou implementar de uma rotina qualquer. Então,
seu script é a roteirização de comandos que orienta o processamento da
máquina. Grosso modo: “Faça A, depois B. Se verdadeiro, execute C.” é um
exemplo de script.

E veja só, com isso você tem atendidos os **princípios fundamentais da
análise de dados**. A confiabilidade e a integridade das análises que
virá a fazer dependem da transparência, simplicidade, reprodutibilidade
e compreensão dos dados. Dito de outra maneira, o script é uma
peça-chave para tornar toda pesquisa **reprodutível**, na medida em que
confere: (1) a possibilidade de rastrear o passo a passo e diagnosticar
eventuais erros na pesquisa (transparência); (2) a capacidade de
qualquer pessoa chegar aos mesmos resultados, com o compartilhamento do
banco de dados, a partir do roteiro indicado; (3) a facilidade de
entender - e não ocultar! - o conteúdo da sua pesquisa e dos dados.

E se você acreditou que isso não se aplica ao setor privado, achou
errado! A reprodutibilidade é ainda mais exigida, seja para facilitar o
trabalho em grupo, seja para possibilitar o controle e a replicação de
resultados. A pesquisa acadêmica, neste caso, está mais atenta à
confiabilidade dos resultados alcançados.

## Comentando seu código!

Para trazer ainda maior facilidade ao seu projeto, o R aceita
comentários (partes que serão ignoradas pelo console) no seu código.
Basta que você use um hashtag *\#* antes do texto que deseja inserir
como comentário.

Noutras palvras, se uma linha de código R começar com o símbolo \#, ela
não é executada. Se uma linha de código começa com comandos e depois se
insere um hashtag, somente o conteúdo após o hastag será ignorado. Veja
os exemplos:

``` r
# Este código não será executado
UNIFESP <- c(1,2,3,4,5,6,7,8,9,10) # ; mean(UNIFESP)
UNIFESP
```

    ##  [1]  1  2  3  4  5  6  7  8  9 10

Tanto a primeira linha é um comentário, quanto o comando de cálculo de
média, na segunda linha, também é um comentário! Por isso, quando a
terceira linha do meu código pede para que o R exiba o objeto UNIFESP,
só aparecem os valores do conjunto - sem a média.

**Obs.** Documentar integra a arte de programar! Tenha isso em mente,
pois lhe garanto que você esquecerá o que fez no seu script em um tempo
menor do que imagina.

## Painéis do R Studio

Ao iniciar o ambiente pela primeira vez, você verá três grandes painéis:
Console (Console, Terminal), Global Enviroment (Enviroment, History e
Connections) e Outputs (Files, Plots, Packages, Help e Viewer). Haverá
um quarto painel que será seu primeiro Script!

Para isso, você tem dois caminhos: pelo caminho na barra de menus: File
\> New File \> R Script; ou direto no ícone com uma página em branco e
um “mais”(+) e, em seguida, R Script.

``` r
library(knitr)
knitr::include_graphics(path = "/home/vinicius/Área de Trabalho/Curso R - Tutoriais/rstudio-console.png")
```

![](rstudio-console.png)<!Tutoriais/rstudio-console.png>
![](joins.png)<!Tutoriais/joins.png>
Um último ponto: Veja que com o R Studio (IDE) você pode salvar seu
trabalho em scripts. Assim, poderá editá-los e, inclusive, salvá-los
como texto como faria em qualquer editor de textos. Ainda que o script
tenha extensão **.R**, será comum, num futuro próximo, que você escreva
seus códigos em blocos de notas **.txt** e depois atualize seu script -
ou vice-versa. Já o global enviroment pode ser salvo em formato
**.RData**. Por fim, os diferentes objetos criados poderão ser salvos em
formatos diversos ex. um gráfico em .jpeg; uma página em html; um
data-frame em .csv …

Pronto! Estamos preparados para começar a aprender a programar em R.
