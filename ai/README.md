 # Inteligência Artificial
 
Escreva um programa que retorne as raízes de uma equação de segundo grau. Escreva um programa que calcule a menor rota entre dois pontos. Escreva um programa que auxilie uma empresa de transporte a minimizar o tempo de entrega e os gastos com combustível. Escreva um programa que reconheça pessoas pelo rosto ou pela fala. Escreva um programa para dirigir um carro de forma autônoma. Escreva um programa para idenitificar buracos negros. Escreva um programa que controle os jogadores de um time de futebol de robôs. Escreva um programa que jogue Dota 2 e seja melhor que o melhor jogador humano. 

Qual estrutura de dados esses programas utilizam? Qual a complexidade desses algoritmos? O que eles tem em comum? O que eles tem de diferentes? Existe mais de um algoritmo que resolve o mesmo problema? Você consegue pensar em pelo menos uma solução para cada problema? O ser humano consegue resolver todos esses problemas? Como o ser humano consegue resolver todos esses problemas? Responder essas perguntas pode ser relativamente difícil, portanto, vamos assumir algumas premissas antes de começar: a primeira dela é que o ser humano consegue realizar boa parte das tarefas diárias porque ele é bom em reconhecer padrões. 

Padrões, de acordo com o discionário Michaelis on-line, é "aquilo que tem forma, tamanho, dimensões mais comuns em sua categoria ou em seu gênero; modelo, tipo". Um médico consegue, com um conjunto de sintomas e de resultados de exames clínicos, diagnosticar se um paciente está com algum problema cardíaco. Para isso, ele utiliza o conhecimento adquirido durante os 6 anos de formação acadêmica e sua experiência durante o exercício da profissão. É provável que somente utilizando o conhecimento adquirido nos livros o médico fosse capaz de diagnosticar. Mas, será que a experiência também não é um fator importante? 

Nos primórdios da Inteligência Artificial (IA), por volta de 1970, esses conhecimentos eram extraídos dos especialistas e regras lógicas eram construídas de forma a possibilitar a automatização das tarefas, sejam elas de diagnósticos de doenças, predizer se o banco deveria ou não emprestar dinheiro para uma pessoa e etc. Ou seja, o processo de aquisição de conhecimento normalmente envolvia entrevistas e a cooperação por parte do especialista resultando em um conjunto de regreas completamente subjetivas.

Nas últimas décadas, com a expansão da coleta de dados, o crescimento dos volumes de dados coletados, a necessidade de processamento desses dados e extração de conhecimento de forma automática, surgiu a necessidade de automatizar a extração de conhecimento. Ou seja, surgiu a necessidade de ferramentas que fossem capazes de criar por si próprias, a partir de experiência passada, uma hipótese ou função capaz de resolver um determinado problema. Uma hipótese ou função pode ser um regra ou conjunto de regras que descrevem o comportamento de um problema em relação a algum comportamento esperado. Esse processo de construção/indução de uma hipótese ou função recebe o nome de Aprendizado de Máquina (AM).

Uma das definições clássicas de AM foi dada por Mitchell em 1997 no livro *Machine Learning*: "Aprendizado de Máquina é a capacidade de melhorar o desempenho na realização de uma tarefa por meio da experiência". Ou seja, esperamos um comportamento inteligente quando temos a capacidade de memorizar, observar e aprender fatos por meio de práticas de organização do conhecimento em novas representações. Ethem Alpaydin em 2014 no livro *Introduction to Machine Learning* classificou como objetivo dos algoritmos de AM "programar computadores para usar dados ou experiências anteriores para resolver um determinado problema." 

O conjunto de dados *Jogar Tênis* é um problema de classificação binária em que pretende-se classificar se uma pessoa deve ou não, dado certas condições climáticas, jogar tênis. Nessa base de dados, cada linha representa uma amostra/dado/objeto e cada coluna/variável/atributo uma característica relacionada a essa amostra. Os atributos de entrada são o *Tempo*, *Temperatura*, *Umidade* e *Vento*. O conjunto tem 14 amostras de treinamento e a última coluna denominada *Joga* representa os rótulos jogar ou não tênis.

![](jogatenis.png) *Base de dados Jogar Tênis. Adaptado de Katti Faceli et al., (2011)*

Naturalmente podemos contratar um climatólogo expert em tênis para nos dizer quando e onde devemos jogar tênis baseado em muitos modelos climáticos e matemáticos. Provavelmente, ele usuaria uma fórmula matemática complexa e muito difícil de ser aplicada. Outra alternativa seria utilizar o aprendizado indutivo.

