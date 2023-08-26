## 4.3.1.8 LAB: Dia do ano: escrever e utilizar as suas próprias funções
## Tempo estimado
20-30 minutos

## Nível de dificuldade
Médio

## Pré-requisitos
LAB 4.3.1.6
LAB 4.3.1.7

## Objetivos
Familiarizar o aluno a:

* projetar e escrever funções parametrizadas;
* utilizar a return declaração;
* construir um conjunto de funções de utilidade;
* utilizar as próprias funções do aluno.

## Cenário

A sua tarefa consiste em escrever e testar uma função que toma três argumentos (um ano, um mês e um dia do mês) e devolve o dia correspondente do ano, ou devolve `None` se algum dos argumentos for inválido.

Use as funções previamente escritas e testadas. Adicione alguns casos de teste ao código. Este teste é apenas um começo.

```
def is_year_leap(year):
#
# Your code from LAB 4.3.1.6.
#

def days_in_month(year, month):
#
# Your code from LAB 4.3.1.7.
#

def day_of_year(year, month, day):
#
# Write your new code here.
#

print(day_of_year(2000, 12, 31))
```