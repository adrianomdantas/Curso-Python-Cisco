## 3.5.1.1 Fundamentos da OOP: Herança

## Herança - porquê e como?
Antes de começarmos a falar sobre heranças, queremos apresentar um novo e prático mecanismo utilizado pelas classes e objetos Python - **a forma como o objeto é capaz de se introduzir a si próprio.**

Vamos começar com um exemplo. Veja o código no editor.

```
class Star:
    def __init__(self, name, galaxy):
        self.name = name
        self.galaxy = galaxy


sun = Star("Sun", "Milky Way")
print(sun)
```

O programa imprime apenas uma linha de texto, que no nosso caso é a seguinte:

output

`<__main__.Star object at 0x7f1074cc7c50>`


Se executar o mesmo código no seu computador, verá algo muito semelhante, embora o número hexadecimal (a substring a começar por 0x) será diferente, uma vez que é apenas um identificador de objeto interno utilizado pelo Python, e é improvável que pareça o mesmo quando o mesmo código é executado num ambiente diferente.

Como pode ver, a impressão aqui não é realmente útil, e algo mais específico, ou apenas mais bonito, pode ser mais preferível.

Felizmente, o Python oferece precisamente tal função.

## 3.5.1.2 Fundamentos da OOP: Herança

## Herança - porquê e como?

Quando o Python precisa que qualquer classe/objeto seja apresentado como uma string (colocar um objeto como argumento na invocação de função `print()` encaixa-se nesta condição) ele tenta invocar um método chamado `__str__()` do objeto e usar a string que ele devolve.

O método por defeito `__str__()` devolve a string anterior - feia e não muito informativa. Pode alterá-lo apenas **definindo o seu próprio método do nome.**

Acabamos de fazer isso - veja o código no editor.

```
class Star:
    def __init__(self, name, galaxy):
        self.name = name
        self.galaxy = galaxy

    def __str__(self):
        return self.name + ' in ' + self.galaxy


sun = Star("Sun", "Milky Way")
print(sun)
```

Este novo método `__str__()` faz uma string consistindo nos nomes da estrela e da galáxia - nada de especial, mas os resultados da impressão parecem melhores agora, certo?

Consegue adivinhar o output? Execute o código para verificar se estava certo.

output

`Sun in Milky Way`

## 3.5.1.3 Fundamentos da OOP: Herança

## Herança - porquê e como?

O termo herança (inheritance) é mais antigo do que a programação de computadores, e descreve a prática comum de passar vários bens de uma pessoa para outra após a morte da primeira. O termo, quando relacionado à programação de computadores, tem um significado completamente diferente.


![O conceito de herança 2](../Imagens/conceitoHeranca2.jpg)


Vamos definir o termo para os nossos propósitos:

A herança é uma prática comum (na programação de objetos) de **passar atributos e métodos da superclasse (definida e existente) para uma classe recém-criada, chamada subclasse**.

Por outras palavras, a herança é **uma forma de construir uma nova classe, não a partir do zero, mas usando um repertório de traços já definidos**. A nova classe herda (e esta é a chave) todo o equipamento já existente, mas é capaz de adicionar alguns novos se necessário.

Graças a isso, é possível **construir classes mais especializadas (mais concretas)** usando alguns conjuntos de regras e comportamentos gerais predefinidos.

O fator mais importante do processo é a relação entre a superclasse e todas as suas subclasses (nota: se *B* é uma subclasse de *A* e *C* é uma subclasse de *B*, isto também significa que *C* é uma subclasse de *A*, uma vez que a relação é totalmente transitória).

Um exemplo muito simples de herança de **dois níveis** é apresentado aqui:

```
class Vehicle:
    pass


class LandVehicle(Vehicle):
    pass


class TrackedVehicle(LandVehicle):
    pass
```

Todas as classes apresentadas estão vazias por agora, pois vamos mostrar-lhe como funcionam as relações mútuas entre as super e as subclasses. Em breve iremos preenchê-las com conteúdos.

Podemos dizer que:

* A classe `Vehicle` é a superclasse para ambas as classes `LandVehicle` e `TrackedVehicle` ;
* A classe `LandVehicle` é uma subclasse de `Vehicle` e uma superclasse de `TrackedVehicle` ao mesmo tempo;
* A classe `TrackedVehicle` é uma subclasse de ambas as classes `Vehicle` e `LandVehicle` .

O conhecimento acima vem da leitura do código (por outras palavras, nós conhecemo-lo porque o podemos ver).

O Python sabe o mesmo? É possível perguntar ao Python sobre isso? Sim, é.

## 3.5.1.4 Fundamentos da OOP: Herança

## Herança: issubclass()

O Python oferece uma função que é capaz de **identificar uma relação entre duas classes**, e embora o seu diagnóstico não seja complexo, pode **verificar se uma determinada classe é uma subclasse de qualquer outra classe.**

É este o seu aspecto:

`issubclass(ClassOne, ClassTwo)`

A função devolve True Se `ClassOne` for uma subclasse de `ClassTwo`, e False caso contrário.

Vamos vê-lo em ação - pode surpreendê-lo. Veja o código no editor. Leia-o com atenção.

Existem dois loops nested. O seu objetivo é **verificar todos os pares de classes ordenados possíveis, e imprimir os resultados da verificação para determinar se o par corresponde à relação subclasse-superclasse.**

