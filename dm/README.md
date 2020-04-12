# Mineração de Dados

A etapa de Mineração de Dados engloba a preparação, a análise estatística e o pré-processamento dos dados. Alguns estudos apontam que essas etapas juntas representam 60% de todo o tempo gasto até a indução dos modelos de AM. Outros estudos também  apontam que um pré-processamento adequado é fundamental para a indução dos algoritmos de AM de forma eficiente. As seções seguintes irão abordar essas etapas.   
   
## Preparação e Análise dos Dados

A preparação e análise dos dados é uma etapa fundamental da tarefa de AM. Ela permite que informações valiosas como a descoberta de padrões e tendências nos padrões que geraram os dados. Algumas podem ser obtidas por meio de fórmulas estatísticas e outras por meio de técnicas de visualização dos dados.

### Conjuntos de Dados

Um conjunto de dados são formados por **amostras** ou **objetos** físicos ou abstratos. Cada objeto é descrito por um conjunto de **atributo de entrada** ou  **atributo preditivo** ou **vetor e característica**. Cada objeto corresponde a uma ocorrência desses dados. Cada atributo esta relacionado a uma propriedade do objeto. Em bases supervisionadas, o conjunto de dados tem um atributo especial chamado de **atributo de saída** ou **rótulo**. Esse atributo de saída pode ser contínuo ou discreto. Quando contínuo, dizemos que esse conjunto de dados é de regressão e quando discreto, de classificação.

Formalmente esse conjunto de dados é representado por uma matriz <img src="https://render.githubusercontent.com/render/math?math=X_{nxd}"/> onde *n* é o número de objetos e *d* é o número de atributos de entrada. Os rótulos são um vetor <img src="https://render.githubusercontent.com/render/math?math=y = \{c_1, c_2,...c_l \}"/> onde <img src="https://render.githubusercontent.com/render/math?math=c_l"/> representa os *l* atributos de saída da base de dados. Cada elemento dessa matriz <img src="https://render.githubusercontent.com/render/math?math=x^{j}_{i}"/> contém o valor da j-ésima característica para o i-ésimo objeto. Também podemos representar os *d* atributos como eixos ortogonais, os objetos como pontos no espaço de dimensão *d* e os rótulos como formato ou cor desses pontos.  

Apesar do crescente número de bases disponíveis, na maioria das vezes não é possível aplicar os algoritmos de AM de forma direta. Portanto, uma etapa anterior de análise dos dados e outra de pré-processamento são fundamentais. Enquanto a análise permite entender os dados que serão tratados, a etapa de pré-processamento permite a integração dos dados de diferentes fontes em estrutura em forma de matriz, a eliminação de atributos irrelevantes que não representam informações relacionadas ao contexto, o balanceamento das amostras para tornar a base mais uniforme, a presença de ruído, dados incosistentes e a transformação são outros problemas. 

### Análise dos Dados

O conjunto de dados *Jogar Tênis* é um problema de classificação aonde pretende-se classificar se uma pessoa deve ou não, dado certas condições climáticas, jogar tênis. Nessa base de dados, <img src="https://render.githubusercontent.com/render/math?math=X_{nxd}"/> o valor *n* é 14 e o valor de *d* é 4. Como é uma supervisionada com rótulos discretos, ela apresenta um rótulos são um vetor <img src="https://render.githubusercontent.com/render/math?math=y = \{c_1, c_2, ... c_l\}"/> com *l* igual a 2. Cada linha representa uma amostra/dado/objeto e cada coluna/variável/atributo uma característica relacionada a essa amostra. Os atributos de entrada são o *Tempo*, *Temperatura*, *Umidade* e *Vento*. A última coluna denominada *Joga* representa os rótulos jogar ou não tênis.

![](jogatenis.png) 
*Base de dados Jogar Tênis. Adaptado de Katti Faceli et al., (2011)*

