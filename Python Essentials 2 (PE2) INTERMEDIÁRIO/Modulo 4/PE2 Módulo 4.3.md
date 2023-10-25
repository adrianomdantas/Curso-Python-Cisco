## 4.3.1.1 Trabalhar com arquivos reais

## Processamento de arquivos de texto

Nesta lição vamos preparar um arquivo de texto simples com algum conteúdo curto e simples.

Vamos mostrar-lhe algumas técnicas básicas que pode utilizar para **ler o conteúdo do arquivo**, a fim de o processar.

O processamento será muito simples - vai copiar o conteúdo do arquivo para a consola, e contar todos os carateres que o programa tenha lido.

Mas lembre-se - a nossa compreensão de um arquivo de texto é muito rigorosa. No nosso sentido, é um arquivo de texto simples - pode conter apenas texto, sem quaisquer decorações adicionais (formatação, tipos de letra diferentes, etc.).

É por isso que deve evitar criar o arquivo utilizando qualquer processador de texto avançado como MS Word, LibreOffice Writer, ou algo do género. Utilize os básicos que o seu sistema operativo oferece: Bloco de notas, vim, gedit, etc.

Se os seus arquivos de texto contiverem alguns carateres nacionais não abrangidos pelo padrão de carateres ASCII, poderá necessitar de um passo adicional. A sua invocação de função `open()` pode exigir um argumento que denote uma codificação de texto específica.

Por exemplo, se estiver a usar um SO Unix/Linux configurado para usar o UTF-8 como uma configuração de todo o sistema, a função `open()` pode ter o seguinte aspeto:

`stream = open('file.txt', 'rt', encoding='utf-8')`


onde o argumento de codificação tem de ser definido para um valor que é uma string que representa a codificação de texto adequada (UTF-8, aqui).

Consulte a documentação do seu SO para encontrar um nome codificador adequado ao seu ambiente.


**Nota**

Para os fins das nossas experiências com processamento de arquivos realizadas nesta secção, vamos utilizar um conjunto de arquivos pré-carregados (ou seja, arquivos `tzop.txt`, ou `text.txt` ) com os quais poderá trabalhar. Se desejar trabalhar com os seus próprios arquivos localmente na sua máquina, encorajamo-lo vivamente a fazê-lo, e a utilizar o IDLE (ou qualquer outro IDE que possa preferir) para realizar os seus próprios testes.

```
# Opening tzop.txt in read mode, returning it as a file object:
stream = open("tzop.txt", "rt", encoding = "utf-8")

print(stream.read()) # printing the content of the file
```

output

```
The Zen of Python
=================

::

    Beautiful is better than ugly.
    Explicit is better than implicit.
    Simple is better than complex.
    Complex is better than complicated.
    Flat is better than nested.
    Sparse is better than dense.
    Readability counts.
    Special cases aren't special enough to break the rules.
    Although practicality beats purity.
    Errors should never pass silently.
    Unless explicitly silenced.
    In the face of ambiguity, refuse the temptation to guess.
    There should be one-- and preferably only one --obvious way to do it.
    Although that way may not be obvious at first unless you're Dutch.
    Now is better than never.
    Although never is often better than *right* now.
    If the implementation is hard to explain, it's a bad idea.
    If the implementation is easy to explain, it may be a good idea.
    Namespaces are one honking great idea -- let's do more of those!



----------------
source: https://github.com/python/peps/blob/master/pep-0020.txt
```

## 4.3.1.2 Trabalhar com arquivos reais

## Processamento de arquivos de texto: continuação

A leitura do conteúdo de um arquivo de texto pode ser feita usando vários métodos diferentes - nenhum deles é melhor ou pior do que qualquer outro. Depende de si qual deles prefere e gosta.

Alguns deles serão por vezes mais práticos, e por vezes mais problemáticos. Seja flexível. Não tenha medo de mudar as suas preferências.

O mais básico destes métodos é o que é oferecido pela função `read()` , que foi capaz de ver em ação na lição anterior.

