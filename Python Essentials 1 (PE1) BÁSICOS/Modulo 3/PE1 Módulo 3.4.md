## 3.4.1.1 Listas - coleções de dados

## Porque precisamos de listas?
Pode acontecer que tenha de ler, armazenar, processar e, finalmente, imprimir dezenas, talvez centenas, talvez até milhares de números. E então, é necessário criar uma variável em separado para cada valor? É necessário passar várias horas escrevendo declarações como as abaixo?
```
var1 = int(input())
var2 = int(input())
var3 = int(input())
var4 = int(input())
var5 = int(input())
var6 = int(input())
:
:
```

Se pensar que esta não é uma tarefa complicada, então pegue num pedaço de papel e escreva um programa que:

* leia cinco números,
* que os imprima por ordem do mmenor para o maior (este tipo de processamento chama-se triagem).

Deve chegar à conclusão de que não tem sequer papel suficiente para completar a tarefa.

Até agora, aprendeu a declarar variáveis que são capazes de armazenar exatamente um determinado valor de cada vez. Tais variáveis são por vezes chamadas **escalares**, por analogia com a matemática. Todas as variáveis que utilizou até agora são na verdade, escalares.

Pense no quão conveniente seria declarar uma variável que pudesse **armazenar mais do que um valor**. Por exemplo, cem, ou mil, ou até dez mil. Seria ainda uma e a mesma variável, mas muito ampla e espaçosa. Parece apelativa? Talvez, mas como lidaria com um recipiente cheio de valores diferentes? Como escolheria apenas aquele de que necessita?


E se pudesse simplesmente numerá-los? E depois dizer: dá-me o valor número 2; atribui o valor número 15; aumenta o valor número 10000.

Vamos mostrar-lhe como declarar tais **variáveis multi-valores**. Vamos fazer isto com o exemplo que acabámos de sugerir. Vamos escrever um **programa que ordena uma sequência de números**. Não seremos particularmente ambiciosos - vamos assumir que existem exatamente cinco números.

Vamos criar uma variável chamada `numbers`; é atribuída não apenas com um número, mas é preenchida com uma lista constituída por cinco valores (nota: a **lista começa com um parêntesis reto aberto e termina com um parêntesis reto fechado**; o espaço entre os parêntesis é preenchido com cinco números separados por vírgulas).

`numbers = [10, 5, 7, 2, 1]`

Digamos a mesma coisa usando terminologia adequada: `numbers` **é uma lista constituída por cinco valores, todos eles números**. Podemos também dizer que esta declaração cria uma lista de comprimento igual a cinco (visto existir cinco elementos no seu interior).

Os elementos dentro de uma lista **podem ter tipos diferentes**. Alguns deles podem ser inteiros, outros floats, e outros ainda podem ser listas.

O Python adotou uma convenção, afirmando que os elementos numa lista são **sempre numerados a partir do zero**. Isto significa que o artigo armazenado no início da lista terá o número zero. Uma vez que existem cinco elementos na nossa lista, ao último deles é atribuído o número quatro. Não esqueça isto.

Rapidamente se acostumará a isto, e tornar-se-á uma segunda natureza.

Antes de avançarmos na nossa discussão, temos de referir o seguinte: a nossa **lista é uma coleção de elementos, mas cada elemento é um escalar**.

## 3.4.1.2 Listas - coleções de dados | Indexação

## Indexar listas

Como se altera o valor de um elemento escolhido na lista?

Vamos **atribuir um novo valor de** `111` **ao primeiro elemento** na lista. Fazemos assim:
```
numbers = [10, 5, 7, 2, 1]
print("Original list content:", numbers)  # Printing original list content.

numbers[0] = 111
print("New list content: ", numbers)  # Current list content.
```
<hr>

E agora queremos que **o valor do quinto elemento seja copiado para o segundo elemento** - consegue adivinhar como o fazer?
```
numbers = [10, 5, 7, 2, 1]
print("Original list content:", numbers)  # Printing original list content.

numbers[0] = 111
print("\nPrevious list content:", numbers)  # Printing previous list content.

numbers[1] = numbers[4]  # Copying value of the fifth element to the second.
print("New list content:", numbers)  # Printing current list content.
```

O valor dentro dos parêntesis que seleciona um elemento da lista é chamado um **index**, enquanto a operação de selecionar um elemento da lista é conhecida como **indexing** (indexação).

