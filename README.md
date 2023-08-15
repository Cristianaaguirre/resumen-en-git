# RESUMEN DE SQL

Postgres es un motor de bases de datos, existen tres conceptos importantes en torno a las bases de datos:

* El lenguaje
* El motor
* Servidor

Postgres es un motor de base de datos, nacido en el año 1986, que se basa en el uso de objetos relacionales.

Uno de los aspectos mas importantes es que Postgres cumple con el protocolo ACID:

* A: **Atomicidad** -> Separar las funciones desarrolladas en la BD como pequeñas tareas y ejecutarlas como un todo. Si alguna tarea falla se hace un rollback(Se deshacen los cambios)

* C: **Consistency** -> Todo lo que se desarrolló en base al objeto relacional. Los datos tienen congruencia.

* I: **Isolation**-> Varias tareas ejecutándose al mismo tiempo dentro de la BD.

* D: **Durability** -> Puedes tener seguridad que la información no se perderá por un fallo catastrófico. PostgreSQL guarda la información en una Bitácora.

Es una de las bases de datos mas utilizadas por las empresas, ya sea por el tipo de datos, su integridad, servicios adicionales y tambien por su fiabilidad y seguridad.


### DATA TYPES O TIPOS DE DATOS

En PostgreSQL disponemos de gran variedad de Data Types (tipos de datos) nativos en PostgreSQL que podemos utilizar para almacenar nuestros valores. La variedad de tipos de datos variará según para lo que necesitemos, **podemos decantarnos por los más corriente y usados**, como los tipos numéricos, de cadenas, fechas, booleanos, etc. Pero, además de éstos data types típicos, **disponemos de otros data types que no son tan corrientes y son utilizados solo para casos puntuales**, estos son los tipos binarios, enumeradores, arrays, JSONs, geométricos, Network, email y muchos más, incluso podemos **crear nuestro propio data type** muy sencillo, tan solo con un comando (CREATE TYPE).

**Tipos Numéricos (Numeric Types)**
Disponemos de tres tipos para almacenar cadenas dependiendo del número de caracteres que queramos contener. Tenemos dos tipos de longitud fija, `character varying(n)` y `character(n)`, más utilizados como `varchar(n)` y `char(n)` respectivamente. El otro tipo para almacenar cadenas es el `text`, éste último permite contener cadenas de longitud ilimitada.

**Tipos Fechas (Date / Time Type)**
Otro de los tipos más utilizados son los de tipo de fecha y hora, estos tipos suelen traer más de un quebradero de cabeza por la diversidad de los formatos que podemos utilizar. PostgreSQL nos permite separar la fecha y la hora principalmente en dos tipos, `date Type` para sólo la fecha y `time Type` para sólo la hora. También podemos obtener la fecha y la hora a la vez en un único tipo, con o sin la zona horaria éste tipo es llamado `timestamp`. Disponemos de un tipo `interval` con el que podemos establece un intervalo temporal, por ejemplo los años, meses, etc.

**Tipo Booleanos (Boolean Type)**

Éste tipo de dato es utilizado para evaluar un estado en verdadero o falso según la condición que necesitamos. En la siguiente tabla vemos una serie de valores para el campo «a» y el campo «b» y dos de las operaciones lógicas más utilizadas en el mundo informático, el resultado de estas operaciones da lugar a un estado u otro de un boolean type.

<p align="center"><img src="https://www.todopostgresql.com/wp-content/uploads/2018/07/boolean.png" /></p>


### JERARQUIA DE BASE DE DATOS

Toda jerarquía de base de datos se basa en los siguientes elementos:

  - **Servidor de base de datos**: Computador que tiene un motor de base de datos instalado y en ejecución.

  - **Motor de base de datos**: Software que provee un conjunto de servicios encargados de administrar una base de datos.

  - **Base de datos**: Grupo de datos que pertenecen a un mismo contexto.

  - **Esquemas de base de datos en PostgreSQL**: Grupo de objetos de base de datos que guarda relación entre sí (tablas, funciones, relaciones, secuencias).

  - **Tablas de base de datos**: Estructura que organiza los datos en filas y columnas formando una matriz.

