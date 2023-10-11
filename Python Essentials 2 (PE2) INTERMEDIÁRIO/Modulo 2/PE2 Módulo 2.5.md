## 2.5.1.1 Quatro programas simples

## A Cifra César: encriptar uma mensagem

Vamos mostrar-lhe quatro programas simples, para apresentar alguns aspetos do processamento de string em Python. Eles são propositadamente simples, mas os problemas do lab serão significativamente mais complicados.

O primeiro problema que queremos mostrar chama-se **Caesar cipher** - mais detalhes aqui: https://en.wikipedia.org/wiki/Caesar_cipher.

Esta cifra foi (provavelmente) inventada e usada por Caio Júlio César e suas tropas durante as Guerras Gálicas. A ideia é bastante simples - cada letra da mensagem é substituída pela sua consequente mais próxima (A torna-se B, B torna-se C, e assim por diante). A única exceção é Z, que se torna A.

O programa no editor é uma implementação muito simples (mas funcional) do algoritmo.

```
# Caesar cipher.
text = input("Enter your message: ")
cipher = ''
for char in text:
    if not char.isalpha():
        continue
    char = char.upper()
    code = ord(char) + 1
    if code > ord('Z'):
        code = ord('A')
    cipher += chr(code)

print(cipher)
```

Escrevemo-lo utilizando os seguintes pressupostos:

* aceita apenas letras latinas (nota: os romanos não usavam espaços em branco nem dígitos)
* todas as letras da mensagem estão em maiúsculas (nota: os romanos conheciam apenas maiúsculas)

Vamos rastrear o código:

* linha 02: pedir ao utilizador para inserir a mensagem aberta (não encriptada), de uma linha;
* linha 03: preparar uma string para uma mensagem encriptada (vazia por agora)
* linha 04: iniciar a iteração através da mensagem;
* linha 05: se o caratere atual não for alfabético...
* linha 06: ...ignorá-lo;
* linha 07: converter a letra em maiúsculas (é preferível fazê-lo cegamente, em vez de verificar se é necessário ou não)
* linha 08: obter o código da letra e incrementá-lo em um;
* linha 09: se o código resultante tiver “deixado” o alfabeto latino (se for maior do que o código Z)...
* linha 10: ...alterá-lo para o código A;
* linha 11: anexar o caratere recebido ao fim da mensagem encriptada;
* linha 13: imprimir a cifra.

O código, alimentado com esta mensagem:

`AVE CAESAR`

tem como output:

output

`BWFDBFTBS`

Faça os seus próprios testes.

## 2.5.1.2 Quatro programas simples

## A Cifra César: decifrar uma mensagem

A transformação inversa deve agora ser clara para si - vamos apenas apresentar-lhe o código tal como está, sem quaisquer explicações.

Veja o código no editor. Verifique cuidadosamente se funciona. Use o criptograma do programa anterior.

```
# Caesar cipher - decrypting a message.
cipher = input('Enter your cryptogram: ')
text = ''
for char in cipher:
    if not char.isalpha():
        continue
    char = char.upper()
    code = ord(char) - 1
    if code < ord('A'):
        code = ord('Z')
    text += chr(code)

print(text)
```

output

```
Enter your cryptogram: 9
Enter your cryptogram: teste
SDRSD
```

## 2.5.1.3 Quatro programas simples

## O Processador de Números

O terceiro programa mostra um método simples que lhe permite introduzir uma linha cheia de números, e processá-los facilmente. Nota: a função de rotina `input()` , combinada juntamente com as funções `int()` ou `float()` , é inadequada para esta finalidade.

O processamento será extremamente fácil - queremos que os números sejam somados.

Veja o código no editor. Vamos analisá-lo.

A utilização da compreensão de lista pode tornar o código mais magro. Pode fazer isso se quiser.

```
# Numbers Processor.

line = input("Enter a line of numbers - separate them with spaces: ")
strings = line.split()
total = 0
try:
    for substr in strings:
        total += float(substr)
    print("The total is:", total)
except:
    print(substr, "is not a number.")
```

