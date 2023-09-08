## 4.6.1.1 Tuplas e dicionários

## Tipos de sequência e mutabilidade

Antes de começarmos a falar sobre `tuplas` e `dicionários`, temos de introduzir dois conceitos importantes: tipos de `sequência` e `mutabilidade`.

Um **tipo de sequência é um tipo de dados em Python que é capaz de armazenar mais de um valor (ou menos de um, pois uma sequência pode estar vazia), e estes valores podem ser pesquisados sequencialmente (daí o nome)**, elemento a elemento.

Como o loop `for` é uma ferramenta especialmente concebida para iterar através de sequências, podemos expressar a definição como: **uma sequência é um dado que pode ser analisado pelo loop** `for` .

Até agora encontrou uma sequência Python - a lista. A lista é um exemplo clássico de uma sequência Python, embora existam outras sequências que vale a pena mencionar, e vamos agora apresentar-lhas.

A segunda noção - a **mutabilidade** - é uma propriedade de qualquer dado Python que descreve a sua disponibilidade para ser livremente alterado durante a execução do programa. Existem dois tipos de dados Python: **mutáveis** e **imutáveis**.

**Os dados mutáveis podem ser atualizados livremente a qualquer momento** - chamamos esta operação in situ.

In situ é uma frase em latim que se traduz literalmente para no local. Por exemplo, a instrução a seguir modifica os dados in situ:

`list.append(1)`

**Dados imutáveis não podem ser modificados desta maneira.**

Imagine que uma lista só pode ser atribuída e lida. Não seria possível anexar-lhe um elemento, nem remover qualquer elemento da mesma. Isto significa que anexar um elemento ao fim da lista exigiria a recriação da lista a partir do zero.

Teria de construir uma lista completamente nova, constituída por todos os elementos da lista já existente, mais o novo elemento.

O tipo de dados de que lhe queremos falar agora é um **tupla. Um tuple é um tipo de sequência imutável**. Pode comportar-se como uma lista, mas não pode ser modificado in situ.

## O que é um tupla?

A primeira e mais clara distinção entre listas e tuples é a sintaxe utilizada para as criar - as **tuplas preferem usar parêntesis curvos**, enquanto as listas gostam de ver parêntesis retos (colchetes), embora também seja **possível criar um tuple a partir de um conjunto de valores separados por vírgulas.**

Veja o exemplo:
```
tuple_1 = (1, 2, 4, 8)
tuple_2 = 1., .5, .25, .125
```

Existem dois tuples, ambos contendo **quatro elementos**.

Vamos imprimi-los:
```
tuple_1 = (1, 2, 4, 8)
tuple_2 = 1., .5, .25, .125

print(tuple_1)
print(tuple_2)
```

Isto é o que você deve ver no console:

output
```
(1, 2, 4, 8)
(1.0, 0.5, 0.25, 0.125)
```

Nota: **cada elemento tuple pode ser de um tipo diferente** (floating-point, inteiro, ou qualquer outro tipo de dados ainda não introduzidos).

## Como criar uma tupla?

É possível criar um tuple vazio - são necessários então parêntesis:

`empty_tuple = ()`


Se quiser criar uma **tupla de um elemento**, tem de levar em consideração o fato de que, devido a razões de sintaxe (um tuple tem de ser distinguível de um valor comum e único), tem de terminar o valor com uma vírgula:
```
one_element_tuple_1 = (1, )
one_element_tuple_2 = 1.,
```

A remoção das vírgulas não estragará o programa em nenhum sentido sintático, mas em vez disso obterá duas variáveis únicas, não tuples.

## 4.6.1.2 Tuples e dicionários

## Como usar uma tupla?

Se quiser obter os elementos de um tuple a fim de os ler, pode utilizar as mesmas convenções a que está habituado enquanto utiliza listas.

Observe o código no editor.

```
my_tuple = (1, 10, 100, 1000)

print(my_tuple[0])
print(my_tuple[-1])
print(my_tuple[1:])
print(my_tuple[:-2])

for elem in my_tuple:
    print(elem)
```

