# Lista de exercícios 1 - Grupo de estudo Python - COVID-19

# Questão 1

1. Leia o código abaixo e tente prever seu comportamento. Depois teste e confirme sua resposta.

```python
x = 3
y = 1
x += x**2 + y # Idêntico a x = x + x**2 +y
x = x + y
print (x)
```

2. Construa uma expressão que tenha como entrada uma variável x e calcule o valor de:

* $y=\sqrt{1+e^{x}}$

Dica: Use a biblioteca Numpy.

3. Explique a diferença entre as expressões abaixo. Depois teste e confirme sua resposta.

```python
x = 10/2/5
x = 10/(2/5)
```

4. Leia o código abaixo e tente prever seu comportamento. Depois teste e confirme sua resposta.

```python
x = 2
x = x + 2
x = x + 2
x = x + 2
```

5. Leia o código abaixo e tente prever seu comportamento. Depois teste e confirme sua resposta.

```python
x, y = 2, 3
print(x, y)

x, y = y, x
print(x, y)

x = y = 3
print(x, y)
```

```python
# Use este espaço para testar o código.
x, y = 2, 3 # x=2 e y=3
print(x, y)
x, y = y, x # swap
print(x,y)
```
> 2 3  
> 3 2



# Questão 3

1. Considere o código abaixo e tente prever seu comportamento, depois teste:

```python
#                   (-2)(-1)
#         012345678901
string = 'Universidade'
x = string[2]    #i
y = string[-1]   #e
z = string[2:5]  #ive
u = string[2:]   #iversidade
v = string[:5]   #Unive
```

2. Teste os seguintes comandos e entenda o que acontece:

```python
nome_1 = 'Bernardo'
nome_2 = 'Bianca'

print(nome_1 + nome_2)
print(nome_1 + nome_1)
print(2*nome_1 + 3*nome_2)
```

```python
import numpy as np
x = int(input("Entre com um número: "))
# x = '102' # x = 102
y = np.sqrt(1 + np.exp(x))
print(x, y)
```
> Entre com um número: 5  
> 5 12.223467556408721
