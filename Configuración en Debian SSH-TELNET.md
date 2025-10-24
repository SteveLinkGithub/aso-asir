# Creación de un entorno de trabajo y conectividad básica Telnet y SSH

Para empezar la configuración de Telnet y SSH, instalaremos la máquina de Debian, para la máquina cliente, clonaremos la misma, para
después empezar a instalar los servicios de Telnet y SSH.

Tenemos varias maneras de conectar a la misma red la máquina cliente y servidor, 
pero a continuación pondré las dos dichas en clase:

- La primera manera sería ponerla en red interna y en Adaptador puente, es decir el servidor contará con dos tarjetas de red: una en red interna y la otra adaptador puente, solo que yo la he puesto en adaptador puente. Es por eso que el cliente tendrá que estar conectado a la red interna para poder establecer la comunicación con el servidor (**a través de la tarjeta de red interna**). 
Un paso importante sería configurar la (**NAT**) para que en el servidor, tenga conexión con el cliente y tenga acceso a la red.

Para que el cliente tenga acceso a Internet, deberá de contar con una tarjeta de red red interna. 

- Pero como queremos que las dos máquinas se conecten entre sí, deberemos de ponerlo en adaptador puente, ya que así
sería la única manera en que las dos máquinas puedan trabajar juntas, es por eso que,  
