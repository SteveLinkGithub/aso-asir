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


## 7. Archivo docker-compose.yml

El despliegue se realizará mediante Docker Compose.

Ejemplo de archivo docker-compose.yml:


## 8. Despliegue de la aplicación

Para iniciar el proyecto:

**(docker compose up -d)**

Comprobar que los contenedores están en ejecución:

**(docker compose ps)**

## 9. Acceso a GLPI

Abrir el navegador y acceder a:

http://localhost:8080

Desde ahí:

- Seguir el asistente de instalación de GLPI
- Configurar la conexión con la base de datos
- Finalizar la instalación

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

1. Explicación de la arquitectura
2. Archivo docker-compose.yml
3. Capturas de:
    - Contenedores en ejecución
    - Acceso a GLPI
4. Explicación del uso de volúmenes
5. Conclusiones personales

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
