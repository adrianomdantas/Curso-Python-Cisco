## 3.2.1.1 Uma curta viagem da abordagem processual à abordagem ao objeto

## O que é uma stack?

**Uma stack (pilha) é uma estrutura desenvolvida para armazenar dados de uma forma muito específica**. Imagine uma pilha de moedas. Não se pode colocar uma moeda em mais lado nenhum, a não ser no topo da pilha.

Da mesma forma, não se pode tirar uma moeda da pilha de qualquer outro lugar que não seja do topo da pilha. Se quiser obter a moeda que está no fundo, tem de retirar todas as moedas dos níveis superiores.

O nome alternativo para uma pilha (mas apenas em terminologia de TI) é **LIFO**.

É uma abreviação para uma descrição muito clara do comportamento da pilha: **Last In - First Out**. A moeda que chegou em último lugar à pilha sairá primeiro.

**Uma stack é um objeto** com duas operações elementares, convencionalmente denominadas **push** (quando um novo elemento é colocado no topo) e **pop** (quando um elemento existente é retirado do topo).

As stacks são muitas vezes utilizadas em muitos algoritmos clássicos, e é difícil imaginar a implementação de muitas ferramentas amplamente utilizadas sem o uso de stack.

![O conceito de stack](../Imagens/conceitoStack.jpg)

Vamos implementar uma stack no Python. Esta será uma stack muito simples, e mostrar-lhe-emos como fazê-lo em duas abordagens independentes: processual e objetiva.

Vamos começar com a primeira.

## 3.2.1.2 Uma curta viagem da abordagem processual à abordagem ao objeto

## A stack - a abordagem processual

Primeiro, é preciso decidir como armazenar os valores que chegarão à stack. Sugerimos a utilização do mais simples dos métodos, e **o emprego de uma lista** para este trabalho. Vamos assumir que o tamanho da stack não é limitado de forma alguma. Vamos também assumir que o último elemento da lista armazena o elemento superior.

A stack em si já está criada:

`stack = []`

Estamos prontos para **definir uma função que coloca um valor na stack**. Aqui estão os pressupostos para tal:

* o nome para a função é `push`;
* a função obtém um parâmetro (este é o valor a ser colocado na stack)
* a função não devolve nada;
* a função anexa o valor do parâmetro ao fim da stack;

Foi assim que o fizemos - observe:

```
def push(val):
    stack.append(val)
```

Agora é hora de uma **função tirar um valor da stack**. É assim que o pode fazer:

* o nome da função é pop;
* a função não obtém nenhum parâmetro;
* a função devolve o valor retirado da stack
* a função lê o valor da parte superior da stack e remove-o.

A função está aqui:

```
def pop():
    val = stack[-1]
    del stack[-1]
    return val
```

Nota: a função não verifica se existe algum elemento na stack.

Vamos juntar todas as peças para pôr a stack em movimento. O **programa completo** empurra três números para a stack, puxa-os para fora e imprime os seus valores no ecrã. Pode vê-lo na janela do editor.

```
stack = []


def push(val):
    stack.append(val)


def pop():
    val = stack[-1]
    del stack[-1]
    return val


push(3)
push(2)
push(1)

print(pop())
print(pop())
print(pop())
```

O programa faz output do seguinte texto para o ecrã:

output

```
1
2
3
```

Teste-o.

## 3.2.1.3 Uma curta viagem da abordagem processual à abordagem ao objeto

## A stack - a abordagem processual vs. a abordagem orientada a objetos

A stack processual está pronta. Claro que existem algumas fraquezas, e a implementação poderia ser melhorada de muitas maneiras (aproveitar as exceções para o trabalho é uma boa ideia), mas em geral a stack está totalmente implementada, e pode utilizá-la se for necessário.

Mas quanto mais vezes a utilizar, mais desvantagens encontrará. Aqui estão algumas delas:

* a variável essencial (a lista da stack) é altamente **vulnerável**; qualquer pessoa pode modificá-la de uma forma incontrolável, destruindo a stack, de facto; isto não significa que tenha sido feita de forma maliciosa - pelo contrário, pode acontecer como resultado de descuido, por exemplo, quando alguém confunde nomes de variáveis; imagine que escreveu acidentalmente algo do género:

`stack[0] = 0`

O funcionamento da stackserá completamente desorganizado;

* pode também acontecer que um dia precise de mais do que uma stack; terá de criar outra lista para o armazenamento da stack, e provavelmente outras funções `push` e `pop` também;

* também pode acontecer que precisa não só de funções `push` e `pop` , mas também de algumas outras conveniências; poderia certamente implementá-las, mas tente imaginar o que aconteceria se tivesse dezenas de stacks implementadas separadamente.

A abordagem objetiva proporciona soluções para cada um dos problemas acima referidos. Vamos nomeá-las primeiro:

* a capacidade de ocultar (proteger) valores selecionados contra o acesso não autorizado chama-se **encapsulamento; os valores encapsulados não podem ser acedidos nem modificados se se quiser utilizá-los exclusivamente;**

* quando se tem uma classe implementando todos os comportamentos de stack necessários, pode-se produzir quantas stacks se quiser; não é necessário copiar ou replicar qualquer parte do código;

* a capacidade de enriquecer a stack com novas funções vem da herança; pode-se criar uma nova classe (uma subclasse) que herda todos os traços existentes da superclasse, e acrescenta alguns novos.

![A stack - abordagem processual vs. ao objeto](../Imagens/stack.jpg)

Vamos agora escrever uma nova implementação de stack a partir do zero. Desta vez, vamos utilizar a abordagem objetiva, guiando-o passo a passo para o mundo da programação de objetos.

## 3.2.1.4 Uma curta viagem da abordagem processual à abordagem ao objeto

## 

## 3.2.1.5 Uma curta viagem da abordagem processual à abordagem ao objeto

## 3.2.1.6 Uma curta viagem da abordagem processual à abordagem ao objeto

## 3.2.1.7 Uma curta viagem da abordagem processual à abordagem ao objeto

## 3.2.1.8 Uma curta viagem da abordagem processual à abordagem ao objeto


## 3.2.1.9 Uma curta viagem da abordagem processual à abordagem ao objeto


## 3.2.1.10 Uma curta viagem da abordagem processual à abordagem ao objeto

## 3.2.1.11 Uma curta viagem da abordagem processual à abordagem ao objeto

## 3.2.1.12 Uma curta viagem da abordagem processual à abordagem ao objeto

## 3.2.1.13 RESUMO DA SECÇÃO

## 3.2.1.14 Contar stacks

## 3.2.1.15 Queue, também conhecida como FIFO

## 3.2.1.16 Queue também conhecida como FIFO: parte 2
