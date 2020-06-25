# Sejam bem-vindos.
Grupo de estudo Python - COVID-19

# Geradores

* Geradores podem ser declarados de forma semalhante a funções.
* No lugar da cláusula return, usa-se yield.
* Geradores se comportam como iteradors.
* A cada iteração, o gerador retorna a executar a partir do último yield.

```python
# Define-se gerador da mesma forma que funções, mas com a cláusula yield.
def quadrados():
    yield 0
    yield 1
    yield 4
    yield 9
    yield 16
```

```python
# Existe a classe generator
print(quadrados()) # Objeto gerador
```
> <generator object quadrados at 0x7f868cc87db0>

```python
# Você pode obter todos os valores produzidos. (Cuidado com geradores infinitos.)
print(*quadrados())
```
> 0 1 4 9 16

```python
# Você pode iterar em um gerador
for i in quadrados():
    print(i)
```
> 0  
> 1  
> 4  
> 9  
> 16

```python
# Você pode iterar em uma compreensão de lista:
x = [2*i for i in quadrados()]
print(x)
```
> [0, 2, 8, 18, 32]

```python
# Existe a função next

x = quadrados()

print(next(x))
print(next(x))
print(next(x))
print(next(x))
print(next(x))
```
> 0  
> 1  
> 4  
> 9  
> 16

```python
# Você pode inserir laços
def quadrados():
    x = 0
    while x<10:
        yield x**2
        x += 1

print(*quadrados())
```
> 0 1 4 9 16 25 36 49 64 81

```python
g = quadrados()
print(next(g))
print(next(g))
print(next(g))
```
> 0  
> 1  
> 4

```python
# Laço for
def cubos():
    for i in range(0, 10):
        yield i**3

print(*cubos())
```
> 0 1 8 27 64 125 216 343 512 729

```python
# Geradores podem ter efeitos colaterais (side effect)
# (= qualquer alteração fora do escopo da função / gerador)

def cubos():
    for i in range(0, 10):
        print('Eu posso escrever na tela.')
        yield i**3

for i in cubos():
    print(i)
```
> Eu posso escrever na tela.  
> 0  
> Eu posso escrever na tela.  
> 1  
> Eu posso escrever na tela.  
> 8  
> Eu posso escrever na tela.  
> 27  
> Eu posso escrever na tela.  
> 64  
> Eu posso escrever na tela.  
> 125  
> Eu posso escrever na tela.  
> 216  
> Eu posso escrever na tela.  
> 343  
> Eu posso escrever na tela.  
> 512  
> Eu posso escrever na tela.  
> 729

```python
# Em relação ao gerador definido na célula anterior,
# explique a diferença de comportamento:

print (*cubos())
```
> Eu posso escrever na tela.  
> Eu posso escrever na tela.  
> Eu posso escrever na tela.  
> Eu posso escrever na tela.  
> Eu posso escrever na tela.  
> Eu posso escrever na tela.  
> Eu posso escrever na tela.  
> Eu posso escrever na tela.  
> Eu posso escrever na tela.  
> Eu posso escrever na tela.  
> 0 1 8 27 64 125 216 343 512 729

```python
# Um gerador pode receber parâmetros
def quadrados(n):
    x = 0
    while x<n:
        yield x**2
        x += 1

print(*quadrados(4))
```
> 0 1 4 9

```python
f = quadrados(10)
g = quadrados(5)
print(*f)
print(*g)
```
> 0 1 4 9 16 25 36 49 64 81  
> 0 1 4 9 16

```python
# Veja como se usa
f = quadrados(4)
print(type(f))
for i in f:
    print(i)
```
> <class 'generator'>  
> 0  
> 1  
> 4  
> 9

```python
# Gerador fica extinto
f = quadrados(4)

print('A. ',*f)
print('B. ',*f)
```
> A.  0 1 4 9  
> B.

```python
# Você pode instanciar geradores independentes da mesma classe
f = quadrados(5)
g = quadrados(10)

print('f. ', next(f))
print('f. ',next(f))
print('f. ',next(f))
print('g. ',next(g))
print('g. ',next(g))
print('f. ',next(f))
```
> f.  0  
> f.  1  
> f.  4  
> g.  0  
> g.  1  
> f.  9

```python
def quadrados(n):
    x = 0
    while x<n:
        mensagem = yield x**2
        print('Recebi: ', mensagem)
        x += 1

f = quadrados(10)
print(next(f))  # não se pode mandar mensagem para gerador recém criado, mande por parâmetros.
print(f.send(10)) # manda mensagem e retorna valor produzido
```
> 0  
> Recebi:  10  
> 1

```python
# Definindo geradores em linha
g = (x**2 for x in range(10)) # Define uma instância.
print(*g)
```
> 0 1 4 9 16 25 36 49 64 81

```python
# Pode-se usar funções lambda funções que retornam geradores.
quadrados = lambda n: (x**2 for x in range(n))

g = quadrados(10)
print(*g)
```
> 0 1 4 9 16 25 36 49 64 81

```python
f = lambda n: (x**2 for x in range(n))
print(f(10))
```
> <generator object <lambda>.<locals>.<genexpr> at 0x7f868c81f360>

```python
# Pode-se criar geradores infinitos. Cuidado com * e for
def quadrados():
    x = 0
    while True:
        yield x**2
        x += 1

f = quadrados()
for i in range(10):
    print(next(f))
```
> 0  
> 1  
> 4  
> 9  
> 16  
> 25  
> 36  
> 49  
> 64  
> 81

```python
# Função enumerate

A = ['a', 'b', 'c', 'd']

for i, x in enumerate(A):
    print(i, x)
```
> 0 a  
> 1 b  
> 2 c  
> 3 d

```python
for i, x in enumerate(quadrados()):
    print(x)
    if i > 10:
        break
```
> 0  
> 1  
> 4  
> 9  
> 16  
> 25  
> 36  
> 49  
> 64  
> 81  
> 100  
> 121

```python
print(*enumerate(A))
```
> (0, 'a') (1, 'b') (2, 'c') (3, 'd')