O programa deve produzir o seguinte output - execute-o e verifique:

output

```
1
1000
(10, 100, 1000)
(1, 10)
1
10
100
1000
```

As semelhanças podem ser enganadoras - **não tente modificar o conteúdo de um tuple!** Não é uma lista!

Todas estas instruções (exceto a mais acima) causarão um erro de runtime:
```
my_tuple = (1, 10, 100, 1000)

my_tuple.append(10000)
del my_tuple[0]
my_tuple[1] = -10
```

Esta é a mensagem que o Python lhe dará na janela de console:

output

`AttributeError: 'tuple' object has no attribute 'append'`


## 4.6.1.3 Tuples e dicionários

## Como usar um tuple: continuação

Que mais podem os tuples fazer por si?

* a função `len()` aceita tuples, e devolve o número de elementos contidos no seu interior;
* o operador `+` pode juntar tuples (já lhe mostrámos isto)
* o operador `*` pode multiplicar tuples, assim como listas;
* os operadores `in` e `not in` trabalham da mesma maneira que nas listas.

O snippet no editor apresenta-os a todos.
```
my_tuple = (1, 10, 100)

t1 = my_tuple + (1000, 10000)
t2 = my_tuple * 3

print(len(t2))
print(t1)
print(t2)
print(10 in my_tuple)
print(-10 not in my_tuple)
```

O output deve ter a seguinte aparência:

output

```
9
(1, 10, 100, 1000, 10000)
(1, 10, 100, 1, 10, 100, 1, 10, 100)
True
True
```

Uma das propriedades mais úteis da tuple é a sua capacidade de **aparecer no lado esquerdo do operador de atribuição**. Viu este fenômeno há algum tempo, quando foi necessário encontrar uma ferramenta elegante para trocar os valores de duas variáveis.

Observe o snippet abaixo:
```
var = 123

t1 = (1, )
t2 = (2, )
t3 = (3, var)

t1, t2, t3 = t2, t3, t1

print(t1, t2, t3)
```

Mostra três tuples que interagem - com efeito, os valores neles armazenados "circulam" - `t1` torna-se `t2`, `t2` torna-se `t3`, e `t3` torna-se `t1`.

Nota: o exemplo apresenta mais um fato importante: os **elementos de uma tupla podem ser variáveis**, e não apenas literais. Além disso, podem ser expressões se estiverem no lado direito do operador de atribuição.

## 4.6.1.4 Tuples e dicionários

## O que é um dicionário?

O **dicionário** é outra estrutura de dados Python. **Não é um tipo de sequência** (mas pode ser facilmente adaptado ao processamento de sequências) e é **mutável**.

Para explicar o que é realmente o dicionário Python, é importante compreender que se trata literalmente de um dicionário.

O dicionário Python funciona da mesma forma que **um dicionário bilingue**. Por exemplo, tem uma palavra inglesa (por exemplo, cat) e precisa do seu equivalente francês. Navega no dicionário para encontrar a palavra (pode usar diferentes técnicas para o fazer - não importa) e eventualmente obtém-na. A seguir, verifica o homólogo francês e é (muito provavelmente) a palavra "chat".

No mundo de Python, a palavra que se procura chama-se `key`. A palavra que obtém do dicionário chama-se um `value`.

Isto significa que um dicionário é um conjunto de pares de **key-values** (valores-chave). Nota:

* cada chave deve ser **única** - não é possível ter mais do que uma chave com o mesmo valor;
* uma chave pode ser **qualquer tipo de objeto imutável**: pode ser um número (inteiro ou float), ou mesmo uma string, mas não uma lista;
* um dicionário não é uma lista - uma lista contém um conjunto de valores numerados, enquanto que um **dicionário contém pares de valores**;
* a função `len()` funciona também para dicionários - devolve o número de elementos de key-value no dicionário;
* um dicionário é uma **ferramenta de sentido único** - se tiver um dicionário inglês-francês, pode procurar por equivalentes franceses de termos ingleses, mas não vice-versa.
Agora podemos mostrar-lhe alguns exemplos de trabalho.


## Como fazer um dicionário?

