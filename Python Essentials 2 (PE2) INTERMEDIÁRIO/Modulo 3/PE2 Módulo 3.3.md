## 3.3.1.1 OOP: Propriedades

## Variáveis de instância

Em geral, uma classe pode ser equipada com dois tipos diferentes de dados para formar as propriedades de uma classe. Já viu um deles quando estávamos a olhar para stacks.

Este tipo de propriedade de classe existe quando e só quando é explicitamente criada e adicionada a um objeto. Como já sabe, isto pode ser feito durante a inicialização do objeto, realizada pelo construtor.

Além disso, pode ser feito em qualquer momento da vida do objeto. Mais, qualquer propriedade existente pode ser removida em qualquer altura.

Uma tal abordagem tem algumas consequências importantes:

* objetos diferentes da mesma classe **podem possuir conjuntos diferentes de propriedades;**
* deve haver uma forma de **verificar com segurança se um objeto específico possui a propriedade** que pretende utilizar (a menos que queira provocar uma exceção - vale sempre a pena considerar)
* cada objeto **carrega o seu próprio conjunto de propriedades** - eles não interferem uns com os outros de forma alguma.

Tais variáveis (propriedades) são chamadas **variáveis de instância**.

A palavra *instância* sugere que elas estão intimamente ligadas aos objetos (que são instâncias de classe), não às classes propriamente ditas. Vamos dar-lhes uma olhadela mais atenta.

Aqui está um exemplo:
```
class ExampleClass:
    def __init__(self, val = 1):
        self.first = val

    def set_second(self, val):
        self.second = val


example_object_1 = ExampleClass()
example_object_2 = ExampleClass(2)

example_object_2.set_second(3)

example_object_3 = ExampleClass(4)
example_object_3.third = 5

print(example_object_1.__dict__)
print(example_object_2.__dict__)
print(example_object_3.__dict__)
```

Precisa de uma explicação adicional antes de entrarmos em qualquer outro detalhe. Dê uma vista de olhos às três últimas linhas do código.

Os objetos Python, quando criados, são dotados de um **pequeno conjunto de propriedades e métodos pré-definidos**. Cada objeto tem-nos, quer os queira ou não. Um deles é uma variável chamada `__dict__` (é um dicionário).

A variável contém os nomes e valores de todas as propriedades (variáveis) que o objeto carrega atualmente. Vamos utilizá-la para apresentar o conteúdo de um objeto em segurança.

Vamos agora mergulhar no código:

* a classe nomeada `ExampleClass` tem um construtor, que **cria incondicionalmente uma variável de instância** chamada `first`, e define-a com o valor passado através do primeiro argumento (da perspetiva do utilizador da classe) ou do segundo argumento (da perspetiva do construtor); note o valor por defeito do parâmetro - qualquer truque que se possa fazer com um parâmetro de função regular também pode ser aplicado aos métodos;

* a classe também tem um **método que cria outra variável de instância**, denominada `second`;

* criámos três objetos da classe `ExampleClass`, mas todas estas instâncias diferem:

    * `example_object_1` só tem a propriedade nomeada `first`;

    * `example_object_2` tem duas propriedades: `first` e `second`;

    * `example_object_3` foi enriquecido com uma propriedade chamada `third` enquanto em movimento, fora do código da classe - isto é possível e totalmente admissível.

Os outputs do programa mostram claramente que os nossos pressupostos estão corretos - aqui está:

output

```
{'first': 1}
{'second': 3, 'first': 2}
{'third': 5, 'first': 4}
```

Há uma conclusão adicional que deve ser afirmada aqui: **a modificação de uma variável de instância de qualquer objeto não tem impacto em todos os objetos restantes**. As variáveis de instância estão perfeitamente isoladas umas das outras.

## 3.3.1.2 OOP: Propriedades

## Variáveis de instância: continuação

Dê uma vista de olhos ao exemplo modificado no editor.

```
class ExampleClass:
    def __init__(self, val = 1):
        self.__first = val

    def set_second(self, val = 2):
        self.__second = val


example_object_1 = ExampleClass()
example_object_2 = ExampleClass(2)

example_object_2.set_second(3)

example_object_3 = ExampleClass(4)
example_object_3.__third = 5


print(example_object_1.__dict__)
print(example_object_2.__dict__)
print(example_object_3.__dict__)
```

