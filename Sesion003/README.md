# Sesión 03: Preparación de datos
Dificultad 😀😀😀😀 (fácil)  
Uso de código: 🐍🐍 (poco)

## 3.1 Selección de filas y columnas
El archivo "hoteles-vienna.xlsx" contiene información de hoteles con habitaciones disponibles para cierto fin de semana. Aunque tenemos varias variables, solamente utilizaremos las siguientes:
- hotel_id: es un identificador que reemplaza el nombre del hotel por razones de confidencialidad. [Culitativas Nominales]
- accommodationtype: tipo de hospedaje [nominal]
- price: precio. [Cuantitativa de Razon]
- center1distance: distancia al centro [Cuantitativa de Razon]
- starrating: calificación de 1 a 5 estrellas (más es mejor).  [cualitativa Ordinal]
- guestreviewsrating: calificación promedio otorgada por los clientes. [Cunatitativa de intervalo]

- Discrtos:Entre dos valores cualquiera hay una cantidad finita de datos
- Continuos: Entre dos valores cualquiera hay una cantidad infinita de datos
- Longitudinales:Series de datos
- Corte de transversal: en un punto en el tiempo



```python
# Importa la biblioteca de pandas
import pandas as pd
```


```python
# Carga el archivo 'data/hotelbookingdata-vienna.xlsx'
df = pd.read_excel('data/hoteles-viena.xlsx')
```


```python
variables = ["hotel_id", "accommodationtype", "price", "center1distance",
             "starrating", "guestreviewsrating"]
# Selecciona las variables del listado en el dataframe
df = df[variables]
```

La base de datos abarca diferentes tipos de hospedajes. En un dataframe llamad 'df' podemos consultar qué categorías tiene una variable "A" y con qué frecuencia aparece mediante `df['A'].value_counts()`


```python
# Obtén la frecuencia por tipo de hospedaje
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 430 entries, 0 to 429
    Data columns (total 6 columns):
     #   Column              Non-Null Count  Dtype  
    ---  ------              --------------  -----  
     0   hotel_id            430 non-null    int64  
     1   accommodationtype   430 non-null    object 
     2   price               430 non-null    int64  
     3   center1distance     430 non-null    float64
     4   starrating          430 non-null    float64
     5   guestreviewsrating  395 non-null    float64
    dtypes: float64(3), int64(2), object(1)
    memory usage: 20.3+ KB



```python
# Selecciona las filas correspondientes a hoteles
df = df[df['accommodationtype'] == 'Hotel']
```


```python
# Consulta la información de las variables
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Index: 266 entries, 1 to 428
    Data columns (total 6 columns):
     #   Column              Non-Null Count  Dtype  
    ---  ------              --------------  -----  
     0   hotel_id            266 non-null    int64  
     1   accommodationtype   266 non-null    object 
     2   price               266 non-null    int64  
     3   center1distance     266 non-null    float64
     4   starrating          266 non-null    float64
     5   guestreviewsrating  265 non-null    float64
    dtypes: float64(3), int64(2), object(1)
    memory usage: 14.5+ KB



