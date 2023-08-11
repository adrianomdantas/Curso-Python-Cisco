## 3.2.1.1 Loops em Python | while
## Fazer loop ao seu código com while

Concorda com a declaração apresentada abaixo?
```
while there is something to do
    do it
```

Note-se que este registo também declara que se não houver nada a fazer, nada acontecerá.

Em geral, em Python, um loop pode ser representado da seguinte forma:
```
while conditional_expression:
    instruction
```

Se notar algumas semelhanças com a instrução if, não há problema. De facto, a diferença sintática é apenas uma: usa-se a palavra `while` em vez da palavra `if`.

A diferença semântica é mais importante: quando a condição é cumprida, if executa as suas declarações **apenas uma vez**; `while` **repete a execução enquanto a condição se avalie a** `True`.

Nota: todas as regras relativas à **indentação** são aplicáveis também aqui. Vamos mostrar-lhe isso em breve.

Veja o algoritmo abaixo:
```
while conditional_expression:
    instruction_one
    instruction_two
    instruction_three
    :
    :
    instruction_n
```

Agora é importante lembrar que:

* se quiser executar **mais do que uma declaração dentro de um** `while`, deve (como com `if`) **indentar** todas as instruções da mesma forma;
* uma instrução ou conjunto de instruções executadas no interior do loop `while` é chamada **corpo do loop**;
* se a condição é `False` (igual a zero) logo que é testada pela primeira vez, o corpo não é executado nem uma vez (note-se a analogia de não ter de fazer nada se não houver nada a fazer);
* o corpo deve ser capaz de alterar o valor da condição, porque se a condição estiver `True` no início, o corpo pode correr continuamente até ao infinito (repare que fazer uma coisa normalmente diminui o número de coisas a fazer).

## m loop infinito

Um loop infinito, também chamado **endless loop**, é uma sequência de instruções num programa que se repete indefinidamente (loop interminável).

Eis um exemplo de um loop que não é capaz de terminar a sua execução:
```
while True:
    print("I'm stuck inside a loop.")
```

Este loop será infinitamente imprimido `"I'm stuck inside a loop."` no ecrã.

**NOTA**

Se quiser obter a melhor experiência de aprendizagem ao ver como se comporta um loop infinito, lance o IDLE, crie um New File, copie-cole o código acima, guarde o seu ficheiro, e execute o programa. O que irá ver é a sequência interminável de strings `"I'm stuck inside a loop."` impressas na janela do console do Python. Para terminar o seu programa, basta premir Ctrl-C (ou Ctrl-Break em alguns computadores). Isto causará a chamada exceção **KeyboardInterrupt** e deixa o seu programa sair do loop. Falaremos sobre isso mais tarde no curso.
<hr>

Voltemos ao esboço do algoritmo que lhe mostrámos recentemente. Vamos mostrar-lhe como utilizar este loop recentemente aprendido para encontrar o maior número a partir de um grande conjunto de dados introduzidos.

Analise o programa com cuidado. Veja onde o loop começa (linha 8). Localize o corpo do loop e descubra **como é que o corpo sai**:
```
# Store the current largest number here.
largest_number = -999999999

# Input the first value.
number = int(input("Enter a number or type -1 to stop: "))

# If the number is not equal to -1, continue.
while number != -1:
    # Is number larger than largest_number?
    if number > largest_number:
        # Yes, update largest_number.
        largest_number = number
    # Input the next number.
    number = int(input("Enter a number or type -1 to stop: "))

# Print the largest number.
print("The largest number is:", largest_number)
```

Verifique como este código implementa o algoritmo que lhe mostramos anteriormente.

## 3.2.1.2 em Python | while
## Os loops loop while : mais exemplos

