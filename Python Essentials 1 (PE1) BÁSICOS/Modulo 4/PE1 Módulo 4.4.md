## 4.4.1.1 Scopes em Python

## Funções e scopes

Vamos começar com uma definição:

O **scope de um nome** (por exemplo, um nome de variável) é a parte de um código onde o nome é devidamente reconhecido.

Por exemplo, o scope do parâmetro de uma função é a própria função. O parâmetro é inacessível fora da função.

Vamos verificar. Veja o código no editor. O que acontecerá quando o executar?
```
def scope_test():
    x = 123


scope_test()
print(x)
```

O programa falhará quando executado. A mensagem de erro lerá:

output

`NameError: name 'x' is not defined`


Isto é de se esperar.

Vamos realizar consigo algumas experiências para lhe mostrar como o Python constrói os scopes, e como pode usar os seus hábitos em seu benefício.

## 4.4.1.2 Scopes em Python

## Funções e scopes: continuação

Vamos começar verificando se uma variável criada fora de qualquer função é ou não visível dentro das funções. Por outras palavras, o nome de uma variável propaga-se no corpo de uma função?

Veja o código no editor. A nossa cobaia está lá.
```
def my_function():
    print("Do I know that variable?", var)


var = 1
my_function()
print(var)
```

O resultado do teste é positivo - o código faz os outputs:

output

```
Do I know that variable? 1
1
```

A resposta é: **uma variável existente fora de uma função tem um scope dentro dos corpos das funções.**

Esta regra tem uma exceção muito importante. Vamos tentar encontrá-la.


Vamos fazer uma pequena alteração no código:
```
def my_function():
    var = 2
    print("Do I know that variable?", var)


var = 1
my_function()
print(var)
```

O resultado também mudou - o código produz um output ligeiramente diferente agora:

output

```
Do I know that variable? 2
1
```


O que aconteceu?

* a variável `var` criada dentro da função não é a mesmo que quando definida fora dela - parece que existem duas variáveis diferentes com o mesmo nome;
* além disso, a variável da função sombreia a variável proveniente do mundo exterior.

Podemos tornar a regra anterior mais precisa e adequada:

**Uma variável existente fora de uma função tem um scope dentro dos corpos das funções, excluindo aqueles que definem uma variável com o mesmo nome.**

Isto também significa que o **scope de uma variável existente fora de uma função só é suportado quando se obtém o seu valor** (reading). Atribuir um valor força a criação da própria variável da função.

Certifique-se de que entende bem isto e realize as suas próprias experiências.

## 4.4.1.3 Scopes em Python | global

## Funções e scopes: a keyword global .

Esperamos que agora tenha chegado à seguinte pergunta: isto significa que uma função não é capaz de modificar uma variável definida fora dela? Isso criaria muito desconforto.

Felizmente, a resposta é não.

Existe um método especial Python que pode **expandir o scope de uma variável de forma a incluir os corpos das funções** (mesmo que se pretenda não só ler os valores, mas também modificá-los).

Tal efeito é causado por uma keyword chamada `global`:
```
global name
global name1, name2, ...
```

Utilizar esta keyword dentro de uma função com o nome (ou nomes separados por vírgulas) de uma variável, força o Python a abster-se de criar uma nova variável dentro da função - a que é acessível a partir do exterior será utilizada em vez disso.

Por outras palavras, este nome torna-se global (tem um **scope global**, e não importa se é o assunto de leitura ou atribuição).


Veja o código no editor.

```
def my_function():
    global var
    var = 2
    print("Do I know that variable?", var)


var = 1
my_function()
print(var)
```

Adicionámos `global` à função.

O código agora faz o output:

output

```
Do I know that variable? 2
2
```


Isto deve ser prova suficiente para mostrar que a keyword global faz o que promete.

## 4.4.1.4 Scopes em Python

## Como a função interage com os seus argumentos

Vamos agora descobrir como a função interage com os seus argumentos.

O código no editor deve ensinar-lhe algo. Como se pode ver, a função altera o valor do seu parâmetro. A alteração afeta o argumento?

Execute o programa e verifique.
```
def my_function(n):
    print("I got", n)
    n += 1
    print("I have", n)


var = 1
my_function(var)
print(var)
```

O output do código é:

output

```
I got 1
I have 2
1
```

