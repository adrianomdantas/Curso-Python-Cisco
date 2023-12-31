## 4.4.1.1 O módulo os

## Introdução ao módulo os .

Nesta secção, aprenderá sobre um módulo chamado os, que lhe permite **interagir com o sistema operativo utilizando o Python.**

Este fornece funções que estão disponíveis em sistemas Unix e/ou Windows. Se estiver familiarizado com a linha de comandos, verá que algumas funções dão os mesmos resultados que os comandos disponíveis nos sistemas operativos.

Um bom exemplo disto é a função `mkdir` , que permite criar uma diretoria tal como o comando mkdir em Unix e Windows. Se não conhecer este comando, não se preocupe.

Em breve terá a oportunidade de aprender as funções do módulo os, para executar operações em ficheiros e diretorias juntamente com os comandos correspondentes.

Além das operações de ficheiro e diretoria, o módulo os permite-lhe:

* obter informações sobre o sistema operativo;
* gerir processos;
* operar em streams I/O utilizando file descriptors (descritores de ficheiro).


Dentro de momentos, verá como obter informações básicas sobre o seu sistema operativo, embora a gestão de processos e o trabalho com os file descriptors não sejam discutidos aqui, visto serem tópicos mais avançados que requerem conhecimento dos mecanismos do sistema operativo.

Preparado?

## 4.4.1.2 O módulo os

## Obter informações sobre o sistema operativo

Antes de criar a sua primeira estrutura de diretoria, verá como pode obter informações sobre o sistema operativo atual. Isto é realmente fácil porque o módulo os fornece uma função chamada uname, que devolve um objeto contendo os seguintes atributos:

* **systemname** — armazena o nome do sistema operativo;
* **nodename** — armazena o nome da máquina na network;
* **release** — armazena o lançamento do sistema operativo;
* **version** — armazena a versão do sistema operativo;
* **machine** — armazena o identificador de hardware, por exemplo, x86_64.

Vejamos como é na prática:

```
import os
print(os.uname())
```

Resultado:

output
```
posix.uname_result(sysname='Linux', nodename='192d19f04766', release='4.4.0-164-generic', version='#192-Ubuntu SMP Fri Sep 13 12:02:50 UTC 2019', machine='x86_64')
```

Como pode ver, a função *uname* devolve um objeto contendo informações sobre o sistema operativo. O código acima foi lançado em Ubuntu 16.04.6 LTS, por isso não se surpreenda se obtiver um resultado diferente, porque depende do seu sistema operativo.

Infelizmente, a função *uname* só funciona em alguns sistemas Unix. Se utilizar o Windows, pode usar a função *uname* no módulo platform, que devolve um resultado semelhante.

O módulo os permite-lhe distinguir rapidamente o sistema operativo utilizando o atributo name, que suporta um dos seguintes nomes:

* **posix** — obterá este nome se utilizar Unix;
* **nt** — obterá este nome se utilizar o Windows;
* **java** — obterá este nome se o seu código estiver escrito em Jython.

Para o Ubuntu 16.04.6 LTS, o atributo name devolve o nome posix:
```
import os
print(os.name)
```

Resultado:

output

`posix`


**NOTA**: Em sistemas Unix, existe um comando chamado uname que devolve as mesmas informações (se o executar com a opção -a) que a função uname.

## 4.4.1.3 O módulo os

## Criar diretorias em Python

O módulo os fornece uma função chamada *mkdir*, que, tal como o comando mkdir em Unix e Windows, permite criar uma diretoria. A função *mkdir* requer um caminho, que pode ser relativo ou absoluto. Recordemos como são ambos os caminhos na prática:

* **my_first_directory** — este é um caminho relativo que irá criar a diretoria *my_first_directory* na diretoria de trabalho atual;
* **./my_first_directory** — este é um caminho relativo que aponta explicitamente para a diretoria de trabalho atual. Tem o mesmo efeito que o caminho acima;
* **../my_first_directory** — este é um caminho relativo que criará a diretoria *my_first_directory* na diretoria pai da diretoria de trabalho atual;
* **/python/my_first_directory** — este é o caminho absoluto que irá criar a diretoria *my_first_directory*, que por sua vez está na diretoria *Python* na diretoria de raiz.

Veja o código no editor. Este mostra um exemplo de como criar a diretoria *my_first_directory* usando um caminho relativo. Esta é a variante mais simples do caminho relativo, que consiste em passar apenas o nome da diretoria.

```
import os

os.mkdir("my_first_directory")
print(os.listdir())
```

Se testar o seu código aqui, ele produzirá a diretoria recém-criada `['my_first_directory']` (e todo o conteúdo do catálogo de trabalho atual).

A função *mkdir* cria uma diretoria no caminho especificado. Note que a execução do programa duas vezes levantará um *FileExistsError*.

