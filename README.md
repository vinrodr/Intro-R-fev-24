<h1 align="center"> Introdução à programação em R (fev-24) </h1>
<p align="center">
<img loading="lazy" src="http://img.shields.io/static/v1?label=STATUS&message=Primeira%20Oferta&color=GREEN&style=for-the-badge"/>
</p>
Curso de introdução à programação em R. Ofertado em modalidade extensionista no primeiro semestre de 2024, presencialmente no campus da Escola Paulista de Política, Economia e Negócios da Universidade Federal de São Paulo (EPPEN-UNIFESP).


> Exceto quando indicado diretamente, este trabalho está licenciado sob <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons BY-NC-SA 4.0</a>.

<h2 align="center"> Apresentação </h2> <p align="center">
  
O curso pretende oferecer uma iniciação à lógica de programação em linguagem R para os alunas(os) e comunidade UNIFESP. Em específico, propõe-se apresentá- las(los) e treiná-las(los) no uso de ferramentas computacionais para (i)coleta, (ii)organização, (iii) preparação e (iv) apresentação de dados. Neste sentido, não se trata de um curso de estatística, nem de metodologia, mas sim, de iniciação em uma linguagem de programação por meio do aprendizado de suas potencialidades na análise exploratória de dados.

Dentro desta perspectiva, o curso abordará desde o elementar da linguagem (instalação do software e reconhecimento do layout e suas opções) até aplicações mais complexas como a raspagem de dados da web e elaboração de mapas. De toda maneira, o foco está na “alfabetização” do participante na linguagem R (operações matemáticas, tipos de dados e objetos, operadores relacionais e lógicos, loops e funções) a partir da manipulação de dados em data-frames.

## Roteiro das aulas (tutoriais)
Obs. Tópicos 7 a 10 estão sujeitos a alteração.

