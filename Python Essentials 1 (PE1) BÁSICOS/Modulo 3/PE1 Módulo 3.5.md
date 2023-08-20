## 3.5.1.1 Ordenar listas simples - o algoritmo bubble sort

## O bubble sort

Agora que pode efetivamente fazer malabarismos com os elementos das listas, é tempo de aprender a **ordená-los**. Muitos algoritmos de ordenação foram inventados até agora, que diferem muito na velocidade, bem como na complexidade. Vamos mostrar-lhe um algoritmo muito simples, fácil de compreender, mas infelizmente também não muito eficiente. É utilizado muito raramente, e certamente não para listas grandes e extensas.

Digamos que uma lista pode ser ordenada de duas maneiras:

* crescente (ou mais precisamente - não decrescente) - se em cada par de elementos adjacentes, o primeiro elemento não for maior do que o segundo;
* decrescente (ou mais precisamente - não crescente) - se em cada par de elementos adjacentes, o primeiro elemento não for inferior ao segundo.

Nas secções seguintes, ordenaremos a lista por ordem crescente, de modo a que os números sejam ordenados do mais pequeno para o maior.

Aqui está a lista:
`[8, 10, 6, 2, 4]`

Tentaremos usar a seguinte abordagem: tomaremos o primeiro e o segundo elementos e iremos comparar-los; se determinarmos que estão na ordem errada (ou seja, o primeiro é maior que o segundo), iremos troca-los; se a sua ordem for válida, não faremos nada. Um olhar sobre a nossa lista confirma esta última - os elementos 01 e 02 estão na ordem correta, como em 8 < 10.

Agora olhe para o segundo e o terceiro elementos. Estão nas posições erradas. Temos de os trocar:

`[8, 6, 10, 2, 4]`

Vamos mais longe, e olhemos para o terceiro e quarto elementos. Novamente, não é assim que deveria ser. Temos de os trocar:

`[8, 6, 2, 10, 4]`

Agora verificamos o quarto e o quinto elementos. Sim, eles também estão nas posições erradas. Outra troca ocorre:

`[8, 6, 2, 4, 10]`

A primeira passagem pela lista já está terminada. Ainda estamos longe de terminar o nosso trabalho, mas algo de curioso aconteceu entretanto. O maior elemento, 10, já foi para o final da lista. Note que este é o lugar desejado para ele. Todos os elementos restantes formam uma confusão pitoresca, mas este já está no lugar.

Agora, por um momento, tente imaginar a lista de uma forma ligeiramente diferente - nomeadamente, assim:

|10|
|---|
|4|
|2|
|6|
|8|

Olhe - `10` está no topo. Poderíamos dizer que flutuou do fundo para a superfície, tal como a **bolha numa taça de champanhe**. O método de classificação deriva o seu nome da mesma observação - chama-se um **bubble sort** (uma espécie de bolha).

Agora começamos com a segunda passagem através da lista. Olhamos para o primeiro e segundo elementos - é necessária uma troca:

`[6, 8, 2, 4, 10]`
 
Tempo para o segundo e terceiro elementos: temos de os trocar também:

`[6, 2, 8, 4, 10]`


Agora o terceiro e quarto elementos, e a segunda passagem está terminada, visto `8` já estar no lugar:

`[6, 2, 4, 8, 10]`

Começamos a próxima passagem imediatamente. Observe cuidadosamente o primeiro e o segundo elementos - é necessária outra troca:

`[2, 6, 4, 8, 10]`

Agora `6` precisa de ser posto no lugar. Trocamos o segundo e o terceiro elementos:

`[2, 4, 6, 8, 10]`

A lista já está ordenada. Não temos mais nada a fazer. Isto é exatamente o que queremos.

Como pode ver, a essência deste algoritmo é simples: **comparamos os elementos adjacentes e, trocando alguns deles, atingimos o nosso objetivo**

Vamos codificar em Python todas as ações realizadas durante uma única passagem através da lista, e depois vamos considerar quantas passagens realmente precisamos para a realizar. Ainda não explicamos isto até agora, e faremos isso um pouco mais tarde.

## 3.5.1.2 Ordenar listas simples - o algoritmo bubble sort

## Classificar uma lista
Quantas passagens precisamos para ordenar a lista completa?

