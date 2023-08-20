## 3.6.1.9 LAB: Operações com listas - noções básicas

## Tempo estimado
10-15 minutos

## Nível de dificuldade
Fácil

## Objetivos
Familiarizar o aluno a:

* indexação de lista;
* utilizar os operadores in e not in .

## Cenário

Imagine uma lista - não muito longa, não muito complicada, apenas uma simples lista contendo alguns números inteiros. Alguns desses números podem ser repetidos, e esta é a pista. Não queremos repetições. Queremos que sejam removidas.

A sua tarefa é escrever um programa que remova todas as repetições de números da lista. O objetivo é ter uma lista na qual todos os números não aparecem mais de uma vez.

Nota: suponha que a source list está codificada dentro do código - não tem de a introduzir a partir do teclado. É claro que pode melhorar o código e adicionar uma parte que pode realizar uma conversa com o utilizador e obter todos os dados a partir dele.

Dica: encorajamo-lo a criar uma nova lista como área de trabalho temporária - não precisa de atualizar a lista in situ.

Não fornecemos dados de teste, pois isso seria demasiado fácil. Pode usar o nosso esqueleto em vez disso.

`````
my_list = [1, 2, 4, 4, 1, 4, 2, 6, 2, 9]
#
# Write your code here.
#
print("The list with unique elements only:")
print(my_list)
`