Vamos utilizar a função `print()` para imprimir o conteúdo da lista cada vez que fazemos as alterações. Isto ajudar-nos-á a seguir cada passo com mais cuidado e a ver o que se passa após uma determinada modificação da lista.

```
numbers = [10, 5, 7, 2, 1]
print("List content:", numbers)  # Printing original list content.
```

Nota: todos os índices usados até agora são literais. Os seus valores são fixados em runtime, mas **qualquer expressão também pode ser o index**. Isto oferece muitas possibilidades.

## 3.4.1.3 Listas - coleções de dados | Indexação

## Aceder ao conteúdo da lista

Cada um dos elementos da lista pode ser acedido separadamente. Por exemplo, pode ser impresso:

`print(numbers[0]) # Accessing the list's first element.`

Assumindo que todas as operações anteriores tenham sido concluídas com sucesso, o snippet enviará `111` para o console.

Como pode ver no editor, a lista também pode ser impressa como um todo - tal como aqui:

`print(numbers)  # Printing the whole list.`

Como provavelmente já notou antes, o Python decora o output de uma forma que sugere que todos os valores apresentados formam uma lista. O output do exemplo acima é o seguinte:

```[111, 1, 7, 2, 1]```

## O método len() .

O **comprimento de uma lista** pode variar durante a execução. Novos elementos podem ser acrescentados à lista, enquanto outros podem ser retirados da mesma. Isto significa que a lista é uma entidade muito dinâmica.

Se quiser verificar o comprimento atual da lista, pode usar uma função chamada `len()` (o seu nome vem de length (comprimento)).

A função toma o **nome da lista como argumento, e devolve o número de elementos atualmente armazenados** dentro da lista (por outras palavras - o comprimento da lista).

Veja a última linha de código no editor, execute o programa e verifique que valor irá imprimir para a consola. Consegue adivinhar?

```
numbers = [10, 5, 7, 2, 1]
print("Original list content:", numbers)  # Printing original list content.

numbers[0] = 111
print("\nPrevious list content:", numbers)  # Printing previous list content.

numbers[1] = numbers[4]  # Copying value of the fifth element to the second.
print("Previous list content:", numbers)  # Printing previous list content.

print("\nList length:", len(numbers))  # Printing the list's length.

Output
Original list content: [10, 5, 7, 2, 1]

Previous list content: [111, 5, 7, 2, 1]
Previous list content: [111, 1, 7, 2, 1]

List length: 5
```

## 3.4.1.4 Listas - coleções de dados | Operações em listas

## Remover elementos de uma lista

Qualquer elemento da lista pode ser **removido** a qualquer momento - isto é feito com uma instrução chamada `del` (delete). Nota: é uma `instrução`, não uma função.

É preciso apontar o elemento a ser removido - desaparecerá da lista, e o comprimento da lista será reduzido em um.

Olhe para o snippet abaixo. Consegue adivinhar que output irá produzir? Execute o programa no editor e verifique.
```
del numbers[1]
print(len(numbers))
print(numbers)
```
<hr>

**Não se pode aceder a um elemento que não existe** - não se pode obter o seu valor nem atribuir-lhe um valor. Ambas estas instruções irão agora causar erros de runtime:
```
print(numbers[4])
numbers[4] = 1

```

Adicione o snippet acima após a última linha de código no editor, execute o programa e verifique o que acontece.

```
output
List length: 4
Traceback (most recent call last):
  File "main.py", line 18, in <module>
    print(numbers[4])
IndexError: list index out of range
```

Nota: retirámos um dos elementos da lista - agora só há quatro elementos na lista. Isto significa que o elemento número quatro não existe.
```
numbers = [10, 5, 7, 2, 1]
print("Original list content:", numbers)  # Printing original list content.

numbers[0] = 111
print("\nPrevious list content:", numbers)  # Printing previous list content.

numbers[1] = numbers[4]  # Copying value of the fifth element to the second.
print("Previous list content:", numbers)  # Printing previous list content.

print("\nList's length:", len(numbers))  # Printing previous list length.

###

del numbers[1]  # Removing the second element from the list.
print("New list's length:", len(numbers))  # Printing new list length.
print("\nNew list content:", numbers)  # Printing current list content.

###
```

## 3.4.1.5 Listas - coleções de dados | Operações em listas
## Índices negativos são legais

Pode parecer estranho, mas os índices negativos são legais, e podem ser muito úteis.

Um elemento com um index igual a `-1` é **o último na lista**.

`print(numbers[-1])`