Indução, de acordo com o discionário Michaelis on-line, significa "forma de raciocínio que leva à conclusão de um certo caso com base na observação da regularidade de uma ocorrência". Ou seja, podemos entender que os algoritmos de AM aprendem por meio da experiência, ou seja, aprendizado indutivo. Quando um algoritmo de AM esta aprendendo a partir de um conjunto de dados, ele esta procurando uma hipótese, no espaço de possíveis hipóteses, capaz de descrever as relações entre objetos e que melhor se ajuste aos dados.

Exemplos de aprendizado indutivo:
* Seu pai quando diz que o melhor lugar para pescar é na rocha próximo a curva do rio; 
* Seu avô quando olha para o céu e diz que vai chover em 20 minutos;
* Sua avó quando diz que andar de moto é perigoso. 

## Indução da Hipótese ou Função

O que se deseja é construir uma hipótese capaz de predizer se devemos ou não jogar tênis para uma amostra antes nunca vista. Assim, uma vez induzida uma hipótese, é esperado que ela também seja válida para outras amostras do mesmo domínio mas, que não fazem do conjunto de treinamento. A essa capacidade da hipótese continuar valendo para outros objetos dá-se o nome de capacidade de generalização da hipótese. 

O objetivo de um algoritmo de AM utilizado nessa tarefa é aprender, a partir de um subconjunto dos dados, um modelo, hipótese ou função capaz de relacionar os valores dos atributos de entrada de um objeto ao valor do seu atributo de saída. Além disso, é importante que os algoritmos de AM sejam capazes de lidar com dados imperfeitos. Muitos conjuntos de dados apresentam algum tipo de imperfeição como presença de ruídos, dados ausentes e redundantes.

Quando uma hipótese apresenta baixa capacidade de generalização, pode ser que ela esteja superajustada aos dados (overfitting). Também podemos dizer que a hipótese memorizou os dados. Quando a hipótese apresenta baixa capacidade de generalização inclusive no conjunto de treianmento, dizemos que ela subajustou aos dados (underfitting). Essa condição pode acontecer quando o conjunto de treinamento é pequeno e pouco representativo ou o algoritmo utilizado para construir a hipótese é muito simples. A Figura a seguir apresenta exemplos de *overfitting*, *underfitting* e um hipótese ideal.

![](over_under.png) 
*Exemplo de hipóteses para uma base de dados.*

## Viés dos Algoritmos

Sem viés não haverá aprendizado. Portanto, todos os algoritmos de AM apresentam algum viés. Viés pode ser definido como características que restringem as hipóteses que serão visitadas no espaço de busca pelo algoritmo. Segundo Mitchell (1997), o viés permite que o algoritmo generalize o conhecimento adquirido durante a fase de treinamento para aplicá-lo com sucesso aos novos dados. Assim, cada algoritmo de AM apresenta dois vieses: o de representação e o de busca.

### Viés de Representação

O viés de representação está associado a forma como cada algoritmo de AM representa o conhecimento para descrever a hipótese induzida. A Árvore de Decisão (AD) representa o conhecimento por meio de uma estrutura de dados na forma de árvore. Os nós dessa árvore são perguntas a respeito de um atributo que levam aos nós folhas associados a uma classe da base de dados. Quando um novo exemplo é apresentado a esse modelo, a AD é percorrida da raíz até as folhas. Em uma Rede Neural Artificial (RNA) o modelo pode ser representado por matrizes que armazenam os valores dos pesos das conexões entre os neurônios e as diversas camadas da rede. Uma vez treinada (pesos calibrados), a rede propaga os novos exemplos multiplicando os valores de entrada com os pesos das conexões até a camada de saída.        

![](vies_representacao.png) 
*Exemplo de viés de representação para uma AD e Redes Neurais.*

### Viés de Busca

O viés de busca esta associado a forma como os algoritmos de AM buscam a hipótese que melhor se ajusta aos dados. Uma AD, por exemplo, pode utilizar o atributo mais informativo como nó raíz da árvore. Para descobrir qual atributo é esse, diversas medidas podem ser usadas como entropia, índice Gini e etc. O tamanho dessa AD também está relacionada ao viés de busca. Algumas ADs podem ser mais profundas em detrimentos de outras. O mesmo acontece com as RNAs.    

## Classificação do Aprendizado

Quando falamos de AM, estamos nos referindo ao aprendizado indutivo. Ou seja, aqueles algoritmos em que o aprendizado ocorre por meio da generalização dos exemplos de treinamento. Quando esses dados apresentam rótulos/classes ou um atributo alvo, normalmente estamos interessados em encontrar uma hipótese ou função que seja capaz de, utilizando os atributos da base, predizer o atributo alvo. Assim estamos nos referindo a um subconjunto de algoritmos dentro da etapa de AM chamados de preditivos ou supervisionados. As tarefas supervisionadas ainda se distinguem em dois tipos: rótulos contínuos (regressão) e discretos (classificação).    
