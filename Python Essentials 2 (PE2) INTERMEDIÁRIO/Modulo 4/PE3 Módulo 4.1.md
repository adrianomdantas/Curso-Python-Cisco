## Python Essentials 2 - Módulo 4

## Python Essentials 2:
## Módulo 4

Diversos

Neste módulo, aprenderá sobre:

* Geradores, iteradores e closures;
* Trabalhar com sistemas-ficheiro, árvore de diretorias e ficheiros;
* Módulos selecionados da Biblioteca Padrão de Python (os, datetime, time, e calendar.)

## 4.1.1.1 Geradores e closures

## Geradores - onde encontrá-los

**Gerador** - a que associa esta palavra? Talvez se refira a algum dispositivo eletrónico. Ou talvez se refira a uma máquina pesada e séria concebida para produzir energia, elétrica ou outra.

Um gerador Python é **uma peça de código especializado capaz de produzir uma série de valores, e de controlar o processo de iteração**. É por isso que os geradores são muitas vezes chamados **iteradores**, e embora alguns possam encontrar uma distinção muito subtil entre estes dois, vamos tratá-los como um só.

Pode não se aperceber, mas já encontrou geradores muitas, muitas vezes antes. Veja este snippet muito simples:

```
for i in range(5):
    print(i)
```

A função `range()` é, de facto, um gerador, que é (de facto, mais uma vez) um iterador.

Qual é a diferença?

Uma função devolve um valor bem definido - pode ser o resultado de uma avaliação mais ou menos complexa de, por exemplo, um polinómio, e é invocada uma vez - apenas uma vez.

Um gerador **devolve uma série de valores** e, em geral, é (implicitamente) invocado mais de uma vez.

No exemplo, o gerador `range()` é invocado seis vezes, fornecendo cinco valores subsequentes de zero a quatro, e finalmente sinalizando que a série está completa.

```
for i in range(5):
    print(i)
```

O processo acima é completamente transparente. Vamos lançar alguma luz sobre ele. Vamos mostrar-lhe o **protocolo iterador**.

## 4.1.1.2 Geradores e closures

## Geradores - onde encontrá-los: continuação

O **protocolo iterador é uma forma de um objeto se comportar de acordo com as regras impostas pelo contexto das declarações** `for` **e** `in` . Um objeto em conformidade com o protocolo iterador é chamado um **iterador**.

Um iterador deve fornecer dois métodos:

* `__iter__()` que deve **devolver o objeto em si** e que é invocado uma vez (é necessário para que Python inicie com sucesso a iteração)
* `__next__()` que se destina a **devolver o próximo valor** (primeiro, segundo, etc.) da série desejada - será invocado pelas declarações `for`/`in` a fim de passar pela próxima iteração; se não houver mais valores a fornecer, o método deve **levantar a exceção** `StopIteration` .
Parece estranho? De modo algum. Veja o exemplo no editor.

Construímos uma classe capaz de iterar através dos primeiros valores n (onde `n` é um parâmetro construtor) dos números de Fibonacci.

Recordemos - os números Fibonacci (Fibi) são definidos da seguinte forma:

Fib<sub>1</sub> = 1
Fib<sub>2</sub> = 1
Fib<sub>i</sub> = Fib<sub>i-1</sub> + Fib<sub>i-2</sub>

Por outras palavras:

* os dois primeiros números de Fibonacci são iguais a 1;
* qualquer outro número de Fibonacci é a soma dos dois anteriores (por exemplo, Fib<sub>3</sub> = 2, Fib<sub>4</sub> = 3, Fib<sub>5</sub> = 5, e assim por diante)

Vamos mergulhar no código:

```
class Fib:
    def __init__(self, nn):
        print("__init__")
        self.__n = nn
        self.__i = 0
        self.__p1 = self.__p2 = 1

    def __iter__(self):
        print("__iter__")
        return self

    def __next__(self):
        print("__next__")				
        self.__i += 1
        if self.__i > self.__n:
            raise StopIteration
        if self.__i in [1, 2]:
            return 1
        ret = self.__p1 + self.__p2
        self.__p1, self.__p2 = self.__p2, ret
        return ret


for i in Fib(10):
    print(i)

```

