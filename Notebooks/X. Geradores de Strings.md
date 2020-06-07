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

```python

```
>

```python

```
>

```python

```
>

```python

```
>

```python

```
>

```python

```
>

```python

```
>

```python

```
>

```python

```
>

```python

```
>

```python

```
>

```python

```
>

```python

```
>

```python

```
>