Se quiser atribuir alguns pares iniciais a um dicionário, deverá utilizar a seguinte sintaxe:
```
dictionary = {"cat": "chat", "dog": "chien", "horse": "cheval"}
phone_numbers = {'boss': 5551234567, 'Suzy': 22657854310}
empty_dictionary = {}

print(dictionary)
print(phone_numbers)
print(empty_dictionary)
```

No primeiro exemplo, o dicionário usa chaves e valores que são ambas strings. No segundo, as chaves são strings, mas os valores são inteiros. A disposição inversa (teclas → números, valores → strings) também é possível, bem como a combinação número-número.

A lista de pares é **rodeada por chavetas**, enquanto os pares em si são **separados por vírgulas**, e as chaves e valores por **dois pontos**.

O primeiro dos nossos dicionários é um dicionário inglês-francês muito simples. O segundo - uma diretoria telefónica muito pequena.

Os dicionários vazios são construídos por um **par vazio de chavetas** - nada de invulgar.


O dicionário como um todo pode ser impresso com uma única invocação `print()` . O snippet pode produzir o seguinte output:

output

```
{'dog': 'chien', 'horse': 'cheval', 'cat': 'chat'}
{'Suzy': 5557654321, 'boss': 5551234567}
{}
```

Notou alguma coisa surpreendente? A ordem dos pares impressos é diferente do que na atribuição inicial. O que é que isso significa?

Em primeiro lugar, é uma confirmação de que **os dicionários não são listas** - não preservam a ordem dos seus dados, uma vez que a ordem não tem qualquer significado (ao contrário do que acontece nos dicionários de papel reais). A ordem em que um dicionário **armazena os seus dados está completamente fora do seu controle**, e das suas expectativas. Isso é normal. (*)

**NOTA**

(*) Em Python 3.6x os dicionários tornaram-se coleções **ordenadas** por defeito. Os seus resultados podem variar dependendo da versão Python que estiver utilizando.

## 4.6.1.5 Tuples e dicionários

## Como usar um dicionário?

Se quiser obter algum dos valores, tem de entregar um key-value válido:
```
print(dictionary['cat'])
print(phone_numbers['Suzy'])
```

A obtenção do valor de um dicionário assemelha-se a uma indexação, especialmente graças aos parêntesis retos que rodeiam o valor da chave.

Nota:

* se a chave for uma string, é necessário especificá-la como uma string;
* **as chaves são sensíveis a maiúsculas e minúsculas:** `'Suzy'` é algo diferente de `'suzy'`.

O snippet produz duas linhas de texto:

output
```
chat
5557654321
```

E agora a notícia mais importante: **não se deve usar uma chave inexistente**. Tentar algo assim:

`print(phone_numbers['president'])`


causará um erro de runtime. Tente fazê-lo.


Felizmente, há uma maneira simples de evitar tal situação. O operador `in` , juntamente com o seu companheiro, `not in`, podem salvar esta situação.

O seguinte código procura com segurança algumas palavras francesas:
```
dictionary = {"cat": "chat", "dog": "chien", "horse": "cheval"}
words = ['cat', 'lion', 'horse']

for word in words:
    if word in dictionary:
        print(word, "->", dictionary[word])
    else:
        print(word, "is not in dictionary")
```

O output do código é o seguinte:

output

```
cat -> chat
lion is not in dictionary
horse -> cheval
```

**NOTA**

Quando se escreve uma expressão grande ou longa, pode ser uma boa ideia mantê-la verticalmente alinhada. É assim que pode tornar o seu código mais legível e mais fácil de programar, por exemplo
```
# Example 1:
dictionary = {
              "cat": "chat",
              "dog": "chien",
              "horse": "cheval"
              }

# Example 2:
phone_numbers = {'boss': 5551234567,
                 'Suzy': 22657854310
                 }
```

Tais formas de formatação de código são chamadas **hanging indents** (indentações penduradas).

## 4.6.1.6 Tuples e dicionários | métodos

## Como usar um dicionário: o keys()

Os dicionários podem ser **consultados** usando o loop `for` , como listas ou tuples?

