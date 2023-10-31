## 4.5.1.22 LAB: Os módulos datetime e time

## Tempo estimado
15-45 minutos

## Nível de dificuldade
Fácil

## Objetivos
* melhorar as competências do aluno na formatação de data e hora;
* melhorar as competências do aluno na utilização do método `strftime` .

## Cenário
Durante este curso, aprendeu sobre o método `strftime` , que requer o conhecimento de diretivas para criar um formato. Chegou o momento de pôr em prática as diretivas conhecidas.

A propósito, terá a oportunidade de trabalhar com documentação, porque terá de encontrar diretivas que ainda não conhece.

**Aqui está a sua tarefa:**
Escreva um programa que crie um objeto `datetime` para 4 de novembro de 2020, 14:53:00. O objeto criado deve chamar o método `strftime` com o formato apropriado para exibir o seguinte resultado:

output esperado

```
2020/11/04 14:53:00
20/November/04 14:53:00 PM
Wed, 2020 Nov 04
Wednesday, 2020 November 04
Weekday: 3
Day of the year: 309
Week number of the year: 44
```

**Nota:** Cada linha de resultado deve ser criada chamando o método *strftime* com pelo menos uma diretiva no argumento do formato.

