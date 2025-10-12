# Comunicación de procesos: señales de teclado y valores de retorno

El objetivo de esta actividad es conocer dos formas de comunicarse con los procesos: las señales de teclado Ctrl+C y Ctrl+Z y los valores de retorno.

Para realizar esta tarea se pide poner en marcha un proceso (por ejemplo, el mandato yes ) y enviarle señales mediante la combinación de teclas Ctrl+C y Ctrl+Z . Posteriormente es necesario analizar cuáles han sido estas señales viendo el valor de retorno del proceso.


### Primero arrancamos el proceso yes y lo detenemos con la combinación Ctrl+C : ###

<img width="638" height="406" alt="image" src="https://github.com/user-attachments/assets/dd8abf92-cdd7-4d5a-b3c0-416228f6527b" />

(y ^c): Este sería el resultado de saturar la terminal con el proceso "Yes", y de cancelar este proceso con **Control+C.**


### Inmediatamente comprobamos el valor que nos devuelve el proceso al recibir la señal. El valor de retorno se guarda en la variable representada por el símbolo de interrogación ( ?) ###

<img width="214" height="27" alt="image" src="https://github.com/user-attachments/assets/2a409c48-ac60-4929-bdaa-81f086081d1c" />

El resultado del siguiente proceso sería comprobar y devolvernos el valor después de que este reciba la señal, es por eso que la variable **(echo $? 130)**


### Si restamos 128 a ese valor de retorno obtenemos el código de esta señal. En este caso la señal 2 corresponde a SIGINT. Hagamos lo mismo con Ctrl+Z : ###

<img width="640" height="401" alt="image" src="https://github.com/user-attachments/assets/16c981f6-be16-48c9-bd7f-5c44728c3ace" />

Al detenerlo con **Control+Z** obtendremos el código de la señal del valor, siendo exactos a **SIGINT**

<img width="195" height="97" alt="image" src="https://github.com/user-attachments/assets/8247161a-213f-4433-86a8-2d5b2b1bdd9d" />


En este caso se trata de la señal 20 (148-128), que corresponde a SIGTSP.

**(echo $? 148)**


# Comunicación de procesos con el orden kill y captura de señales

El objetivo de esta actividad es practicar el envío de señales con el comando kill y ver cómo se puede capturar una señal para efectuar una acción diferente a la inicialmente programada.

Para realizar esta tarea se considera el siguiente script Bash, que podemos llamar trap.sh:

He creado el archivo con **(sudo nano trap.sh)** y después he ehcho un ls para ver que estaba el archivo correctamente en el directorio correspondiente.

<img width="646" height="410" alt="image" src="https://github.com/user-attachments/assets/4668df77-3edf-4614-a5bb-9df482c9ed07" />

El comando era **(ls)**

<img width="562" height="56" alt="image" src="https://github.com/user-attachments/assets/42b7741e-847f-4ca5-8adf-c37010d3a2ab" />


### Se pide que este script no pueda ser detenido ni con Ctrl+C ni con Ctrl+Z . Para ello será necesario capturar estas señales de teclado.

### Por otra parte, si estas señales son rechazadas… ¿cómo podríamos detener este proceso?


Debe crear el script y darle permisos de ejecución. Como puede ver, es un simple contador que sólo se detiene al terminar de contar hasta 200.000. Puede comprobar cuánto tiempo tarda en hacer este bucle con el comando time y cambiar el bucle para ajustar el tiempo a sus necesidades:


Tras comprobarlo el proceso nos ha dado el tiempo total que tarda el bucle en ejecutarse

<img width="238" height="73" alt="image" src="https://github.com/user-attachments/assets/cfb5653f-0143-44bf-8f27-d7cdff4c7fa7" />


Puede comprobar que mientras se ejecuta responde a las señales de teclado. Para capturarlos hay que añadir la siguiente línea de trap:

<img width="644" height="403" alt="image" src="https://github.com/user-attachments/assets/910cfcfc-c87c-4538-b91f-0b0e8c79c37b" />

Una vez añadida la línea procederemos a comprobar si funciona correctamente esta línea.


Con esta línea de código, cuando el proceso recibe una señal de teclado SIGTSTP ( Ctrl+Z ) o SIGINT ( Ctrl+C ) es capturado y presenta el siguiente mensaje:

