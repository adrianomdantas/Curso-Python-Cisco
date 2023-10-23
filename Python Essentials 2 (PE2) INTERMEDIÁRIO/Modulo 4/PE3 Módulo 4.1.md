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

## 4.1.1.9 Geradores e closures

## 4.1.1.10 Geradores e closures

## 4.1.1.11 Geradores e closures

## 4.1.1.12 Geradores e closures

## 4.1.1.13 Geradores e closures

## 4.1.1.14 Geradores e closures

## 4.1.1.15 RESUMO DA SEÇÃO