```python
# Revisa las primeras cinco filas
df.head(5)
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>hotel_id</th>
      <th>accommodationtype</th>
      <th>price</th>
      <th>center1distance</th>
      <th>starrating</th>
      <th>guestreviewsrating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>21897</td>
      <td>Hotel</td>
      <td>81</td>
      <td>1.7</td>
      <td>4.0</td>
      <td>3.95</td>
    </tr>
    <tr>
      <th>2</th>
      <td>21901</td>
      <td>Hotel</td>
      <td>85</td>
      <td>1.4</td>
      <td>4.0</td>
      <td>3.75</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21902</td>
      <td>Hotel</td>
      <td>83</td>
      <td>1.7</td>
      <td>3.0</td>
      <td>45.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>21903</td>
      <td>Hotel</td>
      <td>82</td>
      <td>1.2</td>
      <td>4.0</td>
      <td>3.95</td>
    </tr>
    <tr>
      <th>6</th>
      <td>21906</td>
      <td>Hotel</td>
      <td>103</td>
      <td>0.9</td>
      <td>4.0</td>
      <td>3.95</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Revisa las primeras cinco filas
df.tail(5)
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>hotel_id</th>
      <th>accommodationtype</th>
      <th>price</th>
      <th>center1distance</th>
      <th>starrating</th>
      <th>guestreviewsrating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>423</th>
      <td>22402</td>
      <td>Hotel</td>
      <td>95</td>
      <td>1.5</td>
      <td>4.0</td>
      <td>4.15</td>
    </tr>
    <tr>
      <th>424</th>
      <td>22403</td>
      <td>Hotel</td>
      <td>73</td>
      <td>1.5</td>
      <td>3.0</td>
      <td>3.45</td>
    </tr>
    <tr>
      <th>426</th>
      <td>22406</td>
      <td>Hotel</td>
      <td>185</td>
      <td>0.8</td>
      <td>5.0</td>
      <td>4.35</td>
    </tr>
    <tr>
      <th>427</th>
      <td>22407</td>
      <td>Hotel</td>
      <td>100</td>
      <td>1.0</td>
      <td>4.0</td>
      <td>4.45</td>
    </tr>
    <tr>
      <th>428</th>
      <td>22408</td>
      <td>Hotel</td>
      <td>58</td>
      <td>1.4</td>
      <td>3.0</td>
      <td>3.25</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.sample(5)
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>hotel_id</th>
      <th>accommodationtype</th>
      <th>price</th>
      <th>center1distance</th>
      <th>starrating</th>
      <th>guestreviewsrating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>355</th>
      <td>22321</td>
      <td>Hotel</td>
      <td>140</td>
      <td>7.8</td>
      <td>4.0</td>
      <td>3.55</td>
    </tr>
    <tr>
      <th>105</th>
      <td>22026</td>
      <td>Hotel</td>
      <td>127</td>
      <td>0.8</td>
      <td>4.0</td>
      <td>45.00</td>
    </tr>
    <tr>
      <th>203</th>
      <td>22140</td>
      <td>Hotel</td>
      <td>79</td>
      <td>1.3</td>
      <td>4.0</td>
      <td>3.75</td>
    </tr>
    <tr>
      <th>354</th>
      <td>22320</td>
      <td>Hotel</td>
      <td>99</td>
      <td>7.7</td>
      <td>3.0</td>
      <td>3.75</td>
    </tr>
    <tr>
      <th>118</th>
      <td>22039</td>
      <td>Hotel</td>
      <td>371</td>
      <td>0.5</td>
      <td>5.0</td>
      <td>4.65</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['accommodationtype'].count
```




    <bound method Series.count of 1      Hotel
    2      Hotel
    3      Hotel
    4      Hotel
    6      Hotel
           ...  
    423    Hotel
    424    Hotel
    426    Hotel
    427    Hotel
    428    Hotel
    Name: accommodationtype, Length: 266, dtype: object>



## 3.2 Datos duplicados
En algunas ocasiones puede haber datos duplicados en nuestra base de datos. Para visualizar los datos duplicados podemos usar *duplicated()* de la siguiente manera:
`df[df.duplicated()]`. Si nos interesa en la variable "A" en particular encontonces es `df[df['A'].duplicated()]`


```python
# Identifica los datos duplicados en todas las variables 
df[df.duplicated()]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>hotel_id</th>
      <th>accommodationtype</th>
      <th>price</th>
      <th>center1distance</th>
      <th>starrating</th>
      <th>guestreviewsrating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>129</th>
      <td>22050</td>
      <td>Hotel</td>
      <td>242</td>
      <td>0.0</td>
      <td>4.0</td>
      <td>4.85</td>
    </tr>
    <tr>
      <th>242</th>
      <td>22185</td>
      <td>Hotel</td>
      <td>84</td>
      <td>0.8</td>
      <td>3.0</td>
      <td>2.25</td>
    </tr>
  </tbody>
</table>
</div>



Una opción para eliminar datos duplicados es usar *drop_duplicates()*. En nuestro ejemplo sería: `df.drop_duplicates()`. Esto sólo elimina observaciones filas duplicadas en todas las variables.De manera predeterminada, solamente conserva la primera fila de ellas.  
En algunas ocasiones necesitaremos eliminar observaciones duplicadas en solamente algunas variables. En ese caso se puede agregar un listado con el argumento *subset*. En nuestro ejemplo: `df.drop_duplicates(subset=['hotel_id'])`


```python
# Elimina las observaciones duplicadas
df = df.drop_duplicates()
```


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Index: 264 entries, 1 to 428
    Data columns (total 6 columns):
     #   Column              Non-Null Count  Dtype  
    ---  ------              --------------  -----  
     0   hotel_id            264 non-null    int64  
     1   accommodationtype   264 non-null    object 
     2   price               264 non-null    int64  
     3   center1distance     264 non-null    float64
     4   starrating          264 non-null    float64
     5   guestreviewsrating  263 non-null    float64
    dtypes: float64(3), int64(2), object(1)
    memory usage: 14.4+ KB


## 3.3 Datos perdidos
Cuando se presentan datos perdidos, es necesario evaluar si los datos perdidos se puede considerar aleatorios o no aleatorios.

# se considera datos perdidos es de 5% razonable a 10% grabe
# problema metodologico




```python
# Identifica qué variables tienen valores perdidos con 'info()'
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Index: 264 entries, 1 to 428
    Data columns (total 6 columns):
     #   Column              Non-Null Count  Dtype  
    ---  ------              --------------  -----  
     0   hotel_id            264 non-null    int64  
     1   accommodationtype   264 non-null    object 
     2   price               264 non-null    int64  
     3   center1distance     264 non-null    float64
     4   starrating          264 non-null    float64
     5   guestreviewsrating  263 non-null    float64
    dtypes: float64(3), int64(2), object(1)
    memory usage: 14.4+ KB


