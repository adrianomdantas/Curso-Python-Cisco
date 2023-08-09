## 3.2.1.3 LAB: Essenciais do loop while - Adivinhe o número secreto

## Tempo estimado
15 minutos

## Nível de dificuldade
Fácil

## Objetivos
Familiarizar o aluno a:

* a utilização do loop while ;
* refletir situações da vida real em código informático.

## Cenário
Um mágico júnior escolheu um número secreto. Ele escondeu-o numa variável chamada `secret_number`. Ele quer que todos os que executam o seu programa joguem o jogo do Adivinhe o número secreto, e adivinhe que número escolheu para eles. Aqueles que não adivinharem o número ficarão presos num loop infinito para sempre! Infelizmente, ele não sabe como completar o código.

A sua tarefa é ajudar o mágico a completar o código no editor, de modo a que o código:

* peça ao utilizador para introduzir um número inteiro;
* utilize um loop while ;
* verifique se o número introduzido pelo utilizador é o mesmo que o número escolhido pelo mágico. Se o número escolhido pelo utilizador for diferente do número secreto do mágico, o utilizador deve ver a mensagem `"Ha ha! You're stuck in my loop!"` e ser solicitado a introduzir novamente um número. Se o número introduzido pelo utilizador corresponder ao número escolhido pelo mágico, o número deve ser impresso no ecrã, e o mágico deve dizer as seguintes palavras: `"Well done, muggle! You are free now."`
The magician is counting on you! Não o dececione.

```
secret_number = 777

print(
"""
+================================+
| Welcome to my game, muggle! |
| Enter an integer number |
| and guess what number I've |
| picked for you. |
| So, what is the secret number? |
+================================+
""")

```

## INFORMAÇÃO EXTRA

A propósito, olha para a função `print()` . A forma como a utilizámos aqui chama-se impressão multi-linha. Pode usar aspas triplas para imprimir strings em várias linhas a fim de tornar o texto mais fácil de ler, ou criar um desenho especial baseado em texto. Experimente-o.


 