```
class Vehicle:
    pass


class LandVehicle(Vehicle):
    pass


class TrackedVehicle(LandVehicle):
    pass


for cls1 in [Vehicle, LandVehicle, TrackedVehicle]:
    for cls2 in [Vehicle, LandVehicle, TrackedVehicle]:
        print(issubclass(cls1, cls2), end="\t")
    print()
```

Execute o código. O programa produz o seguinte output:

output

```
True	False	False	
True	True	False	
True	True	True	
```

Vamos tornar o resultado mais legível:

|**↓ é uma subclasse de →**	|**Vehicle**	|**LandVehicle**	|**TrackedVehicle**|
|---|---|---|---|
|**Vehicle**	|`True`	|`False`	|`False`|
|**LandVehicle**	|`True`	|`True`	|`False`|
|**TrackedVehicle**	|`True`	|`True`	|`True`|

Há uma observação importante a fazer: **cada classe é considerada como uma subclasse de si mesma.**


## 3.5.1.5 Fundamentos da OOP: Herança

## Herança: isinstance()

Como já sabe, **um objeto é uma incarnação de uma classe**. Isto significa que o objeto é como um bolo cozido utilizando uma receita que está incluída dentro da classe.

Isto pode gerar alguns problemas importantes.

Vamos supor que tem um bolo (por exemplo, como um argumento passado para a sua função). Você quer saber qual a receita utilizada para o fazer. Porquê? Porque quer saber o que esperar dele, por exemplo, se contém nozes ou não, o que é uma informação crucial para algumas pessoas.

Da mesma forma, pode ser crucial se o objeto tiver (ou não tiver) certas características. Por outras palavras, **se é um objeto de uma determinada classe ou não.**

Tal fato pode ser detetado pela função chamada `isinstance()`:

`isinstance(objectName, ClassName)`

As funções devolvem True se o objeto for uma instância da classe, ou False caso contrário.

**Ser uma instância de uma classe significa que o objeto (o bolo) foi preparado utilizando uma receita contida quer na classe quer numa das suas superclasses.**

Não se esqueça: se uma subclasse contém pelo menos o mesmo equipamento que qualquer uma das suas superclasses, significa que os objetos da subclasse podem fazer o mesmo que os objetos derivados da superclasse, portanto, é uma instância da sua home class e de qualquer uma das suas superclasses.

Vamos testá-lo. Analise o código no editor.

Criamos três objetos, um para cada uma das classes. Em seguida, utilizando dois loops nested, verificamos todos os pares possíveis da classe de objeto **para descobrir se os objetos são instâncias das classes.**

Execute o código.

```
class Vehicle:
    pass


class LandVehicle(Vehicle):
    pass


class TrackedVehicle(LandVehicle):
    pass


my_vehicle = Vehicle()
my_land_vehicle = LandVehicle()
my_tracked_vehicle = TrackedVehicle()

for obj in [my_vehicle, my_land_vehicle, my_tracked_vehicle]:
    for cls in [Vehicle, LandVehicle, TrackedVehicle]:
        print(isinstance(obj, cls), end="\t")
    print()
```

Isto é o que obtemos:

output

```
True	False	False	
True	True	False	
True	True	True	
```

Vamos novamente tornar o resultado mais legível:

|**↓ é uma instância de →**	|**Vehicle**	|**LandVehicle**	|**TrackedVehicle**|
|**my_vehicle**	|True	|False	|False|
|**my_land_vehicle**	|True	|True	|False|
|**my_tracked_vehicle**	|True	|True	|True|

Será que a tabela confirma as nossas expetativas?

## 3.5.1.6 Fundamentos da OOP: Herança

## Herança: o operador is .

Há também um operador Python que vale a pena mencionar, pois refere-se diretamente a objetos - aqui está ele:

`object_one is object_two`

**O operador** `is` **verifica se duas variáveis (**`object_one` **e** `object_two` **aqui) se referem ao mesmo objeto.**

Não se esqueça que **as variáveis não armazenam os objetos em si, mas apenas os manípulos que apontam para a memória interna do Python.**

Atribuir um valor de uma variável de objeto a outra variável não copia o objeto, mas apenas o seu manípulo. É por isso que um operador como `is` pode ser muito útil em circunstâncias particulares.

Observe ao código no editor. Vamos analisá-lo:

```
class SampleClass:
    def __init__(self, val):
        self.val = val


object_1 = SampleClass(0)
object_2 = SampleClass(2)
object_3 = object_1
object_3.val += 1

print(object_1 is object_2)
print(object_2 is object_3)
print(object_3 is object_1)
print(object_1.val, object_2.val, object_3.val)

string_1 = "Mary had a little "
string_2 = "Mary had a little lamb"
string_1 += "lamb"

print(string_1 == string_2, string_1 is string_2)
```

* existe uma classe muito simples equipada com um construtor simples, criando apenas uma propriedade. A classe é utilizada para instanciar dois objetos. O primeiro é então atribuído a outra variável, e a sua propriedade `val` é incrementada por um.
* depois, o operador `is` é aplicado três vezes para verificar todos os pares de objetos possíveis, e todos os valores de propriedade `val` também são impressos.
* a última parte do código realiza outra experiência. Após três atribuições, ambas as cadeias contêm os mesmos textos, mas **estes textos são armazenados em objetos diferentes.**

O código imprime:

output

```
False
False
True
1 2 1
True False
```

Os resultados demonstram que `object_1` e `object_3` são na verdade os mesmos objetos, enquanto `string_1` e `string_2` não são, apesar de seu conteúdo ser o mesmo.

