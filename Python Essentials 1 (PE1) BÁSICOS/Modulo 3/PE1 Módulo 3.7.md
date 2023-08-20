## 3.7.1.1 Listas em aplicações avançadas

## Listas em listas
As listas podem consistir em escalares (nomeadamente números) e elementos de uma estrutura muito mais complexa (já viu exemplos como strings, booleanos, ou mesmo outras listas nas lições do Resumo da Secção anterior). Vamos analisar mais de perto o caso em que os elementos de uma lista são apenas listas.

Encontramos frequentemente tais arrays (matrizes) nas nossas vidas. Provavelmente o melhor exemplo disto é um tabuleiro de xadrez.

Um tabuleiro de xadrez é composto por linhas e colunas. Existem oito linhas (em inglês, rows) e oito colunas. Cada coluna é marcada com as letras de A a H. Cada linha é marcada com um número de um a oito.

A localização de cada campo é identificada por pares de letras-dígitos. Assim, sabemos que o canto inferior esquerdo do tabuleiro (o que tem a torre branca) é A1, enquanto que o canto oposto é H8.


Vamos assumir que somos capazes de utilizar os números selecionados para representar qualquer peça de xadrez. Podemos também assumir que cada linha do tabuleiro de xadrez é uma lista.

Veja o código abaixo:

row = []

for i in range(8):
    row.append(WHITE_PAWN)


Constrói uma lista contendo oito elementos que representam a segunda linha do tabuleiro de xadrez - a que está cheia de peões (suponha que WHITE_PAWN é um símbolo pré-definido que representa um peão branco).

O mesmo efeito pode ser alcançado através de uma compreensão de lista, a sintaxe especial utilizada por Python para preencher listas massivas.

Uma compreensão de lista é na realidade uma lista, mas criada durante a execução do programa, e não é descrita estaticamente.

Veja o snippet:

row = [WHITE_PAWN for i in range(8)]


A parte do código colocada dentro dos parêntesis retos especifica:

os dados a utilizar para preencher a lista (WHITE_PAWN)
a cláusula que especifica quantas vezes os dados ocorrem dentro da lista (for i in range(8))
Deixe-nos mostrar-lhe alguns outros exemplos de compreensão de lista:

Exemplo #1:

squares = [x ** 2 for x in range(10)]


O snippet produz uma lista de dez elementos preenchida com quadrados de dez números inteiros começando do zero (0, 1, 4, 9, 16, 25, 36, 49, 64, 81)

Exemplo #2:

twos = [2 ** i for i in range(8)]


O snippet cria um array de oito elementos contendo as primeiras oito potências de dois (1, 2, 4, 8, 16, 32, 64, 128)

Exemplo #3:

odds = [x for x in squares if x % 2 != 0 ]


O snippet faz uma lista apenas com os elementos ímpares da lista squares .