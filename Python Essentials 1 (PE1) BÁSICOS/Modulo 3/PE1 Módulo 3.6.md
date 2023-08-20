## 3.6.1.1 Operações em listas

## A vida interna das listas

Agora queremos mostrar-lhe uma característica importante e muito surpreendente das listas, que as distingue fortemente das variáveis comuns.

Queremos que o memorize - pode afetar os seus programas futuros, e causar graves problemas se esquecido ou negligenciado.

Veja o snippet no editor.

O programa:

* cria uma lista de um elemento chamada `list_1`;
* atribui-o a uma nova lista chamada `list_2`;
* altera o único elemento de `list_1`;
* imprime `list_2`.

```
list_1 = [1]
list_2 = list_1
list_1[0] = 2
print(list_2)

output
[2]
```
A parte surpreendente é o fato de que o programa fará o output: `[2]`, não `[1]`, que parece ser a solução óbvia.

As listas (e muitas outras entidades complexas de Python) são armazenadas de formas diferentes das variáveis ordinárias (escalares).

Pode-se dizer que:

* o nome de uma variável ordinária é o **nome do seu conteúdo**;
* o nome de uma lista é o nome de um **local de memória onde a lista é armazenada**.

Leia estas duas linhas mais uma vez - a diferença é essencial para compreender aquilo de que vamos falar a seguir.

A atribuição: `list_2 = list_1` copia o nome do array, não o seu conteúdo. Com efeito, os dois nomes (`list_1 e list_2`) identificam o mesmo local na memória do computador. Modificar um deles afeta o outro, e vice-versa.

Como se lida com isso?

## 3.6.1.2 Operações em listas | slices

## Slices poderosas

Felizmente, a solução está ao seu alcance - o seu nome é **slice**.

Uma slice é um elemento da sintaxe Python que lhe permite **fazer uma cópia completamente nova de uma lista ou partes de uma lista**.

Na verdade, a slice copia o conteúdo da lista, não o seu nome.

Isto é exatamente o que necessita. Observe o snippet em baixo:
```
list_1 = [1]
list_2 = list_1[:]
list_1[0] = 2
print(list_2)
```

O seu output é `[1]`.

Esta parte inconspícua do código descrito como `[:]` é capaz de produzir uma lista completamente nova.
<hr>

Uma das formas mais gerais da slice tem o seguinte aspecto:

`my_list[start:end]`

Como pode ver, assemelha-se à indexação, mas os dois pontos no interior fazem uma grande diferença.

Uma slice desta forma **faz uma nova lista (alvo), retirando elementos da source list - os elementos dos índices desde o início até** `end - 1`.

Nota: não para `end` mas para `end - 1`. Um elemento com um índice igual a `end` é o primeiro elemento que **não participa no slicing**.

É possível utilizar valores negativos tanto para o início como para o fim (tal como na indexação).

Veja o snippet:
```
my_list = [10, 8, 6, 4, 2]
new_list = my_list[1:3]
print(new_list)

output
[8, 6]
```

A `new_list` lista terá `end - start` (3 - 1 = 2) elementos - aqueles com índices iguais a `1` e `2` (mas não  ).

O output do snippet é: `[8, 6]`

## 3.6.1.3 Operações em listas | slices

## Slices - índices negativos

Veja o snippet em baixo:

`my_list[start:end]`


Para repetir:

* `start` é o index do primeiro elemento **incluído no slice**;
* `end` é o index do primeiro elemento **não incluído no slice**.

É assim que os índices negativos funcionam com o slice:
```
my_list = [10, 8, 6, 4, 2]
new_list = my_list[1:-1]
print(new_list)
```

O output do snippet é:

`[8, 6, 4]`



Se o `start` especifica um elemento que se encontra mais longe do que o descrito pelo `end` (do ponto de vista inicial da lista), o slice estará vazio:
```
my_list = [10, 8, 6, 4, 2]
new_list = my_list[-1:1]
print(new_list)
```

O output do snippet é:

`[]`

## 3.6.1.4 Operações em listas | slices

## Slices: continuação

Se omitir o `start` no seu slice, assume-se que pretende obter um slice começando pelo elemento com index `0`.

Por outras palavras, o slice desta forma:

`my_list[:end]`

é um equivalente mais compacto de:

`my_list[0:end]`

Veja o snippet em baixo:
```
my_list = [10, 8, 6, 4, 2]
new_list = my_list[:3]
print(new_list)
```

É por isso que o seu output é: `[10, 8, 6]`.

