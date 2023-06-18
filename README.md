# Projeto da disciplina de PAA (Projeto e Análise de Algoritmos)

Este projeto foi criado com o intuito de enfatizar os conhecimentos adquiridos durante a disciplica. Abaixo será descrito o problema abordado e os passos que tomamos para resolvê-lo.

## Encontre maneiras totais de chegar ao nº degrau com no máximo 'm' passos

### 1. Descrição do problema

<p style="text-align: justify;">
    Dada uma escada, encontre o número total de maneiras de chegar ao n-ésimo degrau a partir da base da escada quando uma pessoa só pode subir no máximo m degraus de cada vez. Por exemplo, considere que a entrada do algoritmo seja de chegar ao quarto degrau da escada (n = 4) onde a pessoa só pode subir no máximo dois degraus de cada vez (m = 2). A saída do algoritmo será o <strong>total de maneiras</strong> de chegar ao 4° degrau com no máximo 2 degraus. Analisando o problema manualmente, temos as seguintes formas de resolver essa ocorrência: 
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
<p style="text-align: justify;">
    Esse algoritmo apresenta uma versão recursiva da solução do problema, sendo executado em complexidade de tempo exponencial, uma vez que são calculadas soluções para os mesmos subproblemas repetidamente.  
</p>
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

<p style="text-align: justify;">
    Após o tratamento dos casos bases, a função inicializa uma variável de nome <strong>count</strong> para fazer o papel de contador e inicia o loop. O loop incrementa essa variável com o retorno da chamada recursiva de <strong>totalWays</strong>, onde o valor de n é decrementado pelo valor i que vai de 1 até o número menor ou igual a m no loop, desde que (n - i) >= 0 retorne verdadeiro, uma vez que nosso algoritmo não recebe números negativos como entrada. Após o término do loop, a função retorna o valor de <strong>count</strong>.
</p>

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

#### 2.2. Exemplo de execução
<p style="text-align: justify;">
    Neste caso com algoritmo recursivo, o exemplo será demonstrado através da Árvore de Recursividade, onde através dela é possível mostrar de forma simples todas as chamadas recursivas do algoritmo. Segue a imagem abaixo:
</p>
&nbsp;
<div align="center">
    <img src="assets/arvRec.png" alt="Árvore de Recursividade" style="max-width: 500px;"/>
</div>
&nbsp;

### 3. ALGORITMO 02 - Abordagem de baixo para cima  
<p style="text-align: justify;">
    Esse algoritmo utiliza tabulação para resolver o problema de forma ascendente. Para isso, um array temporário é construído para armazenar os resultados de cada subproblema usando os resultados já computados dos subproblemas menores.
</p>
<p style="text-align: justify;">
    A seguir temos o pseudocódigo.
</p>

```C++
totalWays(n, m)

// Entradas: Dois inteiros n e m, com n >= 0 e m > 0, que são as escadas e os passos respectivamente.
// Saída: Um número inteiro maior ou igual a zero que representa o total de formas que se pode chegar ao n-ésimo degrau.

     cria lookup[n + 1]     // Array temporário que armazena números inteiros

     // Caso base 1: Para alcançar o degrau 0 ou o degrau 1.
     se n >= 0 então
          lookup[0] <- 1

    // Armazenando os resultados: 
	para i de 1 até n faça
        lookup[i] <- 0
    	para j de 1 até m enquanto (i - j) >= 0 faça
        	lookup[i] <- lookup[i] + lookup[i - j]
    	fim para
	fim para

	retorne lookup[n]
```

<p style="text-align: justify;">
    A função <strong>totalWays</strong> apresenta no seu código pré-loop a criação do array temporário <strong>lookup</strong> que será utilizado para guardar a solução dos subproblemas e o tratamento de dois casos base que vão armazenar os valores dos subproblemas menores neste array. Mais detalhes são apresentados a seguir.
</p>

- Criação do array temporário
    <p style="text-align: justify;">
        O array temporário lookup consiste em uma estrutura de dados que guardará (como número do tipo inteiro) as soluções dos subproblemas gerados pelo algoritmo. A solução final desejada será armazenada no índice do n-ésimo degrau correspondente. Note que lookup é criado com n+1 posições, ou seja, seus índices abrangem a faixa de números inteiros de 0 até n.
    </p>

- Caso base 
    <p style="text-align: justify;">
        Esse caso base consiste em um if que testa se a entrada n é maior ou igual a 0. Como uma pessoa só pode executar um passo para alcançar o degrau 0, o valor 1 é atribuído a lookup[0].
    </p>
