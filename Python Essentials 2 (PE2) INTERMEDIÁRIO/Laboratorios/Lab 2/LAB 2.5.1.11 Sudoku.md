## 2.5.1.11 LAB: Sudoku

## Tempo estimado
60-90 minutos

## Nível de dificuldade
Difícil

## Objetivos
* melhorar as competências do aluno em operar com strings e listas;
* converter strings em listas.

## Cenário
Como provavelmente sabe, o Sudoku é um puzzle de colocação de números jogado num tabuleiro 9x9. O jogador tem de preencher o tabuleiro de uma forma muito específica:

* cada linha do tabuleiro deve conter todos os dígitos de 1 a 9 (a ordem não importa)
* cada coluna do tabuleiro deve conter todos os dígitos de 1 a 9 (novamente, a ordem não importa)
* cada uma das nove "regiôes" 3x3 (vamos nomeá-las “sub-quadrados”) da tabela deve conter todos os dígitos de 1 a 9.

Se precisar de mais detalhes, pode encontrá-los [aqui](https://en.wikipedia.org/wiki/Sudoku).

A sua tarefa é escrever um programa que:

* leia 9 linhas do Sudoku, cada uma contendo 9 dígitos (verifique cuidadosamente se os dados introduzidos são válidos)
* faz o output Yes se o Sudoku for válido, e No caso contrário.

Teste o seu código utilizando os dados por nós fornecidos.

## Dados de teste
Input de amostra:

```
295743861
431865927
876192543
387459216
612387495
549216738
763524189
928671354
154938672
```

Exemplo de output:

`Yes`


Input de amostra:

```
195743862
431865927
876192543
387459216
612387495
549216738
763524189
928671354
254938671
```

Exemplo de output:

`No`
