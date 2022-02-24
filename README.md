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

3. Para obtener más información sobre la gestión de tablas, consulte:

* https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/WorkingWithTables.html


## Paso 2: cargar datos de muestra

En este paso, rellena la tabla Películas con datos de muestra.

Este escenario utiliza un archivo de datos de muestra que contiene información 
sobre unos pocos miles de películas de Internet Movie Database (IMDb). Los datos 
de la película están en formato JSON, como se muestra en el siguiente ejemplo. 
Para cada película, hay un año, un título y un mapa JSON llamado info.

```
[
   {
      "year" : ... ,
      "title" : ... ,
      "info" : { ... }
   },
   {
      "year" : ...,
      "title" : ...,
      "info" : { ... }
   },

    ...

]
```


En los datos JSON, tenga en cuenta lo siguiente:

* El año y el título se utilizan como valores de atributo de clave principal para la tabla Películas.

* El resto de los valores de información se almacenan en un solo atributo llamado información. Este programa ilustra cómo puede almacenar JSON en un atributo de Amazon DynamoDB.

El siguiente es un ejemplo de datos de película.

```
{
    "year" : 2013,
    "title" : "Turn It Down, Or Else!",
    "info" : {
        "directors" : [
            "Alice Smith",
            "Bob Jones"
        ],
        "release_date" : "2013-01-18T00:00:00Z",
        "rating" : 6.2,
        "genres" : [
            "Comedy",
            "Drama"
        ],
        "image_url" : "http://ia.media-imdb.com/images/N/O9ERWAU7FS797AJ7LU8HN09AMUP908RLlo5JF90EWR7LJKQ7@@._V1_SX400_.jpg",
        "plot" : "A rock band plays their music at high volumes, annoying the neighbors.",
        "rank" : 11,
        "running_time_secs" : 5215,
        "actors" : [
            "David Matthewman",
            "Ann Thomas",
            "Jonathan G. Neff"
       ]
    }
}
```


### Paso 2.1: Descargue el archivo de datos de muestra

Descargue el archivo de datos de muestra: [moviedata.zip](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/samples/moviedata.zip)

Extraiga el archivo de datos (moviedata.json) del archivo.

Copie el archivo moviedata.json en su directorio actual.

### Paso 2.2: Cargue los datos de muestra en la tabla de películas

Después de descargar los datos de muestra, puede ejecutar el siguiente programa para completar la tabla Películas.

1. Copie el siguiente programa y péguelo en un archivo llamado MoviesLoadData.py.

2. Para ejecutar el programa, ingrese el siguiente comando. 
python MoviesLoadData.py



## Paso 3: crear, leer, actualizar y eliminar un elemento con Python

En este paso, realiza operaciones de lectura y escritura en un elemento de la 
tabla Películas. 

Para obtener [más información](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/WorkingWithItems.html) sobre cómo leer y escribir datos, consulte Trabajar 
con elementos y atributos.


### Paso 3.1: Crear un nuevo elemento
En este paso, agrega un nuevo elemento a la tabla Películas. 
1. Copie el siguiente programa y péguelo en un archivo llamado MoviesItemOps01.py.

2. To run the program, enter the following command.
python MoviesItemOps01.py

Note:

* Se requiere la clave principal. Este código agrega un elemento que tiene una clave principal (año, título) y atributos de información. El atributo de información almacena JSON de muestra que proporciona más información sobre la película.

* La clase DecimalEncoder se usa para imprimir números almacenados usando la clase Decimal. El SDK de Boto utiliza la clase Decimal para contener los valores numéricos de Amazon DynamoDB.

### Paso 3.2: Leer un artículo
In the previous program, you added the following item to the table.

```
{
   year: 2015,
   title: "The Big New Movie",
   info: {
        plot: "Nothing happens at all.",
        rating: 0
   }
}
```

Puede utilizar el método get_item para leer el elemento de la tabla Películas. Debe especificar los valores de la clave principal para que pueda leer cualquier elemento de Películas si sabe su año y título.

1. Copie el siguiente programa y péguelo en un archivo llamado MoviesItemOps02.py.

2. Para ejecutar el programa, ingrese el siguiente comando. 

Python MoviesItemOps02.py


### Paso 3.3: Actualizar un artículo

Puede utilizar el método update_item para modificar un elemento existente. Puede actualizar los valores de los atributos existentes, agregar nuevos atributos o eliminar atributos.

En este ejemplo, realiza las siguientes actualizaciones:

* Cambiar el valor de los atributos existentes (puntuación, gráfico).

* Agregue un nuevo atributo de lista (actores) al mapa de información existente.

A continuación se muestra el elemento existente.
```
{
   year: 2015,
   title: "The Big New Movie",
   info: {
        plot: "Nothing happens at all.",
        rating: 0
   }
}
```
El elemento se actualiza de la siguiente manera.
```
{
   year: 2015,
   title: "The Big New Movie",
   info: {
           plot: "Everything happens all at once.",
           rating: 5.5,
           actors: ["Larry", "Moe", "Curly"]
   }
}
```

1. Copie el siguiente programa y péguelo en un archivo llamado MoviesItemOps03.py.

Nota
* Este programa utiliza UpdateExpression para describir todas las actualizaciones que desea realizar en el elemento especificado.

* El parámetro ReturnValues indica a DynamoDB que devuelva solo los atributos actualizados (UPDATED_NEW).

2. Para ejecutar el programa, ingrese el siguiente comando. 

Python MoviesItemOps03.py


### Paso 3.4: Incrementa un Contador Atómico

DynamoDB admite contadores atómicos, que usan el método update_item para 
incrementar o disminuir el valor de un atributo existente sin interferir con 
otras solicitudes de escritura. (Todas las solicitudes de escritura se aplican 
en el orden en que se reciben).

El siguiente programa muestra cómo incrementar la calificación de una película. 
Cada vez que ejecuta el programa, incrementa este atributo en uno.

1. Copie el siguiente programa y péguelo en un archivo llamado MoviesItemOps04.py.

2. Para ejecutar el programa, ingrese el siguiente comando. 
Python MoviesItemOps04.py


### Paso 3.5: Actualizar un artículo (condicionalmente)
### Paso 3.6: eliminar un elemento

```
code
```


