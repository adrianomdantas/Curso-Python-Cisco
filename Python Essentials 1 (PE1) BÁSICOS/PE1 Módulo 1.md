# Python Essentials 1:
# Módulo 1

# Introdução ao Python e à programação informática

Neste módulo, aprenderá sobre:

Os fundamentos da programação informática, ou seja, como o computador funciona, como o programa é executado, como a linguagem de programação é definida e construída;
a diferença entre compilação e interpretação;
o que é o Python, como se posiciona entre outras linguagens de programação, e o que distingue as diferentes versões de Python

## Como funciona um programa de computador?

Este curso tem como objetivo mostrar o que é a linguagem Python e para o que é utilizada. Vamos começar a partir do básico.

Um programa torna um computador utilizável. Sem um programa, um computador, mesmo o mais poderoso, nada mais é do que um objeto. Da mesma forma, sem um pianista, um piano não é mais do que uma caixa de madeira.

Os computadores são capazes de executar tarefas muito complexas, mas essa capacidade não lhes é inata. A natureza de um computador é bastante diferente.

Ele só pode executar operações extremamente simples, por exemplo, um computador não pode avaliar o valor de uma função matemática complicada por si só, embora isto não esteja fora do âmbito das possibilidades num futuro próximo.

Computadores contemporâneos só podem avaliar os resultados de operações muito fundamentais, como adicionar ou dividir, mas podem fazê-lo muito rapidamente, e podem repetir estas ações virtualmente um qualquer número de vezes.

Imagine que quer saber a velocidade média que alcançou durante uma longa viagem. Sabe a distância, sabe o tempo, precisa da velocidade.

Naturalmente, o computador será capaz de calcular isto, mas o computador não está ciente de coisas como distância, velocidade ou tempo. Portanto, é necessário instruir o computador a:

* aceitar um número que represente a distância;
* aceitar um número que represente o tempo de viagem;
* dividir o valor anterior pelo último e armazenar o resultado na memória;
* exibir o resultado (representando a velocidade média) num formato legível.

Estas quatro simples ações formam um programa. É claro que estes exemplos não são formalizados, e estão muito longe do que o computador pode compreender, mas são suficientemente bons para serem traduzidos para uma linguagem que o computador possa aceitar.

**Linguagem (Language)** é a palavra-chave.

## Linguagens naturais vs. linguagens de programação

Uma linguagem é um meio (e uma ferramenta) para expressar e registar pensamentos. Há muitas linguagens ao nosso redor. Algumas delas não requerem nem a fala nem a escrita, como a linguagem corporal; é possível expressar os seus sentimentos mais profundos com muita precisão sem dizer uma palavra.

Outra linguagem que usa diariamente é a sua língua materna, que usa para manifestar a sua vontade e para pensar na realidade. Os computadores também têm a sua própria linguagem, chamada linguagem de **máquina,** que é muito rudimentar.

Um computador, mesmo o mais sofisticado tecnicamente, é desprovido até mesmo de um vestígio de inteligência. Pode-se dizer que é como um cão bem treinado - responde apenas a um conjunto pré-determinado de comandos conhecidos.

Os comandos que reconhece são muito simples. Podemos imaginar que o computador responde a ordens como "pega nesse número, divide-o por outro e guarda o resultado".

Um conjunto completo de comandos conhecidos é chamado de **lista de instruções**, por vezes abreviado para **IL** (do inglês, Instruction List). Os diferentes tipos de computadores podem variar em função do tamanho das suas IL, e as instruções podem ser completamente diferentes em diferentes modelos.

Nota: as linguagens de máquina são desenvolvidas por humanos.

Atualmente, nenhum computador é capaz de criar uma nova linguagem. No entanto, isso pode mudar em breve. Por outro lado, as pessoas também utilizam uma série de línguas muito diferentes, mas estas línguas desenvolveram-se naturalmente. Além disso, ainda estão a evoluir.

São criadas novas palavras todos os dias e as palavras antigas desaparecem. Estas línguas são chamadas linguagens **naturais.**

## O que faz uma linguagem?

Podemos dizer que cada linguagem (de máquina ou natural, não importa) é constituída pelos seguintes elementos:

