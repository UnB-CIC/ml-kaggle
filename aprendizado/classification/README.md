# Classificação

## Árvores de Decisão e Regressão

As Árvores de Decisão e Regressão são algoritmos supervisionados. O objetivo principal é induzir um modelo que seja capaz de predizer uma classe/rótulo/valor de uma variável resposta por meio do aprendizado de regras simples inferidas do conjunto de treinamento. Essas regras são geradas por meio da estratégia de devisão e consquista, que recursivamente tende a diminuir a complexidade do problema tornando-o mais simples. Os modelos em árvore são designados Árvores de Decisão (AD) para problemas de classificação e Árvores de Regressão (AR) para problemas de regressão.   

### Componentes de uma AD

Formalmente uma AD é um grafo acíclico direcionado em cada nó é um nó de devisão ou um nó folha:

* **Nó de divisão:** Possui dois ou mais sucessores. Contém teste condicional baseado nos valores dos atributos. Normalmente o teste é univariado, ou seja, em um único atributo. Exemplo: Idade > 18, Profissão &#8712; {professor, estudante}, 0.3 + 0.2x – 0.5x² &#8924; 0

* **Nó folha:** É rotulado com uma função que considera valores da variável alvo dos exemplos que chegam na folha. Em uma AD de classificação podemos usar uma função de minimização de custo 0-1 como a moda. Em AD de regressão minimizando erro médio quadrático ou desvio absoluto. Exemplo: média/mediana

### Uma AD genérica

A Figura a seguir representa uma AD e sua divisão no espaço para uma base de dados com dois atributos preditivos (x_1 e x_2). Cada nó da árvore corresponde a uma região nesse espaço. As regiões nos nós folhas são mutualmente excludentes e a junção de todas as regiões cobre todo o espaço definido pelos atributos. Os hiperplanos gerados são ortogonais aos eixos dos atributos testados e parapelo a todos os outros eixos. Todas as regiões são hiper-retângulos.

![Exemplo de uma Árvore de Decisão](https://github.com/UnB-CIC/ml-kaggle/blob/master/aprendizado/classification/ad.png)

### Algoritmo

O algoritmo de AD é mostrado na Figura a seguir. A entrada para afunção é o conjunto de treinamento **D** e sua saída é uma AD. Na sequencia o critério de parada é avaliado. Se mais divisões do conjunto de treinamento são necessárias, é escolhido um atributo que maximiza alguma medida de impureza. Na sequencia a função de geração da árvore é chamada recursivamente e aplicada a uma partição do conjunto de treinamento **D**.

![Algoritmo de uma Árvore de Decisão](https://github.com/UnB-CIC/ml-kaggle/blob/master/aprendizado/classification/ad_alg.png)

É importante dizer que a geração de uma árvore minila é um problema NP-completo. Os algoritmos exploram heurísticas que localmente executam pesquisa um passo a frente. Uma vez que uma decisão é tomanda ela nunca é desfeita. Isso pode gerar uma solução ótima localmente o que pode estar longe do ótimo global. 

### Regras de divisão para classificação


### Exemplo Ilustrativo

### Regras de divisão para regressão

### Estratégia de poda

## Floresta Aleatória

## Redes Neurais

## _Boosting_