É quase o mesmo que o anterior. A única diferença está nos nomes das propriedades. **Adicionamos dois underscores** (`__`) à frente deles.

Como sabe, tal adição torna a variável de instância **privada** - torna-se inacessível a partir do mundo exterior.

O comportamento real destes nomes é um pouco mais complicado, por isso vamos executar o programa. Este é o output:

output

```
{'_ExampleClass__first': 1}
{'_ExampleClass__first': 2, '_ExampleClass__second': 3}
{'_ExampleClass__first': 4, '__third': 5}
```

Consegue ver estes estranhos nomes cheios de underscores? De onde vieram eles?

Quando o Python vê que quer adicionar uma variável de instância a um objeto, e vai fazê-lo dentro de qualquer um dos métodos do objeto, ele **modula a operação** da seguinte forma:

* coloca um nome de classe antes do seu nome;
* coloca um underscore adicional no início.

É por isso que o `__first` torna-se `_ExampleClass__first`.

**O nome é agora totalmente acessível a partir do exterior da classe**. Pode executar um código como este:

`print(example_object_1._ExampleClass__first)`

e obterá um resultado válido, sem erros ou exceções.

Como pode ver, tornar uma propriedade privada é limitado.

**O mangling não funcionará se se adicionar uma variável de instância privada fora do código de classe**. Neste caso, comportar-se-á como qualquer outra propriedade.

## 3.3.1.3 OOP: Propriedades

## Variáveis de classe

Uma variável de classe é **uma propriedade que existe apenas numa cópia e é armazenada fora de qualquer objeto.**

Nota: não existe uma variável de instância se não houver nenhum objeto na classe; existe uma variável de classe numa cópia, mesmo que não haja objetos na classe.

As variáveis de classe são criadas de forma diferente dos seus irmãos de instância. O exemplo dir-lhe-á mais:

```
class ExampleClass:
    counter = 0
    def __init__(self, val = 1):
        self.__first = val
        ExampleClass.counter += 1


example_object_1 = ExampleClass()
example_object_2 = ExampleClass(2)
example_object_3 = ExampleClass(4)

print(example_object_1.__dict__, example_object_1.counter)
print(example_object_2.__dict__, example_object_2.counter)
print(example_object_3.__dict__, example_object_3.counter)
```

Veja:

* existe uma atribuição na primeira lista da definição da classe - define a variável chamada `counter` até 0; inicializar a variável dentro da classe mas fora de qualquer um dos seus métodos torna a variável uma variável de classe;
* o acesso a tal variável tem o mesmo aspeto que o acesso a qualquer atributo de instância - pode vê-la no corpo do construtor; como pode ver, o construtor incrementa a variável por um; com efeito, a variável conta todos os objetos criados.
* 
A execução do código causará o seguinte output:

output
```
{'_ExampleClass__first': 1} 3
{'_ExampleClass__first': 2} 3
{'_ExampleClass__first': 4} 3
```

Duas conclusões importantes vêm do exemplo:

* variáveis de classe **não são mostradas num objeto** `__dict__` (isto é natural porque as variáveis de classe não são partes de um objeto) mas pode sempre tentar olhar para a variável do mesmo nome, mas ao nível da classe - vamos mostrar-lhe isto muito em breve;
* uma variável de classe **apresenta sempre o mesmo valor** em todas as instâncias de classe (objetos)

## 3.3.1.4 OOP: Propriedades

## Variáveis de classe: continuação

A mutilação do nome de uma variável de classe tem os mesmos efeitos que aqueles com que já está familiarizado.

Veja o exemplo no editor. Consegue adivinhar o seu output?

```
class ExampleClass:
    __counter = 0
    def __init__(self, val = 1):
        self.__first = val
        ExampleClass.__counter += 1


example_object_1 = ExampleClass()
example_object_2 = ExampleClass(2)
example_object_3 = ExampleClass(4)

print(example_object_1.__dict__, example_object_1._ExampleClass__counter)
print(example_object_2.__dict__, example_object_2._ExampleClass__counter)
print(example_object_3.__dict__, example_object_3._ExampleClass__counter)
```