Para identificar las filas con datos perdidos podemos usar `df[df.isna().any(axis=1)]`. El método *isna()* sirve para indicar qué valores son perdidos y el método *any* sirve para indicar qué filas tienen al menos un valor perdido.


```python
# Identifica qué observaciones tienen datos perdidos 
# ¿Qué característica tienen en común la mayoría?
df[df.isna().any(axis=1)]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>hotel_id</th>
      <th>accommodationtype</th>
      <th>price</th>
      <th>center1distance</th>
      <th>starrating</th>
      <th>guestreviewsrating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>14</th>
      <td>21916</td>
      <td>Hotel</td>
      <td>106</td>
      <td>0.7</td>
      <td>2.5</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



Los métodos más comunes para tratar con datos perdidos son:
- Borrar filas o columnas con datos perdidos.
- Agregar una variable que distinga los datos perdidos.
- Imputación simple: Reemplazar los datos perdidos con un valor calculado a partir de la misma variable.
- Imputación multivariada: Reemplazar los datos perdidos con un valor calculado a partir de otras variables.  

**Imputación univariada**  
La práctica más común es reemplazar los valores con la media, mediana o moda. Una opción es utilizar la biblioteca de pandas. La imputación con la media para una columna 'A' es:  
`df['A'] = df['A'].fillna(df['A'].mean())`  
La imputación con la mediana es  
`df['A'] = df['A'].fillna(df['A'].median())` 
La imputación con la moda es:  
`df['A'] = df['A'].fillna(df['A'].mode().iloc[0])` 

Utiliza la media para reemplazar valores perdidos


```python
# Consulta las variables que tienen datos perdidos con 'info()'

```


```python
# Reemplaza los valores perdidos con la media
df['guestreviewsrating'] = df['guestreviewsrating'].fillna(df['guestreviewsrating'].mean())
```


```python
df[df.isna().any(axis=1)]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>hotel_id</th>
      <th>accommodationtype</th>
      <th>price</th>
      <th>center1distance</th>
      <th>starrating</th>
      <th>guestreviewsrating</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Index: 264 entries, 1 to 428
    Data columns (total 6 columns):
     #   Column              Non-Null Count  Dtype  
    ---  ------              --------------  -----  
     0   hotel_id            264 non-null    int64  
     1   accommodationtype   264 non-null    object 
     2   price               264 non-null    int64  
     3   center1distance     264 non-null    float64
     4   starrating          264 non-null    float64
     5   guestreviewsrating  264 non-null    float64
    dtypes: float64(3), int64(2), object(1)
    memory usage: 14.4+ KB



