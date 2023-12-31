## 3.2.1.11 LAB: A declaração continue - o Pretty Vowel Eater

## Tempo estimado
5-15 minutos

## Nível de dificuldade
Fácil

## Objetivos
Familiarizar o aluno a:

* a utilização do loop `continue` em loops;
* modificar e atualizar o código existente;
* refletir situações da vida real em código informático.

## Cenário

A sua tarefa aqui é ainda mais especial do que antes: deve redesenhar o comedor de vogais (feio) do laboratório anterior (3.1.2.10) e criar um comedor de vogais (bonito) melhor e mais aperfeiçoado! Escreva um programa que use:

* um loop `for` ;
* o conceito de execução condicional (if-elif-else)
* a declaração `continue` .

O seu programa deve:

* pedir ao utilizador para introduzir uma palavra;
* usar `user_word = user_word.upper()` para converter a palavra introduzida pelo utilizador em maiúsculas; falaremos sobre os chamados **métodos de strings** e o método `upper()` muito em breve - não se preocupe;
* usar execução condicional e a declaração `continue` para “comer” as seguintes vogais A, E, I, O, U da palavra introduzida;
* atribuir as letras não comidas à variável `word_without_vowels` e imprimir a variável no ecrã.
  
Veja o código no editor. Criámos `word_without_vowels` e atribuimos-lhe uma string vazia. Utilize a operação de concatenação para pedir ao Python que combine as letras selecionadas numa string mais longa durante os loops subsequentes, e atribua-a à variável word_without_vowels .

```
word_without_vowels = ""

# Prompt the user to enter a word
# and assign it to the user_word variable.


for letter in user_word:
    # Complete the body of the loop.

# Print the word assigned to word_without_vowels.
```

Teste o seu programa com os dados que lhe fornecemos.


Dados de teste
Input de amostra: `Gregory`

Output esperado:

`GRGRY`

Input de amostra: `abstemious`

Output esperado:

`BSTMS`

Input de amostra: `IOUEA`

Output esperado:

 