Vejamos outro exemplo empregando o loop `while` . Siga os comentários para descobrir a ideia e a solução.
```
# A program that reads a sequence of numbers
# and counts how many numbers are even and how many are odd.
# The program terminates when zero is entered.

odd_numbers = 0
even_numbers = 0

# Read the first number.
number = int(input("Enter a number or type 0 to stop: "))

# 0 terminates execution.
while number != 0:
    # Check if the number is odd.
    if number % 2 == 1:
        # Increase the odd_numbers counter.
        odd_numbers += 1
    else:
        # Increase the even_numbers counter.
        even_numbers += 1
    # Read the next number.
    number = int(input("Enter a number or type 0 to stop: "))

# Print results.
print("Odd numbers count:", odd_numbers)
print("Even numbers count:", even_numbers)
```

Certas expressões podem ser simplificadas sem alterar o comportamento do programa.

Tente lembrar-se de como o Python interpreta a verdade de uma condição e observe que estas duas formas são equivalentes:

`while number != 0:` e `while number:`.

A condição que verifica se um número é ímpar também pode ser codificada nestas formas equivalentes:

`if number % 2 == 1:` e `if number % 2:`.


# Usar uma variável counter para sair de um loop

Veja o snippet abaixo:
```
counter = 5
while counter != 0:
    print("Inside the loop.", counter)
    counter -= 1
print("Outside the loop.", counter)
```

Este código destina-se a imprimir a string `"Inside the loop."` e o valor armazenado na variável counter durante um determinado loop exatamente cinco vezes. Uma vez que a condição não foi atendida (a variável `counter` atingiu `0`), o loop é encerrado, e a mensagem `"Outside the loop."` bem como o valor armazenado em `counter` é impresso.

Mas há uma coisa que pode ser escrita de forma mais compacta - a condição do loop `while` .

Consegue ver a diferença?
```
counter = 5
while counter:
    print("Inside the loop.", counter)
    counter -= 1
print("Outside the loop.", counter)
```

É mais compacto do que anteriormente? Um pouco. É mais legível? Isso é discutível.

**LEMBRE-SE**

Não se sinta obrigado a codificar os seus programas de uma forma que seja sempre a mais curta e a mais compacta. A legibilidade pode ser um fator mais importante. Mantenha o seu código preparado para um novo programador.

## 3.2.1.3 LAB: Essenciais do loop while - Adivinhe o número secreto
## 3.2.1.4 Loops em Python | for
## Fazer loop ao seu código com for

Outro tipo de loop disponível em Python vem da observação de que por vezes é mais importante **contar as "voltas" do loop** do que verificar as condições.

Imagine que o corpo de um loop precisa de ser executado exatamente cem vezes. Se desejar utilizar o loop `while` para o fazer, pode ser assim:
```
i = 0
while i < 100:
    # do_something()
    i += 1
```

Seria bom se alguém pudesse fazer esta contagem aborrecida por si. Isso é possível?

Claro que é - há um loop especial para estes tipos de tarefas, e é chamado `for`.

Na verdade, o loop `for` foi concebido para realizar tarefas mais complicadas - **pode "navegar" por grandes coleções de dados item por item**. Mostraremos como fazê-lo em breve, mas neste momento vamos apresentar uma variante mais simples da sua aplicação.
<hr>

Dê uma vista de olhos no snippet:
```
for i in range(100):
    # do_something()
    pass
```

Existem alguns novos elementos. Deixe-nos falar sobre eles:

* a keyword for abre o loop `for` ; nota - não há nenhuma condição depois; não é preciso pensar nas condições, uma vez que são verificadas internamente, sem qualquer intervenção;
* qualquer variável após a keyword for é a **variável de controle** do loop; conta as voltas do loop, e fá-lo automaticamente;
* a keyword `in` introduz um elemento de sintaxe que descreve a gama de valores possíveis que estão a ser atribuídos à variável de controle;
* a função `range()` (esta é uma função muito especial) é responsável por gerar todos os valores desejados da variável de controle; no nosso exemplo, a função irá criar (podemos mesmo dizer que irá **alimentar** o loop com) valores subsequentes a partir do conjunto seguinte: 0, 1, 2 .. 97, 98, 99; nota: neste caso, a função `range()` começa o seu trabalho a partir do 0 e termina um passo (um número inteiro) antes do valor do seu argumento;
* note a keyword pass dentro do corpo do loop - não faz nada; é uma **instrução vazia** - colocamo-la aqui porque a `for` sintaxe do laço exige pelo menos uma instrução dentro do corpo (a propósito - `if`, `elif`, `else` e `while` expressam a mesma coisa)
Os nossos próximos exemplos serão um pouco mais modestos no número de repetições do loop.