Vamos apresentar a nossa versão:

* linha 03: pedir ao utilizador para introduzir uma linha preenchida com qualquer número de números (os números podem ser floats)
* linha 04: dividir a linha recebendo uma lista de substrings;
* linha 05: iniciar a soma total a zero;
* linha 06: como a conversão de string-float pode levantar uma exceção, o melhor é continuar com a proteção do bloco try-except;
* linha 07: iterar através da lista...
* linha 08: ...e tentar converter todos os seus elementos em números float; se funcionar, aumentar a soma;
* linha 09: tudo está bem até agora, por isso imprimir a soma;
* linha 10: o programa termina aqui no caso de um erro;
* linha 11: imprimir uma mensagem de diagnóstico mostrando ao utilizador o motivo da falha.

O código tem um ponto fraco importante - apresenta um resultado falso quando o utilizador introduz uma linha vazia. Consegue consertá-lo?

## 2.5.1.4 Quatro programas simples

## O validador IBAN

O quarto programa implementa (de uma forma ligeiramente simplificada) um algoritmo utilizado pelos bancos europeus para especificar números de conta. A norma denominada **IBAN** (International Bank Account Number) fornece um método simples e bastante fiável de validação dos números de conta contra erros de digitação simples que possam ocorrer durante a reescrita do número, por exemplo, de documentos em papel, como faturas ou contas, para computadores.

Pode encontrar mais detalhes aqui: https://en.wikipedia.org/wiki/International_Bank_Account_Number.

Um número de conta compatível com IBAN consiste em:

* um código de país de duas letras retirado da norma ISO 3166-1 (por exemplo, FR para a França, GB para a Grã-Bretanha, DE para a Alemanha, e assim por diante)
* dois dígitos de verificação utilizados para realizar as verificações de validade - testes rápidos e simples, mas não totalmente fiáveis, mostrando se um número é inválido (distorcido por uma gralha) ou se parece ser válido;
* o número real da conta (até 30 carateres alfanuméricos - o comprimento desta parte depende do país)
A norma diz que a validação requer os seguintes passos (de acordo com a Wikipédia):

* (passo 1) Verificar se o comprimento total do IBAN está correto de acordo com o país (este programa não o fará, mas pode modificar o código para cumprir este requisito, assim o desejar; nota: tem de ensinar ao código todos os comprimentos utilizados na Europa)
* (passo 2) Mover os quatro carateres iniciais para o final da string (ou seja, o código do país e os dígitos de verificação)
* (passo 3) Substituir cada letra na string por dois dígitos, expandindo assim a string, onde A = 10, B = 11... Z = 35;
* (passo 4) Interpretar a string como um número inteiro decimal e calcular o resto desse número na divisão por 97; Se o resto for 1, o teste de verificação de dígito é passado e o IBAN pode ser válido.

Veja o código no editor. Vamos analisá-lo:

```
# IBAN Validator.

iban = input("Enter IBAN, please: ")
iban = iban.replace(' ','')

if not iban.isalnum():
    print("You have entered invalid characters.")
elif len(iban) < 15:
    print("IBAN entered is too short.")
elif len(iban) > 31:
    print("IBAN entered is too long.")
else:
    iban = (iban[4:] + iban[0:4]).upper()
    iban2 = ''
    for ch in iban:
        if ch.isdigit():
            iban2 += ch
        else:
            iban2 += str(10 + ord(ch) - ord('A'))
    iban = int(iban2)
    if iban % 97 == 1:
        print("IBAN entered is valid.")
    else:
        print("IBAN entered is invalid.")
```