Execute o programa e verifique se as suas previsões estavam corretas. Tudo funciona como esperado, não é verdade?

## 3.3.1.5 OOP: Propriedades

## Variáveis de classe: continuação

Dissemos-lhe antes que as variáveis de classe existem mesmo quando nenhuma instância de classe (objeto) tenha sido criada.

Agora vamos aproveitar a oportunidade para lhe mostrar a **diferença entre estas duas variáveis** `__dict__` , a da classe e a do objeto.

Veja o código no editor. A prova está lá.

Vamos analisar mais de perto:

1. Definimos uma classe chamada `ExampleClass`;

2. A classe define uma variável de classe chamada `varia`;

3. O construtor de classe define a variável com o valor do parâmetro;

4. Nomear a variável é o aspeto mais importante do exemplo porque:
    * Alterar a atribuição para `self.varia = val` criaria uma variável de instância com o mesmo nome que o da classe;
    * Alterar a atribuição para `varia = val` operaria na variável local de um método; (encorajamo-lo vivamente a testar os dois casos acima referidos - isto facilitar-lhe-á a lembrar-se da diferença)

5. A primeira linha do código fora da classe imprime o valor do atributo `ExampleClass.varia` ; nota - usamos o valor antes que o primeiro objeto da classe seja instanciado.
 
Execute o código no editor e verifique o seu output.

```
class ExampleClass:
    varia = 1
    def __init__(self, val):
        ExampleClass.varia = val


print(ExampleClass.__dict__)
example_object = ExampleClass(2)

print(ExampleClass.__dict__)
print(example_object.__dict__)
```

Como pode ver, a classe `__dict__` contém muito mais dados do que a contraparte do seu objeto. A maioria deles são inúteis agora - aquele que queremos que verifique cuidadosamente mostra o valor varia corrente.

Observe que o `__dict__` do objeto está vazio - o objeto não tem variáveis de instância.

## 3.3.1.6 OOP: Propriedades

## Verificação da existência de um atributo

A atitude do Python em relação à instanciação de objetos levanta uma questão importante - em contraste com outras linguagens de programação, **não se pode esperar que todos os objetos da mesma classe tenham o mesmo conjunto de propriedades.**

Assim como no exemplo no editor. Olhe com atenção.

```
class ExampleClass:
    def __init__(self, val):
        if val % 2 != 0:
            self.a = 1
        else:
            self.b = 1


example_object = ExampleClass(1)

print(example_object.a)
print(example_object.b)
```

O objeto criado pelo construtor pode ter apenas um dos dois atributos possíveis: `a` ou `b`.

A execução do código produzirá o seguinte output:

output

```
1
Traceback (most recent call last):
  File ".main.py", line 11, in 
    print(example_object.b)
AttributeError: 'ExampleClass' object has no attribute 'b'
```

Como pode ver, o acesso a um atributo de objeto (classe) inexistente causa uma AttributeError exceção.

## 3.3.1.7 OOP: Propriedades

## Verificação da existência de um atributo: continuação

A instrução `try-except` dá-lhe a oportunidade de evitar problemas com propriedades inexistentes.

É fácil - veja o código no editor.

```
class ExampleClass:
    def __init__(self, val):
        if val % 2 != 0:
            self.a = 1
        else:
            self.b = 1


example_object = ExampleClass(1)
print(example_object.a)

try:
    print(example_object.b)
except AttributeError:
    pass
```

Como se pode ver, esta ação não é muito sofisticada. Essencialmente, apenas varremos o problema para debaixo do tapete.

Felizmente, há mais uma forma de lidar com o problema.

O Python fornece uma **função capaz de verificar com segurança se algum objeto/classe contém uma propriedade especificada.** A função é chamada hasattr, e espera que lhe sejam transmitidos dois argumentos:

* A classe ou o objeto a ser verificado;
* o nome da propriedade cuja existência tem de ser comunicada (nota: tem de ser uma string contendo o nome do atributo, e não apenas o nome)

