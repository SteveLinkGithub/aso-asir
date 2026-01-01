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
en mi máquina real, y configuraremos paso a paso, la máquina de windows server 2022 y pondremos de nombre **(TAILWIND-DC1)**, y seleccionaremos la experiencia de escritorio,
después le daremos a instalación personalizada y seguiremos los pasos para instalarlo, le pondremos contraseña al administrador que en nuestro caso sería la **(Pa55w.rdPa55w.rd)**.
También miraremos la configuración de red y seguiremos los pasos de la preparación de windows server.

<img width="322" height="245" alt="image" src="https://github.com/user-attachments/assets/49a9d40a-c640-4966-af99-dd4e42c282fb" />

<img width="516" height="392" alt="image" src="https://github.com/user-attachments/assets/e61e3082-b4a1-46ca-9542-2e39839065f9" />

<img width="332" height="249" alt="image" src="https://github.com/user-attachments/assets/babb8155-6169-44e0-9ce1-382fff2ff165" />

<img width="620" height="449" alt="image" src="https://github.com/user-attachments/assets/952fa4ca-dded-4970-a672-1b1367fc25b0" />


Como vemos en la configuración de red no me deja usar la propuesta así que por eso lo he dejado en dhcp.
<img width="203" height="233" alt="image" src="https://github.com/user-attachments/assets/b2cf559b-307d-4dc5-94b4-966f9847b288" />

A continuación cambiaremos el nombre del equipo.

<img width="341" height="160" alt="image" src="https://github.com/user-attachments/assets/baa88302-8c3c-4039-8b08-dd8ba611cba3" />


<img width="179" height="17" alt="image" src="https://github.com/user-attachments/assets/882bdda0-60b0-4c3b-a449-2278a5a96760" />

 A continuación agregaremos el rol de servicio de dominio de active directory en roles y características, una vez agregado el servicio
 lo que haremos será a darle a instalar y renicio automático.
 
<img width="410" height="288" alt="image" src="https://github.com/user-attachments/assets/c6d7cf92-ef1f-4937-ae00-23834af4259e" />

<img width="395" height="299" alt="image" src="https://github.com/user-attachments/assets/5664a92b-94c6-4bae-b1a2-551f144dc642" />

<img width="397" height="281" alt="image" src="https://github.com/user-attachments/assets/82b1cafd-e7c7-43fe-a9a3-c5fd8ba8f007" />

<img width="400" height="287" alt="image" src="https://github.com/user-attachments/assets/7282196d-30f0-43ad-a7d8-25e41c80dfda" />

<img width="833" height="388" alt="image" src="https://github.com/user-attachments/assets/914d3579-461d-48eb-85e2-81b3b7a457f3" />


Ahora promocionaremos el servidor a controlador de dominio, y procederemos con la configuración del bosque que hemos creado, y le daremos
a siguiente en el resto de opciones ya que no las tocaremos, hasta a llegar a la parte de la instalación.

<img width="387" height="286" alt="image" src="https://github.com/user-attachments/assets/13a9162b-a6a1-4f64-8685-563c9b70bfbc" />


<img width="386" height="286" alt="image" src="https://github.com/user-attachments/assets/3ec3db40-086b-4a2e-9307-025d7e90116e" />


<img width="384" height="282" alt="image" src="https://github.com/user-attachments/assets/84ade991-07b8-4264-87e3-3a83c9b70054" />


<img width="383" height="281" alt="image" src="https://github.com/user-attachments/assets/a454c841-d4e1-4401-8767-f46474cea58b" />


<img width="383" height="281" alt="image" src="https://github.com/user-attachments/assets/bd4f19d8-5133-4c03-946e-9d330ac7d6d6" />


<img width="386" height="282" alt="image" src="https://github.com/user-attachments/assets/0dde5552-9e0c-40ad-90c8-fa6cfdcf0d3e" />


Una vez instalado, nos meteremos en el dominio como **tailwindtraders\administrator** con la contraseña de administrador predeterminada **(Pa55w.rdPa55w.rd)**


<img width="385" height="279" alt="image" src="https://github.com/user-attachments/assets/20d47419-e1a1-4800-bdd2-9c251c170c3e" />


<img width="519" height="332" alt="image" src="https://github.com/user-attachments/assets/0db28587-da2e-4bef-ab56-299927eaa51c" />


# Crear un servidor miembro del dominio de Windows Server

En esta tarea, se implementa y configura un servidor miembro del dominio de Windows Server 2022 para el laboratorio donde se realizan tareas relacionadas con la credencial de habilidad aplicada.
Esta tarea también utiliza el archivo ISO de la edición de evaluación.

A continuación crearemos el servidor miembro del dominio, siguiendo los pasos de la tarea, y cambiaremos el nombre del equipo.

También configuraremos la red del **(TAILWIND-MBR1)**.


<img width="395" height="299" alt="image" src="https://github.com/user-attachments/assets/c3f6522a-d8fb-4b07-8dfe-8a2b345f8644" />




<img width="180" height="15" alt="image" src="https://github.com/user-attachments/assets/aa2bc91f-2622-4e07-aabc-9200c4a80c8a" />




<img width="344" height="110" alt="image" src="https://github.com/user-attachments/assets/2a158a7a-ddc0-4e6f-8d68-f2097b395bf9" />




<img width="633" height="472" alt="image" src="https://github.com/user-attachments/assets/990bedf2-d1df-4d5a-b36b-74baf12cf310" />





