# Funções definidas pelo usuário, lambda

# Questão 1
Escreva uma função que recebe um número inteiro entre 0 e 19 e retorna sua escrita por extenso. Exemplo: f(1) retorna 'um'.

# Questão 2
Crie uma outra função que funcione para todos os inteiros entre 0 e 99.

```python
# Espaço para trabalhar
def numero(x):
    lista = ['zero', 'um', 'dois', 'três', 'quatro']
    return lista[x]

# numero(2)

def numero99(x):
    dezenas =['', '', 'vinte', 'trinta', 'quarenta', 'cinquenta']
    if x<20:
        return numero(x)

    dezena = x//10 # Pega dezena: 27 => 2
    unidade = x%10 # Pega unidade: 27  => 7

    if unidade==0:
        return dezenas[dezena]

    return dezenas[dezena] + ' e ' + numero(unidade)

print(numero99(53))
```
> cinquenta e três

```python
print(25//10)
print(25%10)
str(25)[1]
```
> 2  
> 5  
> '5'



# Questao 3

* Leia a função dada.
* Descubra o que fazem os métodos split() e upper().
* Entenda o comportamento geral da função.

```python
def gera_iniciais(nome):
    lista_de_palavras = nome.split()
    iniciais = ""
    for palavra in lista_de_palavras:
        iniciais += palavra[0]

    return iniciais.upper()

x = "universidade federal do rio grande do sul"

print(gera_iniciais(x))
```
> UFDRGDS

```python
nome="Universidade Federal do Rio"
print(nome.split())
```
> ['Universidade', 'Federal', 'do', 'Rio']



# Questão 4

* Entenda a seguinte linha de comando:
```python
nome = "universidade federal do rio grande do sul"
lista_de_iniciais = [palavra[0] for palavra in nome.split()]
```

* Leia sobre o comando join() e comprenda o que ele faz. Teste as seguintes linhas:
```python
"123".join(['A', 'B'])
"".join(['A', 'B'])
```

* Entenda a seguinte linha de comando:
```python
nome = "universidade federal do rio grande do sul"
iniciais = "".join(palavra[0] for palavra in nome.split())
```

* Use o método upper() ao final da mesma linha para gerar letras maiúsculas.

* Escreva uma função lambda que substitua gera_iniciais()


```python
nome = "universidade federal do rio grande do sul"
lista_de_iniciais = [palavra[0] for palavra in nome.split()]
# print(lista_de_iniciais)
"".join(['s', 'f', 'p'])
```
> 'sfp'

```python
#@title Resposta. Para ver a resposta, clique com botão direito do mouse, form, show code.
f = lambda x: "".join(palavra[0] for palavra in x.split()).upper()
```
