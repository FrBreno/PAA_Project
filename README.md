# Projeto da disciplina de PAA (Projeto e Análise de Algoritmos)

Este projeto foi criado com o intuito de enfatizar os conhecimentos adquiridos durante a disciplica. Abaixo será descrito o problema abordado e os passos que tomamos para resolvê-lo.

## Encontre maneiras totais de chegar ao nº degrau com no máximo 'm' passos

### 1. Descrição do problema

<p style="text-align: justify;">
Dada uma escada, encontre o número total de maneiras de chegar ao n-ésimo degrau a partir da base da escada quando uma pessoa só pode subir no máximo m degraus de cada vez. Por exemplo, considere que a entrada do algoritmo seja de chegar ao quarto degrau da escada (n = 4) onde a pessoa só pode subir no máximo dois degraus de cada vez (m = 2). A saída do algoritmo será o **total de maneiras** de chegar ao 4° degrau com no máximo 2 degraus. Analisando o problema manualmente, temos as seguintes formas de resolver essa ocorrência: 
</p>

* 1 degrau + 1 degrau + 1 degrau + 1 degrau
* 1 degrau + 1 degrau  + 2 degraus
* 1 degrau + 2 degraus + 1 degrau
* 2 degraus + 1 degrau + 1 degrau
* 2 degraus + 2 degraus 

<p style="text-align: justify;">
Com isso, sabemos que a saída do algoritmo retornará o valor 5, referente ao total de maneiras que o problema pode ser resolvido.
Um segundo exemplo que podemos analisar seria o de chegar ao quarto degrau (n = 4) com no máximo quatro degraus de cada vez (m = 4). Analisando o problema manualmente, temos as seguintes maneiras de resolvê-lo:
</p>

* 1 degrau + 1 degrau + 1 degrau + 1 degrau
* 1 degrau + 1 degrau + 2 degraus
* 1 degrau + 2 degraus + 1 degrau
* 2 degraus + 1 degrau + 1 degrau
* 2 degraus + 2 degraus
* 1 degrau + 3 degraus
* 3 degraus + 1 degrau
* 4 degraus

<p style="text-align: justify;">
Dessa forma, a saída do algoritmo retornará o valor 8, referente ao total de maneiras que o problema pode ser solucionado.Note que para o algoritmo ser executada de forma correta as entradas n e m têm que respeitar as seguintes propriedades:
</p>

* n - Um número inteiro maior ou igual a 0.
* m - Um número inteiro maior que 0.

<p style="text-align: justify;">
Com as entradas válidas, o algoritmo retornará um número inteiro maior que 0 referente ao total de formas em que se pode chegar ao n-ésimo degrau com no máximo m degraus de cada vez. Neste resente artigo serão apresentados e analisados dois algoritmos para essa problemática que, de forma resumida, apresentam as seguintes diferenças no que tange a complexidade de tempo:
</p>

* **ALGORITMO 01:** Recursivo.
A complexidade de tempo da solução é exponencial, pois o problema exibe subproblemas sobrepostos uma vez que o algoritmo calcula soluções para os mesmos problemas repetidamente.

* **ALGORITMO 02:** Abordagem de baixo para cima, utilizando programação dinâmica.
É uma abordagem de baixo para cima onde podemos usar a tabulação para resolver esse problema de forma ascendente. A ideia principal é construir um array temporário que armazena os resultados de cada subproblema usando os resultados já computados dos subproblemas menores.

Cada algoritmo será aprofundado nos tópicos a seguir.

### 2. ALGORITMO 01 - Recursivo

Esse algoritmo apresenta uma versão recursiva da solução do problema, sendo executado em complexidade de tempo exponencial, uma vez que são calculadas soluções para os mesmos subproblemas repetidamente.  
A seguir temos o pseudocódigo.
```C++
totalWays(n, m) 
 
    // Entradas: Dois inteiros n e m, com n >= 0 e m > 0 que representam as escadas e os passos respectivamente.
    // Saída: Um número inteiro maior ou igual a zero que representa o total de formas que se pode chegar ao n-ésimo degrau. 

    // Caso base 1: 1 caminho (sem passos)
    se n = 0 então
      retorne 1

    count <- 0
    para i de 1 até m enquanto (n - i >= 0) faça
      count <- count + totalWays(n - i, m) // Chamada recursiva.
    fim para
   
    retorne count
```  

A função recursiva **totalWays** apresenta no seu código pré-loop o tratamento de dois casos bases:
- Caso base  
Consiste em um **if** que testa se a entrada n é um valor nulo e retorna 1. 

Após o tratamento dos casos bases, a função inicializa uma variável de nome **count** para fazer o papel de contador e inicia o loop. O loop incrementa essa variável com o retorno da chamada recursiva de **totalWays**, onde o valor de n é decrementado pelo valor i que vai de 1 até o número menor ou igual a m no loop, desde que (n - i) >= 0 retorne verdadeiro, uma vez que nosso algoritmo não recebe números negativos como entrada.
	Após o término do loop, a função retorna o valor de **count**.

#### 2.1. Corretude
- Especificação:
  1. Entrada dois números inteiros positivos n e m.
  1. Saída um número inteiro maior que 0.
- Invariante:
  1. Variável i que irá percorrer de 1 até m e fará a chamada recursiva receber sempre n - i, até n = 0.
- Condição de saída:
    1. Se por acaso passar pela a condição do caso base e entrar ele irá retornar um valor dentro da recursividade e fechará um galho da árvore binária.
- Estabeleça o invariante do loop:
    1. São os casos bases, se por acaso o código executar as condições do caso e não entrar dentro deles ele irá realizar o looping e se invariante.
- Finalização:
    1. Após sair do looping ele retorna o valor de count que será um número inteiro maior que zero.