A função devolve `True` ou `False`.

É assim que a pode utilizar:
```
class ExampleClass:
    def __init__(self, val):
        if val % 2 != 0:
            self.a = 1
        else:
            self.b = 1


example_object = ExampleClass(1)
print(example_object.a)

if hasattr(example_object, 'b'):
    print(example_object.b)
```
## 3.3.1.8 OOP: Propriedades

## Verificação da existência de um atributo: continuação

Não se esqueça que a função `hasattr()` também pode operar em classes. Pode utilizá-la **para descobrir se uma variável de classe está disponível**, tal como aqui no exemplo do editor.

A função devolve `True` se a classe especificada contiver um determinado atributo, e `False` caso contrário.

Consegue adivinhar o output do código? Execute-o para verificar as suas suposições.

```
class ExampleClass:
    attr = 1


print(hasattr(ExampleClass, 'attr'))
print(hasattr(ExampleClass, 'prop'))
```

otput

```
True
False
```

E mais um exemplo - veja o código abaixo e tente prever o seu output:
```
class ExampleClass:
    a = 1
    def __init__(self):
        self.b = 2


example_object = ExampleClass()

print(hasattr(example_object, 'b'))
print(hasattr(example_object, 'a'))
print(hasattr(ExampleClass, 'b'))
print(hasattr(ExampleClass, 'a'))
```

Foi bem sucedido? Execute o código para verificar as suas previsões.

Muito bem, chegámos ao fim desta secção. Na secção seguinte vamos falar de métodos, uma vez que os métodos conduzem os objetos e os tornam ativos.

## 3.3.1.9 RESUMO DA SECÇÃO

## Key takeaways

1. Uma **variável de instância** é uma propriedade cuja existência depende da criação de um objeto. Cada objeto pode ter um conjunto diferente de variáveis de instância.

Além disso, eles podem ser livremente adicionados aos, e removidos dos, objetos durante a sua vida útil. Todas as variáveis de instância de objeto são armazenadas dentro de um dicionário dedicado, chamado `__dict__`, contido em cada objeto separadamente.

2. Uma variável de instância pode ser privada quando o seu nome começa por `__`, mas não se esqueça que tal propriedade ainda é acessível de fora da classe, utilizando um **nome mangled** construído como `_ClassName__PrivatePropertyName`.

3. Uma **variável de classe** é uma propriedade que existe exatamente numa cópia, e não precisa de nenhum objeto criado para ser acessível. Tais variáveis não são mostradas como conteúdo `__dict__` .

Todas as variáveis de classe de uma classe são armazenadas dentro de um dicionário dedicado, chamado `__dict__`, contido em cada classe separadamente.

4. Uma função chamada `hasattr()` pode ser utilizada para determinar se um qualquer objeto/classe contém uma propriedade especificada.

Por exemplo:
```
class Sample:
    gamma = 0 # Class variable.
    def __init__(self):
        self.alpha = 1 # Instance variable.
        self.__delta = 3 # Private instance variable.


obj = Sample()
obj.beta = 2  # Another instance variable (existing only inside the "obj" instance.)
print(obj.__dict__)
```

Output do código:

output

`{'alpha': 1, '_Sample__delta': 3, 'beta': 2}`


**Exercício 1**

Quais das `Python` propriedades de classe são variáveis de instância, e quais são variáveis de classe? Quais delas são privadas?
```
class Python:
    population = 1
    victims = 0
    def __init__(self):
        self.length_ft = 3
        self.__venomous = False
```
Verifique

`population` e `victims` são variáveis de **classe**, enquanto `length` e `__venomous` são variáveis de **instância** (a última também é **privada**).

**Exercício 2**

Vai negar a `__venomous` propriedade do objeto version_2 , ignorando o facto de que a propriedade é privada. Como vai fazer isto?

`version_2 = Python()`


Verifique

`version_2._Python__venomous = not version_2._Python__venomous`


**Exercício 3**

Escreva uma expressão que verifica se o objeto `version_2` contém uma propriedade de instância chamada `constrictor` (sim, constrictor!).

Verifique

`hasattr(version_2, 'constrictor')`