```python
# Função zip

f = [1, 2, 3, 4, 5]
g = ['a', 'b', 'c', 'd', 'e']

for x, y in zip(f, g):  # Se tamanhos forem distintos, interrompe no final da menor.
    print(x, y)
```
> 1 a  
> 2 b  
> 3 c  
> 4 d  
> 5 e



# A biblioteca itertools

* Traz diversos iteradores implementados de forma eficiente.
* Abaixo funções selecionadas.
* https://docs.python.org/3/library/itertools.html

```python
import itertools as it # Não use iter, pois isso é função built-in
```

```python
# itertools.count(start=0, step=1) - Contador infinito

g = it.count(10, 2)

print(next(g))
print(next(g))
print(next(g))
```
> 10  
> 12  
> 14

```python
# itertools.cycle(iterable)
# Gerador infinito que gera repetições do iterável

f = ['A', 'B', 22]
g = it.cycle(f)

for n, x in enumerate(g):
    print(x)
    if n==10:
        break
```
> A  
> B  
> 22  
> A  
> B  
> 22  
> A  
> B  
> 22  
> A  
> B  

```python
A = ['A', 'B', 'C']
for i, x in enumerate(it.cycle(A)):
    print(i, x)
    if i==50:
        break
```
> 0 A  
> 1 B  
> 2 C  
> 3 A  
> 4 B  
> ...  
> 48 A  
> 49 B  
> 50 C

```python
print(A*2)
```
> ['A', 'B', 'C', 'A', 'B', 'C']

```python
# itertools.filterfalse(predicate, iterable)

f = [0, 10, 22, 10, 5, 30, 2]

g = [0, 1, 2, 3, 4, 5, 6, 7]
print(*it.filterfalse(lambda x: x>=5, g))
```
> 0 1 2 3 4

```python
# itertools.permutations(iterable, r=None)

f = ['A', 'B', 'C']

print(*it.permutations(f, 2))
print(*it.permutations(f, 3))
```
> ('A', 'B') ('A', 'C') ('B', 'A') ('B', 'C') ('C', 'A') ('C', 'B')  
> ('A', 'B', 'C') ('A', 'C', 'B') ('B', 'A', 'C') ('B', 'C', 'A') ('C', 'A', 'B') ('C', 'B', 'A')

```python
for i, j in it.permutations(f, 2):
    print(i, j)
```
> A B  
> A C  
> B A  
> B C  
> C A  
> C B

```python
# Você entende o seguinte código?

S = 'UFRGS'
lista = ["".join(l) for l in it.permutations(S, 5)]    
# lista.sort()
print(lista)
```
> ['UFRGS', 'UFRSG', 'UFGRS', 'UFGSR', 'UFSRG', 'UFSGR', 'URFGS', 'URFSG', 'URGFS', 'URGSF', 'URSFG', 'URSGF', 'UGFRS', 'UGFSR', 'UGRFS', 'UGRSF', 'UGSFR', 'UGSRF', 'USFRG', 'USFGR', 'USRFG', 'USRGF', 'USGFR', 'USGRF', 'FURGS', 'FURSG', 'FUGRS', 'FUGSR', 'FUSRG', 'FUSGR', 'FRUGS', 'FRUSG', 'FRGUS', 'FRGSU', 'FRSUG', 'FRSGU', 'FGURS', 'FGUSR', 'FGRUS', 'FGRSU', 'FGSUR', 'FGSRU', 'FSURG', 'FSUGR', 'FSRUG', 'FSRGU', 'FSGUR', 'FSGRU', 'RUFGS', 'RUFSG', 'RUGFS', 'RUGSF', 'RUSFG', 'RUSGF', 'RFUGS', 'RFUSG', 'RFGUS', 'RFGSU', 'RFSUG', 'RFSGU', 'RGUFS', 'RGUSF', 'RGFUS', 'RGFSU', 'RGSUF', 'RGSFU', 'RSUFG', 'RSUGF', 'RSFUG', 'RSFGU', 'RSGUF', 'RSGFU', 'GUFRS', 'GUFSR', 'GURFS', 'GURSF', 'GUSFR', 'GUSRF', 'GFURS', 'GFUSR', 'GFRUS', 'GFRSU', 'GFSUR', 'GFSRU', 'GRUFS', 'GRUSF', 'GRFUS', 'GRFSU', 'GRSUF', 'GRSFU', 'GSUFR', 'GSURF', 'GSFUR', 'GSFRU', 'GSRUF', 'GSRFU', 'SUFRG', 'SUFGR', 'SURFG', 'SURGF', 'SUGFR', 'SUGRF', 'SFURG', 'SFUGR', 'SFRUG', 'SFRGU', 'SFGUR', 'SFGRU', 'SRUFG', 'SRUGF', 'SRFUG', 'SRFGU', 'SRGUF', 'SRGFU', 'SGUFR', 'SGURF', 'SGFUR', 'SGFRU', 'SGRUF', 'SGRFU']

```python
#p = it.permutations(S)
print(len(lista))
```
> 120

```python
# itertools.product(*iterables, repeat=1)

f = [1, 2, 3]
g = ['a', 'b', 'c']

# Todas as combinações de um elemento de f e um elemento de g
for x, y in it.product(f, g):
    print(x, y)
```
> 1 a  
> 1 b  
> 1 c  
> 2 a  
> 2 b  
> 2 c  
> 3 a  
> 3 b  
> 3 c

```python
for i, j in it.product(range(3), range(5)):
    print(i, j)
```
> 0 0  
> 0 1  
> 0 2  
> 0 3  
> 0 4  
> 1 0  
> 1 1  
> 1 2  
> 1 3  
> 1 4  
> 2 0  
> 2 1  
> 2 2  
> 2 3  
> 2 4

```python
# itertools.product(*iterables, repeat=1)

f = [1, 2]
g = ['a', 'b']
h = ['x', 'y']

for x, y, z in it.product(f, g, h):
    print(x, y, z)
```
> 1 a x  
> 1 a y  
> 1 b x  
> 1 b y  
> 2 a x  
> 2 a y  
> 2 b x  
> 2 b y