O snippet de exemplo terá como output 1. Execute o programa e verifique.
```
numbers = [111, 7, 2, 1]
print(numbers[-1])
print(numbers[-2])

output
1
2
```

Da mesma forma, o elemento com um index igual a `-2` é **o penúltimo na lista**.

`print(numbers[-2])`

O snippet de exemplo terá como output 2.

O último elemento acessível da nossa lista é numbers[-4] (o primeiro) - não tente ir mais longe!

## 3.4.1.6 LAB: Noções básicas de listas
## 3.4.1.7 Listas - coleções de dados | Funções e métodos

## Funções vs. métodos

Um **método é um tipo específico de função** - comporta-se como uma função e parece uma função, mas difere na forma como atua, e no seu estilo de invocação.

Uma **função não pertence a nenhum dado** - recebe dados, pode criar novos dados e (geralmente) produz um resultado.

Um método faz todas estas coisas, mas também é capaz de **alterar o estado de uma entidade selecionada**.

**Um método é propriedade dos dados para os quais trabalha, enquanto uma função é propriedade de todo o código**.


Isto também significa que a invocação de um método requer alguma especificação dos dados a partir dos quais o método é invocado.

Pode parecer intrigante aqui, mas lidaremos com isso em profundidade quando nos aprofundarmos na programação orientada ao objeto.

Em geral, uma invocação de função típica pode parecer-se com isto:

`result = function(arg)`

A função toma um argumento, faz algo, e devolve um resultado.


Um método típico de invocação é geralmente semelhante a este:

`result = data.method(arg)`

Nota: o nome do método é precedido do nome dos dados que possuem o método. Em seguida, adiciona-se um **ponto**, seguido do **nome do método**, e um par de **parêntesis que encerra os argumentos**.

O método comportar-se-á como uma função, mas pode fazer algo mais - **pode alterar o estado interno dos dados** a partir dos quais foi invocado.
<hr>

Pode perguntar: porque estamos falando de métodos e não de listas?

Esta é uma questão essencial neste momento, pois vamos mostrar-lhe como adicionar novos elementos a uma lista existente. Isto pode ser feito com métodos pertencentes a todas as listas, e não por funções.

## 3.4.1.8 Listas - coleções de dados | métodos de lista
## Adicionar elementos a uma lista: append() e insert()

Um novo elemento pode ser colado no fim da lista existente:

`list.append(value)`

Tal operação é realizada por um método chamado `append()`. Toma o valor do seu argumento e coloca-o **no final da lista** que possui o método.

O comprimento da lista aumenta então em um.
<hr>

O método `insert()` é um pouco mais inteligente - pode acrescentar um novo elemento em **qualquer lugar da lista**, e não apenas no final.

`list.insert(location, value)`

São necessários dois argumentos:

* o primeiro mostra a localização necessária do elemento a ser inserido; nota: todos os elementos existentes que ocupam locais à direita do novo elemento (incluindo o que se encontra na posição indicada) são deslocados para a direita, a fim de criar espaço para o novo elemento;
* o segundo é o elemento a ser inserido.

Veja o código no editor. Veja como utilizamos os `append()` e `insert()` métodos. Preste atenção ao que acontece após a utilização `insert()`: o primeiro elemento é agora o segundo, o segundo o terceiro, e assim por diante.
<hr>

Adicione o seguinte snippet após a última linha de código no editor:

`numbers.insert(1, 333)`


Imprima o conteúdo da lista final para o ecrã e veja o que acontece. O snippet acima do snippet insere 333 na lista, tornando-o no segundo elemento. O anterior segundo elemento torna-se o terceiro, o terceiro o quarto, e assim por diante.

```
numbers = [111, 7, 2, 1]
print(len(numbers))
print(numbers)

###

numbers.append(4)

print(len(numbers))
print(numbers)

###

numbers.insert(0, 222)
print(len(numbers))
print(numbers)

#

numbers.insert(1, 333)
print(len(numbers))
print(numbers)

output
4
[111, 7, 2, 1]
5
[111, 7, 2, 1, 4]
6
[222, 111, 7, 2, 1, 4]
7
[222, 333, 111, 7, 2, 1, 4]
```

## 3.4.1.9 Listas - coleções de dados | métodos de lista
## Adicionar elementos a uma lista: continuação

Pode **iniciar a vida de uma lista tornando-a vazia** (isto é feito com um par de parêntesis retos vazio) e depois adicionando-lhe novos elementos conforme necessário.

