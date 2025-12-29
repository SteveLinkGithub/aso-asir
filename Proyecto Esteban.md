# Proyecto guiado: Administración de Active Directory Domain Services


**Este proyecto guiado le ayuda a prepararse para administrar los servicios de dominio de Active Directory, entre los que se incluyen:**

- Creación e implementación de dominios.
- Configurar objetos de directiva de grupo.
- Establecimiento y aplicación de contraseñas.
- Mantener la seguridad de Active Directory.

### Objetivos de aprendizaje

**En este módulo, practicará cómo:**

- Configure las operaciones del controlador de dominio.
- Configure las operaciones de administración de usuarios.
- Administrar directivas de contraseñas.
- Configure las opciones de seguridad.


### Requisitos previos

**Conocimientos y experiencia trabajando con:**

- Windows Server.
- Principales tecnologías de red.

## Introducción

Le damos la bienvenida a esta experiencia interactiva de validación de aptitudes. Completar este módulo le ayuda a prepararse para la evaluación de Administración de Active Directory Domain Services.

Este módulo trata los pasos principales para implementar, configurar y mantener un controlador de dominio. Ofrece una oportunidad para promover un controlador de dominio en un entorno virtualizado mediante una máquina con Windows 10 o Windows 11.

## Escenario

Imagine que es administrador del sistema de una empresa de tamaño medio que está expandiendo su infraestructura de red. Se le ha encargado configurar un nuevo controlador de dominio para administrar el acceso y la seguridad de los usuarios. Sin embargo, debe usar el hardware existente que ejecute Windows 10 o Windows 11 debido a restricciones en el presupuesto. Este escenario le guiará a través del proceso de configuración de un entorno virtualizado en su máquina para ejecutar dos máquinas virtuales de Windows Server 2022 Evaluation Edition.

## Objetivos de aprendizaje

**En este módulo, practicará cómo:**

- Configure operaciones del controlador de dominio.
- Configure operaciones de administración de usuarios.
- Administre directivas de contraseña.
- Configure opciones de seguridad.

# Preparación

Se trata de un proyecto guiado, donde se completa una serie de tareas. Es esencial completar las unidades en orden. 
Cada unidad requiere recursos y configuración de unidades anteriores para funcionar correctamente.

## Información general del proyecto
En este proyecto guiado, se describen los pasos principales para crear, configurar y mantener un controlador de dominio. 
También tiene la oportunidad de promover un controlador de dominio.

## Configurar

Para reducir los requisitos de acceso a recursos (como el acceso a Windows Server o una suscripción a Microsoft Azure), este proyecto guiado usa una máquina Windows 10 o Windows 11 para ejecutar un entorno virtualizado. Configuras un subsistema de Hyper-V de un equipo con Windows 10 o Windows 11 para admitir las dos máquinas virtuales de Windows Server 2022 Evaluation Edition que usa en este proyecto. Necesita la edición Professional o Enterprise de Windows 10 o Windows 11 para realizar estas tareas.

El equipo que funciona como host de virtualización de Hyper-V debe tener al menos 16 GB de RAM. También puede usar una versión de evaluación de Windows Server con el rol de Hyper-V instalado como host para estas máquinas virtuales o para configurar una plataforma de virtualización de terceros para hospedar ambas máquinas virtuales. Los ejercicios y tareas de este laboratorio usan Windows 11 al describir el host de Hyper-V. Las opciones que se presentan aquí facilitan la localización de archivos de máquinas virtuales de gran tamaño si desea quitar la configuración después de finalizar con el proyecto.

La sección Setup consta de tres tareas principales:

**Instalar Hyper-V**

- Creación de una máquina virtual del controlador de dominio de Windows Server
- Crear servidor miembro de dominio de Windows Server
- Inicie el ejercicio y siga las instrucciones. Cuando haya terminado, asegúrese de volver a esta página para continuar con el aprendizaje.

**link a la iso:** (https://www.microsoft.com/es-es/evalcenter/download-windows-server-2022)

Para empezar la instalación la hare en virtual box, me he instalado la iso de la página oficial de microsoft, en vez de instalarmelo,
en mi máquina real.





