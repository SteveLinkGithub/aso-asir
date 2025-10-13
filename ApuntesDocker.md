# Unidad: Introducción a Contenedores y Docker

## 1. Introducción
- Introducción al concepto de contenedores.
- Enfoque en contenedores Linux y tecnología Docker.

## 2. Conceptos Previos

### 2.1 Virtualización
- Tecnologías de hardware y software que permiten abstraer hardware.
- Crean la “ilusión” de administrar recursos virtuales como si fueran reales.
- Usos: despliegue de sistemas, desarrollo de software, análisis de malware, escalado horizontal.
- Ventajas: ahorro de costes (energía, mantenimiento).

### 2.2 Máquina Virtual
- Permite probar sistemas operativos o software sin disponer de máquina física.
- Simula una máquina completa y ejecuta programas como si fueran reales.
- Tecnologías para crear máquinas virtuales:
  - Máquinas virtuales de proceso
  - Emuladores
  - Hipervisores
  - Contenedores (Docker)

### 2.3 Máquina Virtual de Proceso
- Ejecuta programas diseñados para un sistema/arquitectura diferente.
- Ejemplos:
  - Máquina Virtual de Java (JVM)
  - Plataforma .NET (Microsoft)

### 2.4 Emulador
- Software que emula hardware completo o API concreta.
- Ejemplo: Wine emula API de Windows en otros sistemas.

### 2.5 Hipervisor
- Simula total o parcialmente hardware de una máquina.
- Permite instalar distintos sistemas operativos.
- Ejemplos: VirtualBox, VMWare, emuladores de consolas.

## 3. Contenedores

### 3.1 Qué son
- Virtualización que utiliza el sistema base de la máquina anfitrión.
- Actúa como un “entorno privado” aislado (procesos, memoria, sistema de ficheros, red).
- Tipo de virtualización: OS Level Virtualization.
- No se puede ejecutar nativamente en un sistema operativo distinto del host.

### 3.2 Analogía con contenedores marítimos
- Cumplen estándares de tamaño, peso y forma.
- Tipo de carga independiente del contenedor.
- Igual con software en contenedores: puede ejecutarse en cualquier máquina que soporte el estándar.

### 3.3 Contenedores para desarrollo y despliegue
- Facilitan compilación, testeo y despliegue de aplicaciones.
- Evitan problemas de compatibilidad.
- Usados en CI/CD (Continuous Integration/Continuous Delivery).

### 3.4 Contenedores para servicios
- Despliegue de servidores (web, correo, bases de datos, DNS).
- Mantienen versiones consistentes entre local y nube.
- Facilitan escalado horizontal.

### 3.5 Ventajas e inconvenientes
**Ventajas:**
- Ocupan menos espacio que máquinas virtuales completas.
- Ejecución más rápida que con hipervisores.
- Amplio soporte de empresas y disponibilidad de imágenes oficiales.

**Inconvenientes:**
- Rendimiento inferior a hardware real.
- Persistencia y acceso a datos más complejos.
- Uso principalmente por línea de comandos; entorno gráfico tedioso.

### 3.6 Cuándo usar
- Usuarios: probar algo rápido sin complicaciones.
- Desarrolladores: distribuir aplicaciones y entornos de desarrollo.
- Testeo con distintas configuraciones.
- Escalado horizontal de servicios.

## 4. Contenedores en Linux

### 4.1 Historia
- Precursores: Chroot (Unix, 1982) y Jail (FreeBSD, 1999).
- Contenedores modernos: LXC (2008), luego LXD y LXCFS.

### 4.2 Funcionamiento
- **Linux namespaces:** aislan procesos con recursos específicos.
- **Cgroups:** limitan recursos (memoria, procesos, E/S).

### 4.3 Contenedores en Windows y MacOS
- Posible ejecutar contenedores Linux virtualizando Linux (WSL2, Hyper-V, Hyperkit).
- Instalación recomendada: Docker Desktop.

## 5. Docker

### 5.1 Qué es
- Sistema de contenedores Linux usando características del kernel.
- Versiones:
  - Docker CE (Community Edition)
  - Docker EE (Enterprise Edition)
- Integrable con servicios cloud: AWS, Azure, Google Cloud.

### 5.2 Arquitectura
- Cliente: se comunica con el servidor.
- Servidor (Docker Host): gestiona contenedores e imágenes.
- Registro (Registry): almacena imágenes (Docker Hub).

