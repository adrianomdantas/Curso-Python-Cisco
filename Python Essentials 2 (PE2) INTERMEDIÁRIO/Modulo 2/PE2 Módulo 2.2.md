## 2.2.1.1 A natureza das strings em Python

## Strings - uma breve revisão

Vamos fazer uma breve revisão sobre a natureza das strings do Python.

Em primeiro lugar, as strings do Python (ou simplesmente strings, pois não vamos discutir as strings de qualquer outra linguagem) são sequências imutáveis.

É muito importante notar isto, porque significa que se deve esperar algum comportamento familiar por parte delas.

Vamos analisar o código no editor para perceber do que estamos a falar:

* Observe o **Exemplo 1**. A função `len()` utilizada para strings devolve um número de carateres contidos pelos argumentos. O snippet faz o output `2`.
* Qualquer string pode estar vazia. O seu comprimento é de `0` então - assim como no **Exemplo 2**.
* Não se esqueça que uma barra invertida (`\`) utilizada como caratere de escape não está incluída no comprimento total da string. O código no `Exemplo 3`, portanto, gera o output `3`.

Execute os três códigos de exemplo e verifique.

```
# Example 1

word = 'by'
print(len(word))


# Example 2

empty = ''
print(len(empty))


# Example 3

i_am = 'I\'m'
print(len(i_am))
```

## 2.2.1.2 A natureza das strings em Python

## Strings multiline

Agora é um momento muito bom para lhe mostrar outra forma de especificar strings dentro do source code de Python. Note que a sintaxe que já conhece não o deixará usar uma string que ocupa mais do que uma linha de texto.

Por esta razão, o código aqui está errado:
```
multiline = 'Line #1
Line #2'

print(len(multiline))
```

Felizmente, para este tipo de strings, o Python oferece uma sintaxe separada, conveniente e simples.


Veja o código no editor. É este o seu aspeto.

Como pode ver, a string começa com três `apóstrofes`, não uma. A mesma apóstrofe tripla é utilizada para a terminar.

O número de linhas de texto colocadas dentro de tal string é arbitrário.

O snippet faz o output `15`.

Conte os carateres com cuidado. Este resultado está correto ou não? À primeira vista parece estar, mas quando se conta os carateres não está.

`Line #1` contém sete carateres. Duas dessas linhas compreendem 14 carateres. Perdemos um caratere? Onde? Como?

Não, não perdemos.

**O caratere que falta é simplesmente invisível - é um espaço em branco**. Ele está localizado entre as duas linhas de texto.

É denotado como: `\n`.

Lembra-se? É um caratere especial (de controlo) utilizado para **forçar uma line feed** (alimentação de linha) (daí o seu nome: LF). Não se consegue vê-lo, mas conta.

As strings multiline também podem ser delimitadas por **aspas triplas**, tal como aqui:

```
multiline = """Line #1
Line #2"""

print(len(multiline))
```

Escolha o método que lhe seja mais confortável. Ambos funcionam da mesma forma.

## 2.2.1.3 A natureza das strings em Python

## Operações em strings

Como outros tipos de dados, as strings têm o seu próprio conjunto de operações permitidas, embora sejam bastante limitadas em comparação com os números.

Em geral, as strings podem ser:

* **concatenadas** (juntas)
* **replicadas**.

A primeira operação é realizada pelo operador + (note: não é uma adição) enquanto a segunda pelo operador * (note novamente: não é uma multiplicação).

A capacidade de utilizar o mesmo operador contra tipos de dados completamente diferentes (como números vs. strings) chama-se overloading (visto tal operador estar sobrecarregado com tarefas diferentes).

Analise o exemplo:

```
str1 = 'a'
str2 = 'b'

print(str1 + str2)
print(str2 + str1)
print(5 * 'a')
print('b' * 4)
```

* O operador `+` utilizado contra duas ou mais strings produz uma nova string contendo todos os carateres dos seus argumentos (nota: a ordem importa - este `+` overloaded, em contraste com a sua versão numérica, **não é comutativa**)
* o operador `*` precisa de uma string e um número como argumentos; neste caso, a ordem não importa - pode colocar o número antes da string, ou vice-versa, o resultado será o mesmo - uma nova string criada pela enésima replicação da string do argumento.
O snippet produz o seguinte output:

```
ab
ba
aaaaa
bbbb
```


Nota: as variantes de atalho dos operadores acima referidos são também aplicáveis para strings (`+=` e `*=`).

## 2.2.1.4 A natureza das strings em Python

## Operações em strings: ord()

Se quiser **saber o valor do code point ASCII/UNICODE de um caratere específico**, pode usar uma função chamada `ord()` (como em ordinal).

A função precisa de uma **string de um único caratere como seu argumento** - violar este requisito causa uma exceção TypeError , e devolve um número que representa o code point do argumento.

Veja o código no editor, e execute-o. O snippet faz o output:

```
# Demonstrating the ord() function.

char_1 = 'a'
char_2 = ' '  # space

print(ord(char_1))
print(ord(char_2))
```

output

```
97
32
```

Agora atribua valores diferentes para `char_1` e `char_2`, por exemplo, `α` (alfa grego), e `ę` (uma letra no alfabeto polonês); em seguida execute o código e veja o resultado que ele produz. Realize as suas próprias experiências.

## 2.2.1.5 A natureza das strings em Python

## Operações em strings: chr()

Se conhece o code point (número) e pretende obter o caratere correspondente, pode utilizar uma função chamada `chr()`.

A função **toma um code point e devolve o seu caratere**.

Invocá-lo com um argumento inválido (por exemplo, um code point negativo ou inválido) causa ValueError ou TypeError exceções.

Execute o código no editor. O output do snippet de exemplo:

```
a
α
```

Nota:

* `chr(ord(x)) == x`
* `ord(chr(x)) == x`

Mais uma vez, faça as suas próprias experiências.

```
# Demonstrating the chr() function.

print(chr(97))
print(chr(945))
# Demonstrating the chr() function.
```

## 2.2.1.6 A natureza das strings em Python

## Strings como sequências: indexação

Dissemos-lhe antes que as **strings de Python são sequências**. É hora de lhe mostrar o que isso realmente significa.

As strings não são listas, mas **pode tratá-las como listas em muitos casos particulares**.

Por exemplo, se quiser aceder a qualquer um dos carateres de uma string, pode fazê-lo utilizando a **indexação**, tal como no exemplo abaixo. Execute o programa:

```
# Indexing strings.

the_string = 'silly walks'

for ix in range(len(the_string)):
    print(the_string[ix], end=' ')

print()
```

Tenha cuidado - não tente passar os limites de uma string - isso causará uma exceção.

O output do exemplo é:

`s i l l y   w a l k s`


A propósito, os índices negativos também se comportam como esperado. Verifique isto você mesmo.


## Strings como sequências: iteração

**Iterar através das strings** também funciona. Veja o exemplo abaixo:

```
# Iterating through a string.

the_string = 'silly walks'

for character in the_string:
    print(character, end=' ')

print()
```

O output é o mesmo que anteriormente. Verifique.

`s i l l y   w a l k s `

## 2.2.1.7 A natureza das strings em Python

## Slices

Além disso, tudo o que sabe sobre **slices** ainda é utilizável.

Reunimos alguns exemplos que mostram como as slices funcionam no mundo das strings. Olhe para o código no editor, analise-o e execute-o.

Não verá nada de novo no exemplo, mas queremos que tenha a certeza de que pode explicar todas as linhas do código.

```
# Slices

alpha = "abdefg"

print(alpha[1:3])
print(alpha[3:])
print(alpha[:3])
print(alpha[3:-2])
print(alpha[-3:4])
print(alpha[::2])
print(alpha[1::2])
```

O output do código é:

```
bd
efg
abd
e
e
adf
beg
```

Agora faça as suas próprias experiências.


## 2.2.1.8 A natureza das strings em Python

## Os loops Operadores in e not in .

**O operador** `in` .

O operador `in` não deve surpreendê-lo quando aplicado a strings - simplesmente **verifica se o seu argumento esquerdo (uma string) pode ser encontrado em qualquer lugar dentro do argumento direito (outra string)**.

O resultado da verificação é simplesmente `True` ou `False`.

Veja o programa de exemplo abaixo. É assim que o operador `in` funciona:

```
alphabet = "abcdefghijklmnopqrstuvwxyz"

print("f" in alphabet)
print("F" in alphabet)
print("1" in alphabet)
print("ghi" in alphabet)
print("Xyz" in alphabet)
```

O output do exemplo é:

```
True
False
False
True
False
```

**O método** `not in` .

Como provavelmente suspeita, o operador not in também é aplicável aqui.

É assim que funciona:

```
alphabet = "abcdefghijklmnopqrstuvwxyz"

print("f" not in alphabet)
print("F" not in alphabet)
print("1" not in alphabet)
print("ghi" not in alphabet)
print("Xyz" not in alphabet)
```

O output do exemplo é:

```
False
True
True
False
True
```

## 2.2.1.9 A natureza das strings em Python

## As strings de Python são imutáveis

Também lhe dissemos que **as strings de Python são imutáveis**. Esta é uma característica muito importante. O que significa isto?

Isto significa principalmente que a semelhança de strings e listas é limitada. Nem tudo o que se pode fazer com uma lista pode ser feito com uma string.

A primeira diferença importante **não lhe permite utilizar a instrução** `del` **para remover qualquer coisa de uma string.**

O exemplo aqui não vai funcionar:

```
alphabet = "abcdefghijklmnopqrstuvwxyz"
del alphabet[0]
```

A única coisa que pode fazer com `del` e uma string é **remover a string como um todo**. Tente fazê-lo.


As strings de Python **não têm o método** `append()` - não se pode expandi-las de forma alguma.

O exemplo abaixo está errado:

```
alphabet = "abcdefghijklmnopqrstuvwxyz"
alphabet.append("A")
```

com a ausência do método `append()` , **o método** `insert()` **é ilegal**, também:

```
alphabet = "abcdefghijklmnopqrstuvwxyz"
alphabet.insert(0, "A")
```

## 2.2.1.10 A natureza das strings em Python

## Operações em strings: continuação

Não pense que a imutabilidade de uma string limita a sua capacidade de operar com strings.

A única consequência é que tem de se lembrar disso, e implementar o seu código de uma forma ligeiramente diferente - veja o exemplo do código no editor.

Esta forma de código é totalmente aceitável, funcionará sem contornar as regras do Python, e trará o alfabeto latino completo para o seu ecrã:

`abcdefghijklmnopqrstuvwxyz`

Poderá perguntar-se se **a criação de uma nova cópia de uma string, cada vez que modifica o seu conteúdo, piora a eficácia do código.**

Sim, piora. Um pouco. No entanto, não é de todo um problema.

```
alphabet = "bcdefghijklmnopqrstuvwxy"

alphabet = "a" + alphabet
alphabet = alphabet + "z"

print(alphabet)
```

`abcdefghijklmnopqrstuvwxyz`

## 2.2.1.11 A natureza das strings em Python

## Operações em strings: min()

Agora que compreende que as strings são sequências, podemos mostrar-lhe algumas capacidades de sequência menos óbvias. Vamos apresentá-las utilizando strings, mas não se esqueça de que as listas também podem adotar os mesmos truques.

Vamos começar com uma função chamada `min()`.

A função **encontra o elemento mínimo da sequência passada como um argumento**. Há uma condição - a sequência (string, lista, não importa) **não pode estar vazia**, ou então terá uma exceção ValueError .

O programa do **Exemplo 1** tem como output:

`A`

Nota: É uma maiúscula A. Porquê? Lembre-se da tabela ASCII - que letras ocupam os primeiros locais - superior ou inferior?

Preparamos mais dois exemplos para analisar: **Exemplos 2 & 3**.

Como pode ver, eles apresentam mais do que apenas strings. O output esperado parece-se com o seguinte:

```
[ ]
0
```

Nota: usamos os parêntesis retos para evitar que o espaço seja negligenciado no ecrã.

```
# Demonstrating min() - Example 1:
print(min("aAbByYzZ"))


# Demonstrating min() - Examples 2 &amp; 3:
t = 'The Knights Who Say "Ni!"'
print('[' + min(t) + ']')

t = [0, 1, 2]
print(min(t))
```

## 2.2.1.12 A natureza das strings em Python

## Operações em strings: max()

Da mesma forma, uma função chamada `max()` **encontra o elemento máximo da sequência.**

Veja o Exemplo 1 no editor. O output do programa de exemplo:

`z`

Nota: É um *z* minúsculo.

Agora vamos ver a função `max()` aplicada aos mesmos dados que anteriormente. Veja os **Exemplos 2 & 3** no editor.

O output esperado é:

output

```
[y]
2
```

Realize as suas próprias experiências.

```
# Demonstrating max() - Example 1:
print(max("aAbByYzZ"))


# Demonstrating max() - Examples 2 &amp; 3:
t = 'The Knights Who Say "Ni!"'
print('[' + max(t) + ']')

t = [0, 1, 2]
print(max(t))
```

## 2.2.1.13 A natureza das strings em Python

## Operações em strings: o método index() .

A classe `index()` (é um método, não uma função) **pesquisa a sequência desde o início, a fim de encontrar o primeiro elemento do valor especificado no seu argumento.**

Nota: o elemento pesquisado deve ocorrer na sequência - **a sua ausência causará uma exceção** ValueError .

O método devolve o **index da primeira ocorrência do argumento** (o que significa que o menor resultado possível é 0, enquanto o maior é o comprimento do argumento decrescido por 1).

```
# Demonstrating the index() method:
print("aAbByYzZaA".index("b"))
print("aAbByYzZaA".index("Z"))
print("aAbByYzZaA".index("A"))
```

Portanto, o exemplo do editor dará o output:

```
2
7
1
```

## 2.2.1.14 A natureza das strings em Python

## Operações em strings: o método list() .

A função `list()` **toma o seu argumento (uma string) e cria uma nova lista contendo todos os carateres da string, um por elemento de lista**.

Nota: não é estritamente uma função string - `list()` é capaz de criar uma nova lista de muitas outras entidades (por exemplo, de tuples e dicionários).

Observe o exemplo de código no editor.

```
# Demonstrating the list() function:
print(list("abcabc"))

# Demonstrating the count() method:
print("abcabc".count("b"))
print('abcabc'.count("d"))
```

O output do exemplo:

`['a', 'b', 'c', 'a', 'b', 'c']`


## Operações em strings: o método count() .

A classe `count()` **conta todas as ocorrências do elemento dentro da sequência.** A ausência de tais elementos não causa problemas.

Veja o segundo exemplo no editor. Consegue adivinhar o seu output?

É:

output

```
2
0
```

Além disso, as strings em Python têm um número significativo de métodos destinados exclusivamente ao processamento de carateres. Não espere que funcionem com quaisquer outras coleções. A lista completa é apresentada aqui: https://docs.python.org/3.4/library/stdtypes.html#string-methods.

Vamos mostrar-lhe as que consideramos mais úteis.

## 2.2.1.15 RESUMO DA SECÇÃO

## Key takeaways

1. As strings de Python são **sequências imutáveis** e podem ser indexadas, sliced (cortadas) e iteradas como qualquer outra sequência, além de serem sujeitas aos operadores `in` e `not in` . Existem dois tipos de strings em Python:

* strings **one-line**, que não podem cruzar limites de linha - denotamo-las usando apóstrofes (`'string'`) ou aspas (`"string"`)
* strings **multi-line**, que ocupam mais de uma linha de source code, delimitadas por trígrafos:

```
'''
string
'''
```

ou

```
"""
string
"""
```

2. O comprimento de uma string é determinado pela função `len()` . O caratere de escape (`\`) não é contado. Por exemplo:

`print(len("\n\n"))`


tem como output 2.


1. As strings podem ser **concatenadas** usando o operador `+` e **replicadas** usando o operador `*` . Por exemplo:

```
asterisk = '*'
plus = "+"
decoration = (asterisk + plus) * 4 + asterisk
print(decoration)
```

tem como output `*+*+*+*+*`.


4. O par de funções chr() e ord() pode ser utilizado para criar um caratere usando o seu codepoint, e para determinar um codepoint correspondente a um caratere. Ambas as expressões a seguir são sempre verdadeiras:

chr(ord(character)) == character
ord(chr(codepoint)) == codepoint


5. Algumas outras funções que podem ser aplicadas a strings são:

list() — criar uma lista composta por todos os carateres da string;
max() — encontrar o caratere com o codepoint máximo;
min() — encontrar o caratere com o codepoint mínimo;

6. O método chamado index() encontra o index de uma determinada substring dentro da string.


**Exercício 1**

Qual é o comprimento da seguinte string supondo que não haja espaços em branco entre as aspas?

```
"""
"""
```

Verifique

`1`



**Exercício 2**

Qual é o output esperado do seguinte código?

```
s = 'yesteryears'
the_list = list(s)
print(the_list[3:6])
```

Verifique

`['t', 'e', 'r']`



**Exercício 3**

Qual é o output esperado do seguinte código?

```
for ch in "abc":
    print(chr(ord(ch) + 1), end='')
```

Verifique

`bcd`

## 2.3.1.1 Métodos de String

## Os loops capitalize() .

Vamos passar por alguns métodos padrão de string Python. Vamos atravessá-los por ordem alfabética - para ser honesto, qualquer ordem tem tantas desvantagens como vantagens, pelo que a escolha pode também ser aleatória.

O método `capitalize()` faz exatamente o que diz - **cria uma nova string cheia de carateres retirados da source string**, mas tenta modificá-los da seguinte forma:

* **se o primeiro caratere dentro da string for uma letra** (nota: o primeiro caratere é um elemento com um index igual a 0, não apenas o primeiro caratere visível), **será convertido para maiúsculas**;
* **todas as letras restantes da string serão convertidas em minúsculas.**

Não se esqueça:

* a string original (da qual o método é invocado) não é alterada de forma alguma (a imutabilidade de uma string deve ser obedecida sem reservas)
* a string modificada (capitalizada neste caso) é devolvida como resultado - se não a utilizar de qualquer forma (atribuí-la a uma variável, ou passá-la a uma função/método) ela desaparecerá sem deixar rasto.

Nota: os métodos não têm de ser invocados apenas de dentro das variáveis. Podem ser invocados diretamente de dentro de literais de string. Vamos utilizar regularmente essa convenção - simplificará os exemplos, uma vez que os aspetos mais importantes não desaparecerão entre as tarefas desnecessárias.

Veja o exemplo no editor. Execute-o.

```
# Demonstrating the capitalize() method:
print('aBcD'.capitalize())
```

Isto é o que ele imprime:

output

`Abcd`


Experimente alguns exemplos mais avançados e teste o seu output:

```
print("Alpha".capitalize())
print('ALPHA'.capitalize())
print(' Alpha'.capitalize())
print('123'.capitalize())
print("αβγδ".capitalize())
```

## 2.3.1.2 Métodos de String

## 