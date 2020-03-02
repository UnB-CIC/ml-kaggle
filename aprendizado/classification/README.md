# Classificação

## Árvores de Decisão e Regressão

As [Árvores de Decisão](https://pt.wikipedia.org/wiki/%C3%81rvore_de_decis%C3%A3o) e Regressão são algoritmos supervisionados. O objetivo principal é induzir um modelo que seja capaz de predizer uma classe/rótulo/valor de uma variável resposta por meio do aprendizado de regras simples inferidas do conjunto de treinamento. Essas regras são geradas por meio da estratégia de [divisão e consquista](https://pt.wikipedia.org/wiki/Divis%C3%A3o_e_conquista) que recursivamente tende a diminuir a complexidade do problema tornando-o mais simples. A combinação dessas regras produz uma árvore capaz de gerar uma solução para o problema complexo. Os modelos em árvore são designados Árvores de Decisão (AD) para problemas de classificação e Árvores de Regressão (AR) para problemas de regressão.   

### Componentes de uma AD

Formalmente uma AD é um grafo acíclico direcionado em que cada nó é um nó de divisão ou um nó folha:

* **Nó de divisão:** Possui dois ou mais sucessores. Ele contém um teste condicional baseado nos valores dos atributos. Normalmente o teste é univariado, ou seja, em um único atributo. Exemplo: Idade > 18, Profissão &#8712; {professor, estudante}.

* **Nó folha:** É rotulado com uma função que considera valores da variável alvo dos exemplos que chegam na folha. Em uma AD de classificação podemos usar uma função de minimização de custo 0-1 como a moda. Em AR de regressão podemos usar uma função de minimização do erro médio quadrático ou desvio absoluto. Exemplo: média/mediana

### Uma AD genérica

A Figura a seguir representa uma AD e sua divisão no espaço para uma base de dados com dois atributos preditivos  (x<sub>1</sub> e x<sub>2</sub>). Cada nó da árvore corresponde a uma região nesse espaço. As regiões nos nós folhas são mutualmente excludentes e a junção de todas as regiões cobre todo o espaço definido pelos atributos. Os hiperplanos gerados são ortogonais aos eixos dos atributos testados e paralelo a todos os outros eixos. Todas as regiões são hiper-retângulos.

![](https://github.com/UnB-CIC/ml-kaggle/blob/master/aprendizado/classification/ad.png) *Exemplo de uma Árvore de Decisão. Adaptado de Katti Faceli et al., (2011)*

### Algoritmo

O algoritmo de AD é mostrado na Figura a seguir. A entrada para a função é o conjunto de treinamento **D** e sua saída é uma AD. Na sequencia o critério de parada é avaliado. Se mais divisões do conjunto de treinamento são necessárias, é escolhido um atributo que maximiza alguma medida de impureza. Na sequencia a função de geração da árvore é chamada recursivamente e aplicada a uma partição do conjunto de treinamento **D**.

![](https://github.com/UnB-CIC/ml-kaggle/blob/master/aprendizado/classification/ad_alg.png) *Algoritmo de uma Árvore de Decisão. Adaptado de Katti Faceli et al., (2011)*

É ressaltar que a geração de uma árvore minimal é um problema [NP-completo](https://pt.wikipedia.org/wiki/NP-completo). Os algoritmos exploram heurísticas que localmente executam pesquisa um passo a frente. Uma vez que uma decisão é tomanda ela nunca é desfeita. Isso pode gerar uma solução ótima localmente o que pode estar longe do [ótimo global](https://pt.wikipedia.org/wiki/Algoritmo_guloso). 

### Regras de Divisão para Classificação

Considere um nó *t* de divisão de uma AD em que a probabilidade de observar exemplos de classe c<sub>i</sub> é dado por p<sub>i</sub>. Portanto a probabilidade de observar todas as classes é p<sub>1</sub>,p<sub>2</sub>,...p<sub>n</sub> então a impureza sobre um nó *t* é uma função sobre a proporção da classe daquele nó <img src="https://render.githubusercontent.com/render/math?math=i(t) = \phi(p_1,p_2,...p_n)">. Portanto a redução de impureza gerado pela divisão S de um conjuntos de treinamento em dois subconjuntos L e R pode ser medida como:

<img src="https://render.githubusercontent.com/render/math?math=d(S) = \phi(p_1,p_2,...p_n) - P_L * \phi(p_{1L},p_{2L},...p_{nL}) - P_R * \phi(p_{1R},p_{2R},...p_{nR})">

Nessa equação P<sub>L</sub> e P<sub>R</sub> representam a probabilidade de um exemplo quando aplicado a regra de divisão pertencer ao subconjunto L ou R, respectivamente. 

A função de impureza apresentam caracteristicas gerais como: simetria, ter máximo quando <img src="https://render.githubusercontent.com/render/math?math=p_1 = p_2 = ... = p_n"> e ter um mínimo quando <img src="https://render.githubusercontent.com/render/math?math=p_i = 1">. Logo a proposta natural de uma AD deve tentar maximar a divisão dos subconjuntos que geram menor erro. Portanto uma divisão que mantém a proporção de classes em todo o subconjunto não tem utilizade e uma divisão em que cada subconjunto contém somente exemplos de uma classe tem utilizade máxima. Casos intermediarios são tratados de forma diferente por cada medida de impureza.

#### Entropia e Ganho de Informação

Existem diversas medidas de impureza como ganho de informação, entropia, distância, ângulo, qui-quadrado e etc. Nessa seção vamos abordar a entropia e ganho de informação, medidas base para o entendimento do algoritmo [C4.5](https://pt.wikipedia.org/wiki/Algoritmo_C4.5) proposto por Ross Quinlan em 1993. 

A entropia mede a aleatoriedade de uma variável aleatória em bits. Suponha uma variável aleatória A com domínio <img src="https://render.githubusercontent.com/render/math?math=a_1,a_2,...,a_v">. Suponha que a probabilidade de observar os valores são <img src="https://render.githubusercontent.com/render/math?math=p_1,p_2,...,p_v">. A entropis de A é calculada como:

<img src="https://render.githubusercontent.com/render/math?math=H(A) = -\sum_{i}p_i \ln p_i">

Em uma AD, entropia é usada para medir a aleatoriedade do atributo alvo. A cada nó de decisão da árvore, o atributo que mais reduz a aleatoriedade da variável alvo será escolhido para dividir os dados. O ganho de informação é medido em cada atributo para verificar o quanto eles reduzem a entropia do sistema. Portanto o ganho de informação é medido como a diferença da entropia do conjunto de dados e a soma ponderada da entropia das partições. 

Assumindo que temos um problema de classificação binária, ou seja, duas classes e que cada uma delas tenha *p* e *q* exemplos no conjunto de treinamento, respectivamente. Dessa forma podemos calcular a entropa das classes da seguinte forma:

<img src="https://render.githubusercontent.com/render/math?math=H(p,q) = -\frac{p}{p %2B q} \ln \frac{p}{p %2B q} - \frac{q}{p %2B q} \ln \frac{q}{p%2B q}">

Alem disso, essa base tem um atributo A com *v* categorias. Para calcular a entropia desse atributo precisamos considerar a entropia das partições, ou seja, a entropia de cada uma das *v* categorias. A seguinte equação representa a entropia das partições *p* e *q* do atributo A: 

<img src="https://render.githubusercontent.com/render/math?math=E(A,p,q) = \sum_{i=1}^{v}\frac{p_i %2B q_i}{p %2B q} H(p_i,q_i)">

Uma vez que sabemos a entropia do conjunto de dados e a entropia do atributo A, podemos calcular o ganho de informação por meio da diferença entre a entropia da base e a entropia das partições. A equação a seguir representa esse conceito: 

<img src="https://render.githubusercontent.com/render/math?math=IG(A,p,q) = H(p,q) - E(A,p,q)">

A heurística apresentada deve ser aplicada para todos atributos da base com o bojetivo de selecionar aquele que maximiza o ganho de infromação para aquele conjunto de dados. Como mensionado, normalmente os testes são realizados em atributos nominais e irá dividir os dados em tantos subconjuntos quantos os valores do atributo. 

### Exemplo Ilustrativo

O conjunto de dados *Jogar Tênis* é um problema de classificação binária aonde pretende-se classificar se uma pessoa deve ou não, dado certas condições climáticas, jogar tênis. Os atributos de entrada são o *Tempo*, *Temperatura*, *Umidade* e *Vento*. O conjunto tem 14 amostras de treinamento e a última coluna denominada *Joga* representa os rótulos jogar ou não tênis. Os atributos *Tempo* e *Vento* são categoricos e os atributos *Temperatura* e *Umidade* são contínuos.  

![](https://github.com/UnB-CIC/ml-kaggle/blob/master/aprendizado/classification/jogatenis.png) *Base de dados Jogar Tênis. Adaptado de Katti Faceli et al., (2011)*

Para construir uma AD precisamos descobrir o atributo que melhor discrimina as classes. Para isso precisamos calcular as probabilidades associadas de cada classe, a entropia do conjunto de treinamento, a entropia das partições e então estimar o ganho de informação de cada atributo. A seguir iremos calcular o ganho de informação do atributo *Tempo*.

**1⁰ Passo:** 

Probabilidade associada de cada classe:

<img src="https://render.githubusercontent.com/render/math?math=p(Joga = Sim) = \frac{9}{14}">
<img src="https://render.githubusercontent.com/render/math?math=p(Joga = Nao) = \frac{5}{14}">

Entropia da classe para todo o conjunto de treinamento:

<img src="https://render.githubusercontent.com/render/math?math=H(Joga) = - \frac{9}{14} * \ln \frac{9}{14} - \frac{5}{14} *  \ln \frac{5}{14} = 0.940 bit">

**2⁰ Passo:** 

Estimar a probabilidades de observar as classes dado cada categoria do atributo *Tempo*:

<img src="https://render.githubusercontent.com/render/math?math=p(Joga = Sim | Tempo = Ensolarado) = \frac{2}{5}">
<img src="https://render.githubusercontent.com/render/math?math=p(Joga = Nao | Tempo = Ensolarado) = \frac{3}{5}">
<img src="https://render.githubusercontent.com/render/math?math=H(Joga | Tempo = Ensolarado) = - \frac{2}{5} * \ln \frac{2}{5} - \frac{3}{5} * \ln \frac{3}{5} = 0.971 bit">

<img src="https://render.githubusercontent.com/render/math?math=p(Joga = Sim | Tempo = Nublado) = \frac{4}{4}">
<img src="https://render.githubusercontent.com/render/math?math=p(Joga = Nao | Tempo = Nublado) = \frac{0}{4}">
<img src="https://render.githubusercontent.com/render/math?math=H(Jogar | Tempo = Nublado) = - \frac{4}{4} * \ln \frac{4}{4} - \frac{0}{4} * \ln \frac{0}{4} = 0 bit">

<img src="https://render.githubusercontent.com/render/math?math=p(Joga = Sim | Tempo = Chuvoso) = \frac{3}{5}">
<img src="https://render.githubusercontent.com/render/math?math=p(Joga = Nao | Tempo = Chuvoso) = \frac{2}{5}">
<img src="https://render.githubusercontent.com/render/math?math=H(Jogar | Tempo = Chuvoso) = - \frac{3}{5} * \ln \frac{3}{5} - \frac{2}{5} * \ln \frac{2}{5} = 0.971 bit">

**3⁰ Passo:** Calcular a entropia ponderada para o atributo *Tempo*:

<img src="https://render.githubusercontent.com/render/math?math=H(Tempo) = \frac{5}{14} * 0.971 + \frac{4}{14} * 0 + \frac{5}{14} * 0.971 = 0.693 bit">

**4⁰ Passo:** Calcular o ganho de informação em dividir o conjunto de acordo com os valores do atributo *Tempo*:

<img src="https://render.githubusercontent.com/render/math?math=IG(Tempo) = H(Joga) - H(Joga|Tempo)">
<img src="https://render.githubusercontent.com/render/math?math=IG(Tempo) = 0.940 - 0.693 = 0.247 bit">

Uma vez que foi calculado o ganho de informação gerado pelo atributo *Tempo*, o mesmo precisa ser feito para o atributo *Vento*, *Temperatura* e *Umidade*. No caso dos dois últimos, como eles são atributos contínuos, alguma estratégia precisa ser utilizada para permitir a divisão desse atributo em partições. 

As estratégias mais utilizadas é a discretização ou a escolha de um ponto de corte binário. A discretização esta relacionada a transformação dos dados contínuos em categoricos por meio de estratégias como o [histograma](https://pt.wikipedia.org/wiki/Histograma) enquanto a escolha de um ponto de corte define um valor do conjunto de treinamento (normalmente utilizando uma função de mérito) que permite a construção de uma partição binária. Usualmente utiliza-se a segunda estratégia.

No exemplo da base *Jogar Tênis*, um ponto de corte interessante para o atributo *Temperatura* é o valor 70.5. Esse valor permite separar as amostrar em partições interessantes. A seguir os passos 2, 3 e 4 são repetidos:

**2⁰ Passo:** 

Estimar a probabilidades de observar as classes dado cada categoria do atributo *Temperatura*:

<img src="https://render.githubusercontent.com/render/math?math=p(Joga = Sim | Temperatura \leq 70.5) = \frac{4}{5}">
<img src="https://render.githubusercontent.com/render/math?math=p(Joga = Nao | Temperatura \leq 70.5) = \frac{1}{5}">
<img src="https://render.githubusercontent.com/render/math?math=H(Joga | Temperatura \leq 70.5) = - \frac{4}{5} * \ln \frac{4}{5} - \frac{1}{5} * \ln \frac{1}{5} = 0.721 bit">

<img src="https://render.githubusercontent.com/render/math?math=p(Joga = Sim | Temperatura > 70.5) = \frac{5}{9}">
<img src="https://render.githubusercontent.com/render/math?math=p(Joga = Nao | Temperatura > 70.5) = \frac{4}{9}">
<img src="https://render.githubusercontent.com/render/math?math=H(Joga | Temperatura = Ensolarado) = - \frac{5}{9} * \ln \frac{5}{9} - \frac{4}{9} * \ln \frac{4}{9} = 0.991 bit">

**3⁰ Passo:** Calcular a entropia ponderada para o atributo *Temperatura*:

<img src="https://render.githubusercontent.com/render/math?math=H(Temperatura) = \frac{5}{14} * 0.721 + \frac{9}{14} * 0.991 = 0.895 bit">

**4⁰ Passo:** Calcular o ganho de informação em dividir o conjunto de acordo com os valores do atributo *Temperatura*:

<img src="https://render.githubusercontent.com/render/math?math=IG(Temperatura) = H(Joga) - H(Joga|Temperatura)">
<img src="https://render.githubusercontent.com/render/math?math=IG(Temperatura) = 0.940 - 0.895 = 0.045 bit">

Sumarizando o ganho de informação para todos os atributos temos os seguintes valores:

<img src="https://render.githubusercontent.com/render/math?math=IG(Tempo) = 0.940 - 0.693 = 0.247 bit">
<img src="https://render.githubusercontent.com/render/math?math=IG(Temperatura) = 0.940 - 0.895 = 0.045 bit">
<img src="https://render.githubusercontent.com/render/math?math=IG(Umidade) = 0.940 - 0.789 = 0.151 bit">
<img src="https://render.githubusercontent.com/render/math?math=IG(Vento) = 0.940 - 0.892 = 0.048 bit">

Portanto podemos concluir que o atributo *Tempo* é que gera maior redução no ganho de informação. Logo o nó raiz da AD é composta pelo nó *Tempo* com 3 ramos, cada um relacionado a uma categoria desse atributo categórico (ensolarado, chuvoso e nublado). Como o algoritmo é baseado em dividir para conquistar, cada nó filho da árvore precisa ser construido baseado em sua partição dos dados. O processo se repete até que todos os nós sejam puros ou uma estratégia de poda seja aplicada.      

### Regras de Divisão para Regressão

A construção de uma AR é em tudo semelhante à construção de uma AD, tendo em conta a função de custo a minimizar que normalmente é o erro quadrático. Por esse motivo, a constante associada às folhas de uma AR é a média dos valores do atributo alvo dos exemplos de treinamento que caem em uma folha. A variância do atributo alvo é dado pela equação a seguir aonde **D** representa o conjunto de treinamento, *n* o número de exemplos, *y<sub>i</sub>* o valor do exemplo *i* e *y* o valor médio.

<img src="https://render.githubusercontent.com/render/math?math=sd(D,y) = \sqrt{\frac{1}{n} * \sum_{i=1}^{n} (y_i - y)^2}">
  
Para estimar o mérito de uma partição, a medida *Standard Deviation Reduction* (SDR) é bastante utilizada. Assumindo que o teste do atributo A verifica se ele é menor do que um determinado valor, os exemplos do conjunto **D** serão divididos em partições L e R de tamanhos n<sub>L</sub> e n<sub>R</sub>, respectivamente. Pode-se estimar a redução em variância obtida pela aplicação do teste como:

<img src="https://render.githubusercontent.com/render/math?math=SDR(S) = sd(D, y) - \frac{n_L}{n} * sd(L, y) - \frac{n_R}{n} * sd(R, y)">

Essa equação é aplicada para todos os atributos e todas as categorias ou pontos de corte escolhidos. Com isso podemos avaliar a redução da variância associada aos testes. Aquele teste que provocar maior redução será escolhido para compor a árvore.  

### Estratégia de poda

As estatísticas calculadas em nós mais razos em uma AD costumam ser os mais importantes enquanto estatísticas de nós mais profundos costumam ter níveis de importancia menores. Isso se dá porque os nós mais razos refletem os conceitos mais gerais enquanto os mais profundos os conceitos mais específicos e normalmente relacionados ao [super ajustamento](https://pt.wikipedia.org/wiki/Sobreajuste). O super ajustamento esta diretamente relacionado ao tamanho da árvore. Quanto maior, mais super ajustada e mais difícil de ser interpretada. Portanto, pordar uam árvore, que é trocar nós profundos por nós folhas, pode ajudar a minimizar esse problema.

A troca dos nós mais profundos por folhas pode causar a classificação erronea de alguns exemplos do conjunto de treinamento. Apensar de parecer contra-intuitivo, isso pode melhorar o desempenho para exemplos novos nunca antes vistos. Os métodos de poda mais conhecidos são: pré-poda e pós-poda. Enquanto a pré-poda é realizada durante a construção da árvore, a pós-poda é realizada depois da construção da árvore. 

## _Bootstrap_

## _Random Forest_

## _Boosting_

## _Gradient Boosting_

## _XGBoost_

## Redes Neurais Artificiais

### _Perceptron_

### _Perceptron_ Multicamadas

### Algoritmo _Backpropagation_
