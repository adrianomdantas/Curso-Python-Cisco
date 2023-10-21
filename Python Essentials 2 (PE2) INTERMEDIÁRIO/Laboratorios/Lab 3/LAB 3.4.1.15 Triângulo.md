## 3.4.1.15 Triângulo

## Tempo estimado
30-60 minutos

## Nível de dificuldade
Médio

## Objetivos
melhorar as competências do aluno na definição das classes a partir do zero;
utilizar a composição.

## Cenário
Vamos agora incorporar a classe `Point` (ver Lab 3.4.1.14) dentro de outra classe. Além disto, vamos colocar três pontos numa classe, o que nos permitirá definir um triângulo. Como podemos fazer isto?

A nova classe será chamada `Triangle` e esta é a lista das nossas expetativas:

* o construtor aceita três argumentos - todos eles são objetos da classe `Point` ;
* os pontos são armazenados dentro do objeto como uma lista privada;
* a classe fornece um método sem parâmetros chamado perimeter(), que calcula o perímetro do triângulo descrito pelos três pontos; o perímetro é uma soma de todos os comprimentos das pernas (mencionamo-lo para registo, embora estejamos certos de que o conhece perfeitamente.)

Complete o template que fornecemos no editor. Execute o seu código e verifique se o perímetro avaliado é igual ao nosso.

Em baixo pode copiar o código da classe `Point` que usámos no lab anterior:

```
import math


class Point:
    #
    # The code copied from the previous lab.
    #


class Triangle:
    def __init__(self, vertice1, vertice2, vertice3):
        #
        # Write code here
        #

    def perimeter(self):
        #
        # Write code here
        #


triangle = Triangle(Point(0, 0), Point(1, 0), Point(0, 1))
print(triangle.perimeter())

```

Verifique

Output esperado

`3.414213562373095`

