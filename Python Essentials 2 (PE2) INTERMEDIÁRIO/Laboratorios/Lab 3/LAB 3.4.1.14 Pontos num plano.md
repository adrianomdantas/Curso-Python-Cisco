## 3.4.1.14 Pontos num plano

## Tempo estimado
30-60 minutos

## Nível de dificuldade
Fácil/Médio

## Objetivos
* melhorar as competências do aluno na definição das classes a partir do zero;
* definir e utilizar variáveis de instância;
* definir e utilizar métodos.

## Cenário
Vamos visitar um lugar muito especial - um plano com o sistema de coordenadas cartesianas (pode saber mais sobre este conceito aqui: https://en.wikipedia.org/wiki/Cartesian_coordinate_system).

Cada ponto localizado no plano pode ser descrito como um par de coordenadas habitualmente chamadas **x** e **y**. Esperamos que seja capaz de escrever uma classe Python que armazena ambas as coordenadas como números float. Além disso, queremos que os objetos desta classe avaliem as distâncias entre qualquer um dos dois pontos situados no plano.

A tarefa é bastante fácil se se empregar a função denominada hypot() (disponível através do módulo math) que avalia o comprimento da hipotenusa de um triângulo retângulo (mais detalhes aqui: https://en.wikipedia.org/wiki/Hypotenuse) e aqui: https://docs.python.org/3.7/library/math.html#trigonometric-functions.

É assim que imaginamos a classe:

* é chamada Point;
* o seu construtor aceita dois argumentos (x e y respetivamente), ambos a zero, por defeito;
* todas as propriedades devem ser privadas;
* a classe contém dois métodos sem parâmetros chamados `getx()` e `gety()`, que devolvem cada uma das duas coordenadas (as coordenadas são armazenadas de forma privada, pelo que não podem ser acedidas diretamente do interior do objeto);
* a classe fornece um método chamado `distance_from_xy(x,y)`, que calcula e devolve a distância entre o ponto armazenado dentro do objeto e o outro ponto dado como um par de floats;
* a classe fornece um método chamado `distance_from_point(point)`, que calcula a distância (como o método anterior), mas a localização do outro ponto é dada como outro Ponto objeto de classe;

Complete o modelo que fornecemos no editor e execute o seu código e verifique se o seu output tem o mesmo aspeto que o nosso.

```
import math


class Point:
    def __init__(self, x=0.0, y=0.0):
        #
        # Write code here
        #

    def getx(self):
        #
        # Write code here
        #

    def gety(self):
        #
        # Write code here
        #

    def distance_from_xy(self, x, y):
        #
        # Write code here
        #

    def distance_from_point(self, point):
        #
        # Write code here
        #


point1 = Point(0, 0)
point2 = Point(1, 1)
print(point1.distance_from_point(point2))
print(point2.distance_from_xy(2, 0))

```

Output esperado

```
1.4142135623730951
1.4142135623730951
```


