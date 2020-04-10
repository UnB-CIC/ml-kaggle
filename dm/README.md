# Mineração de Dados

A etapa de Mineração de Dados engloba a preparação, a análise estatística e o pré-peocessamento dos dados. Alguns estudos apontam que essas etapas juntas representam 60% de todo o tempo gasto até a indução dos modelos de AM. Outros estudos também  apontam que um pré-processamento adequado é fundamental para a indução dos algoritmos de AM de forma eficiente. As seções seguintes irão abordar essas etapas.   
   
## Preparação e Análise dos Dados

A preparação e análise dos dados é uma etapa fundamental da tarefa de AM. Ela permite que informações valiosas como a descoberta de padrões e tendências nos padrões que geraram os dados. Algumas podem ser obtidas por meio de fórmulas estatísticas e outras por meio de técnicas de visualização dos dados.

### Conjuntos de Dados

Um conjunto de dados são formados por **amostras** ou **objetos** físicos ou abstratos. Cada objeto é descrito por um conjunto de **atributo de entrada** ou  **atributo preditivo** ou **vetor e característica**. Cada objeto corresponde a uma ocorrência desses dados. Cada atributo esta relacionado a uma propriedade do objeto. Em bases supervisonadas, o conjunto de dados tem um atributo especial chamado de **atributo de saída** ou **rótulo**. Esse atributo de saída pode ser contínuo ou discreto. Quando contínuo dizemos que esse conjunto de dados é de regressão e quando discreto, de classificação.

Formalmente esse conjunto de dados é representado por uma matriz <img src="https://render.githubusercontent.com/render/math?math=X_{nxd}"/> onde *n* é o número de objetos e *d* é o número de atributos de entrada. Cada elemento dessa matriz <img src="https://render.githubusercontent.com/render/math?math=x^{j}_{i}"/> contém o valor da j-ésima característica para o i-ésimo objeto. Os rótulos podem ser representados por um vetor  <img src="https://render.githubusercontent.com/render/math?math=y = \{c_1, c_2,...c_l \}"/> onde <img src="https://render.githubusercontent.com/render/math?math=c_l"/> representa os *l* rótulos da base de dados. Também podemos representar os *d* atributos como eixos ortogonais, os objetos como pontos no espaço de dimensão *d* e os rótulos como formato ou cor desses pontos.  

Apesar do crescente número de bases disponíveis, na maioria das vezes não é possível aplicar os algoritmos de AM de forma direta. Portanto uma etapa anterior de pré-processamento é fundamental. Dentre as tarefas envolvidas no pré-processamento tempos a integração dos dados de diferentes fontes em estrutura em forma de matriz, a eliminação manual de atributos irrelevantes como ID e outros que não represetam informações relacionadas ao contexto, o balanceamento das amostras para tornar a base mais uniforme, a presença de ruído, dados incosistêntes e a transformação são outros problemas. 

### Análise dos Dados

## Pré-processamento dos Dados

### Limpeza dos Dados

#### Incompletos

#### Redudantes

#### Desbalanceamento

#### Ruídos

### Transformação dos Dados

### Redução de Dimensionalidade


