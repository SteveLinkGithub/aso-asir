# 2. Actividades

## Creación de un entorno de trabajo y conectividad básica Telnet y SSH

El objetivo de esta actividad es crear un entorno de trabajo con máquinas virtuales y comprobar en ese entorno la conectividad básica remota mediante Telnet y SSH. Este entorno de trabajo nos servirá para desarrollar el resto de actividades.

Los pasos para crear el entorno de trabajo de máquinas virtuales recomendado son los siguientes:

- Montar un servidor virtual Debian llamado ioc-Server . Este servidor tendrá conectividad con el exterior mediante el servicio NAT integrado que abastece a VirtualBox.
- Montar un cliente virtual Debian llamado ioc-Client . Esta máquina estará conectada al servidor mediante una red interna constituyendo una intranet sin salida al exterior.
- Opcionalmente se puede montar un segundo cliente virtual Windows 7 conectado a esta misma red interna por si se quieren realizar pruebas de conexión y administración remota con sistemas heterogéneos.

Una vez que esta red virtual esté operativa se pide instalar y probar la conectividad remota básica, ejecutando comandos de consola en el 
servidor (yoc-Server) desde la máquina remota (yoc-Client) mediante:

- Conexión Telnet
- Conexión segura SSH


Primero debemos preparar el **entorno de trabajo**:

- Se crea e instala una máquina virtual Debian en configuración de red NAT llamada ioc-Server. 
Por defecto, el DHCP integrado de VirtualBox asignará a esta máquina la siguiente configuración de IP:

<img width="628" height="298" alt="image" src="https://github.com/user-attachments/assets/1c7cc36b-0a82-4cef-89c7-a58357e92856" />

Hemos visto la configuración del servidor con (**ifconfig**).


- Antes de continuar, compruebe la conectividad con el exterior, por ejemplo accediendo a Internet con el 
navegador.

- Añadimos ahora a esta máquina virtual ioc-Server una segunda tarjeta de red, pero esta vez configurada
como red interna.

- Al arrancar de nuevo el equipo reconocerá un segundo adaptador de red que deberemos configurar
manualmente con IP fija, ya sea editando manualmente el archivo /etc/network/interfaces, mediante la
aplicación network-manager o la alternativa wicd. Podemos darle una IP del tipo 192.168.56.10.

- Crearemos e instalaremos una segunda máquina virtual Debian (yoc-Client), que actuará de cliente con 
sólo una tarjeta de red configurada como red interna y una IP fija del mismo rango que eth2 en el servidor 
(por ejemplo, 192. 168. 56. 11).

- Opcionalmente completaremos la red interna con una máquina virtual donde instalaremos un sistema
operativo Windows 7 (yoc-w7) por si se quiere realizar pruebas de administración remota con sistemas
heterogéneos.

- Antes de continuar, compruebe la conectividad de la intranet mediante pings entre las máquinas.

