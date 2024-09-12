# Introducción
En Jupyter Notebook podemos tener celdas de texto con formato (*Markdown*) o celdas con código. En la parte superior puedes seleccionar entre estas opciones.

En las celdas con código, para ejecutar un comando en Python utilizaremos SHIFT+ENTER. Por ejemplo, utilicemos el comando print para mostrar un texto.


```python
print('Hola mundo')
```

    Hola mundo


Podemos agregar comentarios al código añadiendo el símbolo de #. Si el comentario abarca más de una línea podemos utilizar triple comilla doble al principio y al final.


```python
# Este es un comentario
```

## Variables en Python
**Números**: pueden ser enteros (*int*) o reales (*float*). El separador decimal es el punto. Generalmente Python intentará decidir qué tipo de número es.


```python
numero = 2
```


```python
print(numero)
```

    2


**Texto**: Las variables que contienen texto se denominan *strings* (str). El texto se coloca entre comillas sencillas (') o dobles ("). 


```python
texto = 'En un lugar de la Mancha'
```


```python
print(texto)
```

    En un lugar de la Mancha


## Operaciones aritméticas


```python
# Suma
1 +2
```




    3




```python
# Multiplicación
4.5 * 3
```




    13.5




```python
# División. El resultado siempre será decimal
10 / 5
```




    2.0




```python
# Aplican las reglas usuales de prioridad de operaciones
1 + 2 * 3
```




    7




```python
# Es recomendable usar paréntesis para indicar orden en operaciones
(1 + 2) / (4 + 2)
```




    0.5




```python
# Pueden existir errores de redondeo al pasar de binario a decimal
(4 / 5)*3
```




    2.4000000000000004




```python
# Cociente de una división
10 // 3
```




    3




```python
# Resto de una división
10 % 3
```




    1




```python
# Potencias
2**3
```




    8




```python
# Redondeo
round(3.1416)
```




    3



## Listas y diccionarios

Las listas son conjuntos de datos en los cuales hay un orden. Un aspecto importante es que primer elemento corresponde a la posición 0. Es posible modificar los elementos de una lista e incluso puede haber duplicados. Las listas se ponen entre corchetes [ ]. Por ejemplo:


```python
lista = ['Coahuila', 'Nuevo León', 'Tamaulipas']
```


```python
lista
```




    ['Coahuila', 'Nuevo León', 'Tamaulipas']




```python
lista[0]
```




    'Coahuila'



En un diccionario cada elemento está asociado a algo más. Los diccionarios se crea colocando sus elementos entre llaves {}. Se denominan *keys* a las "palabras" y *values* a las definiciones. No existen dos *keys* iguales pero sí puede haber dos *values* iguales.


```python
diccionario = {'Coahuila':'Saltillo', 'Nuevo León':'Monterrey'}
```


```python
diccionario
```




    {'Coahuila': 'Saltillo', 'Nuevo León': 'Monterrey'}



## Indentación
En Python, se utilizan bloques de 4 espacios para agrupar el código. Las líneas que estén indentadas al misno nivel pertenecen al mismo bloque de código.


```python
numero = 2
if (numero==2):
    print("El valor numérico es dos")
elif (numero!=2):
    print("El valor numérico no es dos")
```

    El valor numérico es dos


En el ejemplo anterior la sentencia if/elif se utiliza para condiciones o decisiones. Sin embargo, esto se revisará en otra sesión.


```python

```
