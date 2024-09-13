# Sesión 05: Relaciones entre variables
Dificultad 😀😀😀 (regular)  
Uso de código: 🐍🐍 (poco)

## 5.1 Introducción
¿Cómo evaluar si dos variables cualitativas están relacionadas? Una forma inicial de explorar la relación entre dos variables cualitativas es mediante una tabla cruzada.  
Para la siguiente práctica utilizaremos el archivo "b03_enigh2020"


```python
# Importa la biblioteca de pandas, numpy y matplotlib.pyplot
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```


```python
# Carga el archivo con la base de datos
df = pd.read_excel('data/b03_enigh2020.xlsx')
```


```python
# Obtén las dimensiones de la base de datos
df.shape
```




    (2332, 24)




```python
# Explora la información básica de las variables
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 2332 entries, 0 to 2331
    Data columns (total 24 columns):
     #   Column      Non-Null Count  Dtype  
    ---  ------      --------------  -----  
     0   folioviv    2332 non-null   int64  
     1   ubica_geo   2332 non-null   object 
     2   clave_mun   2332 non-null   int64  
     3   tam_loc     2332 non-null   int64  
     4   est_socio   2332 non-null   object 
     5   clase_hog   2332 non-null   object 
     6   sexo_jefe   2332 non-null   object 
     7   edad_jefe   2332 non-null   int64  
     8   educa_jefe  2332 non-null   int64  
     9   tot_integ   2332 non-null   int64  
     10  hombres     2332 non-null   int64  
     11  mujeres     2332 non-null   int64  
     12  p65mas      2332 non-null   int64  
     13  ing_cor     2332 non-null   float64
     14  gasto_mon   2332 non-null   float64
     15  alimentos   2332 non-null   float64
     16  cereales    2332 non-null   float64
     17  carnes      2332 non-null   float64
     18  leche       2332 non-null   float64
     19  huevo       2332 non-null   float64
     20  bebidas     2332 non-null   float64
     21  agua        2332 non-null   float64
     22  energia     2332 non-null   float64
     23  cuida_pers  2332 non-null   float64
    dtypes: float64(11), int64(9), object(4)
    memory usage: 437.4+ KB


# Obtén la estadística descriptiva
df.describe().T

## 5.2 Tabla cruzada

Una forma básica de realizar una tabla cruzada es mediante el método *crosstab* de Pandas, especificando las variables en las filas y columnas respectivamente. Por ejemplo, para las variables "A" y "B", utilizaremos:  
`pd.crosstab(df['A'], df['B'], margins=True)`
El argumento *margins* se puede agregar para mostrar la suma por fila o columna. Cada celda dentro de la tabla mostrará la frecuencia observada en esa intersección.  


Tabla cruzada / tabla de contingecia



```python
tabla = pd.crosstab(df['sexo_jefe'], df['est_socio'])
tabla
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>est_socio</th>
      <th>alto</th>
      <th>bajo</th>
      <th>medio_alto</th>
      <th>medio_bajo</th>
    </tr>
    <tr>
      <th>sexo_jefe</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>hombre</th>
      <td>263</td>
      <td>188</td>
      <td>511</td>
      <td>818</td>
    </tr>
    <tr>
      <th>mujer</th>
      <td>102</td>
      <td>39</td>
      <td>179</td>
      <td>232</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Crea una tabla cruzada para relacionar "sexo_jefe" con "est_socio"
tabla_margins = pd.crosstab(df['sexo_jefe'], df['est_socio'],margins=True)
tabla_margins
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>est_socio</th>
      <th>alto</th>
      <th>bajo</th>
      <th>medio_alto</th>
      <th>medio_bajo</th>
      <th>All</th>
    </tr>
    <tr>
      <th>sexo_jefe</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>hombre</th>
      <td>263</td>
      <td>188</td>
      <td>511</td>
      <td>818</td>
      <td>1780</td>
    </tr>
    <tr>
      <th>mujer</th>
      <td>102</td>
      <td>39</td>
      <td>179</td>
      <td>232</td>
      <td>552</td>
    </tr>
    <tr>
      <th>All</th>
      <td>365</td>
      <td>227</td>
      <td>690</td>
      <td>1050</td>
      <td>2332</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Crea una tabla cruzada para relacionar "sexo_jefe" con "est_socio"
