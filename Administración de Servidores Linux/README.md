# Administración de Servidores Linux

## Getsión del árbol de directorios

- **pwd**: Se utiliza para imprimir el nombre del directorio actual.
- **ls**: Unumera el contenido y la información opcional de los directorios y archivos.
    - **ls -l**: ofrece mas información.
- **touch**: Se usa principalmente para crear archivos vacíos y cambiar marcas de tiempo de archivos o carpetas.
- **mkdir**: Se utiliza para crear un nuevo subdirectorio o carpeta del sistema de archivos.
- **rm**: Se utilizapara eliminar archivos y directorios del sistema de archivos.
    - **rm -r**: Para eliminar directorios(carpetas).
- **cp**: copia ficheros y directorios.
    ```
    cp ARCHIVO_A_COPIAR NOMBRE_DEL_ARCHIVO_NUEVO
    ```

## Lectura de Archivos

- **cat**: Nos permite leer archivos en su totalidad.
- **less**: Nos ayuda a leer el contenido de nuestros archivos por páginas. Nos movemos con las flechas del teclado o la tecla de espacio. Salimos de la lectura del archivo con la letra **q**. Buscamos palabras especificamente escribiendo **/palabra**.
- **tail**: Nos muetsra las últimas 10 lineas de nuestro archivos.
    - **tail -f**: Monitiar un archivo en tiempo real. Se pueden monitorear archivos simultanios indicando la direccion de cada uno.
- **head**: Nos muestra las primeras 10 lineas de nuestro archivos. 

## Interacción con archivos y permisos

Con el comando **ls -l** podemos observar la lista de archivos de nuestro directorio arctual con información un poco más detallada. El primer campo nos indica los diferentes permisos para cada archivo o directorio. Por ejemplo *-rwxrw-r--*.

El primer carácter nos indica si tenemos un archivo **( - )**, en lace de simbolo **( l )** o directorio **( d )**.

Los sigientes caracteres se dividen en grupos de 3: lectura **( r )**, escritura **( w )** y ejecución **( x )**. El primer grupo son los permisos del usuario que creó ese archivo, el segundo para el grupo al que pertenece este usuario y el tercero para cualquier otro usuario de tu sistema operativo.

Los grupos nos ayudan a darle los mismos permisos a diferentes usuarios sin nesecidad de asignarlos a cada uno individualmente. Todos los usuarios que pertenezcan al grupo tendrán los mismos permisos.

**Si en vez de una letra encuentras un ( - ) significa que ese usuario o grupo de usuarios no tiene permiso para esa acción en particular.**

Per ejemplo: **-rwxrw-r--** nos indica que trabajamos con un archivo. Todos los usuairos del sistema tienen permisos de lectura. El usuario creador y su grupo tienen permiso de escritura. Y solo el usuario creador puede ejecutar el archivo.

También podemos encontrar estos permisos como 3 números del 1 al 7. Estos números son la suma de los 3 caracteres de permisos para cada usuairo o grupo.

- **( - )**: 0
- **( x )**: 1
- **( w )**: 2
- **( r )**: 4

Por lo tanto, los permisos de nuestros archivo de ejemplo serian: **7**(1+2+4), **6**(0+2+4) y **4**(0+0+4).

Para cambiar los permisos de un archivo o directorio podemos usar el comando **chmod** + a quién queremos añadir o quitar los permisos:

- El usuario propietario: **u**.
- El grupo: **g**.
- El resto de los usuarios: **o**.
- Para todos: **a**.

Por ejemplo, para añadir permisos de ejecución a nuestros usuarios propietario usamos:

```
chmod u+x nombre-del-archivo
```

Tambien podmeos cambiar al usuario propietario del archivo con el comando **chown**:

```
sudo chown nuevo-usuario:grupo-usuarios nombre-del-archivo
```

## Conociendo las terminales en linux

Las distribuciones de Linux para servidores no incluyen interfaz gráfica, ya que consumen muchos recursos, Esto significa que siempre vamos a trabajar desde la terminal.

Tendremos disponiblres **6** terminales virtuales a las que podemos entrar o salir con las teclas **Ctrl + Alt + Fx**. También podemos usar el comando chvt. La séptima terminal es la interfaz grafica, así qu en este caso no disponemos de ella.

Cada usuario activo en nuestro sistema operativo crea una nueva conexión. Podemos ver todas estas conexiones con los comandos **who** y **w** (este último nos da un poco más de información).

Para ver todos los procesos que corren en el sistema podemos usar el comando **ps**. Para filtrar los procesos y ver unicamenete las conexiones de los usuarios usamos **ps -ft tty**.

Este comando nos muestra el identificador de cada proceso. Para terminarlo podemos usar el comando **kill -9 PID**.

## Manejo y monitoreo de procesos y recursoso del sistema

Para ver todos los procesos que corren en el sistema podemos usar el comando **ps**. Recuarda que puedes ver la codumentación de este comando con el comando **man ps**.

EL comando **grep** nos ayuda a filtrar el resultado de un comando o archivo dependiendo de las palabras de cada linea. Para esto también vamos a usar el pipe **( | )**, un simbolo que nos ayuda a enviar el resultado de un comando a un segundo comando.

POr ejemplo, el comando **ps aux | grep platzi** imprimer todos los procesos artivos del sistema y con ayuda del pipe, enviá la lista al comando **grep** para filtrar el resultado, mostrando únicamente las líneas con la pablabra *platzi*.q

## Monitoreo de recursos del sistema

EL comando **top** nos permite interactuar con una interfaz gráfica que nos muestra información especifica del sistema operativo: cantidad de usuarios, tareas corriendo o durmiendo, identificadores de los procesos, entre otras. 

Para ver la información de la CPU podemos usar el comando **cat /proc/cpuinfo | grep "processor"**. Recuerda que linux hace diferencia entre minúsculas y mayúsculas, pero puedes usar el comando **grep -i** para filtrar sin estas diferencias.

Para ver la información de la memoria podemos usar el comando free o para que la información sea más facil de leer, **free -sh**. Y para ver el uso del disco está el comando **du** o **du -hsc**.