### 5.3 Docker en Windows y MacOS
- Docker Desktop optimiza la ejecución.
- Windows: WSL2 o Hyper-V.
- MacOS: Hyperkit o Docker Desktop.

### 5.4 Contenedores Windows y MacOS
- Docker puede ejecutar contenedores Windows Server Core y MacOS con virtualización adicional.

## 6. Conclusión
- Se repasaron conceptos de virtualización.
- Se introdujo el concepto de contenedor y sus características.
- Se presentó Docker como solución principal para contenedores Linux.




# Unidad 02: Instalación de Docker

En esta unidad aprendemos a instalar Docker y a configurar algunos aspectos básicos después de la instalación. Aunque Docker funciona en Windows y MacOS, siempre que sea posible se recomienda usar Linux, donde su implementación es más estable y evita problemas comunes.


## Instalación en Linux (Ubuntu y derivados)

- Se recomienda instalar **Docker Engine CE** desde el repositorio oficial de Docker para evitar versiones antiguas de los repositorios de Ubuntu.  
- Versiones soportadas: Ubuntu Bionic 18.04, Focal 20.04, Jammy 22.04, Kinetic 22.10.  
- Antes de instalar, conviene eliminar versiones antiguas de Docker para evitar conflictos.  
- Se añade el repositorio oficial de Docker y se instalan los paquetes necesarios.  
- Instalación completa de Docker Engine CE con `docker-compose-plugin` y `docker-buildx-plugin`.  
- Comprobación de instalación con `docker version`.

### Post-instalación en Linux

- Permitir que usuarios normales usen Docker sin permisos de root creando un grupo `docker` y añadiendo los usuarios.  
- Configurar Docker para que arranque automáticamente al iniciar el sistema o desactivar esta opción.  
- Control manual de servicios con `systemctl` para iniciar, parar o reiniciar Docker y containerd.

### Desinstalación en Linux

- Docker se puede eliminar con `apt-get purge`.  
- Contenedores e imágenes permanecen a menos que se eliminen con `docker system prune` o borrando `/var/lib/docker`.


## Instalación en Windows

- Se usa **Docker Desktop**.  
- Windows 10 Pro o Windows Server: se requiere habilitar **Hyper-V**.  
- Windows 10 Home: se necesita instalar **WSL2** y una distribución Linux (como Ubuntu).  
- Una vez listo, se instala Docker Desktop y se verifica con `docker version`.  
- Problemas comunes: errores tras actualizaciones o permisos. Se suelen solucionar desinstalando Docker Desktop, borrando la carpeta `.docker` y las variables de entorno relacionadas, reiniciando y reinstalando.


## Instalación en MacOS

- Se instala Docker Desktop descargando el paquete `.dmg` desde Docker Hub.  
- Permite ejecutar contenedores Linux aunque el rendimiento puede variar frente a Linux nativo.


## Playgrounds de Docker

- Entornos online como [Play with Docker](https://labs.play-with-docker.com/) permiten practicar sin instalar nada.  
- Útiles para probar comandos, crear contenedores y desplegar aplicaciones de forma segura.


## Conclusión

- La unidad muestra cómo instalar Docker en Linux, Windows y MacOS, y cómo realizar configuraciones básicas.  
- La recomendación general sigue siendo usar **Linux** para minimizar problemas y garantizar un mejor rendimiento.  
- Con Docker instalado se puede empezar a experimentar con contenedores, tanto para desarrollo como para despliegue de aplicaciones y servicios.


# PASOS PARA INSTALAR Y DESINSTALAR DOCKER EN UBUNTU, WINDOWS Y MAC OS

#### 2.2.1 Paso 1: Eliminando versiones antiguas de Docker Engine

sudo apt-get remove docker docker-engine docker.io containerd runc

#### 2.2.2 Paso 2: Incluir el repositorio de Docker CE

sudo apt-get update

sudo apt-get install apt-transport-https ca-certificates curl
gnupg-agent software-properties-common

**Una vez realizado este paso, descargamos la clave GPG del repositorio de Docker CE y la
incluiremos. Podemos hacer todo con las siguientes línea:s**

sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o
/etc/apt/keyrings/docker.gpg

**Ahora, solo nos queda añadir el repositorio de Docker CE como fuente para instalación de
paquetes. MUCHO OJO en este paso en distribuciones derivadas, como Linux Mint. El motivo es
el siguiente. Al configurar la fuente de paquetes indicamos la versión de Ubuntu. El comando que
utilizamos para obtener la versión de Ubuntu es el siguiente:
lsb_release -cs**

**Este comando nos dirá qué distribución tenemos. Por ejemplo, si tenemos “Ubuntu Kinetic 22.10
(LTS)”, este comando imprimirá por pantalla “Kinetic”.
En algunas versiones derivadas de Ubuntu, como Linux Mint, aunque la distribución esté basada en
Ubuntu Kinetic, no devolverá el texto “Kinetic”, sino otro diferente. Si estáis en este caso, deberéis
introducir a mano la versión de Ubuntu en que se basa vuestra distribución (sustituyendo el
comando de “lsb_release -cs” de la siguiente línea)**

Aclarado esto, con el siguiente comando podéis añadir el repositorio:

echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg]
https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list >
/dev/null

