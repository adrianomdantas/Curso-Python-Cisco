## 3.2.1.14 Contar stacks

## Tempo estimado
20-45 minutos

## Nível de dificuldade
Fácil/Médio

## Objetivos
* melhorar as competências do aluno na definição das classes;
* utilizar classes existentes para criar novas classes equipadas com novas funcionalidades.

## Cenário
Mostrámos recentemente como alargar as possibilidades de Stack definindo uma nova classe (ou seja, uma subclasse) que mantém todas as características herdadas e acrescenta alguns novos.

A sua tarefa é alargar o comportamento da classe `Stack` de modo a que a classe seja capaz de contar todos os elementos que são empurrados e popped (assumimos que a contagem de pops é suficiente). Utilize a classe `Stack` que fornecemos no editor.

Siga as dicas:

* introduza uma propriedade concebida para contar operações pop e nomeie-a de uma forma que garanta a sua ocultação;
* inicialize-a a zero no interior do construtor;
* forneça um método que devolva o valor atualmente atribuído ao contador (nomeie-o get_counter()).

Complete o código no editor. Execute-o para verificar se o seu código faz o output 100.

```
class Stack:
    def __init__(self):
        self.__stk = []

    def push(self, val):
        self.__stk.append(val)

    def pop(self):
        val = self.__stk[-1]
        del self.__stk[-1]
        return val


class CountingStack(Stack):
    def __init__(self):
    #
    # Fill the constructor with appropriate actions.
    #

    def get_counter(self):
    #
    # Present the counter's current value to the world.
    #

    def pop(self):
    #
    # Do pop and update the counter.
    #
	

stk = CountingStack()
for i in range(100):
    stk.push(i)
    stk.pop()
print(stk.get_counter())

```