Não e sim.

Não, porque um dicionário **não é um tipo de sequência** - o loop `for` é inútil com ele.

Sim, porque existem ferramentas simples e muito eficazes que podem **adaptar qualquer dicionário aos** `for` **requisitos do loop** (por outras palavras, construindo um link intermediário entre o dicionário e uma entidade de sequência temporária).

O primeiro deles é um método chamado `keys()`, possuído por cada dicionário. O método **devolve um objeto iterável que consiste em todas as chaves recolhidas dentro do dicionário**. Ter um grupo de chaves permite-lhe aceder a todo o dicionário de uma forma fácil e prática.

Tal como aqui:
```
dictionary = {"cat": "chat", "dog": "chien", "horse": "cheval"}

for key in dictionary.keys():
    print(key, "->", dictionary[key]
```

O output do código é o seguinte:

output

```
horse -> cheval
dog -> chien
cat -> chat
```

## O método sorted() .

Quer que seja **classificado**? Apenas enriqueça o loop `for` , para obter tal forma:

`for key in sorted(dictionary.keys()):`

A função `sorted()` fará o seu melhor - o output irá ficar assim:

output

```
cat -> chat
dog -> chien
horse -> cheval
```


## 4.6.1.7 Tuples e dicionários | métodos

## Como usar um dicionário: Os métodos items() e values() .

Outra forma é baseada na utilização de um método de dicionário chamado `items()`. O método **devolve tuplas** (este é o primeiro exemplo onde os tuples são algo mais do que apenas um exemplo de si mesmos) **onde cada tuple é um par key-value.**

É assim que funciona:
```
dictionary = {"cat": "chat", "dog": "chien", "horse": "cheval"}

for english, french in dictionary.items():
    print(english, "->", french)
```

Note-se a forma como o tuple foi utilizado como uma `for` variável de loop.

O exemplo imprime:
output
```
cat -> chat
dog -> chien
horse -> cheval
```

Há também um método chamado `values()`, que funciona de forma semelhante a `keys()`, mas **devolve valores**.

Aqui está um exemplo simples:
```
dictionary = {"cat": "chat", "dog": "chien", "horse": "cheval"}

for french in dictionary.values():
    print(french)
```

Como o dicionário não consegue encontrar automaticamente uma chave para um determinado valor, o papel deste método é bastante limitado.

Este é o output esperado:

output

```
cheval
chien
chat
```

## 4.6.1.8 Tuples e dicionários

## Como utilizar um dicionário: modificar e adicionar valores

Atribuir um novo valor a uma chave existente é simples - visto os dicionários serem totalmente **mutáveis**, não há obstáculos para os modificar.

Vamos substituir o valor `"chat"` com `"minou"`, o que não é muito preciso, mas funcionará bem com o nosso exemplo.

Veja:
```
dictionary = {"cat": "chat", "dog": "chien", "horse": "cheval"}

dictionary['cat'] = 'minou'
print(dictionary)
```

O output é:

output

`{'cat': 'minou', 'dog': 'chien', 'horse': 'cheval'}`

## Adicionar uma nova chave

Adicionar um novo par key-value a um dicionário é tão simples como alterar um valor - basta atribuir um valor a uma nova **chave, previamente inexistente.**

Nota: este é um comportamento muito diferente em relação às listas, que não permitem atribuir valores a índices inexistentes.

Vamos adicionar um novo par de palavras ao dicionário - um pouco estranho, mas ainda assim válido:
```
dictionary = {"cat": "chat", "dog": "chien", "horse": "cheval"}

dictionary['swan'] = 'cygne'
print(dictionary)
```

O output do exemplo:

output

`{'cat': 'chat', 'dog': 'chien', 'horse': 'cheval', 'swan': 'cygne'}`

**EXTRA**

Também pode inserir um item num dicionário utilizando o método `update()` , por exemplo:
```
dictionary = {"cat": "chat", "dog": "chien", "horse": "cheval"}

dictionary.update({"duck": "canard"})
print(dictionary)
```

## Remover uma chave

