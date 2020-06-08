# Questão 1

Tente prever os valores de k e n ao final do laço while:
```python
k = 0
n = 1
while k<5:
    k += 1
    n *= 2
print(k, n)
```

```python
# Teste aqui
k = 0
n = 1
while k<5:
    k += 1
    n *= 2
print(k, n)
```
> 5 32



# Questão 2

Considere o seguinte código
```python
animais = ['gato', 'cachorro', 'porco']
i = 0
while i<3:
    print(animais[i])
    i += 1

```
Reescreva o laço usando for

```python
# Teste aqui
animais = ('gato', 'cachorro', 'porco')

for animal in animais:
    print(animal)
```
> gato  
> cachorro  
> porco



# Questão 3

Considere o código:
```python
x = input('Entre com uma palavra: ')
```

Esta função pede ao usuário digitar uma string. Inclua esta linha em um bloco de código que repita a pergunta até que uma string de 5 caracteres começando com vogal seja digitada.

```python
# Teste aqui
x = ''

while len(x) != 5 or x[0].lower() not in 'aeiou': # ~(A & B) = ~A | ~B
    x = input('Entre com uma palavra: ')
```
> Entre com uma palavra: oi  
> Entre com uma palavra: tchau  
> Entre com uma palavra: aeiou  



# Questão 4

Escreva um dicionário que ligue o nome dos seguintes países a seus repectivos em português:
* Brazil, Italy, USA, France, Spain

```python
# Teste aqui
dic = {'Brazil':'Brasil', 'Italy':'Itália', 'USA':'EUA', 'France':'França', 'Spain':'Espanha'}
dic['Italy']
dic['Singapore'] = 'Cingapura'
print(dic)
```
> {'Brazil': 'Brasil', 'Italy': 'Itália', 'USA': 'EUA', 'France': 'França', 'Spain': 'Espanha', 'Singapore': 'Cingapura'}



# Questão 5

Seja o dicionário:
```python
autores = {'Machado de Assis':['Dom Casmurro', 'Memórias Póstumas de Brás Cubas'],
           'Eça de Queirós':['Os Maias', 'O Crime do Padre Amaro']}
```

Usando um comando do Python, acrescente ao dicionário a entrada "Memorial de Aires" a Machado de Assis.

```python
# Teste aqui
autores = {'Machado de Assis':['Dom Casmurro', 'Memórias Póstumas de Brás Cubas'],
           'Eça de Queirós':['Os Maias', 'O Crime do Padre Amaro']}

autores['Machado de Assis'].append('Memorial de Aires')

print(autores)
```
> {'Machado de Assis': ['Dom Casmurro', 'Memórias Póstumas de Brás Cubas', 'Memorial de Aires'], 'Eça de Queirós': ['Os Maias', 'O Crime do Padre Amaro']}

```python
autores['Machado de Assis'][0] = 'Dom'

print(autores)
```
> {'Machado de Assis': ['Dom', 'Memórias Póstumas de Brás Cubas', 'Memorial de Aires'], 'Eça de Queirós': ['Os Maias', 'O Crime do Padre Amaro']}



# Questão 6

A partir do dicionário da questão anterior, escreva um laço for para mostrar o nome do autor e o número de obras listadas.

```python
# Teste aqui
for autor in autores:
    print(autor, len(autores[autor]))
```
> Machado de Assis 3  
> Eça de Queirós 2



# Questão 7

Escreva uma função que recebe um número qualquer de números como parâmetros e retorne o produto deles. Exemplo:
* f(2) = 2
* f(2, 3) = 6
* f(2, 3, 10) = 60