```python
# itertools.combinations(iterable, r) -  Combições sem repetição
# itertools.combinations_with_replacement(iterable, r) -  Com repetição

f = ['A', 'B', 'C']

print(*it.permutations(f, 2))
print(*it.combinations(f, 2))
print(*it.combinations_with_replacement(f, 2))
```
> ('A', 'B') ('A', 'C') ('B', 'A') ('B', 'C') ('C', 'A') ('C', 'B')  
> ('A', 'B') ('A', 'C') ('B', 'C')  
> ('A', 'A') ('A', 'B') ('A', 'C') ('B', 'B') ('B', 'C') ('C', 'C')



# Métodos e funções para strings

* Strings são objetos imutáveis, então você sempre cria uma nova string.
* https://docs.python.org/2/library/string.html

```python
# Definindo string

x = 'Python'
y = "Python"
z = """Python"""  # Permite text multilinha

print(x, y, z)

# Observação, strings em sequência são concatenados
x = '123' 'abc' """AQ"""

print(x)
```
> Python Python Python  
> 123abcAQ

```python
# String multilinhas

x = """Linha 1
Linha 2"""

print(x)
```
> Linha 1  
> Linha 2

```python
# String multilinhas

x = "Linha 1\nLinha 2"  #\n = newline

print(x)
```
> Linha 1  
> Linha 2

```python
# Aspas literais dentro de strings

x = 'O "nome".'
y = "O \"nome\"."

z = """O "nome"."""
u = "\"nome\""
print(x, y, z, u)

# Idem para '
```
> O "nome". O "nome". O "nome". "nome"

```python
# Tabulação

print("A\tb\tc") # https://docs.python.org/3/reference/lexical_analysis.html
```
> A    b    c

```python
# Barras

x = '\\   \\\\'

print(x)
```
> \\    \\\

```python
# Unicode

print('\U0001f600') # Unicode 32 hex
print('\u76f3')     # Unicode 16 hex
```
> 😀  
> 盳

```python
# Conversões caracter <=> Unicode

print(ord('ã'), ord('😀'))
print(chr(227), chr(128512), chr(0x1f600)) #0x = hexadecimal.
```
> 227 128512  
> ã 😀 😀

```python
# Conversões

for i in range(400):
    print(chr(0x1f600 + i), end='')
    if i%30 == 29:
        print()
```
> 😀😁😂😃😄😅😆😇😈😉😊😋😌😍😎😏😐😑😒😓😔😕😖😗😘😙😚😛😜😝  
> 😞😟😠😡😢😣😤😥😦😧😨😩😪😫😬😭😮😯😰😱😲😳😴😵😶😷😸😹😺😻  
> 😼😽😾😿🙀🙁🙂🙃🙄🙅🙆🙇🙈🙉🙊🙋🙌🙍🙎🙏🙐🙑🙒🙓🙔🙕🙖🙗🙘🙙  
> 🙚🙛🙜🙝🙞🙟🙠🙡🙢🙣🙤🙥🙦🙧🙨🙩🙪🙫🙬🙭🙮🙯🙰🙱🙲🙳🙴🙵🙶🙷  
> 🙸🙹🙺🙻🙼🙽🙾🙿🚀🚁🚂🚃🚄🚅🚆🚇🚈🚉🚊🚋🚌🚍🚎🚏🚐🚑🚒🚓🚔🚕  
> 🚖🚗🚘🚙🚚🚛🚜🚝🚞🚟🚠🚡🚢🚣🚤🚥🚦🚧🚨🚩🚪🚫🚬🚭🚮🚯🚰🚱🚲🚳  
> 🚴🚵🚶🚷🚸🚹🚺🚻🚼🚽🚾🚿🛀🛁🛂🛃🛄🛅🛆🛇🛈🛉🛊🛋🛌🛍🛎🛏🛐🛑  
> 🛒🛓🛔🛕🛖🛗🛘🛙🛚🛛🛜🛝🛞🛟🛠🛡🛢🛣🛤🛥🛦🛧🛨🛩🛪🛫🛬🛭🛮🛯  
> 🛰🛱🛲🛳🛴🛵🛶🛷🛸🛹🛺🛻🛼🛽🛾🛿🜀🜁🜂🜃🜄🜅🜆🜇🜈🜉🜊🜋🜌🜍  
> 🜎🜏🜐🜑🜒🜓🜔🜕🜖🜗🜘🜙🜚🜛🜜🜝🜞🜟🜠🜡🜢🜣🜤🜥🜦🜧🜨🜩🜪🜫  
> 🜬🜭🜮🜯🜰🜱🜲🜳🜴🜵🜶🜷🜸🜹🜺🜻🜼🜽🜾🜿🝀🝁🝂🝃🝄🝅🝆🝇🝈🝉  
> 🝊🝋🝌🝍🝎🝏🝐🝑🝒🝓🝔🝕🝖🝗🝘🝙🝚🝛🝜🝝🝞🝟🝠🝡🝢🝣🝤🝥🝦🝧  
> 🝨🝩🝪🝫🝬🝭🝮🝯🝰🝱🝲🝳🝴🝵🝶🝷🝸🝹🝺🝻🝼🝽🝾🝿🞀🞁🞂🞃🞄🞅  
> 🞆🞇🞈🞉🞊🞋🞌🞍🞎🞏

```python
# String são imutáveis, logo você não pode fazer:
# string[3] ='a'
# Uma saída é criar outra string:

x = '0123456789'
x = x[:3] + 'A' + x[4:]

print(x)
```
> 012A456789

```python
# string.upper(), string.lower() e string.title() - Maiúsculas e minúscula.

s = 'Biblioteca de Alexandria'
x = s.upper()
y = s.lower()
z = s.title()
u = s.swapcase()

print(x)
print(y)
print(z)
print(u)
```
> BIBLIOTECA DE ALEXANDRIA  
> biblioteca de alexandria  
> Biblioteca De Alexandria  
> bIBLIOTECA DE aLEXANDRIA

```python
# Conversões

x = '12.34'
y = float(x)
z = y + 2
print([x, y, z]) # x é string e y é float
```
> ['12.34', 12.34, 14.34]

