## 3.1.1.12 LAB: Fundamentos da declaração if-elif-else
## Tempo estimado
10-25 minutos

## Nível de dificuldade
Fácil/Médio

## Objetivos
Familiarizar o aluno a:

* a utilização do loop if-elif-else ;
* encontrar a correta implementação de regras definidas verbalmente;
* testar código utilizando input e output de amostra.

## Cenário
Como certamente sabe, devido a algumas razões astronómicas, os anos podem ser bissextos ou comuns. Os primeiros têm 366 dias de duração, enquanto os segundos têm 365 dias de duração.

Desde a introdução do calendário gregoriano (em 1582), a seguinte regra é utilizada para determinar o tipo de ano:

* se o número do ano não for divisível por quatro, é um ano comum;
* caso contrário, se o número do ano não for divisível por 100, é um ano bissexto;
* caso contrário, se o número do ano não for divisível por 400, é um ano comum;
* caso contrário, é um ano bissexto.

Veja o código no editor - lê apenas um número de ano, e precisa de ser completado com as instruções de implementação do teste que acabámos de descrever.
```
year = int(input("Enter a year: "))

#
# Write your code here.
#
```

O código deve fazer output de uma de duas mensagens possíveis, que são `Leap year` ou `Common year`, dependendo do valor inserido.

Seria bom verificar se o ano introduzido cai na era Gregoriana, e faz output de um aviso caso contrário: `Not within the Gregorian calendar period`. Dica: use os operadores `!=` e `%` .

Teste o seu código utilizando os dados por nós fornecidos.

## Dados de teste
Input de amostra: `2000`

Output esperado: `Leap year`
<hr>

Input de amostra: `2015`

Output esperado: `Common year`
<hr>

Input de amostra: `1999`

Output esperado: `Common year`
<hr>

Input de amostra: `1996`

Output esperado: `Leap year`
<hr>

Input de amostra: `1580`

Output esperado: `Not within the Gregorian calendar period`