## 3.5.1.7 Fundamentos da OOP: Herança

## De que forma o Python encontra propriedades e métodos

Vamos agora ver como o Python lidar com métodos de herança.

Observe o exemplo no editor. Vamos analisá-lo:

```
class Super:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return "My name is " + self.name + "."


class Sub(Super):
    def __init__(self, name):
        Super.__init__(self, name)


obj = Sub("Andy")

print(obj)
```

* há uma classe chamada Super, que define o seu próprio construtor, usado para atribuir a propriedade do objeto, chamada name.
* a classe também define o método __str__() , o que torna a classe capaz de apresentar a sua identidade na forma de um texto claro.
* a classe é então utilizada como base para criar uma subclasse chamada Sub. A classe Sub define o seu próprio construtor, que invoca o da superclasse. Observe como o fizemos: Super.__init__(self, name).
* nomeamos explicitamente a superclasse, e apontámos para o método para invocar __init__(), fornecendo todos os argumentos necessários.
* instanciámos um objeto de classe Sub e imprimimo-lo.

Output do código:

output

`My name is Andy.`

Nota: Como não há um método `__str__()` dentro da classe `Sub` , a string impressa deve ser produzida dentro da classe `Super` . Isto significa que o método `__str__()` foi herdado pela classe `Sub` .

## 3.5.1.8 Fundamentos da OOP: Herança

## Como o Python encontra propriedades e métodos: continuação

Veja o código no editor. Modificámo-lo para lhe mostrar outro método de acesso a qualquer entidade definida dentro da superclasse.

```
class Super:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return "My name is " + self.name + "."


class Sub(Super):
    def __init__(self, name):
        super().__init__(name)


obj = Sub("Andy")

print(obj)
```

No último exemplo, nomeamos explicitamente a superclasse. Neste exemplo, fazemos uso da função `super()` , que **acede à superclasse sem a necessidade de saber o seu nome:**

`super().__init__(name)`

A função `super()` cria um contexto em que não é necessário (além disso, não se deve) passar o argumento self ao método invocado - é por isso que é possível ativar o construtor da superclasse usando apenas um argumento.

Nota: pode utilizar este mecanismo não só **para invocar o construtor da superclasse, mas também para ter acesso a qualquer um dos recursos disponíveis dentro da superclasse.**

## 3.5.1.9 Fundamentos da OOP: Herança

## Como o Python encontra propriedades e métodos: continuação

Vamos tentar fazer algo semelhante, mas com propriedades (mais precisamente: com **variáveis de classe**).

Observe o exemplo no editor.

```
# Testing properties: class variables.
class Super:
    supVar = 1


class Sub(Super):
    subVar = 2


obj = Sub()

print(obj.subVar)
print(obj.supVar)
```

Como pode ver, a classe `Super` define uma variável de classe chamada `supVar`, e a classe `Sub` define uma variável chamada `subVar`.

Ambas as variáveis são visíveis dentro do objeto da classe `Sub` - é por isso que o código faz o output:

output

```
2
1
```

## 3.5.1.10 Fundamentos da OOP: Herança

## Como o Python encontra propriedades e métodos: continuação

O mesmo efeito pode ser observado com **variáveis de instância** - veja o segundo exemplo no editor.

```
# Testing properties: instance variables.
class Super:
    def __init__(self):
        self.supVar = 11


class Sub(Super):
    def __init__(self):
        super().__init__()
        self.subVar = 12


obj = Sub()

print(obj.subVar)
print(obj.supVar)
```

O construtor de classe `Sub` cria uma variável de instância chamada `subVar`, enquanto o construtor `Super` faz o mesmo com uma variável chamada `supVar`. Como anteriormente, ambas as variáveis são acessíveis de dentro do objeto da classe `Sub`.

```
# Testing properties: instance variables.
class Super:
    def __init__(self):
        self.supVar = 11


class Sub(Super):
    def __init__(self):
        super().__init__()
        self.subVar = 12


obj = Sub()

print(obj.subVar)
print(obj.supVar)
```

O output do programa é:

output

```
12
11
```

Nota: a existência da variável `supVar` é obviamente condicionada pela invocação do construtor de classe `Super` . Omiti-la resultaria na ausência da variável no objeto criado (experimente-o você mesmo).

## 3.5.1.11 Fundamentos da OOP: Herança

## Como o Python encontra propriedades e métodos: continuação

Agora é possível formular uma declaração geral descrevendo o comportamento do Python.

Quando se tenta aceder à entidade de qualquer objeto, o Python tentará (por esta ordem):

* encontrá-lo **dentro do próprio objeto**;
* encontrá-lo **em todas as classes** envolvidas na linha de herança do objeto, de baixo para cima;

Se ambos os itens acima falharem, uma **exceção (`AttributeError`) é levantada**.

A primeira condição pode precisar de alguma atenção adicional. Como sabe, todos os objetos derivados de uma determinada classe podem ter diferentes conjuntos de atributos, e alguns dos atributos podem ser acrescentados ao objeto muito tempo após a sua criação.

O exemplo no editor resume isto numa **linha de herança de três níveis**. Analise-o cuidadosamente.