```python
# Conversões

x = 12.34
y = str(x)

print([x, y])
print([*y])
```
> [12.34, '12.34']  
> ['1', '2', '.', '3', '4']

```python
# O método format

n = 2
s = 'O número {} é par'.format(n)

print(s)
```
> O número 2 é par

```python
# O método format

#x, y = 1/3, 3
x = 1/3
y = 3

print('x = {} e y = {}'.format(x, y))
```
> x = 0.3333333333333333 e y = 3

```python
# Especificando a formatação

x = 1.234567890123456
y = 123456789.0123456

print('x = {}'.format(x))
print('x = {:f}'.format(x)) # Notação fixa
print('x = {:e}'.format(x)) # Notação científica
print('x = {:g}'.format(x)) # Escolhe conforme tamanho, vide doc.
print()
print('y = {}'.format(y))
print('y = {:f}'.format(y)) # Notação fixa
print('y = {:e}'.format(y)) # Notação científica
print('y = {:g}'.format(y)) # Escolha
```
> x = 1.234567890123456  
> x = 1.234568  
> x = 1.234568e+00  
> x = 1.23457  
>
> y = 123456789.0123456  
> y = 123456789.012346  
> y = 1.234568e+08  
> y = 1.23457e+08

```python
print('y = {:.5f}'.format(1/3)) # Notação científica
```
> y = 0.33333



# Notação científica

Se $x = 13000 = 1.3 \times 10^4$, então:
$$x = 13000 = 1.3 \times 10^4$$

* LaTex

```python
# Especificando o tamanho

x = 30.1234567890123456

print('x = {:.8f}'.format(x))
print('x = {:.8e}'.format(x))
print('x = {:.8g}'.format(x))
```
> x = 30.12345679  
> x = 3.01234568e+01  
> x = 30.123457

```python
# Você pode controlar a largura
x = 123.456
y = 1.23456
print('x = {:>10.5f}'.format(x))
print('y = {:>10.5f}'.format(y))
```
> x =  123.45600  
> y =    1.23456

```python
# Percentagem
x = 0.123456
print('x = {:.2%}'.format(x))
print('x = {:.4%}'.format(x))
```
> x = 12.35%  
> x = 12.3456%

```python
# Controlando parâmetros
x = 1
y = 2

print('{1} {0}'.format(x, y))
print('{0} {0} {1}'.format(x, y))
```
> 2 1  
> 1 1 2

```python
# Parâmetros com nomes
print('{x} {area:.5f}'.format(x=1, area=2))
```
> 1 2.00000

```python
# Strings

print('{}'.format('Computador'))
print('{!s}'.format('Computador'))
print('{!r}'.format('Computador'))
```
> Computador  
> Computador  
> 'Computador'

```python
# Alinhamento
x = 'Python'
y = 'JavaScript'

print('{:>10}'.format(x))
print('{:>10}'.format(y))
print()
print('{:<10}'.format(x))
print('{:<10}'.format(y))
print()
print('{:^10}'.format(x))
print('{:^10}'.format(y))
```
>    Python  
> JavaScript
>
> Python    
> JavaScript
>
>   Python  
> JavaScript

```python
# Datas
import datetime
hoje = datetime.datetime.now()
print('{:%d/%m/%y, %H:%M:%S}'.format(hoje))
print('{:%d/%m/%Y, %H:%M:%S}'.format(hoje))
print('{:%d - %m}'.format(hoje))
```
> 07/06/20, 02:46:44  
> 07/06/2020, 02:46:44  
> 07 - 06

