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


- **Antes de continuar, compruebe la conectividad con el exterior, por ejemplo accediendo a Internet con el 
navegador.**

Como tenemos la IP (**10.2.1.254**), como puerta de enlace hacia el exterior haremos ping como prueba.

<img width="516" height="180" alt="image" src="https://github.com/user-attachments/assets/fff2cd02-9bc4-4f73-b49a-5ec26aa82bfe" />

- **Añadimos ahora a esta máquina virtual ioc-Server una segunda tarjeta de red, pero esta vez configurada
como red interna.**

- **Al arrancar de nuevo el equipo reconocerá un segundo adaptador de red que deberemos configurar
manualmente con IP fija, ya sea editando manualmente el archivo /etc/network/interfaces, mediante la
aplicación network-manager o la alternativa wicd. Podemos darle una IP del tipo 192.168.56.10.**

Nos vamos al directorio y le daremos la IP que le corresponda.

<img width="766" height="299" alt="image" src="https://github.com/user-attachments/assets/814f6236-b6f2-4008-8cd8-2283cb120cac" />

- **Crearemos e instalaremos una segunda máquina virtual Debian (yoc-Client), que actuará de cliente con 
sólo una tarjeta de red configurada como red interna y una IP fija del mismo rango que eth2 en el servidor 
(por ejemplo, 192. 168. 56. 11).**

Haremos lo mismo con la máquina cliente.

<img width="776" height="312" alt="image" src="https://github.com/user-attachments/assets/68e3f198-5df2-42aa-af1d-f2a68f5a02f1" />

- **Opcionalmente completaremos la red interna con una máquina virtual donde instalaremos un sistema
operativo Windows 7 (yoc-w7) por si se quiere realizar pruebas de administración remota con sistemas
heterogéneos.**

No tenemos un sistema operativo cliente instalado

- **Antes de continuar, compruebe la conectividad de la intranet mediante pings entre las máquinas.**

Haremos ping entre la máquina cliente y el servidor.

**Ping 10.2.1.127** y **Ping 10.2.1.128**

<img width="531" height="176" alt="image" src="https://github.com/user-attachments/assets/8e883203-2bf6-456e-9d1e-e5159ac186a6" />

<img width="508" height="183" alt="image" src="https://github.com/user-attachments/assets/e6d356c8-cabe-4db3-8aef-13d25a0ce5a8" />


El objetivo es conseguir una estructura de red similar a la de la figura:

<img width="565" height="661" alt="image" src="https://github.com/user-attachments/assets/1efb880c-69c5-4210-9127-dacf95708272" />


Ahora comprobaremos la conectividad remota básica.

- Abra las máquinas virtuales que hacen de servidor (yoc-Server) y cliente remoto (yoc-Client).

- Compruebe la conectividad de la intranet haciendo un ping en el servidor desde el cliente.


<img width="512" height="170" alt="image" src="https://github.com/user-attachments/assets/2a97ea10-a107-4cda-9580-7303a9b02339" />


- Presuponemos que ya están instalados en el servidor y en el cliente los programas Telnet y openSSH. Si no es así, procede a instalarlos según se indica en los apuntes.

- Abra una sesión Telnet en el servidor con un usuario/contraseña válidos y compruebe que puede ejecutar comandos:

<img width="729" height="561" alt="image" src="https://github.com/user-attachments/assets/a3270e6b-4959-47a8-8877-2c05ee0ba61c" />

- Salga de la sesión Telnet:

<img width="292" height="57" alt="image" src="https://github.com/user-attachments/assets/dad95dd8-7e13-44ca-b9c9-53f30f0711a8" />


- Ahora pruebe la conexión remota segura SSH:

<img width="729" height="418" alt="image" src="https://github.com/user-attachments/assets/43746396-47c7-4978-bbd7-d643c01b07ca" />

La conexión segura nos funciona correctamente.


## Restricción de acceso al servicio SSH


El objetivo de esta actividad es conocer las acciones preventivas y de seguridad en lo que respecta al acceso al servicio SSH.

Se pide configurar el servidor SSH para que:

- Sólo puedan acceder por SSH los usuarios Josep y Anna.

- Sólo se pueda acceder desde el equipo 192.168.56.15.

### Para restringir el acceso remoto vía SSH a unos usuarios determinados deberemos editar como superusuario ( root ) el archivo de configuración /etc/ssh/sshd_config:

**$ sudo gedit /etc/ssh/sshd_config**, lo he configurado mediante el editor de textos (**nano**).

<img width="1286" height="807" alt="image" src="https://github.com/user-attachments/assets/25580883-7b69-4de9-abc9-e6a9c2047bba" />


y añadir la línea:

<img width="1289" height="936" alt="image" src="https://github.com/user-attachments/assets/9b617f3f-9192-455b-8679-7dc614541e2e" />

Por otra parte, para gestionar el acceso en función de la IP de los equipos debemos editar los archivos de control de acceso a servicios /etc/hosts.allow y /etc/hosts.deny. 
En este caso, en /etc/host.deny añadimos la siguiente línea para denegar el acceso a cualquier equipo no autorizado:

Añadimos la línea (**sshd**), para entrar he utilizado el editor de textos nano.

<img width="306" height="27" alt="image" src="https://github.com/user-attachments/assets/ba0f188d-b956-4c86-9918-3a5a50533ef6" />

<img width="1284" height="806" alt="image" src="https://github.com/user-attachments/assets/26271f9a-5951-4aa5-a889-b5f3bbc91452" />


A /etc/host.allowella añadimos la siguiente línea para definir específicamente los equipos que pueden acceder:

He accedido al archivo, y lo he configurado mediante nano y he añadido esta línea.

(**sshd: 192.168.56.15**)

<img width="295" height="25" alt="image" src="https://github.com/user-attachments/assets/2511ae98-551d-4b52-bbe9-358db8b91162" />

<img width="1285" height="811" alt="image" src="https://github.com/user-attachments/assets/2cb8791c-f456-4515-8bcf-fabef455486b" />

Recuerde que para que los cambios tengan efecto se debe reiniciar el servicio:

(**$ sudo /etc/init.d/ssh restart**), este comando está desactualizado así que para reiniciar, aún así como este sistema es antiguo,
si nos aceptará el antiguo comando para reiniciar el servicio ssh.

El servicio ssh, deberemos de poner este comando en (**sudo systemctl restart ssh**) vez del otro.

<img width="368" height="115" alt="image" src="https://github.com/user-attachments/assets/49fa41fa-8ef2-4f04-b97e-f81b37da04f7" />

# Acceso a Internet mediante un servidor intermedio y túneles SSH

En la configuración de la intranet que hemos diseñado, el ordenador ioc-Client pertenece a la intranet y no tiene acceso a Internet. El 
objetivo de esta actividad es crear un túnel SSH para conectarnos a un servidor y navegar por páginas web utilizando la conexión a Internet 
del servidor. Queremos hacerlo mediante dos técnicas:

- La transparencia de red

- El enderezamiento dinámico de puertos: servidor SOCKS

La primera opción permite ejecutar el navegador directamente en el servidor y, mediante el túnel SSH y la 
transparencia de red, que el resultado se visualice en el servidor X del ordenador cliente.

- Primero debemos asegurarnos de que tenemos iniciado el servicio SSH en el servidor:

(**/etc/init.d/ssh start**), Poniendo este comando desde el cliente iniciaremos el servicio ssh.

<img width="368" height="115" alt="image" src="https://github.com/user-attachments/assets/7282f3e3-8dd6-45ac-87f5-1590c68e9c71" />








