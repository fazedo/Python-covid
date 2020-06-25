# Questão 1

* Construa um gerador que produz as vogais minúsculas em sequência.

```python
def vogais():
    yield 'a'
    yield 'e'
    yield 'i'
    yield 'o'
    yield 'u'

#[x for x in vogais()]
#[*vogais()]
#for x in vogais():
#    print(x)
f = vogais() # Instanciar

print(next(f))
print(next(f))
```
> a  
> e



# Questão 2

* Construa um gerador infinito que produz as vogais minúsculas em ciclo: a, e, i, o, u, a, e, i, ...

```python
def vogais():
    while True:
        yield 'a'
        yield 'e'
        yield 'i'
        yield 'o'
        yield 'u'

# Código de teste - deixar

for j, vogal in enumerate(vogais()):
    print (vogal)
    if j == 12:
        break
```
> a  
> e  
> i  
> o  
> u  
> a  
> e  
> i  
> o  
> u  
> a  
> e  
> i



# Questão 3

* Use uma função do itertools para simplificar o seguinte laço aninhado:

```python
import numpy as np
x = 0
for i in range(5):
    for j in range(6):
        x += np.cos(i + j**2)
print(x)
```

* Resuma a uma linha o código obtido usando a função sum() a um gerador adequado.

```python
# Primeira parte
import itertools as it
import numpy as np

x = 0
for i, j in it.product(range(5), range(6)):
    x += np.cos(i + j**2)
print(x)

# Segunda parte

x = sum(np.cos(i + j**2) for i, j in it.product(range(5), range(6)))
print(x)
```
> -0.09158289250374219  
> -0.09158289250374219



# Questão 4

* Um programador acostumado à linguagem C escreveu o seguinte código em Python:

```python
x = ['Relógio', 'Livro', 'Televisor', 'Grampeador']
y = ['amarelo', 'verde', 'vermelho', 'azul']

frases = ['', '', '', '']

for i in range(4):
    frases[i] = x + ' ' + y

print(frases)
```

* Reescreva o seguinte código de forma mais Pythônica.

```python
# Resolva aqui

x = ['Relógio', 'Livro', 'Televisor', 'Grampeador']
y = ['amarelo', 'verde', 'vermelho', 'azul']

frases = [i + ' ' + j for i, j in zip(x, y)]

print(frases)
```
> ['Relógio amarelo', 'Livro verde', 'Televisor vermelho', 'Grampeador azul']



# Questão 5

Para a lista x na questão anterior, escreva um laço que escreve no console:
```
Relógio tem 7 letras
Livro tem 5 letras
Televisor tem 9 letras
Grampeador tem 10 letras
```

```python
x = ['Relógio', 'Livro', 'Televisor', 'Grampeador']

for palavra in x:
    print('{} tem {} letras'.format(palavra, len(palavra)))

print()
# Ou
for palavra in x:
    print(f'{palavra} tem {len(palavra)} letras')
```
> Relógio tem 7 letras  
> Livro tem 5 letras  
> Televisor tem 9 letras  
> Grampeador tem 10 letras  
>   
> Relógio tem 7 letras  
> Livro tem 5 letras  
> Televisor tem 9 letras  
> Grampeador tem 10 letras



# Questão 6

* Escreva um laço para mostrar na tela os elementos da lista dada abaixo de forma alinhada:


```
lista[0] =    0.00000
lista[1] =    0.54030
lista[2] =   -1.66459
lista[3] =   -8.90993
lista[4] =  -10.45830
lista[5] =    7.09155
lista[6] =   34.56613
lista[7] =   36.94121
lista[8] =   -9.31200
lista[9] =  -73.80155
```

```python
import numpy as np

lista = [x**2 * np.cos(x) for x in range(10)]

for i, x in enumerate(lista):
    # print('lista[{}] = {:>10.5f}'.format(i, x))
    print(f'lista[{i}] = {x:>10.5f}')

    #print('lista[{}] = {:.5f}'.format(i, x))
```
> lista[0] =    0.00000  
> lista[1] =    0.54030  
> lista[2] =   -1.66459  
> lista[3] =   -8.90993  
> lista[4] =  -10.45830  
> lista[5] =    7.09155  
> lista[6] =   34.56613  
> lista[7] =   36.94121  
> lista[8] =   -9.31200  
> lista[9] =  -73.80155



# Questão 7

* Escreva uma expressão regular para casar com o nome 'Tiago' grafado com 'T' ou 'Th', 'i' ou 'y'.

```python
import re

lista  = ['Tiago', 'Thiago', 'Tyago', 'Thyago']
regex = 'Th?[iy]ago'

for nome in lista:
    print(re.match(regex, nome))
```
> <\_sre.SRE\_Match object; span=(0, 5), match='Tiago'>  
> <\_sre.SRE\_Match object; span=(0, 6), match='Thiago'>  
> <\_sre.SRE\_Match object; span=(0, 5), match='Tyago'>  
> <\_sre.SRE\_Match object; span=(0, 6), match='Thyago'>