```python
# Uso de {} literal
print('{{ e {}'.format(1))
print('{{}} e {}'.format(1))
```
> { e 1  
> {} e 1

```python
# Caracteres especiais
print('1\t2\n3') # \t = tab, \n = nova linha
print('OBS: Escreva \\\\ para obter \\.')
```
> 1	    2  
> 3  
> OBS: Escreva \\\ para obter \\.

```python
# Srings cruas (raw strings)

print(r'Nas r-strings, \n não é um código de escape.')
```
> Nas r-strings, \n não é um código de escape.

```python
# r-strings produzem strings normais.
# Não são uma nova classe.

x = 'a\tb'
y = r'a\tb'

print(x, type(x), len(x), sep='\t')
print(y, type(y), len(y), sep='\t')
```
> a b	<class 'str'>	3  
> a\tb	<class 'str'>	4

```python
# A função repr retorna a representação python de um objeto
import numpy as np

x = 'Livro'
y = np.array([1, 2, 3, 'Livro'])

print(x)
print(repr(x))

print(y)
print(repr(y))
```
> Livro  
> 'Livro'  
> ['1' '2' '3' 'Livro']  
> array(['1', '2', '3', 'Livro'], dtype='<U21')

```python
# Pode-se executar uma expressão Python

x = 2
print(eval('x*3 + 2'))
```
> 8

```python
# Comentado para não interromper execução das células em série
x = input('Entre com uma expressão:')
print(eval(x))
```
> Entre com uma expressão:1 + 1  
> 2

```python
# Cuidado com função com efeitos colaterais!
# # (= qualquer alteração fora do escopo da função/gerador/etc chamado)

print(eval('print(3)'))
```
> 3  
> None

```python
# Exemplo

expr = input('Entre com uma expressão: ')
print('O resultado é {}'.format(eval(expr)))
```
> Entre com uma expressão: 5 * 5  
> O resultado é 25

```python
# Procurando uma substring
x = 'Python é uma linguagem orientada a objetos.'

pos = x.find('or')  # Que acontece se você procura uma subtring inexistente?
print(pos, x[pos:])
```
> 23 orientada a objetos.

```python
# Procurando uma substring
x = 'Python é uma linguagem orientada a objetos.'
print(x.find('o'), x.rfind('o')) # r = right
```
> 4 40

```python
# Procurando todas as ocorrências de uma substring

x = """Vozes veladas, veludosas vozes,
Volúpias dos violões, vozes veladas,
Vagam nos velhos vórtices velozes
Dos ventos, vivas, vãs, vulcanizadas.""" # Cruz e Sousa

ocorrencias = []
pos = 0
while True:
    pos = x.find('v', pos)
    if pos == -1:
        break
    ocorrencias.append(pos)
    pos += 1

print(ocorrencias)
```
> [6, 15, 25, 45, 54, 60, 79, 86, 95, 107, 115, 117, 122, 127]

```python
"vozes veladas".find('v', 5)
```
> 6

```python
# Substituindo
x = 'Python é uma linguagem orientada a objetos.'

print(x.replace('Python', 'C++'))
print(x.replace(' ', '-'))  # Troca todas as ocorrências
```
> C++ é uma linguagem orientada a objetos.  
> Python-é-uma-linguagem-orientada-a-objetos.

```python
# Dividindo
x = 'Python é uma linguagem orientada a objetos'
print(x.split())
```
> ['Python', 'é', 'uma', 'linguagem', 'orientada', 'a', 'objetos']

```python
# Separando linhas

Manoel = """Todas as coisas cujos valores podem ser
disputados no cuspe à distância
servem para a poesia

O homem que possui um pente
e uma árvore
serve para poesia"""

print(Manoel.splitlines())
```
> ['Todas as coisas cujos valores podem ser', 'disputados no cuspe à distância', 'servem para a poesia', '', 'O homem que possui um pente', 'e uma árvore', 'serve para poesia']

```python
# join()

x = '---a---'.join(['casa', 'amarela', 'azul'])
print(x)
```
> casa---a---amarela---a---azul



# f-strings

* Introduzidas na versão 3.6
* https://www.python.org/dev/peps/pep-0536/

```python
x = 20
texto = 'Python'

print( f'{x} {texto}')
```
> 20 Python

```python
# Podem conter expressões

x = 2
y = 3
print(f'{x+y**2}')
```
> 11

```python
# Podem incluir formatação
x = 1/3
print(f'{x:.6e}')
```
> 3.333333e-01

```python
# Podem incluir código complicado

s = 'inês pereira'

print(f'{s.upper()} e {s.title()}')
```
> INÊS PEREIRA e Inês Pereira

```python
# Aninhamento de f-strings. Pode ficar confuso!

x = 2.2

print(f'{x:.3f}')
print(f'{x:.3f}'.replace('.', ','))
print(f"{   f'{x:.3f}'.replace('.', ',')   } é a representação de {x} com vírgulas." )
```
> 2.200  
> 2,200  
> 2,200 é a representação de 2.2 com vírgulas.

```python
# Obs f-strings produzem strings normais. Não se trata de produzir
# uma classe diferente de strings.

x = 1/3

s = f'{x:.4f}'
print(type(s), type('1/3'))
```
> <class 'str'> <class 'str'>



# Formatação tipo C.
* The not so good old style

```python
# The not so good old style

x = "O número é %d." % 10
print(x)
```
> O número é 10.

```python
# Você pode inserir comandos de formatação

print("O número é %.6f." % 10)
```
> O número é 10.000000.

```python
# Você pode inserir múltiplas entradas

print("Os números são %.6f e %g." % (10, 3.03))
```
> Os números são 10.000000 e 3.03.



# Expressões Regulares
* Vulgo regex
* https://docs.python.org/pt-br/3.8/howto/regex.html
* https://docs.python.org/3/library/re.html
* Testes em https://pythex.org/

```python
import re
```

```python
x = 'Python é uma linguagem orientada a objetos.'

print(re.match(r'Py', x)) # r = raw
print(re.match(r'yt', x))
print(re.match(r'P.t..n', x)) # . = qualquer caracter exceto nova linha
print(re.match(r'P[ayi]', x)) # . = qualquer caracter dentro dos colchetes.
```
> <\_sre.SRE\_Match object; span=(0, 2), match='Py'>  
> None  
> <\_sre.SRE\_Match object; span=(0, 6), match='Python'>  
> <\_sre.SRE\_Match object; span=(0, 2), match='Py'>

```python
print(r'ab\nc', 'ab\nc')
```
> ab\nc ab  
> c

```python
x = 'Python é uma linguagem orientada a objetos.'.split()
print(x,'\n')
for palavra in x:
    print(palavra.ljust(20), re.match(r'[A-Zaol][rb]', palavra))
```
> ['Python', 'é', 'uma', 'linguagem', 'orientada', 'a', 'objetos.']
>
> Python               None  
> é                    None  
> uma                  None  
> linguagem            None  
> orientada            <\_sre.SRE\_Match object; span=(0, 2), match='or'>  
> a                    None  
> objetos.             <\_sre.SRE\_Match object; span=(0, 2), match='ob'>

```python
x = 'Uma string pode conter números como 10, 20 e 33.'

m = re.search(r'[a-z]n', x)
print(m)

m = re.search(r'[a-z]m', x)
print(m)

m = re.search(r'[0-9]', x)
print(m)
```
> <\_sre.SRE\_Match object; span=(7, 9), match='in'>  
> <\_sre.SRE\_Match object; span=(32, 34), match='om'>  
> <\_sre.SRE\_Match object; span=(36, 37), match='1'>

```python
x = 'Carlos, Marcelo, Maria e Carla'

m = re.search(r'[A-Za-z]*', x)  # * permite repetições (zero ou mais) do caractere anterior
print(m)

m = re.search(r'M.*', x)  # .* = Qualquer coisa de qualquer tamanho
print(m)

m = re.search(r'[A-Za-z\s]*,', x)  # * = Qualquer tamanho, \s = espaço em branco
print(m)

m = re.search(r'^[A-Za-z]', x)  #  ^ = negação
print(m)

m = re.search(r'\sM', x)  
print(m)

m = re.search(r'(.)..\1', x) # (.) campo formado por um caractere qualquer.
print(m)
```
> <\_sre.SRE\_Match object; span=(0, 6), match='Carlos'>  
> <\_sre.SRE\_Match object; span=(8, 30), match='Marcelo, Maria e Carla'>  
> <\_sre.SRE\_Match object; span=(0, 7), match='Carlos,'>  
> <\_sre.SRE\_Match object; span=(0, 1), match='C'>  
> <\_sre.SRE\_Match object; span=(7, 9), match=' M'>  
> <\_sre.SRE\_Match object; span=(18, 22), match='aria'>  

```python
# Case insensitive

x= 'Casa Bela'
m = re.search(r'BELA', x, flags=re.IGNORECASE)
print(m)
```
> <\_sre.SRE\_Match object; span=(5, 9), match='Bela'>

```python
# Procurando todas a ocorrências

x = """Vozes veladas, veludosas vozes,
Volúpias dos violões, vozes veladas,
Vagam nos velhos vórtices velozes
Dos ventos, vivas, vãs, vulcanizadas.""" # Cruz e Sousa

print(re.findall(r'v.*?\s', x, flags=re.IGNORECASE))
# *? qualquer quantidade, mas o mínimo possível
```
> ['Vozes ', 'veladas, ', 'veludosas ', 'vozes,\n', 'Volúpias ', 'violões, ', 'vozes ', 'veladas,\n', 'Vagam ', 'velhos ', 'vórtices ', 'velozes\n', 'ventos, ', 'vivas, ', 'vãs, ']

```python
# É possível iterar
for i in re.finditer(r'v.*?\s', x, flags=re.IGNORECASE):
    print(i)
```
> <\_sre.SRE\_Match object; span=(0, 6), match='Vozes '>  
> <\_sre.SRE\_Match object; span=(6, 15), match='veladas, '>  
> <\_sre.SRE\_Match object; span=(15, 25), match='veludosas '>  
> <\_sre.SRE\_Match object; span=(25, 32), match='vozes,\n'>  
> <\_sre.SRE\_Match object; span=(32, 41), match='Volúpias '>  
> <\_sre.SRE\_Match object; span=(45, 54), match='violões, '>  
> <\_sre.SRE\_Match object; span=(54, 60), match='vozes '>  
> <\_sre.SRE\_Match object; span=(60, 69), match='veladas,\n'>  
> <\_sre.SRE\_Match object; span=(69, 75), match='Vagam '>  
> <\_sre.SRE\_Match object; span=(79, 86), match='velhos '>  
> <\_sre.SRE\_Match object; span=(86, 95), match='vórtices '>  
> <\_sre.SRE\_Match object; span=(95, 103), match='velozes\n'>  
> <\_sre.SRE\_Match object; span=(107, 115), match='ventos, '>  
> <\_sre.SRE\_Match object; span=(115, 122), match='vivas, '>  
> <\_sre.SRE\_Match object; span=(122, 127), match='vãs, '>

```python
# Compilando

regex_compilado = re.compile(r'v.*?\s')
print(regex_compilado.findall(x))
```
> ['veladas, ', 'veludosas ', 'vozes,\n', 'violões, ', 'vozes ', 'veladas,\n', 'velhos ', 'vórtices ', 'velozes\n', 'ventos, ', 'vivas, ', 'vãs, ']



# Distância de string

* Existem inúmeros algoritmos para comparar strings: distância de edição, sequências contidas, fonéticos etc.

* https://pypi.org/project/textdistance/

```python
!pip install textdistance
import textdistance
```

```python
# distância de hamming -

print(textdistance.hamming('Python', 'Python'))  # Distância entre strings iguais é 0
print(textdistance.hamming('Python', 'Pithon'))  # Um caractere diferente
print(textdistance.hamming('Python', 'Pytho'))   # Um caractere faltante
print(textdistance.hamming('Python', 'Ptyhon'))  # Dois caracteres diferentes
print(textdistance.hamming('Python', 'abc'))     # Todos diferentes
print(textdistance.hamming('Python', 'ython'))   # Todos diferentes
```
> 0  
> 1  
> 1  
> 2  
> 6  
> 6

```python
# distância de Levenshtein
# Número mínimo de edições para transformar uma string na outra.
# Inclui inserções, eliminações e substituições de caracteres

print(textdistance.levenshtein('Python', 'Python'))  # Distância entre strings igais é 0
print(textdistance.levenshtein('Python', 'Pithon'))  # Um caractere diferente
print(textdistance.levenshtein('Python', 'Pytho'))   # Um caractere faltante
print(textdistance.levenshtein('Python', 'Ptyhon'))  # Dois caracteres diferentes
print(textdistance.levenshtein('Python', 'abc'))     # Todos diferentes
print(textdistance.levenshtein('Python', 'ython'))   # Todos diferentes, mas basta inserir 1
```
> 0  
> 1  
> 1  
> 2  
> 6  
> 1

```python
# distância de Damerau-Levenshtein
# Número mínimo de edições para transformar uma string na outra.
# Inclui inserções, eliminações, transposições e substituições de caracteres

print(textdistance.damerau_levenshtein('Python', 'Python'))  # Distância entre strings igais é 0
print(textdistance.damerau_levenshtein('Python', 'Pithon'))  # Um caractere diferente
print(textdistance.damerau_levenshtein('Python', 'Pytho'))   # Um caractere faltante
print(textdistance.damerau_levenshtein('Python', 'Ptyhon'))  # Dois caracteres diferentes, mas basta transpor
print(textdistance.damerau_levenshtein('Python', 'abc'))     # Todos diferentes
print(textdistance.damerau_levenshtein('Python', 'ython'))   # Todos diferentes, mas basta inserir 1
```
> 0  
> 1  
> 1  
> 1  
> 6  
> 1

```python
import prettytable

tabela = prettytable.PrettyTable()
tabela.field_names = ['String', 'Hamming', 'Levenshtein',
                      'Damerau-Levenshtein', 'Jaro–Winkler (s)',
                      'Strcmp95 (s)']

lista = ['Python', 'Pytho', 'Pithon', 'Piton', 'Paithon', 'Paiton', 'Pthon',
         'Qython', 'nohtyP', 'yPhtno']
criterios = [textdistance.hamming, textdistance.levenshtein,
             textdistance.damerau_levenshtein, textdistance.jaro,
             textdistance.strcmp95]

for palavra in lista:
    distancias = []
    for criterio in criterios:
        distancias.append(criterio('Python', palavra))

    tabela.add_row([palavra] + distancias)

tabela.align["String"] = 'l'

print(tabela)
```
> +---------+---------+-------------+---------------------+---------------------+---------------------+  
> | String  | Hamming | Levenshtein | Damerau-Levenshtein |   Jaro–Winkler (s)  |     Strcmp95 (s)    |  
> +---------+---------+-------------+---------------------+---------------------+---------------------+  
> | Python  |    0    |      0      |          0          |          1          |          1          |  
> | Pytho   |    1    |      1      |          1          |  0.9444444444444445 |  0.9666666666666667 |  
> | Pithon  |    1    |      1      |          1          |  0.888888888888889  |  0.9299999999999999 |  
> | Piton   |    4    |      2      |          2          |  0.8222222222222223 |        0.873        |  
> | Paithon |    6    |      2      |          2          |  0.8492063492063492 |  0.8921428571428571 |  
> | Paiton  |    3    |      3      |          3          |  0.7777777777777777 |  0.8300000000000001 |  
> | Pthon   |    5    |      1      |          1          |  0.9444444444444445 |  0.9500000000000001 |  
> | Qython  |    1    |      1      |          1          |  0.888888888888889  |  0.888888888888889  |  
> | nohtyP  |    6    |      6      |          5          | 0.38888888888888884 | 0.38888888888888884 |  
> | yPhtno  |    6    |      4      |          3          |  0.8333333333333334 |  0.8333333333333334 |  
> +---------+---------+-------------+---------------------+---------------------+---------------------+

```python
# Comparações fonéticas (em inglês)
tabela = prettytable.PrettyTable()
tabela.field_names = ['String', 'Damerau-Levenshtein', 'Editex', 'MRA (s)']

lista = ['Helena', 'Helen', 'Elena', 'Hellen', 'Yelena', 'Yellow', 'eHelan']
criterios = [textdistance.damerau_levenshtein, textdistance.editex,
             textdistance.mra]

for palavra in lista:
    distancias = []
    for criterio in criterios:
        distancias.append(criterio('Helena', palavra))

    tabela.add_row([palavra] + distancias)

tabela.align["String"] = 'l'

print(tabela)
```
> +--------+---------------------+--------+---------+  
> | String | Damerau-Levenshtein | Editex | MRA (s) |  
> +--------+---------------------+--------+---------+  
> | Helena |          0          |   0    |    3    |  
> | Helen  |          1          |   2    |    3    |  
> | Elena  |          2          |   2    |    2    |  
> | Hellen |          2          |   2    |    3    |  
> | Yelena |          1          |   2    |    2    |  
> | Yellow |          4          |   7    |    1    |  
> | eHelan |          3          |   5    |    0    |  
> +--------+---------------------+--------+---------+

```python
lista = ['Elliana', 'Elianna', 'Aliana', 'Alianna', 'Ellianna', 'Elyana',
 'Eliyanah', 'Alyanna', 'Aliyana', 'Alyana', 'Eleana', 'Ellyana', 'Aliyanna']

criterios = [textdistance.damerau_levenshtein, textdistance.editex]
nome_criterios = ['Damerau Levenshtein', 'Editex']

print('{} / {}'.format(*nome_criterios))

tabela = prettytable.PrettyTable()
tabela.field_names = ['nome'] + lista
for i in range(len(lista)):
    row = [lista[i]]
    for j in range(len(lista)):
        d0 = criterios[0](lista[i], lista[j])
        d1 = criterios[1](lista[i], lista[j])
        row.append('{} / {}'.format(d0, d1) if i<=j else '')
    tabela.add_row(row)
print(tabela)
```
> Damerau Levenshtein / Editex  
> +----------+---------+---------+--------+---------+----------+--------+----------+---------+---------+--------+--------+---------+----------+  
> |   nome   | Elliana | Elianna | Aliana | Alianna | Ellianna | Elyana | Eliyanah | Alyanna | Aliyana | Alyana | Eleana | Ellyana | Aliyanna |  
> +----------+---------+---------+--------+---------+----------+--------+----------+---------+---------+--------+--------+---------+----------+  
> | Elliana  |  0 / 0  |  2 / 0  | 2 / 1  |  3 / 1  |  1 / 0   | 2 / 1  |  3 / 3   |  4 / 2  |  3 / 2  | 3 / 2  | 2 / 1  |  1 / 1  |  4 / 2   |  
> | Elianna  |         |  0 / 0  | 2 / 1  |  1 / 1  |  1 / 0   | 2 / 1  |  3 / 3   |  2 / 2  |  3 / 2  | 3 / 2  | 2 / 1  |  3 / 1  |  2 / 2   |  
> |  Aliana  |         |         | 0 / 0  |  1 / 0  |  3 / 1   | 2 / 2  |  3 / 4   |  2 / 1  |  1 / 1  | 1 / 1  | 2 / 2  |  3 / 2  |  2 / 1   |  
> | Alianna  |         |         |        |  0 / 0  |  2 / 1   | 3 / 2  |  4 / 4   |  1 / 1  |  2 / 1  | 2 / 1  | 3 / 2  |  4 / 2  |  1 / 1   |  
> | Ellianna |         |         |        |         |  0 / 0   | 3 / 1  |  4 / 3   |  3 / 2  |  4 / 2  | 4 / 2  | 3 / 1  |  2 / 1  |  3 / 2   |  
> |  Elyana  |         |         |        |         |          | 0 / 0  |  2 / 4   |  2 / 1  |  2 / 3  | 1 / 1  | 1 / 1  |  1 / 0  |  3 / 3   |  
> | Eliyanah |         |         |        |         |          |        |  0 / 0   |  4 / 5  |  2 / 3  | 3 / 5  | 3 / 4  |  2 / 4  |  3 / 3   |  
> | Alyanna  |         |         |        |         |          |        |          |  0 / 0  |  2 / 2  | 1 / 0  | 3 / 2  |  3 / 1  |  1 / 2   |  
> | Aliyana  |         |         |        |         |          |        |          |         |  0 / 0  | 1 / 2  | 3 / 3  |  2 / 3  |  1 / 0   |  
> |  Alyana  |         |         |        |         |          |        |          |         |         | 0 / 0  | 2 / 2  |  2 / 1  |  2 / 2   |  
> |  Eleana  |         |         |        |         |          |        |          |         |         |        | 0 / 0  |  2 / 1  |  4 / 3   |  
> | Ellyana  |         |         |        |         |          |        |          |         |         |        |        |  0 / 0  |  3 / 3   |  
> | Aliyanna |         |         |        |         |          |        |          |         |         |        |        |         |  0 / 0   |  
> +----------+---------+---------+--------+---------+----------+--------+----------+---------+---------+--------+--------+---------+----------+

```python
lista = ['Tiago', 'Thiago', 'Tyago', 'Thyago', 'Tiagho', 'Thiagho',
         'Tyagho', 'Thyagho']

criterios = [textdistance.damerau_levenshtein, textdistance.editex]
nome_criterios = ['Damerau Levenshtein', 'Editex']
print('Como funciona em português?')
print('{} / {}'.format(*nome_criterios))

tabela = prettytable.PrettyTable()
tabela.field_names = ['nome'] + lista
for i in range(len(lista)):
    row = [lista[i]]
    for j in range(len(lista)):
        d0 = criterios[0](lista[i], lista[j])
        d1 = criterios[1](lista[i], lista[j])
        row.append('{} / {}'.format(d0, d1) if i<=j else '')
    tabela.add_row(row)
print(tabela)
```
> Como funciona em português?  
> Damerau Levenshtein / Editex  
> +---------+-------+--------+-------+--------+--------+---------+--------+---------+  
> |   nome  | Tiago | Thiago | Tyago | Thyago | Tiagho | Thiagho | Tyagho | Thyagho |  
> +---------+-------+--------+-------+--------+--------+---------+--------+---------+  
> |  Tiago  | 0 / 0 | 1 / 2  | 1 / 1 | 2 / 3  | 1 / 2  |  2 / 4  | 2 / 3  |  3 / 5  |  
> |  Thiago |       | 0 / 0  | 2 / 3 | 1 / 1  | 2 / 4  |  1 / 2  | 3 / 5  |  2 / 3  |  
> |  Tyago  |       |        | 0 / 0 | 1 / 2  | 2 / 3  |  3 / 5  | 1 / 2  |  2 / 4  |  
> |  Thyago |       |        |       | 0 / 0  | 3 / 5  |  2 / 3  | 2 / 4  |  1 / 2  |  
> |  Tiagho |       |        |       |        | 0 / 0  |  1 / 2  | 1 / 1  |  2 / 3  |  
> | Thiagho |       |        |       |        |        |  0 / 0  | 2 / 3  |  1 / 1  |  
> |  Tyagho |       |        |       |        |        |         | 0 / 0  |  1 / 2  |  
> | Thyagho |       |        |       |        |        |         |        |  0 / 0  |  
> +---------+-------+--------+-------+--------+--------+---------+--------+---------+



# Aplicação
* Recuperando dados de páginas web

```python
import urllib

url = 'http://ti.saude.rs.gov.br/covid19/'
with urllib.request.urlopen(url) as f:
    conteudo = f.read()
# print(conteudo)
```

```python
import ast  # (Abstract Syntax Trees) https://docs.python.org/3/library/ast.html

# Busca posição de variável JavaScript
inicio = conteudo.find(b'<script>')
inicio = conteudo.find(b'=', inicio) + 1
fim = conteudo.find(b']') + 1

variavel = conteudo[inicio:fim].replace(b'lat', b'"lat"').replace(b'lng', b'"lng"')

# Analisa a variável e cria uma variável python com o mesmo conteúdo
cidades = ast.literal_eval(variavel.decode().lstrip())

# Mostra estrutura obtida
for i, cidade in enumerate(cidades):
    print(i, cidade)
    if i==5:
        break

# Converte entradas em string para inteiro
for i in range(len(cidades)):
    cidades[i]['total'] = int(cidades[i]['total'])
    cidades[i]['cv'] = int(cidades[i]['cv']) # Incidência por 100.000?
    cidades[i]['populacao'] = int(cidades[i]['populacao'].replace('.', ''))

print()

# Mostra como ficou
for i, cidade in enumerate(cidades):
    print(i, cidade)
    if i==5:
        break
```

```python
# Ordena a lista de cidades conforme chave dada
cidades.sort(key = lambda x: x['total']/x['populacao'], reverse=True )  # Tente outras chaves

for i, cidade in enumerate(cidades):
    print(i, cidade)
    if i==5:
        break
```

```python
# Agora vamos olhar para evolução do número total de casos

from datetime import datetime as dt

# Busca posição de variável JavaScript
inicio = conteudo.find(b'("GraphTotalCasos")')
inicio = conteudo.find(b'[', inicio)
fim = conteudo.find(b']', inicio) + 1

variavel = conteudo[inicio:fim]

datas = ast.literal_eval(variavel.decode().lstrip()) # Recupera as datas


# Vamos procurar o número de casos
inicio = conteudo.find(b'data:', fim)+5
inicio = conteudo.find(b'[', inicio)
fim = conteudo.find(b']', inicio) + 1

variavel = conteudo[inicio:fim]

# Analisa a variável e cria uma variável python com o mesmo conteúdo
numero_de_casos = ast.literal_eval(variavel.decode().lstrip())

for i in range(len(datas)):
    datas[i] =  dt.strptime(datas[i]+'/20', '%d/%m/%y')

print(datas)
print(numero_de_casos)
```

```python
import matplotlib.pyplot as plt
import matplotlib.ticker as ticker

fig, ax = plt.subplots()

ax.plot(datas, numero_de_casos)

# Ajusta ticks a 45 graus
plt.xticks(rotation=45)
ax.xaxis.set_major_locator(ticker.AutoLocator())

# Adiciona rótulo aos eixos
plt.ylabel("Número de casos", fontsize=14)

# Adiciona grade
ax.grid(True)

# Escala logaritmica
# ax.set_yscale('log')

# Título
fig.suptitle('Evolução número total de casos.')
fig.patch.set_facecolor('white')
fig.set_size_inches(10, 4)
```

```python
x = ['Fabio', 'Caio']

j = 0
for i, nome in enumerate(x):
    print(i, nome)
    j += 1
```
> 0 Fabio  
> 1 Caio