tabla = pd.crosstab(df['sexo_jefe'], df['est_socio'])
tabla
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>est_socio</th>
      <th>bajo</th>
      <th>medio_bajo</th>
      <th>medio_alto</th>
      <th>alto</th>
    </tr>
    <tr>
      <th>sexo_jefe</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>mujer</th>
      <td>39</td>
      <td>232</td>
      <td>179</td>
      <td>102</td>
    </tr>
    <tr>
      <th>hombre</th>
      <td>188</td>
      <td>818</td>
      <td>511</td>
      <td>263</td>
    </tr>
  </tbody>
</table>
</div>



En muchas ocasiones se requiere representar esta tabla cruzada mediante proporciones. Para ello se puede utilizar el argumento *normalize* con los siguientes valores:
- *'all'*: para divididr cada cantidad entre el total.
- *'index'*: para dividir las celdas en cada fila entre el total de la fila.
- *'columns'*: para dividir las celdas en cada columna entre el total de la columna.


```python
# Modifica la tabla anterior para mostrar las cantidades *normalizadas* entre el total
tabla_all = pd.crosstab(df['sexo_jefe'], df['est_socio'], normalize='all')
tabla_all
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>est_socio</th>
      <th>alto</th>
      <th>bajo</th>
      <th>medio_alto</th>
      <th>medio_bajo</th>
    </tr>
    <tr>
      <th>sexo_jefe</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>hombre</th>
      <td>0.112779</td>
      <td>0.080617</td>
      <td>0.219125</td>
      <td>0.350772</td>
    </tr>
    <tr>
      <th>mujer</th>
      <td>0.043739</td>
      <td>0.016724</td>
      <td>0.076758</td>
      <td>0.099485</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Modifica la tabla anterior para mostrar las cantidades *normalizadas* entre el total
tabla_index = pd.crosstab(df['sexo_jefe'], df['est_socio'], normalize='index')
tabla_index
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>est_socio</th>
      <th>alto</th>
      <th>bajo</th>
      <th>medio_alto</th>
      <th>medio_bajo</th>
    </tr>
    <tr>
      <th>sexo_jefe</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>hombre</th>
      <td>0.147753</td>
      <td>0.105618</td>
      <td>0.287079</td>
      <td>0.459551</td>
    </tr>
    <tr>
      <th>mujer</th>
      <td>0.184783</td>
      <td>0.070652</td>
      <td>0.324275</td>
      <td>0.420290</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Modifica la tabla anterior para mostrar las cantidades *normalizadas* entre el total
tabla_columns = pd.crosstab(df['sexo_jefe'], df['est_socio'], normalize='columns')
tabla_columns
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>est_socio</th>
      <th>alto</th>
      <th>bajo</th>
      <th>medio_alto</th>
      <th>medio_bajo</th>
    </tr>
    <tr>
      <th>sexo_jefe</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>hombre</th>
      <td>0.720548</td>
      <td>0.828194</td>
      <td>0.74058</td>
      <td>0.779048</td>
    </tr>
    <tr>
      <th>mujer</th>
      <td>0.279452</td>
      <td>0.171806</td>
      <td>0.25942</td>
      <td>0.220952</td>
    </tr>
  </tbody>
</table>
</div>



Opcionalmente, si quieres modificar el orden de las filas o columnas puedes usar el módulo *Categorical* de Pandas, que convierte una columna de un dataframe en datos de tipo categórico, a los cuales se les puede dar un orden específico.


```python
orden_sexo = ['mujer', 'hombre']
orden_estrato = ['bajo', 'medio_bajo', 'medio_alto', 'alto']
df['sexo_jefe']=pd.Categorical(df['sexo_jefe'], categories=orden_sexo, ordered=True)
df['est_socio']=pd.Categorical(df['est_socio'], categories=orden_estrato, ordered=True)
```

## 5.3 Prueba Chi cuadrada
Para evaluar la dependencia o independencia entre dos variables cualitativas se puede utilizar la prueba Chi cuadrada. Las hipótesis son:
- Hipótesis nula (H0): No existe dependencia entre ambas variables (son independientes).
- Hipótesis alternativa (H1): Existe dependencia entre ambas variables.


Para realizar la prueba Chi cuadrada necesitamos importar la biblioteca *scipy.stats*


- A y b son independientes


```python
import numpy as np
from scipy.stats import chi2_contingency
```

Un ejemplo de la aplicación a una tabla de contingencia es:  
`chi2, p, dof, expected = chi2_contingency(tabla)`  
Esta instrucción arrojará  los siguientes resultados:
- El estadístico de prueba
- El p-valor
- Los grados de libertad
- La tabla de frecuencias esperadas
Para imprimir estos resultados:  
```
print('Estadístico de prueba:', chi2) 
print('Valor p:', p)  
print('Grados de libertad:', dof)  
print('Tabla de frecuencias esperadas')   
print(expected)
```



```python
# Realiza una prueba chi cuadrada a la tabla obtenida
chi2, p, dof, expected = chi2_contingency(tabla)
```


```python
print('Estadístico de prueba \t', chi2) 
print('Valor p \t \t', p)  
print('Grados de libertad \t', dof)  
print('\n Tabla de frecuencias esperadas:')   
print(expected)
```

    Estadístico de prueba 	 12.395857313087394
    Valor p 	 	 0.006143128316573984
    Grados de libertad 	 3
    
     Tabla de frecuencias esperadas:
    [[ 53.73241852 248.54202401 163.32761578  86.39794168]
     [173.26758148 801.45797599 526.67238422 278.60205832]]



```python
alfa = 0.05
if p <=alfa:
    print('Las variables son dependientes (Se rechaza la hipótesis nula)')
