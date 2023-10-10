## 2.3.1.1 Métodos de String

## Os loops capitalize() .

Vamos passar por alguns métodos padrão de string Python. Vamos atravessá-los por ordem alfabética - para ser honesto, qualquer ordem tem tantas desvantagens como vantagens, pelo que a escolha pode também ser aleatória.

O método `capitalize()` faz exatamente o que diz - **cria uma nova string cheia de carateres retirados da source string**, mas tenta modificá-los da seguinte forma:

* **se o primeiro caratere dentro da string for uma letra** (nota: o primeiro caratere é um elemento com um index igual a 0, não apenas o primeiro caratere visível), **será convertido para maiúsculas**;
* **todas as letras restantes da string serão convertidas em minúsculas.**

Não se esqueça:

* a string original (da qual o método é invocado) não é alterada de forma alguma (a imutabilidade de uma string deve ser obedecida sem reservas)
* a string modificada (capitalizada neste caso) é devolvida como resultado - se não a utilizar de qualquer forma (atribuí-la a uma variável, ou passá-la a uma função/método) ela desaparecerá sem deixar rasto.

Nota: os métodos não têm de ser invocados apenas de dentro das variáveis. Podem ser invocados diretamente de dentro de literais de string. Vamos utilizar regularmente essa convenção - simplificará os exemplos, uma vez que os aspetos mais importantes não desaparecerão entre as tarefas desnecessárias.

Veja o exemplo no editor. Execute-o.

```
# Demonstrating the capitalize() method:
print('aBcD'.capitalize())
```

Isto é o que ele imprime:

output

`Abcd`


Experimente alguns exemplos mais avançados e teste o seu output:

```
print("Alpha".capitalize())
print('ALPHA'.capitalize())
print(' Alpha'.capitalize())
print('123'.capitalize())
print("αβγδ".capitalize())
```

## 2.3.1.2 Métodos de String

## Os loops center() .

A variante de um parâmetro do método `center()` faz uma cópia da string original, tentando centralizá-la dentro de um campo de uma largura especificada.

A centralização é realmente feita **adicionando alguns espaços antes e depois da string.**

Não espere que este método demonstre quaisquer competências sofisticadas. É bastante simples.

O exemplo no editor usa parêntesis retos para mostrar claramente onde começa e termina a string centrada.

O seu output é o seguinte:

`[  alpha   ]`

Se o comprimento do campo alvo for demasiado pequeno para caber na string, a string original é devolvida.

Pode ver o método `center()` em mais exemplos aqui:

```
print('[' + 'Beta'.center(2) + ']')
print('[' + 'Beta'.center(4) + ']')
print('[' + 'Beta'.center(6) + ']')
```

Execute os snippets acima e verifique qual o output que eles produzem.

**A variante de dois parâmetros de** `center()` **faz uso do caratere do segundo argumento, em vez de um espaço.** Analise o exemplo abaixo:

`print('[' + 'gamma'.center(20, '*') + ']')`


É por isso que o output agora se assemelha a este:

`[*******gamma********]`

Realize mais experiências.

## 2.3.1.3 Métodos de String

## Os loops endswith() .

A classe `endswith()` **verifica se a string dada termina com o argumento especificado e devolve** `True` **ou** `False`, dependendo do resultado da verificação.

Nota: a substring deve aderir ao último caratere da string - não pode estar localizada apenas algures perto do final da string.

Veja o nosso exemplo no editor, analise-o, e execute-o. O seu output é:

`yes`

Deverá agora ser capaz de prever o output do snippet abaixo:

```
t = "zeta"
print(t.endswith("a"))
print(t.endswith("A"))
print(t.endswith("et"))
print(t.endswith("eta"))
```

Execute o código para verificar as suas previsões.

```
# Demonstrating the endswith() method:
if "epsilon".endswith("on"):
    print("yes")
else:
    print("no")
```

output

`yes`

## 2.3.1.4 Métodos de String

## Os loops find() .

A classe `find()` é semelhante a `index()`, que já conhece - **procura uma substring e devolve o index de primeira ocorrência desta substring**, mas:

* é mais seguro - **não gera um erro para um argumento que contém uma substring inexistente** (devolve -1 então)
* **funciona apenas com strings** - não tente aplicá-lo a qualquer outra sequência.

