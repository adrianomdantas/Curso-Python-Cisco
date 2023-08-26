## 4.3.1.9 LAB: Números primos - como encontrá-los

## Tempo estimado
15-20 minutos

## Nível de dificuldade
Médio

## Objetivos
* familiarizar o aluno com noções e algoritmos clássicos;
* melhorar as habilidades do aluno na definição e utilização de funções.

## Cenário

_Um número natural é ***primo*** se for maior que 1 e não tiver divisores além de 1 e dele próprio._

Complicado? De modo algum. Por exemplo, 8 não é um número primo, uma vez que se pode dividi-lo por 2 e 4 (não podemos utilizar divisores iguais a 1 e 8, uma vez que a definição o proíbe).

Por outro lado, 7 é um número primo, uma vez que não conseguimos encontrar quaisquer divisores legais para ele.


A sua tarefa é escrever uma função para verificar se um número é primo ou não.

A função:

* é chamada `is_prime`;
* toma um argumento (o valor a verificar)
* devolve `True` se o argumento for um número primo, e `False` caso contrário.

Dica: tente dividir o argumento por todos os valores subsequentes (começando por 2) e verifique os restos - se for zero, o seu número não pode ser um primo; pense cuidadosamente sobre quando deve parar o processo.

Se precisar de conhecer a raiz quadrada de qualquer valor, pode utilizar o operador `**` . Lembre-se: a raiz quadrada de x é o mesmo que x<sup>0.5</sup>

Complete o código no editor.

Execute o seu código e verifique se o seu output é o mesmo que o nosso.

## Output esperado

`2 3 5 7 11 13 17 19`

```
def is_prime(num):
#
# Write your code here.
#

for i in range(1, 20):
	if is_prime(i + 1):
			print(i + 1, end=" ")
print()
```