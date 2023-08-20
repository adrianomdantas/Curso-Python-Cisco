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


