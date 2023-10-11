## 2.4.1.1 Strings em ação

## Comparar strings

As strings de Python **podem ser comparadas utilizando o mesmo conjunto de operadores** que os utilizados em relação aos números.

Dê uma vista de olhos a estes operadores - todos eles também podem comparar strings:

```
* ==
* !=
* >
* >=
* <
* <=
```
Existe um "mas" - os resultados de tais comparações podem por vezes ser um pouco surpreendentes. Não se esqueça que Python não está ciente (não pode de forma alguma) de questões linguísticas subtis - **apenas compara valores de code point, caratere por caratere.**

Os resultados que se obtêm com tal operação são por vezes surpreendentes. Vamos começar com os casos mais simples.

Duas strings são iguais quando consistem nos mesmos carateres, na mesma ordem. Pela mesma forma, duas strings não são iguais quando não consistem nos mesmos carateres, na mesma ordem.

Ambas as comparações dão True como resultado:

```
'alpha' == 'alpha'
'alpha' != 'Alpha'
```

A relação final entre strings é determinada pela comparação do primeiro caratere diferente em ambas as strings (ter sempre em mente os code points ASCII/UNICODE).

Quando se comparam duas strings de comprimentos diferentes, e a mais curta é idêntica à mais longa, **a string mais longa é considerada maior.**

Tal como aqui:

`'alpha' < 'alphabet'`

A relação é `True`.

A comparação de strings é sempre sensível às maiúsculas e minúsculas (letras maiúsculas são tomadas como menores do que as minúsculas).

A expressão é `True`:

`'beta' > 'Beta'`

## 2.4.1.2 Strings em ação

## Comparar strings: continuação

Mesmo que uma string contenha apenas dígitos, ainda assim não é um número. É interpretada como qualquer outra string regular, e o seu (potencial) aspeto numérico não é tomado em consideração de forma alguma.

Veja os exemplos:

```
'10' == '010'
'10' > '010'
'10' > '8'
'20' < '8'
'20' < '80'
```

Eles produzem os seguintes resultados:

output

```
False
True
False
True
True
```

**Comparar strings com números é geralmente uma má ideia.**

As únicas comparações que pode efetuar com impunidade são estas simbolizadas pelos `==` e `!=` . O primeiro dá sempre `False`, enquanto o último produz sempre `True`.

A utilização de qualquer um dos restantes operadores de comparação irá levantar uma TypeError exceção.

Verifiquemos:

```
'10' == 10
'10' != 10
'10' == 1
'10' != 1
'10' > 10
```

Os resultados neste caso são:

output

```
False
True
False
True
TypeError exception
```

Execute todos os exemplos, e realize mais experiências.

## 2.4.1.3 Strings em ação

## Sorting

A comparação está estreitamente relacionada com o sorting (ordenação) (ou melhor, o sorting é de facto um caso muito sofisticado de comparação).

Esta é uma boa oportunidade para lhe mostrar duas formas possíveis de **ordenar listas contendo strings**. Tal operação é muito comum no mundo real - sempre que se vê uma lista de nomes, bens, títulos, ou cidades, espera-se que sejam ordenados.

Vamos supor que quer ordenar a seguinte lista:

` greek = ['omega', 'alpha', 'pi', 'gamma']`

Em geral, o Python oferece duas formas diferentes de ordenar listas.

O primeiro é implementado como **uma função chamada** `sorted()`.

A função toma um argumento (uma lista) e **devolve uma nova lista**, preenchida com os elementos do argumento ordenados. (Nota: esta descrição é um pouco simplificada em comparação com a implementação real - discuti-la-emos mais tarde).

A lista original permanece intacta.

```
# Demonstrating the sorted() function:
first_greek = ['omega', 'alpha', 'pi', 'gamma']
first_greek_2 = sorted(first_greek)

print(first_greek)
print(first_greek_2)
```

Veja o código no editor, e execute-o. O snippet produz o seguinte output:

output

```
['omega', 'alpha', 'pi', 'gamma']
['alpha', 'gamma', 'omega', 'pi']
```

O segundo método afeta a própria lista - **nenhuma nova lista é criada**. A ordenação é realizada in situ pelo método chamado `sort()`.

```
# Demonstrating the sort() method:
second_greek = ['omega', 'alpha', 'pi', 'gamma']
print(second_greek)

second_greek.sort()
print(second_greek)
```

O output não foi alterado:

output

```
['omega', 'alpha', 'pi', 'gamma']
['alpha', 'gamma', 'omega', 'pi']
```

Se precisar de uma ordem que não seja não-decrescente, tem de convencer a função/método a alterar os seus comportamentos padrão. Vamos discutir isso em breve.

## 2.4.1.4 Strings em ação

## Strings vs. números

Há duas questões adicionais que devem ser discutidas aqui: **como converter um número (um número inteiro ou um float) numa string, e vice-versa**. Pode ser necessário realizar tal transformação. Além disso, é uma forma rotineira de processar dados de input/output.

A conversão número-string é simples, pois é sempre possível. É feita por uma função chamada `str()`.

Tal como aqui:

```
itg = 13
flt = 1.3
si = str(itg)
sf = str(flt)

print(si + ' ' + sf)
```

Output do código:

output

`13 1.3`

A transformação inversa (string-número) é possível quando e só quando a string representa um número válido. Se a condição não for cumprida, espere uma ValueError .

Utilize a função `int()` , se quiser obter um número inteiro, e `float()` se precisar de um valor de floating-point.

Tal como aqui:

```
si = '13'
sf = '1.3'
itg = int(si)
flt = float(sf)

print(itg + flt)
```

Isto é o que verá na consola:

output

`14.3`

Na secção seguinte, vamos mostrar-lhe alguns programas simples que processam strings.

## 2.4.1.5 RESUMO DA SECÇÃO

## Key takeaways

1. Strings podem ser comparadas com strings utilizando operadores de comparação geral, mas compará-las com números não dá nenhum resultado razoável, visto **nenhuma string poder ser igual** a qualquer número. Por exemplo:

* `string == number` é sempre `False`;
* `string != number` é sempre `True`;
* `string >= number` **levanta sempre uma exceção**.

2. A ordenação de listas de strings pode ser feita por:

* uma função chamada `sorted()`, criando uma lista nova e ordenada;
* um método chamado `sort()`, que classifica a lista in situ

3. Um número pode ser convertido numa string usando a função `str()` .

4. Uma string pode ser convertida num número (embora não todas as strings) usando ou a função `int()` ou a função `float()` . A conversão falha se uma string não contiver uma imagem numérica válida (uma exceção é então levantada).

**Exercício 1**

Qual das linhas a seguir descreve uma condição **verdadeira**?
```
1 'smith' > 'Smith'
2 'Smiths' < 'Smith'
3 'Smith' > '1000'
4 '11' < '8'
5
```


Verifique
1, 3 e 4

**Exercício 2**

Qual é o output esperado do seguinte código?

```
s1 = 'Where are the snows of yesteryear?'
s2 = s1.split()
s3 = sorted(s2)
print(s3[1])
```

Verifique

`are`


**Exercício 3**

Qual é o resultado esperado do seguinte código?

```
s1 = '12.8'
i = int(s1)
s2 = str(i)
f = float(s2)
print(s1 == s2)
```

Verifique
O código levanta uma exceção `ValueError` .