else:
    print('Las variables son independientes (No se rechaza la hipótesis nula)')
```

    Las variables son dependientes (Se rechaza la hipótesis nula)


Para visualizar la relación entre ambas variables se puede utilizar un "mapa de calor". Es recomendable utilizar la librería *seaborn* como en el siguiente ejemplo:
`ax = sns.heatmap(tabla, annot=True, cmap='YlGnBu', fmt='d')`
*annot=True* sirve para indicar la cantidad en cada celda, *fmt=d* se utiliza para que se despliegue como números enteros, y *cmap* se utiliza para seleccionar una paleta de colores (ver https://matplotlib.org/stable/gallery/color/colormap_reference.html)


```python
import seaborn as sns
```


```python
ax = sns.heatmap(tabla_index, annot=True, cmap='Greens')
```


    
![png](images/output_27_0.png)
    



```python
ax = sns.heatmap(tabla, annot=True, cmap='Reds', fmt='d')
```


    
![png](images/output_28_0.png)
    


## 5.4 Análisis de correspondencia múltiple

El análisis de correspondencia múltiple permite observar la relación entre las categorías de diferentes variables cualitativas. Para realizar el análisis de correspondencia se recomienda instalar la biblioteca *Prince* (solo es necesario hacerlo la primera vez) 
`pip install prince`  
La documentación se puede consultar en: documentación https://libraries.io/pypi/prince


```python
# Instalar la biblioteca Prince
!pip install prince
```

    Collecting prince
      Obtaining dependency information for prince from https://files.pythonhosted.org/packages/ea/47/05a78e27a6c7f85b5e006169e4ddf27637867124ef841176f5e4f5ce7f88/prince-0.13.0-py3-none-any.whl.metadata
      Downloading prince-0.13.0-py3-none-any.whl.metadata (638 bytes)
    Collecting altair<6.0.0,>=4.2.2 (from prince)
      Obtaining dependency information for altair<6.0.0,>=4.2.2 from https://files.pythonhosted.org/packages/c5/e4/7fcceef127badbb0d644d730d992410e4f3799b295c9964a172f92a469c7/altair-5.2.0-py3-none-any.whl.metadata
      Downloading altair-5.2.0-py3-none-any.whl.metadata (8.7 kB)
    Requirement already satisfied: pandas<3.0.0,>=1.4.1 in c:\programdata\anaconda3\lib\site-packages (from prince) (2.0.3)
    Requirement already satisfied: scikit-learn<2.0.0,>=1.0.2 in c:\programdata\anaconda3\lib\site-packages (from prince) (1.3.0)
    Requirement already satisfied: jinja2 in c:\programdata\anaconda3\lib\site-packages (from altair<6.0.0,>=4.2.2->prince) (3.1.2)
    Requirement already satisfied: jsonschema>=3.0 in c:\programdata\anaconda3\lib\site-packages (from altair<6.0.0,>=4.2.2->prince) (4.17.3)
    Requirement already satisfied: numpy in c:\programdata\anaconda3\lib\site-packages (from altair<6.0.0,>=4.2.2->prince) (1.24.3)
    Requirement already satisfied: packaging in c:\programdata\anaconda3\lib\site-packages (from altair<6.0.0,>=4.2.2->prince) (23.1)
    Requirement already satisfied: toolz in c:\programdata\anaconda3\lib\site-packages (from altair<6.0.0,>=4.2.2->prince) (0.12.0)
    Requirement already satisfied: python-dateutil>=2.8.2 in c:\programdata\anaconda3\lib\site-packages (from pandas<3.0.0,>=1.4.1->prince) (2.8.2)
    Requirement already satisfied: pytz>=2020.1 in c:\programdata\anaconda3\lib\site-packages (from pandas<3.0.0,>=1.4.1->prince) (2023.3.post1)
    Requirement already satisfied: tzdata>=2022.1 in c:\programdata\anaconda3\lib\site-packages (from pandas<3.0.0,>=1.4.1->prince) (2023.3)
    Requirement already satisfied: scipy>=1.5.0 in c:\programdata\anaconda3\lib\site-packages (from scikit-learn<2.0.0,>=1.0.2->prince) (1.11.1)
    Requirement already satisfied: joblib>=1.1.1 in c:\programdata\anaconda3\lib\site-packages (from scikit-learn<2.0.0,>=1.0.2->prince) (1.2.0)
    Requirement already satisfied: threadpoolctl>=2.0.0 in c:\programdata\anaconda3\lib\site-packages (from scikit-learn<2.0.0,>=1.0.2->prince) (2.2.0)
    Requirement already satisfied: attrs>=17.4.0 in c:\programdata\anaconda3\lib\site-packages (from jsonschema>=3.0->altair<6.0.0,>=4.2.2->prince) (22.1.0)
    Requirement already satisfied: pyrsistent!=0.17.0,!=0.17.1,!=0.17.2,>=0.14.0 in c:\programdata\anaconda3\lib\site-packages (from jsonschema>=3.0->altair<6.0.0,>=4.2.2->prince) (0.18.0)
    Requirement already satisfied: six>=1.5 in c:\programdata\anaconda3\lib\site-packages (from python-dateutil>=2.8.2->pandas<3.0.0,>=1.4.1->prince) (1.16.0)
    Requirement already satisfied: MarkupSafe>=2.0 in c:\programdata\anaconda3\lib\site-packages (from jinja2->altair<6.0.0,>=4.2.2->prince) (2.1.1)
    Downloading prince-0.13.0-py3-none-any.whl (415 kB)
       ---------------------------------------- 0.0/415.6 kB ? eta -:--:--
        --------------------------------------- 10.2/415.6 kB ? eta -:--:--
       -- ------------------------------------ 30.7/415.6 kB 660.6 kB/s eta 0:00:01
       ----------------------------- ---------- 307.2/415.6 kB 3.8 MB/s eta 0:00:01
       ---------------------------------------- 415.6/415.6 kB 4.3 MB/s eta 0:00:00
    Downloading altair-5.2.0-py3-none-any.whl (996 kB)
       ---------------------------------------- 0.0/996.9 kB ? eta -:--:--
       ----------------------------------- --- 901.1/996.9 kB 28.7 MB/s eta 0:00:01
       --------------------------------------- 996.9/996.9 kB 15.9 MB/s eta 0:00:00
    Installing collected packages: altair, prince
    Successfully installed altair-5.2.0 prince-0.13.0



```python
import prince
```

Seleccionamos un conjunto de variables cualitativas


```python
var_cat = ['est_socio', 'sexo_jefe', 'ubica_geo']
```


```python
# Creación de instancia del modelo
mca = prince.MCA(n_components = 2)
# Ajuste del modelo a los datos
mca = mca.fit(df[var_cat])
# Crea gráfico
ax = mca.plot(df[var_cat], show_column_labels=True, show_row_markers=False)
ax
```





<style>
  #altair-viz-ba39bff60a814f8796eff8ba4936ee64.vega-embed {
    width: 100%;
    display: flex;
  }

  #altair-viz-ba39bff60a814f8796eff8ba4936ee64.vega-embed details,
  #altair-viz-ba39bff60a814f8796eff8ba4936ee64.vega-embed details summary {
    position: relative;
  }
</style>
<div id="altair-viz-ba39bff60a814f8796eff8ba4936ee64"></div>
<script type="text/javascript">
  var VEGA_DEBUG = (typeof VEGA_DEBUG == "undefined") ? {} : VEGA_DEBUG;
  (function(spec, embedOpt){
    let outputDiv = document.currentScript.previousElementSibling;
    if (outputDiv.id !== "altair-viz-ba39bff60a814f8796eff8ba4936ee64") {
      outputDiv = document.getElementById("altair-viz-ba39bff60a814f8796eff8ba4936ee64");
    }
    const paths = {
      "vega": "https://cdn.jsdelivr.net/npm/vega@5?noext",
      "vega-lib": "https://cdn.jsdelivr.net/npm/vega-lib?noext",
      "vega-lite": "https://cdn.jsdelivr.net/npm/vega-lite@5.16.3?noext",
      "vega-embed": "https://cdn.jsdelivr.net/npm/vega-embed@6?noext",
    };

    function maybeLoadScript(lib, version) {
      var key = `${lib.replace("-", "")}_version`;
      return (VEGA_DEBUG[key] == version) ?
        Promise.resolve(paths[lib]) :
        new Promise(function(resolve, reject) {
          var s = document.createElement('script');
          document.getElementsByTagName("head")[0].appendChild(s);
          s.async = true;
          s.onload = () => {
            VEGA_DEBUG[key] = version;
            return resolve(paths[lib]);
          };
          s.onerror = () => reject(`Error loading script: ${paths[lib]}`);
          s.src = paths[lib];
        });
    }

    function showError(err) {
      outputDiv.innerHTML = `<div class="error" style="color:red;">${err}</div>`;
      throw err;
    }

    function displayChart(vegaEmbed) {
      vegaEmbed(outputDiv, spec, embedOpt)
        .catch(err => showError(`Javascript Error: ${err.message}<br>This usually means there's a typo in your chart specification. See the javascript console for the full traceback.`));
    }

    if(typeof define === "function" && define.amd) {
      requirejs.config({paths});
      require(["vega-embed"], displayChart, err => showError(`Error loading script: ${err.message}`));
    } else {
      maybeLoadScript("vega", "5")
        .then(() => maybeLoadScript("vega-lite", "5.16.3"))
        .then(() => maybeLoadScript("vega-embed", "6"))
        .catch(showError)
        .then(() => displayChart(vegaEmbed));
    }
  })({"config": {"view": {"continuousWidth": 300, "continuousHeight": 300}}, "layer": [{"mark": {"type": "circle", "size": 50}, "encoding": {"color": {"field": "variable", "type": "nominal"}, "tooltip": [{"field": "variable", "type": "nominal"}, {"field": "value", "type": "nominal"}, {"field": "component 0", "type": "quantitative"}, {"field": "component 1", "type": "quantitative"}], "x": {"axis": {"title": "component 0 \u2014 11.53%"}, "field": "component 0", "scale": {"zero": false}, "type": "quantitative"}, "y": {"axis": {"title": "component 1 \u2014 9.73%"}, "field": "component 1", "scale": {"zero": false}, "type": "quantitative"}}, "name": "view_2"}, {"mark": {"type": "text"}, "encoding": {"text": {"field": "label", "type": "nominal"}, "x": {"axis": {"title": "component 0 \u2014 11.53%"}, "field": "component 0", "scale": {"zero": false}, "type": "quantitative"}, "y": {"axis": {"title": "component 1 \u2014 9.73%"}, "field": "component 1", "scale": {"zero": false}, "type": "quantitative"}}}], "data": {"name": "data-b11c96c453779ac14b2a9f0ed47c81d9"}, "params": [{"name": "param_2", "select": {"type": "interval", "encodings": ["x", "y"]}, "bind": "scales", "views": ["view_2"]}], "$schema": "https://vega.github.io/schema/vega-lite/v5.16.3.json", "datasets": {"data-b11c96c453779ac14b2a9f0ed47c81d9": [{"component 0": -1.0176761830634646, "component 1": 0.3573312272454294, "variable": "column", "value": "est_socio_alto", "label": "est_socio_alto"}, {"component 0": 1.5044597368819854, "component 1": 2.059337605756099, "variable": "column", "value": "est_socio_bajo", "label": "est_socio_bajo"}, {"component 0": -0.8779164188398537, "component 1": 0.22514380608366094, "variable": "column", "value": "est_socio_medio_alto", "label": "est_socio_medio_alto"}, {"component 0": 0.6054302624242403, "component 1": -0.7173759625228011, "variable": "column", "value": "est_socio_medio_bajo", "label": "est_socio_medio_bajo"}, {"component 0": 0.13152326245786786, "component 1": 0.03761626501110188, "variable": "column", "value": "sexo_jefe_hombre", "label": "sexo_jefe_hombre"}, {"component 0": -0.4241148680706596, "component 1": -0.12129882557927671, "variable": "column", "value": "sexo_jefe_mujer", "label": "sexo_jefe_mujer"}, {"component 0": -0.579757722692408, "component 1": -0.17039082035642175, "variable": "column", "value": "ubica_geo_Apodaca", "label": "ubica_geo_Apodaca"}, {"component 0": 1.232241106382967, "component 1": -0.8356982929234784, "variable": "column", "value": "ubica_geo_Cadereyta", "label": "ubica_geo_Cadereyta"}, {"component 0": 0.6784189577103888, "component 1": 0.8813502300187667, "variable": "column", "value": "ubica_geo_Escobedo", "label": "ubica_geo_Escobedo"}, {"component 0": 1.716633940079337, "component 1": 2.0967246613905117, "variable": "column", "value": "ubica_geo_Garcia", "label": "ubica_geo_Garcia"}, {"component 0": -0.6536493445732646, "component 1": 0.5213327546937263, "variable": "column", "value": "ubica_geo_Guadalupe", "label": "ubica_geo_Guadalupe"}, {"component 0": 0.8291411219192464, "component 1": -0.3145149594503285, "variable": "column", "value": "ubica_geo_Juarez", "label": "ubica_geo_Juarez"}, {"component 0": -0.5464195383972104, "component 1": -0.3646201228675453, "variable": "column", "value": "ubica_geo_Monterrey", "label": "ubica_geo_Monterrey"}, {"component 0": 1.0233440310173938, "component 1": -1.9588582654225095, "variable": "column", "value": "ubica_geo_Pesqueria", "label": "ubica_geo_Pesqueria"}, {"component 0": -1.071979927446886, "component 1": 0.20345325932288624, "variable": "column", "value": "ubica_geo_San_Nicolas", "label": "ubica_geo_San_Nicolas"}, {"component 0": -1.1811848003155594, "component 1": 0.34711461911449515, "variable": "column", "value": "ubica_geo_San_Pedro", "label": "ubica_geo_San_Pedro"}, {"component 0": -0.49399853655471937, "component 1": -0.3926880873278872, "variable": "column", "value": "ubica_geo_Santa_Catarina", "label": "ubica_geo_Santa_Catarina"}]}}, {"mode": "vega-lite"});
