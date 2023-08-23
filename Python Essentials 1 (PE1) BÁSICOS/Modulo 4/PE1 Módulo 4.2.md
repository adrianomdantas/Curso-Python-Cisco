## 4.2.1.1 Como as funções comunicam com o seu ambiente

## Funções parametrizadas

Todo o potencial da função é revelado quando esta pode ser equipada com uma interface capaz de aceitar dados fornecidos pelo invocador. Tais dados podem modificar o comportamento da função, tornando-a mais flexível e adaptável às condições em mudança.

Um parâmetro é na verdade uma variável, mas há dois fatores importantes que tornam os parâmetros diferentes e especiais:

* **os parâmetros existem apenas dentro das funções em que foram definidos**, e o único lugar onde o parâmetro pode ser definido é um espaço entre um par de parêntesis na declaração `def` ;
* **atribuir um valor ao parâmetro é feito no momento da invocação da função**, especificando o argumento correspondente.

```
def function(parameter):
    ###
```

Não se esqueça:

* **os parâmetros vivem dentro de funções** (este é o seu ambiente natural)
* **os argumentos existem fora de funções**, e são portadores de valores passados para parâmetros correspondentes.

Existe uma fronteira clara e inequívoca entre estes dois mundos.

Vamos enriquecer a função acima com apenas um parâmetro - vamos usá-lo para mostrar ao utilizador o número de um valor que a função pede.

Temos de reconstruir a declaração `def` - é assim que se parece agora:
```
def message(number):
    ###
```

A definição especifica que a nossa função opera apenas num parâmetro chamado `number`. Pode utilizá-lo como uma variável comum, mas **apenas dentro da função** - ele não é visível em qualquer outro lugar.

Vamos agora melhorar o corpo da função:
```
def message(number):
    print("Enter a number:", number)
```

Fizemos uso do parâmetro. Nota: não atribuímos o parâmetro com qualquer valor. Está correto?

Sim, está.

Um valor para o parâmetro chegará a partir do ambiente da função.

Lembre-se: **especificar um ou mais parâmetros na definição de uma função** também é um requisito, e tem de o cumprir durante a invocação. Deve **fornecer tantos argumentos quantos os parâmetros definidos.**

Não o fazer causará um erro.

## 4.2.1.2 Como as funções comunicam com o seu ambiente

## Funções parametrizadas: continuação

Tente executar o código no editor.

```
def message(number):
    print("Enter a number:", number)

message()
```
Isto é o que verá no console:

`TypeError: message() missing 1 required positional argument: 'number'`


Isto parece melhor, com certeza:
```
def message(number):
    print("Enter a number:", number)

message(1)
```

Além disso, comporta-se melhor. O código irá produzir o seguinte output:

`Enter a number: 1`


Vê como funciona? O valor do argumento utilizado durante a invocação (`1`) foi passado para a função, definindo o valor inicial do parâmetro chamado `number`.
<hr>

Temos de o tornar sensível a uma circunstância importante.

É válido, e possível, ter uma **variável com o mesmo nome que o parâmetro de uma função**.

O snippet ilustra o fenômeno:
```
def message(number):
    print("Enter a number:", number)

number = 1234
message(1)
print(number)
```

Uma situação como esta ativa um mecanismo chamado **sombreamento**:

* parâmetro `x` sombreia qualquer variável do mesmo nome, mas...
* ... apenas dentro da função que define o parâmetro.

O parâmetro chamado `number` é uma entidade completamente diferente da variável chamada `number`.

Isto significa que o snippet acima irá produzir o seguinte output:
```
Enter a number: 1
1234
```

## 4.2.1.3 Como as funções comunicam com o seu ambiente

## Funções parametrizadas: continuação

Uma função pode ter **tantos parâmetros quantos quiser**, mas quanto mais parâmetros tiver, mais difícil é memorizar os seus papéis e propósitos.

Vamos modificar a função - tem **dois parâmetros** agora:
```
def message(what, number):
    print("Enter", what, "number", number)
```

Isto também significa que invocar a função irá requerer **dois argumentos**.

O primeiro parâmetro novo destina-se a levar o nome do valor desejado.

Aqui está:
```
def message(what, number):
    print("Enter", what, "number", number)

message("telephone", 11)
message("price", 5)
message("number", "number")
```

Esta é o output que está prestes a ver:
```
Enter telephone number 11
Enter price number 5
Enter number number number
```

Execute o código, modifique-o, adicione mais parâmetros e veja como isso afeta o output.

## 4.2.1.4 Como as funções comunicam com o seu ambiente

## Passagem de parâmetros posicionais

Uma técnica que atribui o i<sup>ésimo</sup> (primeiro, segundo, e assim por diante) argumento ao i<sup>ésimo</sup> (primeiro, segundo, e assim por diante) parâmetro de função é chamada **passagem de parâmetro posicional**, enquanto os argumentos passados desta forma são denominados **argumentos posicionais**.

Já o usou, mas o Python pode oferecer muito mais. Vamos agora falar-lhe sobre isso.
```
def my_function(a, b, c):
    print(a, b, c)

my_function(1, 2, 3)
```