**O en el caso que tengáis una distribución basada en Ubuntu con el problema comentado
anteriormente, sustituir “$(lsb_release -cs)” a mano por el nombre, de una forma similar a:**

echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg]
https://download.docker.com/linux/ubuntu \
kinetic stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

### 2.2.3 Paso 3: Instalando Docker Engine CE

sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin
docker-compose-plugin

sudo docker version

### 2.3.1 Permitir administrar Docker con usuarios sin privilegios

**Docker utiliza sockets Unix. Para la creación y reserva de un socket Unix, es necesario tener
permisos de root, por lo cual Docker Engine necesita permisos de root para ejecutarse.**

**A veces, en algunos contextos, puede sernos útil que Docker se ejecute por usuarios sin permisos
de root. Pongamos un contexto de un aula de ordenadores, que será utilizada por alumnos con los
que queremos realizar actividades que utilizan Docker.**

**(Para ello, en primer lugar crearemos un grupo llamado “docker”.)**

sudo groupadd docker

**Tras ello añadiremos a los usuarios que queremos que usen Docker sin permisos de root al grupo
con un comando similar al siguiente, donde $USER es el nombre de usuario:**

sudo usermod -aG docker $USER

**si lanzaste comandos de Docker usando sudo con uno de estos usuarios antes de
esta operación, es posible que al lanzar Docker te aparezca un mensaje similar a este:**

WARNING: Error loading config file: /home/user/.docker/config.json -
stat /home/user/.docker/config.json: permission denied

**Para arreglar este error, las opciones son eliminar el directorio “.docker” con:**

sudo rm -rf ~/.docker/


**o cambiar el propietario y permisos del directorio, usando**

sudo chown "$USER":"$USER" /home/"$USER"/.docker -R
sudo chmod g+rwx "$HOME/.docker" -R

#### 2.3.2 Activar/desactivar arranque al inicio

**Para indicar que el servicio de Docker se inicie al arrancar la máquina, podemos indicarlo mediante
los siguientes comandos:**

sudo systemctl enable docker.service
sudo systemctl enable containerd.service

**Si lo que queremos es deshabilitar este arranque automático, podemos usar:**

sudo systemctl disable docker.service
sudo systemctl disable containerd.service

**Para iniciar/parar/reiniciar los servicios manualmente, podemos usar:**

sudo systemctl start/stop/restart docker.service
sudo systemctl start/stop/restart containerd.service

### 2.4 Desinstalando Docker en Ubuntu

**Si en algún momento queremos desinstalar Docker en Ubuntu, podemos usar el comando**

sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin
docker-compose-plugin

**Este comando eliminará Docker Engine, pero no eliminará contenedores e imágenes presentes en
el sistema. Si queremos eliminar estos datos, tenemos dos opciones.
La primera consiste en, previamente a la eliminación de Docker Engine, ejecutar el comando:**

sudo docker system prune -a

**La segunda opción, se debe realizar tras eliminar Docker y consiste en el borrado manual de las
mismas, con el comando:**

sudo rm -rf /var/lib/docker

## 3. INSTALACIÓN DE DOCKER EN SISTEMAS WINDOWS

En este apartado veremos cómo instalar Docker Desktop en sistemas Windows.
Docker posee dos guías diferenciadas de instalación en sistemas Windows:

- Guía para Windows 10 Pro y Windows Server

 https://docs.docker.com/docker-for-windows/install/

- Guía para Windows 10 Home

