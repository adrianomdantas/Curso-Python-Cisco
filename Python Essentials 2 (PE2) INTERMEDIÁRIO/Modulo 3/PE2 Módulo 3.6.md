## 3.6.1.1 Exceções mais uma vez

# Mais sobre exceções

Discutir a programação de objetos oferece uma excelente oportunidade para regressar às exceções. A natureza objetiva das exceções de Python torna-as uma ferramenta muito flexível, capaz de se adaptar a necessidades específicas, mesmo aquelas que ainda não conhece.

Antes de mergulharmos na **face objetiva das exceções**, queremos mostrar-lhe alguns aspetos sintáticos e semânticos da forma como o Python trata o bloco try-except, uma vez que oferece um pouco mais do que aquilo que temos apresentado até agora.

A primeira característica que queremos discutir aqui é um possível ramo adicional, que pode ser colocado dentro (ou melhor, diretamente atrás) do bloco try-except - é a parte do código que começa com `else` - tal como no exemplo no editor.

Um código assim rotulado é executado quando (e apenas quando) nenhuma exceção tiver sido levantada dentro da parte `try`: . Podemos dizer que exatamente um ramo pode ser executado após `try`: - quer o que começa com `except` (não se esqueça de que pode haver mais do que um ramo deste tipo) ou o que começa com `else`.

Nota: o ramo else: tem de ser localizado após o último ramo except .

```
def reciprocal(n):
    try:
        n = 1 / n
    except ZeroDivisionError:
        print("Division failed")
        return None
    else:
        print("Everything went fine")
        return n


print(reciprocal(2))
print(reciprocal(0))
```

O código de exemplo produz o seguinte output:

output

```
Everything went fine
0.5
Division failed
None
```

## 3.6.1.2 Exceções mais uma vez

## Mais sobre exceções

O bloco try-except pode ser prolongado de mais uma forma - adicionando uma parte encabeçada pela keyword `finally` (deve ser o último ramo do código concebido para lidar com exceções).

Nota: estas duas variantes (`else` e `finally`) não são de modo algum dependentes, e podem coexistir ou ocorrer independentemente.

O bloco `finally` é sempre executado (finaliza a execução do bloco try-except, daí o seu nome), independentemente do que aconteceu anteriormente, mesmo quando se levanta uma exceção, independentemente de esta ter sido tratada ou não.

```
def reciprocal(n):
    try:
        n = 1 / n
    except ZeroDivisionError:
        print("Division failed")
        n = None
    else:
        print("Everything went fine")
    finally:
        print("It's time to say goodbye")
        return n


print(reciprocal(2))
print(reciprocal(0))
```

Veja o código no editor. O seu output é:

output

```
Everything went fine
It's time to say good bye
0.5
Division failed
It's time to say good bye
None
```

## 3.6.1.3 Exceções mais uma vez

## Exceções são classes

Todos os exemplos anteriores se contentavam em detetar um tipo específico de exceção e responder-lhe de uma forma adequada. Agora vamos aprofundar, e olhar para dentro da própria exceção.

Provavelmente não ficará surpreendido ao saber que **exceções são classes**. Além disso, quando é levantada uma exceção, um objeto da classe é instanciado, e passa por todos os níveis de execução do programa, procurando o ramo exceto o que está preparado para lidar com ele.

Tal objeto traz alguma informação útil que pode ajudá-lo a identificar com precisão todos os aspetos da situação pendente. Para atingir esse objetivo, o Python oferece uma variante especial da cláusula de exceção - pode encontrá-la no editor.

Como pode ver, a declaração `except` é prolongada, e contém uma frase adicional que começa com a keyword `as` , seguida por um identificador. O identificador é concebido para apanhar o objeto de exceção, para que se possa analisar a sua natureza e tirar as devidas conclusões.

Nota: o scope do identificador abrange o seu ramo `except` , e não vai mais longe.

O exemplo apresenta uma forma muito simples de utilizar o objeto recebido - basta imprimi-lo (como pode ver, o output é produzido pelo método do objeto `__str__()` ) e contém uma breve mensagem descrevendo a razão.

A mesma mensagem será impressa se não houver nenhum bloco de encaixe `except` no código, e o Python é forçado a lidar com ela sozinho.

```
try:
    i = int("Hello!")
except Exception as e:
    print(e)
    print(e.__str__())
```

## 3.6.1.4 Exceções mais uma vez

## Exceções são classes
Todas as exceções Python integradas formam uma hierarquia de classes. Não há qualquer obstáculo à sua extensão se a considerar razoável.

Veja o código no editor.