Se aplicada a um arquivo de texto, a função é capaz de:

* ler um número desejado de carateres (incluindo apenas um) do arquivo, e devolvê-los como uma string;
* ler todo o conteúdo do arquivo, e devolvê-lo como uma string;
* se não houver mais nada para ler (a cabeça de leitura virtual chega ao fim do arquivo), a função devolve uma string vazia.

Começaremos com a variante mais simples e utilizaremos um arquivo com o nome `text.txt`. O arquivo tem o seguinte conteúdo:
```
Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
text.txt
```

Vejamos agora o código no editor, e vamos analisá-lo.

```
from os import strerror

try:
    cnt = 0
    s = open('text.txt', "rt")
    ch = s.read(1)
    while ch != '':
        print(ch, end='')
        cnt += 1
        ch = s.read(1)
    s.close()
    print("\n\nCharacters in file:", cnt)
except IOError as e:
    print("I/O error occurred: ", strerror(e.errno))
```

A rotina é bastante simples:

* utilizar o mecanismo try-except e abrir o arquivo do nome pré-determinado (text.txt no nosso caso)
* tentar ler o primeiro caratere do arquivo (`ch = s.read(1)`)
* se for bem sucedido (isto é comprovado por um resultado positivo da verificação do estado `while` ), fazer output do caratere (note o argumento `end=` - é importante! Não se quer saltar para uma nova linha depois de cada caratere!);
* atualizar o contador (`cnt`), também;
* tentar ler o próximo caratere, e o processo repete-se.

## 4.3.1.3 Trabalhar com arquivos reais

## Processamento de arquivos de texto: continuação

Se tem a certeza absoluta de que o comprimento do arquivo é seguro e pode ler todo o arquivo para a memória de uma só vez, pode fazê-lo - a função `read()` , invocada sem quaisquer argumentos ou com um argumento que avalia `None`, vai fazer o trabalho por si.

Lembre-se - **a leitura de um arquivo de um terabyte usando este método pode corromper o seu sistema operativo.**

Não espere milagres - a memória do computador não é esticável.

Veja o código no editor. O que pensa disto?

```
from os import strerror

try:
    cnt = 0
    s = open('text.txt', "rt")
    content = s.read()
    for ch in content:
        print(ch, end='')
        cnt += 1
    s.close()
    print("\n\nCharacters in file:", cnt)
except IOError as e:
    print("I/O error occurred: ", strerr(e.errno))
```

Vamos analisá-lo:

* abra o arquivo como anteriormente;
* leia o seu conteúdo através de uma invocação da função `read()` ;
* em seguida, processe o texto, iterando através dele com um loop `for` , e atualizando o valor do contador a cada turno do loop;
  
O resultado será exatamente o mesmo que anteriormente.

## 4.3.1.4 Trabalhar com arquivos reais

## Processamento de arquivos de texto: readline()

Se quiser tratar o conteúdo do arquivo **como um conjunto de linhas** e não como um monte de carateres, o método `readline()` irá ajudá-lo com isso.

O método tenta **ler uma linha completa de texto do arquivo**, e devolve-a como uma string em caso de sucesso. Caso contrário, ele devolve uma string vazia.

Isto abre novas oportunidades - agora também se podem contar linhas facilmente, não apenas carateres.

Vamos fazer uso disso. Veja o código no editor.

```
from os import strerror

try:
    ccnt = lcnt = 0
    s = open('text.txt', 'rt')
    line = s.readline()
    while line != '':
        lcnt += 1
        for ch in line:
            print(ch, end='')
            ccnt += 1
        line = s.readline()
    s.close()
    print("\n\nCharacters in file:", ccnt)
    print("Lines in file:     ", lcnt)
except IOError as e:
    print("I/O error occurred:", strerror(e.errno))
```

Como se pode ver, a ideia geral é exatamente a mesma que nos dois exemplos anteriores.

## 4.3.1.5 Trabalhar com arquivos reais

## Processamento de arquivos de texto: readlines()

