## 2.7.1.1 A anatomia das exceções

## Exceções

O Python 3 define **63 exceções incorporadas**, e todas elas formam uma **hierarquia em forma de árvore**, embora a árvore seja um pouco estranha, uma vez que a sua raiz está localizada no topo.  

Algumas das exceções incorporadas são mais gerais (incluem outras exceções) enquanto outras são completamente concretas (representam-se apenas a si próprias). Podemos dizer que **quanto mais próxima da raiz se encontra uma exceção, mais geral (abstrata) ela é**. Por sua vez, as exceções localizadas nas extremidades dos ramos (podemos chamar-lhes **folhas**) são concretas.

Dê uma vista de olhos à figura:

![HierarquiaEexceções](../Imagens/HierarquiaEexcecoes.jpg)

Mostra uma pequena secção da árvore de exceção completa. Vamos começar a examinar a árvore a partir da ZeroDivisionError folha.

Nota:

* ZeroDivisionError é um caso especial de uma classe de exceção mais geral chamada ArithmeticError;
* ArithmeticError é um caso especial de uma classe de exceção mais geral chamada apenas Exception;
* Exception é um caso especial de uma classe mais geral chamada BaseException;

Podemos descrevê-la da seguinte forma (note-se a direção das setas - apontam sempre para a entidade mais geral):


<p align="center">
  BaseException
</p>
<p align="center">
  ↑
</p>
<p align="center">
  Exception
</p>
<p align="center">
  ↑
</p>
<p align="center">
  ArithmeticError
</p>
<p align="center">
  ↑
</p>
<p align="center">
  ZeroDivisionError
</p>

Vamos mostrar-lhe como funciona esta generalização. Vamos começar com um código realmente simples.

## 2.7.1.2 A anatomia das exceções

## Exceções: continuação

Veja o código no editor. É um exemplo simples para começar. Execute-o.

```
try:
    y = 1 / 0
except ZeroDivisionError:
    print("Oooppsss...")

print("THE END.")
```

O output que esperamos ver é semelhante a este:

output

```
Oooppsss...
THE END.
```

Agora veja o código abaixo:

```
try:
    y = 1 / 0
except ArithmeticError:
    print("Oooppsss...")

print("THE END.")
```

Alguma coisa mudou nele - nós substituímos `ZeroDivisionError` por `ArithmeticError`.

Já sabe que `ArithmeticError` é uma classe geral, incluindo (entre outros) a exceção `ZeroDivisionError` .

Assim, o output do código permanece inalterado. Teste-o.

Isto também significa que a substituição do nome da exceção por `Exception` ou `BaseException` não vai mudar o comportamento do programa.

Vamos resumir:

* cada exceção levantada **cai no primeiro ramo correspondente**;
* o ramo correspondente não tem de especificar exatamente a mesma exceção - basta que a exceção seja **mais geral** (mais abstrata) do que a exceção levantada.

## 2.7.1.3 A anatomia das exceções

## Exceções: continuação

Veja o código no editor. O que vai acontecer aqui?

```
try:
    y = 1 / 0
except ZeroDivisionError:
    print("Zero Division!")
except ArithmeticError:
    print("Arithmetic problem!")

print("THE END.")
```

O primeiro ramo correspondente é o que contém `ZeroDivisionError`. Isto significa que a consola irá mostrar:

output

```
Zero division!
THE END.
```

Irá mudar alguma coisa se trocarmos os dois ramos `except` ? Tal como aqui em baixo:

```
try:
    y = 1 / 0
except ArithmeticError:
    print("Arithmetic problem!")
except ZeroDivisionError:
    print("Zero Division!")

print("THE END.")
```

A mudança é radical - o output do código é agora:

output

```
Arithmetic problem!
THE END.
```

Porquê, se a exceção levantada é a mesma que anteriormente?

A exceção é a mesma, mas a exceção mais geral é agora listada em primeiro lugar - também irá apanhar todas as divisões zero. Significa também que não há hipótese de qualquer exceção atingir o ramo ZeroDivisionError . Este ramo é agora completamente inacessível.

Lembre-se:

* a ordem dos ramos é importante!
* não ponha exceções mais gerais antes de exceções mais concretas;
* isto tornará este último inalcançável e inútil;
* Além disso, tornará o seu código confuso e inconsistente;
* O Python não irá gerar quaisquer mensagens de erro relativamente a esta questão.

## 2.7.1.4 A anatomia das exceções

## Exceções: continuação

Se quiser tratar **duas ou mais exceções** da mesma forma, pode usar a seguinte sintaxe:

```
try:
    :
except (exc1, exc2):
    :
```

É simplesmente necessário colocar todos os nomes de exceção envolvidos numa lista separada por vírgulas, e não esquecer os parêntesis.

Se uma **exceção for levantada dentro de uma função**, pode ser tratada:

* dentro da função;
* fora da função;

Vamos começar com a primeira variante - veja o código no editor.

A exceção `ZeroDivisionError` (sendo um caso concreto da classe de exceção ArithmeticError ) é levantada dentro da função `bad_fun()` , e não deixa a função - a própria função cuida dela.

```
def bad_fun(n):
    try:
        return 1 / n
    except ArithmeticError:
        print("Arithmetic Problem!")
    return None

bad_fun(0)

print("THE END.")
```

O programa acima faz o output:

output

```
Arithmetic problem!
THE END.
```

Também é possível deixar que a exceção se propague **fora da função**. Vamos testá-la agora.

Veja o código em baixo:

```
def bad_fun(n):
    return 1 / n

try:
    bad_fun(0)
except ArithmeticError:
    print("What happened? An exception was raised!")

print("THE END.")
```

O problema tem de ser resolvido pelo invocador (ou pelo invocador do invocador, e assim por diante).

O programa faz o output:

output

```
What happened? An exception was raised!
THE END.
```

Nota: a **exceção levantada pode ultrapassar os limites da função e do módulo**, e viajar através da cadeia de invocação procurando uma cláusula except correspondente capaz de a tratar.

Se não existir tal cláusula, a exceção permanece sem ser acionada, e o Python resolve o problema à sua maneira padrão - **terminando o seu código e emitindo uma mensagem de diagnóstico**.

Agora vamos suspender esta discussão, pois queremos apresentar-lhe uma nova instrução Python.

## 2.7.1.5 A anatomia das exceções | raise

## Exceções: continuação

A instrução `raise` levanta a exceção especificada chamada exc como se fosse levantada de uma forma normal (natural):

`raise exc`

Nota: `raise` é uma keyword.

A instrução permite-lhe:

* simular o levantamento de exceções reais (por exemplo, para testar a sua estratégia de tratamento)
* parcialmente tratar uma exceção e tornar outra parte do código responsável por completar o tratamento (separação de preocupações).

Veja o código no editor. É assim que o pode utilizar na prática.

```def bad_fun(n):
    raise ZeroDivisionError


try:
    bad_fun(0)
except ArithmeticError:
    print("What happened? An error?")

print("THE END.")
```

O output do programa permanece inalterado.

Desta forma, pode **testar a sua rotina de tratamento de exceções** sem forçar o código a fazer coisas estúpidas.


## 2.7.1.6 A anatomia das exceções | raise

## Exceções: continuação

A instrução `raise` também pode ser utilizada da seguinte maneira (observe a ausência do nome da exceção):

`raise`


Existe uma restrição grave: este tipo de instrução `raise` pode ser utilizada **dentro do ramo** `except` apenas; usá-la em qualquer outro contexto causa um erro.

A instrução voltará imediatamente a levantar a mesma exceção que é atualmente tratada.


Graças a isto, pode distribuir o tratamento de exceções entre diferentes partes do código.

Veja o código no editor. Execute-o - vamos vê-lo em ação.

```
def bad_fun(n):
    try:
        return n / 0
    except:
        print("I did it again!")
        raise


try:
    bad_fun(0)
except ArithmeticError:
    print("I see!")

print("THE END.")
```

A exceção `ZeroDivisionError` é levantado duas vezes:

* primeiro, dentro da parte do código try (isto é causado pela divisão real zero)
* segundo, dentro da parte except pela instrução raise .

Com efeito, o código faz o output:

output

```
I did it again!
I see!
THE END.
```