</script>



Cada punto corresponde a una observación o una categoría. La interpretación de las dimensiones depende del contexto. En general, la distancia entre los puntos de cada categoría indican la relación entre ellas. Entre más corta sea la distancia, mayor será la asociación de las categorías. Observaciones y categorías en el mismo cuadrante tienden a tener relaciones más fuertes, mientras que observaciones y categorías en cuatrantes opuestos pueden representar relaciones negativas. Una categoría cerca del centro generalmente indica que esa categoría no está fuertemente asociada con ninguna de las dimensiones, por ejemplo, por ser independiente, tener baja variabilidad o baja frecuencia.


## 5.4 Análisis de correlación

Para calcular un coeficiente de correlación de Pearson entre dos columnas se puede utilizar el método *corr()* de Pandas. Por ejemplo:
`correlacion = df['X'].corr(df['Y'])`  
Para calcular el coeficiente de correlación de Spearman (*¿cuándo se recomienda utilizarlo?*) se puede agregar como argumento:  
`correlacion = df['X'].corr(df['Y'], method='spearman')`  


```python
# Calcula la correlación entre "ing_cor" y "gasto_mon"
correlacion = df['ing_cor'].corr(df['gasto_mon'])
correlacion
```




    0.6183850511096656



Otra opción para calcular el coeficiente de correlación es mediante la biblioteca *scipy.stats* con la ventaja de que se puede obtener el valor p. Para ello se puede usar:  
`corr_coef, p_valor = pearsonr(df['X'], df['Y'])`