```
class Level1:
    variable_1 = 100
    def __init__(self):
        self.var_1 = 101

    def fun_1(self):
        return 102


class Level2(Level1):
    variable_2 = 200
    def __init__(self):
        super().__init__()
        self.var_2 = 201
    
    def fun_2(self):
        return 202


class Level3(Level2):
    variable_3 = 300
    def __init__(self):
        super().__init__()
        self.var_3 = 301

    def fun_3(self):
        return 302


obj = Level3()

print(obj.variable_1, obj.var_1, obj.fun_1())
print(obj.variable_2, obj.var_2, obj.fun_2())
print(obj.variable_3, obj.var_3, obj.fun_3())

```

Todos os comentários que fizemos até agora estão relacionados com **herança única**, quando uma subclasse tem exatamente uma superclasse. Esta é a situação mais comum (e a mais recomendada também).

O Python, no entanto, oferece muito mais aqui. Nas próximas lições, vamos mostrar-lhe alguns exemplos de **herança múltipla**.

## 3.5.1.12 Fundamentos da OOP: Herança

## Como o Python encontra propriedades e métodos: continuação

**A herança múltipla ocorre quando uma classe tem mais de uma superclasse**. Sintaticamente, tal herança é apresentada como uma lista separada por vírgulas de superclasses colocadas dentro de parêntesis, após o novo nome da classe - tal como aqui:

```
class SuperA:
    var_a = 10
    def fun_a(self):
        return 11


class SuperB:
    var_b = 20
    def fun_b(self):
        return 21


class Sub(SuperA, SuperB):
    pass

obj = Sub()

print(obj.var_a, obj.fun_a())
print(obj.var_b, obj.fun_b())
```

A classe `Sub` tem duas superclasses: `SuperA` e `SuperB`. Isto significa que a classe `Sub` **herda todos os bens oferecidos por ambos `SuperA` e `SuperB`**.

O código imprime:

output

```
10 11
20 21
```

Agora é tempo de introduzir um termo completamente novo - **overriding**.

O que pensa que acontecerá se mais do que uma das superclasses definir uma entidade com um determinado nome?

## 3.5.1.13 Fundamentos da OOP: Herança

## Como o Python encontra propriedades e métodos: continuação

Vamos analisar o exemplo no editor.

```
class Level1:
    var = 100
    def fun(self):
        return 101


class Level2(Level1):
    var = 200
    def fun(self):
        return 201


class Level3(Level2):
    pass


obj = Level3()

print(obj.var, obj.fun())
```

Ambas as classes `Level1` e `Level2` definem um método chamado `fun()` e uma propriedade chamada `var`. Isto significa que o objecto de classe `Level3` poderá ter acesso a duas cópias de cada entidade? De modo algum.

**A entidade definida mais tarde (no sentido da herança) sobrepõe-se à mesma entidade definida mais cedo**. É por isso que o código produz o seguinte output:

output

`200 201`

Como pode ver, o argumento de keyword `var` e método `fun()` a partir da classe `Level2` substituem as entidades com os mesmos nomes derivados da classe `Level1` .

Esta característica pode ser intencionalmente utilizada para modificar comportamentos padrão (ou previamente definidos) de classe quando qualquer uma das suas classes precisa de agir de uma forma diferente da dos seus antepassados.

Podemos também dizer que **o Python procura uma entidade de baixo para cima**, e está plenamente satisfeito com a primeira entidade do nome desejado.

Como funciona quando uma classe tem dois antepassados que oferecem a mesma entidade, e eles estão no mesmo nível? Por outras palavras, o que se deve esperar quando uma classe emerge usando herança múltipla? Vamos ver isto.

## 3.5.1.14 Fundamentos da OOP: Herança

## Como o Python encontra propriedades e métodos: continuação

Vejamos o exemplo no editor.

```
class Left:
    var = "L"
    var_left = "LL"
    def fun(self):
        return "Left"


class Right:
    var = "R"
    var_right = "RR"
    def fun(self):
        return "Right"


class Sub(Left, Right):
    pass


obj = Sub()

print(obj.var, obj.var_left, obj.var_right, obj.fun())
```

A classe `Sub` herda bens de duas superclasses, `Left` e `Right` (estes nomes destinam-se a ser significativos).

Não há dúvida de que a variável de classe `var_right` vem da classe `Right` , e `var_left` vem de Left respetivamente.

Isto é evidente. Mas de onde `var` vem? É possível adivinhá-lo? O mesmo problema é encontrado com o método `fun()` - será invocado a partir de `Left` ou a partir de `Right`? Vamos executar o programa - o seu output é:

output

`L LL RR Left`

Isto prova que ambos os casos pouco claros têm uma solução dentro da `Left` classe. Será esta uma premissa suficiente para formular uma regra geral? Sim, é.

Podemos dizer que **o Python procura componentes de objeto** na seguinte ordem:

* **dentro do próprio objeto;**
* **nas suas superclasses**, de baixo para cima;
* se houver mais do que uma classe num determinado caminho de herança, o Python analisa-os da esquerda para a direita.

Precisa de mais alguma coisa? Basta fazer uma pequena emenda no código - substituir: `class Sub(Left, Right)`: por: `class Sub(Right, Left)`:, em seguida, execute o programa novamente e veja o que acontece.

O que vê agora? Nós vemos:

output

`R LL RR Right`


Vê o mesmo, ou algo diferente?

## 3.5.1.15 Fundamentos da OOP: Herança

## Como construir uma hierarquia de classes

A construção de uma hierarquia de classes não é apenas arte por causa da arte.

