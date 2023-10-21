## 3.4.1.13 Dias da semana

## Tempo estimado
30-60 minutos

## Nível de dificuldade
Fácil/Médio

## Objetivos
* melhorar as competências do aluno na definição das classes a partir do zero;
* definir e utilizar variáveis de instância;
* definir e utilizar métodos.

## Cenário
A sua tarefa é implementar uma classe chamada Weeker. Sim, os seus olhos não o enganam - este nome vem do facto de que os objetos dessa classe serão capazes de armazenar e manipular dias de uma semana.

O construtor de classe aceita um argumento - uma string. A string representa o nome do dia da semana e os únicos valores aceitáveis devem vir do seguinte conjunto:

`Mon Thu Wed Thu Fri Sat Sun`

Invocar o construtor com um argumento de fora deste conjunto deveria levantar a exceção WeekDayError (defina-a você mesmo; não se preocupe, em breve falaremos sobre a natureza objetiva das exceções). A classe deve fornecer as seguintes facilidades:

* os objetos da classe devem ser "imprimíveis", ou seja, devem ser capazes de se converter implicitamente em strings da mesma forma que os argumentos do construtor;
* a classe deve ser equipada com métodos de um parâmetro chamado `add_days(n)` e `subtract_days(n)`, sendo **n** um número inteiro e atualizando o dia da semana armazenado dentro do objeto de forma a refletir a mudança de data pelo número de dias indicado, para a frente ou para trás.
* todas as propriedades do objeto devem ser privadas;

Complete o modelo que fornecemos no editor e execute o seu código e verifique se o seu output tem o mesmo aspeto que o nosso.

```
class WeekDayError(Exception):
    pass
	

class Weeker:
    #
    # Write code here
    #

    def __init__(self, day):
        #
        # Write code here
        #

    def __str__(self):
        #
        # Write code here
        #

    def add_days(self, n):
        #
        # Write code here
        #

    def subtract_days(self, n):
        #
        # Write code here
        #


try:
    weekday = Weeker('Mon')
    print(weekday)
    weekday.add_days(15)
    print(weekday)
    weekday.subtract_days(23)
    print(weekday)
    weekday = Weeker('Monday')
except WeekDayError:
    print("Sorry, I can't serve your request.")

```

## Output esperado

```
Mon
Thu
Sun
Sorry, I can't serve your request.
```