Isto significa que não podemos criar uma diretoria se ela já existir. Para além do argumento path, a função *mkdir* pode opcionalmente tomar o argumento *mode*, que especifica as permissões de diretoria. No entanto, em alguns sistemas, o argumento mode é ignorado.

Para alterar as permissões de diretoria, recomendamos a função *chmod*, que funciona de forma semelhante ao comando *chmod* em sistemas Unix. Pode encontrar mais informações sobre o assunto na documentação.

No exemplo acima, outra função fornecida pelo módulo os, chamada *listdir*, é utilizada. A função *listdir* devolve uma lista contendo os nomes dos ficheiros e diretorias que se encontram no caminho passado como um argumento.

Se nenhum argumento lhe for passado, será utilizada a diretoria de trabalho atual (como no exemplo acima). É importante que o resultado da função *listdir* omita as entradas '.' e '..', que são exibidas, por exemplo, ao usar o comando ls -a em sistemas Unix.

**NOTA**: No Windows e no Unix, há um comando chamado *mkdir*, que requer uma diretoria path. O equivalente ao código acima que cria a diretoria *my_first_directory* é o comando *mkdir my_first_directory*.

## 4.4.1.4 O módulo os

## Criação de diretoria recursiva

A função `mkdir` é muito útil, mas e se precisar de criar outra diretoria na diretoria que acabou de criar? Obviamente, pode ir à diretoria criada e criar outra diretoria dentro dela, mas felizmente o módulo os fornece uma função chamada `makedirs`, o que torna esta tarefa mais fácil.

A função *makedirs* permite a criação de diretoria recursiva, o que significa que todas as diretorias no caminho serão criadas. Vamos olhar para o código no editor e ver como ele é na prática.

O código deve produzir o seguinte resultado:

output

`['my_second_directory']`

O código cria duas diretorias. A primeira delas é criada na diretoria de trabalho atual, enquanto a segunda é criada na diretoria *my_first_directory*.

```
import os

os.makedirs("my_first_directory/my_second_directory")
os.chdir("my_first_directory")
print(os.listdir())
```

Não tem de ir à diretoria *my_first_directory* para criar a diretoria *my_second_directory*, porque a função *makedirs* faz isto por si. No exemplo acima, vamos à diretoria *my_first_directory* para mostrar que o comando *makedirs* cria a subdiretoria *my_second_directory*.

Para se mover entre diretorias, pode usar uma função chamada *chdir*, que altera a diretoria de trabalho atual para o caminho especificado. Como argumento, toma qualquer caminho relativo ou absoluto. No nosso exemplo, passámos-lhe o nome da primeira diretoria.

**NOTA**: O equivalente à função makedirs nos sistemas Unix é o comando mkdir com o sinalizador -p, enquanto no Windows é simplesmente o comando mkdir com o caminho:

* Sistemas semelhantes a Unix:

`mkdir -p my_first_directory/my_second_directory`

* Windows:

`mkdir my_first_directory/my_second_directory`

## 4.4.1.5 O módulo os

## Onde estou agora?

Já sabe como criar diretorios e como se mover entre eles. Pos vezes, quando se tem uma estrutura de diretorias muito grande por onde navegar, pode não se saber em que diretoria se está atualmente a trabalhar.

Como provavelmente adivinhou, o módulo *os* fornece uma função que devolve informação sobre o diretorio de trabalho atual. É chamada `getcwd`. Olhe para o código no editor para ver como a utilizar na prática.

```
import os

os.makedirs("my_first_directory/my_second_directory")
os.chdir("my_first_directory")
print(os.getcwd())
os.chdir("my_second_directory")
print(os.getcwd())
```

Resultado:

output

```
.../my_first_directory
.../my_first_directory/my_second_directory
```

No exemplo, criamos o diretorio *my_first_directory* e o diretorio *my_second_directory* dentro desta. Na passo seguinte, alteramos a diretoria de trabalho atual para a diretoria my_first_directory, e depois exibimos a diretoria de trabalho atual (primeira linha do resultado).

Em seguida, vamos para a diretoria my_second_directory e exibimos novamente a diretoria de trabalho atual (segunda linha do resultado). Como pode ver, a função getcwd devolve o caminho absoluto para as diretorias.

**NOTA**: Em sistemas semelhantes a Unix, o equivalente à função *getcwd* é o comando *pwd*, que imprime o nome do diretorio de trabalho atual.

## 4.4.1.6 O módulo os

## Eliminar diretorias em Python

O módulo os também permite eliminar diretorias. Dá-lhe a opção de eliminar uma única diretoria ou uma diretoria com as suas subdiretorias. Para eliminar uma única diretoria, pode-se utilizar uma função chamada `rmdir`, que toma o caminho como seu argumento. Veja o código no editor.

```
import os

os.mkdir("my_first_directory")
print(os.listdir())
os.rmdir("my_first_directory")
print(os.listdir())
```

