## 4.3.1.16 LAB: Histograma de frequência de carateres ordenados

## Tempo estimado
15-30 minutos

## Nível de dificuldade
Médio

## Pré-requisitos
4.3.1.15

## Objetivos
* melhorar as capacidades do aluno em operar com ficheiros (leitura/escrita)
* utilizar lambdas para alterar a ordem de classificação.

## Cenário
O código anterior precisa de ser melhorado. Está tudo bem, mas tem de ser melhor.

A sua tarefa é fazer algumas alterações, que geram os seguintes resultados:

* o histograma de output será ordenado com base na frequência dos carateres (o contador maior deve ser apresentado primeiro)
* o histograma deve ser enviado para um ficheiro com o mesmo nome que o de input, mas com o sufixo '.hist' (deve ser concatenado com o nome original)
Assumindo que o ficheiro de input contém apenas uma linha preenchida:

`cBabAa`
samplefile.txt

o output esperado deve ter a seguinte aparência:

output

```
a -> 3
b -> 2
c -> 1
```

**Dica:** Use um `lambda` para alterar a ordem de classificação.

