## 4.3.1.6 LAB: Um ano bissexto: escrever as suas próprias funções

## Tempo estimado
10-15 minutos

## Nível de dificuldade
Fácil

## Objetivos
Familiarizar o aluno a:

* projetar e escrever funções parametrizadas;
* utilizar a return declaração;
* testar as funções.

## Cenário

A sua tarefa é escrever e testar uma função que leva um argumento (um ano) e devolve True se o ano for um ano bissexto, ou False caso contrário.

A seed da função já está semeada no código esqueleto no editor.
```
def is_year_leap(year):
#
# put your code here
#

test_data = [1900, 2000, 2016, 1987]
test_results = [False, True, True, False]
for i in range(len(test_data)):
	yr = test_data[i]
	print(yr,"->",end="")
	result = is_year_leap(yr)
	if result == test_results[i]:
		print("OK")
	else:
		print("Failed")
```

Nota: preparámos também um pequeno código de teste, que pode utilizar para testar a sua função.

O código utiliza duas listas - uma com os dados do teste, e a outra com os resultados esperados. O código dirá se algum dos seus resultados é inválido.