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

## 3.3.1.7 OOP: Propriedades

## 3.3.1.8 OOP: Propriedades

## 3.3.1.9 RESUMO DA SECÇÃO