Outro método, que trata o arquivo de texto como um conjunto de linhas e não de carateres, é `readlines()`.

A classe `readlines()` , quando invocado sem argumentos, tenta **ler todo o conteúdo do arquivo, e devolve uma lista de strings, um elemento por linha de arquivo.**

Se não tiver a certeza se o tamanho do arquivo é suficientemente pequeno e não quiser testar o SO, pode convencer o método `readlines()` a ler não mais do que um número especificado de bytes ao mesmo tempo (o valor de retorno permanece o mesmo - é uma lista de uma string).

Sinta-se à vontade para experimentar o seguinte código de exemplo para compreender como o método `readlines()` funciona:

```
s = open("text.txt")
print(s.readlines(20))
print(s.readlines(20))
print(s.readlines(20))
print(s.readlines(20))
s.close()
```

**O tamanho máximo aceite do buffer de input é passado para o método como seu argumento.**

Pode esperar que `readlines()` pode processar o conteúdo de um arquivo de forma mais eficaz do que `readline()`, uma vez que pode precisar de ser invocado menos vezes.

Nota: quando não há nada a ler do arquivo, o método devolve uma lista vazia. Utilize-o para detetar o fim do arquivo.

Na medida do tamanho do buffer, é de esperar que o seu aumento possa melhorar o desempenho de input, mas não há nenhuma regra de ouro para isso - tente você mesmo encontrar os valores ótimos.

Veja o código no editor. Modificámo-lo para lhe mostrar como usar `readlines()`.

```
from os import strerror

try:
    ccnt = lcnt = 0
    s = open('text.txt', 'rt')
    lines = s.readlines(20)
    while len(lines) != 0:
        for line in lines:
            lcnt += 1
            for ch in line:
                print(ch, end='')
                ccnt += 1
        lines = s.readlines(10)
    s.close()
    print("\n\nCharacters in file:", ccnt)
    print("Lines in file:     ", lcnt)
except IOError as e:
    print("I/O error occurred:", strerror(e.errno))

```

Decidimos usar um buffer de 15 bytes. Não pense que se trata de uma recomendação.

Utilizámos esse valor para evitar a situação em que a primeira invocação `readlines()` consome o arquivo inteiro.

Queremos que o método seja forçado a trabalhar mais, e a demonstrar as suas capacidades.

Existem **dois nested loops no código:** o externo utiliza o resultado de `readlines()` para iterar através dele, enquanto que o interior imprime as linhas caratere a caratere.

## 4.3.1.6 Trabalhar com arquivos reais

## Processamento de arquivos de texto: continuação

O último exemplo que queremos apresentar mostra uma característica muito interessante do objeto devolvido pela função `open()` no modo de texto.

Achamos que pode surpreendê-lo - **o objeto é uma instância da classe iterável.**

Estranho? De modo algum. Utilizável? Sim, completamente.

O **protocolo de iteração definido para o objeto de arquivo** é muito simples - o seu método `__next__` **apenas devolve a próxima linha lida a partir do arquivo.**

Além disso, pode esperar que o objeto invoque automaticamente `close()` quando qualquer uma das leituras do arquivo chegar ao fim do arquivo.

Olhe para o editor e veja como o código se tornou agora simples e claro.

```
from os import strerror

try:
	ccnt = lcnt = 0
	for line in open('text.txt', 'rt'):
		lcnt += 1
		for ch in line:
			print(ch, end='')
			ccnt += 1
	print("\n\nCharacters in file:", ccnt)
	print("Lines in file:     ", lcnt)
except IOError as e:
	print("I/O error occurred: ", strerror(e.errno))
```

## 4.3.1.7 Trabalhar com arquivos reais

## Lidar com arquivos de texto: write()

Escrever arquivos de texto parece ser mais simples, pois de fato existe um método que pode ser utilizado 
para realizar tal tarefa.

O método é chamado `write()` e espera apenas um argumento - uma string que será transferida para um arquivo aberto (não esquecer - o modo aberto deve refletir a forma como os dados são transferidos - **escrever um arquivo aberto em modo de leitura não será bem sucedido).**

