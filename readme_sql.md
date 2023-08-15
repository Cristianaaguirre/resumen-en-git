# RESUMEN DE SQL

- [Data types o tipos de datos](#jerarquia-de-base-de-datos)

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

### COMANDO UTILES DE POSTGRES

PostgreSQL está más estrechamente acoplado al entorno UNIX que algunos otros sistemas de bases de datos, utiliza las cuentas de usuario nativas para determinar quién se conecta a ella (de forma predeterminada). El programa que se ejecuta en la consola y que permite ejecutar consultas y comandos se llama psql, psql es la terminal interactiva para trabajar con PostgreSQL, es la interfaz de línea de comando o consola principal, así como PgAdmin es la interfaz gráfica de usuario principal de PostgreSQL.

**Comandos de ayuda**

En consola los dos principales comandos con los que podemos revisar el todos los comandos y consultas son:

  - **\?**: Con el cual podemos ver la lista de todos los comandos disponibles en consola, comandos que empiezan con backslash ( \ )

  - **\h**: Con este comando veremos la información de todas las consultas SQL disponibles en consola. Sirve también para buscar ayuda sobre una consulta específica, para buscar información sobre una consulta específica basta con escribir `\h` seguido del inicio de la consulta de la que se requiera ayuda, así: `\h ALTER`

**Comandos de navegación y consulta de información**

  - **\c**: Saltar entre bases de datos

  - **\l**: Listar base de datos disponibles

  - **\dt**: Listar las tablas de la base de datos

  - **\d <nombre_tabla>**: Describir una tabla

  - **\dn**: Listar los esquemas de la base de datos actual

  - **\df**: Listar las funciones disponibles de la base de datos actual

  - **\dv**: Listar las vistas de la base de datos actual

  - **\du**: Listar los usuarios y sus roles de la base de datos actual

**Comandos de inspección y ejecución**

  - **\g**: Volver a ejecutar el comando ejecutando justo antes

  - **\s**: Ver el historial de comandos ejecutados

  - **\s <nombre_archivo>**: Si se quiere guardar la lista de comandos ejecutados en un archivo de texto plano

  - **\i <nombre_archivo>**: Ejecutar los comandos desde un archivo

  - **\e**: Permite abrir un editor de texto plano, escribir comandos y ejecutar en lote. `\e` abre el editor de texto, escribir allí todos los comandos, luego guardar los cambios y cerrar, al cerrar se ejecutarán todos los comandos guardados.

  - **\ef**: Equivalente al comando anterior pero permite editar también funciones en PostgreSQL

**Comandos para debug y optimización**

  - **\timing**: Activar / Desactivar el contador de tiempo por consulta

**Comandos para cerrar la consola**

  - **\q**: Cerrar la consola
