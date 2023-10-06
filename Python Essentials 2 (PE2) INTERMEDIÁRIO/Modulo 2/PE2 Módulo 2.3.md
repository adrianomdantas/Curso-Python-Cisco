## 2.3.1.1 Métodos de String

## Os loops capitalize() .

Vamos passar por alguns métodos padrão de string Python. Vamos atravessá-los por ordem alfabética - para ser honesto, qualquer ordem tem tantas desvantagens como vantagens, pelo que a escolha pode também ser aleatória.

O método `capitalize()` faz exatamente o que diz - **cria uma nova string cheia de carateres retirados da source string**, mas tenta modificá-los da seguinte forma:

* **se o primeiro caratere dentro da string for uma letra** (nota: o primeiro caratere é um elemento com um index igual a 0, não apenas o primeiro caratere visível), **será convertido para maiúsculas**;
* **todas as letras restantes da string serão convertidas em minúsculas.**

Não se esqueça:

* a string original (da qual o método é invocado) não é alterada de forma alguma (a imutabilidade de uma string deve ser obedecida sem reservas)
* a string modificada (capitalizada neste caso) é devolvida como resultado - se não a utilizar de qualquer forma (atribuí-la a uma variável, ou passá-la a uma função/método) ela desaparecerá sem deixar rasto.

Nota: os métodos não têm de ser invocados apenas de dentro das variáveis. Podem ser invocados diretamente de dentro de literais de string. Vamos utilizar regularmente essa convenção - simplificará os exemplos, uma vez que os aspetos mais importantes não desaparecerão entre as tarefas desnecessárias.

Veja o exemplo no editor. Execute-o.

```
# Demonstrating the capitalize() method:
print('aBcD'.capitalize())
```

Isto é o que ele imprime:

output

`Abcd`


Experimente alguns exemplos mais avançados e teste o seu output:

```
print("Alpha".capitalize())
print('ALPHA'.capitalize())
print(' Alpha'.capitalize())
print('123'.capitalize())
print("αβγδ".capitalize())
```

## 2.3.1.2 Métodos de String

## 