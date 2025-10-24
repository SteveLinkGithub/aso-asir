# Creación de un entorno de trabajo y conectividad básica Telnet y SSH

## Para empezar la configuración de Telnet y SSH, instalaremos la máquina de Debian, para la máquina cliente, clonaremos la misma, para
después empezar a instalar los servicios de Telnet y SSH.

**Tenemos varias maneras de conectar a la misma red la máquina cliente y servidor, 
pero a continuación pondré las dos dichas en clase:**

- La primera manera sería ponerla en red interna y en Adaptador puente, es decir el servidor contará con dos tarjetas de red: una en red interna y la otra adaptador puente, solo que yo la he puesto en adaptador puente. Es por eso que el cliente tendrá que estar conectado a la red interna para poder establecer la comunicación con el servidor (**a través de la tarjeta de red interna**). 
Un paso importante sería configurar la (**NAT**) para que en el servidor, tenga conexión con el cliente y tenga acceso a la red.

Para que el cliente tenga acceso a Internet, deberá de contar con una tarjeta de red red interna. 

- Pero como queremos que las dos máquinas se conecten entre sí, deberemos de ponerlo en adaptador puente, ya que así
sería la única manera en que las dos máquinas puedan trabajar juntas, es por eso que, elegiremos esta opción ya que a varios compañeros, les ha funcionado de esta manera.

## A continuación Procederemos con la instalación de cada máquina (TELNET-SSH)

En este caso, empezaremos con la instalación de **SSH**, así que tendremos que poner este comando para instalarlo (**sudo apt-get install openssh-server**)-(**apt-get install openssh-server**), pero en este caso no hace falta ponerlo en **sudo**,
ya que en nuestro caso ya somo usuarios **root**, es por eso que para que los nuevos usuarios que creemos desde el servidor no nos dejarán conectarlos al cliente, por la configuración de seguridad que viene por defecto
en Debian.

El comando para añadir usuarios sería el siguiente:

(**sudo adduser nombre_usuario sudo usermod -aG sudo nombre_usuario**) - (**adduser nombre_usuario sudo usermod -aG sudo nombre_usuario**)

Por eso nos deberemos de meternos a un archivo para que nos deje conectarnos con un usario desde el servidor
hacia el cliente, para ello deberemos de editar este archivo de texto **ssh_config**, para editarlo nos deberemos de meternos en el directorio (**cd /etc/ssh**),
y leugo meternos al archivo mediante (**nano ssh_config**), y deberemos de poner lo siguiente, abajo del archivo de configuración:

(**Host IP_SERVIDOR
Ciphers aes128-cbc
Compresion yes
User Usarioquecreamos
Puerto 30**)





