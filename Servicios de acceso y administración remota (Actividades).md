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

