# Lista de exercícios 2 - Grupo de estudo Python - COVID-19

# Questão 1 - Operações básicas

1.
```python
lista = [1, 2, 3, 4]
lista[0] = 5
print(lista)
```

2.
```python
lista = [1, 2, 3, 4]
lista[0] = lista[1]
print(lista)
```

3.
```python
lista = [1, 2, 3, 4]
lista.append(5)
print(lista)
```

4.
```python
lista = [1, 2, 3, 4]
lista = lista + lista[2:]
print(lista)
```

5.
```python
lista = [1, 2, 3, 4]
lista = lista + lista[2:]
print(lista)
```

6.
```python
lista = [1, 2, 3, 4]
lista[2:] = [7, 8]
print(lista)
```

```python
# Use este espaço para testes
lista = [1, 2, 3, 4]
lista[2:] = [5, 6]
print(lista)
```
> [1, 2, 5, 6]



# Questão 2 - Construindo listas a partir de outras listas e strings

Leia os códigos abaixo e tente prever o comportamento de cada um. Depois teste e confirme sua resposta.

1.
```python
lista = [7, 8, 9, 10, 11]
lista[1:4] = range(0, 3)
print (lista)
```

2.
```python
lista = [i**2 for i in range(1, 10)]
soma = sum (lista)
comprimento = len (lista)
print (soma, comprimento)
```

3.
```python
lista = [i for i in range(1, 10) if i<5]
print(lista)
```

4.
```python
palavra = 'Estatística'
lista = [i for i in palavra]
print(lista)
```

5.
```python
palavra = 'Estatística'
lista = [i for i in palavra if i<'s']
print(lista)
```

```python
string = 'Estatística'
lista = [c for c in string if c<'s']  

#lista2 = [*string]           # idêntico
print(lista)
```
> ['E', 'a', 'i', 'c', 'a']



# Questão 3 - Métodos e funções selecionadas

Rode os comandos a seguir e descubra o comportamento:

1.
```python
lista = ['Porto Alegre', 'Florianópolis', 'Curitiba']
lista.reverse()
print(lista)
```

2.
```python
lista = ['Porto Alegre', 'Florianópolis', 'Curitiba']
lista.sort()
print(lista)
```

3.
```python
lista = ['Porto Alegre', 'Florianópolis', 'Curitiba']
lista.sort(reverse=True)
print(lista)
```

4.
```python
lista = ['Porto Alegre', 'Florianópolis', 'Curitiba']
lista.sort(key=len)
print(lista)
```


5.
```python
import numpy as np
lista = [np.sin(x) for x in range(0, 10)]
lista.sort()
print(lista)
```

6.
```python
import numpy as np
lista = [0, 1, 2, 3, 4, 5, 6, 7]
print(lista)
lista.sort(key=np.sin)
print(lista)
lista_senos = [np.sin(x) for x in lista]
print(lista_senos)
```

6.
```python
nome = 'Luís Vaz de Camões'
lista = nome.split()
```

7.
```python
nome = 'Luís Vaz de Camões'
print(nome.replace('z', 's'))
```

# Atenção:
* Strings não imutáveis
* Listas são mútáveis

```python
nome = 'Luís Vaz de Camões'
novo_nome = nome.replace('z', 's')  # nome fica inalterado
lista = [3, 1, 2]
lista.sort()            # lista é alterada
```

```python
nome = 'Luís Vaz de Camões'
nome = nome.replace('z', 's')
print(nome)
nome = 'a' + nome[1:]
print(nome)
```
> Luís Vas de Camões  
> auís Vas de Camões



# Operador lógicos

Preveja o resultado

1.
```python
a = 2
b = 3
c = 10
d = 1

print(a>b or c>d) # True ou False?
print(a>b and c>d) # True ou False?
print(not a>b and c>d) # True ou False?

```

2.
```python
x = [1, 2, 3, 4, 5]
print(3 in x)
print(6 in x)
print(4 not in x)
```

```python
x = [1, 2, 3, 4, 5]
print(3 in x)
print(6 in x)
print(4 not in x)
```
> True  
> False  
> False

```python
# Loop = laço, exite o for e o while (depois)
for x in range(4, 10, 2): # (inicio, fim, passo)
    x = x+1
    print(x)

print(x)
```
> 5  
> 7  
> 9  
> 9