Veja o snippet abaixo. Consegue prever o seu output?
```
for i in range(10):
    print("The value of i is currently", i)
```

Execute o código para verificar se estava certo.
```
>>> for i in range(10):
    print("The value of i is currently", i)

    
The value of i is currently 0
The value of i is currently 1
The value of i is currently 2
The value of i is currently 3
The value of i is currently 4
The value of i is currently 5
The value of i is currently 6
The value of i is currently 7
The value of i is currently 8
The value of i is currently 9
>>> 
```

**Nota:**

* o loop foi executado dez vezes (é o argumento da função `range()` )
* o valor da última variável de controlo é 9 (não 10, visto começar a partir de 0, não a partir de 1)
<hr>

A função `range()` pode ser equipada com dois argumentos, e não apenas um:
```
for i in range(2, 8):
    print("The value of i is currently", i)
```

Neste caso, o primeiro argumento determina o (primeiro) valor inicial da variável de controle.

O último argumento mostra o primeiro valor que a variável de controlo não será atribuída.

Nota: a função `range()` **aceita apenas inteiros como seus argumentos**, e gera sequências de inteiros.

Consegue adivinhar o output do programa? Execute-o para verificar se também estava certo agora.

O primeiro valor mostrado é `2` (retirado do primeiro argumento `range()`.)

O último é `7` (embora o `range()` segundo argumento seja `8`).

## 3.2.1.5 Loops em Python | for

# Mais sobre o loop for e a range() função com três argumentos

A função `range()` também pode aceitar **três argumentos** - dê uma olhada no código no editor.
```
for i in range(2, 8, 3):
    print("The value of i is currently", i)
```

O terceiro argumento é um **incremento** - é um valor acrescentado para controlar a variável em cada volta do loop (como se pode suspeitar, **o valor por defeito do incremento é 1**).

Consegue dizer-nos quantas linhas irão aparecer na consola, e que valores irão conter?

Execute o programa para saber se estava certo.


Deve ser capaz de ver as seguintes linhas na janela da consola:
```
The value of i is currently 2
The value of i is currently 5
```

Sabe porquê? O primeiro argumento passado para a função `range()` diz-nos qual o **número inicial da sequência (logo, `2` no output). O segundo argumento informa à função onde parar a sequência (a função gera números até ao número indicado pelo segundo argumento, mas não o inclui). Finalmente, o terceiro argumento indica a etapa, que na realidade significa a diferença entre cada número na sequência de números gerados pela função.**

`2` (número inicial) → `5` (`2` incremento de `3` é igual a `5` - o número está dentro do intervalo de 2 a 8) → `8` (`5` incremento de 3 é igual a 8 - o número não está dentro do intervalo de 2 a 8, porque o parâmetro stop não está incluído na sequência de números gerados pela função.)
<hr>

Nota: se o conjunto gerado pela função `range()` está vazio, o loop não irá executar de todo o seu corpo.

Tal como aqui - não haverá output:
```
for i in range(1, 1):
    print("The value of i is currently", i)
```
<hr>

Nota: o conjunto gerado pelo `range()` tem de estar ordenado por **ordem crescente**. Não há como forçar o `range()` a criar um conjunto de uma forma diferente quando a função `range()` aceita exatamente dois argumentos. Isto significa que o segundo argumento de `range()` deve ser maior que o primeiro.