Se dividir um problema entre classes e decidir qual delas deve ser localizada no topo e qual deve ser colocada na base da hierarquia, tem de analisar cuidadosamente a questão, mas antes de lhe mostrarmos como o fazer (e como não o fazer), queremos destacar um efeito interessante. Não é nada de extraordinário (é apenas uma consequência das regras gerais apresentadas anteriormente), mas lembrá-la pode ser fundamental para compreender como funcionam alguns códigos, e como o efeito pode ser utilizado para construir um conjunto flexível de classes.

Observe o código no editor. Vamos analisá-lo:

```
class One:
    def do_it(self):
        print("do_it from One")

    def doanything(self):
        self.do_it()


class Two(One):
    def do_it(self):
        print("do_it from Two")


one = One()
two = Two()

one.doanything()
two.doanything()
```

* existem duas classes, nomeadas `One` e `Two`, enquanto `Two` é derivada de `One`. Nada de especial. No entanto, uma coisa parece notável - o método `do_it()` .
* o método `do_it()` é **definido duas vezes**: originalmente dentro `One` e subsequentemente dentro `Two`. A essência do exemplo reside no facto de ser **invocado apenas uma** vez - no interior `One`.

A questão é - qual dos dois métodos será invocado pelas duas últimas linhas do código?

A primeira invocação parece ser simples, e é simples, na verdade - invocando `doanything()` a partir do objeto chamado `one` irá obviamente ativar o primeiro dos métodos.

A segunda invocação precisa de alguma atenção. Também é simples, se tivermos em mente como o Python encontra componentes de classe. A segunda invocação irá lançar `do_it()` na forma existente dentro da classe `Two` , independentemente do facto de a invocação ter lugar dentro da classe `One` .

Com efeito, o código produz o seguinte output:

output

```
do_it from One
do_it from Two
```

Nota: a situação em que **a subclasse é capaz de modificar o seu comportamento de superclasse (tal como no exemplo) é chamada polimorfismo**. A palavra vem do grego (polys: "muitas" e morphe, "forma"), o que significa que uma e a mesma classe pode tomar várias formas dependendo das redefinições feitas por qualquer uma das suas subclasses.

O método, redefinido em qualquer uma das superclasses, alterando assim o comportamento da superclasse, é chamado **virtual**.

Por outras palavras, nenhuma classe é dada de uma vez por todas. O comportamento de cada classe pode ser modificado em qualquer altura por qualquer uma das suas subclasses.

Vamos mostrar-lhe **como usar o polimorfismo para alargar a flexibilidade de classe.**

## 3.5.1.16 Fundamentos da OOP: Herança

## Como construir uma hierarquia de classes: continuação

Veja o exemplo no editor.

Parece-se com alguma coisa? Sim, claro que sim. Refere-se ao exemplo mostrado no início do módulo quando falamos sobre os conceitos gerais da programação objetiva.

Pode parecer estranho, mas não utilizámos a herança de forma alguma - apenas para mostrar que ela não nos limita, e conseguimos obter a nossa.

Definimos duas classes distintas capazes de produzir dois tipos diferentes de veículos terrestres. A principal diferença entre eles está na forma como viram. Um veículo com rodas apenas vira as rodas da frente (geralmente). Um veículo com lagartas tem de parar uma das lagartas.

Consegue seguir o código?

```
import time

class TrackedVehicle:
    def control_track(left, stop):
        pass

    def turn(left):
        control_track(left, True)
        time.sleep(0.25)
        control_track(left, False)


class WheeledVehicle:
    def turn_front_wheels(left, on):
        pass

    def turn(left):
        turn_front_wheels(left, True)
        time.sleep(0.25)
        turn_front_wheels(left, False)
```

* um veículo com lagartas faz uma curva ao parar e deslocar-se numa das suas lagartas (isto é feito pelo método control_track() , que será implementado mais tarde)
* um veículo com rodas gira quando as suas rodas da frente giram (isto é feito pelo método turn_front_wheels() )
* o método turn() utiliza o método adequado para cada veículo em particular.

Consegue ver **o que está errado com o código?**

Os métodos `turn()` parecem demasiado semelhantes para os deixar nesta forma.

Vamos reconstruir o código - vamos introduzir uma superclasse para reunir todos os aspetos semelhantes dos veículos de condução, deslocando todos os aspetos específicos para as subclasses.

## 3.5.1.17 Fundamentos da OOP: Herança

## Como construir uma hierarquia de classes: continuação

Veja o código no editor novamente. Isto é o que fizemos:

```
import time

class Vehicle:
    def change_direction(left, on):
        pass

    def turn(left):
        change_direction(left, True)
        time.sleep(0.25)
        change_direction(left, False)


class TrackedVehicle(Vehicle):
    def control_track(left, stop):
        pass

    def change_direction(left, on):
        control_track(left, on)


class WheeledVehicle(Vehicle):
    def turn_front_wheels(left, on):
        pass

    def change_direction(left, on):
        turn_front_wheels(left, on)
```

* definimos uma superclasse chamada `Vehicle`, que usa o método `turn()` para implementar um esquema geral de viragem, enquanto a viragem propriamente dita é feita por um método denominado `change_direction()`; nota: o método anterior está vazio, pois vamos colocar todos os detalhes na subclasse (tal método é muitas vezes chamado **método abstrato**, pois demonstra apenas alguma possibilidade que será instanciada mais tarde)
* definimos uma subclasse chamada `TrackedVehicle` (nota: é derivada da classe `Vehicle` ) que instanciou o método `change_direction()` utilizando o método específico (concreto) denominado `control_track()`
* respetivamente, a subclasse nomeada `WheeledVehicle` faz o mesmo truque, mas usa o método `turn_front_wheels()` para forçar o veículo a virar.

