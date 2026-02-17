# TEMA 10 – PROYECTO FINAL: DESPLIEGUE DE GLPI CON DOCKER

## 1. Introducción al proyecto final


El proyecto final del curso consiste en el **despliegue completo de una aplicación real de uso profesional** utilizando contenedores Docker, aplicando todos los conocimientos adquiridos a lo largo del curso.

La aplicación seleccionada es **GLPI**, una herramienta ampliamente utilizada en entornos empresariales para la gestión de servicios TI (**ITSM**), inventario y soporte técnico.

Este proyecto **NO utiliza Kubernetes**, ya que su objetivo es consolidar el dominio de Docker, volúmenes, redes y Docker Compose.


## 2. Qué es GLPI

**GLPI (Gestionnaire Libre de Parc Informatique)** es una aplicación web de código abierto que permite:

- Gestión de incidencias (helpdesk)
- Inventario de equipos
- Gestión de activos TI
- Control de usuarios y permisos
- Seguimiento de tareas y SLA

Es una herramienta real, utilizada en empresas y administraciones públicas, lo que convierte este proyecto en un **caso práctico 
profesional**.

## 3. Objetivos del proyecto

El alumnado deberá ser capaz de:

- Desplegar una aplicación web compleja con Docker
- Utilizar Docker Compose
- Configurar volúmenes persistentes
- Gestionar redes entre contenedores
- Documentar correctamente el proceso
- Comprender una arquitectura cliente-servidor real

## 4. Arquitectura del proyecto

La arquitectura del proyecto se basa en **varios contenedores**:

- Contenedor GLPI (PHP + Apache)
- Contenedor base de datos (MariaDB)
- Volúmenes persistentes
- Red Docker dedicada

Componentes:

- Frontend web
- Backend (base de datos)
- Persistencia de datos

## 5. Requisitos del sistema

- Sistema Linux
- Docker instalado
- Docker Compose instalado
- Acceso a Internet
- Navegador web
Editor de texto

## 6. Preparación del entorno


Comprobar versiones:

**(docker --version  
docker compose version)**

Crear un directorio de trabajo:

**(mkdir proyecto_glpi  
cd proyecto_glpi)**



<img width="556" height="94" alt="image" src="https://github.com/user-attachments/assets/55bd9324-a748-46fd-b554-fc59a79ac4c3" />



## 7. Archivo docker-compose.yml

El despliegue se realizará mediante Docker Compose.

Ejemplo de archivo docker-compose.yml:


<img width="431" height="64" alt="image" src="https://github.com/user-attachments/assets/a6ac56ec-3662-427e-8204-21db7e4d4137" />




<img width="1133" height="746" alt="image" src="https://github.com/user-attachments/assets/938fff7f-45f6-44be-83bb-0ef95c37e459" />



## 8. Despliegue de la aplicación

Para iniciar el proyecto:

**(docker compose up -d)**



<img width="738" height="503" alt="image" src="https://github.com/user-attachments/assets/23a75bb8-e268-4a9b-a630-e0ce28291b93" />



Comprobar que los contenedores están en ejecución:

**(docker compose ps)**



<img width="889" height="128" alt="image" src="https://github.com/user-attachments/assets/5d70d0a3-9a5a-40ab-a31f-cbf00928e951" />


## 9. Acceso a GLPI

Abrir el navegador y acceder a:

http://localhost:8080


<img width="1453" height="790" alt="image" src="https://github.com/user-attachments/assets/1153cdf1-83ab-41d1-9f0b-8793fbe60680" />



Desde ahí:

- Seguir el asistente de instalación de GLPI
- Configurar la conexión con la base de datos
- Finalizar la instalación



<img width="961" height="456" alt="image" src="https://github.com/user-attachments/assets/14447e8f-8a5d-409c-828a-c07b76750176" />


## 10. Persistencia de datos

Gracias a los volúmenes:

- La base de datos se conserva
- La configuración de GLPI persiste
- Se pueden reiniciar los contenedores sin perder datos

Esto demuestra el uso correcto de volúmenes Docker.

## 11. Seguridad básica aplicada
 
Durante el proyecto se deben aplicar buenas prácticas:

- Uso de red privada Docker
- No exponer la base de datos
- Uso de contraseñas
- Separación de servicios
- Documentación de configuraciones

## 12. Entrega del proyecto

El alumno debe entregar un PDF que incluya:

**1. Explicación de la arquitectura**

La arquitectura del proyecto se basa en el modelo cliente-servidor donde el navegador web accede a través de localhost:8080 al contenedor glpi_app, siendo una de (imagen diouxx/glpi con PHP+Apache), que a su vez se comunica internamente por la red Docker glpi_net con el contenedor glpi_db (MariaDB 10.6). Este último no expone los puertos al host por seguridad, y ambos servicios utilizan volúmenes persistentes: db_data para los datos MySQL en /var/lib/mysql y glpi_data para los archivos de la aplicación en /var/www/html/glpi, garantizando que la información no se borre de los contenedores.

**2. Archivo docker-compose.yml**

Aquí tenemos la arquitectura docker-compose.yml


<img width="589" height="373" alt="image" src="https://github.com/user-attachments/assets/20c71c4b-c84a-4ea2-9e3b-9a345031da48" />


**3. Capturas de:
    - Contenedores en ejecución
    - Acceso a GLPI**
    

<img width="465" height="49" alt="image" src="https://github.com/user-attachments/assets/54639467-4bb3-41c8-8c90-a9d47838046f" />



<img width="916" height="447" alt="image" src="https://github.com/user-attachments/assets/17aa9de1-d02c-40fe-a7d1-f199cc7c88e5" />

   
**4. Explicación del uso de volúmenes**

Hice docker compose down,es decir, que borra todo lo que haya en el contenedor, luego hiuce docker-compose up -d y el login glpi/glpi seguía funcionando, debiod a ello los volúmenes db_data (base datos) y glpi_data (archivos) guardan todo fuera de los contenedores, por eso no se pierde nada.

Es por ello que los volúmenes son recomendables crearlos para evitar perder la información.


**5. Conclusiones personales**





## 13. Criterios de evaluación

| Criterio                | Puntos |
|--------------------------|--------|
| Docker Compose correcto  | 2      |
| Contenedores funcionales | 2      |
| GLPI accesible           | 2      |
| Uso de volúmenes         | 2      |
| Documentación            | 2      |
| **TOTAL**                | **10** |



## 14. Ampliación (opcional)

Para alumnado avanzado:

- Uso de HTTPS
- Copias de seguridad de la base de datos
- Cambio de puertos
- Personalización de GLPI
- Control de usuarios



## 15. Resumen

Este proyecto final permite:

- Aplicar todos los conceptos de Docker
- Trabajar con una aplicación real
- Simular un entorno profesional
- Desarrollar competencias prácticas de ASIR

Con este proyecto se cierra el curso de forma coherente y aplicada.


**¡ESCRIBE db glpi glpi → CONTINUAR → YA ESTÁ!**