Consegue adivinhar como se remove uma chave de um dicionário?

Nota: remover uma chave causará sempre a **remoção do valor associado. Valores não podem existir sem as suas chaves.**

Isto é feito com a `del` instrução.

Aqui está o exemplo:
```
dictionary = {"cat": "chat", "dog": "chien", "horse": "cheval"}

del dictionary['dog']
print(dictionary)
```

Nota: `a remoção de uma chave não existente causa um erro.`

O output do exemplo:

output

`{'cat': 'chat', 'horse': 'cheval'}`


**EXTRA**

Para remover o último item num dicionário, pode-se utilizar o método `popitem()` :
```
dictionary = {"cat": "chat", "dog": "chien", "horse": "cheval"}

dictionary.popitem()
print(dictionary)    # outputs: {'cat': 'chat', 'dog': 'chien'}
```

Nas versões mais antigas do Python, ou seja, antes do 3.6.7, o método `popitem()` remove um item aleatório de um dicionário.

## 4.6.1.9 Tuplas e dicionários

## Tuplas e dicionários podem trabalhar em conjunto

Preparamos um exemplo simples, mostrando como tuples e dicionários podem trabalhar em conjunto.

Vamos imaginar o seguinte problema:

* é necessário um programa para avaliar as notas médias dos alunos;
* o programa deve pedir o nome do aluno, seguido da sua pontuação única;
* Os nomes podem ser indicados em qualquer ordem;
* a introdução de um nome vazio termina a introdução dos dados (nota 1: a introdução de uma pontuação vazia levantará a exceção ValueError, mas não se preocupe com isso agora, verá como lidar com tais casos quando falarmos de exceções na segunda parte da série de cursos Python Essentials)
* uma lista de todos os nomes, juntamente com a pontuação média avaliada, deve então ser emitida.

Veja o código no editor. Esta é a forma de o fazer.

```
school_class = {}

while True:
    name = input("Enter the student's name: ")
    if name == '':
        break
    
    score = int(input("Enter the student's score (0-10): "))
    if score not in range(0, 11):
	    break
    
    if name in school_class:
        school_class[name] += (score,)
    else:
        school_class[name] = (score,)
        
for name in sorted(school_class.keys()):
    adding = 0
    counter = 0
    for score in school_class[name]:
        adding += score
        counter += 1
    print(name, ":", adding / counter)
```

Agora, vamos analisá-lo linha a linha:

* **linha 1**: criar um dicionário vazio para os dados introduzidos; o nome do aluno é usado como chave, enquanto todas as notas associadas são armazenadas num tuple (o tuple pode ser um valor de dicionário - isso não é um problema)
* **linha 3**: entrar num loop "infinito" (não se preocupe, vai quebrar-se no momento certo)
* **linha 4**: ler o nome do aluno aqui;
* **linha 5-6**: se o nome for uma string vazia (` `), leave the loop;
* **linha 8**: pedir uma das pontuações do aluno (um inteiro do intervalo 0-10)
* **linha 9-10**: se a pontuação introduzida não estiver dentro do intervalo de 0 a 10, deixar o loop;
* **linha 12-13**: se o nome do aluno já estiver no dicionário, alongar o tuple associado com a nova pontuação (note o operador +=)
* **linha 14-15**: se este for um novo aluno (desconhecido do dicionário), criar uma nova entrada - o seu valor é um tuple de um elemento contendo a pontuação introduzida;
* **linha 17**: iterar através dos nomes dos alunos ordenados;
* **linha 18-19**: inicializar os dados necessários para avaliar a média (soma e contador)
* **linha 20-22**: iteramos através do tuple, tomando todas as pontuações subsequentes e atualizando a soma, juntamente com o contador;
* **linha 23**: avaliar e imprimir o nome e a pontuação média do aluno.
Este é um registo de uma conversa que tivemos com o nosso programa:

output
```
Enter the student's name: Bob
Enter the student's score (0-10): 7
Enter the student's name: Andy
Enter the student's score (0-10): 3
Enter the student's name: Bob
Enter the student's score (0-10): 2
Enter the student's name: Andy
Enter the student's score (0-10): 10
Enter the student's name: Andy
Enter the student's score (0-10): 3
Enter the student's name: Bob
Enter the student's score (0-10): 9
Enter the student's name:
Andy : 5.333333333333333
Bob : 6.0
```