Veja o snippet no editor. Tente adivinhar o seu output após a execução do loop `for` . Execute o programa para verificar se estava certo.
```
my_list = []  # Creating an empty list.

for i in range(5):
    my_list.append(i + 1)

print(my_list)

output
[1, 2, 3, 4, 5]
```
Será uma sequência de números inteiros consecutivos a partir de 1 (depois adiciona-se um a todos os valores anexados) até 5.


Modificámos um pouco o snippet:
```
my_list = []  # Creating an empty list.

for i in range(5):
    my_list.insert(0, i + 1)

print(my_list)

output
[5, 4, 3, 2, 1]
```

O que acontecerá agora? Execute o programa e verifique se desta vez também estava certo.

Deve obter a mesma sequência, mas em **ordem inversa** (este é o mérito de usar o método `insert()` ).

## 3.4.1.10 Listas - coleções de dados | listas e loops

## Utilização de listas

O loop `for` tem uma variante muito especial que pode `processar listas` muito eficazmente - vejamos isso.

Vamos supor que deseja **calcular a soma de todos os valores armazenados na lista** `my_list` .

É necessária uma variável cuja soma será armazenada e à qual será inicialmente atribuído um valor de `0` - o seu nome será total. (Nota: não vamos nomeá-la sum visto o Python usar o mesmo nome para uma das suas funções internas - `sum()`. **Utilizar o mesmo nome seria geralmente considerado uma má prática**). Em seguida, acrescenta-lhe todos os elementos da lista utilizando o loop `for` . Veja o snippet no editor.

Vamos comentar este exemplo:

* à lista é atribuída uma sequência de cinco valores inteiros;
* a variável `i` toma os valores `0`, `1`, `2`, `3`, e `4`, e depois indexa a lista, selecionando os elementos seguintes: o primeiro, o segundo, o terceiro, o quarto e o quinto;
* cada um destes elementos é adicionado em conjunto pelo operador `+=` à variável `total` , dando o resultado final no fim do loop;
* observe a forma como a função `len()` foi utilizada - torna o código independente de quaisquer possíveis alterações no conteúdo da lista.

## A segunda face do loop for .

Mas o loop `for` pode fazer muito mais. Pode ocultar todas as ações ligadas à indexação da lista, e entregar todos os elementos da lista de uma forma prática.

Este snippet modificado mostra como isto funciona:
```
my_list = [10, 1, 8, 3, 5]
total = 0

for i in my_list:
    total += i

print(total)
```

O que acontece aqui?

* a instrução `for` especifica a variável usada para navegar na lista (`i` aqui) seguida pela keyword `in` e pelo nome da lista que está a ser processada (`my_list` aqui)
* à variável i são atribuídos os valores de todos os elementos da lista subsequente, e o processo ocorre tantas vezes quantos os elementos da lista;
* isto significa que se utiliza a variável `i` como uma cópia dos valores dos elementos, e não se precisa de utilizar índices;
* a função `len()` também não é necessária aqui.

## 3.4.1.11 Listas - coleções de dados | listas e loops

## Listas em ação

Deixemos as listas de lado por um breve momento e vejamos uma questão intrigante.

Imagine que precisa de reorganizar os elementos de uma lista, ou seja, inverter a ordem dos elementos: o primeiro e o quinto, bem como o segundo e o quarto elementos serão trocados. O terceiro permanecerá intocado.


Pergunta: como se pode trocar os valores de duas variáveis?

Veja o snippet:
```
variable_1 = 1
variable_2 = 2

variable_2 = variable_1
variable_1 = variable_2
```

Se fizer algo como isto, **perderá o valor previamente armazenado** em `variable_2`. Alterar a ordem das atribuições não ajudará. É necessária uma **terceira variável que sirva como armazenamento auxiliar**.

É assim que se pode fazer:
```
variable_1 = 1
variable_2 = 2

auxiliary = variable_1
variable_1 = variable_2
variable_2 = auxiliary
```

O Python oferece uma forma mais conveniente de fazer a troca - veja:
```
variable_1 = 1
variable_2 = 2

variable_1, variable_2 = variable_2, variable_1
```

Claro, eficaz e elegante - não é?

## 3.4.1.12 Listas - coleções de dados | listas e loops

## Listas em ação

Agora pode facilmente **trocar** os elementos da lista para **inverter a sua ordem**:
```
my_list = [10, 1, 8, 3, 5]

my_list[0], my_list[4] = my_list[4], my_list[0]
my_list[1], my_list[3] = my_list[3], my_list[1]

print(my_list)
```

