## 4.3.1.17 LAB: Avaliar os resultados dos estudantes

## Tempo estimado
30-90 minutos

# Nível de dificuldade
Médio

# Objetivos
* melhorar as competências do aluno em operar com ficheiros (leitura)
* aperfeiçoar as capacidades do aluno na definição e utilização de exceções e dicionários auto-definidos.

# Cenário
O Prof. Jekyll realiza aulas com os estudantes e faz regularmente anotações num ficheiro de texto. Cada linha do ficheiro contém três elementos: o primeiro nome do estudante, o último nome do estudante, e o número de pontos que o estudante recebeu durante certas aulas.

Os elementos são separados por espaços em branco. Cada estudante pode aparecer mais de uma vez no ficheiro do Prof. Jekyll.

O ficheiro pode ter a seguinte aparência:

```
John	Smith	5
Anna	Boleyn	4.5
John	Smith	2
Anna	Boleyn	11
Andrew	Cox	1.5
```
samplefile.txt


A sua tarefa é escrever um programa que:

* pergunta ao utilizador o nome do ficheiro do Prof. Jekyll;
* lê o conteúdo do ficheiro e conta a soma dos pontos recebidos por cada estudante;
* imprime um relatório simples (mas ordenado), tal como este:

output

```
Andrew Cox 	 1.5
Anna Boleyn 	 15.5
John Smith 	 7.0
```

Nota:

* o seu programa deve ser totalmente protegido contra todas as falhas possíveis: a inexistência do ficheiro, o vazio do ficheiro, ou qualquer falha nos dados introduzidos; o encontro de qualquer erro de dados deve causar a terminação imediata do programa, e o erro deve ser apresentado ao utilizador;
* implemente e utilize a sua própria hierarquia de exceções - apresentámo-la no editor; a segunda exceção deve ser levantada quando uma linha má é detetada, e a terceira quando o source file existe mas está vazio.

**Dica:** Utilize um dicionário para armazenar os dados dos estudantes.