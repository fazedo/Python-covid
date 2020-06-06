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