Este programa descarta todas as classes de exceção pré-definidas sob a forma de uma impressão em forma de árvore.

Como **uma árvore é um exemplo perfeito de uma estrutura de dados recursiva**, uma recursividade parece ser a melhor ferramenta para a atravessar. A função `print_exception_tree()` toma dois argumentos:

* um ponto dentro da árvore a partir do qual começamos a atravessar a árvore;
* um nível de nesting (vamos utilizá-lo para construir um desenho simplificado dos ramos da árvore)

Comecemos pela raiz da árvore - a raiz das classes de exceção de Python é a classe `BaseException` (é uma superclasse de todas as outras exceções).

Para cada uma das classes encontradas, realize o mesmo conjunto de operações:

* imprimir o seu nome, retirado da propriedade `__name__` ;
* iterar através da lista de subclasses entregue pelo método `__subclasses__()` , e invocar recursivamente a função `print_exception_tree()` , incrementando o nível de nesting respetivamente.

Note-se como desenhámos os ramos e as bifurcações. A impressão não é classificada de forma alguma - pode tentar classificá-la você mesmo, se quiser um desafio. Além disso, existem algumas imprecisões subtis na forma como alguns ramos são apresentados. Isso também pode ser corrigido, se assim o desejar.

```
def print_exception_tree(thisclass, nest = 0):
    if nest > 1:
        print("   |" * (nest - 1), end="")
    if nest > 0:
        print("   +---", end="")

    print(thisclass.__name__)

    for subclass in thisclass.__subclasses__():
        print_exception_tree(subclass, nest + 1)


print_exception_tree(BaseException)
```

É este o seu aspecto:

output

```
BaseException
   +---Exception
   |   +---TypeError
   |   +---StopAsyncIteration
   |   +---StopIteration
   |   +---ImportError
   |   |   +---ModuleNotFoundError
   |   |   +---ZipImportError
   |   +---OSError
   |   |   +---ConnectionError
   |   |   |   +---BrokenPipeError
   |   |   |   +---ConnectionAbortedError
   |   |   |   +---ConnectionRefusedError
   |   |   |   +---ConnectionResetError
   |   |   +---BlockingIOError
   |   |   +---ChildProcessError
   |   |   +---FileExistsError
   |   |   +---FileNotFoundError
   |   |   +---IsADirectoryError
   |   |   +---NotADirectoryError
   |   |   +---InterruptedError
   |   |   +---PermissionError
   |   |   +---ProcessLookupError
   |   |   +---TimeoutError
   |   |   +---UnsupportedOperation
   |   |   +---herror
   |   |   +---gaierror
   |   |   +---timeout
   |   |   +---Error
   |   |   |   +---SameFileError
   |   |   +---SpecialFileError
   |   |   +---ExecError
   |   |   +---ReadError
   |   +---EOFError
   |   +---RuntimeError
   |   |   +---RecursionError
   |   |   +---NotImplementedError
   |   |   +---_DeadlockError
   |   |   +---BrokenBarrierError
   |   +---NameError
   |   |   +---UnboundLocalError
   |   +---AttributeError
   |   +---SyntaxError
   |   |   +---IndentationError
   |   |   |   +---TabError
   |   +---LookupError
   |   |   +---IndexError
   |   |   +---KeyError
   |   |   +---CodecRegistryError
   |   +---ValueError
   |   |   +---UnicodeError
   |   |   |   +---UnicodeEncodeError
   |   |   |   +---UnicodeDecodeError
   |   |   |   +---UnicodeTranslateError
   |   |   +---UnsupportedOperation
   |   +---AssertionError
   |   +---ArithmeticError
   |   |   +---FloatingPointError
   |   |   +---OverflowError
   |   |   +---ZeroDivisionError
   |   +---SystemError
   |   |   +---CodecRegistryError
   |   +---ReferenceError
   |   +---BufferError
   |   +---MemoryError
   |   +---Warning
   |   |   +---UserWarning
   |   |   +---DeprecationWarning
   |   |   +---PendingDeprecationWarning
   |   |   +---SyntaxWarning
   |   |   +---RuntimeWarning
   |   |   +---FutureWarning
   |   |   +---ImportWarning
   |   |   +---UnicodeWarning
   |   |   +---BytesWarning
   |   |   +---ResourceWarning
   |   +---error
   |   +---Verbose
   |   +---Error
   |   +---TokenError
   |   +---StopTokenizing
   |   +---Empty
   |   +---Full
   |   +---_OptionError
   |   +---TclError
   |   +---SubprocessError
   |   |   +---CalledProcessError
   |   |   +---TimeoutExpired
   |   +---Error
   |   |   +---NoSectionError
   |   |   +---DuplicateSectionError
   |   |   +---DuplicateOptionError
   |   |   +---NoOptionError
   |   |   +---InterpolationError
   |   |   |   +---InterpolationMissingOptionError
   |   |   |   +---InterpolationSyntaxError
   |   |   |   +---InterpolationDepthError
   |   |   +---ParsingError
   |   |   |   +---MissingSectionHeaderError
   |   +---InvalidConfigType
   |   +---InvalidConfigSet
   |   +---InvalidFgBg
   |   +---InvalidTheme
   |   +---EndOfBlock
   |   +---BdbQuit
   |   +---error
   |   +---_Stop
   |   +---PickleError
   |   |   +---PicklingError
   |   |   +---UnpicklingError
   |   +---_GiveupOnSendfile
   |   +---error
   |   +---LZMAError
   |   +---RegistryError
   |   +---ErrorDuringImport
   +---GeneratorExit
   +---SystemExit
   +---KeyboardInterrupt
```

