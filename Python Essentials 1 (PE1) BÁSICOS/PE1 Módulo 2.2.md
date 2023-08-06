# Python Essentials 1:
# Módulo 2.2

## Literais - os dados em si

Agora que tem um pouco de conhecimento de algumas das poderosas características oferecidas pela função ```print()``` , é hora de aprender sobre algumas novas questões, e um novo termo importante - o **literal**.

**Um literal são dados cujos valores são determinados pelo próprio literal.**

Como este é um conceito difícil de compreender, um bom exemplo pode ser útil.

Dê uma vista de olhos ao seguinte conjunto de dígitos:

`123`

Consegue adivinhar que valor representa? Claro que consegue - é cento e vinte e três.

Mas e quanto a isto:

`c`

Representa algum valor? Talvez. Pode ser o símbolo da velocidade da luz, por exemplo. Também pode ser a constante de integração. Ou mesmo o comprimento de uma hipotenusa no sentido de um teorema de Pitágoras. Existem muitas possibilidades.


Não se pode escolher o certo sem algum conhecimento adicional.

E esta é a pista: `123` é um literal, e `c` não é.

Utiliza literais **para codificar dados e para os colocar no seu código**. Vamos agora mostrar-lhe algumas convenções a que tem de obedecer quando utiliza o Python.

Comecemos com uma simples experiência - veja o snippet no editor.

A primeira linha parece familiar. A segunda parece estar errada devido à visível falta de aspas.

Tente executá-lo.

![Literais 1](Imagens/Literais1.jpg)

Se tudo correu bem, deverá agora ver duas linhas idênticas.

O que aconteceu? O que significa isto?

Através deste exemplo, depara-se com dois tipos diferentes de literais:

* uma **string**, que já conhece,
* e um número **inteiro**, algo completamente novo.

A função `print()` apresenta-os exatamente da mesma forma - este exemplo é óbvio, uma vez que a sua representação legível em termos humanos é também a mesma. Internamente, na memória do computador, estes dois valores são armazenados de formas completamente diferentes - a string existe apenas como uma string - uma série de letras.

O número é convertido em representação mecânica (um conjunto de bits). A função `print()` é capaz de mostrar ambos de uma forma legível para os seres humanos.

Vamos agora gastar algum tempo a discutir os literais numéricos e a sua vida interna.

## Inteiros

Pode já saber um pouco sobre como os computadores efetuam cálculos sobre números. Talvez já tenha ouvido falar do **sistema binário**, e saiba que é o sistema que os computadores utilizam para armazenar números, e que eles podem realizar qualquer operação sobre eles.

Não vamos explorar aqui as complexidades dos sistemas de numeração posicional, mas vamos dizer que os números tratados pelos computadores modernos são de dois tipos:

* **inteiros**, isto é, aqueles que são desprovidos da parte fraccionada;
* e números **floating-point** (ou simplesmente **float**), que contêm (ou são capazes de conter) a parte 
fraccionada.

Esta definição não é inteiramente exata, mas suficiente por agora. A distinção é muito importante, e a fronteira entre estes dois tipos de números é muito rigorosa. Ambos os tipos de números diferem significativamente na forma como são armazenados na memória de um computador e no intervalo de valores aceitáveis.

A característica do valor numérico que determina o seu tipo, intervalo, e aplicação, é chamada **type**.

Se codificar um literal e o colocar dentro do código Python, a forma do literal determina a representação (type) que o Python utilizará para **o armazenar na memória**.

Por agora, vamos deixar de lado os números floating-point (voltaremos a eles em breve) e considerar a questão de como o Python reconhece os inteiros.


O processo é quase como escrevê-los com um lápis no papel - é simplesmente uma string de dígitos que compõem o número. Mas há uma reserva - não deve interpor quaisquer carateres que não sejam dígitos dentro do número.

Tomemos, por exemplo, o número onze milhões cento e onze mil cento e onze. Se pegasse agora mesmo num lápis, escreveria o número desta forma: `11,111,111,` ou assim: `11.111.111,` ou mesmo assim: `11 111 111`.

É evidente que esta disposição facilita a leitura, especialmente quando o número é composto por muitos dígitos. No entanto, o Python não aceita coisas como estas. É proibido. O que o Python permite, no entanto, é a utilização de **underscores** em literais numéricos.*

Por conseguinte, pode escrever este número desta forma: `11111111`, ou assim: `11_111_111`.

