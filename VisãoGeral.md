# Visão Geral

### Caracterização de uma linguagem de programação

* Uma linguagem de programação pode ser caracterizada por sua sintaxe (aparência
e forma de seus elementos) e por sua semântica (o significado destes elementos);
* Uma forma de especificar a sintaxe de uma linguagem é a gramática livre de
contexto (BNF – Forma de Backus-Naur);
* Além de especificar a semântica, a gramática livre de contexto auxilia a tradução
de programa, por meio da técnica denominada tradução dirigida pela sintaxe;
* A especificação da semântica é mais complicada, de modo que em muitos casos é
feita por meio de exemplos e descrições informais.

### Compilador de expressões infixas para posfixas

* A tradução dirigida pela sintaxe será ilustrada por meio do desenvolvimento de
um compilador simples de uma passagem que traduz expressões na forma infixa
para a forma posfixa;
* Por exemplo, a expressão 1-2+3, que está na forma infixa (o operador está
posicionado entre os operandos), corresponde a expressão posfixa 12-3+ (o
operador sucede os dois operandos, assuma que cada operando consiste em um
único dígito);
* A forma posfixa pode ser convertida diretamente para um programa que executa a
expressão usando uma pilha;
* O analisador léxico gerará um fluxo de tokens que alimentarão o tradutor dirigido
pela sintaxe (o qual combinará o analisador sintático com o gera.

### Estrutura de interface de vanguarda do compilador

![image](https://user-images.githubusercontent.com/85000470/176506141-4bf87684-408a-473c-9049-1f5ef4eb04ff.png)

### Definições

* Uma gramática deve descrever a estrutura hierárquica de seus elementos
* Por exemplo, o comando if-else da linguagem C, possui a forma:

if (expressão) comando else comando

a qual pode ser expressão como

cmd → if (expr) cmd else cmd

* A expressão acima é uma regra de produção, onde a seta significa “pode ter a
forma”;
* Os elementos léxicos da produção (palavras-chaves, parêntesis) são chamados
tokens ou terminais;
* Variáveis como expr e cmd representam sequências de tokens e são denominadas
não-terminais.

### Componentes da linguagem livre de contexto

1. Um conjunto de tokens, denominados símbolos terminais;
2. Um conjunto de não-terminais;
3. Um conjunto de produções. Cada produção é definida por um não-terminal (lado
esquerdo), seguido de uma seta, sucedida por uma sequência de tokens e/ou
não-terminais (lado direito);
4. Designação de um dos não-terminais como símbolo de partida.

### Convenções de notação da gramática livre de contexto

* A gramática é especificada por uma lista de produções;
* O símbolo de partida é definido como o não-terminal da primera produção listada;
* Dígitos, símbolos e palavras em negrito são terminais;
* Não-terminais são grafados em itálico;
* Os demais símbolos são tokens;
* Produções distintas de um mesmo não-terminal podem ser agrupadas por meio do
caractere '|', que significa, neste contexto, “ou”.

### Exemplo de sintaxe para expressões infixas com adição e subtração

* Considere a seguinte gramática para expressões compostas por dígitos decimais e
as operações de adição e subtração, em forma infixa:

![image](https://user-images.githubusercontent.com/85000470/176506971-6b407567-6e6d-46d4-952a-e7583d760af2.png)

* Os tokens desta gramática são os dez dígitos decimais e os caracteres '+' e '-';
* Os não-terminais são expr e digito;
* O símbolo de partida é o não-terminal expr.

### Cadeias de tokens

* Uma cadeia de tokens é uma sequência de zero ou mais tokens;
* Uma cadeia contendo zero tokens, grafada como ∊, é denominada cadeia vazia;
* Uma gramática deriva cadeias de tokens começando pelo símbolo de partida,
substituíndo repetidamente um não-terminal pelo lado direito de uma produção
deste não-terminal;
* O conjunto de todas as cadeias de tokens possíveis gerados desta maneira formam
a linguagem definida pela gramática.

### Exemplo de contrução da expressão 1 - 2 + 3 por meio da gramática

1. 1 é expr, pois 1 é digito (terceira alternativa para a produção de expr);
2. Pela segunda alternativa de produção de expr, 1-2 é também expr, pois 1 é
expr e 2 é digito;
3. Por fim, pela primeira alternativa de produção de expr, 1-2+3 é expr, pois 1-2 é
expr e 3 é digito.

### Árvore Gramatical

Dada uma gramática livre de contexto, uma árvore gramatical possui as seguintes
propriedades:

1. A raiz é rotulada pelo símbolo de partida
2. Cada folha é rotulada por um token ou por ∊
3. Cada nó interior é rotulado por um não-terminal
4. Se A é um não-terminal que rotula um nó interior e X1, X2, . . . , XN são os
rótulos de seus filhos (da esquerda para a direita), então

![image](https://user-images.githubusercontent.com/85000470/176509844-bc38915f-5546-4e0e-a3ed-6526509825e0.png)

é uma produção.

### Visualização da árvore gramatical da expressão 1-2+3

![image](https://user-images.githubusercontent.com/85000470/176509960-fa5a5a85-dc64-43b6-b395-4d12e6c445bb.png)

### Características da árvore gramatical

* As folhas da árvore gramatical, quando lidas da esquerda para a direita, formam o
produto da árvore, que é a cadeira gerada ou derivada a partir da raiz não-terminal
* O processo de encontrar uma árvore gramatical para uma dada cadeia de tokens é
chmado de análise gramatical ou análise sintática daquela cadeia
* Uma gramática que permite a construção de duas ou mais árvores gramaticais
distintas para uma mesma cadeia de tokens é denominada gramática ambígua
* A gramatica apresentada não é ambígua
* Contudo, se removida a distinção entre expr e digito, a gramática passaria a ser
ambígua:

![image](https://user-images.githubusercontent.com/85000470/176510157-7f33d1fb-f142-4711-bd8e-343deeca42b8.png)

### Exemplo de gramática ambígua

![image](https://user-images.githubusercontent.com/85000470/176510194-a600eb4d-5e24-4760-93b9-359a291d4f30.png)

### Associatividade de operadores

* Quando um operando está, simultaneamente, à esquerda e à direita de dois
operadores (por exemplo, o dígito 2 na expressão 1-2+3), é preciso decidir qual
destes operadores receberá o operando;
* Uma operação  é associativa à esquerda se a  b  c = (a  b)  c;
* Na maioria das linguagens de programação, os operadores aritméticos (+, -, * e
/) são associativos à esquerda;
* Uma operação  é associativa à direita se a  b  c = a  (b  c);
* Por exemplo, a atribuição (operador =) da linguagem C é associativa à direita: a
expressão a = b = c equivale a expressão a = (b = c);
* Uma gramática possivel para esta atribuição seria:

![image](https://user-images.githubusercontent.com/85000470/176510434-67cb67c3-5263-440f-a604-ca84321ecd63.png)

### Precedência de operadores

* Algumas expressões da aritmética contém ambiguidades que não podem ser
resolvidas apenas por meio da associatividade;
* Por exemplo, qual seria o resultada expressão 1 + 2 * 3? 9 ou 7?
* Dizemos que o operador ⊗ tem maior precedência do que o operador ⊕ se ⊗
captura os operandos antes que ⊕ o faça;
* Na aritmética, a multiplicação e a divisão tem maior precedência do que a adição
e a subtração;
* Se dois operadores tem mesma precedência, a associatividade determina a ordem
que as operações serão realizadas.

### Construção de gramáticas com precedência de operadores

É possível construir uma gramática com precedência de operadores a partir dos
seguintes passos:
1. Construa uma tabela com a associatividade e a precedência dos operadores, em
ordem crescente de precedência (operadores com mesma precedência aparecem na
mesma linha);

![image](https://user-images.githubusercontent.com/85000470/176510681-3f6f845f-a728-4d90-83d2-91d3b6837e52.png)

2. Crie um não-terminal para cada nível (expr e termo) e um não-terminal extra
para as unidades básicas da expressão (fator);

![image](https://user-images.githubusercontent.com/85000470/176510761-1333b9ff-5d3e-4d94-a063-a298176c2284.png)

3. Defina as produções para o último terminal criado para os níveis a partir dos
operadores com maior precedência;

![image](https://user-images.githubusercontent.com/85000470/176510858-ff3168a0-8554-4e7d-9b84-533a614fca48.png)

4. Faça o mesmo para os demais operadores, em ordem decrescente de precedência e
crescente na lista de terminais criados para os níveis.

![image](https://user-images.githubusercontent.com/85000470/176510892-92b40b6b-cec2-4e32-92c6-b5c0d3a8c0e3.png)

A presença de parêntesis na definição de f ator permite escrever expressões com níveis
arbitrários de aninhamento, sendo que os parêntesis tem precedência sobre todos os
operadores definidos.

### Notação posfixa

![image](https://user-images.githubusercontent.com/85000470/176511123-d8d8f9e6-5170-4186-a5a5-36cec0df3c52.png)

### Definições dirigidas pela sintaxe

* Uma definição dirigida pela sintaxe usa a gramatica livre de contexto para
especificar a estrutura sintática da entrada;
* Ela associa, a cada símbolo da gramática, um conjunto de atributos e, a cada
produção, um conjunto de regras semânticas para computar os valores dos
atributos associados aos símbolos presentes na produção;
* A gramática e o conjunto de regras semânticas constiturem a definição dirigida
pela sintaxe;
* Um atributo é dito sintetizado se seu valor depende apenas dos valores dos
atributos dos nós filhos de seu nó na árvore gramatical;
* Os atributos sintetizados podem ser computados por meio de uma travessia por
profundidade.

### Definição dirigida pela sintaxe para a tradução de notação infixa para posfixa

![image](https://user-images.githubusercontent.com/85000470/176511362-dcdd1969-1348-4f45-b51f-d5ac9d002262.png)

A notação X.t indica que t é um atributo de X e || indica concatenação de caracteres.

### Valores dos atributos nos nós da árvore gramatical da expressão 1-2+3

![image](https://user-images.githubusercontent.com/85000470/176511490-98df5d6f-82df-4ebf-839d-9b5f0159336d.png)

### Esquema de tradução

* Um esquema de tradução é uma gramática livre de contexto na qual fragmentos
de programas, denominados ações semânticas, são inseridos nos lados direitos das
produções;
* Num esquema de tradução, a ordem de avaliação das ações semânticas é
explicitamente mostrada;
* A posição na qual uma ação semântica deve ser executada marcada no lado
direito da produção, por meio de chaves;
* Na árvore gramatical uma ação semântica é indicada por um filho extra,
conectado por meio de uma linha pontilhada;
* Nós rotulados por ações gramaticas não possui filhos.

### Ações semânticas para a tradução de expressões para a notação posfixa

![image](https://user-images.githubusercontent.com/85000470/176511732-2a0fee3d-0232-4785-a69a-71a3535d19c5.png)

### Árvore gramatical com ações semânticas que traduz a expressão 1-2+3

![image](https://user-images.githubusercontent.com/85000470/176511807-607c9124-6e29-4b15-9fd9-42a2bf403e1c.png)

### Análise gramatical

* A análise gramatical é o processo de se determinar se uma cadeia de tokens pode
ser gerada por uma gramática;
* O compilador deve ser capaz de construir uma árvore gramatical, mesmo que de
forma implícita;
* Um analisador gramatical pode ser construído para qualquer gramática;
* Para qualquer gramáticas livres de contexto existe um analisador gramatical que
analisa N tokens com complexidade O(N^3);
* Contudo, existem analisadores lineares para quase todas as gramáticas livres de
contexto que surgem na prática.

### Análise _top-down_ e _bottom-up_

* Há duas classes principais de analisadores gramaticais;
* Analisadores top-down a construção parte da raiz da árvore gramatical para suas
folhas;
* Analisadores bottom-up partem das folhas em direção à raiz;
* Os analisadores top-down são mais populares, pois é possível construir
analisadores eficientes desta classe de forma manual;
* Já os analisadores bottom-up podem manipular uma gama mais ampla de
gramáticas;
* Geradores de analisadores gramaticais tendem a usar métodos bottom-up.

### Construção _top-down_ de uma árvore gramatical

1. Inicie na raiz, rotulada pelo não-terminal de partida
2. Repita os seguintes passos:
(a) Para o nó n, rotulado pelo não-terminal A, selecione uma das produções para A e
construa os filhos de n com os símbolos do lado direito da produção
(b) Encontre o próximo nó no qual uma subárvore deve ser construída

Observações:
(i) A depender da gramática, esta construção pode ser implementada com uma única
passagem da entrada, da esquerda para a direita;
(ii) O token que está sendo observado é frequentemente denominado lookahead;
(iii) Inicialmente lookahead é o token mais à esquerda da entrada.

### Exemplo: gramática para geração de subtipos em Pascal

![image](https://user-images.githubusercontent.com/85000470/176512364-8c45111c-cd20-4f1a-b112-e7a5182932a3.png)

Observação: os dois pontos (‘..’) formam um único token.

### Exemplo de construção _top-down_ da árvore gramatical

Considere a expressão array [ num .. num ] of integer, gerada a partir da
gramática de subtipos em Pascal.

(a) A construção inicial na raiz da árvore. O rótulo da raiz é o não-terminal de partida

tipo

(b) A única produção de tipo que inicia com o lookahead (neste momento, array) é
a terceira. Esta produção será usada para a criação dos filhos do nó raiz.

![image](https://user-images.githubusercontent.com/85000470/176512546-24c9bb4a-7061-49b8-b2fd-aea2ce0f0b72.png)