A vantagem mais importante (omitindo questões de legibilidade) é que esta forma de código permite implementar um algoritmo de viragem novinho em folha, apenas modificando o método `turn()` , que pode ser feito num só local, uma vez que todos os veículos o obedecerão.

É desta forma que o **polimorfismo ajuda o programador a manter o código limpo e consistente.**

## 3.5.1.18 Fundamentos da OOP: Herança

## Como construir uma hierarquia de classes: continuação

A herança não é a única forma de construir classes adaptáveis. Pode-se alcançar os mesmos objetivos (nem sempre, mas muito frequentemente) usando uma técnica denominada composição.

**Composição é o processo de compor um objeto utilizando outros objetos diferentes**. Os objetos utilizados na composição fornecem um conjunto de características desejadas (propriedades e/ou métodos) para que possamos dizer que agem como blocos utilizados para construir uma estrutura mais complicada.

Pode-se dizer que:

* a **herança alarga as capacidades de uma classe**, acrescentando novos componentes e modificando os existentes; por outras palavras, a receita completa está contida dentro da própria classe e de todos os seus antepassados; o objeto toma todos os pertences da classe e faz uso deles;
* a **composição projeta uma classe como um recipiente** capaz de armazenar e utilizar outros objetos (derivados de outras classes) onde cada um dos objetos implementa uma parte do comportamento de uma classe desejada.
Vamos ilustrar a diferença utilizando os veículos previamente definidos. A abordagem anterior levou-nos a uma hierarquia de classes em que a classe mais alta estava ciente das regras gerais utilizadas na viragem do veículo, mas não sabia como controlar os componentes apropriados (rodas ou lagartas).

As subclasses implementaram esta capacidade através da introdução de mecanismos especializados. Vamos fazer (quase) a mesma coisa, mas usando a composição. A classe - como no exemplo anterior - está ciente de como virar o veículo, mas a viragem real é feita por um objeto especializado armazenado numa propriedade chamada `controller`. A classe `controller` é capaz de controlar o veículo, manipulando as peças relevantes do veículo.

Observe o editor - é assim que poderia parecer.

```
import time

class Tracks:
    def change_direction(self, left, on):
        print("tracks: ", left, on)


class Wheels:
    def change_direction(self, left, on):
        print("wheels: ", left, on)


class Vehicle:
    def __init__(self, controller):
        self.controller = controller

    def turn(self, left):
        self.controller.change_direction(left, True)
        time.sleep(0.25)
        self.controller.change_direction(left, False)


wheeled = Vehicle(Wheels())
tracked = Vehicle(Tracks())

wheeled.turn(True)
tracked.turn(False)
```

Existem duas classes nomeadas `Tracks` e `Wheels` - elas sabem controlar a direção do veículo. Há também uma classe chamada Vehicle que pode utilizar qualquer um dos controladores disponíveis (os dois já definidos, ou qualquer outro definido no futuro) - a `controller` é ela própria passada para a classe durante a iniciação.

Desta forma, a capacidade de viragem do veículo é composta utilizando um objeto externo, não implementado no interior da `Vehicle` classe.

Por outras palavras, temos um veículo universal e podemos instalar nele tanto lagartas como rodas.

O código produz o seguinte output:

output

```
wheels:  True True
wheels:  True False
tracks:  False True
tracks:  False False
```

## 3.5.1.19 Fundamentos da OOP: Herança

## Herança única vs. herança múltipla

Como já sabe, não existem obstáculos à utilização de herança múltipla em Python. Pode derivar qualquer nova classe a partir de mais de uma classe previamente definida.

Existe apenas um "mas". O fato de o poder fazer não significa que tenha de o fazer.

Não se esqueça disso:

* uma única classe de herança é sempre mais simples, mais segura e mais fácil de compreender e manter;

* a herança múltipla é sempre arriscada, pois tem muito mais oportunidades de cometer um erro na identificação destas partes das superclasses, que irão influenciar efetivamente a nova classe;

* herança múltipla pode tornar o overriding extremamente complicado; além disso, a utilização da função `super()` torna-se ambígua;

