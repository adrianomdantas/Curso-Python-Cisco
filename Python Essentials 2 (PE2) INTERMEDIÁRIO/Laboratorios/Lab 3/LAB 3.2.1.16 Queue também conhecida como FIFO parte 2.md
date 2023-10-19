## 3.2.1.16 Queue também conhecida como FIFO: parte 2

## Tempo estimado
15-30 minutos

## Nível de dificuldade
Fácil/Médio

## Objetivos
* Melhorar as competências do aluno na definição de subclasses;
* adicionar uma nova funcionalidade a uma classe existente.

## Cenário
A sua tarefa é alargar ligeiramente as capacidades da classe `Queue` . Queremos que ele tenha um método sem parâmetros que devolva `True` se a queue estiver vazia e False caso contrário.

Complete o código que fornecemos no editor. Execute-o para verificar se ele produz um resultado semelhante ao nosso.

```
class QueueError(???):
    pass


class Queue:
    #
    # Code from the previous lab.
    #


class SuperQueue(Queue):
    #
    # Write new code here.
    #


que = SuperQueue()
que.put(1)
que.put("dog")
que.put(False)
for i in range(4):
    if not que.isempty():
        print(que.get())
    else:
        print("Queue empty")

```

Abaixo pode copiar o código que utilizámos no laboratório anterior:

Verifique
class QueueError(IndexError):
    pass


class Queue:
    def __init__(self):
        self.queue = []
    def put(self,elem):
        self.queue.insert(0,elem)
    def get(self):
        if len(self.queue) > 0:
            elem = self.queue[-1]
            del self.queue[-1]
            return elem
        else:
            raise QueueError




Output esperado

```
1
dog
False
Queue empty
```

