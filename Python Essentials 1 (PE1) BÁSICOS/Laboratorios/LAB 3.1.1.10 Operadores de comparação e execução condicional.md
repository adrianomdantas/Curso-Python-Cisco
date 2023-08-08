## 3.1.1.10 LAB: Operadores de comparação e execução condicional

## Tempo estimado
5-15 minutos

## Nível de dificuldade
Fácil

## Objetivos
* familiarizar-se com a função input() ;
* familiarizar-se com operadores de comparação em Python;
* familiarizar-se com o conceito de execução condicional.

## Cenário
O [Spathiphyllum](https://upload.wikimedia.org/wikipedia/commons/b/bd/Spathiphyllum_cochlearispathum_RTBG.jpg), mais vulgarmente conhecido como o lírio de paz ou a planta de vela branca, é uma das mais populares plantas de interior, capaz de filtrar toxinas nocivas do ar. Algumas das toxinas que neutraliza incluem o benzeno, o formaldeído e o amoníaco.

Imagine que o seu programa de computador adora estas plantas. Sempre que recebe um input na forma da palavra `Spathiphyllum`, involuntariamente grita para a consola a seguinte string: `"Spathiphyllum is the best plant ever!"`

Escreve um programa que utilize o conceito de execução condicional, toma uma string como entrada, e:

* imprime a frase `"Yes - Spathiphyllum is the best plant ever!"` para o ecrã, se a cadeia de caracteres inseridos é `"Spathiphyllum"` (upper-case)
* Impressões `"No, I want a big Spathiphyllum!"` se a cadeia de caracteres inseridos é `"spathiphyllum"` (lower-case)
* Impressões `"Spathiphyllum! Not [input]!"` caso contrário. Nota: `[input]` é a string tomada como input.

Teste o seu código utilizando os dados que lhe fornecemos. E arranje também um Spathiphyllum!


Dados de Teste
Input de amostra: `spathiphyllum`

Output esperado: `No, I want a big Spathiphyllum!`
<hr>

Input de amostra: `pelargonium`

Output esperado: `Spathiphyllum! Not pelargonium!`
<hr>

Input de amostra: `Spathiphyllum`

Output esperado: `Yes - Spathiphyllum is the best plant ever!`