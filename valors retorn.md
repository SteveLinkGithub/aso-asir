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


### Es demana que aquest script no pugui ser aturat ni amb Ctrl+C ni amb Ctrl+Z. Per fer això caldrà capturar aquests senyals de teclat.

### D’altra banda, si aquests senyals són rebutjats… com podríem aturar aquest procés? 