Os valores que os [atributos/variáveis](https://pt.wikipedia.org/wiki/Vari%C3%A1vel_(estat%C3%ADstica)) podem assumir são definidos de diferentes formas. Uma delas é usar a definição de tipo e escala. Enquanto o [tipo](https://pt.wikipedia.org/wiki/Vari%C3%A1vel_(estat%C3%ADstica)) do atributo diz respeito ao grau de quantização nos dados, a [escala](https://pt.wikipedia.org/wiki/Escala_(estat%C3%ADstica)) indica a significância relativa dos valores. O tipo pode ser quantitativo/numérico e qualitativo/simbólico/categórico e a escala pode ser nominais, ordinais, intervalares e racionais. 

Os valores quantitativos/numéricos podem ser contínuos ou discretos mas, frequentemente representados por valores reais e apresentam alguma medida associada. Os atributos qualitativos/simbólicos/categóricos apresentam um número finito de categorias. Alguns atributos qualitativos podem apresentar ordem mas esse caso específico é muitas vezes desencorajado nas bibliotecas de AM. Além disso, esse tipo de dado não aceita operações aritméticas.  

A escala define as operações que podem ser realizadas sobre os valores dos atributos. Enquanto a escala nominal e ordinal são do tipo qualitativo, a escala intervalar e racional é do tipo quantitativo. A escala nominal é apresentada por nomes diferentes. As operações permitidas são de igualdade e diferença. Os valores ordinais, além das operações de igualdade e diferença, também apresentam ordem. Nesse caso podemos verificar se um determinando categoria é maior/superior, menor/inferior ou igual. A escala intervar são números que variam dentro de um intervalo. Nesse caso, é possível diferenciar a ordem e a diferença entre dois valores. Os atributos com escala racional são os mais informativos. Nesse caso, existe um zero absoluto junto com uma unidade de medida de forma que a razão tenha significado.  

Dessa forma podemos classificar os atributos da base de dados *Jogar Tênis* da seguinte forma:

* Tempo: Qualitativo nominal, porque apresenta as categorias chuvoso, ensolarado e nublado que não apresentam ordem;
* Temperatura: Quantitativo intervalar, porque apresenta valores numéricos de temperatura na escala Fahrenheit;
* Umidade: Quantitativo racional, porque apresenta valores numéricos de temperatura na escala de porcentagem, ou seja, temos um zero absoluto;
* Vento: Qualitativo nominal, porque apresenta as categorias sim e não, que não apresentam ordem. 

### Estatística Descritiva

A estatística descritiva resume de forma quantitativa as principais características de um conjunto de dados. Elas assumem que os dados foram gerados por algum processo estocástico. Ou seja, se os dados respeitam uma distribuição normal com média zero e variância 1, essas medidas podem facilmente capturar essa informação. Essas medidas ainda podem ser univariadas ou multivariadas.

#### Univariadas

* Medidas de localidade: [média](https://pt.wikipedia.org/wiki/M%C3%A9dia), [mediana](https://pt.wikipedia.org/wiki/Mediana), intervalo, [desvio padrão](https://pt.wikipedia.org/wiki/Desvio_padr%C3%A3o), [variância](https://pt.wikipedia.org/wiki/Vari%C3%A2ncia), etc.
* Medidas de distribuição: momento, [obliquidade](https://pt.wikipedia.org/wiki/Assimetria_(estat%C3%ADstica)), [curtose](https://pt.wikipedia.org/wiki/Curtose), etc.

#### Multivariadas

* [Covariância](https://pt.wikipedia.org/wiki/Covari%C3%A2ncia), [correlação](https://pt.wikipedia.org/wiki/Correla%C3%A7%C3%A3o), etc.

## Pré-processamento dos Dados

Técnicas de pré-processamento são comumente utilizadas para melhorar a qualidade dos dados por meio da eliminação ou minimização de problemas como os ruídos, as imperfeições, os valores incorretos ou consistentes e os valores ausentes. Além disso, algumas bases podem apresentar alta dimensionalidade ou um número muito grande de amostras o que também pode ser corrigido com técnicas de pré-processamento. 

### Eliminação Manual de Atributos

Os atributos são considerados irrelevantes quando eles não contribuem para a estimativa do valor do atributo alvo. Por exemplo, considere a base de dados *Jogar Tênis*. Se tivessemos os atributos *nome* e *ID* de cada jogador, esses atributos não ajudariam a predizer se alguém deve ou não jogar tênis. Portanto, são atributos irrelevantes. Essa análise é manual, no entanto. não pode ser desconsiderada. Outros exemplos de atributos irrelevantes são aqueles que apresentam valores constantes para todas as amostras ou apresentam pouca variação.

### Amostragem dos Dados

Alguns algoritmos de AM têm dificuldade de lidar com um número muito grande de amostras. Esse é o exemplo do algoritmo *k*-vizinhos mais próximos (*k*NN). Esse algoritmo precisa calcular a distância entre todos os exemplos. Na sequência ele utiliza os *k* vizinhos mais próximos das amostras de teste para realizar a predição das classes. Esse processo de aprendizado, dependendo do tamanho da base, pode necessitar de muita memória e ter um alto custo computacional.

Além disso, existe um balanço entre custo computacional e acurácia. Quanto mais dados utilizados maior tende a ser a taxa de acerto (matemáticamente comprovado) e menor a eficiência computacional no processo de indução dos modelos. Para se obter um bom compromisso entre taxa de acerto e custo computacional, é comum trabalhar com uma amostra do conjunto de treinamento. No entanto, é importante ressaltar que amostras diferentes podem gerar modelos e taxas de acerto diferentes. Quando a amostra respeita a distribuição estatística dos dados originais, essa variação na taxa de acerto pode diminuir. Com isso, seria possível fornecer uma estimativa da informação continda na população original, permitindo tirar conclusões do todo a partir de uma parte dos dados. Exemplos de amostragens:

* Amostragem aleátoria simples (com e sem reposição);
* Amostragem estratificada;
* Amostragem progressiva. 

### Incompletos

Ausência de valores em alguma amostra ou atributo é um problema comum nas bases de dados. Dependendo do problema, a taxa de valores ausentes pode ser maior do que taxa de valores presentes. Normalmente, esses valores ausentes são marcados nas bases de dados por *NULL*, *NA* ou *-*. A origem desses valores ausentes pode ser diversa: o atributo não foi consderado importante para aquela amostra, desconhecimento do valor, erro de preenchimento ou inexistência de valor.

Existem diversas formas de tratar esses valores ausentes: (1) a mais simples é eliminar os objetos ou atributo com valores ausentes. Essa técnica não é indicada quando a eliminação irá impactar muitas amostras ou muitos atributos da base de dados; (2) outra alternativa é preencher os valores ausentes usando alguma heurística como a média, moda e mediana daquele atributo separado por classe ou para todas as amostras; e (3) utilizando como heurística algoritmos de AM para o preenchimento.

Nessa última abordagem que utiliza algoritmos de AM como heurística para o preenchimento de valores ausentes, uma possível solução seria utilizar o algoritmo *k*NN para indicar o valor mais frequente das *k* amostras mais semelhantes daquele com valor ausente a ser estimado. Nesse caso, o atributo alvo poderia ser utilizado como se fosse um atributo preditivo e o atributo com valor ausente o atributo alvo ou aquele a ser estimado.

### Redudantes

As bases de dados podem apresentar tanto amostras quanto atributos redundantes. Uma amostras ou atributo é classificado como redundante quando eles apresentam outra amostra ou atributo muito semelhante ao original. Normalmente, esse tipo de problema é causado durante a fase de coleta ou integração dos dados. O impacto deles durante o processo de indução vai depender do algoritmo de AM, mas, no geral, podemos dizer que pode ocorrer interferência. Essa interferência normalmente está associada a um peso ou importância maior a amostra ou atributo redudante contribuindo mais no modelo final. 

O algoritmo *k*NN por exemplo, é muito influenciado por ambos, amostras e atributos redundantes. As amostras redundantes podem causar uma classificação errônea de um exemplo por conta dos *k* vizinhos mais próximos enquanto o atributo redundante pode dar peso maior para uma informação específica da base de dados durante o cálculo da matriz de distância. Além disso, o tempo de indução pode aumentar e, em alguns casos, gerar a perda de desempenho. 

A remoção de amostras duplicadas normalmente é feita de forma simples através da remoção das amostras que apresentam o mesmo valor. A remoção de atributos redundantes pode ser feita de diversas formas: comparação, [correlação](https://pt.wikipedia.org/wiki/Correla%C3%A7%C3%A3o) e [seleção de atributos](https://en.wikipedia.org/wiki/Feature_selection). Se dois atributos são altamente correlacionados, é possível que estejam representando a mesma informação. A seleção de atributos utiliza alguma técnica específica como CFS, CIFE e técnicas de empacotamento.   

### Desbalanceamento

O desbalanceamento de uma base de dados de classificação pode ser medido extraindo a porcentagem de amostras que temos para cada rótulo/classe da base. Se ocorrer uma disparidade entre as classes podemos dizer que ela é desbalanceada. Quanto maior essa disparidade entre as classes, mais desbalanceada ela é e maior deve ser o efeito causado nos modelos induzidos nessas bases de dados, principalmente para as classes com menor número de amostras. 

Uma forma bem simples de medir o efeito causado é verificar a taxa de acerto dos modelos. Em uma base de classificação binária (com dois rótulos), caso a taxa de acerto seja inferior ou igual a classe majoritária, é possível afirmar que os modelos não estão aprendendo nenhum conceito relevante. Já em uma base multiclasse (com dois ou mais rótulos) é possível utilizar medidas de avaliação mais interessantes como a taxa de acerto por classe ou a média geométrica para avaliar se os modelos induzidos estão generalizando para todas as classes. 

Existem diversas formas de tratar esse problema. As mais comuns são aquelas que procuram balancear artificialmente o conjunto de dados: (1) redefinindo o tamanho do conjunto de dados por acréscimo ou eliminação; (2) utilizando diferentes custos de classificação para as classes durante o processo de indução do algoritmo de AM e (3) induzindo um modelo específico de AM capaz de induzir modelos para uma única classe. Dentre as alternativas o mais comuns temos trabalhar nos dados (1) e alterar os pesos das amostras (2).

* Técnicas de acréscimo/eliminação da classe minoritária/majoritária:
   * [SMOTE, Bordeline-SMOTE, ADASYN, Random Oversampling e Undersampling](https://en.wikipedia.org/wiki/Oversampling_and_undersampling_in_data_analysis)

* Utilizando custos de classificação:
   * [SVM](https://scikit-learn.org/stable/auto_examples/svm/plot_weighted_samples.html), RNA *k*NN, e etc.

* Algoritmos de classificação de uma classe:
   * [One-class SVM](https://scikit-learn.org/stable/modules/generated/sklearn.svm.OneClassSVM.html)

### Redução de Dimensionalidade

Muitas bases de dados apresentam um número elevado de atributos preditivos. Exemplos de bases assim são as de expressão gênica e as de imagens. No caso das bases de expressão gênica, cada atributo pode estar relacionado a um alelo ou gene o que naturalmente pode escalar a milhares deles quando tentamos classificar uma determina doença. O mesmo acontece com as bases de imagens. Nesse caso, cada pixel pode representar um atributo e em uma imagem pequena como 256 x 256 teríamos 65536 atributos. No entanto, somente algumas técnicas de AM conseguem lidar bem com esse alto número de atributos. Esse problema é descrito na literatura como o problema da maldição da dimensionalidade. 

Existem diversas formas de reduzir a dimensionalidade na etapa de pré-processamento. A Agregação e Seleção de atributos são as formas mais comuns. Enquanto as técnicas de agregação substituem os atributos originais por novos atributos formados pela combinação de grupos desses, as técnicas de seleção mantêm uma parte dos atributos originais e descarta os demais. Nesse último é comum ainda separar a classificação em baseada em filtro e baseada em *wrapper*. Enquanto as técnicas baseadas em filtro fazem uso de alguma medida estatística para a seleção dos atributos, a baseada em *wrapper* utiliza o próprio algoritmo de AM para uma seleção caixa-preta. Essa seleção normalmente é guiada por alguma estratégia de busca como *backward generalization* ou *forward generalization*.    

Seguem alguns exemplos de técnicas:

* Agregação dos Atributos
  * [Análise de Componentes Principais (PCA)](https://en.wikipedia.org/wiki/Principal_component_analysis)

* Seleção dos Atributos baseada em Filtro
  * [CFS, CIFE, etc.](https://en.wikipedia.org/wiki/Feature_selection#Filter_method)

* Seleção dos Atributos baseada em *wrapper*
  * [RFE](https://en.wikipedia.org/wiki/Feature_selection#Wrapper_method)

### Transformação dos Dados

A transformação das bases de dados é um requisito fundamental no uso das técnicas de AM. Muitas dessas técnicas lidam somente com valores numéricos e outras somente com valores categóricos. Algumas delas são influenciadas pelo intervalo dos atributos numéricos exigindo a normalização dos dados. Portanto, é importante utilizar técnicas que sejam capazes de transformar os dados da melhor forma possível.

A conversão simbólico-numérico é necessária quando a base de dados apresenta atributos categóricos e as técnicas que pretende utilizar são as RNA e Máquinas de Vetores Suporte (SVM). Se o atributo categórico assume somente dois valores, a transformação natural é substituir os valores por zeros e uns. Para um atributo categórico com mais de dois valores, uma transformação bastante utilizada é a *c*-bits, onde *c* representa o número de categorias.    

O conjunto de dados *Jogar Tênis* é um problema de classificação binária em que pretende-se classificar se uma pessoa deve ou não, dado certas condições climáticas, jogar tênis. Um dos atributos dessa base é o *Tempo* com as categorias *Ensolarado*, *Nublado* e *Chuvoso*.  Utilizando a codificação *c*-bits, temos que *c* é 3 e portanto precisamos de 3 atributos numéricos para codificar esse atributo categórico. Assim, podemos codificar *Ensolarado* como "1,0,0", *Nublado* como "0,1,0" e *Chuvoso* como "0,0,1". Calculado a distância entre esses pontos, percebemos que eles são equidistantes. Caso exista relação de ordem entre as categorias, por exemplo dias da semana, podemos usar valores inteiros ou reais ordenados para representar essas informações. 

Algumas vezes um valor numérico de um atributo precisa ser transformado em outro valor numérico. Isso normalmente acontece quando os valores superiores e inferiores entre os atributos são muito distintos. O objetivo principal é evitar  que um atributo predomine sobre outro. Essa transformação é chamada de normalização.

A normalização por amplitude é a mais utilizada. Ela se baseia na reescala ou padronização. Enquanto a reescala utiliza os valores máximos e mínimos, a padronização usa a média e o desvio padrão. Ambas são aplicadas isoladamente em cada atributo da base de dados. Enquanto a reescala normaliza os valores máximos e mínimos de cada atributo entre 0 e 1, a padronização mantém a média em 0 e o desvio padrão em 1. 

Assumindo que uma base de dados é representado por uma matriz <img src="https://render.githubusercontent.com/render/math?math=X_{nxd}"/> onde *n* é o número de objetos e *d* é o número de atributos de entrada e <img src="https://render.githubusercontent.com/render/math?math=x^j"/> é o atributo *j* da base, então temos:

* Reescala:
<img src="https://render.githubusercontent.com/render/math?math=x^j = \frac{x^j - min(x^j)}{max(x^j) - min(x^j)}"/>

* Padronização:
<img src="https://render.githubusercontent.com/render/math?math=x^j = \frac{x^j - mean(x^j)}{sd(x^j)}"/>