Nota: a passagem de parâmetros posicionais é intuitivamente utilizada pelas pessoas em muitas ocasiões sociais. Por exemplo, pode ser geralmente aceite que quando nos apresentamos mencionemos o(s) nosso(s) nome(s) próprio(s) antes do nosso apelido, por exemplo, "O meu nome é Miguel Matos".

A propósito, os húngaros fazem-no pela ordem inversa.
<hr>

Vamos implementar esse costume social em Python. A seguinte função será responsável pela introdução de alguém:
```
def introduction(first_name, last_name):
    print("Hello, my name is", first_name, last_name)

introduction("Luke", "Skywalker")
introduction("Jesse", "Quick")
introduction("Clark", "Kent")
```

Consegue adivinhar o output? Execute o código e descubra se estava certo.

```
Hello, my name is Luke Skywalker
Hello, my name is Jesse Quick
Hello, my name is Clark Kent
```

Agora imagine que a mesma função está a ser utilizada na Hungria. Nesse caso, o código ficaria assim:
def introduction(first_name, last_name):
    print("Hello, my name is", first_name, last_name)

introduction("Skywalker", "Luke")
introduction("Quick", "Jesse")
introduction("Kent", "Clark")


O output terá um aspeto diferente. Consegue adivinhá-lo?

Execute o código para ver se também estava certo aqui. Está surpreendido?

Pode tornar a função mais independente da cultura?

## 4.2.1.5 Como as funções comunicam com o seu ambiente

## Passagem de argumentos de keyword

O Python oferece outra convenção para passar argumentos, onde **o significado do argumento é ditado pelo seu nome**, não pela sua posição - chama-se **keyword argument passing**.

Veja o snippet:
```
def introduction(first_name, last_name):
    print("Hello, my name is", first_name, last_name)

introduction(first_name = "James", last_name = "Bond")
introduction(last_name = "Skywalker", first_name = "Luke")
```

O conceito é claro - os valores passados para os parâmetros são precedidos pelos nomes dos parâmetros alvo, seguidos do sinal `=` .

A posição não importa aqui - o valor de cada argumento conhece o seu destino com base no nome utilizado.

Deverá ser capaz de prever o output. Execute o código para verificar se estava certo.
<hr>

É claro que **não se deve usar um nome de parâmetro inexistente**.

O snippet seguinte causará um erro de runtime:
```
def introduction(first_name, last_name):
    print("Hello, my name is", first_name, last_name)

introduction(surname="Skywalker", first_name="Luke")
```

Isto é o que Python lhe dirá:

`TypeError: introduction() got an unexpected keyword argument 'surname'`


Experimente você mesmo.

## 4.2.1.6 Como as funções comunicam com o seu ambiente

## Mistura de argumentos posicionais e de keywords

Pode misturar ambos os tipos se quiser - há apenas uma regra inquebrável: tem de colocar **argumentos posicionais antes de argumentos de keyword**.

Se pensar por um momento, certamente adivinhará porquê.

Para lhe mostrar como funciona, utilizaremos a seguinte função simples de três parâmetros:
```
def adding(a, b, c):
    print(a, "+", b, "+", c, "=", a + b + c)
```

O seu objetivo é avaliar e apresentar a soma de todos os seus argumentos.

A função, quando invocada da seguinte maneira:

`adding(1, 2, 3)`

terá como output:

`1 + 2 + 3 = 6`


Foi - como se pode suspeitar - um puro exemplo de **passagem de argumento posicional**.
<hr>

É claro que se pode substituir tal invocação por uma variante de keyword pura, como esta:

`adding(c = 1, a = 2, b = 3)`

O nosso programa fará output de uma linha como esta:

```2 + 3 + 1 = 6```


Observe a ordem dos valores.
<hr>

Vamos tentar misturar ambos os estilos agora.

Veja a invocação da função abaixo:

`adding(3, c = 1, b = 2)`

Vamos analisá-la:

* o argumento (3) para o parâmetro a é passado usando a maneira posicional;
* os argumentos para c e b são especificados como keywords.

Isto é o que verá no console:

`3 + 2 + 1 = 6`
<hr>

Tenha cuidado, e atenção aos erros. Se tentar passar mais do que um valor para um argumento, tudo o que obterá será um erro de runtime.

Olhe para a invocação em baixo - parece que tentamos fixar `a` duas vezes:

`adding(3, a = 1, b = 2)`

A resposta do Python:

`TypeError: adding() got multiple values for argument 'a'`


Olhe para o snippet abaixo. Um código como este está totalmente correto, mas não faz muito sentido:

`adding(4, 3, c = 2)`


Tudo está correto, mas deixar apenas uma keyword parece um pouco estranho - o que acha?

## 4.2.1.7 Como as funções comunicam com o seu ambiente

## Funções parametrizadas - mais detalhes

Acontece por vezes que os valores de um determinado parâmetro são utilizados com mais frequência do que outros. Tais argumentos podem ter os seus **valores padrão (predefinidos)** tomados em consideração quando os seus argumentos correspondentes tiverem sido omitidos.