* linhas 2 a 6: o construtor da classe imprime uma mensagem (vamos usá-la para rastrear o comportamento da classe), prepara algumas variáveis (`__n` para armazenar o limite da série, `__i` para rastrear o número atual de Fibonacci a fornecer, e `__p1` juntamente com `__p2` para guardar os dois números anteriores);

* linhas 8 a 10: o método `__iter__` é obrigado a devolver o próprio objeto iterador; o seu objetivo pode ser um pouco ambíguo aqui, mas não há mistério; tente imaginar um objeto que não seja um iterador (por exemplo, é uma coleção de algumas entidades), mas um dos seus componentes é um iterador capaz de digitalizar a coleção; o método `__iter__` deve **extrair o iterador e confiar-lhe a execução do protocolo de iteração**; como pode ver, o método inicia a sua ação imprimindo uma mensagem;

* linhas 12 a 21: o método `__next__` é responsável pela criação da sequência; é um tanto ou quanto minucioso, mas isto deve torná-lo mais legível; primeiro, imprime uma mensagem, depois atualiza o número de valores desejados, e se chegar ao fim da sequência, o método quebra a iteração levantando a exceção StopIteration; o resto do código é simples, e reflete precisamente a definição que lhe mostrámos anteriormente;

* as linhas 24 e 25 fazem uso do iterador.

O código produz o seguinte output:

output

```
__init__
__iter__
__next__
1
__next__
1
__next__
2
__next__
3
__next__
5
__next__
8
__next__
13
__next__
21
__next__
34
__next__
55
__next__
```


Veja:

* o objeto iterador é instanciado primeiro;
* em seguida, o Python invoca o método `__iter__` para obter acesso ao iterador real;
* o método `__next__` é invocado onze vezes - as primeiras dez vezes produzem valores úteis, enquanto a décima primeira termina a iteração.

## 4.1.1.3 Geradores e closures

## Geradores - onde encontrá-los: continuação

O exemplo anterior mostra uma solução em que o objeto iterador faz parte de uma classe mais complexa.

O código não é realmente sofisticado, mas apresenta o conceito de forma clara.

Observe o código no editor.

```

class Fib:
    def __init__(self, nn):
        self.__n = nn
        self.__i = 0
        self.__p1 = self.__p2 = 1

    def __iter__(self):
        print("Fib iter")
        return self

    def __next__(self):
        self.__i += 1
        if self.__i > self.__n:
            raise StopIteration
        if self.__i in [1, 2]:
            return 1
        ret = self.__p1 + self.__p2
        self.__p1, self.__p2 = self.__p2, ret
        return ret

class Class:
    def __init__(self, n):
        self.__iter = Fib(n)

    def __iter__(self):
        print("Class iter")
        return self.__iter;


object = Class(8)

for i in object:
    print(i)

```

Nós construímos o iterador `Fib` noutra `classe` (podemos dizer que o compusemos na classe `Class` ). É instanciado juntamente com Classdo objeto.

O objeto da classe pode ser usado como um iterador quando (e apenas quando) responde positivamente à invocação `__iter__` - esta classe pode fazê-lo, e se for invocada desta forma, fornece um objeto capaz de obedecer ao protocolo de iteração.

É por isto que o output do código é o mesma que anteriormente, embora o objeto da classe `Fib` não seja usado explicitamente dentro do contexto do loop `for` .

## 4.1.1.4 Geradores e closures

## A função yield .

O protocolo iterador não é particularmente difícil de compreender e utilizar, mas também é indiscutível que **o protocolo é bastante inconveniente**.

O principal desconforto que traz é **a necessidade de guardar o estado da iteração entre subsequentes invocações** `__iter__` .

Por exemplo, o iterador `Fib` é forçado a armazenar com precisão o local onde a última invocação foi interrompida (ou seja, o número avaliado e os valores dos dois elementos anteriores). Isso torna o código maior e menos compreensível.

É por isso que o Python oferece uma maneira muito mais eficaz, conveniente e elegante de escrever iteradores.

O conceito é fundamentalmente baseado num mecanismo muito específico e poderoso fornecido pela keyword `yield` .

Pode pensar na keyword `yield` como uma irmã mais inteligente da declaração `return` , com uma diferença essencial.

Observe esta função:
```
def fun(n):
    for i in range(n):
        return i
```

