# Introdução
### Histórico

* Os primeiros compiladores surgiram na década de 50;
* Não há registros preciso de qual foi o primeiro compilador;
* Os primeiros compiladores lidavam com a tradução de fórmulas aritméticas (FORTRAN – Formula Translator);
* Os compiladores eram considerados programas difíceis de se escrever.

### Definição

Um compilador é um programa que lê um programa escrito em uma linguagem
(linguagem fonte) e o traduz para uma outra linguagem (linguagem alvo).

![Captura de tela 2022-06-23 112407](https://user-images.githubusercontent.com/85000470/175322835-4ac0a453-3244-4ad0-9b36-1dd839d249a4.png)

### Características dos compiladores

* O processo de compilação deve identificar e relatar possíveis erros no programa;
fonte
* Em geral, as linguagens fonte são linguagens de programação tradicionais
(C/C++, Java, Python, etc);
* As linguagens alvo podem ser tanto linguagens tradicionais quanto linguagens de máquina;
* Os compiladores podem ser classificados de diversas formas, dependendo de seu
objetivo ou como foi construído (de uma passagem, múltiplas passagens,
depuradores, etc).

### Criação do programa executável

* Além do compilador, outros programas podem ser usados na criação do programa
executável;
* Antes de ser passado para o compilador, o programa alvo pode ser pré-processado;
(por exemplo, o pré-processador da linguagem C processa as diretivas como
#include e #define);
* Após a compilação, o programa alvo pode demandar processamento adicional
para a construção do executável (novamente no caso da linguagem C, temos o
montador e o linkeditor).

### Exemplo de fluxo de geração de um programa executável

![image](https://user-images.githubusercontent.com/85000470/175323565-2e7373f9-948f-47a4-bda6-147c0ee9a064.png)

### Análise e Síntese

* A compilação é composta por duas partes: análise e síntese;
* A análise divide o programa fonte em partes constituintes e as organiza em uma
representação intermediária;
* Em geral, a representação intermediária consiste em uma árvore sintática, onde cada nó representa uma operação e cada filho representa um operando;
* A síntese constrói o programa alvo a partir desta representação intermediária.

### Exemplo de árvore sintática

![image](https://user-images.githubusercontent.com/85000470/175324147-06e029ad-4b16-46f4-9dd5-4168d0b82025.png)

### Análise do programa fonte

A análise é composta por três fases:
1. análise linear: o fluxo de caracteres que compõem o programa alvo é lido, da esquerda para direita, e agrupado em tokens (sequência de caracteres com
significado coletivo);
2. análise hierárquica: os tokens são ordenados hierarquicamente em coleções
aninhadas com significado coletivo;
3. análise semântica: verificação que garante que os componentes do programa se combinam de forma significativa.

### Análise léxica

Em um compilador, a análise linear também é denominada análise léxica ou
esquadrinhamento. Por exemplo, no enunciado

C = 1.8 * F + 32

a análise léxica identificaria os seguintes tokens:
1. o identificador C
2. o símbolo de atribuição =
3. a constante em ponto flutuante 1.8
4. o símbolo de multiplicação *
5. o identificador F
6. o símbolo de adição +
7. a constante inteira 32

### Análise sintática
