# Naive Bayes 

Uma forma de lidar com dados ruidosos e imprecisos é utilizando algoritmos baseados no Teorema de Bayes. O Teorema de Bayes assume que a probabilidade de um evento A ocorrer dado um outro evento B, depende da relação entre ambos, além da probabilidade de observar esses eventos de forma independentes. Nessa definição, a probabilidade de ocorrência do evento A e B podem ser estimada pela frequência com que esses eventos ocorrem de forma independente P(A) e P(B). De forma semelhante, é possível estimar a probabilidade de um evento ocorrer dado B para cada evento A por meio da probabilidade P(B|A). Com isso podemos estimar a probabilidade de A ocorrer dado B, ou seja, P(A|B). O Teorema de Bayes pode ser definido como:

<img src="https://render.githubusercontent.com/render/math?math=P(A|B) = \frac{P(B|A)*P(A)}{P(B)}">

De forma análoga podemos reescrever esse teorema para calcular a probabidade de ocorrência de cada uma das classes <img src="https://render.githubusercontent.com/render/math?math=y_l"> de uma base de dado para uma amostra <img src="https://render.githubusercontent.com/render/math?math=x">:

<img src="https://render.githubusercontent.com/render/math?math=P(y_l|x) = \frac{P(x|y_l)*P(y_l)}{P(x)}">

Aquela classe <img src="https://render.githubusercontent.com/render/math?math=y_l"> que maximizar a probabilidade *a posteori* deve ser a classe com maior probabilidade. Portanto, temos:

<img src="https://render.githubusercontent.com/render/math?math=y_{MAP} = arg max_l \frac{P(x|y_l)*P(y_l)}{P(x)}">

Como o denominador <img src="https://render.githubusercontent.com/render/math?math=P(x)"> é constante para todas as classes <img src="https://render.githubusercontent.com/render/math?math=y_l">, podemos reescrever a expressão como:   

<img src="https://render.githubusercontent.com/render/math?math=y_{MAP} = arg max_l P(x|y_l)*P(y_l)">

Expandindo a segunda parte da equação temos: 

<img src="https://render.githubusercontent.com/render/math?math=P(x|y_l)*P(y_l)=">
<img src="https://render.githubusercontent.com/render/math?math==P(x_1,...,x_d|y_l)*P(y_l)="> 
<img src="https://render.githubusercontent.com/render/math?math==P(x_1|y_l)*P(x_2,...,x_d|y_l,x_1)*P(y_l)="> <img src="https://render.githubusercontent.com/render/math?math==P(x_1|y_l)*P(x_2|y_l,x_1)*P(x_3,...,x_d|y_l,x_1,x_2)*P(y_l)="> <img src="https://render.githubusercontent.com/render/math?math=..."> 
<img src="https://render.githubusercontent.com/render/math?math==P(x_1|y_l)*P(x_2|y_l,x_1)*P(x_3|y_i,x_1,x_2) *...* P(x_d|y_i,x_1,x_2,...,x_{d-1})*P(y_l)">

Infelizmente é computacionalmente **impraticável calcular todas essas probabilidades**. Pensando nisso, simplificações são propostas. Uma delas, chamada de Naive Bayes (NB), assume que os valores dos atributos é independente portanto, a probabilidade <img src="https://render.githubusercontent.com/render/math?math=P(x|y_l)"> pode ser decomposta em <img src="https://render.githubusercontent.com/render/math?math=P(x_1|y_l)*P(x_2|y_l)*P(x_3|y_l)*...*P(x_d|y_l)">. Assim, podemos definir a probabilidade de uma amostra pertencer a uma classe como:

<img src="https://render.githubusercontent.com/render/math?math=P(y_l|x)=P(y_l)*\prod_{j=1}^{d}P(x_j|y_l)">

As principais vantagens desse algoritmo são: sua eficiência, uma vez que todas as probabilidades podem ser calculadas na etapa de treinamento; a construção do modelo é eficiente além de ser de fácil implementação; o algoritmo também é robusto a ruídos e atributos irrelevantes. As principais desvantagens são: o algoritmo desconsidera a dependência entre os atributos o que pode ser danoso para uma gama de problemas reais; ele traça hiperplanos lineares (o que também pode não ser suficiente dependendo da complexidade do problema); e ele necessita de adaptações quando os atributos são numéricos.   

## Exemplo Ilustrativo