Logo, também não haverá output aqui:
`
for i in range(2, 1):
    print("The value of i is currently", i)
`
<hr>

Vamos dar uma olhada num programa curto, cuja tarefa é escrever algumas das primeiras potências de dois:
```
power = 1
for expo in range(16):
    print("2 to the power of", expo, "is", power)
    power *= 2
```

A variável `expo` é usada como uma variável de controle para o loop, e indica o valor atual do expoente. A exponenciação em si é substituída pela multiplicação por dois. Uma vez que 2<sup>0</sup> é igual a 1, então 2 x; 1 é igual a 2<sup>1</sup>, 2 x; 2<sup>1</sup> é igual a 2<sup>2</sup>, e assim por diante. Qual é o maior expoente para o qual o nosso programa ainda imprime o resultado?

Execute o código e verifique se o output corresponde às suas expetativas.

```
power = 1
for expo in range(16):
    print("2 to the power of", expo, "is", power)
    power *= 2

2 to the power of 0 is 1
2 to the power of 1 is 2
2 to the power of 2 is 4
2 to the power of 3 is 8
2 to the power of 4 is 16
2 to the power of 5 is 32
2 to the power of 6 is 64
2 to the power of 7 is 128
2 to the power of 8 is 256
2 to the power of 9 is 512
2 to the power of 10 is 1024
2 to the power of 11 is 2048
2 to the power of 12 is 4096
2 to the power of 13 is 8192
2 to the power of 14 is 16384
2 to the power of 15 is 327686
```

## 3.2.1.6 LAB: Essenciais do loop for - contar mississippily
## 3.2.1.7 controlo do Loop em Python | break e continue
## Os loops break e declarações continue .

Até agora, temos tratado o corpo do loop como uma sequência indivisível e inseparável de instruções que são executadas completamente a cada volta do loop. No entanto, como programador, poderá ser confrontado com as seguintes escolhas:

* parece que é desnecessário continuar o loop como um todo; deve abster-se de continuar a execução do corpo do loop e continuar;
* parece que é necessário iniciar a próxima volta do loop sem completar a execução da volta atual.

O Python fornece duas instruções especiais para a execução de ambas estas tarefas. Digamos, por uma questão de precisão, que a sua existência na linguagem não é necessária - um programador experiente é capaz de codificar qualquer algoritmo sem estas instruções. Tais adições, que não melhoram o poder expressivo da linguagem, mas apenas simplificam o trabalho do programador, são por vezes chamadas de `doces sintéticos`, ou `açúcar sintético`.

Estas duas instruções são:

* `break` - sai imediatamente do loop, e termina incondicionalmente a operação do loop; o programa começa a executar a instrução mais próxima após o corpo do loop;
* `continue` - comporta-se como se o programa tivesse subitamente chegado ao fim do corpo; inicia-se a volta seguinte e a expressão da condição é testada imediatamente.

Ambas as palavras são **keywords**.

Agora vamos mostrar-lhe dois exemplos simples para ilustrar como as duas instruções funcionam. Veja o código no editor. Execute o programa e analise o output. Modifique o código e experimente.

![break e continue](Imagens/BreakContinue.jpg)
```
# break - example

print("The break instruction:")
for i in range(1, 6):
    if i == 3:
        break
    print("Inside the loop.", i)
print("Outside the loop.")


# continue - example

print("\nThe continue instruction:")
for i in range(1, 6):
    if i == 3:
        continue
    print("Inside the loop.", i)
print("Outside the loop.")

CONSOLE>>

The break instruction:
Inside the loop. 1
Inside the loop. 2
Outside the loop.

The continue instruction:
Inside the loop. 1
Inside the loop. 2
Inside the loop. 4
Inside the loop. 5
Outside the loop.
```

## 3.2.1.8 controlo do Loop em Python | break e continue
## Os loops break e declarações continue : mais exemplos

Voltemos ao nosso programa que reconhece o maior entre os números introduzidos. Iremos convertê-lo duas vezes, utilizando as instruções `break` e `continue` .

