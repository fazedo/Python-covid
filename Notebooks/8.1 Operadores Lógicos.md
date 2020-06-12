# Operadores Lógicos

* Devem ser vacinadas todas as crianças entre 6 e 12 anos e os idosos acima de 65. Pessoas com mais de 80 anos não devem ser vacinadas.
* Todas pessoas cuja idade esteja no conjunto $[6,12]\bigcup [65,80)$ devem ser vacinadas.

Ela foi a primeira pessoa a abrir a porta do prédio.

```python
def f(idade):  # True se deve ser vacinado ou False se não deve
    return (6 <= idade <= 12) or  (65 <= idade < 80)
```

```python
def f(idade):
    if 6 <= idade <= 12:
        return True
    if 65 <= idade < 80:
        return True
    return False
```

```python
def f(idade):
    if idade<6 or idade>=80:
        return False
    if idade>12 and idade<65:
        return False
    return True    
```

```python
def f(idade):
    #return not (idade<6 or idade>=80 or 12<idade<65)
    return not (idade<6 or idade>=80 or (idade>12 and idade<65))
```

```python
def f(idade):
    t6  = (idade >= 6)
    t12 = (idade <= 12)
    t65 = (idade >= 65)
    t80 = (idade <80)

    return t6 and t12 or t65 and t80
```

```python
# Avaliação curto-circuito.
def f():
    print('Olá!')
    return False
```
>

```python
x = 2
(x==2) and f()
x = 2
```
> Olá!

```python
x = 2
y = 2

if (x==2) != (y==3):  # xor =  ou exclusivo
    print('Aqui')
```
> Aqui