Veja o código no editor. É assim que pode utilizá-lo.

```
# Demonstrating the find() method:
print("Eta".find("ta"))
print("Eta".find("mma"))
```

O exemplo imprime:


output

```
1
-1
```

Nota: não use `find()` se quiser apenas verificar se um único caratere ocorre dentro de uma string - o operador `in` será significativamente mais rápido.

Aqui está outro exemplo:

```
t = 'theta'
print(t.find('eta'))
print(t.find('et'))
print(t.find('the'))
print(t.find('ha'))
```

Consegue prever o output? Execute-o e verifique as suas previsões.

Se quiser realizar a procura, não desde o início da string, mas **a partir de qualquer posição**, pode usar uma **variante de dois parâmetros** do `find()` método. Veja o exemplo:

`print('kappa'.find('a', 2))`

O segundo argumento **especifica o index em que a pesquisa será iniciada** (não tem de caber dentro da string).

Entre as duas letras a, apenas a segunda será encontrada. Execute o snippet e verifique.

Pode utilizar o método `find()` para procurar todas as ocorrências da substring, como aqui:

```
the_text = """A variation of the ordinary lorem ipsum
text has been used in typesetting since the 1960s 
or earlier, when it was popularized by advertisements 
for Letraset transfer sheets. It was introduced to 
the Information Age in the mid-1980s by the Aldus Corporation, 
which employed it in graphics and word-processing templates
for its desktop publishing program PageMaker (from Wikipedia)"""

fnd = the_text.find('the')
while fnd != -1:
    print(fnd)
    fnd = the_text.find('the', fnd + 1)
```

O código imprime os índices de todas as ocorrências do artigo the, e o seu output é semelhante a este:

output

```
15
80
198
221
238
```

Há também uma **mutação de três parâmetros do método** `find()` - o terceiro argumento **aponta para o primeiro index que não será tomado em consideração durante a pesquisa** (na realidade é o limite superior da pesquisa).

Veja o nosso exemplo abaixo:

```
print('kappa'.find('a', 1, 4))
print('kappa'.find('a', 2, 4))
```

O segundo argumento especifica o index em que a pesquisa será iniciada (não tem de caber dentro da string).

```
# Demonstrating the find() method:
print("Eta".find("ta"))
print("Eta".find("mma"))
```

Portanto, o exemplo modificado tem como output:

output

```
1
-1
```

(*a* não pode ser encontrado dentro dos limites de pesquisa indicados no segundo `print()`).

## 2.3.1.5 Métodos de String

## Os loops isalnum() .

O método sem parâmetros chamado `isalnum()` **verifica se a string contém apenas dígitos ou carateres alfabéticos (letras) e devolve** `True` **ou** `False` de acordo com o resultado.

Veja o exemplo no editor e execute-o.

```
# Demonstrating the isalnum() method:
print('lambda30'.isalnum())
print('lambda'.isalnum())
print('30'.isalnum())
print('@'.isalnum())
print('lambda_30'.isalnum())
print(''.isalnum())
```

Nota: qualquer elemento de string que não seja um dígito ou uma letra faz com que o método devolva `False`. Uma string vazia também o faz.

O output do exemplo é:

output

```
True
True
True
False
False
False
```
Três exemplos mais intrigantes estão aqui:

```
t = 'Six lambdas'
print(t.isalnum())

t = 'ΑβΓδ'
print(t.isalnum())

t = '20E1'
print(t.isalnum())
```

Execute-os e verifique o seu output.

```
False
True
True
```

Dica: a causa do primeiro resultado é um espaço - não é nem um dígito nem uma letra.

## 2.3.1.6 Métodos de String

## Os loops isalpha() .

A classe `isalpha()` é mais especializado - está interessado **apenas em letras**.

```# Example 1: Demonstrating the isapha() method:
print("Moooo".isalpha())
print('Mu40'.isalpha())
```

Veja o Exemplo 1 - o seu output é:

output
```
True
False
```

## O método isdigit() .

Por sua vez, o método `isdigit()` olha **apenas para os dígitos** - qualquer outra coisa produz `False` como o resultado.