Resolvemos esta questão da seguinte forma: in**troduzimos outra variável**; a sua tarefa é observar se foi feita alguma troca durante a passagem ou não; se não houver troca, então a lista já está ordenada, e nada mais tem de ser feito. Criamos uma variável chamada `swapped`, e atribuímos-lhe um valor de `False` , para indicar que não há trocas. Caso contrário, será atribuído `True`.
```
my_list = [8, 10, 6, 2, 4]  # list to sort

for i in range(len(my_list) - 1):  # we need (5 - 1) comparisons
    if my_list[i] > my_list[i + 1]:  # compare adjacent elements
        my_list[i], my_list[i + 1] = my_list[i + 1], my_list[i]  # If we end up here, we have to swap the elements.
```

Deverá ser capaz de ler e compreender este programa sem quaisquer problemas:
```
my_list = [8, 10, 6, 2, 4]  # list to sort
swapped = True  # It's a little fake, we need it to enter the while loop.

while swapped:
    swapped = False  # no swaps so far
    for i in range(len(my_list) - 1):
        if my_list[i] > my_list[i + 1]:
            swapped = True  # a swap occurred!
            my_list[i], my_list[i + 1] = my_list[i + 1], my_list[i]

print(my_list)
```

Execute o programa e teste-o.

## 3.5.1.3 Ordenar listas simples - o algoritmo bubble sort

## O bubble sort - versão interativa

No editor pode ver um programa completo, enriquecido por uma conversa com o utilizador, e que permite ao utilizador introduzir e imprimir elementos da lista: **O bubble sort - versão interativa final**.
```
my_list = []
swapped = True
num = int(input("How many elements do you want to sort: "))

for i in range(num):
    val = float(input("Enter a list element: "))
    my_list.append(val)

while swapped:
    swapped = False
    for i in range(len(my_list) - 1):
        if my_list[i] > my_list[i + 1]:
            swapped = True
            my_list[i], my_list[i + 1] = my_list[i + 1], my_list[i]

print("\nSorted:")
print(my_list)

```

O Python, contudo, tem os seus próprios mecanismos de ordenação. Ninguém precisa de escrever a sua própria ordenação, uma vez que existe um número suficiente de **ferramentas prontas a usar**.

Explicamos-lhe este sistema de ordenação porque é importante aprender a processar o conteúdo de uma lista, e mostrar-lhe como a ordenação real pode funcionar.

Se quiser que o Python ordene a sua lista, pode fazê-lo desta forma:
```
my_list = [8, 10, 6, 2, 4]
my_list.sort()
print(my_list)
```

É tão simples quanto isso.

O output do snippet é o seguinte:

output
`[2, 4, 6, 8, 10]`

Como pode ver, todas as listas têm um método chamado sort(), que as classifica o mais rapidamente possível. Já aprendeu alguns dos métodos de lista antes, e vai aprender mais sobre outros muito em breve.

## 3.5.1.4 RESUMO DA SECÇÃO

## Key takeaways

1. Pode utilizar a keyword `sort()` para ordenar elementos de uma lista, por exemplo:
```
lst = [5, 3, 1, 2, 4]
print(lst)

lst.sort()
print(lst)  # outputs: [1, 2, 3, 4, 5]
```

2. Há também um método de lista chamado `reverse()`, que pode utilizar para inverter a lista, por exemplo
```
lst = [5, 3, 1, 2, 4]
print(lst)

lst.reverse()
print(lst)  # outputs: [4, 2, 1, 3, 5]
```



**Exercício 1**

Qual é o output do seguinte snippet?
```
lst = ["D", "F", "A", "Z"]
lst.sort()

print(lst)
```

Verifique
`['A', 'D', 'F', 'Z']`

**Exercício 2**

Qual é o output do seguinte snippet?
```
a = 3
b = 1
c = 2

lst = [a, c, b]
lst.sort()

print(lst)
```

Verifique
`[1, 2, 3]`

**Exercício 3**

Qual é o output do seguinte snippet?
```
a = "A"
b = "B"
c = "C"
d = " "

lst = [a, b, c, d]
lst.reverse()

print(lst)
```

Verifique
`[' ', 'C', 'B', 'A']`