Tem um aspecto estranho, não tem? É claro que o loop `for` não tem qualquer hipótese de terminar a sua primeira execução, uma vez que o `return` vai quebrá-lo irrevogavelmente.

Além disso, invocar a função não mudará nada - o loop `for` começará do zero e será quebrado imediatamente.

Podemos dizer que tal função não é capaz de guardar e restaurar o seu estado entre invocações subsequentes.

Isto também significa que uma função como esta **não pode ser usada como gerador**.

Substituímos exatamente uma palavra no código - consegue vê-la?
```
def fun(n):
    for i in range(n):
        yield i
```

Adicionámos `yield` em vez de `return`. Esta pequena emenda **transforma a função num gerador**, e executar a declaração `yield` tem alguns efeitos muito interessantes.

Antes de mais, fornece o valor da expressão especificada após a keyword `yield` , assim como `return`, mas não perde o estado da função.

Todos os valores das variáveis são congelados e aguardam a próxima invocação, quando a execução é retomada (não tirada do zero, como depois `return`).

Há uma limitação importante: tal **função não deve ser invocada explicitamente** porque - na realidade - já não é uma função; **é um objeto gerador**.

A invocação **devolverá o identificador do objeto**, não a série que esperamos do gerador.

Devido às mesmas razões, a função anterior (a função com a declaração `return` ) só pode ser invocada explicitamente, e não deve ser usada como um gerador.

## Como construir um gerador

Deixe-nos mostrar-lhe o novo gerador em ação.

É assim que podemos utilizá-lo:
```
def fun(n):
    for i in range(n):
        yield i


for v in fun(5):
    print(v)
```

Consegue adivinhar o output?

Verifique

```
0
1
2
3
4
```

## 4.1.1.5 Geradores e closures

## Como construir o seu próprio gerador

E se precisar de um **gerador para produzir as primeiras n potências de 2**?

Nada mais fácil. Basta olhar para o código abaixo:
```
def powers_of_2(n):
    power = 1
    for i in range(n):
        yield power
        power *= 2


for v in powers_of_2(8):
    print(v)
```

Consegue adivinhar o output? Copie o código para o editor e execute-o para verificar os seus palpites.

**Compreensões de lista**

Os geradores também podem ser utilizados no âmbito das **compreensões de lista**, tal como aqui:

```
def powers_of_2(n):
    power = 1
    for i in range(n):
        yield power
        power *= 2


t = [x for x in powers_of_2(5)]
print(t)
```

Execute o exemplo e verifique o output.

**A** `list()` .

A função `list()` pode transformar uma série de invocações de geradores subsequentes numa **lista real**:

```
def powers_of_2(n):
    power = 1
    for i in range(n):
        yield power
        power *= 2


t = list(powers_of_2(3))
print(t)
```

Mais uma vez, tente prever o output e execute o código para verificar as suas previsões.

**O operador** `in` .

Além disso, o contexto criado pelo operador `in` também permite a utilização de um gerador.

O exemplo mostra como o fazer:
```
def powers_of_2(n):
    power = 1
    for i in range(n):
        yield power
        power *= 2


for i in range(20):
    if i in powers_of_2(4):
        print(i)
```

Qual é o output do código? Execute o programa e verifique.

**O gerador de números Fibonacci**

Agora vamos ver um **gerador de números Fibonacci**, e assegurar que tenha muito melhor aspeto do que a versão objetiva baseada na implementação do protocolo de iterador direto.

Aqui está:

```
def fibonacci(n):
    p = pp = 1
    for i in range(n):
        if i in [0, 1]:
            yield 1
        else:
            n = p + pp
            pp, p = p, n
            yield n

fibs = list(fibonacci(10))
print(fibs)
```

Adivinhe o output (uma lista) produzida pelo gerador, e execute o código para verificar se estava certo.

## 4.1.1.6 Geradores e closures

## Mais sobre compreensões de lista

Deverá ser capaz de se lembrar das regras que regem a criação e utilização de um fenómeno Python muito especial denominado **compreensão de listas - uma forma simples e muito impressionante de criar listas e o seu conteúdo.**

Caso precise, fornecemos um lembrete rápido no editor.

```
list_1 = []

for ex in range(6):
    list_1.append(10 ** ex)

list_2 = [10 ** ex for ex in range(6)]

print(list_1)
print(list_2)
```