O exemplo acima é realmente simples. Primeiro, a diretoria *my_first_directory* é criada e, em seguida, é removida utilizando-se a função *rmdir*. A função *listdir* é usada como prova de que a diretoria foi removida com sucesso. Neste caso, devolve uma lista vazia. Ao eliminar uma diretoria, certifique-se de que esta existe e está vazio, caso contrário será levantada uma exceção.

Para remover uma diretoria e as suas subdiretorias, pode utilizar a função `removedirs` , o que requer que se especifique um caminho contendo todas as diretorias que devem ser removidos:

```    
import os

os.makedirs("my_first_directory/my_second_directory")
os.removedirs("my_first_directory/my_second_directory")
print(os.listdir())
```

Tal como com a função rmdir, se uma das diretorias não existir ou não estiver vazia, será levantada uma exceção.

**NOTA**: No Windows e no Unix existe um comando chamado rmdir, que, tal como a função rmdir, remove diretorias. Além disso, ambos os sistemas têm comandos para eliminar uma diretoria e o seu conteúdo. No Unix, este é o comando rm com o sinalizador -r.

## 4.4.1.7 O módulo os

## A função system()

Todas as funções apresentadas nesta parte do curso podem ser substituídas por uma função chamada *system*, que executa um comando que lhe é passado como uma string.

A função `system` está disponível tanto no Windows como no Unix. Dependendo do sistema, ela devolve um resultado diferente.

No Windows, devolve o valor retornado pela shell após executar o comando dado, enquanto que no Unix devolve o estado de exit do processo.

Vamos olhar para o código no editor e ver como ele é na prática.

```
import os

returned_value = os.system("mkdir my_first_directory")
print(returned_value)
```

Resultado:

output

`0`


O exemplo acima funcionará tanto no Windows como no Unix. No nosso caso, recebemos o exit status 0, o que indica sucesso em sistemas Unix.

Isto significa que a diretoria *my_first_directory* foi criada. Como parte do exercício, tente listar o conteúdo da diretoria onde criou a diretoria *my_first_directory*.

## 4.4.1.8 O módulo os: LAB

## 4.4.1.9 RESUMO DA SECÇÃO

## Key takeaways

1. A função `uname` devolve um objeto que contém informação sobre o sistema operativo atual. O objeto tem os seguintes atributos:

* systemname (armazena o nome do sistema operativo)
* nodename (armazena o nome da máquina na rede)
* release (armazena a versão do sistema operativo)
* version (armazena a versão do sistema operativo)
* machine (armazena o identificador de hardware, por exemplo x86_64.)

2. O atributo name disponível no módulo `os` permite distinguir o sistema operativo. Devolve um dos três valores seguintes:

* posix (receberá este nome se usar Unix)
* nt (receberá este nome se usar o Windows)
* java (receberá este nome se o seu código estiver escrito em algo como Jython)

3. Os loops `mkdir` cria uma diretoria no caminho percorrido como seu argumento. O caminho pode ser relativo ou absoluto, por exemplo

```
import os

os.mkdir("hello") # the relative path
os.mkdir("/home/python/hello") # the absolute path
```

**Nota**: Se a diretoria existir, uma exceção `FileExistsError` será lançada. Além da função `mkdir` , o módulo `os` fornece a função `makedirs` , que permite criar recursivamente todas as diretorias num caminho.

4. O resultado da função `listdir()` é uma lista contendo os nomes dos ficheiros e diretorias que se encontram no caminho percorrido como seu argumento.

É importante lembrar que a função `listdir` omite as entradas '.' e '..', que são exibidas, por exemplo, quando se utiliza o comando `ls -a` em sistemas Unix. Se o caminho não for passado, o resultado será devolvido para a diretoria de trabalho atual.

5. Para se deslocar entre diretorias, pode usar uma função chamada `chdir()`, que altera a diretoria de trabalho atual para o caminho especificado. Como seu argumento, toma qualquer caminho relativo ou absoluto.

Se quiser descobrir qual é a diretoria de trabalho atual, pode utilizar a função `getcwd()` , que lhe devolve o caminho.

6. Para remover uma diretoria, pode utilizar a função `rmdir()` , mas, para remover uma diretoria e as suas subdiretorias, utilize a função `removedirs()` .

7. Tanto no Unix como no Windows, pode usar a função do sistema, que executa um comando passado a ele como uma string, por exemplo:
```
import os

returned_value = os.system("mkdir hello")
```

A função do sistema no Windows devolve o valor devolvido pela shell após executar o comando dado, enquanto que no Unix devolve o estado de saída do processo.


**Exercício 1**

Qual é o output do seguinte snippet se o executar no Unix?
```
import os
print(os.name)
```

Verifique

`posix`


**Exercício 2**

Qual é o output do seguinte snippet?

```
import os

os.mkdir("hello")
print(os.listdir())
```

Verifique

`['hello']`