Nenhum caratere newline é adicionado ao argumento `write()`, pelo que terá de ser você próprio a adicioná-lo se quiser que o arquivo seja preenchido com um certo número de linhas.

O exemplo no editor mostra um código muito simples que cria um arquivo com o nome newtext.txt (nota: o modo aberto `w` assegura que **o arquivo será criado do zero**, mesmo que este exista e contenha dados) e depois coloca dez linhas no mesmo.

A string a ser gravada consiste na linha da palavra, seguida do número da linha. Decidimos escrever o conteúdo da string caratere a caratere (isto é feito pelo loop `for` interno) mas não é obrigado a fazê-lo desta forma.

Só queríamos mostrar-lhe que `write()` é capaz de operar em carateres individuais.

O código cria um arquivo preenchido com o seguinte texto:

output

```
line #1
line #2
line #3
line #4
line #5
line #6
line #7
line #8
line #9
line #10
```

Pode imprimir o conteúdo do arquivo para a consola?

```
from os import strerror

try:
	fo = open('newtext.txt', 'wt') # A new file (newtext.txt) is created.
	for i in range(10):
		s = "line #" + str(i+1) + "\n"
		for ch in s:
			fo.write(ch)
	fo.close()
except IOError as e:
	print("I/O error occurred: ", strerror(e.errno))
```

Encorajamo-lo a testar o comportamento do método `write()` localmente na sua máquina.

## 4.3.1.8 Trabalhar com arquivos reais

## Lidar com arquivos de texto: continuação

Veja o exemplo no editor. Modificámos o código anterior para escrever linhas inteiras no arquivo de texto.

```
from os import strerror

try:
    fo = open('newtext.txt', 'wt')
    for i in range(10):
        fo.write("line #" + str(i+1) + "\n")
    fo.close()
except IOError as e:
    print("I/O error occurred: ", strerror(e.errno))
```

O conteúdo do arquivo recentemente criado é o mesmo.

Nota: pode usar o mesmo método para escrever para o stream `stderr` , mas não tente abri-lo, pois está sempre aberto implicitamente.

Por exemplo, se quiser enviar uma string de mensagem para `stderr` para o distinguir do output normal de programa, pode ter este aspeto:

```
import sys
sys.stderr.write("Error message")
```


## 4.3.1.9 Trabalhar com arquivos reais

## O que é um bytearray?

Antes de começarmos a falar de arquivos binários, temos de lhe falar de uma das **classes especializadas que o Python utiliza para armazenar dados amorfos.**

**Dados amorfos são dados que não têm formato ou forma específica** - são apenas uma série de bytes.

Isto não significa que estes bytes não possam ter o seu próprio significado, ou não possam representar qualquer objeto útil, por exemplo, gráficos bitmap.

O aspeto mais importante disto é que no local onde temos contacto com os dados, não somos capazes, ou simplesmente não queremos, saber nada sobre isso.

Os dados amorfos não podem ser armazenados utilizando qualquer um dos meios anteriormente apresentados - eles não são strings nem listas.

Deve haver um recipiente especial capaz de tratar de tais dados.

O Python tem mais do que um desses recipientes - um deles é um **bytearray de nome de classe especializado** - como o nome sugere, é **um array contendo bytes (amorfos)**.

Se quiser ter um tal recipiente, por exemplo, para ler uma imagem bitmap e processá-la de qualquer forma, precisa de o criar explicitamente, utilizando um dos construtores disponíveis.

Dê uma vista de olhos:

`data = bytearray(10)`

Tal invocação cria um objeto bytearray capaz de armazenar dez bytes.

Nota: tal construtor **preenche todo o array com zeros.**

## 4.3.1.10 Trabalhar com arquivos reais

## Bytearrays: continuação

Os bytearrays assemelham-se a listas em muitos aspetos. Por exemplo, são **mutáveis**, são um assunto da função `len()` , e pode aceder a qualquer um dos seus elementos utilizando a indexação convencional.