Há duas partes dentro do código, ambas criando uma lista contendo algumas das primeiras potências naturais de dez.

A primeira utiliza uma forma rotineira de utilizar o loop `for` , enquanto a última faz uso da compreensão de lista e constrói a lista in situ, sem precisar de um loop, ou de qualquer outro código alargado.

Parece que a lista é criada dentro de si mesma - não é verdade, claro, pois o Python tem de realizar quase as mesmas operações que no primeiro snippet, mas é indiscutível que o segundo formalismo é simplesmente mais elegante, e permite ao leitor evitar quaisquer detalhes desnecessários.

O exemplo produz duas linhas idênticas contendo o seguinte texto:

output

```
[1, 10, 100, 1000, 10000, 100000]
[1, 10, 100, 1000, 10000, 100000]
```

Execute o código para verificar se estamos certos.

## 4.1.1.7 Geradores e closures

## Mais sobre as compreensões de lista: continuação

Há uma sintaxe muito interessante que queremos mostrar-lhe agora. A sua usabilidade não se limita a compreensões de lista, mas temos de admitir que as compreensões são o ambiente ideal para ela.

É uma **expressão condicional - uma forma de selecionar um de dois valores diferentes com base no resultado de uma expressão Booleana.**

Veja:

expression_one if condition else expression_two

Pode parecer um pouco surpreendente à primeira vista, mas é preciso ter em mente que **não se trata de uma instrução condicional**. Além disso, não é uma instrução de todo. É um operador.

O valor que ele fornece é igual a `expression_one` quando a condição é `True`, e `expression_two` caso contrário.

Um bom exemplo dir-lhe-á mais. Veja o código no editor.

```
the_list = []

for x in range(10):
    the_list.append(1 if x % 2 == 0 else 0)

print(the_list)
```

O código preenche uma lista com `1` e `0` - se o index de um determinado elemento for estranho, o elemento é definido para `0` , e para `1` caso contrário.

Simples? Talvez não à primeira vista. Elegante? Indiscutivelmente.

Pode-se usar o mesmo truque dentro de uma compreensão de lista? Sim, pode-se.

## 4.1.1.8 Geradores e closures

## Mais sobre as compreensões de lista: continuação

Veja o exemplo no editor.

```
the_list = [1 if x % 2 == 0 else 0 for x in range(10)]

print(the_list)
```

Compactidão e elegância - estas duas palavras vêm à mente ao olhar para o código.

Então, o que é que têm em comum, geradores e compreensões de lista? Existe alguma conexão entre eles? Sim. Uma conexão bastante ligeira, mas inequívoca.

Apenas uma mudança pode **transformar qualquer compreensão de lista num gerador.**

**Compreensões de lista vs. geradores**

Agora olhe para o código abaixo e veja se consegue encontrar o detalhe que transforma uma compreensão de lista num gerador:
```
the_list = [1 if x % 2 == 0 else 0 for x in range(10)]
the_generator = (1 if x % 2 == 0 else 0 for x in range(10))

for v in the_list:
    print(v, end=" ")
print()

for v in the_generator:
    print(v, end=" ")
print()
```

São os **parêntesis**. Os parêntesis retos fazem uma compreensão, os parêntesis curvos fazem um gerador.

O código, no entanto, quando executado, produz duas linhas idênticas:

output

```
1 0 1 0 1 0 1 0 1 0
1 0 1 0 1 0 1 0 1 0
```

Como pode saber que a segunda tarefa cria um gerador, não uma lista?

Há algumas provas que lhe podemos mostrar. Aplicar a função `len()` para ambas as entidades.

`len(the_list)` avaliará a 10. Claro e previsível. `len(the_generator)` irá levantar uma exceção, e verá a seguinte mensagem:

output

`TypeError: object of type 'generator' has no len()`

Claro que não é necessário guardar a lista ou o gerador - pode criá-los exatamente no local onde precisa deles - tal como aqui:
```
for v in [1 if x % 2 == 0 else 0 for x in range(10)]:
    print(v, end=" ")
print()

for v in (1 if x % 2 == 0 else 0 for x in range(10)):
    print(v, end=" ")
print()
```