```
# Example 2: Demonstrating the isdigit() method:
print('2018'.isdigit())
print("Year2019".isdigit())
```

Veja o Exemplo 2 - o seu output é:

output

```
True
False
```

Realize mais experiências.

## 2.3.1.7 Métodos de String

## Os loops islower() .

A classe `islower()` é uma variante picuinhas do `isalpha()` - aceita **apenas letras minúsculas**.

Veja o Exemplo 1 no editor - o seu output é:

```# Example 1: Demonstrating the islower() method:
print("Moooo".islower())
print('moooo'.islower())
```

output
```
False
True
```


## O método isspace() .

A classe `isspace()` **identifica apenas os espaços em branco** - ignora qualquer outro caratere (o resultado é `False` então).

Veja o Exemplo 2 no editor - o seu output é:

```# Example 2: Demonstrating the isspace() method:
print(' \n '.isspace())
print(" ".isspace())
print("mooo mooo mooo".isspace())
```

output

```
True
True
False
```


## O método isupper() .

A classe `isupper()` é a versão maiúscula do `islower()` - concentra-se **apenas em letras maiúsculas**.

Novamente, veja o Exemplo 3 no editor - o seu output é:

```# Example 3: Demonstrating the isupper() method:
print("Moooo".isupper())
print('moooo'.isupper())
print('MOOOO'.isupper())
```

output

```
False
False
True
```

## 2.3.1.8 Métodos de String

## Os loops join() .

A classe `join()` é bastante complicado, por isso deixe-nos guiá-lo passo a passo:

* como o seu nome sugere, o método **realiza uma junção** (em inglês, join) - espera um argumento como uma lista; deve ter a certeza de que todos os elementos da lista são strings - o método irá levantar uma exceção TypeError de outra forma;
* todos os elementos da lista serão **unidos numa string**, mas...
* ... a string a partir da qual o método foi invocado é **usada como um separador**, colocado entre as strings;
* a string recém-criada é devolvida como um resultado.

Dê uma vista de olhos no exemplo no editor. Vamos analisá-lo:

```# Demonstrating the join() method:
print(",".join(["omicron", "pi", "rho"]))
```

* o método `join()` é invocado de dentro de uma string contendo uma vírgula (a string pode ser arbitrariamente longa, ou pode estar vazia)
* o argumento `join` é uma lista contendo três strings;
* o método devolve uma nova string.

Aqui está:

output

`omicron,pi,rh`

## 2.3.1.9 Métodos de String

## Os loops lower() .

A classe `lower()` **faz uma cópia de uma source string, substitui todas as letras maiúsculas por minúsculas**, e devolve a string como resultado. Novamente, a source string permanece intocada.

Se a string não contiver carateres maiúsculos, o método devolve a string original.

```# Demonstrating the lower() method:
print("SiGmA=60".lower())
```

Nota: O método `lower()` não toma nenhum parâmetro.

```# Demonstrating the lower() method:
print("SiGmA=60".lower())
```

O exemplo no editor tem como output:

output

`sigma=60`


Como de costume, realize as suas próprias experiências.

## 2.3.1.10 Métodos de String

## Os loops lstrip () .

O parâmetro sem `lstrip()` método **devolve uma cadeia recém-criada formada a partir da original, removendo todos os principais espaços em branco.**

Analise o código de exemplo no editor.

Os parêntesis não fazem parte do resultado - apenas mostram os limites do resultado.

```
# Demonstrating the lstrip() method:
print("[" + " tau ".lstrip() + "]")
```

O output do exemplo:

output

`[tau ]`

O **parâmetro único** `lstrip()` faz o mesmo que a sua versão sem parâmetros, mas **remove todos os caracteres alistados no seu argumento** (uma cadeia), e não apenas espaços em branco:

`print("www.cisco.com".lstrip("w."))`

Não são necessários parêntesis aqui, pois o output é o seguinte:

output

`cisco.com`

Consegue adivinhar a saída do trecho abaixo? Pense bem. Execute o código e verifique as suas previsões.

`print("pythoninstitute.org".lstrip(".org"))`

Surpreendido? Carateres **principais** , espaços em branco principais. Mais uma vez, experimente com os seus próprios exemplos.

## 2.3.1.11 Métodos de String

