## 3.1.1.11 LAB: Fundamentos da declaração if-else
## Tempo estimado
10-20 minutos

## Nível de dificuldade
Fácil/Médio

## Objetivos
Familiarizar o aluno a:

* utilizar a instrução if-else para ramificar o caminho de controlo;
* construir um programa completo que resolva problemas simples da vida real.

## Cenário
Era uma vez uma terra - uma terra de leite e mel, habitada por pessoas felizes e prósperas. As pessoas pagavam impostos, claro - a sua felicidade tinha limites. O imposto mais importante, denominado Imposto sobre o Rendimento das Pessoas Singulares (IRS ou, em inglês, PIT), tinha de ser pago uma vez por ano, e foi avaliado utilizando a seguinte regra:

* se o rendimento do cidadão não fosse superior a 85.528 thalers, o imposto era igual a 18% do rendimento menos 556 thalers e 2 cêntimos (este era o chamado desagravamento fiscal (em inglês, tax relief))
* se o rendimento fosse superior a este montante, o imposto seria igual a 14.839 thalers e 2 cêntimos, mais 32% do excedente acima de 85.528 thalers.

A sua tarefa é escrever uma **calculadora de impostos**.

* Deve aceitar um valor de floating-point: o rendimento.
* A seguir, deve imprimir o imposto calculado, arredondado a thalers completos. Há uma função chamada `round()` que lhe fará o arredondamento por si - encontrá-la-á no código esqueleto no editor.
Nota: este país feliz nunca devolve dinheiro aos seus cidadãos. Se o imposto calculado for inferior a zero, significa apenas que não há qualquer imposto (o imposto é igual a zero). Tenha isto em consideração durante os seus cálculos.

Veja o código no editor - lê apenas um valor de input e faz output de um resultado, pelo que necessita de o completar com alguns cálculos inteligentes.

```
income = float(input("Enter the annual income: "))

#
# Write your code here.
#

tax = round(tax, 0)
print("The tax is:", tax, "thalers")
```

Teste o seu código utilizando os dados por nós fornecidos.

## Dados de teste

Input de amostra: `10000`

Output esperado: `The tax is: 1244.0 thalers`
<hr>

Input de amostra: `100000`

Output esperado: The tax is: `19470.0 thalers`
<hr>

Input de amostra: `1000`

Output esperado: `The tax is: 0.0 thalers`

Input de amostra: -100

Output esperado: The tax is: 0.0 thalers
