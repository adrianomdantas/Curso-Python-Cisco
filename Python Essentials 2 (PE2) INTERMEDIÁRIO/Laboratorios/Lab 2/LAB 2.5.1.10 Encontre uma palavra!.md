## 2.5.1.10 LAB: Encontre uma palavra!

## Tempo estimado
30-45 minutos

## Nível de dificuldade
Médio

## Objetivos
* melhorar as habilidades do aluno a operar com strings;
* utilizar o método `find()` para pesquisar strings.

## Cenário
Vamos jogar um jogo. Dar-lhe-emos duas strings: uma sendo uma palavra (por exemplo, “dog”) e a segunda sendo uma combinação de quaisquer carateres.

A sua tarefa é a de escrever um programa que responda à seguinte questão: **os carateres que compõem a primeira string estão escondidos dentro da segunda string?**

Por exemplo:

* se a segunda string for dada como “vcxzxduybfdsobywuefgas”, a resposta é yes;
* se a segunda string for “vcxzxdcybfdstbywuefsas”, a resposta é no (visto não haver as letras “d”, “o”, ou “g”, nesta ordem)

Dicas:

* deve utilizar as variantes de dois argumentos das funções pos() dentro do seu código;
não se preocupe com a sensibilidade a maiúsculas e minúsculas.
* Teste o seu código utilizando os dados por nós fornecidos.

## Dados de teste
Input de amostra:

```
donor
Nabucodonosor
```

Exemplo de output:

`Yes`


Input de amostra:

```
donut
Nabucodonosor
```
Exemplo de output:

`No`
