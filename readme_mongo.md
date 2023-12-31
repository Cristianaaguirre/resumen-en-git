# RESUMEN INTRODUCTORIO DE MONGODB

* ¿Que son las bases de datos NoSQL?
  - [Las bases de datos no relacionales](#las-bases-de-datos-no-relacionales)
  - [Tipos de bases de datos NoSQL](#tipos-de-bases-de-datos-nosql)
  - [Bases de datos documentales](#bases-de-datos-documentales)
  - [Ventajas y Desventajas](#ventajas-y-desventajas)

* CRUD con MongoDB
  - [Creando una coleccion](#creando-una-coleccion)
  - [CRUD: create, read, update, delete](#crud-create-read-update-delete)
  - [Consultas en sub documentos](#consultas-en-sub-documentos)
  - [Funciones sort(), limit(), skip(), count() y projection()](#funciones-sort-limit-skip-count-y-projection)

* Operadores especiales
  - [Actualizar arrays](#actualizar-arrays)
  - [Operadores de comparacion](#operadores-de-comparacion)
  - [Operadores para arrays](#operadores-para-arrays)
  - [Operador $regex](#operador-regex)
  - [Operadores logicos](#operadores-logicos)
  - [Operador $exp](#operador-exp)

## ¿Que son las bases de datos NoSQL?

### Las bases de datos No Relacionales

Se puede hacer referencia a las bases de datos NoSQL indistintamente como "no relacionales", "bases de datos NoSQL" o "no SQL" para destacar el hecho de que pueden administrar altos volúmenes de datos no estructurados que cambian con rapidez de formas diferentes a una base de datos relacional (SQL) con filas y tablas.

Desde los tweets de celebridades virales hasta la información de los registros médicos electrónicos que sirve para salvar vidas, se están generando tipos de datos y datos nuevos a un ritmo vertiginoso. Las bases de datos NoSQL han evolucionado para ayudar a los desarrolladores a crear rápidamente sistemas de bases de datos para almacenar la nueva información y hacer que esté fácilmente disponible para búsquedas, consolidación y análisis.

### Tipos de bases de datos NoSQL

* Par clave-valor : Los pares clave-valor se almacenan mediante una tabla hash. Los tipos de pares clave-valor funcionan mejor cuando la clave es conocida y el valor asociado con la clave es desconocido.

* En forma de columnas : Las bases de datos de familia de columnas, basadas en columnas o en forma de columnas almacenan los datos con eficacia y consultan las filas de datos dispersos y resultan útiles para consultar columnas específicas de la base de datos.

* Grafo : Las bases de datos de grafos usan un modelo basado en nodos y bordes para representar datos interconectados, como las relaciones entre las personas en una red social, y ofrecen una navegación y un almacenamiento simplificados por las relaciones complejas.

* Documento : Las bases de datos de documentos amplían el concepto de la base de datos de pares clave-valor mediante la organización de documentos completos en grupos denominados colecciones. Admiten los pares clave-valor anidados y permiten realizar consultas de cualquier atributo dentro de un documento.

### Bases de datos documentales

A pesar de que su estructura es completamente distinta, estas bases de datos permiten realizar las mismas operaciones básicas que las bases de datos relacionales, esto es, añadir, actualizar o eliminar información, además de realizar las pertinentes consultas por parte del usuario.

A diferencia de las bases de datos relacionales, en las bases de datos orientadas a documentos no es necesario recorren todas las columnas de una tabla a la hora de realizar una consulta. En lugar de ello se asigna un identificador único a cada documento, de manera que a la hora de hacer una consulta se comprueba el mismo documento. Este identificador puede ser de diferentes tipos, por ejemplo una ruta completa o una cadena de caracteres. Ejemplo:

```js
{
  _id : "5c8eccc1caa187d17ca6ed16",
  name : 'Sue',
  age : 26,
  status : 'A',
  groups : ['new', 'sports'],
  loc : {
    y : 33.33111,
    x : 86.23123
  }
}
```
Las Colecciones es la forma en que guardamos esos documentos y que normalmente comparten datos entre si, o al menos sabemos que tenemos una entidad o un modelo de datos que se relacionan. MongoDB almacena documentos en una colección, usualmente con campos comunes entre si.

<p align="center">
  <img width="350" height="280" src="./img/mongo.webp"/>
</p>

### Ventajas y Desventajas

* Ventajas
  - Permiten almacenar y consultar información semiestructurada sin una estructura definida.
  - Son un modelo muy flexible que puede albergar numerosos tipos de datos.
  - Simplifican las tareas de adición o actualización de datos. La mayoría de aplicaciones web o móviles están sometidas a cambios constantes. Gracias a las bases de datos documentales se pueden añadir nuevos datos o modelos de análisis de manera mucho más flexible
  - Aseguran una escritura rápida, dando prioridad a la disponibilidad de la escritura sobre la consistencia de los datos. Esto permite asegurar la rapidez incluso en casos de fallos en el hardware o en la red, que en otras bases de datos supondría retrasos en la modificación de los datos y repercutiría negativamente en su coherencia.
  - Garantizan un buen rendimiento. La mayoría de bases de datos documentales cuentan con potentes motores de búsqueda y avanzadas propiedades de indexación, lo que asegura una mayor rapidez a la hora de consultar la información.
  - Tienen una gran escalabilidad y son uno de los mejores métodos para el almacenamiento de grandes volúmenes de información.
* Desventajas
  - No utilizan el lenguaje SQL como lenguaje principal de consulta, aunque sí lo pueden usar de apoyo. Es decir, al contrario que las bases relacionales, no existe un lenguaje estandarizado para la creación de estas bases de datos.
  - No siempre pueden garantizar las propiedades ACID de atomicidad, consistencia, integridad y durabilidad.
  - No tienen una gran comunidad detrás y existen mucha menos información acerca de estas bases de datos.
  - Los índices pueden ocupar mucha memoria RAM, sobre todo en las bases documentales que manejan un gran volumen de datos.

<hr>
<br>

## CRUD con MongoDB

### Creando una coleccion

Antes de crear cualquier coleccion es importante saber en cual nos encontramos, para ello podemos usar el comando `db` que nos indica dentro de que coleccion nos encontramos. Tambien podemos usar el comand `show dbs` para listar todas las colecciones. Si alguna coleccion no posee documentos dentro de ella, no sera listada mediante este comando

<div align='center'><img width="300" height="200" src='./img/mongo-1.png' /></div>

> para este caso utilizaremos un contenedor docker donde se levantara una imagen de mongodb, para acceder a ella debemos ejecutar el comando `docker exec -it [nombre del contendor] mongosh`

Para usar una coleccion o crear una nueva, basta con usar el comando `use()`.

```js
use('nombre de la base de datos')
```

Aunque tambien podemos utilizar el comando `db.createCollection()`, con este comando puede crearse una coleccion e incluso tenemos el control de la configuracion de la misma.

```js
db.createCollection("mySecondCollection", {capped : true, size : 2, max : 2})
```
> Las configuraciones son variadas y requiere de una lectura minuciosa, por el momento solo optaremos por el comando `use()` que trae consigo una configuracion predeterminada

### CRUD: create, read, update, delete

* Para insertar datos disponemos de tres opciones:

  1. `insertOne()`
    <br>
    
    ```js
    db.myCollection.insertOne()
    ```

  2. `insertMany()`
    <br>
    
    ```js
    db.myCollection.insertMany([
    {
      "name": "navindu", 
      "age": 22
    },
    {
      "name": "kavindu", 
      "age": 20
    },

    {
      "name": "john doe", 
      "age": 25,
      "location": "colombo"
    }
    ])
    ```

  3. `insert()` es similar al `insertMany()`

* Para buscar documentos en las colecciones disponemos del comando `find()`
  <br>
  ```js
  db.myCollection.find()
  ```

  A traves de este comando tambien podemos filtrar en base al criterio que dispongamos:

  ```js
  db.myCollection.find( 
    { name : 'name' , age : 10} 
  )
  ```

* Para actualizar un documento dentro de la coleccion disponemos de tres comandos:

  1. `update()` actualiza los documentos existentes en una coleccion
  <br>

  ```js
  db.myCollection.update(
    {_id : 1}, 
    { $set : { city : 'Salta' } } 
    )
  ```

  2. `updateMany()` actualiza uno o más documentos que se encuentren en el filtro de la función.
  <br>

  ```js
  db.myCollection.updateMany( 
    {age : 15}, 
    { $inc : { age : 1 } } 
  )
  ```

  3. `updateOne()` actualiza el primer documento que pase el filtro de la función.
  <br>

  ```js
  db.myCollection.updateOne( 
    {_id : 2}, 
    { $rename : { age : 'edad' } } 
  )
  ```
  <br>

  Existen multiples operadores para realizar modificaciones, como es el caso del `$set`, aqui se dejan algunos ejemplos:

  | Operador | Funcion |
  | --- | --- |
  | $inc | Incrementa el valor de un atributo numérico en una cantidad específica. |
  | $mul | Multiplica el valor de un atributo numérico por un factor específico. |
  | $rename | Cambia el nombre de un atributo. |
  | $set | Asigna un valor específico a un atributo. Si este valor no existe, sera creado. |
  | $unset | Elimina un atributo de un documento. |
  | $min | Actualiza el valor de un atributo con el valor mínimo especificado, sólo si el valor actual es mayor que el valor especificado. |
  | $max | Actualiza el valor de un atributo con el valor máximo especificado, sólo si el valor actual es menor que el valor especificado. |
  | $currentDate | Establece el valor de un atributo como la fecha y hora actual. |

  <br>

  > Un configuracion interesante en las actualizaciones de documentos es el upsert, sea chequea si un documento ya existe en la coleccion con los parametros de busqueda, de ser asi lo actualiza, sino, insertara un documento nuevo.
  ```js
  db.sensor_collection.updateOne(
    {
      sensor : 'A001',
      date : '2022-01-04'
    },
    {
      $push : {
        readings : 123
      }
    },
    {
    upsert : true
    }
  )
  ```
  <br>

* Para eliminar documentos dentro de una coleccion disponemos de dos comandos principales:
  <br>

  - El comando `deleteOne()` que elimina el primer documento que pase el filtro de la función.
  <br>

  ```js
  db.myCollection.deleteOne( 
    {_id : 2}
  )
  ```
  <br>

  - El comando `deleteMany()` que elimina uno o más documentos que se encuentren en el filtro de la función.
  <br>

  ```js
  db.myCollection.deleteMany(
    { price : 200 }
  )
  ```

  <br>

  > Cabe remarcar que en muchas ocasiones se menciona el operador `drop()` para eliminar todos los documentos de una coleccion, el problema es que este operador tambien elimina la coleccion. Si no se desea eliminar la coleccion, tambien podemos usar el comando `deleteMany()` con un objeto vacio dentro de él, es decir, que no hay parametros de filtro por lo cual se eliminan todos los documentos. Tambien existe el comando `remove()` que cumple con la misma funcion.

### Consultas en sub documentos

Las “query in subdocs” en MongoDB se refieren a la capacidad de realizar consultas o búsquedas en documentos secundarios (subdocumentos) dentro de un documento principal.

En MongoDB, los documentos pueden contener otros documentos anidados, lo que permite estructurar la información de manera más compleja y jerárquica. Cuando se realizan consultas en subdocumentos, se pueden buscar documentos que cumplan ciertas condiciones en campos específicos de los subdocumentos, en lugar de buscar solo en los campos del documento principal.

Para realizar una consulta en subdocumentos, se utiliza el operador de punto (".") para indicar el campo específico del subdocumento que se desea buscar. Por ejemplo, si se tiene un documento que contiene un subdocumento “address” que a su vez tiene un campo “city”, se puede buscar todos los documentos que tengan una ciudad específica utilizando la siguiente consulta:

```js
db.myCollection.find({"address.city": "New York"})
```

Esta consulta buscará todos los documentos que contengan un subdocumento “address” con el campo “city” igual a “New York”.

Las consultas en subdocumentos pueden ser muy útiles en situaciones en las que se tiene información estructurada jerárquicamente, como en la información de direcciones de un cliente en un sistema de comercio electrónico. Incluso, si uno de los campos es un array de sub documentos, podemos utilizar la siguiente sintaxis:

```js
{
  electrodomesticos : [
    {
      name : 'heladeras',
      componentes : [
        { enchufe : 'A1' }
      ]
    }
  ]
}

// Notas como en el campo electrodomesticos podemos acceder al primer elemento mediante la notacion '.0' y de alli ir anidando las siguientes consultas

db.myCollection.find(
  {
    'electrodomesticos.0.componentes.enchufe' : 'A1'
  }
)
```

<br>

### Funciones sort(), limit(), skip(), count() y projection()

A veces, al obtener datos de la base de datos, podemos necesitar ordenarlos, obtener un cierto número de registros o contarlos, omitir algunos registros o determinar que caracteristicas necesitamos. En este caso, MongoDB tiene los siguientes métodos: sort(), limit(), skip(), count() y projection().

* `sort()` : Esta funcion nos permite determinar el orden de los registros en base al criterio que establezcamos. Si por ejemplo queremos ordenar los registros en base a un valor numerico, usaremos 1 o -1 para determinar si es de forma ascendente o descendente:
<br>

```js

// ascendente
db.myCollection
  .find({})
  .sort( { age : 1 } )

// descendente
db.myCollection
  .find({})
  .sort( { age : -1 } )
```

<br>

* `limit()` : Esta funcion nos permite limitar el numero de documentos que seran extraidos de una coleccion:
<br>

```js

// se muestran o extraen los primeros 4 registros encontrados
db.myCollection
  .find({})
  .limit( 4 )
```

<br>

* `skip()` : Esta funcion nos permite omitir el numero de documentos que seran extraidos de una collecion:

<br>

```js
// se omiten los primeros 3 registros
db.myCollection
  .find({})
  .skip( 3 )
```

<br>

* `count()` : Esta funcion nos permite contar la cantidad de registros extraidos de la base de datos:
<br>

```js
// se cuentan la cantidad de registros cuyo nombre sea igual a 'random'
db.myCollection
  .find({ name : 'random' })
  .count()
```

* `projection()` : Esta funcion nos permite determinar los campos que seran extraidos de los documentos. No obstante la proyeccion tambien puede ser establecida durante la busqueda sin necesidad de usar esta funcion. Para determinar si un campo sera visible o no, se debe utilizar los valores `1` o `0`:

<br>

```js
// Sin la funcion projection()
db.myCollection.find(
  {},
  { _id : 1, name : 1, age : 0 }
)

// Con la funcion projection()

db.myCollection
  .find()
  .projection( { _id : 1, name : 1, age : 0 } )
```

<br>

Es importante aclarar que todas estas funciones pueden ser anidadas entre si, pero hay que tener en cuenta que la salida de una funcion es el dato de entrada a la siguiente por lo cual debemos tener mucho cuidado cuando las utilizamos.

<br>

```js
db.myCollection
  .find( { name : 'random' } ) // encuentra los registros con el nombre 'random'
  .skip( 3 ) // omite los primeros 3 registros
  .limit( 2 ) // solo toma los 2 primeros registros posteriores al skip
  .sort( -1 ) // ordena los registros de manera descendentes
  .projection( { _id : 0 } ) // se mostraran todos los campos disponibles excepto el id
```

<br>

<hr>
<br>

## Operadores Especiales

### Actualizar arrays

Existen dos operadores principales a la hora de actualizar arrays, `$push` y `$pull`, como sus nombres lo indican push nos permite insertar elementos dentro de un array y pull nos permite extraer elementos dentro de un array. Pero cada uno de ellos necesita de operadores adicionales para funcionar correctamente.

- `$push`:
  <br>

  ```js
  db.myCollection.update(
    { _id : 1 },
    {
      $push : {
        tags : 'nuevo elemento'
      }
    }
  )
  ```
  <br>

  Si necesitamos agregar mas de un elemento al array, debemos utilizar el operador `$each`:
  <br>

  ```js
  db.myCollection.update(
    { _id : 1 },
    {
      $push : {
        tags : {
          $each : ['1er elemento', '2do elemento']
        }
      }
    }
  )
  ```
  <br>
  
- `$pull`:
  <br>

  ```js
  db.myCollection.update(
    { _id : 1 },
    {
      $pull : {
        tags : 'elemento a eliminar'
      }
    }
  )
  ```
  <br>

  Ahora si lo que necesitamos es eliminar mas de un elemento, debemos utilizar el operador `$in`:
  <br>

  ```js
  db.myCollection.update(
    { _id : 1 },
    {
      $pull : {
        tags : {
          $in : ['1er elemento', '2do elemento']
        }
      }
    }
  )
  ```

  <br>

  > Los operadores `$in` y `$each`, seran explicados luego, en este caso solo sirven de apoyo para los ejemplos

  <br>

### Operadores de comparacion

Los operadores de comparación pueden utilizarse para comparar valores en uno o más documentos.

| Operador | Sintaxis | Funcion |
| --- | --- | --- |
| $eq | { field : { $eq : value } } | *Igual que*, coincide con los valores que son iguales al valor indicado |
| $ne | { field : { $ne : value } } | *Distinto*, coincide con los valores que son distintos al valor indicado |
| $gt | { field : { $gt : value } } | *Mayor que*, coincide con los valores que son mayor al valor indicado |
| $gte | { field : { $gte : value } } | *Mayor o igual que*, coincide con los valores que son mayor o iguales al valor indicado |
| $lt | { field : { $lt : value } } | *Menor que*, coincide con los valores que son menores al valor indicado |
| $lte | { field : { $lte : value } } | *Menor o igual que*, coincide con los valores que son menores o iguales al valor indicado |
| $lte | { field : { $lte : value } } | *Menor o igual que*, coincide con los valores que son menores o iguales al valor indicado |

### Operadores para arrays

Existen ciertos operadores que nos permiten filtrar busquedas dentro de documentos que contengan arrays.

* Operadores flexibles
  
  - `$in` : obtiene documentos cuyos arreglos, objetos o valores especificos coincidan con los valores suministrados.
  <br>

  ```js
  db.myCollection.find(
    { name : { $in : [value, value] } }
  )

  db.myCollection.find(
    { books : { $in : [value, value] }}
  )
  ```

  <br>

  - `$nin` : obtiene documentos cuyos arreglos, objetos o valores especificos no coincidan con los valores suministrados.
  <br>

  ```js
  db.inventory.find(
    { qty: { $nin: [value, value]} }
  )

  db.inventory.find(
    { tags: { $nin: [value, value] } } 
  )
  ```
  <br>

* Operadores disponibles solo para arrays
  - `$all` : obtiene los documentos que contengan todos los valores especificados, sin importar el orden.
  <br>

  ```js
  db.myCollection.find(
    { tags : { $all : [value, value] } }
  )
  ```
  <br>

  - `$size` : obtiene los documentos que contengan un arreglo con el tamaño especificado.
  <br>

  ```js
  db.myCollection.find(
    { tags : { $size : value } }
  )
  ```
  <br>

  - `$elemMatch` : obtiene los documentos que contengan un arreglo de objetos y necesitamos agregar cierta precision en la busqueda.
  <br>

  ```js
  db.myCollection.find(
    { results : 
      { 
        $elemMatch : 
          { 
            product : value,
            score : { $gte : value }
          }
      } 
    }
  )
  ```
  <br>

### Operador $regex

Las expresiones regulares son patrones utilizados para encontrar una determinada combinación de caracteres dentro de una cadena de texto. Las expresiones regulares proporcionan una manera muy flexible de buscar o reconocer cadenas de texto.

La expresión regular es una funcionalidad útil de MongoDB. Cuando hablamos de MongoDB, usa PCRE (expresión regular compatible con pearl) como expresión regular:

```js
[
  {
    _id : Objectld( '5bbcf4deed6Ø891ceb5b81c1 ') ,
    student_name : "Junaid",
    student_id : 111,
    student_age : 23
  },
  {
    _id : Objectld ( "Sbbcf4eded6€891ceb5b81c2") ,
    student_name : "Shahid",
    student_id : 112,
    student_age : 32
  }
]

  db.myCollection.find(
    {
      student_name : { $regex : 'Junaid' }
    }
  )
```
<br>

Aunque podemos omitir el uso del operador `$regex` y aplicar expresiones regulares mediante el uso de `//`:

```js
db.myCollection.find(
  { student_name : \/Junaid\/ }
)
```

<br>

### Operadores Logicos

Los operadores lógicos nos ayudan a realizar filtrados considerando condiciones lógicas como el OR y AND. Los operadores lógicos soportados son:

* `$and` : Filtra documentos que cumplan todas las condiciones descritas en un array de elementos.
  <br>

  De manera implicita, ya hemos usado el operador `$and` para realizar busquedas mediante la funcion `find()`
  <br>

  ```js
  //and implicito
  db.myCollection.find(
    {
      qty : { $gt : 15 },
      tags : { $in : ['book'] }
    }
  )

  //and explicito
  db.arr_collection.find(
    {
      $and : [
        { qty : { $gt : 15 } },
        { tags : { $in : ['book'] } }
      ]
    }
  )
  ```

<br>

* `$or` : Filtra documentos que cumplan con alguna de las condiciones descritas en un array de elementos.
  <br>

  ```js
    db.arr_collection.find(
    {
      $or : [
        { qty : { $lt : 50 } },
        { tags : { $in : ['book'] } }
      ]
    }
  )
  ```

<br>

* `$nor` : Filtra los elementos que no cumplan con ninguna de las condiciones descritas en un array de elementos.
  <br>

  ```js
  db.arr_collection.find(
    {
      $nor : [
        { qty : { $lt : 20 } },
        { tags : { $in : [ 'book' ] } }
      ]
    }
  )
  ```

<br>

* `$not` : Excluye un elemento en especifico y no tiene forma de array
  <br>

  ```js
  db.arr_collection.find(
    {
      'item.name' : { $not : /mn/ }
    },
    {
      _id : 0,
      item : 1
    }
  )
  ```

### Operador $exp

Este operador sirve para poder hacer referencia a los valores que tienen los campos de un documento, en una consulta. Tambien sirve para ampliar la funcionalidad de algunos operadores.

Veamos el siguiente objeto

```js
{
  name : 'cristian',
  edad : 27,
  mayor : true,
  gastos : 1200,
  dinero_disponible : 1000 
}

```

<br>

Si quisieramos saber si el dinero disponible es mayor a los gastos fijos, deberiamos usar la siguiente operacion
<br>

```js
db.myCollection.find(
  {
    $exp : {
      $gte : ['$gastos' , '$dinero_disponible']
    }
  }
)
```

<br>

El operador `$eq` normalmente se usa con una sintaxis diferente, pero en este caso con el operador $expr lo hacemos de esta forma, por cada documento. se evaluara una condicion en donde si el campo edad en un documento es igual al campo que tiene las llegadas tarde, entonces se agregara al resultado de la consulta.

Incluso podemos anidar diferentes consultas
<br>

```js
db.myCollection.find(
  {
    $exp : { $lt : ['$gastos', '$dinero_disponible']  },
    edad : { $gt : 18 },
    mayor : true
  }
)
```