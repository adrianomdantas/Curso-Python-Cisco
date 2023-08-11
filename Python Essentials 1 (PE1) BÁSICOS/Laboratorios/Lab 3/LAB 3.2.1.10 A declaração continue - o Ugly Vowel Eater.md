## 3.2.1.10 LAB: A declaração continue - o Ugly Vowel Eater

## Tempo estimado
10-20 minutos

## Nível de dificuldade
Fácil

## Objetivos
Familiarizar o aluno a:

* a utilização do loop continue em loops;
* refletir situações da vida real em código informático.

## Cenário

O comando `continue` é utilizada para saltar o bloco atual e avançar para a próxima iteração, sem executar as declarações dentro do loop.

Pode ser utilizada tanto com os loops `while` e `for` .

A sua tarefa aqui é muito especial: tem de conceber um vowel eater (comedor de vogais)! Escreva um programa que use:

* um loop for ;
* o conceito de execução condicional (if-elif-else)
* a declaração continue .

O seu programa deve:

* pedir ao utilizador para introduzir uma palavra;
* usar user_word = user_word.upper() para converter a palavra introduzida pelo utilizador em maiúsculas; falaremos sobre os chamados `**métodos de strings**` e o método `upper()` muito em breve - não se preocupe;
* usar execução condicional e a declaração `continue` para “comer” as seguintes vogais A, E, I, O, U da palavra introduzida;
* imprimir as letras não comidas noo ecrã, cada uma delas numa linha separada.

Teste o seu programa com os dados que lhe fornecemos.

## Dados de teste

Input de amostra: `Gregory`

Output esperado:
```
G
R
G
R
Y
```

Input de amostra: `abstemious`

Output esperado:
```
B
S
T
M
S
```

Input de amostra: `IOUEA`

Output esperado:

 