## 2.7.1.7 A anatomia das exceções | assert

## Exceções: continuação

Agora é um bom momento para lhe mostrar outra instrução Python, chamada `assert`. Esta é uma keyword.

`assert expression`

Como é que funciona?

* Ela avalia a expressão;
* se a expressão for avaliada para `True`, ou um valor numérico não nulo, ou uma string não vazia, ou qualquer outro valor diferente de `None`, não fará mais nada;
* caso contrário, levanta automática e imediatamente uma exceção chamada `AssertionError` (neste caso, dizemos que a assertion falhou)

Como pode ser utilizada?

* pode querer inseri-la no seu código onde quer estar **absolutamente a salvo de dados evidentemente errados**, e onde não tem a certeza absoluta de que os dados já foram cuidadosamente examinados (por exemplo, dentro de uma função utilizada por outra pessoa)
* levantar uma exceção `AssertionError` assegura que o seu código não produz resultados inválidos, e mostra claramente a natureza do fracasso;
* **as assertions não substituem as exceções nem validam os dados** - são seus suplementos.

Se as exceções e a validação de dados forem como uma condução cuidadosa, a assertion pode desempenhar o papel de um airbag.

Vamos ver a instrução assert em ação. Veja o código no editor. Execute-o.

```
import math

x = float(input("Enter a number: "))
assert x >= 0.0

x = math.sqrt(x)

print(x)
```

O programa corre sem falhas se introduzir um valor numérico válido maior ou igual a zero; caso contrário, ele para e emite a seguinte mensagem:

output

```
Traceback (most recent call last):
  File ".main.py", line 4, in 
    assert x >= 0.0
AssertionError
```

## 2.7.1.8 RESUMO DA SECÇÃO

# Key takeaways

1. Não pode acrescentar mais do que um ramo anónimo (não nomeado) `except` após os nomeados.
   
```
:
# The code that always runs smoothly.
:
try:
    :
    # Risky code.
    :
except Except_1:
    # Crisis management takes place here.
except Except_2:
    # We save the world here.
except:
    # All other issues fall here.
:
# Back to normal.
:
```

2. Todas as exceções Python pré-definidas formam uma hierarquia, ou seja, algumas delas são mais gerais (a que se chama `BaseException` é a mais geral), enquanto outras são mais ou menos concretas (por exemplo, `IndexError` é mais concreta do que `LookupError`).

Não deve colocar exceções mais concretas antes das mais gerais dentro da mesma sequência de ramificações `except` . Por exemplo, pode fazer isto:

```
try:
    # Risky code.
except IndexError:
    # Taking care of mistreated lists
except LookupError:
    # Dealing with other erroneous lookups
```

mas não o faça (a menos que tenha a certeza absoluta de que deseja que alguma parte do seu código seja inútil)

```
try:
    # Risky code.
except LookupError:
    # Dealing with erroneous lookups
except IndexError:
    # You'll never get here 
```

3. A declaração Python `raise ExceptionName` pode levantar uma exceção sob demanda. A mesma declaração, mas sem ExceptionName, pode ser usada dentro do ramo `try` **apenas**, e levanta a mesma exceção que está atualmente a ser tratada.

4. A declaração Python `assert expression` avalia a expressão e levanta a exceção `AssertError` quando a expressão é igual a zero, uma string vazia ou None. Pode utilizá-la para proteger algumas partes críticas do seu código de dados devastadores.

**Exercício 1**

Qual é o output esperado do seguinte código?
```
try:
    print(1/0)
except ZeroDivisionError:
    print("zero")
except ArithmeticError:
    print("arith")
except:
    print("some")
```

Verifique

`zero`


**Exercício 2**

Qual é o output esperado do seguinte código?

```
try:
    print(1/0)
except ArithmeticError:
    print("arith")
except ZeroDivisionError:
    print("zero")
except:
    print("some")
```

Verifique

`arith`


**Exercício 3**

Qual é o output esperado do seguinte código?

```
def foo(x):
    assert x
    return 1/x


try:
    print(foo(0))
except ZeroDivisionError:
    print("zero")
except:
    print("some")
```

Verifique

`some`