* um **alfabeto:** um conjunto de símbolos utilizados para construir palavras de uma determinada linguagem (por exemplo, o alfabeto latino para inglês, o alfabeto cirílico para russo, o Kanji para japonês, etc.)
* um **lexis:** (ou seja, um dicionário) um conjunto de palavras que a linguagem oferece aos seus utilizadores (por exemplo, a palavra "computador" vem do dicionário de língua inglesa, enquanto que 
"cmoptrue" não; a palavra "chat" está presente tanto nos dicionários de inglês como de francês, mas os seus significados são diferentes)
* uma **sintaxe:** um conjunto de regras (formais ou informais, escritas ou sentidas intuitivamente) utilizadas para determinar se uma determinada sequência de palavras forma uma frase válida (por exemplo,  "Eu sou uma pitão" é uma frase sintaticamente correta, enquanto "Eu uma pitão sou" não é)
* **semântica:** um conjunto de regras que determinam se uma determinada frase faz sentido (por exemplo, "Comi um donut" faz sentido, mas "Um donut comeu-me" não faz)

O IL é, de facto, o **alfabeto de uma linguagem de máquina**. Este é o conjunto mais simples e primário de símbolos que podemos utilizar para dar comandos a um computador. É a língua materna do computador.

Infelizmente, esta língua está muito longe de ser uma língua materna humana. Todos nós (tanto computadores como humanos) precisamos de algo mais, uma linguagem comum para computadores e humanos, ou uma ponte entre os dois mundos diferentes.

Precisamos de uma linguagem em que os humanos possam escrever os seus programas e uma linguagem que os computadores possam utilizar para executar os programas, uma linguagem que seja muito mais complexa do que a linguagem das máquinas e, no entanto, muito mais simples do que a linguagem natural.

Tais linguagens são muitas vezes chamadas linguagens de programação de alto nível. São pelo menos um pouco semelhantes aos naturais na medida em que utilizam símbolos, palavras e convenções legíveis para os seres humanos. Estas linguagens permitem aos seres humanos expressar comandos a computadores que são muito mais complexos do que os oferecidos pelas ILs.

Um programa escrito numa linguagem de programação de alto nível é chamado **source code** (em contraste com o machine code executado por computadores). Da mesma forma, o ficheiro que contém o source code chama-se **source file**.

## Compilação vs. interpretação

A programação informática é o ato de compor os elementos da linguagem de programação selecionada pela ordem que provocará o efeito desejado. O efeito pode ser diferente em cada caso específico - depende da imaginação, conhecimento e experiência do programador.

É claro que tal composição tem de ser correta em muitos sentidos:

* **alfabeticamente** - um programa precisa de ser escrito num guião reconhecível, tal como romano, cirílico, etc.
* **lexicamente** - cada linguagem de programação tem o seu dicionário e é preciso dominá-lo; felizmente, é muito mais simples e menor do que o dicionário de qualquer língua natural;
* **sintaticamente** - cada linguagem tem as suas regras, e estas devem ser obedecidas;
* **semanticamente** - o programa tem de fazer sentido.
Infelizmente, um programador também pode cometer erros com cada um dos quatro sentidos acima referidos. Cada um deles pode fazer com que o programa se torne completamente inútil.

Vamos supor que tenha escrito um programa com sucesso. Como persuadir o computador a executá-lo? Tem de transformar o seu programa em linguagem de máquina. Felizmente, a tradução pode ser feita pelo próprio computador, tornando todo o processo rápido e eficiente.

Há duas formas diferentes de **transformar um programa de uma linguagem de programação de alto nível em linguagem de máquina:**

**COMPILAÇÃO** - o source program é traduzido uma vez (no entanto, este ato deve ser repetido sempre que modificar o source code) obtendo um ficheiro (por exemplo, um ficheiro .exe se o código se destinar a ser executado no MS Windows) contendo o machine code; agora pode distribuir o ficheiro por todo o mundo; o programa que executa esta tradução chama-se compilador ou tradutor;

**INTERPRETAÇÃO** - você (ou qualquer utilizador do código) pode traduzir o source program cada vez que este tem de ser executado; o programa que executa este tipo de transformação chama-se intérprete, pois interpreta o código cada vez que se pretende executá-lo; também significa que não pode simplesmente distribuir o source code tal como está, porque o utilizador final também precisa do intérprete para o executar.

Devido a algumas razões muito fundamentais, uma linguagem de programação particular de alto nível foi concebida para se enquadrar numa destas duas categorias.

