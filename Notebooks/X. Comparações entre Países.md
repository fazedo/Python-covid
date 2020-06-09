# Comparações entre países

* Traça gráfico compararativo entre países.
* A variável min_casos na terceira célula determina o ponto inicial a ser traçado.
* Cada pais atingiu este limite em datas diferentes, logo a escala em x é relativa.
* A data inicial da cada país é mostrada na legenda ao lado do nome do país.

* OBS: Como os dados são diários, pode não acontecer um dia com dados confirmados exatamente igual a min_casos. Neste caso, a primeira data com número de casos igual ou superior é escolhida como inicial. A série é, então normalizada pela constante casos_min dividido pelo número de casos na data inicial. Isto pode levar a distorções, especialmente quando o mínimo de casos é grande.

```python
# Nesta célula, as seguintes operações são feitas:
# 1. A url do banco de dados é aberta.
# 2. Os dados são baixa numa string em formato csv
# 3. Os dados são convertidos em lista
# 4. A url é fechada com o fim da indentação da clásula with

import urllib       # https://docs.python.org/3.8/library/urllib.html
import csv          # https://docs.python.org/3.8/library/csv.html
import io           # https://docs.python.org/3.8/library/io.html

# https://github.com/CSSEGISandData/COVID-19/blob/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv
url = 'https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv'

# Library
with urllib.request.urlopen(url) as f:                  # Abre a url
    string_recebida_da_url = f.read().decode('utf-8')   # Lê o conteúdo e decodifica em utf-8
    conteudo_csv = csv.reader(io.StringIO(string_recebida_da_url)) # Transforma em iterador csv
    lista_com_dados = list(conteudo_csv)                # Desempacota numa lista

print(lista_com_dados)  # Observe o formato.
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
