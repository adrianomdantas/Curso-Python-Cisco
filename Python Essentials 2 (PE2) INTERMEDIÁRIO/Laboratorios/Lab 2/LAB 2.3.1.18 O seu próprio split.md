## 2.3.1.18 O seu próprio split

## Tempo estimado
 20-25 minutos

## Nível de dificuldade
Médio

## Objetivos
* melhorar as habilidades do aluno a operar com strings;
* utilizar métodos de string Python incorporados.

## Cenário
Já sabe como `split()` funciona. Agora queremos que o prove.

A sua tarefa é **escrever a sua própria função, que se comporta quase exatamente como o método original** `split()` , ou seja:

* deve aceitar exatamente um argumento - uma string;
* deve devolver uma lista de palavras criadas a partir da string, dividida nos locais onde a string contém espaços em branco;
* se a string estiver vazia, a função deve devolver uma lista vazia;
* o seu nome deve ser mysplit()

Utilize o template no editor. Teste o seu código com cuidado.

```
def mysplit(strng):
    #
    # put your code here
    #


print(mysplit("To be or not to be, that is the question"))
print(mysplit("To be or not to be,that is the question"))
print(mysplit("   "))
print(mysplit(" abc "))
print(mysplit(""))

```

Output esperado

```
['To', 'be', 'or', 'not', 'to', 'be,', 'that', 'is', 'the', 'question']
['To', 'be', 'or', 'not', 'to', 'be,that', 'is', 'the', 'question']
[]
['abc']
[]

```