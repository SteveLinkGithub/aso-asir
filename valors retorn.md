# Comunicación de procesos: señales de teclado y valores de retorno

El objetivo de esta actividad es conocer dos formas de comunicarse con los procesos: las señales de teclado Ctrl+C y Ctrl+Z y los valores de retorno.

Para realizar esta tarea se pide poner en marcha un proceso (por ejemplo, el mandato yes ) y enviarle señales mediante la combinación de teclas Ctrl+C y Ctrl+Z . Posteriormente es necesario analizar cuáles han sido estas señales viendo el valor de retorno del proceso.


## Primero arrancamos el proceso yes y lo detenemos con la combinación Ctrl+C : ##

<img width="638" height="406" alt="image" src="https://github.com/user-attachments/assets/dd8abf92-cdd7-4d5a-b3c0-416228f6527b" />

(y ^c): Este sería el resultado de saturar la terminal con el proceso "Yes", y de cancelar este proceso con **Control+C.**


## Inmediatamente comprobamos el valor que nos devuelve el proceso al recibir la señal. El valor de retorno se guarda en la variable representada por el símbolo de interrogación ( ?) ##

<img width="214" height="27" alt="image" src="https://github.com/user-attachments/assets/2a409c48-ac60-4929-bdaa-81f086081d1c" />

El resultado del siguiente proceso sería comprobar y devolvernos el valor después de que este reciba la señal, es por eso que la variable **(echo $? 130)**


## Si restamos 128 a ese valor de retorno obtenemos el código de esta señal. En este caso la señal 2 corresponde a SIGINT. Hagamos lo mismo con Ctrl+Z : ##

<img width="640" height="401" alt="image" src="https://github.com/user-attachments/assets/16c981f6-be16-48c9-bd7f-5c44728c3ace" />

Al detenerlo con **Control+Z** obtendremos el código de la señal del valor, siendo exactos a **SIGINT**

<img width="195" height="97" alt="image" src="https://github.com/user-attachments/assets/8247161a-213f-4433-86a8-2d5b2b1bdd9d" />


En este caso se trata de la señal 20 (148-128), que corresponde a SIGTSP.

**(echo $? 148)**








