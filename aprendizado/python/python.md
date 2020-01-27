# Python

## Preparação

A versão padrão é [Python 3](https://www.python.org/). Assume-se que o sistema operacional é Unix.

```bash
sudo apt install python3 python3-pip
sudo pip3 install matplotlib pandas scikit-learn seaborn
```

## Python

A [documentação](https://docs.python.org/3/) é bem extensa, e o melhor lugar para inicial é o [tutorial](https://docs.python.org/pt-br/3/tutorial/index.html). O [guia para iniciantes](https://wiki.python.org/moin/BeginnersGuide) (também [em Português](https://wiki.python.org/moin/PortugueseLanguage)) é outra fonte de recursos excelente.

### Diferenças Básicas ([para C](https://wiki.python.org.br/ProgramadoresCaprendendoPython))

Python é uma linguagem mais nova ([interpretada](https://pt.stackoverflow.com/a/77088)), que foi projetada com ênfase no esforço do programador sobre o esforço computacional, priorizando a legibilidade do código sobre a velocidade ou expressividade.

* Escopos são definidos pela [identação](https://pt.wikibooks.org/wiki/Python/Conceitos_b%C3%A1sicos/Indenta%C3%A7%C3%A3o).
* [Duck Typing](https://pt.wikipedia.org/wiki/Duck_typing) define a variável, e leva a uma abordagem de que [é mais fácil pedir perdão do que pedir permissão](http://aprenda-python.blogspot.com/2016/04/pedir-permissao-ou-pedir-perdao.html).
* Expressões booleanas também consideram valores _[truthy/falsy](https://docs.python.org/pt-br/3/library/stdtypes.html)_ ([mais detalhes](https://www.freecodecamp.org/news/truthy-and-falsy-values-in-python/)).
* C trabalha com variáveis (em "endereços"), Python com [objetos](https://docs.python.org/pt-br/3/reference/datamodel.html) (em "referências").
* Python gerencia a memória [automaticamente](https://wiki.python.org.br/FuncionamentoGarbageCollector).

### Estruturas de Dados

É importante entender o conceito de [imutabilidade](https://docs.python.org/pt-br/3/glossary.html#term-immutable). Números e strings têm comportamento similar a C, mas com algumas diferenças. [Inteiros](https://docs.python.org/pt-br/3/library/stdtypes.html#typesnumeric) têm precisão arbitrária (e ocupam quanto espaço for necessário/disponível). Reais são sempre armazenados no padrão [IEEE 754 de dupla precisão](https://docs.python.org/pt-br/3/tutorial/floatingpoint.html).

Algumas [estruturas de dados](https://docs.python.org/pt-br/3/tutorial/datastructures.html) são mais interessantes.

* [Listas](https://docs.python.org/pt-br/3/tutorial/introduction.html#lists) funcionam como vetores, mas podem armazenar elementos de tipos distintos. O _[slicing](https://docs.python.org/3/tutorial/introduction.html#strings)_ permite a manipulação de pedaços da lista com facilidade. São _[mutáveis](https://docs.python.org/pt-br/3/glossary.html#term-mutable)_.
* [Tuplas](https://docs.python.org/pt-br/3/tutorial/datastructures.html#tuples-and-sequences) também são sequências ordenadas de elementos (possivelmente heterogêneos), mas são _imutáveis_.
* [Conjuntos](https://docs.python.org/pt-br/3/tutorial/datastructures.html#sets) armazenam elementos únicos de forma bastante eficiente.
* [Dicionários](https://docs.python.org/pt-br/3/tutorial/datastructures.html#dictionaries) definem um par chave:valor, mapeando os elementos (valores) por meio de chaves (não necessariamente numéricas).

* [Machine Learning in Python](https://www.springboard.com/resources/learning-paths/machine-learning-python/)

## Pandas

[Pandas](https://pandas.pydata.org/) fornece implementações eficientes de estruturas de dados, especialmente [séries](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.html#pandas.Series) e [dataframes](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html#pandas.DataFrame). A [documentação](https://pandas.pydata.org/pandas-docs/stable/) é bem completa, e pode-se ter boas noções em apenas [10 minutos](https://pandas.pydata.org/pandas-docs/stable/getting_started/10min.html).

* [How NOT to write pandas code](https://towardsdatascience.com/how-not-to-write-pandas-code-ef88599c6e8f)

## Matplotlib e Seaborn

A [matplotlib](https://matplotlib.org/) é uma biblioteca para gerar gráficos 2D, e é a base da biblioteca [seaborn](https://seaborn.pydata.org/) (as diferenças são ilustradas [aqui](https://www.kdnuggets.com/2019/04/data-visualization-python-matplotlib-seaborn.html)).

* [Make your Data Talk!](https://towardsdatascience.com/make-your-data-talk-13072f84eeac).
* [Intermediate Python for Data Science](https://www.datacamp.com/courses/intermediate-python-for-data-science) (Data Camp)
* [Python Seaborn Tutorial For Beginners](https://www.datacamp.com/community/tutorials/seaborn-python-tutorial) (Data Camp)
* [PythonDataScienceHandbook](https://jakevdp.github.io/PythonDataScienceHandbook/04.14-visualization-with-seaborn.html)

## SKLearn

O [scikit-learn](https://scikit-learn.org/stable/) é uma das bibliotecas mais utilizadas para aplicações de aprendizagem de máquina.
