## 2.6.1.1 Erros - o pão diário do programador

## Erros, fracassos e outras pragas

**Qualquer coisa que possa correr mal, irá correr mal.**

Esta é a lei de Murphy, e funciona em todo o lado e sempre. A execução do seu código também pode correr mal. Se puder, irá.

Veja o código no editor. Há pelo menos duas formas possíveis de "correr mal". Consegue vê-las?

```
import math

x = float(input("Enter x: "))
y = math.sqrt(x)

print("The square root of", x, "equals to", y)
```

* Como um utilizador é capaz de introduzir uma string completamente arbitrária, **não há garantia de que a string possa ser convertida num valor float** - esta é a primeira vulnerabilidade do código;
* a segundo é que a função `sqrt()` **falha se obtiver um argumento negativo**.

Poderá receber uma das seguintes mensagens de erro.

Algo assim:

output

```
Enter x: Abracadabra

Traceback (most recent call last):

  File "sqrt.py", line 3, in <module>

    x = float(input("Enter x: "))

ValueError: could not convert string to float: 'Abracadabra'
```

Ou algo assim:

output

```
Enter x: -1

Traceback (most recent call last):

  File "sqrt.py", line 4, in <module>

    y = math.sqrt(x)

ValueError: math domain error
```

Pode proteger-se de tais surpresas? Claro que pode. Além disso, tem de o fazer para ser considerado um bom programador.

## 2.6.1.2 Erros - o pão diário do programador

## Exceções

Cada vez que o seu código tenta fazer algo de errado/tolo/irresponsável/maluco/imprevisível, o Python faz duas coisas:

* **para o seu programa;**
* cria um tipo especial de dados, chamado uma **exceção.**
  
Ambas estas atividades são designadas por **levantar uma exceção**. Podemos dizer que o Python levanta sempre uma exceção (ou que **foi levantada uma exceção**) quando não tem ideia do que fazer com o seu código.

O que acontece a seguir?

* a exceção levantada espera que alguém ou alguma coisa a note e se encarregue dela;
* se nada acontecer para tratar da exceção levantada, o programa será **terminado à força**, e verá uma **mensagem de erro** enviada para a consola pelo Python;
* caso contrário, se a exceção for cuidada e **tratada** adequadamente, o programa suspenso pode ser retomado e a sua execução pode continuar.

O Python fornece ferramentas eficazes que lhe permitem **observar exceções, identificá-las e tratá-las** eficientemente. Isto é possível devido ao facto de todas as potenciais exceções terem os seus nomes inequívocos, pelo que se pode categorizá-los e reagir adequadamente.

Já conhece alguns **nomes de exceção**. Dê uma vista de olhos à seguinte mensagem de diagnóstico:

output

`ValueError: math domain error` 

A palavra destacada acima é apenas o nome da exceção. Vamos familiarizar-nos com algumas outras exceções.

## 2.6.1.3 Erros - o pão diário do programador

## Exceções: continuação

Veja o código no editor. Execute o programa (obviamente incorreto).

```
value = 1
value /= 0
```

Verá a seguinte mensagem em resposta:

output

```
Traceback (most recent call last):
File "div.py", line 2, in 
value /= 0
ZeroDivisionError: division by zero
```

Este erro de exceção é chamado ZeroDivisionError.

## 2.6.1.4 Erros - o pão diário do programador

## Exceções: continuação

Veja o código no editor. O que acontecerá quando o executar? Verifique.

```
my_list = []
x = my_list[0]
```

Verá a seguinte mensagem em resposta:

output
```
Traceback (most recent call last):
File "lst.py", line 2, in 
x = list[0]
IndexError: list index out of range
```

Este é o IndexError.

## 2.6.1.5 Erros - o pão diário do programador

## Exceções: continuação

Como se tratam (em inglês, handle) as exceções? A palavra `try` é fundamental para a solução.

Além disso, também é uma keyword.

A receita para o sucesso é a seguinte:

* primeiro, é preciso **tentar fazer alguma coisa;**
* a seguir, tem de **verificar se tudo correu bem.**

Mas não seria melhor verificar primeiro todas as circunstâncias, e depois fazer algo apenas se for seguro?

Assim como o exemplo no editor.

```
first_number = int(input("Enter the first number: "))
second_number = int(input("Enter the second number: "))

if second_number != 0:
    print(first_number / second_number)
else:
    print("This operation cannot be done.")

print("THE END.")
```

Assumidamente, esta forma pode parecer a mais natural e compreensível, mas na realidade este método não torna a programação mais fácil. Todas estas verificações podem tornar o **seu código inchado e ilegível.**

