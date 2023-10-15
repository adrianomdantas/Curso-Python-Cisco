## 2.8.1.4 Ler ints em segurança

## Tempo estimado
15-25 minutos

## Nível de dificuldade**
Médio

## Objetivos
* Melhorar as competências do aluno na definição de funções;
* utilizar exceções a fim de proporcionar um ambiente de input seguro.

## Cenário

A sua tarefa é a de escrever uma **função capaz de fazer input de valores inteiros e de verificar se eles estão dentro de um intervalo especificado.**

A função deve:

* aceitar três argumentos: um prompt, um limite inferior aceitável e um limite superior aceitável;
* se o utilizador inserir uma string que não é um valor inteiro, a função deve emitir a mensagem Error: wrong input, e pedir ao utilizador para inserir o valor novamente;
* se o utilizador introduzir um número que fica fora do intervalo especificado, a função deve emitir a mensagem Error: the value is not within permitted range (min..max) e pedir ao utilizador para inserir o valor novamente;
* se o valor de input for válido, devolve-o como um resultado.

## Dados de teste
Teste o seu código com cuidado.

```def read_int(prompt, min, max):
    #
    # Write your code here.
    #


v = read_int("Enter a number from -10 to 10: ", -10, 10)

print("The number is:", v)
```

É assim que a função deve reagir ao input do utilizador:
```
Enter a number from -10 to 10: 100
Error: the value is not within permitted range (-10..10)
Enter a number from -10 to 10: asd
Error: wrong input
Enter number from -10 to 10: 1
The number is: 1
```