* linha 03: pedir ao utilizador para introduzir o IBAN (o número pode conter espaços, uma vez que melhoram significativamente a legibilidade do número...
* linha 04: ...mas remova-os imediatamente)
* linha 05: o IBAN inserido deve consistir apenas em dígitos e letras - se não consistir...
* linha 06:... fazer output da mensagem;
* linha 07: o IBAN não deve ser menor do que 15 carateres (esta é a variante mais curta, usada na Noruega)
* linha 08: se for mais curto, o utilizador é informado;
* linha 09: além disso, o IBAN não pode ter mais de 31 carateres (esta é a variante mais longa, usada em Malta)
* linha 10: se for mais longo, fazer um aviso;
* linha 11: iniciar o processamento em si;
* linha 12: mover os quatro carateres iniciais para o final do número e converter todas as letras em maiúsculas (passo 02 do algoritmo)
* linha 13: esta é a variável utilizada para completar o número, criada através da substituição das letras por dígitos (de acordo com o passo 03 do algoritmo)
* linha 14: iterar através do IBAN;
* linha 15: se o caratere é um dígito...
* linha 16: basta copiá-lo;
* linha 17: caso contrário...
* linha 18: ...convertê-lo em dois dígitos (observe como tal é feito aqui)
* linha 19: a forma convertida do IBAN está pronta - fazer um inteiro dele;
* linha 20: é o resto da divisão de iban2 por 97 igual a 1?
* linha 21: Se sim, então sucesso;
* linha 22: Caso contrário...
* linha 23: ...o número é inválido.

Vamos adicionar alguns dados de teste (todos estes números são válidos - pode invalidá-los alterando qualquer caratere).

* Britânico: GB72 HBZU 7006 7212 1253 00
* Francês: FR76 30003 03620 00020216907 50
* Alemão: DE02100100100152517108

Se for um residente da UE, pode usar o seu próprio número de conta para testes.

## 2.5.1.5 RESUMO DA SECÇÃO

## Key takeaways

1. As strings são ferramentas chave no processamento moderno de dados, uma vez que a maioria dos dados úteis são na realidade strings. Por exemplo, usar um motor de busca web (que parece bastante trivial nos dias de hoje) utiliza processamento de strings extremamente complexo e complicado, envolvendo quantidades inimagináveis de dados.

2. A comparação de strings de uma forma rigorosa (como faz o Python) pode ser muito insatisfatória quando se trata de pesquisas avançadas (por exemplo, durante extensas consultas a bases de dados). Em resposta a esta exigência, foram criados e implementados vários algoritmos de comparação de strings fuzzy (difusas). Estes algoritmos são capazes de encontrar strings que não são iguais no sentido Python, mas são **semelhantes**.

Um desses conceitos é a **distância Hamming**, que é usada para determinar a semelhança de duas strings. Se este problema lhe interessa, pode encontrar mais informações aqui: https://en.wikipedia.org/wiki/Hamming_distance. Outra solução do mesmo tipo, mas baseada numa suposição diferente, é a **distância Levenshtein** descrita aqui: https://en.wikipedia.org/wiki/Levenshtein_distance.

3. Outra forma de comparar strings é encontrar a sua semelhança acústica, o que significa um processo que leva a determinar se duas strings soam de forma semelhante (como "raise" e "race"). Essa semelhança deve ser estabelecida para cada língua (ou mesmo dialeto) separadamente.

Um algoritmo utilizado para efetuar tal comparação para a língua inglesa chama-se **Soundex** e foi inventado - não vai acreditar - em 1918. Pode descobrir mais informações aqui: https://en.wikipedia.org/wiki/Soundex.

4. Devido à limitada precisão de dados nativos float e inteiros, é por vezes razoável armazenar e processar valores numéricos enormes como strings. Esta é a técnica que o Python utiliza quando se o força a funcionar com um número inteiro constituído por um número muito grande de dígitos.

## 2.5.1.6 LAB: Melhorar a cifra César

## 2.5.1.7 LAB: Palíndromos

## 2.5.1.8 LAB: Anagramas

## 2.5.1.9 LAB: O Dígito da Vida

## 2.5.1.10 LAB: Encontre uma palavra!

## 2.5.1.11 LAB: Sudoku