## 4.6.1.10 RESUMO DA SEÇÃO (1/3)

## Key takeaways: tuplas

1. As **tuplas** são coleções de dados ordenados e imutáveis. Podem ser imaginados como listas imutáveis. São escritos entre parêntesis curvos:
```
my_tuple = (1, 2, True, "a string", (3, 4), [5, 6], None)
print(my_tuple)

my_list = [1, 2, True, "a string", (3, 4), [5, 6], None]
print(my_list)
```

Cada elemento tuple pode ser de um tipo diferente (ou seja, inteiros, strings, booleanos, etc.). Além disso, os tuples podem conter outros tuples ou listas (e o inverso).

2. Pode-se criar um tuple vazio como este:
```
empty_tuple = ()
print(type(empty_tuple))    # outputs: <class 'tuple'>
```

3. Um tuple de um elemento pode ser criado da seguinte forma:
```
one_elem_tuple_1 = ("one", )    # Brackets and a comma.
one_elem_tuple_2 = "one",       # No brackets, just a comma.
```

Se remover a vírgula, dirá ao Python para criar uma **variável** e não um tuple:
```
my_tuple_1 = 1, 
print(type(my_tuple_1))    # outputs: <class 'tuple'>

my_tuple_2 = 1             # This is not a tuple.
print(type(my_tuple_2))    # outputs: <class 'int'>
```

4. Pode aceder aos elementos do tuple através da indexação:
```
my_tuple = (1, 2.0, "string", [3, 4], (5, ), True)
print(my_tuple[3])    # outputs: [3, 4]
```

5. Os tuples são **imutáveis**, o que significa que não se pode alterar os seus elementos (não se pode anexar tuples, ou modificar, ou remover elementos tuple). O snippet a seguir causará uma exceção:
```
my_tuple = (1, 2.0, "string", [3, 4], (5, ), True)
my_tuple[2] = "guitar"    # The TypeError exception will be raised.
```

No entanto, é possível apagar um tuple como um todo:
```
my_tuple = 1, 2, 3, 
del my_tuple
print(my_tuple)    # NameError: name 'my_tuple' is not defined
```

6. Pode fazer um loop através dos elementos de um tuple (Exemplo 1), verificar se um elemento específico está (ou não) presente num tuple (Exemplo 2), utilizar a função `len()` para verificar quantos elementos existem num tuple (Exemplo 3), ou mesmo juntar/multiplicar tuples (Exemplo 4):
```
# Example 1
tuple_1 = (1, 2, 3)
for elem in tuple_1:    
    print(elem)

# Example 2
tuple_2 = (1, 2, 3, 4)
print(5 in tuple_2)
print(5 not in tuple_2)

# Example 3
tuple_3 = (1, 2, 3, 5)
print(len(tuple_3))

# Example 4
tuple_4 = tuple_1 + tuple_2
tuple_5 = tuple_3 * 2

print(tuple_4)
print(tuple_5)
```

**EXTRA**

Também pode criar uma tupla usando uma função Python incorporada chamada `tuple()`. Isto é particularmente útil quando se pretende converter um certo iterável (por exemplo, uma lista, range, string, etc.) num tuple:
```
my_tuple = tuple((1, 2, "string"))
print(my_tuple)

my_list = [2, 4, 6]
print(my_list)    # outputs: [2, 4, 6]
print(type(my_list))    # outputs: <class 'list'>
tup = tuple(my_list)
print(tup)    # outputs: (2, 4, 6)
print(type(tup))    # outputs: <class 'tuple'>
```

Da mesma forma, quando se pretende converter um iterável numa lista, pode-se usar uma função Python integrada chamada `list()`:
```
tup = 1, 2, 3, 
my_list = list(tup)
print(type(my_list))    # outputs: <class 'list'>
```

## 4.6.1.10 RESUMO DA SEÇÃO (2/3)