A continuación veremos que nos sale el mensaje que queremos que salga cuando hacemos SIGTSTP **(Ctrl+Z)** o SIGINT **(Ctrl+C)**

<img width="202" height="50" alt="image" src="https://github.com/user-attachments/assets/1a18c29d-bcb5-4769-9856-0d2726eefccf" />

Para detener este proceso ya nada podemos hacer en esta consola. Debemos abrir otra y enviar una señal al proceso mediante kill o killall:

<img width="242" height="31" alt="image" src="https://github.com/user-attachments/assets/5f4660ed-7dc5-41d9-a36b-846bcddec172" />

Si tuviesemos algún proceso desde la otra terminal lo detendría

<img width="642" height="412" alt="image" src="https://github.com/user-attachments/assets/af244939-6594-40cf-a780-59705699d80f" />


<img width="644" height="405" alt="image" src="https://github.com/user-attachments/assets/c8147814-b915-4f4c-8600-0ecba9a1b4c5" />

# Gestión del nivel de ejecución

El objetivo de esta actividad es conocer el funcionamiento de los niveles de ejecución de Linux Debian, cómo se configuran y qué directorios y archivos están involucrados.

Habitualmente en la instalación básica de Debian los niveles de ejecución 2, 3 y 4 son iguales y el nivel por defecto es el 2. Para realizar esta tarea se piden las acciones administrativas siguientes:

- Configurar un nivel de ejecución 3 para que no tenga activo el servicio Apache.
- Este nivel será el nivel predeterminado al arrancar el sistema.

Por último se pide averiguar cómo se configura un nivel por defecto en un Linux que tenga un sistema de arranque basado en upstart ( como Ubuntu).


### Aunque habitualmente es así, primero nos aseguramos que el nivel 2 y el 3 de ejecución son iguales:

 **(rm /etc/rc3.d/*)**
 (cp -d /etc/rc2.d/* /etc/rc3.d)

<img width="224" height="32" alt="image" src="https://github.com/user-attachments/assets/50b51669-aa28-42de-9367-529a706e0cf4" />

<img width="292" height="24" alt="image" src="https://github.com/user-attachments/assets/b373a7a3-4bfc-4381-a7a9-c5d3b87fc936" />

Por lo que se ve nos ha dejado crear y eliminar el nivel 2 y el 3 de ejecución

(NOTA: La opción -d copia los enlaces simbólicos como tales.)

### Si queremos que el servicio Apache quede deshabilitado, al entrar en el nivel 3 sólo es necesario cambiar la S inicial por una K en el nombre del enlace simbólico que apunta al script de control de Apache:

 **(mv /etc/rc3.d/S18apache2 /etc/rc3.d/K18apache2)**

 <img width="210" height="32" alt="image" src="https://github.com/user-attachments/assets/763c5480-70b8-47f5-abe5-bea6c92333b6" />

He intentado hacer el ejercicio, pero en la versión de Debian que uso en la máquina virtual ya no existen los niveles de ejecución clásicos ni los directorios /etc/rc3.d/. Esto solo funcionaba en versiones antiguas de Debian con SysVinit, así que por eso en sistemas ubuntu actuales ya no deja hacerlo.

Puede comprobarse fácilmente que en el nivel 2 desde el navegador se obtiene respuesta a localhost y que en cambio en el nivel 3 no:

**(init 2, init 3)**

Para que el nivel 3 sea el nivel por defecto al arrancar, es necesario editar /etc/inittab. La línea donde dice:

**(The default runlevel.
id: 2 :initdefault:)**

quedará:

**(The default runlevel.
id: 3 :initdefault:)**

En un sistema basado en upstart tenemos dos opciones. Dado que se garantiza la compatibilidad hacia atrás sólo habría que crear un archivo /etc/inittab que sólo tuviera la línea del initdefault. Sin embargo, esta opción se considera obsoleta. Lo correcto es editar el archivo de configuración /etc/init/rc-sysinit.conf y cambiar la variable DEFAULT_RUNLEVEL:

# cat /etc/init/rc-sysinit.conf
# rc-sysinit - System V initialisation compatibility
# Este task runs the old System V-style system initialisation scripts,
# and enters the default runlevel when finished.
...
# Default runlevel, este puede ser overriden en el kernel command-line
# or by faking old /etc/inittab entry
 
env DEFAULT_RUNLEVEL = 3



 

