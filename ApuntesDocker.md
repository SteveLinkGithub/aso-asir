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
