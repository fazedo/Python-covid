# Lista de exercícios 3 - Grupo de estudo Python - COVID-19

# Comandos de repetição e seleção

1. Preveja o comportamento do seguinte código e depois teste:
```python
for x in [1, 2, 3, 0]:
    print(x)
```

2. Explique a diferença no comportamento entres os dois seguintes trechos de programa:
```python
S = 0
for x in [1, 2, 3]:
    S += x
    print(x)
```
e
```python
S = 0
for x in [1, 2, 3]:
    S += x
print(x)
```

3. Preveja o comportamento do seguinte código e depois teste:
```python
S = 0
for x in range(10):
    S += x**2
    print(x)
print(S)
```

4. Preveja o comportamento do seguinte código e depois teste:
```python
string = 'microfone'
string2 = ''
for x in string:
    if x>'i':
        print(x)
        string2 += x
print(string2)
```
5. Preveja o comportamento do seguinte código e depois teste:
```python
for x in [1, 2, 3]:
    for y in [10, 20, 30]:
        print(x+y)
```

6. Preveja o valor n ao final do loop:
```python
n = 0
for x in range(10):
    for y in range(10):
        if x != y:
            n += 1
```

7. Preveja o valor n ao final do loop:
```python
n = 0
for x in range(5):
    for y in range(5):
        if x<2 or y>3:
            n += 1
            print(x, y, n)
```

```python
# Espaço para testes

n = 0
for x in range(5):
    for y in range(5):
        if x<2 or y>3:
            n += 1
            print(x, y, n)
```
> 0 0 1  
> 0 1 2  
> 0 2 3  
> 0 3 4  
> 0 4 5  
> 1 0 6  
> 1 1 7  
> 1 2 8  
> 1 3 9  
> 1 4 10  
> 2 4 11  
> 3 4 12  
> 4 4 13



# Compreensão de listas

1. Escreva uma expressão em uma linha que faça a mesma coisa que o seguinte código.
```python
import numpy as np
lista = [] # Cria uma lista vazia
for x in 'Universidade Federal do Rio Grande do Sul':
        if x in 'aeiou':
            lista.append(x)
```

2. Qual alteração você faria para que o código acima incluísse as vogais maiúsculas?

3. Preveja o comportamento de:
```python
lista = [x for x in 'Universidade']
```

```python
import numpy as np
lista = [] # Cria uma lista vazia
for x in 'Universidade Federal do Rio Grande do Sul':
        if x.upper() in 'AEIOU':
            lista.append(x)

print(lista)
```
> ['U', 'i', 'e', 'i', 'a', 'e', 'e', 'e', 'a', 'o', 'i', 'o', 'a', 'e', 'o', 'u']



# Arrays do Numpy

1. Descreva o comportamento do seguinte código:
```python
import numpy as np
arr1 = np.array([1, 2, 3, 4])
arr2 = np.array([10, 20, 30, 40])
arr3 = arr1 + arr2
arr4 = arr1 * arr2
```

2. Descreva o comportamento do seguinte código:
```python
import numpy as np
arr1 = np.array([i**2 for i in range(10)])
arr2 = arr1[1:] - arr1[:-1]
```

3. Descreva o comportamento do seguinte código:
```python
import numpy as np
arr1 = np.zeros(10)
for i in range(len(arr1)):
    arr1[i] = 1 if i<5 else 2
```

4. Descreva o comportamento do seguinte código:
```python
import numpy as np
arr1 = np.array([1, 2, 3, 4, 5, 6])
print(arr1>3)
```


```python
# Espaço de testes
import numpy as np

arr1 = np.array([1, 2, 3, 4, 5, 6])
print(arr1>3)
# Booleanos.

x= True
y = False
if x:
    print(1)

x=['fabio', 'fabio', 2]
print(len(x[0]))
```
> [False False False  True  True  True]  
> 1  
> 5



# Leitura
Array do numpy não têm o método append.

Para inicializar, você pode usar comandos como:
```python
import numpy as np

A = np.zeros(10)
A = np.ones(10)
A = np.full(10,2)
```

OBS: Você pode criar uma nova array usando a função append:
```python
A = np.append(A, 3)
```