O conjunto de dados *Jogar Tênis* é um problema de classificação binária em que pretende-se classificar se uma pessoa deve ou não, dado certas condições climáticas, jogar tênis. Os atributos de entrada são o *Tempo*, *Temperatura*, *Umidade* e *Vento*. O conjunto tem 14 amostras de treinamento e a última coluna denominada *Joga* representa os rótulos jogar ou não tênis. Os atributos *Tempo* e *Vento* são categóricos e os atributos *Temperatura* e *Umidade* são contínuos.

![](jogatenis.png) 
*Base de dados Jogar Tênis. Adaptado de Katti Faceli et al., (2011)*

Para construir um NB precisamos descobrir as probabilidades associadas dos atributos e das classes para o novo exemplo. Assumindo que o exemplo de teste é (Tempo=Ensolarado, Temperatura=70, Umidade=80 e Vento=Sim), calcule a probabilidade de jogar tênis. 

**1⁰ Passo:**

Probabilidade associada de cada classe:

<img src="https://render.githubusercontent.com/render/math?math=P(Joga = Sim) = \frac{9}{14}">
<img src="https://render.githubusercontent.com/render/math?math=P(Joga = Nao) = \frac{5}{14}">

**2⁰ Passo:**

Estimar a probabilidades de observar os valores do exemplo de teste para cada classe:

<img src="https://render.githubusercontent.com/render/math?math=P(Tempo = Ensolarado | Joga = Sim) = \frac{2}{5}">
<img src="https://render.githubusercontent.com/render/math?math=P(Tempo = Ensolarado | Joga = Nao) = \frac{3}{5}">

Quando temos atributos numéricos como *Temperatura* e *Unidade*, o procedimento consiste em calcular a média geral do atributo e definir esse valor como ponto de corte para o cálculo das probabilidades. Caso a amostra a ser classificada tenha um valor menor do que o ponto de corte, basta calcular a frequência com que isso acontece. 

<img src="https://render.githubusercontent.com/render/math?math=mean(Temperatura) = 73.6">
<img src="https://render.githubusercontent.com/render/math?math=P(Temperatura = 70 | Joga = Sim) = \frac{5}{8}">
<img src="https://render.githubusercontent.com/render/math?math=P(Temperatura = 70 | Joga = Nao) = \frac{3}{8}">

<img src="https://render.githubusercontent.com/render/math?math=mean(Umidade) = 81.6">
<img src="https://render.githubusercontent.com/render/math?math=P(Umidade = 80 | Joga = Sim) = \frac{6}{7}">
<img src="https://render.githubusercontent.com/render/math?math=P(Umidade = 80 | Joga = Nao) = \frac{1}{7}">

<img src="https://render.githubusercontent.com/render/math?math=P(Vento = Sim | Joga = Sim) = \frac{3}{6}">
<img src="https://render.githubusercontent.com/render/math?math=P(Vento = Sim | Joga = Nao) = \frac{3}{6}">

**3⁰ Passo:**

<img src="https://render.githubusercontent.com/render/math?math== P(Joga = Sim) * P(Tempo = Ensolarado | Joga = Sim) * P(Temperatura = 70 | Joga = Sim) * P(Umidade = 80 | Joga = Sim) * P(Vento = Sim | Joga = Sim)">
<img src="https://render.githubusercontent.com/render/math?math== \frac{9}{14} * \frac{2}{5} * \frac{5}{8} * \frac{6}{7} * \frac{3}{6}">
<img src="https://render.githubusercontent.com/render/math?math== 0.06887755">

<img src="https://render.githubusercontent.com/render/math?math==P(Joga = Nao) * P(Tempo = Ensolarado | Joga = Nao) * P(Temperatura = 70 | Joga = Nao) * P(Umidade = 80 | Joga = Nao) * P(Vento = Sim | Joga = Nao)">
<img src="https://render.githubusercontent.com/render/math?math==\frac{5}{14} * \frac{3}{5} * \frac{3}{8} * \frac{1}{7} * \frac{3}{6}">
<img src="https://render.githubusercontent.com/render/math?math== 0.005739796">

**4⁰ Passo:**

<img src="https://render.githubusercontent.com/render/math?math== \frac{0.06887755}{0.06887755 + 0.005739796} = 0.9230769">
<img src="https://render.githubusercontent.com/render/math?math== \frac{0.005739796}{0.06887755 + 0.005739796} = 0.005739796">

Portanto devemos jogar tênis!

## Links úteis

Outras versões desse mesmo algoritmo:
  * [NB](https://scikit-learn.org/stable/modules/naive_bayes.html)
  * [Versões NB](https://en.wikipedia.org/wiki/Naive_Bayes_classifier#Parameter_estimation_and_event_models)
