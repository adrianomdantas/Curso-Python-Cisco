## Python Essentials 1:
## Módulo 3

**Valores Booleanos, Execução Condicional, Loops, Listas e Processamento de Lista, Operações Lógicas e Bitwise**

Neste módulo, serão abordados os seguintes tópicos:

* o tipo de dados Booleano;
* operadores relacionais;
* tomar decisões em Python (if, if-else, if-elif, else)
* como repetir a execução de código utilizando loops (while, for)
* como executar operações lógicas e bitwise em Python;
* listas em Python (construção, indexação e slicing; manipulação de conteúdo)
* como classificar uma lista usando algoritmos de bubble-sort;
* listas multidimensionais e suas aplicações.

## 3.1.1.1 Tomar decisões em Python
## Perguntas e respostas

Um programador escreve um programa e **o programa faz perguntas**.

Um computador executa o programa e **fornece as respostas**. O programa deve ser capaz de **reagir de acordo com as respostas recebidas**.

Felizmente, os computadores conhecem apenas dois tipos de respostas:

* sim, isto é verdade;
* não, isto é falso.

Nunca obterá uma resposta como Deixe-me pensar...., Não sei, ou Provavelmente sim, mas não tenho a certeza.

**Para fazer perguntas, o Python utiliza um conjunto de operadores muito especiais**. Vamos analisá-los um após outro, ilustrando os seus efeitos em alguns exemplos simples.


## Comparação: operador de igualdade

Pergunta: **são dois valores iguais?**

Para fazer esta pergunta, utiliza o operador `==` (igual igual).

Não se esqueça desta importante distinção:

* `=` é um **operador de atribuição**, por exemplo, `a = b` atribui `a` com o valor de `b`;
* `==` é a questão são estes valores iguais?; `a == b` **compara** `a` e `b`.
  
É um **operador binário com ligação do lado esquerdo**. Precisa de dois argumentos e **verifica se são iguais.**

**Exercícios**
Agora vamos fazer algumas perguntas. Tente adivinhar as respostas.

Pergunta #1: Qual é o resultado da seguinte comparação?

`2 == 2`    Verifique

`True` - claro, 2 é igual a 2. O Python responderá `True` (lembre-se deste par de literais predefinidos, `True` e `False` - são também keywords de Python).

Pergunta #2: Qual é o resultado da seguinte comparação?

2 == 2.    Verifique

Esta questão não é tão fácil quanto a primeira. Felizmente, o Python é capaz de converter o valor inteiro no seu verdadeiro equivalente, e consequentemente, a resposta é `True`.

Pergunta #3: Qual é o resultado da seguinte comparação?

`1 == 2`    Verifique

Esta deve ser fácil. A resposta será (ou melhor, será sempre) `False`.

## 3.1.1.2 Fazer decisões em Python
## Igualdade: o operador igual a (==)

A função `==` (igual a) compara os valores de dois operandos. Se forem iguais, o resultado da comparação é `True`. Se eles não forem iguais, o resultado da comparação é `False`.

Veja a comparação de igualdade abaixo - qual é o resultado desta operação?

`var == 0`

Note que não podemos encontrar a resposta se não soubermos qual o valor atualmente armazenado na variável `var`.

Se a variável tiver sido alterada muitas vezes durante a execução do seu programa, ou o seu valor inicial for inserido a partir da consola, a resposta a esta pergunta pode ser dada apenas pelo Python, e apenas em runtime.

Agora imagine um programador que sofre de insónias, e que tem de contar ovelhas pretas e brancas separadamente enquanto houver exatamente o dobro das ovelhas pretas do que das brancas.

A questão será a seguinte:

`black_sheep == 2 * white_sheep`

Devido à baixa prioridade do operador `==` , a questão deve ser tratada como equivalente a esta:

`black_sheep == (2 * white_sheep)`

<hr>
Então, vamos praticar a sua compreensão do operador `==` - consegue adivinhar o output do código abaixo?

```
var = 0  # Assigning 0 to var
print(var == 0)

var = 1  # Assigning 1 to var
print(var == 0)
```

Execute o código e verifique se estava certo.

![True False](Imagens/TrueFalse.jpg)

## Desigualdade: o operador não igual a (!=)

A função `!=` (não igual) também compara os valores de dois operandos. Aqui está a diferença: se eles forem iguais, o resultado da comparação é `False`. Se eles não forem iguais, o resultado da comparação é `True`.

Agora dê uma vista de olhos na comparação de desigualdade em baixo - consegue adivinhar o resultado desta operação?
```
var = 0  # Assigning 0 to var
print(var != 0)

var = 1  # Assigning 1 to var
print(var != 0)
```

Execute o código e verifique se estava certo.

![False True](Imagens/FalseTrue.jpg)

## 3.1.1.3 Tomar decisões em Python
## Operadores de comparação: maior que

Pode também fazer uma pergunta de comparação usando o operador `>` (maior que).

Se quiser saber se há mais ovelhas pretas do que brancas, pode escrevê-lo da seguinte forma:

`black_sheep > white_sheep  # Greater than`

`True` confirma-o; `False` nega-o.

## Operadores de comparação: maior que ou igual a

O operador maior que tem outra variante especial, **não estrita**, mas é denotada de forma diferente da notação aritmética clássica: `>=` (maior que ou igual a)

Existem dois sinais subsequentes, não um.

Ambos os operadores (estritos e não-estritos), bem como os outros dois discutidos na próxima sessão, são operadores **binários com ligação à esquerda**, e a sua **prioridade é maior do que a mostrada por** `==` **e** `!=`.

Se quisermos descobrir se temos ou não de usar um chapéu quente, fazemos a seguinte pergunta:

`centigrade_outside ≥ 0.0  # Greater than or equal to`

## Operadores de comparação: menor que ou igual a

Como já deve ter adivinhado, os operadores utilizados neste caso são: o `<` (less than) operator and its non-strict sibling: `<=` (menor que ou igual a).

Veja este exemplo simples:
```
current_velocity_mph < 85  # Less than
current_velocity_mph ≤ 85  # Less than or equal to
```

Vamos verificar se existe o risco de ser multado pela polícia rodoviária (a primeira pergunta é rigorosa, a segunda não).

## Fazer uso das respostas

O que pode fazer com a resposta (ou seja, o resultado de uma operação de comparação) que obtém do computador?

Há pelo menos duas possibilidades: primeiro, pode memorizá-la (**armazená-la numa variável**) e utilizá-la mais tarde. Como se faz isso? Bem, utilizaria uma variável arbitrária como esta:

`answer = number_of_lions >= number_of_lionesses`

O conteúdo da variável dar-lhe-á a resposta à pergunta feita.

A segunda possibilidade é mais conveniente e muito mais comum: pode usar a resposta que obtém para **tomar uma decisão sobre o futuro do programa**.

Precisa de uma instrução especial para este fim, e discutiremos isso muito em breve.

Agora precisamos de atualizar a nossa **tabela de prioridades** e colocar todos os novos operadores na mesma. Agora parece-se com o seguinte:

|Prioridade|Operador||
|---|---|---|	
|1	|`+`, `-`	|unário|
|2	|`**`	||
|3	|`*`, `/`, `//`, `%`||
|4	|`+`, `-`	|binário|
|5	|`<`, `<=`, `>`, `>=`||	
|6	|`==`, `!=`||

## 3.1.1.4 LAB: Perguntas e respostas