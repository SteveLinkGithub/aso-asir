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