```python
# Utilizando 'describe()' obtén las principales medidas numéricas de resumen
df.describe()
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>hotel_id</th>
      <th>price</th>
      <th>center1distance</th>
      <th>starrating</th>
      <th>guestreviewsrating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>264.000000</td>
      <td>264.000000</td>
      <td>264.000000</td>
      <td>264.000000</td>
      <td>264.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>22161.590909</td>
      <td>129.931818</td>
      <td>1.687500</td>
      <td>3.609848</td>
      <td>11.330989</td>
    </tr>
    <tr>
      <th>std</th>
      <td>147.742786</td>
      <td>103.565794</td>
      <td>1.794869</td>
      <td>0.743321</td>
      <td>15.398060</td>
    </tr>
    <tr>
      <th>min</th>
      <td>21897.000000</td>
      <td>33.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>2.250000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>22030.750000</td>
      <td>81.750000</td>
      <td>0.700000</td>
      <td>3.000000</td>
      <td>3.950000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>22169.500000</td>
      <td>102.000000</td>
      <td>1.100000</td>
      <td>4.000000</td>
      <td>4.350000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>22290.000000</td>
      <td>138.250000</td>
      <td>1.925000</td>
      <td>4.000000</td>
      <td>4.550000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>22408.000000</td>
      <td>1012.000000</td>
      <td>13.000000</td>
      <td>5.000000</td>
      <td>45.000000</td>
    </tr>
  </tbody>
</table>
</div>



Un dataframe lo podemos guardar con `df.to_excel('carpeta/archivo.xlsx', index=False)`


```python
# Exporta el dataframe depurado a la carpeta 'output'
df.to_excel('output/hoteles-viena.xlsx', index=False)
```

## 3.4 Valores atípicos
Los valores atípicos son valores muy alejados de la tendencia central de los datos. No es recomendable su eliminación automática, sino su revisión para evaluar si son parte o no de la muestra. Un método sencillo que podemos utilizar es el método del valor z.


```python
from scipy.stats import zscore

datos = df['price']
z_scores = zscore(datos)
valores_atipicos_z = df[abs(z_scores)>3]
valores_atipicos_z
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>hotel_id</th>
      <th>accommodationtype</th>
      <th>price</th>
      <th>center1distance</th>
      <th>starrating</th>
      <th>guestreviewsrating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>55</th>
      <td>21969</td>
      <td>Hotel</td>
      <td>513</td>
      <td>0.3</td>
      <td>5.0</td>
      <td>4.85</td>
    </tr>
    <tr>
      <th>61</th>
      <td>21976</td>
      <td>Hotel</td>
      <td>806</td>
      <td>0.3</td>
      <td>5.0</td>
      <td>4.55</td>
    </tr>
    <tr>
      <th>87</th>
      <td>22006</td>
      <td>Hotel</td>
      <td>544</td>
      <td>0.5</td>
      <td>5.0</td>
      <td>4.85</td>
    </tr>
    <tr>
      <th>172</th>
      <td>22100</td>
      <td>Hotel</td>
      <td>527</td>
      <td>0.4</td>
      <td>5.0</td>
      <td>4.85</td>
    </tr>
    <tr>
      <th>223</th>
      <td>22164</td>
      <td>Hotel</td>
      <td>587</td>
      <td>0.7</td>
      <td>5.0</td>
      <td>15.00</td>
    </tr>
    <tr>
      <th>302</th>
      <td>22252</td>
      <td>Hotel</td>
      <td>1012</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>4.35</td>
    </tr>
  </tbody>
</table>
</div>




