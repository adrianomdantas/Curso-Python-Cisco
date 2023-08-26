## 4.3.1.10 LAB: Conversão do consumo de combustível

## Tempo estimado
10-15 minutos

## Nível de dificuldade
Fácil

## Objetivos
* melhorar as competências do aluno na definição, utilização e teste de funções.

## Cenário

O consumo de combustível de um carro pode ser expresso de várias maneiras. Por exemplo, na Europa, é mostrado como a quantidade de combustível consumido por 100 quilómetros.

Nos EUA, é mostrado como o número de milhas percorridas por um carro utilizando um galão de combustível.

A sua tarefa é escrever um par de funções convertendo l/100 km em mpg, e vice-versa.

As funções:

* são nomeadas `liters_100km_to_miles_gallon` e `miles_gallon_to_liters_100km` respetivamente;
* tome um argumento (o valor correspondente aos seus nomes)

Complete o código no editor.
```
def liters_100km_to_miles_gallon(liters):
#
# Write your code here.
#

def miles_gallon_to_liters_100km(miles):
#
# Write your code here
#

print(liters_100km_to_miles_gallon(3.9))
print(liters_100km_to_miles_gallon(7.5))
print(liters_100km_to_miles_gallon(10.))
print(miles_gallon_to_liters_100km(60.3))
print(miles_gallon_to_liters_100km(31.4))
print(miles_gallon_to_liters_100km(23.5))
```

Execute o seu código e verifique se o seu output é o mesmo que o nosso.

Aqui estão algumas informações para o ajudar:

* 1 milha americana = 1609,344 metros;
* 1 galão americano = 3,785411784 litros.

Output esperado

```
60.31143162393162
31.36194444444444
23.52145833333333
3.9007393587617467
7.490910297239916
10.009131205673757
```