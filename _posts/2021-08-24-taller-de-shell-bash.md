---
title: "Shell bash - Guía de iniciación"
last_modified_at: 2021-08-26T21:15-04:00
categories: [Talleres]
tags: [Shell, Bash]
toc: true
coments: true
image:
  path: /assets/img/taller-shell-bash-image.png
  lqip: /assets/img/taller-shell-bash-image.png
  alt: Esta guía tiene por objetivo dar una introducción muy clara y concreta a los comandos básicos de la linea de comandos con bash.
---


Esta guía la hice para un taller del shell [bash](https://es.wikipedia.org/wiki/Bash) en la [Academia Desafío Latam](https://desafiolatam.com/) para la carrera de [data science](https://desafiolatam.com/data-science/) impartida por esta institución y en la que entre el 2018 y el 2020 tuve la oportunidad de ser alumno, ayudante y profesor, siendo una de las grandes experiencias que he tenido, conociendo excelentes personas que me ayudaron a impulsar mi carrera (y mi vida) desde un punto muerto hacia lo que hoy soy.  Muchas gracias.

Esta guía tiene por objetivo dar una introducción muy clara y concreta a los comandos básicos de la linea de comandos con [bash](https://es.wikipedia.org/wiki/Bash), no ha sido creada para trabajar directamente con Linux sino de una manera mas genérica dado que en estos tiempos el shell [bash](https://es.wikipedia.org/wiki/Bash) no solo se encuentra en este sistema operativo, sino que es posible encontrarlo en varias implementaciones, como veremos mas adelante.

Si quieres colaborar en este documento, no dudes en ponerte en contacto conmigo para que vamos mejorando el contendido. Se agradece si envían correcciones, puestas al día o incluso párrafos enteros. Esto es muy amable de su parte y es la forma correcta de hacer evolucionar esta guía y el código abierto en general.

# Plataformas de trabajo

[Bash](https://es.wikipedia.org/wiki/Bash) inicialmente fue desarrollado para Unix/Linux sin embargo se ha ido portando a muchas plataformas.  Es por eso que quise independizar del sistema operativo y centrarme en el shell en si.

Esta guía te sirve si:

- Tienes Linux instalado en tu PC ya sea nativo, dual boot, inicio con pendrive, una maquina virtual o un contenedor docker.
- Tienes windows 10 instalado, activaste WLS e instalaste cualquier distribución de la tienda.
- Tienes un ambiente [cygwin](https://www.cygwin.com/) instalado y funcionando.
- Tienes Anaconda instalado y instalaste los paquetes de msys2: https://anaconda.org/msys2/repo
- Tienes Unix instalado.
- Tienes un Apple con MacOS.
- Tienes acceso a un servidor UNIX/Linux remoto vía SSH.

# Algunos datos útiles sobre la linea de comandos (CLI)

- En la CLI estas interactuando con tu servidor a través de comandos que vas introduciendo.
- No existen interfaces gráficas o cursores gráficos... en teoría...
- Lo comandos se crean para hacer una y solo una cosa muy simple... y lo hacen muy bien.
- El nombre de los comandos casi siempre es la forma abreviada de lo que hacen, por ejemplo: `pwd` significa "**P**rint **W**ork **D**itectory".
- Su función original se puede modificar con parámetros y opciones. (Lo veremos mas adelante).
- Mezclando comandos obtenemos un lenguaje de programación muy potente.
- El directorio donde estas parado se llama "directorio de trabajo".

## El símbolo de sistema

Cuando trabajamos en la linea de comandos, al principio de cada linea vemos el siguiente símbolo:

```bash
tu_usuario@nombre-de-host:~$
```

En esta simple linea podemos identificar seis elementos:

1. Tu nombre de usuario: **tu_usuario**.
2. **@** (arroba)
3. El nombre de host o servidor.
4. **:** (dos puntos)
5. El nombre del directorio actual: **~**
6. **$** (signo de peso o signo de dólar)

Los comandos que lancemos irán siempre después del signo `$`

## El directorio home

Todos los usuarios de sistema cuentan con un directorio home, este es su ambiente de trabajo y donde residen las configuraciones para cada aplicación que usemos, ya sea consola o gráfica. 

Generalmente, en un sistema Linux, el directorio home de los usuarios se encuentra en `/home/nombre_de_usuario` y dentro de este el usuario es amo y señor.  Fuera de este no existe ningún directorio en donde un usuario normal pueda hacer modificaciones, al menos por defecto.

Por defecto, el directorio home también se puede llamar por `~` y este es un nombre valido dentro del sistema.

Ademas, existe el usuario **root** que es el súper usuario de sistema, el es quien tiene todos los permisos.  Su directorio de usuario es `/root` y se encarga de administrar el sistema completo, instalar aplicaciones, dar permisos, etc. **El incluso puede eliminar el sistema completo sin preguntas**.

**ATENCIÓN**: El usuario root se debe usar solo para configuraciones y no como el usuario de acceso permanente al sistema.  
Quedan advertidos... ;)

## El entorno de usuario

Dentro del entorno de usuario se pueden crear y dar el orden que este estime conveniente, es el usuario el que tiene el control y puede modificarlo a voluntad.

El entorno no solo lo componen directorios y archivos, también existen variables de sistema que son variables que se definen por defecto al inicio de sesión y que contienen configuraciones especificas del entorno.

Por ejemplo:

`echo $HOME`  
Muestra la ruta completa del directorio home de usuario.

`echo $PATH`  
Muestra los directorios donde el shell ira a buscar los comandos al ejecutarlos.

`echo $RANDOM`  
Muestra un numero entre 0 y 1 al azar.

*Por ahora tienes que creer con fe ciega que esto es así, mas adelante veremos lo que es una variable.*

Si quieres conocer todas las variables de sistema puedes usar el comando `env` o `set` para verlas por pantalla.

Archivos como `.bashrc` o `.profile` permiten personalizar el entorno, agregar variables y ejecutar algunas configuraciones de forma automática al inicio de sesión.

## Paginas de manual.

Si quieres tener mas información de los comandos, archivos o ambiente de sistema UNIX pone a disposición un manual completo de la plataforma a través del comando `man`.

La mayoría de las aplicaciones aportan documentación de manual accesible desde el mismo comando:

`man [comando]`

Por ejemplo, para saber todo lo relacionado sobre la aplicación `man` basta con poner en la CLI:

`man man`

Y se mostrará la información necesaria sobre este.

En ocasiones el mismo programa posee diversas secciones de manual, cuando esto ocurre suele mostrar un mensaje indicando la sección, como man(1) y man(7), o exit(1) y exit(3). Para acceder a estas secciones basta con indicarlo de la siguiente forma:

`man 3 printf`

El manual normalmente está dividido en ocho secciones numeradas, organizadas como sigue:

| Sección | Descripción |
|:---:|:--- |
| 1 | Comandos Generales |
| 2 | Llamadas al sistema |
| 3 | Biblioteca de lenguaje de programación C |
| 4 | Ficheros especiales (normalmente dispositivos, que se pueden encontrar en /dev) y drivers |
| 5 | Formatos de fichero y convenciones |
| 6 | Juegos y salvapantallas |
| 7 | Miscelánea |
| 8 | Comandos de administración del sistema y Demonios |

En algunos sistemas están disponibles también las siguientes secciones:

| Sección | Descripción |
|:---:|:--- |
| 0 | Archivos de cabecera de la biblioteca estándar del Lenguaje de programación C |
| 9 | Rutinas del Kernel |
| n | Tcl/Tk |
| x | X Window System (Entorno grafico) |

# Comandos básicos para trabajar con directorios

`pwd`  
Imprime el directorio donde estas trabajando, osea, donde estas "parado".

`ls`  
Lista todo el contenido de un directorio.

`cd`  
El el comando que usamos para cambiar de directorio, si lo lanzas sin parámetros sirve para ir a tu directorio "home" desde tu directorio de trabajo.

`mkdir un_dir`  
Con esto creamos un directorio.

`cd un_dir`  
Lo usas para cambiarte de directorio, en este caso a uno llamado "un_dir"

`cd ..`  
Esto es para devolverse un nivel hacia atrás.

`cd -`  
Esto permite devolverte al directorio de trabajo anterior.

`rmdir undir`  
Si el directorio esta vacío, lo elimina.  Si no esta vacío se debe usar el comando `rm`.  
**ATENCIÓN: No existe papelera de reciclaje, el directorio se elimina inmediatamente.**

# Comandos básicos para trabajo con archivos

`touch prueba.txt`  
Crea un archivo vacío llamado `prueba.txt`, si el archivo existe solo se actualiza la información de hora del mismo.

`cp prueba.txt copia_prueba.txt`  
Copia el archivo `prueba.txt` a un nuevo archivo llamado `copia_prueba.txt`

`cp prueba.txt un_dir/prueba.txt`  
Copia el archivo `prueba.txt` a un directorio llamado `un_dir/` manteniendo el nombre original.  
Esto funciona si y solo si el directorio `un_dir/` existe en tu directorio de trabajo.

`mv prueba.txt un_dir/prueba.txt`  
Mueve el archivo `prueba.txt` desde el directorio de trabajo al directorio `un_dir/`.  
Esto funciona si y solo si el directorio `un_dir/` existe en tu directorio de trabajo.

`mv prueba.txt nueva_prueba.txt`:  
Renombra el archivo `prueba.txt` a `nueva_prueba.txt`

`rm prueba.txt`  
Borra el archivo `prueba.txt`.  
**ATENCIÓN: No existe papelera de reciclaje, el archivo se elimina inmediatamente.**

# Algunos trucos

1. `clear`: Limpia la terminal.


2. Puedes usar las flechas arriba (↑) y abajo (↓) para encontrar los comandos utilizados anteriormente.


3. Puedes usar el comando `history` para obtener una lista de los comandos usados anteriormente.


4. Se pueden autocompletar comandos, archivos, directorios, etc... con la tecla tabular (→).


5. Con la combinación `Ctrl-R` puedes tipear un comando y se buscara en el historial el ultimo ejecutado que coincida con lo tipeado.

# Imprimiendo en pantalla

`echo "Hello, World!"`  
Imprime Hello, World! en tu pantalla.

`cat datos.csv`  
Imprime el contenido del archivo `datos.csv` en la pantalla.

`head datos.csv`  
Imprime las primeras 10 lineas del archivo `datos.csv` en la pantalla.

`head -50 datos.csv`  
Imprime las primeras 50 lineas del archivo `datos.csv` en la pantalla.

`tail datos.csv`  
Imprime las ultimas 10 lineas del archivo `datos.csv` en la pantalla.

`tail -50 datos.csv`  
Imprime las ultimas 50 lineas del archivo `datos.csv` en la pantalla.

# Contando cosas

`wc datos.csv`  
Cuenta el numero de lineas, palabras y caracteres en el archivo `datos.csv` y los imprime en pantalla.

`wc -l datos.csv`  
Cuenta el numero de lineas en el archivo `datos.csv` y los informa en pantalla. (Nota: `-l` se refiere a "lines".)

`wc -w datos.csv`  
Cuenta el numero de palabras en el archivo `datos.csv` y los informa en pantalla. (Nota: `-w` se refiere a "words".)

`wc -c datos.csv`  
Cuenta el numero de caracteres en el archivo `datos.csv` y los informa en pantalla. (Nota: `-c` se refiere a "chars".)

# Parámetros y opciones

Los parámetros de los comandos pueden modificar el comportamiento original de estos.
Casi todos los comandos tienen múltiples opciones.
Estas se pueden aplicar de la siguiente forma:

  1. Escribe el comando sin parámetros (ej: `wc`)
  2. Agrega un espacio y un guion (ej: ` -`)
  3. Agrega la opción (ej: `w`)

Resultado: `wc -w`

En general el paso de parámetros en los comandos puede variar, algunos como `ps` o `tar`aceptan las opciones sin guiones,  otros como `wc` se le pasan los comandos con un solo guion y a otros aceptan comandos con uno y dos guiones.


En general sintaxis de los parámetros de los comandos es la siguiente:

1. `comando -opción`
2. `comando --opción`

Si se quiere saber cuales son los parámetros y opciones para los comandos existen dos formas:

1. **La forma rápida**:  `comando --help` o en algunos casos `comando -help`
2. **La pagina de manual**: `man comando`, (para mas información, siempre puede hace un `man man`)

Algunos Ejemplos:

`wc -w datos.csv`  
Como ya sabemos, `wc` cuenta el numero de lineas, palabras y caracteres en el archivo datos.csv y los imprime en pantalla.
En este caso modificamos el comportamiento con el parámetro `-w` para que solo cuente las palabras.

`ls -l`  
En este caso sabemos que `ls` lista todo el contenido de un directorio.
Pero en este caso el parámetro `-l` cambia el formato de salida y muestra mayor información sobre los archivos y directorios.

# Imprimiendo cosas a un archivo

En algunos casos y principalmente en proyectos mas complejos no necesitamos imprimir datos a pantalla sino que necesitamos salvar los resultados en archivos para poder trabajarlos después.

Es aquí donde aparecen los caracteres de **redirección** que nos permiten enviar la salida de un comando hacia un archivo.

Los caracteres de redirección pueden ser de dos tipos:
1. `>`: Toma la salida del comando y lo direcciona a un archivo, si el archivo existe este se reescribe desde cero.
2. `>>`: toma la salida del comando y lo direcciona al final de un archivo, si el archivo existe el contenido se agrega después de la ultima linea.

Por ejemplo:

`head datos.csv > datos_diez_primeros.csv`  
Toma las primeras 10 lineas del archivo `datos.csv` y las envía a un archivo llamado `datos_diez_primeros.csv`.  
Si el archivo no existe lo crea.  
Si el archivo existe lo sobrescribe.  

`head datos.csv >> datos_variados.csv`  
Toma las primeras 10 lineas del archivo `datos.csv` y las envía a un archivo llamado `datos_variados.csv`.  
Si el archivo no existe lo crea.  
Si el archivo existe agrega el contenido al final del archivo manteniendo el contenido original.  

# Filtrando datos

Si tenemos un archivo `datos.csv` que es un conjunto de datos separados por `;` y queremos mostrar solo la primera columna del archivo, podemos ejecutar lo siguiente:

`cut -d';' -f1 datos.csv`  
El comando `cut` corta la entrada que se le entrega de acuerdo a los parámetros que se le pasan.  
En este caso se le dice que use como delimitador `-d` el símbolo `;` y que ademas solo muestre la primera columna `-f1` del archivo `datos.csv`.

`cut -d'-' -f1,5,12,13 datos.csv`  
Este es un ejemplo parecido que el anterior pero se le dice que use como delimitador el caracter `-` y que imprima las columnas 1, 5, 12 y 13 del archivo `datos.csv`.

`grep "algo" datos.csv`  
Este comando retornara todas las lineas que contienen el string "algo" dentro del archivo `datos.csv`.  
Por defecto, este comando diferencia entre mayúsculas y minúsculas.

`grep -v "algo" datos.csv`  
Por el contrario del comando anterior, este comando retorna todas las lineas que **NO** contienen el string "algo" dentro del archivo `datos.csv`  

`grep -i "ALGO" datos.csv`  
Este comando retornara todas las lineas que contienen el string dentro del archivo `datos.csv`.  
En este caso, con el parámetro `-i`, **NO** diferencia entre mayúsculas y minúsculas.  

# Valores únicos y ordenados.

`sort datos.csv`  
Muestra en su salida, el archivo ordenado por orden alfabético.

`sort -n datos.csv`  
Muestra en su salida, el archivo ordenado por orden numérico.

`sort -r datos.csv`  
Muestra en su salida, el archivo ordenado por orden alfabético pero de forma reversa.

`sort -r -n datos.csv`  
Muestra en su salida, el archivo ordenado por orden numérico pero en reversa.

`sort -u datos.csv`  
Muestra en su salida, el archivo ordenado por orden alfabético y remueve los duplicados (Nota: `-u` se refiere a unique.)

`sort -n -t',' -k2 datos.csv`  
Muestra en su salida, el archivo ordenado por orden numérico (`-n`) por la segunda columna (`-k2`), utilizando un separador de columnas (`-t`) que es el caracter `,`. 

`uniq datos.csv`  
Muestra en su salida el contenido del archivo sin valores repetidos.

`uniq -c datos.csv`  
Muestra en su salida el contenido del archivo sin valores repetidos y contando el numero de ocurrencias.

# Pipes o tuberías.

En proyectos mas complejos, existen ocasiones en que es necesario pasar la salida de un comando por la entrada de otros.  Para esto se pueden utilizar archivos pero en grandes volúmenes de datos esto puede ser muy poco conveniente.

Es en estos casos cuando podemos usar los **pipes** o tuberías, estos permiten conectar salidas y entradas de comandos haciendo que se comporten como si fuera uno.

Estos pipes se utilizan con el caracter `|`.

Por ejemplo:  
`head -50 datos.csv | tail -10`  
Este comando muestra las lineas 41 a la 50 del archivo `datos.csv` de la siguiente manera:

1. Toma el archivo `datos.csv` y a través de `head` solicita las primeras 50 lineas.
- Luego, la salida de `head` es pasada a través de una tubería hacia el comando `tail`.
- finalmente el comando `tail` muestra las ultimas 10 lineas de la salida del comando `head`.

`sort datos.csv | uniq -c`  
En este caso, se solicita la salida del archivo `datos.csv`de forma ordenada y después, a través de una tubería, se ingresa la salida al comando `uniq` el cual contara las ocurrencias por cada fila única.

`cut -d';' -f1 datos.csv | grep "algo" | wc -l`  
Este comando ejecuta lo siguiente:

1. Muestre la primera columna del archivo `datos.csv` usando como delimitador el símbolo `;`.
- Busque dentro de la salida del comando `cut` el string "algo".
- Cuente la cantidad de lineas donde el string "algo" aparece.

# Automatizar tareas

Se pueden automatizar tareas, scripts y comandos para que se ejecuten automaticamente cada día, hora o incluso cada minuto.

Para esto todo sistema unix tiene una utilidad llamada `cron` y es posible configurarla con el comando `crontab -e`.  Esto abrirá un editor en donde se podrá agregar la configuración de la tarea.

La configuración se realiza agregando una linea por tarea que se quiera programar, cada linea tiene la siguiente sintaxis:

`* * * * * usuario    /tu/comando.sh`

Que significa lo siguiente: 

1. El minuto de la hora en que debe ser ejecutado.
2. Hora del día en que debe ser ejecutado.
3. Día del mes en que debe ser ejecutado.
4. Mes en que debe ser ejecutado.
5. Día de la semana en que debe ser ejecutado.
6. Usuario que debe ejecutarlo (opcional).
7. Comando que debe ser ejecutado.

Los primeros cinco parámetros definen cuando debe ser ejecutado y el sexto define quien y el séptimo define que debe ser ejecutado.

El símbolo `*` es un comodín que significa *todos*.

![Crontab File](/assets/img/taller-de-shell-bash-crontab.png)

Por ejemplo:  

`15 00 * * * /home/usuario/script.sh`  
Ejecutara el `script.sh` a las 00:15 horas, todos los días del mes, todos los meses, todos los días de semana.

Una ayuda muy buena para programar tareas con cron es la pagina: https://crontab.guru/
En ella pueden obtener muchas opciones de ejecución para luego copiar y pegar en su archivo crontab.

# Scripting con BASH

Un script no es mas que un conjunto de comandos útiles ejecutándose juntos y en orden para crear otro comando útil.

Para crear un script necesitas saber usar un editor como `vim`, `emacs` o `nano`.

Si no sabes nada de editores te recomiendo `nano` o uno poco conocido llamado `mcedit` el cual te entrega una interfaz sencilla dentro de la consola de comandos y que se maneja con las teclas de función.

Para instalar mcedit debes instalar el paquete "**Midnight Commander**" (llamado comúnmente mc) en tu distribución, o visitar su sitio web: https://midnight-commander.org/

**Midnight Commander** es una herramienta de exploración de archivos tipo *Norton Commander* que entrega muchas utilidades para la consola incluyendo conexión de red, ftp, etc.

![mcedit](/assets/img/taller-de-shell-bash-mcedit.png)


Para crear un script paso a paso:

1. Abra su editor favorito.
2. Escriba las siguientes lineas:
  ```bash
  echo "Numero de lineas en el archivo:"
  wc -l datos.csv
  echo "Numero de caracteres en el archivo:"
  wc -c datos.csv
  ```
3. En la primera linea del archivo escriba `#!/usr/bin/env bash`.
  Esta linea se llama shebang y le dice al script que debe ejecutarlo con [bash](https://es.wikipedia.org/wiki/Bash).
  También es valido escribir `#!/bin/bash`
4. Guarde su archivo en el mismo directorio donde esta `datos.csv` y nómbrelo como plazca, por ejemplo: `mi_script.sh`
5. Debe darle permisos de ejecución al archivo para que pueda hacer algo: `chmod +x mi_script.sh`
6. Ejecute el archivo ./mi_script.sh
7. LISTO!!

Debería quedar algo como esto:

![mcedit](/assets/img/taller-de-shell-bash-script.png)

La salida debe ser algo como esto:
```bash
Numero de lineas en el archivo::
672
Numero de caracteres en el archivo:e:
11424
```

Ya tenemos nuestro primer script.

## Variables

En [bash](https://es.wikipedia.org/wiki/Bash) podemos asignar valores a variables de forma simple ejecutando lo siguiente:
`VARIABLE=VALOR`

Por convención se utilizan nombres en mayúsculas para diferenciarlos.


Por Ejemplo:  
```bash
A=100
B='hello, world'
VERDAD=true
VALOR=0.75
```

Para llamar la variable debe hacerse con el signo `$` delante:

`echo $A`  
100

`echo $B`  
hello, world

`echo $VERDAD`  
true.

`echo $VALOR`  
0.75

## Condicionales con IF

Como se dijo anteriormente, todos los comandos y propiedades de [bash](https://es.wikipedia.org/wiki/Bash) forman un lenguaje de programación rico y lleno de opciones.  En este caso también cuenta con condicionales las cuales cumplen el siguiente criterio:

```bash
A=10
B=20
if [[ $A == $B ]]; then
    echo 'yes'
else
    echo 'no'
fi
```

El caracter `[` es un alias del comando `test` el cual permite evaluar las condicionantes.  Si la evaluación de `test` es true se ejecuta el comando `echo yes` si es falsa (sino o `else`) se ejecuta `echo no`.

Mucha información se puede encontrar en la pagina de manual de `test` a través del comando `man test`.

## Loops
[Bash](https://es.wikipedia.org/wiki/Bash) también cuenta con loops al igual que cualquier lenguaje y estos pueden ser con `while`, si se requiere la evaluación de una condición o con `for` si se requiere iterar rápidamente.

**Ejemplo `while`:**

```bash
I=0
while [ $I -lt 10 ]; do
    echo $I
    I=$((i + 1))
done
```
En este caso se define una variable `$I` y se le indica a `while` que se repita mientras `$I` sea menor que 10 (`[ $I -lt 10 ]`), luego se imprime `$I` y se aumenta `$I` en uno (`$((i + 1))`).  

El ciclo se repite hasta que se deja de cumplir la condicional.

**Ejemplo `for`:**

```bash
# for sobre iterables
for VARIABLE in 1 2 3 4 5; do
	comando_1
	comando_2
	comando_n
done

# for sobre archivos
for VARIABLE in archivo_1 archivo_2 archivo_3; do
	cat $VARIABLE >> /dev/null
done

# for sobre la salida de un comando
for OUTPUT in $(UnComandoAqui); do
	cut -d";" $OUTPUT
done
```

En estos casos se utiliza for sobre diferentes iterables como pueden ser números, archivos o salidas de comandos.  Las opciones son muchas.

`for` también ofrece la posibilidad de evaluar expresiones como `while`, en este caso sigue una sintaxis parecida al lenguaje  C:

```bash
for (( c=1; c<=5; c++ )); do  
   echo "Hola $c veces"
done
```

Y en el caso de necesitar un loop infinito:
```bash
for (( ; ; )); do  
   echo "Loop infinito [ presione CTRL+C para detener]"
done
```


# Otros comandos útiles

`echo "hola mundo!`  
hola mundo!  
`echo` repite todo lo que se le pasa como parámetro.

`sed`  
`sed` fue creado para analizar y transformar texto en la línea de comando.

`sed 's/,/;/g' datos.csv`  
Reemplaza todas los caracteres `,` por `;` en el archivo `datos.csv` e imprime los resultados en pantalla.

`date`  
Imprime la fecha actual.  
(Ejemplo: Sat Aug 10 23:21:55 UTC 2019)

`date +%D`  
Imprime la fecha en el siguiente formato mm/dd/yy (08/12/19)

`date +%Y-%m-%d`  
Imprime la fecha en el siguiente formato yyyy-mm-dd. (2019-10-10)

`awk`  
`awk` es otra gran herramienta para procesamiento de texto y limpieza de datos.  
Con `awk` se podría dedicar un curso completo ya que representa un lenguaje de programación en si.

`awk -F',' '{print $3,$2,$5}' datos.csv`  
Imprime la 3°, 2° y 5° columna (en ese orden) del archivo `datos.csv` que esta delimitado por `,`.

`awk '{sss+=$1} END {print sss}' solo_numeros.csv`  
Suma todos los números de la primera columna del archivo `solo_numeros.csv`.