Existe uma limitação importante - **não deve definir nenhum elemento de byte array com um valor que não seja um número inteiro** (violar esta regra causará uma exceção TypeError ) e **não lhe é permitido atribuir um valor que não venha do intervalo 0 a 255 inclusive** (a menos que queira provocar uma ValueError exceção).

Pode **tratar qualquer elemento do byte array como valores inteiros** - tal como no exemplo do editor.

Nota: utilizámos dois métodos para iterar os byte arrays, e fizemos uso da função `hex()` para ver os elementos impressos como valores hexadecimais.

``` 
data = bytearray(10)

for i in range(len(data)):
    data[i] = 10 - i

for b in data:
    print(hex(b))
```

Agora vamos mostrar-lhe como **escrever um byte array num arquivo binário** - binário, pois não queremos guardar a sua representação legível - queremos escrever uma cópia um-para-um do conteúdo da memória física, byte por byte.

## 4.3.1.11 Trabalhar com arquivos reais

## Bytearrays: continuação

Então, como escrevemos uma byte array para um arquivo binário?

Veja o código no editor. Vamos analisá-lo:

```
from os import strerror

data = bytearray(10)

for i in range(len(data)):
    data[i] = 10 + i

try:
    bf = open('file.bin', 'wb')
    bf.write(data)
    bf.close()
except IOError as e:
    print("I/O error occurred:", strerror(e.errno))

# Your code that reads bytes from the stream should go here.
```

* primeiro, inicializamos `bytearray` com valores subsequentes a partir de `10`; se quiser que o conteúdo do arquivo seja claramente legível, substitua `10` por algo como `ord('a')` - isto produzirá bytes contendo valores correspondentes à parte alfabética do código ASCII (não pense que fará do arquivo um arquivo de texto - ainda é binário, pois foi criado com uma bandeira `wb` );
* em seguida, criamos o arquivo usando a função `open()` - a única diferença em comparação com as variantes anteriores é o modo aberto que contém a bandeira `b` ;
* o método `write()` toma o seu argumento (`bytearray`) e envia-o (como um todo) para o arquivo;
* a stream é então fechada de forma rotineira.

O método `write()` devolve uma série de bytes escritos com sucesso.

Se os valores diferirem do comprimento dos argumentos do método, poderá anunciar alguns erros de escrita.

Neste caso, não fizemos uso do resultado - isto pode não ser apropriado em todos os casos.

Tente executar o código e analisar o conteúdo do arquivo de output recém-criado.

Vai utilizá-lo na próxima etapa.


## Como ler bytes de uma stream

A leitura a partir de um arquivo binário requer o uso de um nome de método especializado `readinto()`, uma vez que o método não cria um novo objeto de bytearray, mas preenche um previamente criado com os valores retirados do arquivo binário.

Nota:

* o método devolve o número de bytes lidos com sucesso;
* o método tenta preencher todo o espaço disponível dentro do seu argumento; se houver mais dados no arquivo do que espaço no argumento, a operação lida para antes do fim do arquivo; caso contrário, o resultado do método pode indicar que a bytearray só foi preenchida de forma fragmentada (o resultado mostrá-lo-á, também, e a parte do array que não está a ser utilizada pelo conteúdo recentemente lido permanece intacta)

Veja o código completo abaixo:
```
from os import strerror

data = bytearray(10)

try:
    bf = open('file.bin', 'rb')
    bf.readinto(data)
    bf.close()

    for b in data:
        print(hex(b), end=' ')
except IOError as e:
    print("I/O error occurred:", strerror(e.errno))
```

Vamos analisá-lo:

* primeiro, abrimos o arquivo (aquele que criou utilizando o código anterior) com o modo descrito como `rb`;
* em seguida, lemos seu conteúdo na bytearray chamada `data`, de tamanho dez bytes;
* finalmente, imprimimos o conteúdo da bytearray - são os mesmos que você esperava?
Execute o código e verifique se está a funcionar.

