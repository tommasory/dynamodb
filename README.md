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

En los datos JSON, tenga en cuenta lo siguiente:

* El año y el título se utilizan como valores de atributo de clave principal para la tabla Películas.

* El resto de los valores de información se almacenan en un solo atributo llamado información. Este programa ilustra cómo puede almacenar JSON en un atributo de Amazon DynamoDB.

El siguiente es un ejemplo de datos de película.


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

### Paso 2.1: Descargue el archivo de datos de muestra

Descargue el archivo de datos de muestra: [moviedata.zip](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/samples/moviedata.zip)

Extraiga el archivo de datos (moviedata.json) del archivo.

Copie el archivo moviedata.json en su directorio actual.

### Paso 2.2: Cargue los datos de muestra en la tabla de películas

Después de descargar los datos de muestra, puede ejecutar el siguiente programa para completar la tabla Películas.

1. Copie el siguiente programa y péguelo en un archivo llamado MoviesLoadData.py.

2. Para ejecutar el programa, ingrese el siguiente comando. 
python MoviesLoadData.py