[Encontro 1](Encontros/Encontro-1.md). (em [Rpubs](https://rpubs.com/vinrodr/encontro_1_introR_pubs)). Preparação do ambiente computacional: R e RStudio. Introdução à gramática R.

[Encontro 2](Encontros/Encontro-2.md). (em [Rpubs](https://rpubs.com/vinrodr/encontro_2_introR_pubs)). Introdução à gramática R: Vetores e objetos derivados. Operadores matemáticos, relacionais e lógicos.

[Encontro 3](Encontros/Encontro-3.md). (em [Rpubs](https://rpubs.com/vinrodr/encontro_3_introR_pubs)). Alfabetização em R base: Cláusulas condicionais, *loops* e funções.

[Encontro 4](Encontros/Encontro-4.md). (em [Rpubs](https://rpubs.com/vinrodr/encontro_4_introR_pubs)). O pacote Tidyverse: um novo mundo! Abrindo e manipulando dados. (I)

[Encontro 5](Encontros/Encontro-5.md). (em [Rpubs](https://rpubs.com/vinrodr/encontro_5_introR_pubs)). O pacote Tidyverse: Manipulação de data-frames em R  - Organizando, limpando e resumindo dados (II)

[Encontro 6](Encontros/Encontro-6.md). (em [Rpubs](https://rpubs.com/vinrodr/encontro_6_introR_pubs)). O pacote Tidyverse: Manipulação de data-frames em R  - Juntando bancos de dados (*joins*) (III)

[Encontro 7](). (em [Rpubs]()). O pacote Tidyverse: Tabelas (IV). Produção de relatórios com o pacote RMarkdown.

[Encontro 8](). (em [Rpubs]()). O pacote Tidyverse: Visualização de dados e o pacote ggplot2. (V)

[Encontro 9](). (em [Rpubs]()). Aplicações: Raspagem de dados na internet.

[Encontro 10](). (em [Rpubs]()). Aplicações: Soluções via API de terceiros (basedosdados).


## Referências bibliográficas

* Aquino, Jakson Alves de (2014). R para cientistas sociais. Editus.
* Navarro, Danielle; Pedersen, Thomas Lin e Wickham, Hadley (2009). ggplot2: Elegant Graphics for Data Analysis. Ed: Springer. Disponível [aqui](https://ggplot2-book.org/index.html)
* Guerra, Saulo; Oliveira, Paulo Felipe de e McDonnell, Robert (2018). Ciência de
dados com R: Uma Introdução. Disponível [aqui](https://cdr.ibpad.com.br/cdr-intro.pdf)
* Grolemund, Garrett (2014). Hands-On Programming with R. Ed: O'Reilly Media. Disponível [aqui](https://rstudio-education.github.io/hopr/)
* Imai, Kosuke (2017). Quantitative Social Science: An Introduction. Ed: Princeton University Press.
* Imai, Kosuke e Laudete, Elena (2023). Data analysis for social sciences: A friendly and practical approach. Ed: Princeton University Press.
* Silge, Julia e Robinson, David (2017). Text Mining with R: A Tidy Approach. Ed: O'Reilly Media. Disponível [aqui](https://www.tidytextmining.com/)
* Wichkam, Hadley e Grolemund, Garrett (2016). R for Data Science. Ed: O'Reilly Media. Disponível [aqui](https://www.tidytextmining.com/)
* Wichkam, Hadley (2014). Advanced R. Ed: Chapman and Hall/CRC. Disponível [aqui](http://adv-r.had.co.nz/)

## Atividades, tempo de dedicação e recomendações

> [!NOTE]
> É importante ressaltar que não há motivo para receios. Este curso foi pensado para pessoas que nunca programaram na vida, mas que desejam começar e têm curiosidade em conhecer todas as potencialidades da linguagem! Seja qual for sua origem acadêmica/profissional, **não há quaisquer pré-requisitos**. 

> [!NOTE]
> A cópia de códigos não é penalizada, **caso haja indicação de autoria**. Como ficará claro ao longo dos encontros, a atividade de programar funciona muito bem de maneira colaborativa e vale a Lei de Lavoisier "Na natureza (como na programação) nada se cria, nada se perde, tudo se transforma" (grifos nossos).

> [!TIP] 
> **Comentem seu código!**
> Em cada etapa de seu _script_ (e da análise de dados que ele irá processar) é importante observar os princípios da transparência e da reprodutibilidade. O que significa adotar práticas que tornem possíveis o rastreamento das origens de cada resultado e a identificação de eventuais erros. Na prática, isso quer dizer que digitamos o código da maneira mais clara e simples possível, além de comentar as escolhas e os pontos-chave do _script_. O console do R irá ignorar qualquer texto colocado na linha após um _hashtag_ (#), pois interpreta como um _não-comando_. (Além disso, o uso de comentários facilita na lembrança das escolhas que vocês tomaram na escrita. E, acreditem, vocês não irão se lembrar de algo que escreveram há poucos dias).

> [!IMPORTANT]
> Vocês verão que uma pequena quantidade de tempo é suficiente para acessar uma grande quantidade de aprendizado em R. As 40 horas propostas são suficientes para que a(o) participante supere a barreira de entrada na linguagem de programação, contudo é importante que haja algum esforço posterior extra-classe para fixação do aprendizado. Assim, ao final do calendário, cada participante estará apta(o) a aprimorar suas habilidades de maneira autônoma. E, por isso, precisará entregar um projeto final a ser escolhido por ajuste com o docente.
  
## Recursos úteis (Como obter ajuda?) 
* O grande livro do R - disponível [aqui](https://www.bigbookofr.com/index.html) - traz os links de mais de 150 livros tutoriais, que estão disponíveis gratuitamente online e tratam dos mais diferentes temas: de big data à arte, de economia a meio-ambiente. Favoritem, pois será muito útil para o desenvolvimento futuro e aprofundamento nas temáticas que lhes forem de interesse.
* _**Cheatsheets**_ são sínteses das principais funções de cada biblioteca. Serão grandes parceiras no início do aprendizado. Disponíveis [aqui](https://posit.co/resources/cheatsheets/).
* [Stack Overflow](https://stackoverflow.com/) será seu novo google. É um site de perguntas e respostas para programadores profissionais e entusiastas, onde você encontra resposta para qualquer dúvida que venha a ter - e caso não tenha ainda uma solução publicada, basta você copiar o erro no seu código ou escrever sua dúvida, que rapidamente terá alguém respondendo com uma solução. E bônus track! Não é somente para linguagem R, o Stack Overflow oferece soluções para Python, Julia, SQL, Excel ...
* "R Studio Help Menu" você acessa os chamados 'Vignettes', que são descrições condensadas e com exemplos de uso. Você pode acessá-los na aba HELP da janela inferior direita do RStudio, ou na própria linha de comando, colocando um ponto de interrogação antes do termo que deseja conhecer, por exemplo, ?mutate().
* A história completa da linguagem R está no artigo: ['A Brief History of S'](https://pdfs.semanticscholar.org/9b48/46f192aa37ca122cfabb1ed1b59866d8bfda.pdf). Sim, você não leu errado. O R deriva da linguagem S ...

## Desafios
Já que o curso propõe uma aprendizagem ativa dos participantes, o encerramento de cada tópico terá um desafio para que solucionem em duplas. Não haverá nota, mas a não entrega de quaisquer um dos desafios retira a certificação da(o) participante. 

[Desafio 1](Desafio-1.md). - Alfabetização em R base e conceitos iniciais em dplyr

[Desafio 2](). - Manipulação de dados, geração de gráficos e relatórios com tidyverse & RMarkdown

~~[Desafio 3](). - Visualização de dados e produção de gráficos com ggplot2~~

## Trabalho Final
Como um produto melhor acabado do esforço de cada participante e requisito da certificação, o projeto final será autoral. Recomendamos fortemente que ele faça sentido para seu próprio trabalho/pesquisa/estudo.
Igualmente aos desafios, não haverá nota. Mas a não entrega retira a certificação da(o) participante.