## 4.3.1.12 Trabalhar com arquivos reais

## Como ler bytes de uma stream

Uma forma alternativa de ler o conteúdo de um arquivo binário é oferecida pelo método denominado `read()`.

Invocado sem argumentos, tenta **ler todo o conteúdo do arquivo na memória**, tornando-os parte de um objeto recentemente criado da classe bytes.

Esta classe tem algumas semelhanças com `bytearray`, com exceção de uma diferença significativa - é **imutável**.

Felizmente, não existem obstáculos à criação de uma byte array tirando o seu valor inicial diretamente do objeto de bytes, tal como aqui:

```
from os import strerror

try:
    bf = open('file.bin', 'rb')
    data = bytearray(bf.read())
    bf.close()

    for b in data:
        print(hex(b), end=' ')

except IOError as e:
    print("I/O error occurred:", strerror(e.errno))
```

Tenha cuidado - **não utilize este tipo de leitura se não tiver a certeza de que o conteúdo do arquivo se adequa à memória disponível.**

```
from os import strerror

data = bytearray(10)

for i in range(len(data)):
    data[i] = 10 + i

try:
    bf = open('file.bin', 'wb')
    bf.write(data)
    bf.close()
except IOError as e:
    print("I/O error occurred:", strerror(e.errno))

# Your code that reads bytes from the stream should go here.
```

## 4.3.1.13 Trabalhar com arquivos reais

## Como ler bytes de uma stream: continuação

Se o método `read()` é invocado com um argumento, **especifica o número máximo de bytes a serem lidos.**

O método tenta ler o número desejado de bytes do arquivo, e o comprimento do objeto devolvido pode ser utilizado para determinar o número de bytes efetivamente lidos.

Pode usar o método tal como aqui:
```
try:
    bf = open('file.bin', 'rb')
    data = bytearray(bf.read(5))
    bf.close()

    for b in data:
        print(hex(b), end=' ')

except IOError as e:
    print("I/O error occurred:", strerror(e.errno))
```

Nota: os primeiros cinco bytes do arquivo foram lidos pelo código - os cinco seguintes ainda estão à espera de ser processados.

```
from os import strerror

data = bytearray(10)

for i in range(len(data)):
    data[i] = 10 + i

try:
    bf = open('file.bin', 'wb')
    bf.write(data)
    bf.close()
except IOError as e:
    print("I/O error occurred:", strerror(e.errno))

# Your code that reads bytes from the stream should go here.

```

## 4.3.1.14 Trabalhar com arquivos reais

## Cópia de arquivos - uma ferramenta simples e funcional

Agora vai amalgamar todos estes novos conhecimentos, adicionar-lhe alguns elementos novos, e utilizá-los para escrever um código real que seja capaz de copiar efetivamente o conteúdo de um arquivo.

Claro que o objetivo não é fazer um melhor substituto para comandos como copy (MS Windows) ou cp (Unix/Linux), mas ver uma forma possível de criar uma ferramenta de trabalho, mesmo que ninguém a queira utilizar.

Veja o código no editor. Vamos analisá-lo:

```
from os import strerror

srcname = input("Enter the source file name: ")
try:
    src = open(srcname, 'rb')
except IOError as e:
    print("Cannot open the source file: ", strerror(e.errno))
    exit(e.errno)	

dstname = input("Enter the destination file name: ")
try:
    dst = open(dstname, 'wb')
except Exception as e:
    print("Cannot create the destination file: ", strerror(e.errno))
    src.close()
    exit(e.errno)	

buffer = bytearray(65536)
total  = 0
try:
    readin = src.readinto(buffer)
    while readin > 0:
        written = dst.write(buffer[:readin])
        total += written
        readin = src.readinto(buffer)
except IOError as e:
    print("Cannot create the destination file: ", strerror(e.errno))
    exit(e.errno)	
    
print(total,'byte(s) succesfully written')
src.close()
dst.close()

```