○ https://docs.docker.com/docker-for-windows/install-windows-home/

La principal diferencia entre ellas, es que el primer grupo requiere que se activen las características
de Windows para Hyper-V, mientras que la segunda guía requiere la activación de WSL2 (Windows
Subsystem for Linux 2).

### 3.1 Pasos previos Windows 10 Pro y Windows Server: activando Hyper-v

En este enlace se explica cómo habilitar Hyper-V en:

- Windows 10 Pro
○ https://docs.microsoft.com/es-es/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v

- Windows Server
○ https://docs.microsoft.com/es-es/windows-server/virtualization/hyper-v/get-started/install-the-hyper-v-role-on-windows-server

### 3.2 Pasos previos Windows 10 Home: Instalando WSL2

**Guía para instalarlo:**

https://docs.microsoft.com/en-us/windows/wsl/install-win10

**En primer lugar, utilizando una consola PowerShell con permisos de administrador, debemos
habilitar WSL. Lo podemos hacer con el comando.**

dism.exe /online /enable-feature 
/featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

**Una vez habilitado, debemos asegurarnos que tenemos nuestro Windows 10 Home actualizado, al
menos hasta la versión “Versión 1903, Build 18362”. Puedes comprobar tu versión ejecutando el
comando “winver”.**

**Una vez actualizado y reiniciado el sistema, debemos habilitar la característica de “Virtual
Machine”, lo cual podemos hacerlo con una consola powershell con permisos de administrador:**

dism.exe /online /enable-feature /featurename:VirtualMachinePlatform
/all /norestart

**Tras ello, deberás reiniciar tu máquina antes del próximo paso.**

Una vez completado el reinicio, deberás instalar la última versión del Kernel de Linux para WSL2
aquí https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi

Finalizada la instalación, con una powershell con permisos de administrador, deberás establecer
WSL2 como la versión por defecto al instalar una distribución de Linux.

**(wsl --set-default-version 2)**

Con esto terminaríamos la instalación de docker en Windows.

### 3.3 Instalación de Docker Desktop

La instalación de Docker Desktop, que es la versión de Docker CE para sistemas Windows, es
sencilla y básicamente consiste en descargar el instalador desde Docker Hub, en el siguiente enlace
https://hub.docker.com/editions/community/docker-ce-desktop-windows/ y seguir las
instrucciones de instalación en pantalla.

**Enlace vieo instalación: https://www.youtube.com/watch?v=_9AWYlt86B8** 

Una vez la tengamos instalado comprobaremos que Docker Engine CE se ha instalado correctamente ejecutando:

docker version

### 3.4 Resolviendo problemas en la instalación de Docker Desktop

**Docker Desktop puede dar problemas, incluso al instalar actualizaciones, por eso podría a dar algunos bugs típicos:**

https://github.com/docker/for-win/issues/7629

https://forums.docker.com/t/docker-starts-but-trying-to-do-anything-results-in-error-during-connect/49007/4

**Por eso, si es posible, se recomienda usar Docker en Linux, donde funciona mejor.**

**Una solución que suele funcionar es hacer un borrado completo:**

**Desinstala Docker Desktop.**

**Ve a C:\Users\tuUsuario y borra la carpeta .docker si existe.**

**Elimina las variables de entorno relacionadas con Docker (empiezan por DOCKER_, como DOCKER_TLS_VERIFY, DOCKER_CERT_PATH, DOCKER_HOST).**

**Cómo hacerlo:**

https://answers.microsoft.com/es-es/windows/forum/windows_10-other_settings/windows-10-variables-de-entorno-windows-10-version/703ea5fa-1db4-46da-8ff7-6261140bf58b

**Reinicia el sistema.**

**Vuelve a instalar Docker Desktop.**

## 4. INSTALACIÓN DE DOCKER EN SISTEMAS MACOS

**Las instrucciones para la instalación de Docker Desktop en MacOS están descritas en:**

https://docs.docker.com/docker-for-mac/install/.

**Para realizar esta instalación, básicamente debe descargarse el paquete “.dmg” de
https://hub.docker.com/editions/community/docker-ce-desktop-mac/ y seguir las instrucciones de
instalación en pantalla.**

# UD03. PRINCIPALES ACCIONES CON DOCKER

## 1. INTRODUCCIÓN

En esta unidad explicaremos algunas de las principales acciones básicas que podemos realizar con
Docker.

