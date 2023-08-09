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