```python
import numpy as np

datos = df['price']
q1 = np.percentile(datos, 25)
q3 = np.percentile(datos, 75)
iqr =q3-q1
limite_inf= q1-1.5*iqr
limite_sup= q3+1.5*iqr
valores_atipicos_iqr = df[(datos<limite_inf) | (datos>limite_sup)]
valores_atipicos_iqr
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>hotel_id</th>
      <th>accommodationtype</th>
      <th>price</th>
      <th>center1distance</th>
      <th>starrating</th>
      <th>guestreviewsrating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>53</th>
      <td>21967</td>
      <td>Hotel</td>
      <td>299</td>
      <td>0.1</td>
      <td>5.0</td>
      <td>4.55</td>
    </tr>
    <tr>
      <th>55</th>
      <td>21969</td>
      <td>Hotel</td>
      <td>513</td>
      <td>0.3</td>
      <td>5.0</td>
      <td>4.85</td>
    </tr>
    <tr>
      <th>61</th>
      <td>21976</td>
      <td>Hotel</td>
      <td>806</td>
      <td>0.3</td>
      <td>5.0</td>
      <td>4.55</td>
    </tr>
    <tr>
      <th>72</th>
      <td>21989</td>
      <td>Hotel</td>
      <td>261</td>
      <td>0.3</td>
      <td>5.0</td>
      <td>4.85</td>
    </tr>
    <tr>
      <th>87</th>
      <td>22006</td>
      <td>Hotel</td>
      <td>544</td>
      <td>0.5</td>
      <td>5.0</td>
      <td>4.85</td>
    </tr>
    <tr>
      <th>88</th>
      <td>22007</td>
      <td>Hotel</td>
      <td>252</td>
      <td>0.5</td>
      <td>5.0</td>
      <td>4.65</td>
    </tr>
    <tr>
      <th>89</th>
      <td>22008</td>
      <td>Hotel</td>
      <td>323</td>
      <td>0.5</td>
      <td>5.0</td>
      <td>4.55</td>
    </tr>
    <tr>
      <th>109</th>
      <td>22030</td>
      <td>Hotel</td>
      <td>226</td>
      <td>0.5</td>
      <td>5.0</td>
      <td>4.35</td>
    </tr>
    <tr>
      <th>110</th>
      <td>22031</td>
      <td>Hotel</td>
      <td>231</td>
      <td>0.1</td>
      <td>4.0</td>
      <td>4.45</td>
    </tr>
    <tr>
      <th>115</th>
      <td>22036</td>
      <td>Hotel</td>
      <td>384</td>
      <td>0.6</td>
      <td>5.0</td>
      <td>4.85</td>
    </tr>
    <tr>
      <th>118</th>
      <td>22039</td>
      <td>Hotel</td>
      <td>371</td>
      <td>0.5</td>
      <td>5.0</td>
      <td>4.65</td>
    </tr>
    <tr>
      <th>128</th>
      <td>22050</td>
      <td>Hotel</td>
      <td>242</td>
      <td>0.0</td>
      <td>4.0</td>
      <td>4.85</td>
    </tr>
    <tr>
      <th>165</th>
      <td>22092</td>
      <td>Hotel</td>
      <td>354</td>
      <td>0.4</td>
      <td>5.0</td>
      <td>4.55</td>
    </tr>
    <tr>
      <th>172</th>
      <td>22100</td>
      <td>Hotel</td>
      <td>527</td>
      <td>0.4</td>
      <td>5.0</td>
      <td>4.85</td>
    </tr>
    <tr>
      <th>223</th>
      <td>22164</td>
      <td>Hotel</td>
      <td>587</td>
      <td>0.7</td>
      <td>5.0</td>
      <td>15.00</td>
    </tr>
    <tr>
      <th>232</th>
      <td>22175</td>
      <td>Hotel</td>
      <td>240</td>
      <td>0.4</td>
      <td>5.0</td>
      <td>4.55</td>
    </tr>
    <tr>
      <th>249</th>
      <td>22193</td>
      <td>Hotel</td>
      <td>383</td>
      <td>1.9</td>
      <td>3.0</td>
      <td>45.00</td>
    </tr>
    <tr>
      <th>291</th>
      <td>22240</td>
      <td>Hotel</td>
      <td>333</td>
      <td>0.7</td>
      <td>5.0</td>
      <td>4.95</td>
    </tr>
    <tr>
      <th>302</th>
      <td>22252</td>
      <td>Hotel</td>
      <td>1012</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>4.35</td>
    </tr>
  </tbody>
</table>
</div>



## 3.5 Práctica 01

En el notebook 'Practica_S0301', carga la base de datos de hoteles de una ciudad diferente (Londres, Milán, Roma). Selecciona las variables utilizadas en el ejemplo y las filas correspondientes a los hoteles. Luego elimina duplicados y consulta y reemplaza datos perdidos en las variables numéricas. Compara los resultados de esa ciudad con Viena.


```python
df.describe()
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>hotel_id</th>
      <th>price</th>
      <th>center1distance</th>
      <th>starrating</th>
      <th>guestreviewsrating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>264.000000</td>
      <td>264.000000</td>
      <td>264.000000</td>
      <td>264.000000</td>
      <td>264.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>22161.590909</td>
      <td>129.931818</td>
      <td>1.687500</td>
      <td>3.609848</td>
      <td>11.330989</td>
    </tr>
    <tr>
      <th>std</th>
      <td>147.742786</td>
      <td>103.565794</td>
      <td>1.794869</td>
      <td>0.743321</td>
      <td>15.398060</td>
    </tr>
    <tr>
      <th>min</th>
      <td>21897.000000</td>
      <td>33.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>2.250000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>22030.750000</td>
      <td>81.750000</td>
      <td>0.700000</td>
      <td>3.000000</td>
      <td>3.950000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>22169.500000</td>
      <td>102.000000</td>
      <td>1.100000</td>
      <td>4.000000</td>
      <td>4.350000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>22290.000000</td>
      <td>138.250000</td>
      <td>1.925000</td>
      <td>4.000000</td>
      <td>4.550000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>22408.000000</td>
      <td>1012.000000</td>
      <td>13.000000</td>
      <td>5.000000</td>
      <td>45.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
