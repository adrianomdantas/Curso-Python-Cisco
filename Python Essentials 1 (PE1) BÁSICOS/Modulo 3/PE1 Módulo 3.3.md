## 3.3.1.1 Operações de lógica e bit em Python | and, or, not

## Lógica de computador

Já reparou que as condições que utilizámos até agora têm sido muito simples, para não dizer bastante primitivas? As condições que utilizamos na vida real são muito mais complexas. Vejamos esta frase:

Se tivermos algum tempo livre, e o tempo estiver bom, vamos dar um passeio.


Utilizámos a conjunção `and`, o que significa que ir dar um passeio depende do cumprimento simultâneo destas duas condições. Na linguagem da lógica, tal ligação de condições é chamada uma `conjunção`. E agora outro exemplo:

Se estiveres no centro comercial ou eu estiver no centro comercial, um de nós vai comprar um presente para a mãe.

A aparência da palavra `or` significa que a compra depende de pelo menos uma destas condições. Em lógica, tal composto é chamado uma **disjunção**.

É evidente que o Python deve ter operadores para construir conjunções e disjunções. Sem eles, o poder expressivo da linguagem ficaria substancialmente enfraquecido. Eles são chamados **operadores lógicos**.

## and

Um operador de conjunção lógica em Python é a palavra and. É um **operador binário com uma prioridade que é inferior à expressa pelos operadores de comparação**. Permite-nos codificar condições complexas sem o uso de parêntesis como esta:

`counter > 0 and value == 100`

O resultado fornecido pelo operador `and` pode ser determinado com base na `tabela da verdade`.

Se considerarmos a conjunção de `A e B`, o conjunto de valores possíveis de argumentos e valores correspondentes da conjunção parece ser o seguinte:


|Argumento A	|Argumento B	|A e B|
|---|---|---|
|False	|False	|False|
|False	|True	|False|
|True	|False	|False|
|True	|True	|True|

## or

Um operador de disjunção é a palavra `or`. É um **operador binário com uma prioridade inferior a** `and` ( assim como `+` comparado com `*`). A sua tabela de verdade é a seguinte:


|Argumento A	|Argumento B	|A ou B|
|---|---|---|
|False	|False	|False|
|False	|True	|True|
|True	|False	|True|
|True	|True	|True|

## not

Além disso, há outro operador que pode ser aplicado para construir condições. É um **operador unário que executa uma negação lógica**. O seu funcionamento é simples: transforma a verdade em falsidade e a falsidade em verdade.

Este operador é escrito como a palavra `not`, e a sua **prioridade é muito alta: a mesma que o unário** `+` **e** `-`. A sua tabela de verdade é simples:


|Argumento	|not Argumento|
|---|---|
|False	|True|
|True	|False|

## 3.3.1.2 Operações de lógica e bit em Python | and, or, not

## Expressões lógicas
Vamos criar uma variável chamada var e atribuir 1 a ela. As seguintes condições são equivalentes em pares:
```
# Example 1:
print(var > 0)
print(not (var <= 0))


# Example 2:
print(var != 0)
print(not (var == 0))
```

Pode estar familiarizado com as leis de De Morgan. Dizem que:

A negação de uma conjunção é a disjunção das negações.

A negação de uma disjunção é a conjunção das negações.


Vamos escrever a mesma coisa usando Python:
```
not (p and q) == (not p) or (not q)
not (p or q) == (not p) and (not q)
```

Note-se como os parêntesis foram utilizados para codificar as expressões - colocámo-los lá para melhorar a legibilidade.

Devemos acrescentar que nenhum destes operadores de dois argumentos pode ser utilizado sob a forma abreviada conhecida como op=. Vale a pena recordar esta exceção.

## Valores lógicos vs. bits únicos

Os operadores lógicos tomam os seus argumentos como um todo, independentemente da quantidade de bits que contenham. Os operadores só estão conscientes do valor: zero (quando todos os bits são redefinidos) significa `False`; não zero (quando pelo menos um bit está definido) significa `True`.

O resultado das suas operações é um destes valores: `False` ou `True`. Isto significa que este snippet irá atribuir o valor `True` à variável `j` se `i` não for zero; caso contrário, será `False`.
```
i = 1
j = not not i
```

## Operadores bitwise

No entanto, existem quatro operadores que lhe permitem **manipular bits únicos de dados**. São chamados **operadores bitwise**.

Abrangem todas as operações que mencionámos anteriormente no contexto lógico, e um operador adicional. Este é o operador `xor` (como em **exclusivo ou**), e é denotado como `^` (acento circunflexo).

Aqui estão todos eles:

* `&` (e comercial) - conjunção bitwise;
* `|` (barra) - disjunção bitwise;
* `~` (til) - negação bitwise;
* `^` (acento circunflexo) - bitwise exclusive ou (xor).

## Operações bitwise (`&`, `|`, e `^`)

| Argumento A	| Argumento B	| A & B	 | `A | B`	| A ^ B| 
|---|---|---|---|---| 
|0	|0	|0	|0	|0|
|0	|1	|0	|1	|1|
|1	|0	|0	|1	|1|
|1	|1	|1	|1	|0|

## Operações bitwise (~)
|Argumento	|~ Argumento|
|---|---|
|0	|1|
|1	|0|

Vamos facilitar as coisas:

* `&` requer exatamente dois `1` para fornecer `1` como resultado;
* `|` requer pelo menos um `1` para fornecer `1` como resultado;
* `^` requer exatamente um `1` para fornecer `1` como resultado.

<hr>

Acrescentemos uma observação importante: os argumentos destes operadores **devem ser inteiros**; não devemos utilizar floats aqui.

A diferença no funcionamento dos operadores lógicos e de bit é importante: **os operadores lógicos não penetram no nível de bits do seu argumento**. Eles só estão interessados no valor inteiro final.

Os operadores bitwise são mais rigorosos: lidam com **cada bit separadamente**. Se assumirmos que a variável inteira ocupa 64 bits (o que é comum nos sistemas informáticos modernos), podemos imaginar a operação bitwise como uma avaliação de 64 vezes do operador lógico para cada par de bits dos argumentos. Esta analogia é obviamente imperfeita, pois no mundo real todas estas 64 operações são realizadas ao mesmo tempo (simultaneamente).

## 3.3.1.3 Operações de lógica e bit em Python