Da mesma forma, se omitir o `end` no seu slice, presume-se que deseja que o slice termine no elemento com o index `len(my_list)`.

Por outras palavras, o slice desta forma:

`my_list[start:]`


é um equivalente mais compacto de:

`my_list[start:len(my_list)]`


Veja o snippet seguinte:
```
my_list = [10, 8, 6, 4, 2]
new_list = my_list[3:]
print(new_list)
```

O seu output é, portanto: `[4, 2]`.

# 3.6.1.5 Operações em listas | slices, del

## Slices: continuação

Como já dissemos anteriormente, omitindo ambos `start` e `end` faz uma cópia de toda a lista:
```
my_list = [10, 8, 6, 4, 2]
new_list = my_list[:]
print(new_list)
```

O output do snippet é: `[10, 8, 6, 4, 2]`.
<hr>

A instrução anteriormente descrita `del` é capaz de **apagar mais do que apenas um elemento de uma lista ao mesmo tempo - também pode apagar slices**:
```
my_list = [10, 8, 6, 4, 2]
del my_list[1:3]
print(my_list)
```

Nota: neste caso, o slice **não produz nenhuma lista nova**!

O output do snippet é: `[10, 4, 2]`.


A eliminação de **todos os elementos** de uma só vez também é possível:
```
my_list = [10, 8, 6, 4, 2]
del my_list[:]
print(my_list)
```

A lista fica vazia e o output é: `[]`.

A remoção do slice do código muda dramaticamente o seu significado.

Veja:
```
my_list = [10, 8, 6, 4, 2]
del my_list
print(my_list)
```

A instrução `del` **eliminará a lista em si, não o seu conteúdo**.

A `print()` invocação da função a partir da última linha do código causará então um erro de runtime.

## 3.6.1.6 Operações em listas | in, not in

## Os loops in e not in operadores

O Python oferece dois operadores muito poderosos, capazes de **olhar através da lista a fim de verificar se um valor específico está ou não armazenado dentro da lista**

Estes operadores são:
```
elem in my_list
elem not in my_list
```

O primeiro deles `(in)` verifica se um dado elemento (o seu argumento da esquerda) está atualmente armazenado algures dentro da lista (o argumento da direita) - o operador devolve `True` neste caso.

O segundo `(not in)` verifica se um dado elemento (o seu argumento da esquerda) está ausente numa lista - o operador devolve `True` neste caso.
<hr>

Veja o código no editor. O snippet mostra ambos os operadores em ação. Consegue adivinhar o seu output? Execute o programa para verificar se estava certo.
```
my_list = [0, 3, 12, 8, 2]

print(5 in my_list)
print(5 not in my_list)
print(12 in my_list)

Output

False
True
True

```

## 3.6.1.7 Listas - mais detalhes

## Listas - alguns programas simples

Agora queremos mostrar-lhe alguns programas simples que utilizam listas.

O primeiro deles tenta encontrar o maior valor na lista. Veja o código no editor.

O conceito é bastante simples - assumimos temporariamente que o primeiro elemento é o maior, e verificamos a hipótese contra todos os restantes elementos da lista.

O código fará o output `17` (como esperado).
<hr>

O código pode ser reescrito para fazer uso da forma recentemente introduzida do `for` :
```
my_list = [17, 3, 11, 5, 1, 9, 7, 15, 13]
largest = my_list[0]

for i in my_list:
    if i > largest:
        largest = i

print(largest)
```

O programa acima realiza uma comparação desnecessária, quando o primeiro elemento é comparado consigo mesmo, mas isto não é de todo um problema.

O código fará o output `17`, também (nada invulgar).
<hr>

Se precisar de poupar energia do computador, pode utilizar um slice:
```
my_list = [17, 3, 11, 5, 1, 9, 7, 15, 13]
largest = my_list[0]

for i in my_list[1:]:
    if i > largest:
        largest = i

print(largest)
```

A questão é: qual destas duas ações consome mais recursos informáticos - apenas uma comparação, ou slicing de quase todos os elementos de uma lista?

## 3.6.1.8 Listas - mais detalhes

## Listas - alguns programas simples

Agora vamos encontrar a localização de um dado elemento dentro de uma lista:
```
my_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
to_find = 5
found = False

for i in range(len(my_list)):
    found = my_list[i] == to_find
    if found:
        break

if found:
    print("Element found at index", i)
else:
    print("absent")
```

Nota:

* o valor alvo é armazenado na variável `to_find` ;
* o estado atual da pesquisa é armazenado na variável `found` (`True`/`False`)
* quando `found` se torna `True`, o loop `for` é saído.
<hr>