* linhas 3 a 8: pedir ao utilizador o nome do arquivo a copiar, e tentar abri-lo para ler; terminar a execução do programa se a abertura falhar; nota: utilizar a função `exit()` para parar a execução do programa e para passar o código de conclusão para o SO; qualquer código de conclusão que não 0 diz que o programa encontrou alguns problemas; use o valor `errno` para especificar a natureza do problema;
* linhas 10 a 16: repetir quase a mesma ação, mas desta vez para o arquivo de output;
* linha 18: preparar um pedaço de memória para transferir dados do source file para o arquivo alvo; essa área de transferência é muitas vezes chamada de buffer, daí o nome da variável; o tamanho do buffer é arbitrário - neste caso, decidimos usar 64 kilobytes; tecnicamente, um buffer maior é mais rápido a copiar itens, pois um buffer maior significa menos operações I/O; na verdade, há sempre um limite, cujo cruzamento não traz mais melhorias; teste-o você mesmo se quiser.
* linha 19: contar os bytes copiados - este é o contador e o seu valor inicial;
* linha 21: tentar preencher o buffer pela primeira vez;
* linha 22: desde que se obtenha um número não nulo de bytes, repetir as mesmas ações;
* linha 23: escrever o conteúdo do buffer no arquivo de output (nota: utilizámos uma slice para limitar o número de bytes a escrever, uma vez que `write()` prefere sempre escrever todo o buffer)
* linha 24: atualizar o contador;
* linha 25: ler o próximo pedaço de arquivo;
* linhas 30 a 32: alguma limpeza final - o trabalho está feito.

## 4.3.1.15 LAB: Histograma de frequência de carateres

## 4.3.1.16 LAB: Histograma de frequência de carateres ordenados

## 4.3.1.17 LAB: Avaliar os resultados dos estudantes

## 4.3.1.18 RESUMO DA SECÇÃO

## Key takeaways

1. Para ler o conteúdo de um arquivo, podem ser utilizados os seguintes métodos de stream:

* `read(number)` — lê os carateres/bytes `number` do arquivo e devolve-os como uma string; é capaz de ler o arquivo inteiro de uma só vez;
* `readline()` — lê uma única linha do arquivo de texto;
* `readlines(number)` — lê as linhas `number` do arquivo de texto; é capaz de ler todas as linhas ao mesmo tempo;
* `readinto(bytearray)` — lê os bytes do arquivo e preenche o bytearray com eles;

2. Para escrever novos conteúdos num arquivo, podem ser utilizados os seguintes métodos de stream:

* `write(string)` — escreve um `string` para um arquivo de texto;
* `write(bytearray)` — escreve todos os bytes de `bytearray` para um arquivo;

3. Os loops `open()` devolve um objeto iterável que pode ser utilizado para iterar através de todas as linhas do arquivo dentro de um loop `for` . Por exemplo:

```
for line in open("file", "rt"):
    print(line, end='')
```

O código copia o conteúdo do arquivo para a consola, linha a linha. **Nota**: o stream fecha-se **automaticamente** quando chega ao fim do arquivo.


**Exercício 1**

O que esperamos do método `readlines()` quando o stream está associado a um arquivo vazio?

Verifique

Uma lista vazia (uma lista de comprimento zero).



**Exercício 2**

O que se pretende fazer com o seguinte código?
```
for line in open("file", "rt"):
    for char in line:
        if char.lower() not in "aeiouy ":
            print(char, end='')
```

Verifique

Copia o conteúdo do arquivo para a consola, ignorando todas as vogais.



**Exercício 3**

Vai processar um bitmap armazenado num arquivo com o nome `image.png`, e deseja ler o seu conteúdo como um todo numa variável de bytearray chamada `image`. Adicione uma linha ao seguinte código para atingir este objetivo.
```
try:
    stream = open("image.png", "rb")
    # Insert a line here.
    stream.close()
except IOError:
    print("failed")
else:
    print("success")
```

Verifique

`image = bytearray(stream.read())`