<p style="text-align: justify;">
    Ao término dessas etapas, o código entra em dois laços aninhados. No primeiro loop temos que i é inicializado em 1 e vai até o valor de n, e no segundo temos que j inicia em 1 e vai até o valor de m, sempre verificando se a expressão (i - j) >= 0 retorna true (caso contrário, o loop mais interno é interrompido).  A função geral desses laços é de associar os valores dos subproblemas ainda não solucionados aos índices correspondentes no array temporário <strong>lookup</strong>, utilizando as soluções dos subproblemas que já estão armazenadas no mesmo (note que antes dessa operação, os índices dos subproblemas ainda não solucionados recebem o valor 0). Isso é feito somando todos os valores armazenados nos m’s índices anteriores a posição i analisada naquele momento.
</p>
<p style="text-align: justify;">
    Após o término do loop, a função retorna o valor armazenado em Após o término do loop, a função retorna o valor de <strong>lookup[n]</strong>.
</p>

#### 3.1. Corretude
- Especificação:
  1. <pré_cond>: Entrada é n e m inteiros, com m > 0.
  1. <pos_cond>: Saída é um inteiro maior ou igual a zero que representa o total de formas que se pode chegar ao n-ésimo degrau.
- Invariante:
  1. Número de degraus percorridos representados por i até chegar ao n-ésimo degrau. E j é o número de passos m que se pode dar.
- Condição de saída:
  1. j até m e enquanto (i - j) >= 0
  1. i até n
- Estabeleça o invariante do loop:
  1. São os casos bases e passar vai para o loop
- Finalização:
  1. Acabou de sair do loop, o invariante é verdadeiro e a condição de saída é satisfeita. Retorna lookup[n] que satisfaz a <pos_cond>.

#### 3.2. Exemplo de execução
<p style="text-align: justify;">
    Para o algoritmo de programação dinâmica, o mesmo exemplo será representado de duas formas diferentes. A primeira mais completa e complexa em forma de tabela, e a segunda mais simples na forma de uma array.
</p>
<p style="text-align: justify;">
    Para a primeira e segunda forma teremos como entrada n = 4 e m = 2. Segue as imagens abaixo:
</p>
&nbsp;
<div align="center">
    <img src="assets/Tabela_dinâmica01.png" alt="Tabela dinâmica" style="max-width: 500px;"/>
    <img src="assets/Tabela_dinâmica02.png" alt="Tabela dinâmica" style="max-width: 500px;"/>
</div>
&nbsp;
<p style="text-align: justify;">
    Na primeira forma apresentada acima, primeiramente ocorre o preenchimento dos valores retornados pelo caso base. Para m > 0 e n = 0 o índice 0 do array recebe o valor 1.
</p>
<p style="text-align: justify;">
    Ao fim do preenchimento do caso base, cada posição da tabela que ainda não foi preenchida recebe a soma dos valores guardados nas m células imediatamente acima do valor procurado (respeitando o espaço alocado para o armazenamento). Por exemplo, a célula na posição [2,1] recebe o valor da célula que está imediatamente acima, ou seja, o valor da posição [1,1]. No caso da célula da posição [2,2], ela guardará o valor da soma das subsoluções armazenadas nas duas posições imediatamente acima, ou seja, [1,2] + [0,2].
</p>
&nbsp;
<div align="center">
    <img src="assets/Tabela_dinâmica03.png" alt="Tabela dinâmica" style="max-width: 500px;"/>
    <img src="assets/Tabela_dinâmica04.png" alt="Tabela dinâmica" style="max-width: 500px;"/>
</div>
&nbsp;
<p style="text-align: justify;">
    Na segunda forma apresentada acima,  primeiramente ocorre o preenchimento dos valores retornados pelo caso base. Para m > 0 e n = 0 o índice 0 do array recebe o valor 1.
</p>
<p style="text-align: justify;">
    Ao fim do preenchimento dos caso base, cada posição da tabela que ainda não foi preenchida recebe a soma dos valores guardados nos m índices anteriores (respeitando o espaço alocado para o armazenamento) do índice que irá receber o valor procurado.
</p>  

#### 3.3. Exemplo 02 (n = 4 e m = 4)
- Dinâmico.  
<div align="center">
    <img src="assets/Tabela_dinâmica05.png" alt="Tabela dinâmica" style="max-width: 500px;"/>
    <img src="assets/Tabela_dinâmica06.png" alt="Tabela dinâmica" style="max-width: 500px;"/>
    <img src="assets/Tabela_dinâmica07.png" alt="Tabela dinâmica" style="max-width: 500px;"/>
</div>
&nbsp;