## 3.6.1.5 Exceções mais uma vez

## Anatomia detalhada das exceções

Vamos analisar mais de perto o objeto da exceção, uma vez que há aqui alguns elementos realmente interessantes (voltaremos à questão em breve quando considerarmos as técnicas de base de input/output de Python, uma vez que o seu subsistema de exceção estende um pouco estes objetos).

A classe `BaseException` introduz uma propriedade chamada `args`. É um **tuple concebido para reunir todos os argumentos passados ao construtor da classe**. Está vazio se a construção foi invocada sem quaisquer argumentos, ou contém apenas um elemento quando o construtor recebe um argumento (não contamos o argumento `self` aqui), e assim por diante.

Preparamos uma função simples para imprimir a propriedade `args` de uma forma elegante. Pode ver a função no editor.

Utilizamos a função para imprimir o conteúdo da propriedade `args` em três casos diferentes, em que a exceção da classe `Exception` é levantada de três maneiras diferentes. Para o tornar mais espetacular, imprimimos também o próprio objeto, juntamente com o resultado da invocação `__str__()` .

O primeiro caso parece rotineiro - há apenas o nome `Exception` após a keyword `raise` . Isto significa que o objeto desta classe foi criado de uma forma muito rotineira.

O segundo e terceiro casos podem parecer um pouco estranhos à primeira vista, mas não há nada de estranho aqui - estas são apenas as invocações do construtor. Na segunda declaração raise , o construtor é invocado com um argumento, e no terceiro com dois.

```
def print_args(args):
    lng = len(args)
    if lng == 0:
        print("")
    elif lng == 1:
        print(args[0])
    else:
        print(str(args))


try:
    raise Exception
except Exception as e:
    print(e, e.__str__(), sep=' : ' ,end=' : ')
    print_args(e.args)

try:
    raise Exception("my exception")
except Exception as e:
    print(e, e.__str__(), sep=' : ', end=' : ')
    print_args(e.args)

try:
    raise Exception("my", "exception")
except Exception as e:
    print(e, e.__str__(), sep=' : ', end=' : ')
    print_args(e.args)

```

Como pode ver, o output do programa reflete isto, mostrando o conteúdo apropriado da propriedade `args` :

output

```
 :  :
my exception : my exception : my exception
('my', 'exception') : ('my', 'exception') : ('my', 'exception')
```

## 3.6.1.6 Exceções mais uma vez

## Como criar a sua própria exceção

A hierarquia de exceções não está fechada nem terminada, e pode sempre alargá-la se quiser ou precisar de criar o seu próprio mundo povoado com as suas próprias exceções.

Pode ser útil quando se cria um módulo complexo que deteta erros e levanta exceções, e se pretende que as exceções sejam facilmente distinguíveis de quaisquer outras trazidas pelo Python.

Isto é feito **definindo as suas próprias, novas exceções como subclasses derivadas de subclasses predefinidas.**

Nota: se quiser criar uma exceção que será utilizada como um caso especializado de qualquer exceção incorporada, derive-a apenas desta. Se quer construir a sua própria hierarquia, e não quer que ela esteja intimamente ligada à árvore de exceção de Python, derive-a de qualquer uma das classes de exceção de topo, como Exception.

Imagine que criou uma aritmética completamente nova, regida pelas suas próprias leis e teoremas. É evidente que a divisão também foi redefinida, e tem de se comportar de uma forma diferente da divisão de rotina. É também claro que esta nova divisão deve levantar a sua própria exceção, diferente da `ZeroDivisionError`, mas é razoável assumir que em algumas circunstâncias, você (ou o utilizador da sua aritmética) pode querer tratar todas as divisões zero da mesma maneira.

