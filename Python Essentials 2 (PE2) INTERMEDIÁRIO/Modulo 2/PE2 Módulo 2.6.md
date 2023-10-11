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
