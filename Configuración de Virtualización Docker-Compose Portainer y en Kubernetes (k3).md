# Práctica: Configuración de Virtualización Docker · Docker-Compose, Portainer, Kubernetes (k3s)

**Paso 1 – Verificación de Docker instalado**

A continuación hemos realizado la comprobación de que Docker-Engine está instalado en su versión v28.1.1, y de que el servicio se encuentra activo y que el usuario dispone de los permisos necesarios para trabajar con él.

![captura 1](https://github.com/user-attachments/assets/1921f196-b6ad-40cb-b2be-ce57bfbe3296)

**Paso 2 – Instalación de Docker Compose v2**

Se instala el plugin oficial docker-compose-plugin a través de apt, actualizando previamente los repositorios del sistema con apt update. Una vez finalizada la instalación se verifica que la versión disponible es Docker Compose v2.35.1.

![captura 2](https://github.com/user-attachments/assets/efe84c40-8e48-419b-b13e-b9403a799ca3)

**Paso 3 – Creación de la estructura del proyecto**

Se crea el directorio de trabajo /mindverse/proyecto con los permisos de superusuario y se accede a él. Dentro se define el fichero docker-compose.yml mediante el editor de textos nano, donde se declaran los dos servicios principales: web (**nginx**) y db (mariadb).

![captura 3](https://github.com/user-attachments/assets/c5e55c53-4e1f-44ed-897f-b7a40b5b0181)

**Paso 4 – Primer despliegue con Docker-Compose**

Se lanza el stack en segundo plano con 'docker compose up -d'. Durante el proceso se descargan las imágenes nginx:alpine y mariadb:10.11, se crea la red proyecto_default y el volumen proyecto_db_data, y arrancan los contenedores proyecto-db-1 y proyecto-web-1.

![captura 3](https://github.com/user-attachments/assets/014faa78-bc65-4030-ab3b-fb376c90ae8c)

**Paso 5 – Verificación de logs de contenedores**

Mediante 'docker compose logs -f' se revisan los logs en tiempo real de ambos contenedores. Se confirma que nginx arranca sin errores y que MariaDB completa correctamente todos sus procesos de inicialización.

![captura 3](https://github.com/user-attachments/assets/297e914e-7085-4c01-9c4f-a0513400bb55) ![captura 4](https://github.com/user-attachments/assets/f7c91d4c-f343-4dd8-a12f-c895074eaf8c)

**Paso 6 – Configuración de permisos de usuario Docker**

Se añade el usuario actual al grupo docker mediante 'usermod -aG docker $USER' y se aplica el cambio en la sesión activa con 'newgrp docker'. Se actualiza también la lista de paquetes con apt update.

![captura 2](https://github.com/user-attachments/assets/edbe83fc-2ffb-4d84-aff6-8679abfdd7df)

**Paso 7 – Creación del Dockerfile personalizado**

Se genera la estructura myapp/src y se escribe un Dockerfile que parte de la imagen base php:8.2-apache, instala las extensiones PHP necesarias y copia el código fuente al contenedor. Se incluye un fichero index.php de prueba que devuelve el mensaje 'MindVerse Solutions - OK'.

![captura 5](https://github.com/user-attachments/assets/96b4acc8-32bf-41df-bfa8-61021bcc117a)

**Paso 8 – Construcción de la imagen propia (docker compose build**

Se construye la imagen personalizada 'proyecto-app' ejecutando docker compose build. El proceso descarga y procesa todas las capas necesarias de php:8.2-apache y genera la imagen final lista para ser desplegada.

![captura 6](https://github.com/user-attachments/assets/aae350f9-b151-47b4-9812-a5d422e514cf)

**Paso 9 – Stack completo con 3 servicios activos**

Con los tres servicios en marcha se verifica el estado del stack con docker compose ps. Los contenedores proyecto-web-1 (nginx en el puerto 8080), proyecto-db-1 (mariadb en el puerto 3306) y proyecto-app-1 (php-apache en el puerto 8081) aparecen todos en estado Running.

![captura 6](https://github.com/user-attachments/assets/5b3a9030-ebb6-41cf-8802-bdfda200a44a)

**Paso 10 – Portainer: instalación y contenedores visibles**

Se crea el volumen portainer_data y se despliega el contenedor Portainer CE mediante docker run, exponiéndolo en los puertos 9000 y 9443. Al ejecutar docker ps se confirma que los 4 contenedores están activos, incluyendo el propio Portainer.

![captura 6](https://github.com/user-attachments/assets/1d021103-f456-4037-9ad0-342dad02a28b)

**Paso 11 – Portainer: interfaz gráfica (GUI)**

Se accede a la interfaz web de Portainer en http://localhost:9000. Desde el panel se visualizan todos los contenedores del entorno: portainer, proyecto-app-1, proyecto-db-1 y proyecto-web-1 en estado running, además de los contenedores dockerlamp que aparecen como exited.

![captura 8](https://github.com/user-attachments/assets/73946051-1e5e-45fa-8ecc-1e5182fb2ef8)

**Paso 12 – Instalación de Kubernetes (k3s)**

Se instala k3s v1.35.5 sobre Ubuntu utilizando el script oficial mediante el comando 'curl -sfL https://get.k3s.io | sh -'. El proceso descarga el binario, configura el servicio en systemd y lo habilita para que arranque automáticamente con el sistema.

![captura 9](https://github.com/user-attachments/assets/0a4446e0-26ff-4f91-9228-3c3ba60da314)

**Paso 13 – Verificación del cluster Kubernetes**

Se comprueba que el servicio k3s está active y running con systemctl. A continuación se ejecuta 'kubectl get nodes' para verificar el estado del cluster, donde el nodo grupo3 aparece como Ready con el rol control-plane y la versión v1.35.5+k3s1.

![captura 10](https://github.com/user-attachments/assets/a84dc954-2dc3-4994-b216-ace3ffff7322) ![captura 11](https://github.com/user-attachments/assets/99324019-57de-40cc-afd7-c086a80cb010)

**Paso 14 – Configuración de kubectl para el usuario**

Se crea el directorio ~/.kube y se copia el fichero k3s.yaml como configuración de kubectl, ajustando los permisos con chown. Se establece la variable de entorno KUBECONFIG y se comprueba que 'kubectl get nodes' funciona correctamente sin necesidad de usar sudo.

![captura 13](https://github.com/user-attachments/assets/2a5b2e06-405c-4ea3-a281-7222c1ce1bf1)

**Paso 15 – Despliegue de aplicación en Kubernetes**

Se redacta el fichero deployment.yaml definiendo un Deployment con 2 réplicas de nginx:alpine y un Service de tipo NodePort accesible por el puerto 30080. Se aplica la configuración con 'kubectl apply -f' y se verifica que tanto los pods como el servicio se han creado correctamente.

![captura 14](https://github.com/user-attachments/assets/5f181a91-4b84-495b-97f8-37becc386256) ![captura 15](https://github.com/user-attachments/assets/a914380d-881d-47fa-95e6-6e733982ea90)

**Paso 16 – Verificación final: nginx en Kubernetes (puerto 30080)**

Se accede a http://localhost:30080 y se confirma que nginx responde correctamente desde dentro del cluster k3s. La página de bienvenida 'Welcome to nginx!' indica que el despliegue es completo y funcional.

![captura 16](https://github.com/user-attachments/assets/d7def332-89e7-4481-bbba-d63c0c86c593)

**Esta practica también las hemos en el servidor, ya que allí teníamos puesto todo el proyecto, ya que se nos hizo imposible realizarlo fuera del centro en estas dos prácticas.**