Exigências como estas podem ser satisfeitas da forma apresentada no editor. Veja o código, e vamos analisá-lo:

* Definimos a nossa própria exceção, denominada `MyZeroDivisionError`, derivado a partir da incorporada `ZeroDivisionError`. Como pode ver, decidimos não acrescentar novos componentes à classe.

Com efeito, uma exceção a esta classe pode ser - dependendo do ponto de vista desejado - tratada como uma simples `ZeroDivisionError`, ou considerada separadamente.

* A função `do_the_division()` levanta ou uma exceção `MyZeroDivisionError` ou `ZeroDivisionError` , dependendo do valor do argumento.

A função é invocada quatro vezes no total, enquanto as duas primeiras invocações são tratadas utilizando apenas um ramo `except` (o mais geral) e os dois últimos com dois ramos diferentes, capazes de distinguir as exceções (não se esqueça: a ordem dos ramos faz uma diferença fundamental!)

```
class MyZeroDivisionError(ZeroDivisionError):	
    pass


def do_the_division(mine):
    if mine:
        raise MyZeroDivisionError("some worse news")
    else:		
        raise ZeroDivisionError("some bad news")


for mode in [False, True]:
    try:
        do_the_division(mode)
    except ZeroDivisionError:
        print('Division by zero')

for mode in [False, True]:
    try:
        do_the_division(mode)
    except MyZeroDivisionError:
        print('My division by zero')
    except ZeroDivisionError:
        print('Original division by zero')
```

## 3.6.1.7 Exceções mais uma vez

## Como criar a sua própria exceção: continuação

Quando se vai construir um universo completamente novo cheio de criaturas completamente novas que não têm nada em comum com todas as coisas familiares, pode querer **construir a sua própria estrutura de exceção**.

Por exemplo, se trabalhar num grande sistema de simulação destinado a modelar as atividades de um restaurante de pizza, pode ser desejável formar uma hierarquia separada de exceções.

Pode começar a construí-la **definindo uma exceção geral como uma nova classe base** para qualquer outra exceção especializada. Fizemo-lo da seguinte forma:
```
class PizzaError(Exception):
    def __init__(self, pizza, message):
        Exception.__init__(self, message)
        self.pizza = pizza
```

Nota: vamos recolher aqui informações mais específicas do que uma regular `Exception` faz, pelo que o nosso construtor aceitará dois argumentos:

* um que especifique uma pizza como um assunto do processo,
* e um que contenha uma descrição mais ou menos precisa do problema.

Como pode ver, passamos o segundo parâmetro ao construtor de superclasse, e guardamos o primeiro dentro da nossa própria propriedade.

Um problema mais específico (como um excesso de queijo) pode exigir uma exceção mais específica. É possível derivar a nova classe a partir da classe já definida `PizzaError` , como fizemos aqui:
```
class TooMuchCheeseError(PizzaError):
    def __init__(self, pizza, cheese, message):
        PizzaError._init__(self, pizza, message)
        self.cheese = cheese
```

A exceção `TooMuchCheeseError` precisa de mais informações do que a exceção regular `PizzaError` , por isso adicionamo-la ao construtor - o nome `cheese` é então armazenado para processamento posterior.

```
class PizzaError(Exception):
    def __init__(self, pizza, message):
        Exception.__init__(self, message)
        self.pizza = pizza


class TooMuchCheeseError(PizzaError):
    def __init__(self, pizza, cheese, message):
        PizzaError._init__(self, pizza, message)
        self.cheese = cheese
```

## 3.6.1.8 Exceções mais uma vez

## Como criar a sua própria exceção: continuação

Veja o código no editor. Juntámos as duas exceções previamente definidas e aproveitámo-las para trabalhar num pequeno trecho de exemplo.

Um destes é levantado dentro do `make_pizza()` funcionam quando qualquer uma destas duas situações erradas é descoberta: um pedido de pizza errado, ou um pedido de demasiado queijo.

Nota:

* remoção do ramo a começar por `except TooMuchCheeseError` fará com que todas as exceções que aparecem sejam classificadas como `PizzaError`;
* remoção do ramo a começar por `except PizzaErrorwill` causar as exceções `TooMuchCheeseError` a permanecer sem manuseio, e fará com que o programa termine.

A solução anterior, embora elegante e eficiente, tem uma fraqueza importante. Devido à forma algo descontraída de declarar os construtores, as novas exceções não podem ser usadas tal como estão sem uma lista completa dos argumentos requeridos.