## 2. ¿GESTIONAREMOS DOCKER MEDIANTE INTERFAZ GRÁFICA?

Aunque hay herramientas gráficas para gestionar Docker, se trabajará únicamente con la línea de comandos para comprender mejor su funcionamiento.

## 3. IMÁGENES Y CONTENEDORES

### 3.1 ¿Qué es una imagen y un contenedor?

Características de las imágenes y los contenedores

- **Imágenes**
○  La imagen es una plantilla de solo lectura que se utiliza para crear contenedores. A partir de una imagen pueden crearse múltiples contenedores.

○ Las imágenes, además de tener su sistema de ficheros predefinido, tienen una serie de parámetros predefinidos (comandos, variables de entorno, etc.) 
con valores por defecto, que se pueden personalizar al crear el contenedor.

○ Docker permite crear nuevas imágenes basándose en imágenes anteriores. Se puede decir que una imagen está formada por un conjunto de “capas” que modifican una imagen base.

- Al crear una nueva imagen, simplemente se añade una capa a la imagen anterior, que actúa como base.
  
- **Contenedores**

○ Contenedores son instancias de una imagen.

○ Se pueden arrancar, parar y ejecutar.

○ Tienen un ID único de 64 caracteres, aunque normalmente se usa solo los primeros 12.

○ Se pueden referenciar con menos caracteres siempre que sean únicos.

○ si solo un contenedor comienza con “7”, basta con usar “7” para identificarlo. Si hay varios similares, se deben añadir más caracteres.

○ **Símil:** La imagen es como un DVD de instalación de Linux, y el contenedor es el sistema ya instalado.


### 3.2 ¿Dónde se almacenan imágenes, contenedores y datos?

La ubicación donde Docker almacena contenedores e imágenes depende del **sistema operativo, distribución, driver de almacenamiento y versión**.
Se puede consultar esta información usando el comando:

(**docker info**)

El comando docker info muestra el estado de Docker e información clave como:

- Directorio de Docker: dónde se almacenan imágenes y contenedores.

- Driver de almacenamiento: por ejemplo, overlay2 funcionando sobre un sistema de archivos como ext4.

Para más detalles sobre los drivers de almacenamiento, se puede consultar:

