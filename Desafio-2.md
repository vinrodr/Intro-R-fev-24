Desafio 2
================

## Instruções

Tente resolver o que se pede e registre todos os seus passos num
*script* ou em um documento RMarkdown. Comente o código para que suas
estretégias e opções estejam bem claras para você e outros no futuro.
Caso tenha encontrado uma solução em outro lugar, lembre-se de comentar
a autoria no comentário de seu código.

Lembre-se: Estou avaliando seu esforço e raciocínio - e não se conseguiu
cumprir tudo que se pediu. Dentro do possível, responderei com um
*feedback individual* para os *scripts* que enviarem. **Só será preciso
enviar o .RData, caso a base de dados não seja pública**.

## Tarefas

1.  Escolha uma base de dados pública [Dados Abertos da Prefeitura de
    São Paulo](http://dados.prefeitura.sp.gov.br/), [Microdados de
    pesquisas do
    IBGE](https://www.ibge.gov.br/estatisticas/downloads-estatisticas.html),
    [Dados Abertos do Governo Federal](https://dados.gov.br/home),
    [IpeaData](https://www.ipea.gov.br/portal/), [Dados
    Eleitorais](https://dadosabertos.tse.jus.br/organization/tse-agel)
    ou qualquer outro que seja de seu interesse. Baixe duas bases que
    permitam que você faça um *join* para trabalhar com variáveis
    diferentes.

2.  Se tiver dificuldade, deixei três bases da [Pesquisa de Perfil dos
    Municípios do IBGE de 2005](../Data) na pasta de arquivos do github
    do curso: munic1.csv; munic2.csv e munic3.csv. Deixei também um
    arquivo .zip, que tem uma planilha com todas as bases em sheets e o
    dicionário das variáveis na primeira sheet.

3.  Carregue as bases em seu *Global Environment* com alguma função de
    importação - caso tenha dificuldades com os caracteres, lembre-se de
    verificar o *Encoding* e/ou *delimitadores*.

4.  Escolha a(s) chave(s) identificadora(s) e execute um *join* dos seus
    bancos. Atenção para a classe da variável/coluna na hora de executar
    seu *join*.

5.  Faça a validação dos bancos com dois *anti_join()*, para verificar
    se há elementos da ‘tabela1’ que não estão na ‘tabela2’ e
    vice-versa. Caso o *anti_join()* traga elementos, verifique se há
    necessidade de colapsar em alguma medida resumo ou se é esperado que
    a informação da ‘tabela2’ seja aplicada igualmente para mais de uma
    linha da ‘tabela1’. Lembre-se: “tabela1 %\>% join(tabela2)”

6.  Se você teve problemas para unir seus bancos, talvez as perguntas
    abaixo ajudem: 6.1. Qual é a unidade de análise de cada banco? Se
    você usar *distinct()*, o número de linhas se mantêm o mesmo? 6.2.
    Qual(is) variável(is) identificam unicamente as unidades de análise
    de cada banco (chave/ID)?

7.  Se você tem muita informação, talvez seja melhor reduzir o número de
    variáveis. Deixando somente aqueles que você efetivamente irá
    trabalhar.

8.  Estabeleça alguns critérios para selecionar algumas observações.

9.  Produza um gráfico com 1 variável discreta.

10. Produza um gráfico com uma variável contínua.

11. Produza um gráfico com uma variável contínua e outra discreta.

12. Faça um gráfico de curva de densidade para uma variável contínua.
    Mas use outra variável como um atributo estético (color, fill,
    linetype …) para representar diferentes grupos.

13. Faça um gráfico qualquer usando *faced_grid()*.