```python
from scipy.stats import pearsonr
```


```python
corr_coef, p_valor = pearsonr(df['ing_cor'], df['gasto_mon'])
print('Correlacion \t', corr_coef)
print('P-valor \t', p_valor)
```

    Correlacion 	 0.6183850511096658
    P-valor 	 3.9864606022504336e-246



```python
var_cont = ["ing_cor", "gasto_mon", "edad_jefe", "tot_integ"]
```

Para obtener una matriz de correlaciones a partir de una lista de columnas:  
`matriz_corr = df[columnas].corr()`


```python
# Obtén la matriz de correlaciones
matriz_corr = df[var_cont].corr()
matriz_corr
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ing_cor</th>
      <th>gasto_mon</th>
      <th>edad_jefe</th>
      <th>tot_integ</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ing_cor</th>
      <td>1.000000</td>
      <td>0.618385</td>
      <td>0.031953</td>
      <td>0.135281</td>
    </tr>
    <tr>
      <th>gasto_mon</th>
      <td>0.618385</td>
      <td>1.000000</td>
      <td>-0.054339</td>
      <td>0.168204</td>
    </tr>
    <tr>
      <th>edad_jefe</th>
      <td>0.031953</td>
      <td>-0.054339</td>
      <td>1.000000</td>
      <td>-0.158874</td>
    </tr>
    <tr>
      <th>tot_integ</th>
      <td>0.135281</td>
      <td>0.168204</td>
      <td>-0.158874</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
ax = sns.heatmap(matriz_corr, annot=True, cmap='Greens')
ax.set_title('Mapa de calor de las correlaciones');
```


    
![png](images/output_46_0.png)
    




## 5.5 Escalamiento multidimensional


```python
from sklearn.manifold import MDS
```


```python
# Calcular distancias
distancias = 1-np.abs(matriz_corr)
# Aplicar modelo
mds = MDS(n_components=2, dissimilarity='precomputed', normalized_stress='auto')
mds_resultados = mds.fit_transform(distancias)
# Convertir resultados a dataframe
mds_df = pd.DataFrame(mds_resultados, columns=['Dimension 1', 'Dimension 2'])
mds_df['Etiqueta']=var_cont
#Visualización
sns.scatterplot(data=mds_df, hue='Etiqueta', x='Dimension 1', y='Dimension 2')
# Agregar etiquetas a cada punto
for i in range(len(mds_df)):
    plt.text(mds_df['Dimension 1'][i], mds_df['Dimension 2'][i], mds_df['Etiqueta'][i])
plt.show()
```


    
![png](images/output_50_0.png)
    



```python

```