Nota: a mesma aparência do output não significa que ambos os loops funcionam da mesma forma. No primeiro loop, a lista é criada (e iterada através) como um todo - ela existe de facto quando o loop está a ser executado.

No segundo loop, não existe qualquer lista - existem apenas valores subsequentes produzidos pelo gerador, um por um.

Realize as suas próprias experiências.

## 4.1.1.9 Geradores e closures

## A função `lambda` .

A função `lambda` é um conceito emprestado da matemática, mais especificamente, de uma parte chamada cálculo Lambda, mas estes dois fenómenos não são a mesma coisa.

Os matemáticos utilizam o *cálculo Lambda* em muitos sistemas formais ligados à lógica, recorrência, ou provabilidade do teorema. Os programadores usam a função `lambda` para simplificar o código, para torná-lo mais claro e mais fácil de entender.

Uma função `lambda` é uma função sem nome (também se pode chamar-lhe uma **função anônima**). Evidentemente, tal afirmação levanta imediatamente a questão: como utilizar qualquer coisa que não possa ser identificada?

Felizmente, não é um problema, pois pode nomear tal função se realmente precisar, mas, de fato, em muitos casos, a função `lambda` pode existir e trabalhar enquanto permanece totalmente incógnita.

A declaração da função `lambda` não se assemelha a uma declaração de função normal de forma alguma - veja por si mesmo:

`lambda parameters: expression`

Tal cláusula **devolve o valor da expressão quando se tem em conta o valor atual do atual argumento** `lambda` .

Como de costume, um exemplo será útil. O nosso exemplo usa três funções lambda , mas dá-lhes nomes. Olhe com atenção:
```
two = lambda: 2
sqr = lambda x: x * x
pwr = lambda x, y: x ** y

for a in range(-2, 3):
    print(sqr(a), end=" ")
    print(pwr(a, two()))
```

Vamos analisá-lo:

* a primeira `lambda` é uma **função anónima sem parâmetros** que devolve sempre `2`. Como **a atribuímos a uma variável chamada** `two`, podemos dizer que a função já não é anónima, e podemos usar o nome para a invocar.

* a segunda é uma **função anônima de um parâmetro** que devolve o valor do seu argumento ao quadrado. Também a nomeámos como tal.

* a terceira `lambda` **toma dois parâmetros** e devolve o valor do primeiro elevado à potência do segundo. O nome da variável que transporta a `lambda` fala por si. Não utilizamos `pow` para evitar confusão com a função integrada do mesmo nome e do mesmo objetivo.

O programa produz o seguinte output:

output

```
4 4
1 1
0 0
1 1
4 4
```

Este exemplo é suficientemente claro para mostrar como `lambda` são declaradas e como se comportam, mas não diz nada sobre o porquê de serem necessárias, e para que são usadas, uma vez que todas elas podem ser substituídas por funções Python de rotina.

Onde está o benefício?

## 4.1.1.10 Geradores e closures

## Como usar lambdas e para quê?

A parte mais interessante da utilização de lambdas surge quando se pode utilizá-los na sua forma pura - **como partes anónimas de código destinadas a avaliar um resultado.**

Imagine que precisamos de uma função (vamos nomeá-la `print_function`) que imprime os valores de uma determinada (outra) função para um conjunto de argumentos selecionados.

Queremos que `print_function` seja universal - deve aceitar um conjunto de argumentos colocados numa lista e uma função a ser avaliada, ambos como argumentos - não queremos codificar nada.

Veja o exemplo no editor. Foi assim que implementámos a ideia.

```
def print_function(args, fun):
    for x in args:
        print('f(', x,')=', fun(x), sep='')


def poly(x):
    return 2 * x**2 - 4 * x + 2


print_function([x for x in range(-2, 3)], poly)
```

Vamos analisá-la. A função `print_function()` toma dois parâmetros:

* o primeiro, uma lista de argumentos para os quais queremos imprimir os resultados;
* o segundo, uma função que deve ser invocada tantas vezes quanto o número de valores que são recolhidos dentro do primeiro parâmetro.

Nota: também definimos uma função chamada `poly()` - esta é a função cujos valores vamos imprimir. O cálculo que a função realiza não é muito sofisticado - é o polinomial (daí o seu nome) de uma forma:

`f(x) = 2x2 - 4x + 2`

