# Classificação

## Árvores de Decisão

As Árvores de Decisão (AD) são algoritmos supervisionados que podem ser utilizados tanto para problemas de classificação quanto regressão. O objetivo principal é induzir um modelo que seja capaz de predizer uma classe/rótulo/valor de uma variável resposta por meio do aprendizado de regras simples inferidas do conjunto de treinamento.

### Componentes de uma AD

* **Nó de devisão:** Possui dois ou mais sucessores. Contém teste condicional baseado nos valores dos atributos. Normalmente o teste é univariado e em um atributo. Exemplo: Idade > 18, Profissão &#8712; {professor, estudante}, 0.3 + 0.2x – 0.5x² &#8924; 0
* **Nó folha:** É rotulado com uma função que considera valores da variável alvo dos exemplos que chegam na folha. Em uma AD de classificação podemos usar uma função de minimização de custo 0-1 como a moda. Em AD de regressão minimizando erro médio quadrático ou desvio absoluto. Exemplo: média/mediana

### Algoritmo

**Entrada:** conjunto de treinamento D = {(xi ,yi), i=1,...,n}
**Saída:** AD
**Se** critério de parada **então**
  **Retorna** nó folha com rótulo que maximiza função de custo
Escolha o atributo que maximiza o critério de divisão em D
**Para cada** partição Di baseada nos valores do atributo **faça**
    Induzir subárvore *Árvorei = GeraÁrvore(Di)*
**Retorna** Árvore com nó de decisão baseado no atributo escolhido e descendentes *Árvorei*


## Floresta Aleatória

## Redes Neurais

## _Boosting_
