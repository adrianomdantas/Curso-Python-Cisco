## 3.2.1.15 Queue, também conhecida como FIFO

## Tempo estimado
20-45 minutos

## Nível de dificuldade
Fácil/Médio

## Objetivos
* melhorar as competências do aluno na definição das classes a partir do zero;
* implementação de estruturas de dados standard como classes.

## Cenário
Como já sabe, uma stack é uma estrutura de dados que realiza o chamado modelo LIFO (Last In - First Out). É fácil e já se habituou perfeitamente a isso.

Vamos provar algo novo agora. Uma queue (fila de espera) é um modelo de dados caraterizado pelo termo **FIFO: First In - Fist Out**. Nota: uma queue regular (fila) que conhece das lojas ou correios funciona exatamente da mesma maneira - um cliente que chegou primeiro também é servido primeiro.

A sua tarefa é implementar a classe `Queue` com duas operações básicas:

* `put(element)`, que coloca um elemento no final da queue;
* `get()`, que toma um elemento da frente da queue e o devolve como resultado (a queue não pode estar vazia para o executar com êxito.)

Siga as dicas:

* utilize uma lista como seu aramazenamento (tal como fizemos na stack)
* `put()` deve anexar elementos ao início da lista, enquanto get() deve remover os elementos do final da lista;
* defina uma nova exceção chamada `QueueError` (escolha uma exceção para derivá-la) e levante-a quando `get()` tenta operar numa lista vazia.

Complete o código que fornecemos no editor. Execute-o para verificar se o seu output é semelhante ao nosso.

## Output esperado

```
1
dog
False
Queue error
```

```
class QueueError(???):  # Choose base class for the new exception.
    #
    #  Write code here
    #


class Queue:
    def __init__(self):
        #
        # Write code here
        #

    def put(self, elem):
        #
        # Write code here
        #

    def get(self):
        #
        # Write code here
        #


que = Queue()
que.put(1)
que.put("dog")
que.put(False)
try:
    for i in range(4):
        print(que.get())
except:
    print("Queue error")

```