Dizem que o apelido inglês mais popular é Smith. Vamos tentar ter isto em conta.

O valor padrão do parâmetro é definido usando uma sintaxe clara e pictórica:
```
def introduction(first_name, last_name="Smith"):
    print("Hello, my name is", first_name, last_name)
```

Só tem de estender o nome do parâmetro com o sinal `=` , seguido pelo valor padrão.

Vamos invocar a função como de costume:

`introduction("James", "Doe")`

Consegue adivinhar o output do programa? Execute-o e verifique se estava certo.

Então? Tudo parece igual, mas quando se invoca a função de uma forma que à primeira vista parece um pouco suspeita, como esta:

`introduction("Henry")`

ou esta:

`introduction(first_name="William")`

não haverá nenhum erro, ambas as invocações serão bem sucedidas, e o console mostrará o seguinte output:
```
Hello, my name is Henry Smith
Hello, my name is William Smith
```

Teste-o.
<hr>

Pode ir mais além se for útil. Ambos os parâmetros têm agora os seus valores padrão, veja o código em baixo:
```
def introduction(first_name="John", last_name="Smith"):
    print("Hello, my name is", first_name, last_name)
```

Isto faz com que a seguinte invocação seja absolutamente válida:

`introduction()`

E este é o output esperado:

`Hello, my name is John Smith`
<hr>

Se utilizar um argumento de keyword, o restante tomará o valor padrão:

`introduction(last_name="Hopkins")`

O output é:

`Hello, my name is John Hopkins`

Teste-o.

Parabéns - acabou de aprender as formas básicas de comunicar com funções.

## 4.2.1.8 RESUMO DA SEÇÃO

## Key takeaways

1. É possível passar informações para funções utilizando parâmetros. As suas funções podem ter todos os parâmetros que precisar.

Um exemplo de uma função de um parâmetro:
```
def hi(name):
    print("Hi,", name)

hi("Greg")
```

Um exemplo de uma função de dois parâmetros:
```
def hi_all(name_1, name_2):
    print("Hi,", name_2)
    print("Hi,", name_1)

hi_all("Sebastian", "Konrad")
```

Um exemplo de uma função de três parâmetros:
```
def address(street, city, postal_code):
    print("Your address is:", street, "St.,", city, postal_code)

s = input("Street: ")
p_c = input("Postal Code: ")
c = input("City: ")

address(s, c, p_c)
```

2. Pode passar argumentos a uma função utilizando as seguintes técnicas:

* **passagem de argumento posicional** onde a ordem de passagem dos argumentos importa (Ex. 1),
* **passagem de argumento de keyword (nomeada)** onde a ordem dos argumentos passados não importa (Ex. 2),
* uma mistura de passagem de argumentos posicionais e de keyword (Ex. 3).

```
Ex. 1
def subtra(a, b):
    print(a - b)

subtra(5, 2)    # outputs: 3
subtra(2, 5)    # outputs: -3


Ex. 2
def subtra(a, b):
    print(a - b)

subtra(a=5, b=2)    # outputs: 3
subtra(b=2, a=5)    # outputs: 3

Ex. 3
def subtra(a, b):
    print(a - b)

subtra(5, b=2)    # outputs: 3
subtra(5, 2)    # outputs: 3
```

É importante lembrar que **os argumentos posicionais não devem seguir os argumentos de keyword**. É por isso que se tentar executar o seguinte snippet:
```
def subtra(a, b):
    print(a - b)

subtra(5, b=2)    # outputs: 3
subtra(a=5, 2)    # Syntax Error
```

O Python não o deixará fazê-lo através da sinalização de um `SyntaxError`.

3. Pode usar a técnica de passagem de argumentos de keyword para **pré-definir** um valor para um determinado argumento:
```
def name(first_name, last_name="Smith"):
    print(first_name, last_name)

name("Andy")    # outputs: Andy Smith
name("Betty", "Johnson")    # outputs: Betty Johnson (the keyword argument replaced by "Johnson")
```
<hr>


**Exercício 1**

Qual é o output do seguinte snippet?
```
def intro(a="James Bond", b="Bond"):
    print("My name is", b + ".", a + ".")

intro()
```

Verifique
`My name is Bond. James Bond.`

**Exercício 2**

Qual é o output do seguinte snippet?
```
def intro(a="James Bond", b="Bond"):
    print("My name is", b + ".", a + ".")

intro(b="Sean Connery")
```

Verifique
`My name is Sean Connery. James Bond.`

**Exercício 3**

Qual é o output do seguinte snippet?
```
def intro(a, b="Bond"):
    print("My name is", b + ".", a + ".")

intro("Susan")
```

Verifique
`My name is Bond. Susan.`

**Exercício 4**

Qual é o output do seguinte snippet?
```
def add_numbers(a, b=2, c):
    print(a + b + c)

add_numbers(a=1, c=3)
```

Verifique
`SyntaxError` - um argumento não padrão (`c`) segue um argumento padrão (`b=2`)


