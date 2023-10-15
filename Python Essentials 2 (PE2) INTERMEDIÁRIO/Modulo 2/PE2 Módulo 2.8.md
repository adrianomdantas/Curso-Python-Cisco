## 2.8.1.1 Exceções úteis

## Exceções integradas

Vamos mostrar-lhe uma pequena lista das exceções mais úteis. Embora possa parecer estranho chamar "útil" a uma coisa ou fenómeno que é um sinal visível de fracasso ou contratempo, como sabe, errar é humano, e se algo pode correr mal, correrá mal.

As exceções são tão rotineiras e normais como qualquer outro aspeto da vida de um programador.

Para cada exceção, mostraremos:

* o seu nome;
* a sua localização na árvore de exceção;
* uma breve descrição;
* um snippet conciso de código mostrando as circunstâncias em que a exceção pode ser levantada.

Há muitas outras exceções a explorar - simplesmente não temos espaço para as explorar todas.

**ArithmeticError**

**Localização:** `BaseException ← Exception ← ArithmeticError`

**Descrição:** uma exceção abstrata incluindo todas as exceções causadas por operações aritméticas como a divisão zero ou o domínio inválido de um argumento

**AssertionError**

**Localização:** `BaseException ← Exception ← AssertionError`

**Descrição:** uma exceção concreta levantada pela instrução assert quando a sua argumentação avalia para `False`, `None`, `0`, ou uma string vazia

**Código:**
```
from math import tan, radians
angle = int(input('Enter integral angle in degrees: '))

# We must be sure that angle != 90 + k * 180
assert angle % 180 != 90
print(tan(radians(angle)))
```


**BaseException**

**Localização:** `BaseException`

Descrição: mais geral (abstrata) de todas as exceções Python - todas as outras exceções estão incluídas nesta; pode dizer-se que os doss seguintes except ramos são equivalentes: `except:` e `except BaseException:`.

**IndexError**

**Localização:** `BaseException ← Exception ← LookupError ← IndexError`

**Descrição:** uma exceção concreta levantada quando se tenta aceder a um elemento de uma sequência inexistente (por exemplo, o elemento de uma lista)

Código:

```
# The code shows an extravagant way
# of leaving the loop.

the_list = [1, 2, 3, 4, 5]
ix = 0
do_it = True

while do_it:
    try:
        print(the_list[ix])
        ix += 1
    except IndexError:
        do_it = False

print('Done')
```

## 2.8.1.2 Exceções úteis

## KeyboardInterrupt

**Localização:** `BaseException ← KeyboardInterrupt`

**Descrição:** uma exceção concreta levantada quando o utilizador utiliza um atalho de teclado concebido para terminar a execução de um programa (Ctrl-C na maioria dos sistemas operativos); se o tratamento desta exceção não levar à conclusão do programa, o programa continua a sua execução.

Nota: esta exceção não é derivada da Exception classe. Execute o programa em IDLE.

**Código:**

```
# This code cannot be terminated
# by pressing Ctrl-C.

from time import sleep

seconds = 0

while True:
    try:
        print(seconds)
        seconds += 1
        sleep(1)
    except KeyboardInterrupt:
        print("Don't do that!")
```

**LookupError**

**Localização:** `BaseException ← Exception ← LookupError`

**Descrição:** uma exceção abstrata incluindo todas as exceções causadas por erros resultantes de referências inválidas a diferentes coleções (listas, dicionários, tuples, etc.)

**MemoryError**

**Localização:** `BaseException ← Exception ← MemoryError`

**Descrição:** uma exceção concreta levantada quando uma operação não pode ser concluída devido a uma falta de memória livre.

**Código:**

```
# This code causes the MemoryError exception.
# Warning: executing this code may affect your OS.
# Don't run it in production environments!

string = 'x'
try:
    while True:
        string = string + string
        print(len(string))
except MemoryError:
    print('This is not funny!')
```

**OverflowError**
**Localização:** `BaseException ← Exception ← ArithmeticError ← OverflowError`

**Descrição:** uma exceção concreta levantada quando uma operação produz um número demasiado grande para ser armazenado com sucesso

**Código:**

```
# The code prints subsequent
# values of exp(k), k = 1, 2, 4, 8, 16, ...

from math import exp

ex = 1

try:
    while True:
        print(exp(ex))
        ex *= 2
except OverflowError:
    print('The number is too big.')
```

## 2.8.1.3 Exceções úteis

## ImportError

**Localização:** `BaseException ← Exception ← StandardError ← ImportError`

**Descrição:** uma exceção concreta levantada quando uma operação de importação falha

**Código:**

```
# One of these imports will fail - which one?

try:
    import math
    import time
    import abracadabra

except:
    print('One of your imports has failed.')
```


**KeyError**

**Localização:** `baseException ← Exceção ← LookuPerror ← KeyError`

**Descrição:** uma exceção concreta levantada quando se tenta aceder ao elemento inexistente de uma coleção (por exemplo, o elemento de um dicionário)

**Código:**
```
# How to abuse the dictionary
# and how to deal with it?

dictionary = { 'a': 'b', 'b': 'c', 'c': 'd' }
ch = 'a'

try:
    while True:
        ch = dictionary[ch]
        print(ch)
except KeyError:
    print('No such key:', ch)
```

Por agora acabámos com as exceções, mas voltarão quando discutirmos a programação orientada ao objeto em Python. Pode utilizá-las para proteger o seu código contra acidentes graves, mas também tem de aprender a mergulhar nelas, explorando a informação que transportam.

As exceções são de facto objetos - no entanto, nada podemos dizer sobre este aspeto até lhe apresentarmos classes, objetos, e afins.

Por enquanto, se quiser saber mais sobre exceções por si próprio, consulte a Biblioteca Padrão Python em https://docs.python.org/3.6/library/exceptions.html.

## 2.8.1.4 Ler ints em segurança
## 2.8.1.5 RESUMO DA SECÇÃO

## Key takeaways

1. Algumas exceções abstratas incorporadas em Python são:

* `ArithmeticError`,
* `BaseException`,
* `LookupError`.

2. Algumas exceções concretamente incorporadas em Python são:

* `AssertionError`,
* `ImportError`,
* `IndexError`,
* `KeyboardInterrupt`,
* `KeyError`,
* `MemoryError`,
* `OverflowError`.


**Exercício 1**

Qual das exceções irá utilizar para proteger o seu código de ser interrompido pelo uso do teclado?

Verifique

`KeyboardInterrupt`


**Exercício 2**

Qual é o nome da exceção mais geral de todas em Python?

Verifique

`BaseException`


**Exercício 3**

Qual das excepções será levantada através da seguinte avaliação mal sucedida?

`huge_value = 1E250 ** 2`

Verifique

`OverflowError`

## 2.8.1.6 Conclusão do Módulo

## Parabéns! Completou o PE2: Módulo 2.

Muito bem! Chegou ao fim do Módulo 2 e completou um marco importante na sua educação em programação Python. Aqui está um breve resumo dos objetivos que abordou e com os quais se familiarizou no Módulo 2:

* carateres, strings, e padrões de codificação;
* a natureza das strings em Python; strings vs. listas - semelhanças e diferenças;
* métodos de lista e string;
* manipulação de erros em Python;
* controlar o fluxo de erros usando try e except;
* a hierarquia das exceções; revisão das exceções mais úteis.

Está agora pronto para fazer o quiz do módulo e tentar o desafio final: Teste do Módulo 2, que o ajudará a avaliar o que aprendeu até agora.