O nome da função é então passado para o `print_function()` juntamente com um conjunto de cinco argumentos diferentes - o conjunto é construído com uma cláusula de compreensão de lista.

O código imprime as seguintes linhas:

output

```
f(-2)=18
f(-1)=8
f(0)=2
f(1)=0
f(2)=2
```

Podemos evitar definir a função `poly()` , já que não a vamos utilizar mais do que uma vez? Sim, podemos - este é o benefício que uma lambda pode trazer.

Veja o exemplo em baixo. Consegue ver a diferença?

```
def print_function(args, fun):
    for x in args:
        print('f(', x,')=', fun(x), sep='')

print_function([x for x in range(-2, 3)], lambda x: 2 * x**2 - 4 * x + 2)
```

A função `print_function()` permaneceu exatamente a mesma, mas não há nenhuma `poly()` função. Já não precisamos dela, pois o polinómio está agora diretamente dentro da invocação `print_function()` sob a forma de um lambda definido da seguinte forma:

`lambda x: 2 * x**2 - 4 * x + 2`

O código tornou-se mais curto, mais claro e mais legível.

Deixe-nos mostrar-lhe outro lugar onde os lambdas podem ser úteis. Começaremos com uma descrição de `map()`, uma função integrada de Python. O seu nome não é demasiado descritivo, a sua ideia é simples, e a função em si é realmente utilizável.

## 4.1.1.11 Geradores e closures

## Lambdas e a função map() .

No mais simples de todos os casos possíveis, a função `map()` .

`map(function, list)`

toma dois argumentos:

* uma função;
* uma lista.

A descrição acima é extremamente simplificada, uma vez que:

* o segundo argumento `map()` pode ser qualquer entidade que possa ser iterada (por exemplo, um tuple, ou apenas um gerador)
* `map()` pode aceitar mais de dois argumentos.
 
A função `map()` **aplica a função passada pelo seu primeiro argumento a todos os elementos do seu segundo argumento, e devolve um iterador entregando todos os resultados subsequentes da função.**

Pode usar o iterador resultante num loop, ou convertê-lo numa lista usando a função `list()` .

Consegue ver aqui um papel para qualquer lambda?

Veja o código no editor - utilizámos dois lambdas no mesmo.

```
list_1 = [x for x in range(5)]
list_2 = list(map(lambda x: 2 ** x, list_1))
print(list_2)

for x in map(lambda x: x * x, list_2):
    print(x, end=' ')
print()
```

Esta é a intriga:

* construa o `list_1` com valores de `0` até `4`;
* em seguida, utilize `map` juntamente com o primeiro `lambda` para criar uma nova lista na qual todos os elementos tenham sido avaliados como `2` elevados à potência retirada do elemento correspondente de `list_1`;
* list_2 é então impresso;
* no passo seguinte, utilize a função `map()` novamente para fazer uso do gerador que devolve e para imprimir diretamente todos os valores que fornece; como pode ver, envolvemos o segundo `lambda` aqui - apenas eleva ao quadrado cada elemento de `list_2`.
  
Tente imaginar o mesmo código sem lambdas. Seria melhor? É pouco provável.

## 4.1.1.12 Geradores e closures

## Lambdas e a função filter() .

Outra função Python que pode ser significativamente embelezada pela aplicação de um lambda é `filter()`.

Espera o mesmo tipo de argumentos que `map()`, mas faz algo diferente - **filtra o seu segundo argumento ao mesmo tempo que é guiado por instruções que fluem da função especificada como o primeiro argumento** (a função é invocada para cada elemento da lista, tal como em `map()`).

Os elementos que retornam `True` da função **passam o filtro** - os outros são rejeitados.

O exemplo no editor mostra a função `filter()` em ação.

```
from random import seed, randint

seed()
data = [randint(-10,10) for x in range(5)]
filtered = list(filter(lambda x: x > 0 and x % 2 == 0, data))

print(data)
print(filtered)
```

Nota: fizemos uso do módulo `random` para inicializar o gerador de números aleatórios (não confundir com os geradores de que acabámos de falar) com a função `seed()` , e para produzir cinco valores inteiros aleatórios a partir de `-10` até `10` utilizando a função `randint()` .

A lista é então filtrada, e apenas os números que são iguais e superiores a zero são aceites.