Analise o código, e julgue se e como utilizaria qualquer um deles.

A variante `break` vai aqui:
```
largest_number = -99999999
counter = 0

while True:
    number = int(input("Enter a number or type -1 to end program: "))
    if number == -1:
        break
    counter += 1
    if number > largest_number:
        largest_number = number

if counter != 0:
    print("The largest number is", largest_number)
else:
    print("You haven't entered any number.")
```

Execute-a, teste-a e experimente com ela.
<hr>

E agora a variante `continue` :
```
largest_number = -99999999
counter = 0

number = int(input("Enter a number or type -1 to end program: "))

while number != -1:
    if number == -1:
        continue
    counter += 1

    if number > largest_number:
        largest_number = number
    number = int(input("Enter a number or type -1 to end program: "))

if counter:
    print("The largest number is", largest_number)
else:
    print("You haven't entered any number.")

```
Olhe cuidadosamente, o utilizador introduz o primeiro número **antes** de o programa entrar no loop `while` . O número subsequente é inserido quando o programa **já está em loop**.

Novamente - execute o programa, teste-o e experimente com ele.

## 3.2.1.9 LAB: A declaração break - Preso num loop
## 3.2.1.10 LAB: A declaração continue - o Ugly Vowel Eater
## 3.2.1.11 LAB: A declaração continue - o Pretty Vowel Eater
## 3.2.1.12 Loops Python | else
## Os loops while e o ramo else .

Ambos os loops, `while` e `for`, têm uma característica interessante (e raramente usada).

Vamos mostrar-lhe como funciona - tente julgar por si próprio se é utilizável e se pode viver sem ela ou não.

Por outras palavras, tente convencer-se se a característica é valiosa e útil, ou se é apenas **açúcar sintático**.

Veja o snippet no editor. Há algo estranho no final - a keyword `else` .

Como pode ter suspeitado, **os loops podem ter o ramo** `else` **também, como** `if`.

O ramo do loop `else` é **sempre executado uma vez, independentemente de o loop ter entrado no seu corpo ou não**.

Consegue adivinhar o output? Execute o programa para verificar se estava certo.

Modifique um pouco o anippet para que o loop não tenha hipótese de executar o seu corpo nem mesmo uma vez:
```
i = 5
while i < 5:
    print(i)
    i += 1
else:
    print("else:", i)
```

A condição whileé False no início - consegue vê-la?

Execute e teste o programa, e verifique se o ramo else foi executado ou não.

```
i = 1
while i < 5:
    print(i)
    i += 1
else:
    print("else:", i)

>>>
1
2
3
4
else: 5
```

## 3.2.1.13 Loops Python | else
## Os loops for e o ramo else .

`for` os loops comportam-se de forma um pouco diferente - observe o snippet no editor e execute-o.

O output pode ser um pouco surpreendente.
```
for i in range(5):
    print(i)
else:
    print("else:", i)

```
A variável `i` retém o seu último valor.
```
0
1
2
3
4
else: 4
```
Modifique um pouco o código para levar a cabo mais uma experiência.
```
i = 111
for i in range(2, 1):
    print(i)
else:
    print("else:", i)
```

Consegue adivinhar o output?

`else: 111`

O corpo do loop não será executado aqui. Nota: atribuímos a variável `i` antes do loop.

Execute o programa e verifique o seu output.

Quando o corpo do loop não é executado, a variável de controlo retém o valor que tinha antes do loop.

Nota: **se a variável de controle não existir antes do início do loop, não existirá quando a execução atingir o ramo** `else` .

O que acha desta variante de `else`?

Agora vamos falar-lhe de alguns outros tipos de variáveis. As nossas variáveis atuais só podem **armazenar um valor de cada vez**, mas há variáveis que podem fazer muito mais - podem **armazenar tantos valores quantos você quiser**.

## 3.2.1.14 LAB: Essenciais do loop while
