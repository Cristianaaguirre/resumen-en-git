# RESUMEN DE LINUX

* Indices

### ¿Que es la terminal?

La terminal es un programa que ejecuta líneas de comandos, que a su vez estas líneas de comando ejecutan acciones y aquí tienes que aprender dos conceptos: terminal y shell.

Es una interfaz gráfica que simula una linea de comandos y cuando hablamos de una línea de comandos nos referimos a una `shell`.

- **Terminal**: es la ventanita que nos muestra el prompt. Este aloja la shell.
- **Linea de comandos**: programa que toma comandos y los pasa al sistema operativo para hacer algo.

La terminal es mucho menos pesada que el sistema de ventanas y el sistema de ficheros porque te comunicas directamente con los recursos del sistema operativo sin pasar por la interfaz gráfica.

Además, hay casos en los que no cuentas con una interfaz gráfica o también puede dañarse y tendrás que resolver utilizando la terminal de comandos.

### Aprendiendo a caminar en la terminal

El sistema de archivos, será el árbol por el que nos estaremos moviendo en la terminal.

<p aling='center'><img src="./img/carpetas.png"/></p>

Aquí se encuentran los archivos del sistema operativo, así como también los ejecutables, controladores, archivos de configuración, etcétera.

En la carpeta `home` es donde se encuentran los usuarios del sistema operativo. Dentro de la terminal identificamos esta carpeta con el símbolo llamado virgulilla `~`.

* Primeros comandos

| Comando | | Accion |
| ----- | | ----- |
| ls | | Lista los archivos y carpetas del directorio. |
| ls -l | | Lista los archivos y carpetas con toda la información de cada uno. |
| ls -lh | | Lista los archivos y carpetas con la información legible para humanos. |
| cd | | Mueve la terminal al directorio `home` del usuario. |
| cd {folder} | | Mueve la terminal al directorio indicado. |
| clear | | Limpia la pantalla de la terminal (shortcut: `cmd + L`). |
| pwd | | Imprime la ruta actual en la que nos encontramos en la terminal. |
| file {name_file} | | Describe el tipo de archivo que le pasamos como parámetro. |