# Questão 8

* Escreva uma expressão regular para casar com qualquer string de cinco caracteres começando com 'a' e terminando com 'z'

```python
lista = ['aefgz', 'aafiz', 'Aasao']
regex = 'a...z'
regex = 'a.{3}z'
for nome in lista:
    print(re.match(regex, nome))
```
> <\_sre.SRE_Match object; span=(0, 5), match='aefgz'>  
> <\_sre.SRE_Match object; span=(0, 5), match='aafiz'>  
> None



# Questão 9

* Construa expressões regulares para casar strings com as características abaixo. Depois teste na lista de nomes dada.

1. Nomes que começam com P.
2. Nomes que começam com P e têm cinco caracteres. Veja o operador '$'
3. Nomes que começam com P e contenham com a.
4. Nomes que começam com P e terminam com a.
5. Nomes que começam e terminam com vogais.
6. Nomes que contenham letras repetidas ('rr', 'ss', 'll' etc). Considere '(.)/1'.
7. Nomes que começam e terminam com a mesma letra.

* Dica: Entenda o que significa e use flags=re.IGNORECASE

```python
lista = ['Álvaro', 'Amanda', 'Ana', 'Andrea', 'Andressa', 'André', 'Ângelo',
         'Arthur', 'Artur', 'Bruno', 'Carla', 'Carolina', 'Cassia', 'Claudio',
         'César', 'Danilo', 'Diego', 'Douglas', 'Débora', 'Eduardo', 'Erick',
         'Esequia', 'Esthefany', 'Evelyn', 'Fabio', 'Felipe', 'Francisco',
         'Franz', 'Gabriel', 'Gabrieli', 'Gabrielle', 'Giovana', 'Giulio',
         'Greice', 'Guilherme', 'Gustavo', 'Hilarion', 'Ismael', 'Italo',
         'Janderson', 'Joao', 'Kiyo', 'Letícia', 'Lorenzo', 'Luana', 'Lucas',
         'Luisa', 'Luiza', 'Márcia', 'Maria', 'Mariana', 'Marisa', 'Miguel',
         'Murilo', 'Natan', 'Nathália', 'Nathalia', 'Paola', 'Patrick',
         'Paula', 'Pedro', 'Polyana', 'Rafael', 'Roberta', 'Rodrigo', 'Rogério',
         'Samuel', 'Sara', 'Shannon', 'Thaylles', 'Thiago', 'Tiago', 'Victor',
         'Vinicius', 'Vitor', 'Vitória', 'Wellington', 'Weslley', 'Yasmin']

regex_1 = r'p'
regex_2 = r'p....$'
regex_3 = r'p.*a'
regex_4 = r'p.*a$'
regex_5 = r'[aeiouáâ].*[aeiouáâ]$'
regex_6 = r'.*(.)\1'
regex_7 = r'(.).*\1$'

for nome in lista:
    if re.match(regex_4, nome, flags=re.IGNORECASE):
        print(nome)
```
> Paola  
> Paula  
> Polyana



# Distância

* Use a lista com 79 nomes dada no problema anterior e calcule as $\frac{78\times 79}{2}$ distâncias dois-a-dois. Ordene a lista em ordem crescente de distância.
* Teste mais de um algoritmo para distância/semelhança.

```python
!pip install textdistance
```
> Successfully installed textdistance-4.2.0

```python
import textdistance
import itertools as it

criterio = [textdistance.damerau_levenshtein, textdistance.editex][1]

distancias = [] # Lista vazia
for nome_1, nome_2 in it.combinations(lista, 2):
    distancias.append( (nome_1, nome_2, criterio(nome_1, nome_2)) )

distancias.sort(key=lambda x: (x[2], -(len(x[0])+len(x[1]))))
```

```python
for trio in filter(lambda x: x[2]<3, distancias): # Existe it.takewhile
    print('{:<12} {:<12} {}'.format(*trio))
```
> Gabrieli     Gabrielle    1  
> Luisa        Luiza        1  
> Paola        Paula        1  
> Gabriel      Gabrielle    2  
> Nathália     Nathalia     2  
> Gabriel      Gabrieli     2  
> Andrea       Andressa     2  
> Arthur       Artur        2  
> Maria        Marisa       2  
> Thiago       Tiago        2  
> Victor       Vitor        2  
> Diego        Tiago        2  
> Carla        Sara         2

```python
print(distancias)
```
> [('Gabrieli', 'Gabrielle', 1), ('Luisa', 'Luiza', 1), ('Paola', 'Paula', 1) ... ('Márcia', 'Wellington', 16), ('César', 'Wellington', 16), ('Esthefany', 'Miguel', 16)]