O Python prefere uma abordagem completamente diferente.

## 2.6.1.6 Erros - o pão diário do programador | try-except

## Exceções: continuação

Veja o código no editor. Esta é a abordagem favorita do Python.

```
first_number = int(input("Enter the first number: "))
second_number = int(input("Enter the second number: "))

try:
    print(first_number / second_number)
except:
    print("This operation cannot be done.")

print("THE END.")
```

Nota:

* a keyword `try` **inicia um bloco do código** que pode ou não estar a funcionar corretamente;
* a seguir, o Python tenta realizar a ação arriscada; se falhar, é levantada uma exceção e o Python começa a procurar por uma solução;
* a keyword `except` inicia um pedaço de código que será executado **se alguma coisa dentro do bloco** `try` **correr mal** - se uma exceção é levantada dentro de um bloco `try` anterior, **falhará aqui**, pelo que o código localizado após a keyword except deverá fornecer uma **reação adequada** à exceção levantada;
* retornar ao nível de nesting anterior termina a secção do **try-except**.

Execute o código e teste o seu comportamento.


Vamos resumir isto:

try:
    :
    :
except:
    :
    :


* no primeiro passo, o Python tenta executar todas as instruções colocadas entre as `try:` e `except:` declarações;
* se nada estiver errado com a execução e todas as instruções forem executadas com sucesso, a execução salta para o ponto após a última linha do bloco `except:` , e a execução do bloco é considerada completa;
* se alguma coisa correr mal dentro do bloco `try:` e `except:` , a execução salta imediatamente para fora do bloco e para a primeira instrução localizada após a keyword `except:` ; isto significa que algumas das instruções do bloco podem ser silenciosamente omitidas.

## 2.6.1.7 Erros - o pão diário do programador | try-except

## Exceções: continuação

Veja o código no editor. Ajudá-lo-á a compreender este mecanismo.

```
try:
    print("1")
    x = 1 / 0
    print("2")
except:
    print("Oh dear, something went wrong...")

print("3")

```

Esta é o output que produz:

output

```
1
Oh dear, something went wrong...
3
```

Nota: a instrução print("2") foi perdida no processo.

## 2.6.1.8 Erros - o pão diário do programador | try-except

## Exceções: continuação

Esta abordagem tem uma desvantagem importante - se houver a possibilidade de mais do que uma exceção poder saltar para um ramo `except:` , poderá ter **dificuldade em descobrir o que realmente aconteceu.**

Tal como no nosso código no editor. Execute-o e veja o que acontece.

```
try:
    x = int(input("Enter a number: "))
    y = 1 / x
except:
    print("Oh dear, something went wrong...")

print("THE END.")
```

A mensagem: `Oh dear, something went wrong...` que aparece na consola nada diz sobre a razão, enquanto que existem duas causas possíveis para a exceção:

* dados não inteiros inseridos pelo utilizador;
* um valor inteiro igual a 0 atribuído à variável x .

Tecnicamente, existem duas maneiras de resolver o problema:

* construir dois blocos consecutivos try-except , um para cada possível motivo de exceção (fácil, mas causará um crescimento do código desfavorável)
* utilizar uma variante mais avançada da instrução.

É assim que se parece:

```
try:
    :
except exc1:
    :
except exc2:
    :
except:
    :
```

É assim que funciona:

* se o ramo `try` levanta a exceção `exc1` , será tratado pelo bloco `except exc1:` ;
* da mesma forma, se o ramo `try` levanta a exceção `exc2` , será tratado pelo bloco except exc2: ;
* se o ramo `try` levanta qualquer outra exceção, será tratado pelo bloco não nomeado except .

Passemos à próxima parte do curso e vejamo-lo em ação.

## 2.6.1.9 Erros - o pão diário do programador | try-except

## Exceções: continuação

Veja o código no editor. A nossa solução está lá.

```
try:
    x = int(input("Enter a number: "))
    y = 1 / x
    print(y)
except ZeroDivisionError:
    print("You cannot divide by zero, sorry.")
except ValueError:
    print("You must enter an integer value.")
except:
    print("Oh dear, something went wrong...")

print("THE END.")
```

O código, quando executado, produz uma das quatro variantes de output seguintes:

* se introduzir um valor inteiro válido, não nulo (por exemplo 5) diz:

output

```
0.2
THE END.
```

se introduzir `0`, diz:

output

```
You cannot divide by zero, sorry.
THE END.
```

se introduzir qualquer string não inteira, verá:

