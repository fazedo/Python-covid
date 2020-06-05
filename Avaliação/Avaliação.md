# Avaliação - grupo de estudos

## Critérios
As questões de múltipla escolha valem 5 pontos cada e as questões sim/não valem 2 pontos cada. O
teste inteiro soma 110 pontos. O conceito será calculado conforme o algoritmo a seguir:
```python
def conceito(nota):
if nota<50:
    return 'Não aprovado'
if nota<70:
    return 'C'
if nota<90:
    return 'B'
return 'A'
```
Você pode submeter múltiplas vezes as respostas se desejar.



## Questão 1
### Sobre inteiros no Python, é correto dizer:
- [ ] São limitados entre -9223372036854775808 e 9223372036854775807.
- [ ] São potencialmente ilimitados e podem representar números tão grandes como
necessários.
- [ ] São limitados a 16 dígitos.
- [ ] O Python não diferencia inteiro de ponto flutuante.



## Questão 2
### As variáveis da classe float.
- [ ] Estão limitados em tamanho e precisão. Aproximadamente 16 casas decimais.
- [ ] São potencialmente ilimitados e podem representar números tão grandes como
necessários.
- [ ] A expressão x==(x+1) é falsa para todos floats x.
- [ ] A expressão 1==(1+x) é falsa para todos floats x.



## Considere o código dado abaixo:
```python
lista = []
for x in range(10):
    x *= 2
    lista.append(x+1)
```


## Questão 3
### Este código é equivalente a:
- [ ] lista = [2*x + 1 for x in range(10)]
- [ ] lista = (2*x + 1 for x in range(10))
- [ ] lista = {2*(x +1) for x in range(10)]
- [ ] lista = (2*(x + 1) for x in range(10))
- [ ] Outro:



## Questão 4
### Se A é uma lista, é correto afirmar sobre a expressão len(A)==len({*A}):
- [ ] É sempre verdadeira.
- [ ] É sempre falsa.
- [ ] Não é possível prever o comportamento da expressão pois envolve objetos
- [ ] incompatíveis.
- [ ] É verdadeira quando a lista A é formada apenas por elementos distintos entre si.



## Questão 5
### Se S é uma string, o código S[4]='F' é inválido mesmo que o comprimento da string seja superior a 4. Como você contornaria essa limitação?
- [ ] S = S[:4] + 'F' + S[5:]
- [ ] S = S[:3] + 'F' + S[5:]
- [ ] S = S[:4] + 'F' + S[4:]
- [ ] S = S[:3] + 'F' + S[4:]



## Questão 6
### O código "f = lambda x: x**2 + 1":
- [ ] Define um float quando x é um inteiro.
- [ ] Define uma tupla de dois elemento.
- [ ] Define uma função.
- [ ] Define um gerador.



## Questão 7
### Sobre o código A['r'] = 23
- [ ] É inválido.
- [ ] É válido quando A é uma lista e a entrada 'r' estiver definida.
- [ ] É válido quando A é um dicionário, mas apenas se entrada 'r' estiver definida.
- [ ] É válido quando A é um dicionário.



## Considere o código abaixo:
```python
if x == 2:
    y = 4
else:
    y = 6
```


## Questão 8
### Este código é equivalente a
- [ ] y = 4 if x == 2 else 6
- [ ] y = 6 if x == 2 else 4
- [ ] x = 4 if y == 2 else 6
- [ ] x = 6 if y == 2 else 4



## Questão 9
### A string "compreensão" codificada em utf-8 é dada por:
- [ ] b'compreens\xc3\xa3o''
- [ ] b'compreens\xc3'
- [ ] b'compreens\xa3o\xc3'
- [ ] b'compreens\xe3o'



## Questão 10
### A condição de permanência de um laço while é x<0.7 e o bloco de repetição é x = 0.2*np.cos(x) + 0.8*x. A variável x vale 0 antes do laço. Assinale a alternativa com o valor de x ao final do laço:
- [ ] x = 0.7
- [ ] x = 0.7013170947599823
- [ ] x = 0.7138522814858099
- [ ] x = 0.7558452079675517