Há muito poucas linguagens que possam ser compiladas e interpretadas. Normalmente, uma linguagem de programação é projetada com este fator na mente dos seus construtores - será ela compilada ou interpretada?

## O que é que o intérprete realmente faz?

Vamos assumir mais uma vez que escreveu um programa. Agora, existe como um **arquivo de computador**: um programa de computador é na realidade um pedaço de texto, por isso o source code é normalmente colocado em **arquivos de texto.**

Nota: tem de ser **texto puro**, sem quaisquer decorações como diferentes fontes, cores, imagens embutidas ou outros suportes. Agora tem de invocar o intérprete e deixá-lo ler o seu source file.

O intérprete lê o source code de uma forma que é comum na cultura ocidental: de cima para baixo e da esquerda para a direita. Há algumas exceções - elas serão abordadas mais tarde no curso.

Em primeiro lugar, o intérprete verifica se todas as linhas subsequentes estão corretas (utilizando os quatro aspetos abordados anteriormente).

Se o compilador encontrar um erro, termina o seu trabalho imediatamente. O único resultado, neste caso, é uma **mensagem de erro.**

O intérprete informá-lo-á onde se encontra o erro e o que o causou. No entanto, estas mensagens podem ser enganadoras, uma vez que o intérprete não é capaz de seguir exatamente as suas intenções, e pode detetar erros a alguma distância das suas verdadeiras causas.

Por exemplo, se tentar utilizar uma entidade com um nome desconhecido, causará um erro, mas o erro será descoberto no local onde tenta utilizar a entidade, e não onde o nome da nova entidade foi introduzido.

Por outras palavras, a razão real está normalmente localizada um pouco mais cedo no código, por exemplo, no local onde teve de informar o intérprete de que ia utilizar a entidade do nome.

Se a linha parecer boa, o intérprete tenta executá-la (nota: cada linha é normalmente executada separadamente, pelo que o trio "read-check-execute" pode ser repetido muitas vezes - mais vezes do que o número real de linhas no source file, uma vez que algumas partes do código podem ser executadas mais de uma vez).

É também possível que uma parte significativa do código possa ser executada com sucesso antes de o intérprete encontrar um erro. Este é um comportamento normal neste modelo de execução.

Pode perguntar agora: o que é melhor? O modelo "compilador" ou o modelo "intérprete"? Não há uma resposta óbvia. Se houvesse, um destes modelos já teria deixado de existir há muito tempo. Ambos têm as suas vantagens e as suas desvantagens.

## Compilação vs. Interpretação - vantagens e desvantagens
|teste|**COMPILAÇÃO**|**INTERPRETAÇÃO**|
|**VANTAGENS**|a execução do código traduzido é geralmente mais rápida;|pode executar o código assim que o concluir - não há fases adicionais de tradução;|
|teste|apenas o utilizador tem de ter o compilador - o end-user (utilizador final) pode usar o código sem ele;|o código é armazenado usando linguagem de programação, não de máquina - isto significa que pode ser executado em computadores utilizando diferentes linguagens de máquina; não se compila o código separadamente para cada arquitetura diferente.|
|teste|o código traduzido é armazenado utilizando linguagem de máquina - como é muito difícil de entender, as suas próprias invenções e truques de programação provavelmente permanecerão segredo.|teste|
|**DESVANTAGENS**|a compilação em si pode ser um processo muito demorado - pode não ser capaz de executar o seu código imediatamente após qualquer alteração;|não espere que a interpretação aumente o seu código para alta velocidade - o seu código irá partilhar o poder do computador com o intérprete, pelo que não pode ser realmente rápido;|
|teste|tem de ter tantos compiladores quanto plataformas de hardware em que queira que o seu código seja executado|tanto você como o end-user têm de ter o intérprete para executar o seu código.|

## O que significa tudo isto para si?

* O Python é uma **linguagem interpretada**. Isto significa que herda todas as vantagens e desvantagens descritas. Naturalmente, acrescenta algumas das suas características únicas a ambos os conjuntos.
* Se quiser programar em Python, precisará do **intérprete Python**. Não será capaz de executar o seu código sem ele. Felizmente, **o Python é gratuito**. Esta é uma das suas vantagens mais importantes.

Devido a razões históricas, as linguagens concebidas para serem utilizadas na forma de interpretação são muitas vezes chamadas linguagens de scripting, enquanto os source programs codificados que as utilizam são chamados scripts.