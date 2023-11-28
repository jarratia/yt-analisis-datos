# Video 1

- Para levantar un servidor virtual con python, ejecutamos el siguiente comando
  `python -m venv datos`

  Esto crea una carpeta y genera un ambiente virtual.

- Para instalar requirements.txt corremos el siguiente comando:
  `.\datos\Scripts\activate`

Nota: Si se genera el siguiente error con el comando anterior

```
.\datos\Scripts\activate : No se puede cargar el archivo D:\Curso Analisis de Datos con Python\datos\Scripts\Activate.ps1 porque la ejecución de scripts está deshabilitada en este sistema.
```

Se debe correr el siguiente comando para cammbiar la configuración por defecto de windows

```
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`
```

- Ahora, creamos un archivo llamado requirements.txt que contendrá la siguiente información:
  1. pandas
  2. numpy
  3. matplotlib
  4. seaborn

Guardamos el archivo y corremos el comando para instalar todas esas dependencias. `pip install -r .\requirements.txt`

#Video 2
Pandas es una herramienta para el análisis de datos. Este, es un módulo de python, de esta forma hacemos la importación:

```python
import pandas as pd
```

Con el siguiente código creamos una serie de números con Pandas

```python
#Series en Pandas
numeros = [3, 4 , 5, 6, 7, 8]
serie = pd.Series(numeros)
serie, type(serie)
```

El resultado al correr el código anterior es el siguiente:

```python
(0 3
1 4
2 5
3 6
4 7
5 8
dtype: int64,
pandas.core.series.Series)
```

###Data frame
Es como una hoja de cálculo, para generarlos ejecutamos los siguientes pasos

1. Escribimos el código para generar el data frame a partir de un diccionario

```python
#Data frame
data = {
  "Nombre":["Ana", "Juan", "Pedro", "María", "Luis"],
  "Edad":[22, 25, 28, 23, 20],
  "Ciudad":["Barcelona", "Caracas", "Madrid", "Santiago de Chile", "Buenos Aires"]
}
data, type(data)
```

2. Generamos el data frame

```python
#Generar el data frame a partir el diccionario anterior
df = pd.DataFrame(data=data)
df
```

El resultado de ejecución de este data frame es el siguiente:

```py
índice Nombre Edad Ciudad
0      Ana    22    Barcelona
1     Juan    25    Caracas
2     Pedro   28    Madrid
3     María   23    Santiago de Chile
4     Luis    20    Buenos Aires
```

- Para exportar el dataFrame anterior, utilizamos el siguiente código:

```py
#Exportar un dataFrame
df.to_csv("dataf.csv", index_col=0)
```

- Para importar un dataFrame

```
#Importar un dataFrame
import_df = pd.read_csv("dataf.csv")
import_df
```

_Nota: El index_col=0 permite eliminar la generación de columna extra con los índices del arreglo de la tabla._

## Manipulación de datos con pandas

- Seleccionar una columna en específico

```py
#Seleccionar una columna
nombres = df["Nombre"]
nombres
```

Esto retorna únicamente lso valores de la columna nombre de la serie.

- Seleccionar varias columnas

```
#Seleccionar varias columnas
df[["Nombre", "Edad"]]
```

Esto retorna los datos de la columna nombre y edad de la serie.

- También podemos filtrar por el índice

```py
#Filtrar por índice
fila = df.loc[2]
fila
```

- También podemos filtrar a partir de condiciones

```py
#Filtrar por índice
fila = df.loc[2]
fila
```

- Filtrado a partir de varias condiciones, en este caso queremos tener los datos de las personas que sean mayor de 23 años y su nombre empiece por "P".

```py
filtro = (df["Edad"] > 23) & (df["Nombre"].str.startswith("P"))
df[filtro]
```

- Podemos realizar filtrados o consultas como si se tratase de SQL

```py
#Filtrar personas mayores de 23 años mediante Query
df.query("Edad > 23")
```

- Podemos filtrar por varios elementos que se encuentren en el DataFrame

```py
#Extraer la información de varios elementos
df[df["Nombre"].isin(["Ana", "Carlos", "Luis"])]
```

- También podemos pasar funciones al filtrado de datos, esto lo podemos hacer si queremos extraer todos aquellos datos en los que el nombre sea mayor a 5 caracteres.

```py
#Funciones a los filtros realizados
def longitud_5(nombre):
  return len(nombre) == 5

df[df["Nombre"].apply(longitud_5)]
```

- Filtrado a partir de rango de edades

```py
#Filtrar por edades entre 25 a 35 años (inclisivo) con junto cerrado
df[df["Edad"].between(25, 35)]
```

### Tratamiento de datos