Claro que não é provável que receba os mesmos resultados, mas os nossos resultados são estes:

output

```
[6, 3, 3, 2, -7]
[6, 2]
```

## 4.1.1.13 Geradores e closures

## Um breve olhar sobre os closures

Comecemos por uma definição: **o closure é uma técnica que permite o armazenamento de valores apesar do facto de o contexto em que foram criados já não existir**. Intrincado? Um pouco.

Vamos analisar um exemplo simples:
```
def outer(par):
    loc = par


var = 1
outer(var)

print(var)
print(loc)
```

O exemplo é obviamente errado.

As duas últimas linhas causarão uma exceção NameError - nem `par` nem `loc` são acessíveis fora da função. Ambas as variáveis existem quando e só quando a função `outer()` está a ser executada.

Veja o exemplo no editor. Modificámos o código de forma significativa.

```
def outer(par):
    loc = par

    def inner():
        return loc
    return inner


var = 1
fun = outer(var)
print(fun())

```

Há um novo elemento no mesmo - uma função (denominada `inner`) dentro de outra função (nomeada `outer`).

Como é que funciona? Tal como qualquer outra função, exceto o facto de que `inner()` só pode ser invocada a partir do interior `outer()`. Podemos dizer que `inner()` é a ferramenta privada de `outer()`- nenhuma outra parte do código lhe pode aceder.

Veja com atenção:

* a função `inner()` devolve o valor da variável acessível dentro do seu scope, uma vez que `inner()` pode utilizar qualquer uma das entidades à disposição de `outer()`
* a função `outer()` devolve a função `inner()` em si; mais precisamente, devolve uma cópia da função `inner()` , a que estava congelada no momento de invocação `outer()`; a função congelada contém o seu ambiente completo, incluindo o estado de todas as variáveis locais, o que também significa que o valor de `loc` é retido com sucesso, embora `outer()` tenha deixado de existir há muito tempo.

Na verdade, o código é totalmente válido, e tem como output:

output

`1`


A função devolvida durante a invocação `outer()` é um **closure**.

## 4.1.1.14 Geradores e closures

## Um breve olhar sobre closures: continuação

**Um closure tem de ser invocado exatamente da mesma forma como foi declarado.**

No exemplo abaixo:
```
def outer(par):
    loc = par

    def inner():
        return loc
    return inner


var = 1
fun = outer(var)
print(fun())
```

a função `inner()` é sem parâmetros, pelo que temos de a invocar sem argumentos.

Agora veja o código no editor. É totalmente possível **declarar um closure equipado com um número arbitrário de parâmetros**, por exemplo, um, tal como a `power()` função.

```
def make_closure(par):
    loc = par

    def power(p):
        return p ** loc
    return power


fsqr = make_closure(2)
fcub = make_closure(3)

for i in range(5):
    print(i, fsqr(i), fcub(i))
```

Isto significa que o closure não só faz uso do ambiente congelado, como também pode **modificar o seu comportamento, utilizando valores retirados do exterior.**

Este exemplo mostra mais uma circunstância interessante - pode **criar tantos closures quantos quiser usando um e o mesmo código**. Isso é feito com uma função chamada `make_closure()`. Nota:

* o primeiro closure obtido a partir de `make_closure()` define uma ferramenta que enquadra o seu argumento;
* o segundo foi concebido para cubrir o argumento.

É por isso que o código produz o seguinte output:

output

```
0 0 0
1 1 1
2 4 8
3 9 27
4 16 64
```

Realize os seus próprios testes.



## 4.1.1.15 RESUMO DA SEÇÃO

## Key takeaways

1. Um **iterador** é um objeto de uma classe que fornece pelo menos **dois** métodos (sem contar com o construtor!):

* `__iter__()` é invocado uma vez quando o iterador é criado e devolve o **próprio** objeto do iterador;
* `__next__()` é invocado para fornecer **o valor da próxima iteração** e levanta uma exceção `StopIteration` quando a iteração **chega ao fim**.

2. O método `yield` só pode ser utilizada dentro de funções. A declaração `yield` suspende a execução da função e faz com que a função devolva o argumento do yield como resultado. Tal função não pode ser invocada de forma regular - a sua única finalidade é ser usada como um **gerador** (ou seja, num contexto que requer uma série de valores, como um loop `for` .)


