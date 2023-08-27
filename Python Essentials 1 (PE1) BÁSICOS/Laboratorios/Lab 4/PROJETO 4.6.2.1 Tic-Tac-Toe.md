## 4.6.2.1 PROJETO: Tic-Tac-Toe

## Tempo estimado
30-120 minutos

## Nível de dificuldade
Médio/Difícil

## Objetivos

* aperfeiçoar as competências do aluno na utilização de Python para a resolução de problemas complexos,
* integração de técnicas de programação num programa consituído por várias partes.

## Cenário

A sua tarefa é escrever **um programa simples que finja jogar tic-tac-toe com o utilizador**. Para lhe facilitar as coisas, decidimos simplificar o jogo. Aqui estão os nossos pressupostos:

* o computador (ou seja, o seu programa) deve jogar o jogo utilizando `'X'`s;
* o utilizador (por exemplo, você) deve jogar o jogo utilizando `'O'`s;
* o primeiro movimento pertence ao computador - coloca sempre o seu primeiro `'X'` no meio do tabuleiro;
* todos os quadrados são numerados fila a fila começando por `1` (veja a sessão de exemplo abaixo, para referência)
* o utilizador introduz a sua jogada inserindo o número do quadrado que escolhe - o número deve ser válido, ou seja, deve ser um número inteiro, deve ser maior do que `0` e menos do que `10`, e não pode apontar para um campo que já esteja ocupado;
* o programa verifica se o jogo terminou - há quatro vereditos possíveis: o jogo deve continuar, ou o jogo termina com um empate, a sua vitória ou a vitória do computador;
* o computador responde com a sua jogada e a verificação é repetida;
* não implemente nenhuma forma de inteligência artificial - uma escolha de campo aleatória feita pelo computador é suficientemente boa para o jogo.

A sessão de exemplo com o programa pode ter a aparência seguinte:
```
+-------+-------+-------+
|       |       |       |
|   1   |   2   |   3   |
|       |       |       |
+-------+-------+-------+
|       |       |       |
|   4   |   X   |   6   |
|       |       |       |
+-------+-------+-------+
|       |       |       |
|   7   |   8   |   9   |
|       |       |       |
+-------+-------+-------+
Enter your move: 1
+-------+-------+-------+
|       |       |       |
|   O   |   2   |   3   |
|       |       |       |
+-------+-------+-------+
|       |       |       |
|   4   |   X   |   6   |
|       |       |       |
+-------+-------+-------+
|       |       |       |
|   7   |   8   |   9   |
|       |       |       |
+-------+-------+-------+
+-------+-------+-------+
|       |       |       |
|   O   |   X   |   3   |
|       |       |       |
+-------+-------+-------+
|       |       |       |
|   4   |   X   |   6   |
|       |       |       |
+-------+-------+-------+
|       |       |       |
|   7   |   8   |   9   |
|       |       |       |
+-------+-------+-------+
Enter your move: 8
+-------+-------+-------+
|       |       |       |
|   O   |   X   |   3   |
|       |       |       |
+-------+-------+-------+
|       |       |       |
|   4   |   X   |   6   |
|       |       |       |
+-------+-------+-------+
|       |       |       |
|   7   |   O   |   9   |
|       |       |       |
+-------+-------+-------+
+-------+-------+-------+
|       |       |       |
|   O   |   X   |   3   |
|       |       |       |
+-------+-------+-------+
|       |       |       |
|   4   |   X   |   X   |
|       |       |       |
+-------+-------+-------+
|       |       |       |
|   7   |   O   |   9   |
|       |       |       |
+-------+-------+-------+
Enter your move: 4
+-------+-------+-------+
|       |       |       |
|   O   |   X   |   3   |
|       |       |       |
+-------+-------+-------+
|       |       |       |
|   O   |   X   |   X   |
|       |       |       |
+-------+-------+-------+
|       |       |       |
|   7   |   O   |   9   |
|       |       |       |
+-------+-------+-------+
+-------+-------+-------+
|       |       |       |
|   O   |   X   |   X   |
|       |       |       |
+-------+-------+-------+
|       |       |       |
|   O   |   X   |   X   |
|       |       |       |
+-------+-------+-------+
|       |       |       |
|   7   |   O   |   9   |
|       |       |       |
+-------+-------+-------+
Enter your move: 7
+-------+-------+-------+
|       |       |       |
|   O   |   X   |   X   |
|       |       |       |
+-------+-------+-------+
|       |       |       |
|   O   |   X   |   X   |
|       |       |       |
+-------+-------+-------+
|       |       |       |
|   O   |   O   |   9   |
|       |       |       |
+-------+-------+-------+
You won!
```
## Requisitos

Implemente as seguintes características:

* o tabuleiro deve ser armazenado como uma lista de três elementos, enquanto cada elemento é outra lista de três elementos (as listas internas representam linhas) de modo a que todos os quadrados possam ser acedidos utilizando a seguinte sintaxe:

`board[row][column]`

* cada um dos elementos da lista interna pode conter 'O', 'X', ou um dígito que representa o número do quadrado (tal quadrado é considerado livre)
* a aparência do tabuleiro deve ser exatamente a mesma que a apresentada no exemplo.
* implemente as funções definidas para si no editor.

O desenho de um número inteiro aleatório pode ser feito utilizando uma função Python chamada `randrange()`. O programa de exemplo abaixo mostra como utilizá-lo (o programa imprime dez números aleatórios de 0 a 8).

Nota: a instrução `from-import` fornece um acesso à função `randrange` definida dentro de um módulo externo de Python chamado `random`.
```
from random import randrange

for i in range(10):
    print(randrange(8))
```


 
 Sandbox

Code
```
def display_board(board):
# The function accepts one parameter containing the board's current status
# and prints it out to the console.


def enter_move(board):
# The function accepts the board current status, asks the user about their move,
# checks the input and updates the board according to the user's decision.


def make_list_of_free_fields(board):
# The function browses the board and builds a list of all the free squares;
# the list consists of tuples, while each tuple is a pair of row and column numbers.


def victory_for(board, sign):
# The function analyzes the board status in order to check if
# the player using 'O's or 'X's has won the game


def draw_move(board):
# The function draws the computer's move and updates the board.
def display_board(board):

```