A conclusão é óbvia - **a alteração do valor do parâmetro não se propaga fora da função** (em qualquer caso, não quando a variável é uma escalar, como no exemplo).

Isto também significa que uma função recebe o **valor do argumento**, não o argumento em si. Isto é verdade para escalares.

Vale a pena verificar como funciona com listas (lembra-se das peculiaridades de atribuir slices de listas versus atribuir listas como um todo?).
<hr>

O exemplo a seguir irá lançar alguma luz sobre a questão:
```
def my_function(my_list_1):
    print("Print #1:", my_list_1)
    print("Print #2:", my_list_2)
    my_list_1 = [0, 1]
    print("Print #3:", my_list_1)
    print("Print #4:", my_list_2)


my_list_2 = [2, 3]
my_function(my_list_2)
print("Print #5:", my_list_2)
```

O output do código é:
```
Print #1: [2, 3]
Print #2: [2, 3]
Print #3: [0, 1]
Print #4: [2, 3]
Print #5: [2, 3]
```

Parece que a regra anterior ainda funciona.

Finalmente, pode ver a diferença no exemplo abaixo:
```
def my_function(my_list_1):
    print("Print #1:", my_list_1)
    print("Print #2:", my_list_2)
    del my_list_1[0]  # Pay attention to this line.
    print("Print #3:", my_list_1)
    print("Print #4:", my_list_2)


my_list_2 = [2, 3]
my_function(my_list_2)
print("Print #5:", my_list_2)
```

Não alteramos o valor do parâmetro `my_list_1` (já sabemos que isso não afetará o argumento), mas em vez disso modificará a lista identificada por ele..

O output pode ser surpreendente. Execute o código e verifique:
```
Print #1: [2, 3]
Print #2: [2, 3]
Print #3: [3]
Print #4: [3]
Print #5: [3]
```

Consegue explicá-lo?

Vamos tentar:

* se o argumento for uma lista, então alterar o valor do parâmetro correspondente não afeta a lista (lembre-se: as variáveis que contêm listas são armazenadas de uma forma diferente dos escalares),
* mas se alterar uma lista identificada pelo parâmetro (nota: a lista, não o parâmetro!), a lista irá refletir a alteração.

É tempo de escrever algumas funções de exemplo. Faremos na próxima seção.

## 4.4.1.5 RESUMO DA SECÇÃO

## Key takeaways

1. Uma variável que existe fora de uma função tem um scope dentro do corpo da função (Exemplo 1), a menos que a função defina uma variável com o mesmo nome (Exemplo 2, e Exemplo 3), por exemplo:

Exemplo 1:
```
var = 2


def mult_by_var(x):
    return x * var


print(mult_by_var(7))    # outputs: 14
```

Exemplo 2:
```
def mult(x):
    var = 5
    return x * var


print(mult(7))    # outputs: 35
```

Exemplo 3:
```
def mult(x):
    var = 7
    return x * var


var = 3
print(mult(7))    # outputs: 49
```

2. Uma variável que existe dentro de uma função tem um scope dentro do corpo da função (Exemplo 4), por exemplo:

Exemplo 4:
```
def adding(x):
    var = 7
    return x + var


print(adding(4))    # outputs: 11
print(var)    # NameError
```

3. Pode utilizar a keyword global seguida por um nome de variável para tornar o scope da variável global, por exemplo
```
var = 2
print(var)    # outputs: 2


def return_var():
    global var
    var = 5
    return var


print(return_var())    # outputs: 5
print(var)    # outputs: 5
```

Exercício 1

O que acontecerá quando tentar executar o seguinte código?
```
def message():
    alt = 1
    print("Hello, World!")


print(alt)

```
Verifique
A função `NameError` será lançada (`NameError: name 'alt' is not defined`)


Exercício 2

Qual é o output do seguinte snippet?
```
a = 1


def fun():
    a = 2
    print(a)


fun()
print(a)
```

Verifique
```
2
1
```

Exercício 3

Qual é o output do seguinte snippet?
```
a = 1


def fun():
    global a
    a = 2
    print(a)


fun()
a = 3
print(a)
```

Verifique
```
2
3
```

Exercício 4

Qual é o output do seguinte snippet?
```
a = 1


def fun():
    global a
    a = 2
    print(a)


a = 3
fun()
print(a)
```

Verifique
```
2
2
```



