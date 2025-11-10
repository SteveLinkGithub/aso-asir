# Administración de Procesos en Linux mediante Comandos Bash

RA2. Administra procesos del sistema describiéndolos y aplicando criterios de seguridad y eficiencia.

Criterio de Evaluación (**CE**)

Descripción del Criterio

Tarea Práctica (**Comandos Bash**)


**a)**

Se han descrito el concepto de proceso del sistema, tipos, estados y ciclo de vida.

**Tarea a:** Utilice el comando ps junto con opciones de formato (ps -eo state,pid,cmd) y el comando grep para identificar y contar cuántos procesos del sistema se encuentran en los estados 'dormido' (S) o 'zombie' (Z).

<img width="662" height="53" alt="image" src="https://github.com/user-attachments/assets/ef517238-3e04-4979-b97d-792715b377b3" />

El comando (**ps -eo state,pid,cmd | grep -E '^[SZ]' | wc -l**), lo que hace es listar todos los procesos, para después filtrarlos mediante la **S (procesos dormidos)**
o **Z (procesos zombie)** y cuénta cuántos procesos hay en total.

**b)**

Se han utilizado interrupciones y excepciones para describir los eventos internos del procesador.

**Tarea b:** Examine el sistema de archivos /proc y documente la tabla de interrupciones leyendo el archivo /proc/interrupts. Describa qué tipo de dispositivo está asociado con la interrupción ID 1 (típicamente el teclado/mouse).

<img width="588" height="548" alt="image" src="https://github.com/user-attachments/assets/5bcc75c9-51c5-4ff6-8ee2-38a562103307" />



**c)**

Se ha diferenciado entre proceso, hilo y trabajo.

**Tarea c:** Inicie un comando en segundo plano (e.g., sleep 600 &) para crear un "trabajo". Luego, use el comando jobs para listar el trabajo y el comando ps -L para identificar los hilos (LWP) de un proceso multiproceso del sistema, diferenciándolos del PID principal.

**d)**

Se han realizado tareas de creación, manipulación y terminación de procesos.

**Tarea d:** Cree un proceso (e.g., un loop infinito en Bash o sleep 500 &). Manipule su prioridad utilizando el comando renice para reducirla. Finalmente, termine dicho proceso de forma forzosa usando el comando kill con la señal adecuada (por ejemplo, SIGKILL o -9).

**e)**

Se ha utilizado el sistema de archivos como medio lógico para el registro e identificación de los procesos del sistema.

**Tarea e:** Determine el PID de su shell actual ($$). Navegue al directorio correspondiente en el sistema de archivos /proc (cd /proc/<PID>) y localice los links simbólicos que apuntan a los archivos abiertos por su shell (/proc/<PID>/fd) y el ejecutable original.

**f)**

Se han utilizado herramientas gráficas y comandos para el control y seguimiento de los procesos del sistema.

**Tarea f:** Utilice el comando top o htop (si está instalado) para controlar y realizar un seguimiento continuo de los procesos. Identifique el proceso que está consumiendo la mayor cantidad de recursos de CPU y genere un informe filtrado de dicho proceso usando el comando ps.

**g)**

Se ha comprobado la secuencia de arranque del sistema, los procesos implicados y la relación entre ellos.

**Tarea g:** Compruebe la jerarquía de los procesos del sistema utilizando el comando pstree. Identifique específicamente el proceso con PID 1 (el proceso raíz del sistema, fundamental en la secuencia de arranque) y verifique cuáles son sus procesos hijos directos.

**h)**

Se han tomado medidas de seguridad ante la aparición de procesos no identificados.

**Tarea h:** Simule la identificación de un proceso no reconocido (por ejemplo, un proceso que corre bajo un usuario sin privilegios que consume mucha CPU). Utilice el comando lsof -i para verificar si dicho proceso sospechoso está estableciendo conexiones de red y tome medidas de seguridad terminándolo si es necesario.

**i)**

Se han documentado los procesos habituales del sistema, su función y relación entre ellos.

**Tarea i:** Documente la función, el PID y el usuario propietario de dos procesos habituales del sistema (por ejemplo, cron o sshd). Para la documentación, utilice comandos de inspección como systemctl status (si su sistema usa systemd) y ps -fp <PID> para ver el árbol de procesos padre-hijo.
