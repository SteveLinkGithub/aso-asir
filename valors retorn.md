# Comunicación de procesos: señales de teclado y valores de retorno

El objetivo de esta actividad es conocer dos formas de comunicarse con los procesos: las señales de teclado Ctrl+C y Ctrl+Z y los valores de retorno.

Para realizar esta tarea se pide poner en marcha un proceso (por ejemplo, el mandato yes ) y enviarle señales mediante la combinación de teclas Ctrl+C y Ctrl+Z . Posteriormente es necesario analizar cuáles han sido estas señales viendo el valor de retorno del proceso.

## Primero arrancamos el proceso yes y lo detenemos con la combinación Ctrl+C : ##

<img width="638" height="406" alt="image" src="https://github.com/user-attachments/assets/dd8abf92-cdd7-4d5a-b3c0-416228f6527b" />

(y ^c): Este sería el resultado de saturar la terminal con el proceso "Yes", y de cancelar este proceso con **Control+C.**

## Inmediatamente comprobamos el valor que nos devuelve el proceso al recibir la señal. El valor de retorno se guarda en la variable representada por el símbolo de interrogación ( ?) ##