Execute o snippet. O seu output deve ter este aspeto:
```
output
[5, 3, 8, 1, 10]
```

Fica bem com cinco elementos.

Será ainda aceitável com uma lista contendo 100 elementos? Não, não será.

Pode utilizar o loop `for` para fazer a mesma coisa automaticamente, independentemente do comprimento da lista? Sim, pode.
<hr>

Foi assim que o fizemos:
```
my_list = [10, 1, 8, 3, 5]
length = len(my_list)

for i in range(length // 2):
    my_list[i], my_list[length - i - 1] = my_list[length - i - 1], my_list[i]

print(my_list)
```

Nota:

* nós atribuímos a variável `length` com o comprimento da lista atual (isto torna o nosso código um pouco mais claro e mais curto)
* lançamos o loop `for` para correr através do seu corpo `length // 2` vezes (isto funciona bem para listas com comprimentos pares e ímpares, porque quando a lista contém um número ímpar de elementos, o do meio permanece intocado)
* trocamos o i<sup>-ésimo</sup> elemento (desde o início da lista) com o que tem um index igual a `(length - i - 1)` (do final da lista); no nosso exemplo, para `i` igual a `0` o ramo `(lenght - i - 1)` dá `4`; para `i` igual a `1`, dá `3` - Isto é exatamente o que precisavamos.
As listas são extremamente úteis, e irá encontrá-las com muita frequência.

## 3.4.1.14 RESUMO DA SECÇÃO

## Key takeaways

1. A **lista é um tipo de dados** em Python usada para **armazenar vários objetos**. É uma coleção ordenada e mutável de ítens separados por vírgulas, entre parêntesis retos, por exemplo:

`my_list = [1, None, True, "I am a string", 256, 0]`

2. As listas podem ser **indexadas e atualizadas**, por exemplo:
```
my_list = [1, None, True, 'I am a string', 256, 0]
print(my_list[3])  # outputs: I am a string
print(my_list[-1])  # outputs: 0

my_list[1] = '?'
print(my_list)  # outputs: [1, '?', True, 'I am a string', 256, 0]

my_list.insert(0, "first")
my_list.append("last")
print(my_list)  # outputs: ['first', 1, '?', True, 'I am a string', 256, 0, 'last']
```

3. As listas podem ser nested, por exemplo:

`my_list = [1, 'a', ["list", 64, [0, 1], False]]`

Aprenderá mais sobre o nesting no módulo 3.1.7 - por enquanto, só queremos que esteja ciente de que algo como isto também é possível.

4. Os elementos da lista e as listas podem ser **excluídos**, por exemplo:
```
my_list = [1, 2, 3, 4]
del my_list[2]
print(my_list)  # outputs: [1, 2, 4]

del my_list  # deletes the whole list
```

Novamente, aprenderá mais sobre isto no módulo 3.1.6 - não se preocupe. Por enquanto, basta tentar experimentar o código acima e verificar como a sua alteração afeta o output.

5. As listas podem ser **iteradas** através da utilização do loop `for` , por exemplo:
```
my_list = ["white", "purple", "blue", "yellow", "green"]

for color in my_list:
    print(color)
```

6. A função `len()` pode ser usada para **verificar o comprimento da lista**, por exemplo:
```
my_list = ["white", "purple", "blue", "yellow", "green"]
print(len(my_list))  # outputs 5

del my_list[2]
print(len(my_list))  # outputs 4
```

7. Uma invocação de **função** típica parece-se com a seguinte: `result = function(arg)`, enquanto uma invocação de **método** típica parece-se com isto:`result = data.method(arg)`.




**Exercício 1**

Qual é o output do seguinte snippet?
```
lst = [1, 2, 3, 4, 5]
lst.insert(1, 6)
del lst[0]
lst.append(1)

print(lst)
```

Verifique
`[6, 2, 3, 4, 5, 1]`

**Exercício 2**

Qual é o output do seguinte snippet?
```
lst = [1, 2, 3, 4, 5]
lst_2 = []
add = 0

for number in lst:
    add += number
    lst_2.append(add)

print(lst_2)
```

Verifique
`[1, 3, 6, 10, 15]`

**Exercício 3**

O que acontece quando executa o seguinte snippet?
```
lst = []
del lst
print(lst)
```

Verifique
`NameError: name 'lst' is not defined`


**Exercício 4**

Qual é o output do seguinte snippet?
```
lst = [1, [2, 3], 4]
print(lst[1])
print(len(lst))

```
Verifique
```
[2, 3]
3
```

