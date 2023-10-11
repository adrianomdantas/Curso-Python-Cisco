## 2.5.1.6 LAB: Melhorar a cifra César

## Tempo estimado
30-90 minutos

## Nível de dificuldade
Difícil

## Pré-requisitos
Módulo 1.11.1.1, Módulo 1.11.1.2

## Objetivos
* melhorar as habilidades do aluno a operar com strings;
* converter carateres em código ASCII e vice-versa.

## Cenário
Já está familiarizado com a cifra César, e é por isso que queremos que melhore o código que lhe mostrámos recentemente.

A cifra original de César desloca cada caratere por um: a torna-se b, z torna-se a, e assim por diante. Vamos torná-la um pouco mais difícil, e permitir que o valor deslocado venha do intervalo 1..25 inclusive.

Além disso, deixe que o código preserve as letras (letras minúsculas permanecerão minúsculas) e todos os carateres não alfabéticos devem permanecer intocados.

A sua tarefa é escrever um programa que:

* pede ao utilizar uma linha de texto para encriptar;
* pede ao utilizador um valor de deslocamento (um número inteiro no intervalo 1..25 - nota: deve forçar o utilizador a inserir um valor de deslocamento válido (não desista e não deixe que maus dados o enganem!);
* imprime o texto codificado.

Teste o seu código utilizando os dados por nós fornecidos.

## Dados de teste
Input de amostra:

```
abcxyzABCxyz 123
2
```

Exemplo de output:

`cdezabCDEzab 123`

Input de amostra:

```
The die is cast
25
```

Exemplo de output:

`Sgd chd hr bzrs`