(https://docs.docker.com/storage/storagedriver/select-storage-driver/)

**Directorio de Docker:**

Directorio donde se almacena todo lo relacionado con Docker.

(**Docker Root Dir: /var/lib/docker**)

Al utilizar el driver “overlay2” sabemos que:

- Las imágenes se almacenan en: /var/lib/docker/overlay2
- Están formadas por capas
- La configuración de los contenedores se guarda en: /var/lib/docker/containers.
- Para datos persistentes o compartidos, se usan los volúmenes

## 4. REGISTRO: DOCKER HUB

- Docker Hub es la plataforma oficial de registro de imágenes Docker.
- Permite almacenar imágenes públicas o privadas.
- Tienen una gran cantidad de imágenes, con sus correspondientes instrucciones de uso
- Tiene un buscador de imágenes: https://hub.docker.com/search?q=&type=image
- Es el registro por defecto que utiliza Docker, aunque se puede configurar otro o incluso montar un registro privado.

**Más información sobre cómo crear un registro privado en:**

https://www.digitalocean.com/community/tutorials/how-to-set-up-a-private-docker-registry-on-ubuntu-18-04-es


## 5. CREANDO Y ARRANCANDO CONTENEDORES CON “DOCKER RUN”

### 5.1 ¿Qué hace el comando “docker run”?
### 5.2 Creando contenedores sin arrancarlos

**Para crear un contenedor sin arrancarlo (recordamos, “docker run” crea y arranca), existe el
comando “docker create”. La descripción completa del comando “docker create” la podéis
encontrar en (https://docs.docker.com/engine/reference/commandline/create/)**

Es uno de los comandos más usados en Docker, también permite crear contenedores a partir de una imagen y poder arrancarlo casi de inmediato, es por eso que un
error común que tienen varias personas sería pensar que docker run solo arranca contenedores, debido a ello en cada ejecución crea un nuevo contenedor.

La descripción completa del comando “docker run” la podéis encontrar en:

https://docs.docker.com/engine/reference/commandline/run/

### 5.3 Repasando caso práctico “Hello World”

Comando para comprobar que funciona docker:

(**docker run hello-world**)

#### 5.3.1 Repaso parte 1: obteniendo la imagen

La documentación en Docker Hub del contenedor que estamos lanzando la tenemos disponible en
https://hub.docker.com/_/hello-world


Ahí se nos indica que la imagen “hello-word:latest” no está localmente en nuestro sistema. Al no
estar, se descarga del registro por defecto (normalmente Docker Hub) y se almacena localmente.

De hecho, si volvemos a hacer el comando “docker run hello-world”, al tener la imagen ya en el
sistema, no nos aparecerá este texto, ya que la imagen la tenemos almacenada localmente.

Aunque escribamos solo "hello-world", Docker usa en realidad la versión con etiqueta latest (última versión disponible).
Para instalar una versión específica, debemos usar el formato "imagen:nombreversion".


#### 5.3.2 Repaso parte 2: el contenedor se crea y ejecuta un comando

Una vez descargada la imagen, se crea el contenedor, se inicia y ejecuta un proceso. Este proceso
lo podemos proporcionar dentro de la orden “docker run” o si, como en el caso concreto de este
ejemplo, no lo hemos proporcionado, ejecutará un comando predefinido por la propia imagen.

En este caso concreto, al no haber especificado ningún comando, al iniciarse el contenedor lanza
un programa por defecto llamado “hello” y nos muestra por la salida estándar información de
como Docker nos ha generado un mensaje.

Si tenéis curiosidad por ver el código fuente del programa “hello”, está disponible en
https://github.com/docker-library/hello-world/blob/master/hello.c

El programa muestra un mensaje que explica cómo el cliente de Docker se conectó con el servicio, descargó la imagen (si no estaba localmente), 
creó un contenedor con un comando por defecto y envió el resultado a la terminal.

## 6. LISTAR CONTENEDORES DISPONIBLES EN EL SISTEMA CON “DOCKER PS”

Mediante el comando “docker ps” podemos listar los contenedores en ejecución en el sistema. Si
ejecutamos el siguiente comando:

(**docker ps**)

Nos aparecerá un listado como este si no tenemos ningún contenedor en ejecución o si tenemos contenedores en ejecución, 
nos saldrá la lista correspondiente.

Lanzando el siguiente comando:

(**docker ps -a**)

Obtendremos un listado de todos los contenedores, tanto aquellos en funcionamiento como aquellos que están parados.

**La información que obtenemos de los contenedores es la siguiente:**

- CONTAINER_ID: identificador único del contenedor (versión 12 primeros caracteres).
- IMAGE: imagen utilizada para crear el contenedor.
- COMMAND: comando que se lanza al arrancar el contenedor.
- CREATED: cuando se creó el contenedor.
- STATUS: si el contenedor está en marcha o no (indicando cuánto lleva en marcha o cuánto
hace que se paró).
-  PORTS: redirección de puertos del contenedor (lo veremos más adelante en la unidad).
- NAMES: nombre del contenedor. Se puede generar como parámetro al crear el contenedor,
o si no se indica nada, el propio Docker genera un nombre aleatorio.

La descripción completa del comando “docker ps” la podéis encontrar en:
(**https://docs.docker.com/engine/reference/commandline/ps/**)

## 7. PARANDO Y ARRANCANDO CONTENEDORES EXISTENTES CON “DOCKER START/STOP/RESTART”

Para arrancar/parar un contenedor ya creado (recordamos, “docker run” crea y arranca), existen
los comandos “docker start”, “docker stop” y “docker restart”.

La forma más habitual de usar estos comandos, es usar el nombre del comando, seguido del
identificador único o nombre asignado al contendor. Por ejemplo, con identificador:

**(docker start 434d318b3771)**

o con nombre del contenedor

**(docker start stupefied_colden)**

La descripción completa de estos comandos la podéis encontrar en:

- https://docs.docker.com/engine/reference/commandline/start/
- https://docs.docker.com/engine/reference/commandline/stop/
- https://docs.docker.com/engine/reference/commandline/restart/

## 8. INSPECCIONANDO CONTENEDORES CON “DOCKER INSPECT”

El comando “docker inspect” es un comando que nos proporciona diversos detalles de la
configuración de un contenedor. Ofrece distintos datos, entre ellos, identificador único (versión 64
caracteres), almacenamiento, red, imagen en que se basa, etc. Su sintaxis es:

**(docker inspect IDENTIFICADOR/NOMBRE)**

La descripción completa del comando “docker inspect” la podéis encontrar en
https://docs.docker.com/engine/reference/commandline/inspect/.

## 9. EJECUTANDO COMANDOS EN UN CONTENEDOR CON “DOCKER EXEC”

El comando “docker exec” nos permite ejecutar un comando dentro de un contenedor que esté en
ese momento en ejecución. La forma sintaxis habitual para utilizar este comando es la siguiente

**(docker exec [OPCIONES] IDENTIFICADOR/NOMBRE COMANDO [ARGUMENTOS])**

Algunos ejemplos de uso, suponiendo un contenedor en marcha, llamando “contenedor”:

**(docker exec -d contenedor touch /tmp/prueba)**

Ejemplo que se ejecuta en “background”, gracias al parámetro “-d”. Este ejemplo simplemente crea
mediante el comando “touch” un fichero “prueba” en “/tmp”.

**(docker exec -it contenedor bash)**

Orden que ejecutará la “shell” bash en nuestra consola (gracias al parámetro “-it” se enlaza la
entrada y salida estándar a nuestra terminal). A efectos prácticos, con esta orden accederemos a
una “shell” bash dentro del contenedor.

**(docker exec -it -e VAR1=1 contenedor bash)**

Para ejecutar un comando (por ejemplo, en Docker) estableciendo una variable de entorno, se usa el parámetro `-e` seguido de la variable y su valor, como `-e VAR1=1`. Además, con `-it` se enlaza la entrada y salida para disponer de una shell interactiva. Así, al ejecutar `docker run -it -e VAR1=1 imagen bash`, dentro de esa shell estará disponible la variable de entorno `VAR1` con valor `1`, que se puede verificar con el comando `echo $VAR1`.

La descripción completa del comando “docker exec” la podéis encontrar en:

**(https://docs.docker.com/engine/reference/commandline/exec/.)**

## 10. COPIANDO FICHEROS ENTRE ANFITRIÓN Y CONTENEDORES CON “DOCKER CP”

El comando “docker cp” es un comando que nos permite copiar ficheros y directorios del anfitrión
a un contenedor o viceversa. No se permite actualmente la copia de fichero entre contenedores.
Algunos ejemplos de uso:

**(docker cp idcontainer:/tmp/prueba ./)**

Copia el fichero “/tmp/prueba” del contenedor con identificador o nombre “idcontainer” al
directorio actual de la máquina que ejerce como anfitrión.

**(docker cp ./miFichero idcontainer:/tmp)**

Copia el fichero “miFichero” del directorio actual al directorio “/tmp” del contenedor.
La descripción completa del comando “docker cp” la podéis encontrar en

**(https://docs.docker.com/engine/reference/commandline/cp/.)**


## 11. ACCEDIENDO A UN PROCESO EN EJECUCIÓN CON “DOCKER ATTACH”

En algunos casos, deseamos enlazar la entrada o salida estándar de nuestra terminal a un
contenedor que está ejecutando un proceso en segundo plano, de forma similar a la siguiente

**(docker attach [OPCIONES] IDENTIFICADOR/NOMBRE)**

Para probarlo utilizaremos el siguiente ejemplo:

El ejemplo consiste en crear un contenedor que lanza un proceso que genera texto (imprimiendo
la fecha) por la salida estándar de forma indefinida. El comando llama a “sh” con el parámetro -c
(que indica que la siguiente cadena es algo a procesar por la “shell” sh), seguido de una cadena con
un “shell script”. Aquí vemos el comando, que podríamos lanzar en cualquier terminal.

**(sh -c "while true; do $(echo date); sleep 1; done")**

Aplicamos este comando a nuestro ejemplo creando un contenedor:

**(docker run -d --name=muchotexto busybox sh -c "while true; do $(echo date); sleep 1; done")**

Con ese contenedor en marcha, ya podemos probar “docker attach”. Podremos enlazar la entrada
y salida del proceso en ejecución a nuestra terminal y observar el texto generado usando:

**(docker attach muchotexto)**

La descripción completa del comando “docker attach” la podéis encontrar en
(**https://docs.docker.com/engine/reference/commandline/attach/.**)

## 12. OBTENIENDO INFORMACIÓN DE LOS LOGS CON “DOCKER LOGS”

Podemos consultar la información generada con el comando **“docker logs”**

(**docker logs [OPCIONES] IDENTIFICADOR/NOMBRE**)