Vamos supor que escolheu os seguintes números na lotaria: `3`, `7`, `11`, `42`, `34`, `49`.

Os números que foram sorteados são: `5`, `11`, `9`, `42`, `3`, `49`.

A questão é: em quantos números é que acertou?

O programa dará a resposta:
```
drawn = [5, 11, 9, 42, 3, 49]
bets = [3, 7, 11, 42, 34, 49]
hits = 0

for number in bets:
    if number in drawn:
        hits += 1

print(hits)
```

Nota:

* a keyword drawn armazena todos os números sorteados;
* a lista bets armazena as suas apostas;
* a variável hits conta os seus êxitos.

O output do programa é: `4`.

## 3.6.1.10 RESUMO DA SEÇÃO

## Key takeaways

1. Se tiver uma lista `l1`, então a seguinte tarefa: `l2 = l1` não faz uma cópia da lista `l1` , mas faz com que as variáveis `l1` e `l2` **apontem para uma e a mesma lista na memória**. Por exemplo:
```
vehicles_one = ['car', 'bicycle', 'motor']
print(vehicles_one) # outputs: ['car', 'bicycle', 'motor']

vehicles_two = vehicles_one
del vehicles_one[0] # deletes 'car'
print(vehicles_two) # outputs: ['bicycle', 'motor']
```

2. Se quiser copiar uma lista ou parte da lista, pode fazê-lo executando **slicing**:
```
colors = ['red', 'green', 'orange']

copy_whole_colors = colors[:]  # copy the entire list
copy_part_colors = colors[0:2]  # copy part of the list
```

3. Também se podem utilizar **índices negativos** para executar slices. Por exemplo:
```
sample_list = ["A", "B", "C", "D", "E"]
new_list = sample_list[2:-1]
print(new_list)  # outputs: ['C', 'D']
```

4. O objeto da exceção `start` e `end` parâmetros são **opcionais** ao executar uma slice: `list[start:end]`, por exemplo.:
```
my_list = [1, 2, 3, 4, 5]
slice_one = my_list[2: ]
slice_two = my_list[ :2]
slice_three = my_list[-2: ]

print(slice_one)  # outputs: [3, 4, 5]
print(slice_two)  # outputs: [1, 2]
print(slice_three)  # outputs: [4, 5]
```

5. Pode **eliminar slices** usando a instrução `del` :
```
my_list = [1, 2, 3, 4, 5]
del my_list[0:2]
print(my_list)  # outputs: [3, 4, 5]

del my_list[:]
print(my_list)  # deletes the list content, outputs: []
```

6. Pode testar se alguns itens **existem numa lista ou não** usando as keywords `in` e `not` in, por exemplo.:
```
my_list = ["A", "B", 1, 2]

print("A" in my_list)  # outputs: True
print("C" not in my_list)  # outputs: True
print(2 not in my_list)  # outputs: False
```




**Exercício 1**

Qual é o output do seguinte snippet?
```
list_1 = ["A", "B", "C"]
list_2 = list_1
list_3 = list_2

del list_1[0]
del list_2[0]

print(list_3)
```

Verifique
`['C']`

**Exercício 2**

Qual é o output do seguinte snippet?
```
list_1 = ["A", "B", "C"]
list_2 = list_1
list_3 = list_2

del list_1[0]
del list_2

print(list_3)
```

Verifique
`['B', 'C']`

**Exercício 3**

Qual é o output do seguinte snippet?
```
list_1 = ["A", "B", "C"]
list_2 = list_1
list_3 = list_2

del list_1[0]
del list_2[:]

print(list_3)
```

Verifique
`[]`

**Exercício 4**

Qual é o output do seguinte snippet?
```
list_1 = ["A", "B", "C"]
list_2 = list_1[:]
list_3 = list_2[:]

del list_1[0]
del list_2[0]

print(list_3)
```
Verifique
`['A', 'B', 'C']`

**Exercício 5**

Insira in ou not in em vez de ??? para que o código faça output do resultado esperado.
```
my_list = [1, 2, "in", True, "ABC"]

print(1 ??? my_list)  # outputs True
print("A" ??? my_list)  # outputs True
print(3 ??? my_list)  # outputs True
print(False ??? my_list)  # outputs False
```
Verifique
```
my_list = [1, 2, "in", True, "ABC"]

print(1 in my_list)  # outputs True
print("A" not in my_list)  # outputs True
print(3 not in my_list)  # outputs True
print(False in my_list)  # outputs False

```