3. Uma **expressão condicional** é uma expressão construída usando o operador `if-else` . Por exemplo:

`print(True if 0 >=0 else False)`

tem como output `True`.

4. Uma **compreensão de lista** torna-se um **gerador** quando usada dentro de **parêntesis curvos** (usada dentro de parêntesis retos, produz uma lista regular). Por exemplo:

```
for x in (el * 2 for el in range(5)):
    print(x)
```
tem como output `02468`.


1. Uma **função lambda** é uma ferramenta para a criação de **funções anônimas**. Por exemplo:

```
def foo(x,f):
    return f(x)

print(foo(9, lambda x: x ** 0.5))
```

tem como output `3.0`.


5. O módulo `map(fun, list)` cria uma **cópia** de um argumento `list` , e aplica a função `fun` a todos os seus elementos, devolvendo um **gerador** que fornece o novo conteúdo da lista elemento por elemento. Por exemplo:
```
short_list = ['mython', 'python', 'fell', 'on', 'the', 'floor']
new_list = list(map(lambda s: s.title(), short_list))
print(new_list)
```

tem como output `['Mython', 'Python', 'Fell', 'On', 'The', 'Floor'].`


6. A função `filter(fun, list)` cria uma **cópia** desses elementos `list` , que causam que a função `fun` devolva `True`. O resultado da função é um **gerador** que fornece o novo conteúdo da lista elemento por elemento. Por exemplo:
```
short_list = [1, "Python", -1, "Monty"]
new_list = list(filter(lambda s: isinstance(s, str), short_list))
print(new_list)
```

tem como output `['Python', 'Monty']`.

7. O closure é uma técnica que permite o **armazenamento de valores** apesar do fato de o **contexto** em que foram criados **já não existir**. Por exemplo:
```
def tag(tg):
    tg2 = tg
    tg2 = tg[0] + '/' + tg[1:]

    def inner(str):
        return tg + str + tg2
    return inner


b_tag = tag('<b>')
print(b_tag('Monty Python'))
```

tem como output `<b>Monty Python</b>`


**Exercício 1**

Qual é o output esperado do seguinte código?
```
class Vowels:
    def __init__(self):
        self.vow = "aeiouy "  # Yes, we know that y is not always considered a vowel.
        self.pos = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self.pos == len(self.vow):
            raise StopIteration
        self.pos += 1
        return self.vow[self.pos - 1]


vowels = Vowels()
for v in vowels:
    print(v, end=' ')
```

Verifique

`a e i o u y`


**Exercício 2**

Escreva uma função **lambda**, definindo a parte menos significativa do seu argumento inteiro, e aplique-a à função `map()` para produzir a string `1 3 3 5` no console.
```
any_list = [1, 2, 3, 4]
even_list = # Complete the line here.
print(even_list)
```

Verifique

`list(map(lambda n: n | 1, any_list))`


**Exercício 3**

Qual é o output esperado do seguinte código?
```
def replace_spaces(replacement='*'):
    def new_replacement(text):
        return text.replace(' ', replacement)
    return new_replacement


stars = replace_spaces()
print(stars("And Now for Something Completely Different"))
```

Verifique

`And*Now*for*Something*Completely*Different`

Nota

[PEP 8](https://peps.python.org/pep-0008/#programming-recommendations) , o Guia de Estilo do Código Python, recomenda que os **lambdas não sejam atribuídos a variáveis, mas sim que sejam definidos como funções.**

Isto significa que é melhor usar uma declaração `def` , e evitar utilizar uma declaração de atribuição que ligue uma expressão lambda a um identificador. Por exemplo:
```
# Recommended:
def f(x): return 3*x


# Not recommended:
f = lambda x: 3*x
```

A vinculação de lambdas a identificadores geralmente duplica a funcionalidade da declaração `def` . Utilizar declarações `def` , por outro lado, gera mais linhas de código.

É importante compreender que a realidade gosta frequentemente de desenhar os seus próprios cenários, que não seguem necessariamente as convenções ou recomendações formais. A decisão de os seguir ou não dependerá de muitas coisas: as suas preferências, outras convenções adotadas, diretrizes internas da empresa, compatibilidade com o código existente, etc. Esteja atento a isto.