output

```
You must enter an integer value.
THE END.
```

(localmente na sua máquina) se premir Ctrl-C enquanto o programa aguarda a entrada do utilizador (o que provoca uma exceção chamada KeyboardInterrupt), o programa diz:

output

```
Oh dear, something went wrong...
THE END.
```

## 2.6.1.10 Erros - o pão diário do programador | try-except

## Exceções: continuação

Não se esqueça:

* os ramos `except` são pesquisados na mesma ordem em que aparecem no código;
* não deve utilizar mais do que um, exceto um ramo com um certo nome de exceção;
* o número de diferentes ramos `except` é arbitrário - a única condição é que se utilizar `try`, deve colocar pelo menos um `except` (nomeado ou não) depois dele;
* a keyword `except` não deve ser utilizada sem um precedente `try`;
* se algum dos ramos `except` for executado, nenhum outro ramo será visitado;
* se nenhum dos ramos `except` especificados correspondem à exceção levantada, a exceção permanece sem ser tratada (discutiremos isso em breve)
* se um não nomeado `except` ramo existir (um sem nome de exceção), tem de ser especificado como o último.

```
try:
    :
except exc1:
    :
except exc2:
    :
except:
    :
```

Vamos continuar as experiências agora.

Veja o código no editor. Modificámos o programa anterior - removemos o ramo `ZeroDivisionError` .

```
try:
    x = int(input("Enter a number: "))
    y = 1 / x
    print(y)
except ValueError:
    print("You must enter an integer value.")
except:
    print("Oh dear, something went wrong...")

print("THE END.")
```

O que acontece agora se o utilizador introduzir `0` como um input?

Como **não há ramos dedicados** para divisão por zero, a exceção levantada cai no **ramo geral (sem nome)**; isto significa que, neste caso, o programa dirá:

output

```
Oh dear, something went wrong...
THE END.
```

Experimente você mesmo. Execute o programa.

## 2.6.1.11 Erros - o pão diário do programador | try-except

## Exceções: continuação

Vamos estragar o código mais uma vez.

Olhe para o programa no editor. Desta vez, retirámos o ramo não nomeado.

```
try:
    x = int(input("Enter a number: "))
    y = 1 / x
    print(y)
except ValueError:
    print("You must enter an integer value.")

print("THE END."
```

O utilizador insere `0` mais uma vez, e:

* a exceção levantada não será tratada por `ValueError` - não tem nada a ver com isso;
* uma vez que não há outro ramo, deve ver esta mensagem:

output

```
Traceback (most recent call last):
File "exc.py", line 3, in 
y = 1 / x
ZeroDivisionError: division by zero
```

Aprendeu bastante sobre o tratamento de exceções em Python. Na secção seguinte, centrar-nos-emos nas exceções incorporadas em Python e nas suas hierarquias.

## 2.6.1.12 RESUMO DA SECÇÃO

## Key takeaways

1. Uma exceção é um evento na execução de um programa causado por uma situação anormal. A exceção deve ser tratada para evitar a terminação do programa. A parte do seu código que é suspeita de ser a origem da exceção deve ser colocada dentro do ramo `try` .

Quando a exceção acontece, a execução do código não é terminada, mas em vez disso salta para o ramo `except` . Este é o local onde deve ter lugar o tratamento da exceção. O esquema geral de tal construção parece-se com o seguinte:

```
:
# The code that always runs smoothly.
:
try:
    :
    # Risky code.
    :
except:
    :
    # Crisis management takes place here.
    : 
:
# Back to normal.
:
```

1. Se precisar de tratar de mais do que uma exceção proveniente do mesmo ramo `try` , pode adicionar mais do que um ramo `except` , mas é preciso rotulá-los com nomes de exceção diferentes, como este:

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
:
# Back to normal.
:
```

No máximo, um dos ramos `except` é executado - nenhum dos ramos é executado quando a exceção levantada não coincide com as exceções especificadas.


3. Não pode acrescentar mais do que um ramo anónimo (não nomeado) `except` após os nomeados.
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


**Exercício 1**

Qual é o output esperado do seguinte código?
```
try:
    print("Let's try to do this")
    print("#"[2])
    print("We succeeded!")
except:
    print("We failed")
print("We're done")
```

Verifique
```
Let's try to do this
We failed
We're done
```

**Exercício 2**

Qual é o output esperado do seguinte código?
```
try:
    print("alpha"[1/0])
except ZeroDivisionError:
    print("zero")
except IndexingError:
    print("index")
except:
    print("some")
```

Verifique

`zero`

