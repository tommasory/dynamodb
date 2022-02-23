# Amazon DynamoDB

## Paso 1: crea una tabla con Python
En este paso, crea una tabla denominada Películas. La clave principal de la 
tabla se compone de los siguientes atributos:

* year: la clave de partición. El AttributeType es N para el número. 
* title : la clave de clasificación. El AttributeType es S para cadena.

1. Copie el siguiente programa y péguelo en un archivo llamado MoviesCreateTable.py.

Nota
* Establece el punto final para indicar que está creando la tabla en la versión 
descargable de DynamoDB en su computadora.

* En la llamada a create_table, especifica el nombre de la tabla, los atributos 
de la clave principal y sus tipos de datos.

* El parámetro ProvisionedThroughput es obligatorio. Sin embargo, la versión 
descargable de DynamoDB lo ignora. (El rendimiento aprovisionado está más allá 
del alcance de este ejercicio).

* Estos ejemplos usan la función de impresión de estilo Python 3. La línea de 
__future__ import print_function permite la impresión de Python 3 en Python 
2.6 y versiones posteriores.

2. Para ejecutar el programa, ingrese el siguiente comando.

python MoviesCreateTable.py