Vamos remover esta fraqueza ao **definir os valores predefinidos para todos os parâmetros do construtor**. Dê uma vista de olhos:
```
class PizzaError(Exception):
    def __init__(self, pizza='uknown', message=''):
        Exception.__init__(self, message)
        self.pizza = pizza


class TooMuchCheeseError(PizzaError):
    def __init__(self, pizza='uknown', cheese='>100', message=''):
        PizzaError.__init__(self, pizza, message)
        self.cheese = cheese


def make_pizza(pizza, cheese):
    if pizza not in ['margherita', 'capricciosa', 'calzone']:
        raise PizzaError
    if cheese > 100:
        raise TooMuchCheeseError
    print("Pizza ready!")


for (pz, ch) in [('calzone', 0), ('margherita', 110), ('mafia', 20)]:
    try:
        make_pizza(pz, ch)
    except TooMuchCheeseError as tmce:
        print(tmce, ':', tmce.cheese)
    except PizzaError as pe:
        print(pe, ':', pe.pizza)
```

Agora, se as circunstâncias o permitirem, é possível utilizar os nomes das classes sozinhos.

```
class PizzaError(Exception):
    def __init__(self, pizza, message):
        Exception.__init__(self, message)
        self.pizza = pizza


class TooMuchCheeseError(PizzaError):
    def __init__(self, pizza, cheese, message):
        PizzaError.__init__(self, pizza, message)
        self.cheese = cheese


def make_pizza(pizza, cheese):
    if pizza not in ['margherita', 'capricciosa', 'calzone']:
        raise PizzaError(pizza, "no such pizza on the menu")
    if cheese > 100:
        raise TooMuchCheeseError(pizza, cheese, "too much cheese")
    print("Pizza ready!")

for (pz, ch) in [('calzone', 0), ('margherita', 110), ('mafia', 20)]:
    try:
        make_pizza(pz, ch)
    except TooMuchCheeseError as tmce:
        print(tmce, ':', tmce.cheese)
    except PizzaError as pe:
        print(pe, ':', pe.pizza)
```

## 3.6.1.9 RESUMO DA SEÇÃO

## Key takeaways

1. A função `else:` da declaração `try` é executado quando não houve nenhuma exceção durante a execução do bloco `try:` .

2. O método `finally:` da declaração `try` é **sempre** executado.

3. A sintaxe `except Exception_Name as an exception_object:` permite-lhe interceptar um objeto portador de informação sobre uma exceção pendente. A propriedade do objeto chamada `args` (um tuple) armazena todos os argumentos passados para o construtor do objeto.

4. As classes de exceção podem ser alargadas para as enriquecer com novas capacidades, ou para adotar as suas características a novas exceções definidas.

Por exemplo:
```
try:
    assert __name__ == "__main__"
except:
    print("fail", end=' ')
else:
    print("success", end=' ')
finally:
    print("done")
```

O código faz o output: `success done`.

**Exercício 1**

Qual é o output esperado do seguinte código?
```
import math

try:
    print(math.sqrt(9))
except ValueError:
    print("inf")
else:
    print("fine")
```

Verifique
```
3.0
fine
```


**Exercício 2**

Qual é o output esperado do seguinte código?
```
import math

try:
    print(math.sqrt(-9))
except ValueError:
    print("inf")
else:
    print("fine")
finally:
    print("the end")
```

Verifique
```
inf
the end
```

**Exercício 3**

Qual é o output esperado do seguinte código?
```
import math

class NewValueError(ValueError):
    def __init__(self, name, color, state):
        self.data = (name, color, state)

try:
    raise NewValueError("Enemy warning", "Red alert", "High readiness")
except NewValueError as nve:
    for arg in nve.args:
        print(arg, end='! ')
```

Verifique

`Enemy warning! Red alert! High readiness! `

## 3.6.1.10 Conclusão do Módulo

## Parabéns! Completou o PE2: Módulo 3.

Muito bem! Chegou ao fim do Módulo 3 e completou um marco importante na sua educação em programação Python. Aqui está um breve resumo dos objetivos que abordou e com os quais se familiarizou no Módulo 3:

* Os fundamentos e conceitos básicos da programação orientada a objetos;
* As diferenças entre as abordagens processuais e de objeto no exemplo da stack;
* propriedades (variáveis de instância e de classe, atributos)
* métodos (métodos de classe e de objeto, o construtor, parâmetros e propriedades)
* o conceito de herança (funções, métodos, hierarquias de classe, polimorfismo, composição, herança única vs. múltipla)
* a natureza objetiva das exceções em Python.

Está agora pronto para fazer o quiz do módulo e tentar o desafio final: Teste do módulo 3, que o ajudará a avaliar o que aprendeu até agora.