* a herança múltipla viola o **princípio da responsabilidade única** (mais detalhes aqui: https://en.wikipedia.org/wiki/Single_responsibility_principle) uma vez que faz uma nova classe de duas (ou mais) classes que nada sabem uma sobre a outra;

* sugerimos fortemente a herança múltipla como a última de todas as soluções possíveis - se precisar realmente das muitas funcionalidades diferentes oferecidas pelas diferentes classes, a composição pode ser uma alternativa melhor.

## 3.5.1.20 Fundamentos da OOP: MRO

## O que é o Method Resolution Order (MRO) e porque é que nem todas as heranças fazem sentido?

MRO, em geral, é uma forma (pode-se chamar-lhe uma **estratégia**) em que uma determinada linguagem de programação analisa a parte superior da hierarquia de uma classe, a fim de encontrar o método de que ela necessita atualmente. Vale a pena salientar que línguas diferentes utilizam ligeiramente (ou mesmo completamente) diferentes MROs. O Python é uma criatura única a este respeito, contudo, e os seus costumes são um pouco específicos.

Vamos mostrar-lhe como funciona o MRO de Python em dois casos peculiares, que são exemplos claros de problemas que podem ocorrer quando se tenta usar a herança múltipla de forma demasiado imprudente. Vamos começar com um snippet que inicialmente pode parecer simples. Veja o que preparámos para si no editor.

Temos a certeza de que, se analisar o snippet você mesmo, não verá quaisquer anomalias no mesmo. Sim, tem toda a razão - parece claro e simples, e não suscita preocupações. Se executar o código, este produzirá o seguinte output previsível:

output

```
bottom
middle
top
```


Sem surpresas até agora. Vamos fazer uma pequena alteração neste código. Veja:

```
class Top:
    def m_top(self):
        print("top")


class Middle(Top):
    def m_middle(self):
        print("middle")


class Bottom(Middle, Top):
    def m_bottom(self):
        print("bottom")


object = Bottom()
object.m_bottom()
object.m_middle()
object.m_top()
```

Consegue ver a diferença? Está escondida nesta linha:

`class Bottom(Middle, Top):`

Desta forma exótica, transformamos um código muito simples com um claro caminho de uma única herança num misterioso enigma de múltiplas heranças. “É válido?” pode-se perguntar. Sim, é. "Como é isso possível?" deve perguntar agora, e esperamos que sinta realmente a necessidade de fazer esta pergunta.

Como pode ver, a ordem em que as duas superclasses foram listadas entre parêntesis está em conformidade com a estrutura do código: a classe `Middle` precede a classe `Top` , assim como no caminho da herança real.

Apesar da sua estranheza, a amostra está correta e funciona como esperado, mas é preciso afirmar que esta notação não traz nenhuma nova funcionalidade ou significado adicional.

Vamos modificar o código mais uma vez - agora vamos trocar os dois nomes de superclasse na definição de classe `Bottom` . Este é o aspeto que o snippet tem agora:

```
class Top:
    def m_top(self):
        print("top")


class Middle(Top):
    def m_middle(self):
        print("middle")


class Bottom(Top, Middle):
    def m_bottom(self):
        print("bottom")


object = Bottom()
object.m_bottom()
object.m_middle()
object.m_top()
```

Para antecipar a sua pergunta, diremos que esta emenda estragou o código, e que já não funcionará mais. Que pena. A ordem que tentamos forçar (Top, Middle) é incompatível com o caminho da herança que é derivado da estrutura do código. O Python não vai gostar. Isto é o que veremos:

output

`TypeError: Cannot create a consistent method resolution order (MRO) for bases Top, Middle`

Achamos que a mensagem fala por si. O MRO de Python não pode ser distorcido ou violado, não só porque é assim que o Python funciona, mas também porque é uma regra a que se tem de obedecer.

## 3.5.1.21 Fundamentos da OOP: MRO

## O problema do diamante

O segundo exemplo do espectro de questões que podem eventualmente surgir de heranças múltiplas é ilustrado por um problema clássico chamado o **problema do diamante**. O nome reflete a forma do diagrama da herança - dê uma vista de olhos na imagem:

![O conceito do problema do diamante](../Imagens/conceitoDiamante.jpg)

* Existe a superclasse mais alta chamada A;
* Existem duas subclasses derivadas de A: B e C;
* e há também a subclasse mais baixa chamada D, derivada de B e C (ou C e B, pois estas duas variantes significam coisas diferentes em Python)

Consegue ver o diamante ali?

Observe o código no editor. A mesma estrutura, mas expressa em Python.

```
class A:
    pass


class B(A):
    pass


class C(A):
    pass


class D(B, C):
    pass


d = D()
```

Algumas linguagens de programação proíbem a herança múltipla, e como consequência, não o deixam construir um diamante - esta é a rota que Java e C# escolheram seguir desde as suas origens.

O Python, contudo, escolheu uma rota diferente - permite herança múltipla, e não se importa se escrever e executar um código como o que está no editor. Mas não se esqueça do MRO - é sempre ele que manda.


Vamos reconstruir o nosso exemplo da página anterior para o tornar mais parecido com um diamante, tal como abaixo:
```
class Top:
    def m_top(self):
        print("top")


class Middle_Left(Top):
    def m_middle(self):
        print("middle_left")


class Middle_Right(Top):
    def m_middle(self):
        print("middle_right")


class Bottom(Middle_Left, Middle_Right):
    def m_bottom(self):
        print("bottom")


object = Bottom()
object.m_bottom()
object.m_middle()
object.m_top()
```

Nota: ambas as classes `Middle` **definem um método com o mesmo nome:** **m_middle()**.

Introduz uma pequena incerteza na nossa amostra, embora estejamos absolutamente certos de que pode responder à seguinte pergunta-chave: qual dos dois métodos `m_middle()` será realmente invocado quando a seguinte linha for executada?

`Object.m_middle()`

Por outras palavras, o que verá no ecrã: `middle_left` ou `middle_right`?

Não precisa de se apressar - pense duas vezes e tenha em mente o MRO do Python!

Está preparado?

Sim, tem razão. A invocação ativará o método `m_middle()` , que vem da classe `Middle_Left` . A explicação é simples: a classe está listada antes `Middle_Right` na lista de herança da classe `Bottom` . Se quiser ter a certeza de que não há dúvidas, tente trocar estas duas classes na lista e verifique os resultados.

Se quiser experimentar algumas impressões mais profundas sobre a herança múltipla e pedras preciosas, tente modificar o nosso snippet e equipar a classe `Upper` com outro espécime do método `m_middle()` , e investigue cuidadosamente o seu comportamento.

Como pode ver, os diamantes podem trazer alguns problemas à sua vida - tanto os verdadeiros como os oferecidos pelo Python.

## 3.5.1.22 RESUMO DA SECÇÃO 1/2

## Key takeaways

1. Um método chamado `__str__()` é responsável pela **conversão do conteúdo de um objeto numa string (mais ou menos) legível**. Pode redefini-la se quiser que o seu objeto se possa apresentar de uma forma mais elegante. Por exemplo:

```
class Mouse:
    def __init__(self, name):
        self.my_name = name


    def __str__(self):
        return self.my_name


the_mouse = Mouse('mickey')
print(the_mouse)  # Prints "mickey". 
```

2. Uma função chamada `issubclass(Class_1, Class_2)` é capaz de determinar se `Class_1` é uma **subclasse** de `Class_2`. Por exemplo:

```
class Mouse:
    pass


class LabMouse(Mouse):
    pass


print(issubclass(Mouse, LabMouse), issubclass(LabMouse, Mouse))  # Prints "False True"
```

3. Uma função chamada `isinstance(Object, Class)` verifica se um objeto **vem de uma classe indicada**. Por exemplo:

```
class Mouse:
    pass


class LabMouse(Mouse):
    pass


mickey = Mouse()
print(isinstance(mickey, Mouse), isinstance(mickey, LabMouse))  # Prints "True False".
```

4. Um operador chamado `is` verifica se duas variáveis se referem **ao mesmo objeto**. Por exemplo:

```
class Mouse:
    pass


mickey = Mouse()
minnie = Mouse()
cloned_mickey = mickey
print(mickey is minnie, mickey is cloned_mickey)  # Prints "False True".
```

5. Uma função sem parâmetros chamada `super()` devolve uma **referência para a superclasse mais próxima da classe.** Por exemplo:

```
class Mouse:
    def __str__(self):
        return "Mouse"


class LabMouse(Mouse):
    def __str__(self):
        return "Laboratory " + super().__str__()


doctor_mouse = LabMouse();
print(doctor_mouse)  # Prints "Laboratory Mouse".
```

6. Os métodos, bem como as variáveis de instância e classe definidas numa superclasse, são **automaticamente herdados** pelas suas subclasses. Por exemplo:
```
class Mouse:
    Population = 0
    def __init__(self, name):
        Mouse.Population += 1
        self.name = name

    def __str__(self):
        return "Hi, my name is " + self.name

class LabMouse(Mouse):
    pass

professor_mouse = LabMouse("Professor Mouser")
print(professor_mouse, Mouse.Population)  # Prints "Hi, my name is Professor Mouser 1"
```

7. Para encontrar qualquer propriedade objeto/classe, o Python procura-a no interior:

* do objeto em si;
* de todas as classes envolvidas na linha de herança do objeto, de baixo para cima;
* se houver mais do que uma classe num determinado caminho de herança, o Python digitaliza-as da esquerda para a direita;
* se ambos acima falharem, a exceção `AttributeError` é levantada.

8. Se qualquer uma das subclasses definir uma variável de método/classe variável/instância com o mesmo nome que a existente na superclasse, o novo nome **sobrepõe-se** a qualquer uma das instâncias anteriores do nome. Por exemplo:
```
class Mouse:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return "My name is " + self.name

class AncientMouse(Mouse):
    def __str__(self):
        return "Meum nomen est " + self.name

mus = AncientMouse("Caesar")  # Prints "Meum nomen est Caesar"
print(mus)
```

## 3.5.1.23 RESUMO DA SECÇÃO 2/2

## Exercícios

**Cenário**

Suponha que o seguinte snippet de código foi executado com sucesso:
```
class Dog:
    kennel = 0
    def __init__(self, breed):
        self.breed = breed
        Dog.kennel += 1
    def __str__(self):
        return self.breed + " says: Woof!"


class SheepDog(Dog):
    def __str__(self):
        return super().__str__() + " Don't run away, Little Lamb!"


class GuardDog(Dog):
    def __str__(self):
        return super().__str__() + " Stay where you are, Mister Intruder!"


rocky = SheepDog("Collie")
luna = GuardDog("Dobermann")
```

Agora responda às perguntas dos exercícios 1-4.


**Exercício 1**

Qual é o output esperado do seguinte snippet de código?
```
print(rocky)
print(luna)
```
Verifique

```
Collie says: Woof! Don't run away, Little Lamb!
Dobermann says: Woof! Stay where you are, Mister Intruder!
```

**Exercício 2**

Qual é o output esperado do seguinte snippet de código?
```
print(issubclass(SheepDog, Dog), issubclass(SheepDog, GuardDog))
print(isinstance(rocky, GuardDog), isinstance(luna, GuardDog))
```

Verifique
```
True False
False True
```

**Exercício 3**

Qual é o output esperado do seguinte snippet de código?
```
print(luna is luna, rocky is luna)
print(rocky.kennel)
```
Verifique
```
True False
2
```

**Exercício 4**

Defina uma subclasse `SheepDog` chamada `LowlandDog`, e equipe-a com um método `__str__()` que substitui um método herdado com o mesmo nome. O novo método dog's `__str__()` deve devolver a string “Woof! I don't like mountains!" .

Verifique
```
class LowlandDog(SheepDog):
	def __str__(self):
		return Dog.__str__(self) + " I don't like mountains!"
        ```