## Key takeaways: dicionários

1. Os dicionários são coleções de dados desordenados*, alteráveis (mutáveis), e indexados. (*Em Python 3.6x, os dicionários tornaram-se ordenados por defeito.

Cada dicionário é um conjunto de chaves: pares de valores. Pode criá-lo usando a seguinte sintaxe:
```
my_dictionary = {
    key1: value1,
    key2: value2,
    key3: value3,
    }
```

2. Se quiser aceder a um item de dicionário, pode fazê-lo fazendo referência à sua chave dentro de um par de parêntesis retos (ex. 1) ou usando o método get() (ex. 2):
```
pol_eng_dictionary = {
    "kwiat": "flower",
    "woda": "water",
    "gleba": "soil"
    }

item_1 = pol_eng_dictionary["gleba"]    # ex. 1
print(item_1)    # outputs: soil

item_2 = pol_eng_dictionary.get("woda")
print(item_2)    # outputs: water
```

3. Se quiser alterar o valor associado a uma chave específica, pode fazê-lo referindo-se ao nome da chave do item da seguinte forma:
```
pol_eng_dictionary = {
    "zamek": "castle",
    "woda": "water",
    "gleba": "soil"
    }

pol_eng_dictionary["zamek"] = "lock"
item = pol_eng_dictionary["zamek"]    
print(item)  # outputs: lock
```

4. Para adicionar ou remover uma chave (e o valor associado), utilize a seguinte sintaxe:
```
phonebook = {}    # an empty dictionary

phonebook["Adam"] = 3456783958    # create/add a key-value pair
print(phonebook)    # outputs: {'Adam': 3456783958}

del phonebook["Adam"]
print(phonebook)    # outputs: {}
```

Também pode inserir um item num dicionário utilizando o método `update()` , e remover o último elemento usando o método `popitem()` , por exemplo:
```
pol_eng_dictionary = {"kwiat": "flower"}

pol_eng_dictionary.update({"gleba": "soil"})
print(pol_eng_dictionary)    # outputs: {'kwiat': 'flower', 'gleba': 'soil'}

pol_eng_dictionary.popitem()
print(pol_eng_dictionary)    # outputs: {'kwiat': 'flower'}
```

5. Pode utilizar o loop for para percorrer um dicionário, por exemplo:
```
pol_eng_dictionary = {
    "zamek": "castle",
    "woda": "water",
    "gleba": "soil"
    }

for item in pol_eng_dictionary:
    print(item) 

# outputs: zamek
#          woda
#          gleba
```


6. Se quiser percorrer as chaves e valores de um dicionário, pode usar o método `items()` , por exemplo:
```
pol_eng_dictionary = {
    "zamek": "castle",
    "woda": "water",
    "gleba": "soil"
    }

for key, value in pol_eng_dictionary.items():
    print("Pol/Eng ->", key, ":", value)

```
7. Para verificar se uma determinada chave existe num dicionário, pode utilizar a `in` keyword:
```
pol_eng_dictionary = {
    "zamek": "castle",
    "woda": "water",
    "gleba": "soil"
    }

if "zamek" in pol_eng_dictionary:
    print("Yes")
else:
    print("No")
```

8. Pode utilizar a keyword `del` para remover um item específico, ou apagar um dicionário. Para remover todos os itens do dicionário, é necessário utilizar o `clear()` método:
```
pol_eng_dictionary = {
    "zamek": "castle",
    "woda": "water",
    "gleba": "soil"
    }

print(len(pol_eng_dictionary))    # outputs: 3
del pol_eng_dictionary["zamek"]    # remove an item
print(len(pol_eng_dictionary))    # outputs: 2

pol_eng_dictionary.clear()   # removes all the items
print(len(pol_eng_dictionary))    # outputs: 0

del pol_eng_dictionary    # removes the dictionary
```

9. Para copiar um dicionário, use o `copy()` método:
```
pol_eng_dictionary = {
    "zamek": "castle",
    "woda": "water",
    "gleba": "soil"
    }

copy_dictionary = pol_eng_dictionary.copy()
```
## 4.6.1.12 RESUMO DA SEÇÃO (3/3)

## Key takeaways: tuples e dicionários

Exercício 1

O que acontece quando se tenta executar o seguinte snippet?

my_tup = (1, 2, 3)
print(my_tup[2])


Verifique
O programa irá imprimir 3 para o ecrã.


Exercício 2

Qual é o output do seguinte snippet?

tup = 1, 2, 3
a, b, c = tup

print(a * b * c)


Verifique
O programa irá imprimir 6 para o ecrã. Os elementos do tuple tup foram “descompactados” nas a, b, e c variáveis.


Exercício 3

Complete o código para utilizar corretamente o método count() para encontrar o número de duplicados de 2 no seguinte tuple.

tup = 1, 2, 3, 2, 4, 5, 6, 2, 7, 2, 8, 9
duplicates = # Write your code here.

print(duplicates)    # outputs: 4


Verifique
tup = 1, 2, 3, 2, 4, 5, 6, 2, 7, 2, 8, 9
duplicates = tup.count(2)

print(duplicates)    # outputs: 4


Exercício 4

Escreva um programa que irá "colar" os dois dicionários (d1 e d2) e criar um novo (d3).

d1 = {'Adam Smith': 'A', 'Judy Paxton': 'B+'}
d2 = {'Mary Louis': 'A', 'Patrick White': 'C'}
d3 = {}

for item in (d1, d2):
    # Write your code here.

print(d3)


Verifique
Solução de amostra:
d1 = {'Adam Smith': 'A', 'Judy Paxton': 'B+'}
d2 = {'Mary Louis': 'A', 'Patrick White': 'C'}
d3 = {}

for item in (d1, d2):
    d3.update(item)

print(d3)




Exercício 5

Escreva um programa que irá converter a lista my_list num tuple.

my_list = ["car", "Ford", "flower", "Tulip"]

t =  # Write your code here.
print(t)


Verifique
Solução de amostra:
my_list = ["car", "Ford", "flower", "Tulip"]

t = tuple(my_list)
print(t)


Exercício 6

Escreva um programa que irá converter o tuple colors num dicionário.

colors = (("green", "#008000"), ("blue", "#0000FF"))

# Write your code here.

print(colors_dictionary)


Verifique
Solução de amostra:
colors = (("green", "#008000"), ("blue", "#0000FF"))

colors_dictionary = dict(colors)
print(colors_dictionary)


Exercício 7

O que acontecerá quando executar o seguinte código?

my_dictionary = {"A": 1, "B": 2}
copy_my_dictionary = my_dictionary.copy()
my_dictionary.clear()

print(copy_my_dictionary)


Verifique
O programa irá imprimir {'A': 1, 'B': 2} para o ecrã.


Exercício 8

Qual é o output do seguinte programa?

colors = {
    "white": (255, 255, 255),
    "grey": (128, 128, 128),
    "red": (255, 0, 0),
    "green": (0, 128, 0)
    }

for col, rgb in colors.items():
    print(col, ":", rgb)


Verifique
white : (255, 255, 255)
grey : (128, 128, 128)
red : (255, 0, 0)
green : (0, 128, 0)

## 4.6.2.1 PROJETO: Tic-Tac-Toe
## 4.6.2.2 Conclusão do Módulo

## Parabéns! Completou o Módulo 4.

Muito bem! Chegou ao fim do Módulo 4 e completou um marco importante na sua educação em programação Python. Aqui está um breve resumo dos objetivos que abordou e com os quais se familiarizou no Módulo 4:

* a definição e utilização de funções - a sua fundamentação, finalidade, convenções, e armadilhas;
* o conceito de passar argumentos de diferentes maneiras e definir os seus valores por defeito, juntamente com os mecanismos de devolução dos resultados da função;
* questões relativas ao scope do nome;
* novos agregados de dados: tuples e dicionários, e o seu papel no processamento de dados.

Está agora pronto para fazer o quiz do módulo e tentar o desafio final: Teste do Módulo 4, que o ajudará a avaliar o que aprendeu até agora.

