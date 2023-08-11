## 2.5.1.1 Um comentário sobre os comentário
## Deixar comentários em código: porquê, como, e quando

Pode querer colocar algumas palavras dirigidas não ao Python mas aos humanos, normalmente para explicar a outros leitores do código como funcionam os truques utilizados no código, ou os significados das variáveis, e para manter a informação armazenada sobre quem é o autor e quando o programa foi escrito.

Uma observação inserida no programa, que é **omitida em runtime**, é chamada um **comentário**.

Como se deixa este tipo de comentário no source code? Tem de ser feito de uma forma que não force o Python a interpretá-lo como parte do código.

Sempre que o Python encontra um comentário no seu programa, o comentário é completamente transparente para ele - do ponto de vista de Python, este é apenas um espaço (independentemente da duração do comentário real).

Em Python, um comentário é um pedaço de texto que começa com um sinal `#` (cardinal, ou hash em inglês) e se estende até ao final da linha.

Se quiser um comentário que abranja várias linhas, tem de colocar um hash à frente de todas elas.

Tal como aqui:
```
# This program evaluates the hypotenuse c.
# a and b are the lengths of the legs.
a = 3.0
b = 4.0
c = (a ** 2 + b ** 2) ** 0.5  # We use ** instead of square root.
print("c =", c)
```

Programadores bons e responsáveis **descrevem cada peça de código importante**, por exemplo, explicando o papel das variáveis; embora deva ser declarado que a melhor maneira de comentar as variáveis é nomeá-las de uma forma inequívoca.

Por exemplo, se uma determinada variável for concebida para armazenar uma área de algum quadrado único, o nome `square_area` será obviamente melhor do que `aunt_jane`.

Dizemos que o primeiro nome é **self-commenting** (autocomenta-se).

Os comentários podem ser úteis noutro aspeto - pode utilizá-los para **marcar um pedaço de código que atualmente não é necessário** por qualquer razão. Veja o exemplo abaixo, se **descomentar** a linha realçada, isto afetará o output do código:
```
# This is a test program.
x = 1
y = 2
# y = y + x
print(x + y)
```

Isto é frequentemente feito durante os testes de um programa, a fim de isolar o local onde um erro possa estar escondido.

SUGESTÃO

Se quiser comentar ou descomentar rapidamente várias linhas de código, selecione a(s) linha(s) que deseja modificar e use o seguinte atalho de teclado: **CTRL + /** (Windows) ou **CMD + /** (Mac OS). É um truque muito útil, não é? Experimente este código na Sandbox.

## 2.5.1.3 RESUMO DA SECÇÃO
## Key takeaways

1. Os comentários podem ser utilizados para deixar informações adicionais em código. São omitidos em runtime. A informação deixada no source code é dirigida aos leitores humanos. Em Python, um comentário é um pedaço de texto que começa com #. O comentário estende-se até ao fim da linha.

2. Se quiser colocar um comentário que abranja várias linhas, precisa de colocar # à frente de todas elas. Além disso, pode utilizar um comentário para marcar um pedaço de código que não é necessário neste momento (ver a última linha do snippet abaixo), por exemplo:

# This program prints
# an introduction to the screen.
print("Hello!")  # Invoking the print() function
# print("I'm Python.")


3. Sempre que possível e justificado, deve dar nomes self-commenting às variáveis, por exemplo, se estiver a utilizar duas variáveis para armazenar um comprimento (em inglês, length) e largura (width) de algo, os nomes das variáveis length e width podem ser uma escolha melhor do que myvar1 e myvar2.

4. É importante utilizar comentários para tornar os programas mais fáceis de compreender, e utilizar nomes de variáveis legíveis e significativos em código. Contudo, é igualmente importante não usar nomes de variáveis que sejam confusos, ou deixar comentários que contenham informações erradas ou incorretas!

5. Os comentários podem ser importantes quando você estiver a ler o seu próprio código após algum tempo (confie em nós, os programadores esquecem-se do que o seu próprio código faz), e quando outros estão a ler o seu código (pode ajudá-los a compreender o que os seus programas fazem e como o fazem mais rapidamente).




Exercício 1

Qual é o output do seguinte snippet?

# print("String #1")
print("String #2")


Verifique
String #2

Exercício 2

O que acontecerá quando executar o seguinte código?

# This is
a multiline
comment. #

print("Hello!")


Verifique
SyntaxError: invalid syntax