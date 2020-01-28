# Classificação

## Árvores de Decisão e Regressão

As Árvores de Decisão e Regressão são algoritmos supervisionados. O objetivo principal é induzir um modelo que seja capaz de predizer uma classe/rótulo/valor de uma variável resposta por meio do aprendizado de regras simples inferidas do conjunto de treinamento. Essas regras são geradas por meio da estratégia de devisão e consquista que recursivamente tende a diminuir a complexidade do problema tornando-o mais simples. A combinação dessas regras produz uma árvore capaz de gerar uma solução para o problema complexo. Os modelos em árvore são designados Árvores de Decisão (AD) para problemas de classificação e Árvores de Regressão (AR) para problemas de regressão.   

### Componentes de uma AD

Formalmente uma AD é um grafo acíclico direcionado em que cada nó é um nó de divisão ou um nó folha:

* **Nó de divisão:** Possui dois ou mais sucessores. Ele contém um teste condicional baseado nos valores dos atributos. Normalmente o teste é univariado, ou seja, em um único atributo. Exemplo: Idade > 18, Profissão &#8712; {professor, estudante}, 0.3 + 0.2x – 0.5x² &#8804; 0

* **Nó folha:** É rotulado com uma função que considera valores da variável alvo dos exemplos que chegam na folha. Em uma AD de classificação podemos usar uma função de minimização de custo 0-1 como a moda. Em AR de regressão podemos usar uma função de minimização do erro médio quadrático ou desvio absoluto. Exemplo: média/mediana

### Uma AD genérica

A Figura a seguir representa uma AD e sua divisão no espaço para uma base de dados com dois atributos preditivos  (x<sub>1</sub> e x<sub>2</sub>). Cada nó da árvore corresponde a uma região nesse espaço. As regiões nos nós folhas são mutualmente excludentes e a junção de todas as regiões cobre todo o espaço definido pelos atributos. Os hiperplanos gerados são ortogonais aos eixos dos atributos testados e parapelo a todos os outros eixos. Todas as regiões são hiper-retângulos.

![](https://github.com/UnB-CIC/ml-kaggle/blob/master/aprendizado/classification/ad.png) *Exemplo de uma Árvore de Decisão. Adaptado de Katti Faceli et al., (2011)*

### Algoritmo

O algoritmo de AD é mostrado na Figura a seguir. A entrada para a função é o conjunto de treinamento **D** e sua saída é uma AD. Na sequencia o critério de parada é avaliado. Se mais divisões do conjunto de treinamento são necessárias, é escolhido um atributo que maximiza alguma medida de impureza. Na sequencia a função de geração da árvore é chamada recursivamente e aplicada a uma partição do conjunto de treinamento **D**.

![](https://github.com/UnB-CIC/ml-kaggle/blob/master/aprendizado/classification/ad_alg.png) *Algoritmo de uma Árvore de Decisão. Adaptado de Katti Faceli et al., (2011)*

É importante dizer que a geração de uma árvore minimal é um problema NP-completo. Os algoritmos exploram heurísticas que localmente executam pesquisa um passo a frente. Uma vez que uma decisão é tomanda ela nunca é desfeita. Isso pode gerar uma solução ótima localmente o que pode estar longe do ótimo global. 

### Regras de divisão para classificação

Considere um nó *t* de divisão de uma AD em que a probabilidade de observar exemplos de classe c<sub>i</sub> é dado por p<sub>i</sub>. Portanto a probabilidade de observar todas as classes é p<sub>1</sub>,p<sub>2</sub>,...p<sub>n</sub> então a impureza sobre um nó *t* é uma função sobre a proporção da classe daquele nó <img src="https://render.githubusercontent.com/render/math?math=i(t) = o(p_1,p_2,...p_n)">. Portanto a redução de impureza gerado pela divisão S de um conjuntos de treinamento em dois subconjuntos L e R pode ser medida como:

<img src="https://render.githubusercontent.com/render/math?math=d(S) = o(p_1,p_2,...p_n) - P_L * o(p_{1L},p_{2L},...p_{nL}) - P_R * o(p_{1R},p_{2R},...p_{nR})">

Nessa equação P<sub>L</sub> e P<sub>R</sub> representam a probabilidade de um exemplo quando aplicado a regra de divisão pertencer ao subconjunto L ou R, respectivamente. 

A função de impureza apresentam caracteristicas gerais como: simetria, ter máximo quando <img src="https://render.githubusercontent.com/render/math?math=p_1 = p_2 = ... = p_n"> e ter um mínimo quando <img src="https://render.githubusercontent.com/render/math?math=p_i = 1">. Logo a proposta natural de uma AD deve tentar maximar a divisão dos subconjuntos que geram menor erro. Portanto uma divisão que mantém a proporção de classes em todo o subconjunto não tem utilizade e uma divisão em que cada subconjunto contém somente exemplos de uma classe tem utilizade máxima. Casos intermediarios são tratados de forma diferente por cada medida de impureza.

#### Entropia e Ganho de Informação

Existem diversas medidas de impureza como ganho de informação, entropia, distância, ângulo, qui-quadrado e etc. Nessa seção vamos abordar a entropia e ganho de informação, medidas base para o entendimento do algoritmo C4.5 proposto por Quinlan (1993). 

A entropia mede a aleatoriedade de uma variável aleatória em bits. Suponha uma variável aleatória A com domínio <img src="https://render.githubusercontent.com/render/math?math=a_1,a_2,...,a_v">. Suponha que a probabilidade de observar os valores são <img src="https://render.githubusercontent.com/render/math?math=p_1,p_2,...,p_v">. A entropis de A é calculada como:

<img src="https://render.githubusercontent.com/render/math?math=H(A) = -\sum_{i}p_i \ln p_i">

Em uma AD, entropia é usada para medir a aleatoriedade do atributo alvo. A cada nó de decisão da árvore, o atributo que mais reduz a aleatoriedade da variável alvo será escolhido para dividir os dados. O ganho de informação é medido em cada atributo para verificar o quanto eles reduzem a entropia do sistema. Portanto o ganho de informação é medido como a diferença da entropia do conjunto de dados e a soma ponderada da entropia das partições. 

<img src="https://render.githubusercontent.com/render/math?math=H(p,q) = -\frac{p}{p %2B q} \ln \frac{p}{p %2B q} - \frac{q}{p %2B q} \ln \frac{q}{ p%2B q}">
<img src="https://render.githubusercontent.com/render/math?math=E(A,p,q) = \sum_{i=1}^{v}\frac{p_i %2B q_i}{p %2B q} H(p_i,q_i)">
<img src="https://render.githubusercontent.com/render/math?math=IG(A,p,q) = H(p,q) - E(A,p,q)">


### Exemplo Ilustrativo

### Regras de divisão para regressão

### Estratégia de poda

## Floresta Aleatória

## Redes Neurais

## _Boosting_