NOTA *Python 3.6 introduziu underscores em letras numéricas, permitindo a colocação de underscores únicos entre dígitos e após especificadores de base para melhorar a legibilidade. Este recurso não está disponível em versões mais antigas de Python.


E como codificamos números negativos em Python? Como de costume - adicionando um menos. Pode escrever: `-11111111`, ou `-11_111_111`.

Os números positivos não precisam de ser precedidos pelo sinal de mais, mas é permitido, se o desejar fazer. As linhas a seguir descrevem o mesmo número: `+11111111` e `11111111`.

## Inteiros: números octais e hexadecimais

Há duas convenções adicionais em Python que são desconhecidas no mundo da matemática. A primeira permite-nos utilizar números numa representação octal.

Se um número inteiro for precedido por um `0O` ou `0o` prefixo (zero-o), ele será tratado como um valor octal. Isto significa que o número deve conter apenas dígitos retirados do intervalo [0..7].

`0o123` é um número **octal** com um valor (decimal) igual a 83.

A classe `print()` faz a conversão automaticamente. Experimente isto:

`print(0o123)`

![octal](Imagens/Octal.jpg)

A segunda convenção permite-nos utilizar números hexadecimais. Estes números devem ser precedidos pelo prefixo `0x` ou `0X` (zero-x).

`0x123` é um número **hexadecimal** com um valor (decimal) igual a `291`. A função `print()` também pode gerir estes valores. Experimente isto:

`print(0x123)`

![hexadecimal](Imagens/Hexadecimal.jpg)

## Floats

Agora é hora de falar de outro tipo, que foi concebido para representar e armazenar os números que (como diria um matemático) têm uma **fração decimal não vazia**.

São os números que têm (ou podem ter) uma parte fracionada após o ponto decimal, e embora tal definição seja muito pobre, é certamente suficiente para o que desejamos discutir.

Sempre que utilizamos um termo como dois e meio ou menos zero ponto quatro, pensamos em números que o computador considera números de **floating-point**:

```
2.5
-0.4
```

Nota: dois e meio parece normal quando se escreve num programa, embora se a sua língua materna preferir usar uma vírgula em vez de um ponto no número, deve assegurar-se de que o seu **número não contém quaisquer vírgulas**.

O Python não aceitará isso, ou (em casos muito raros mas possíveis) pode interpretar mal as suas intenções, uma vez que a própria vírgula tem o seu significado reservado em Python.

Se quiser usar apenas um valor de dois e meio, deve escrevê-lo como mostrado acima. Nota mais uma vez - há um ponto entre 2 e 5 - não uma vírgula.

Como provavelmente pode imaginar, o valor de zero ponto quatro pode ser escrito em Python como:

`0.4`

Mas não se esqueça desta regra simples - pode omitir o zero quando é o único dígito em frente ou após o ponto decimal.

Em essência, pode escrever o valor `0.4` como:

```
.4
```

Por exemplo: o valor de `4.0` pode ser escrito como:

```
4.
```
Isto não mudará nem o seu tipo nem o seu valor.

## Ints vs. floats

O ponto decimal é essencialmente importante no reconhecimento de números de floating-point em Python.

Veja estes dois números:

```
4
4.0
```

Pode pensar que eles são exatamente os mesmos, mas o Python vê-os de uma forma completamente diferente.

`4` é um número **inteiro**, enquanto que `4.0` é um número **floating-point**.

O ponto é o que faz um float.

Por outro lado, não são apenas os pontos que fazem um float. Também pode utilizar a letra `e`.

Quando quiser usar números muito grandes ou muito pequenos, pode usar **notação científica**.

Tome, por exemplo, a velocidade da luz, expressa em metros por segundo. Escrito diretamente, ficaria assim: `300000000`.

Para evitar escrever tantos zeros, os livros de física utilizam uma forma abreviada, que provavelmente já viu: 3 x 10<sup>8</sup>.

Lê-se: três vezes dez à potência de oito.

Em Python, o mesmo efeito é conseguido de uma forma ligeiramente diferente - veja:

`3E8`

A letra `E` (também pode utilizar a letra minúscula `e` - vem da palavra **expoente**) é um registo conciso da frase vezes dez à potência de.

Nota:

o **expoente** (o valor após o E) deve ser um número inteiro;
a **base** (o valor à frente do E) pode ser um inteiro.



