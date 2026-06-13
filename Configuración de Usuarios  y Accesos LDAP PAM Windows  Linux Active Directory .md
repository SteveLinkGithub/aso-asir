# PRÁCTICA: CONFIGURACIÓN DE USUARIOS Y ACCESOS PAM / LDAP Linux / Active Directory Windows

---

## BLOQUE 1 — PAM (PLUGGABLE AUTHENTICATION MODULES)

### 1. Introducción a PAM

PAM (Pluggable Authentication Modules) es el sistema de autenticación modular de Linux. Permite configurar de forma centralizada cómo el sistema gestiona la autenticación, autorización y cambio de contraseñas sin modificar las aplicaciones individualmente.

En esta práctica se configuran los siguientes módulos:

- **pam_pwquality** — Política de complejidad de contraseñas
- **pam_faillock** — Bloqueo de cuentas tras intentos fallidos
- **pam_access** — Restricción de acceso por usuario/grupo
- **pam_limits** — Límites de recursos del sistema

---

### 2. Inspección de la estructura PAM

Antes de modificar nada se examina la estructura de ficheros de configuración PAM y el contenido de los ficheros principales.

**Comandos ejecutados:**

```bash
ls /etc/pam.d/
cat /etc/pam.d/common-auth
cat /etc/pam.d/common-password
```

El directorio `/etc/pam.d/` contiene un fichero por cada servicio. En `common-auth` se observan `pam_unix.so` (autenticación local) y `pam_sss.so` (preparado para SSSD/LDAP). En `common-password` aparece `pam_pwquality.so` con `retry=3`.

![captura 17](https://github.com/user-attachments/assets/ac50d6c3-8b39-4db9-8c1b-1574c7264021)

---

### 3. Creación de usuarios y grupos

Se crean dos grupos departamentales y tres usuarios de prueba con distintos niveles de acceso.

**Creación de grupos:**

```bash
sudo groupadd it
sudo groupadd rrhh
```

**Creación de usuarios:**

```bash
sudo useradd -m -s /bin/bash -G it alumno1
sudo useradd -m -s /bin/bash -G rrhh alumno2
sudo useradd -m -s /bin/bash alumno3
```

**Verificación:**

```bash
cat /etc/passwd | grep alumno
id alumno1 && id alumno2 && id alumno3
```

![captura 18](https://github.com/user-attachments/assets/31ac4b9d-65cb-4ace-a5a6-68f5d7eb08fd)
![captura 19](https://github.com/user-attachments/assets/151b434a-551e-4416-8199-55b89bfb31cf)

---

### 4. Política de contraseñas (pam_pwquality)

Se instala y configura `pam_pwquality` para exigir contraseñas robustas con múltiples tipos de caracteres.

**Instalación:**

```bash
sudo apt install libpam-pwquality -y
```

**Copias de seguridad:**

```bash
sudo cp /etc/pam.d/common-password /etc/pam.d/common-password.bak
sudo cp /etc/security/pwquality.conf /etc/security/pwquality.conf.bak
```

**Configuración de `/etc/security/pwquality.conf`:**

```bash
sudo nano /etc/security/pwquality.conf
```

**Parámetros aplicados:**

```
minlen = 12       # Longitud mínima 12 caracteres
dcredit = -1      # Al menos 1 dígito
ucredit = -1      # Al menos 1 mayúscula
lcredit = -1      # Al menos 1 minúscula
ocredit = -1      # Al menos 1 carácter especial
maxrepeat = 3     # Máximo 3 caracteres consecutivos iguales
usercheck = 1     # No puede contener el nombre de usuario
retry = 3         # 3 intentos antes de error
```

![captura 20](https://github.com/user-attachments/assets/27b6f73b-7e72-4841-9d57-6d33da81774c)
![captura 21](https://github.com/user-attachments/assets/fa9e50f6-1178-46cb-804d-a1ee8afaa0ca)

**Prueba de la política** — se introduce primero una contraseña sin mayúsculas y el sistema la rechaza. Luego se acepta `Mindverse2025!`:

![captura 22](https://github.com/user-attachments/assets/88e91a1c-db25-4320-b131-d5426d712dcf)

---

### 5. Bloqueo por intentos fallidos (faillock)

Se configura `faillock` para bloquear automáticamente una cuenta tras 3 intentos fallidos de autenticación.

**Copia de seguridad:**

```bash
sudo cp /etc/pam.d/common-auth /etc/pam.d/common-auth.bak
```

**Configuración de `/etc/security/faillock.conf`:**

```bash
sudo nano /etc/security/faillock.conf
```

**Parámetros configurados:**

```
deny = 3            # Bloqueo tras 3 intentos fallidos
unlock_time = 300   # Desbloqueo automático a los 5 minutos
fail_interval = 900 # Ventana de 15 minutos para contar fallos
silent              # No informa al usuario del bloqueo
audit               # Registra en el log del sistema
```

![captura 23](https://github.com/user-attachments/assets/1d0a1edf-cb3c-488d-9833-6be19aeee6f1)

**Prueba del bloqueo:**

```bash
su - alumno1          # Contraseña incorrecta x3
sudo faillock --user alumno1
sudo faillock --user alumno1 --reset
```

![captura 24](https://github.com/user-attachments/assets/bdc0ff84-628e-4d4b-aaa2-bffc260d8399)

---

### 6. Restricción de acceso por grupos (pam_access)

Se configura el `pam_access` para controlar qué usuarios pueden iniciar sesión, permitiendo el grupo `it` y `alumno1`, y denegando a `alumno3`.

**Copia de seguridad y edición:**

```bash
sudo cp /etc/security/access.conf /etc/security/access.conf.bak
sudo nano /etc/security/access.conf
```

**Reglas añadidas al final del fichero:**

```
+ : root    : LOCAL   # root solo desde consola local
+ : (it)    : ALL     # grupo it acceso total
+ : alumno1 : LOCAL   # alumno1 solo local
- : alumno3 : ALL     # alumno3 denegado
- : ALL     : ALL     # resto denegado
```

![captura 25](https://github.com/user-attachments/assets/3ab3957e-0dfa-4daa-9449-da6b6d3b7a7b)

**Activación del módulo en `common-account` y `su`:**

```bash
sudo nano /etc/pam.d/common-account   # Añadir: account required pam_access.so
sudo nano /etc/pam.d/su               # Añadir: account required pam_access.so
```

![captura 26](https://github.com/user-attachments/assets/d807c5d7-5efa-4f0a-825d-d26d4776dedf)

**Verificación:**

```bash
grep 'pam_access' /etc/pam.d/common-account
grep 'pam_access' /etc/pam.d/su
tail -6 /etc/security/access.conf
```

![captura 27](https://github.com/user-attachments/assets/9a1665f6-f92c-44b1-9bd4-73faeb6cd09a)
![captura 28](https://github.com/user-attachments/assets/0b4a4154-961c-49a1-ae2b-1557e730b961)

---

### 7. Límites de recursos (pam_limits)

Se configura `pam_limits` para establecer restricciones de recursos por usuario y grupo.

**Edición de `/etc/security/limits.conf`:**

```bash
sudo nano /etc/security/limits.conf
```

**Líneas añadidas al final:**

```
alumno1  soft  nproc     50     # Máx 50 procesos (aviso)
alumno1  hard  nproc     100    # Límite duro 100 procesos
@it      soft  nofile    1024   # Grupo it: 1024 ficheros abiertos
@it      hard  nofile    2048   # Grupo it: límite duro 2048
@rrhh    hard  nproc     30     # Grupo rrhh: máx 30 procesos
*        hard  maxlogins 3      # Todos: máx 3 sesiones simultáneas
```

![captura 29](https://github.com/user-attachments/assets/46ed3cd6-3db0-4e6c-bfb6-dcf050fbbbe7)

**Verificación:**

```bash
tail -10 /etc/security/limits.conf
ulimit -a
su - alumno1 -c "ulimit -a"
```

![captura 30](https://github.com/user-attachments/assets/29093393-218d-4fa6-a94a-84c8bb9feece)

---

### 8. Verificación final y logs

Se revisan los logs de autenticación, el historial de sesiones y el estado de los módulos PAM activos.

**Log de autenticación:**

```bash
sudo tail -20 /var/log/auth.log
last
```

El `auth.log` muestra toda la actividad: sesiones abiertas/cerradas de alumno1-3, intentos fallidos y operaciones sudo realizadas durante la práctica.

![captura 31](https://github.com/user-attachments/assets/d641eb9b-8d2f-4ca0-b582-187058b3510e)

**Módulos PAM activos:**

```bash
sudo pam-auth-update --list
```

Módulos activos confirmados: Pwquality, Unix authentication, SSS authentication, Register user sessions in systemd, GNOME Keyring Daemon, Inheritable Capabilities Management.

![captura 32](https://github.com/user-attachments/assets/de819652-a290-4648-b441-35d968718504)

---

## BLOQUE 2 — OPENLDAP EN UBUNTU LINUX

### 9. Instalación de OpenLDAP (slapd)

Se instala el servidor OpenLDAP (`slapd`) junto con las utilidades de cliente `ldap-utils`. Durante la instalación se establece la contraseña del administrador LDAP.

```bash
sudo apt update
sudo apt install slapd ldap-utils -y
```

> Durante la instalación: contraseña de administrador LDAP → `Mindverse2025!`

**Verificación del servicio:**

```bash
sudo systemctl status slapd
```

![captura 33](https://github.com/user-attachments/assets/fa6726dd-c2c1-49fc-99f0-656f2a92c856)
![captura 34](https://github.com/user-attachments/assets/6fc91edb-624e-495e-9a3f-368ce2304a98)

---

### 10. Configuración del dominio LDAP

Se reconfigura `slapd` para establecer el dominio `mindverse.local` y el nombre de la organización `MindVerse Solutions`.

```bash
sudo dpkg-reconfigure slapd
```

**Respuestas al asistente de configuración:**

| Pregunta | Respuesta |
|---|---|
| ¿Omitir configuración? | No |
| Nombre DNS del dominio | `mindverse.local` |
| Nombre de la organización | `MindVerse Solutions` |
| Contraseña administrador | `Mindverse2025!` |
| ¿Eliminar base de datos al purgar? | No |
| ¿Mover base de datos antigua? | Sí |

**Verificación de la base de datos LDAP:**

```bash
sudo slapcat | head -20
```

La salida confirma: `dn: dc=mindverse,dc=local`, `o: MindVerse Solutions`, administrador `cn=admin,dc=mindverse,dc=local`.

![captura 35](https://github.com/user-attachments/assets/a3029a43-5ccb-458e-a830-f5cac12835e2)

---

### 11. Creación de unidades organizativas (OUs)

Se crea la estructura jerárquica del directorio con dos unidades organizativas: una para usuarios y otra para grupos.

**Fichero `estructura.ldif`:**

```bash
nano ~/estructura.ldif
```

```ldif
dn: ou=usuarios,dc=mindverse,dc=local
objectClass: organizationalUnit
ou: usuarios

dn: ou=grupos,dc=mindverse,dc=local
objectClass: organizationalUnit
ou: grupos
```

**Aplicar y verificar:**

```bash
ldapadd -x -D "cn=admin,dc=mindverse,dc=local" -W -f ~/estructura.ldif
ldapsearch -x -LLL -b "dc=mindverse,dc=local" "(objectClass=organizationalUnit)"
```

![captura 37](https://github.com/user-attachments/assets/de606866-8f71-4a91-b10a-a8b55432f075)

---

### 12. Creación de usuarios LDAP

Se generan los usuarios del directorio LDAP con sus atributos POSIX para que puedan autenticarse en el sistema Linux.

**Generar hash de contraseña:**

```bash
HASH=$(slappasswd -s 'Mindverse2025!')
echo $HASH
```

**Crear fichero `usuarios.ldif`:**

```ldif
dn: uid=alumno1,ou=usuarios,dc=mindverse,dc=local
objectClass: inetOrgPerson
objectClass: posixAccount
objectClass: shadowAccount
uid: alumno1
uidNumber: 2001
gidNumber: 2001
homeDirectory: /home/alumno1
loginShell: /bin/bash
userPassword: {SSHA}...

dn: uid=alumno2,ou=usuarios,dc=mindverse,dc=local
objectClass: inetOrgPerson
objectClass: posixAccount
objectClass: shadowAccount
uid: alumno2
uidNumber: 2002
gidNumber: 2002
homeDirectory: /home/alumno2
loginShell: /bin/bash
userPassword: {SSHA}...
```

![captura 38](https://github.com/user-attachments/assets/9ff09d6b-3b4d-4286-9c77-272e7d84c326)
![captura 39](https://github.com/user-attachments/assets/78fda2ca-61a9-42d6-9416-53313cb78d40)
![captura 40](https://github.com/user-attachments/assets/823a1586-2d00-4412-856b-7682472718db)

**Aplicar y verificar:**

```bash
ldapadd -x -D "cn=admin,dc=mindverse,dc=local" -W -f ~/usuarios.ldif
ldapsearch -x -LLL -b "ou=usuarios,dc=mindverse,dc=local"
```

![captura 41](https://github.com/user-attachments/assets/b72a5395-7bda-4be5-9e2d-6a8141bc2a66)

---

### 13. Instalación y configuración de SSSD

SSSD (System Security Services Daemon) actúa como intermediario entre el sistema Linux y el servidor LDAP, permitiendo que los usuarios del directorio se autentiquen como usuarios locales.

**Instalación:**

```bash
sudo apt install sssd sssd-ldap ldap-utils -y
```

**Configuración de `/etc/sssd/sssd.conf`:**

```bash
sudo nano /etc/sssd/sssd.conf
```

```ini
[sssd]
services = nss, pam
config_file_version = 2
domains = mindverse.local

[domain/mindverse.local]
id_provider = ldap
auth_provider = ldap
ldap_uri = ldap://localhost
ldap_search_base = dc=mindverse,dc=local
ldap_default_bind_dn = cn=admin,dc=mindverse,dc=local
ldap_default_authtok = Mindverse2025!
ldap_tls_reqcert = never
enumerate = true
cache_credentials = true
```

**Permisos y reinicio:**

```bash
sudo chmod 600 /etc/sssd/sssd.conf
sudo systemctl restart sssd
sudo systemctl status sssd
```

![captura 43](https://github.com/user-attachments/assets/d482c47e-4be2-442e-a6f9-203a22c10f2a)
![captura 44](https://github.com/user-attachments/assets/8160d7d8-aa5f-429e-9a9d-6877c90256bc)
![captura 45](https://github.com/user-attachments/assets/0a35a20b-25c7-4bf6-8b65-48f9c2fcb57d)

---

### 14. Verificación de autenticación LDAP

Se verifica que el sistema resuelve los usuarios LDAP como si fueran usuarios locales y que la autenticación funciona correctamente.

**Resolución de usuarios via SSSD:**

```bash
getent passwd alumno1
getent passwd alumno2
```

**Prueba de autenticación:**

```bash
su - alumno1   # Contraseña: Mindverse2025!
whoami
id
exit
```

El sistema resuelve correctamente ambos usuarios desde el directorio LDAP. La sesión de `alumno1` se abre con éxito, `whoami` devuelve `alumno1` y el comando `id` muestra `uid=1001` con sus grupos correctos.

![captura 46](https://github.com/user-attachments/assets/0f6052d8-1d54-4f94-aae6-f38a1056639b)

---

## BLOQUE 3 — ACTIVE DIRECTORY EN WINDOWS SERVER

### 15. Nota sobre el entorno — Por qué no se ejecutó

> ⚠️ Este bloque **NO ha podido ejecutarse** en la práctica porque el grupo trabaja sobre un servidor físico real con Ubuntu Linux, sin hipervisor (VirtualBox, VMware, etc.).
>
> A continuación se documenta el procedimiento completo que se seguiría con acceso a una máquina Windows Server, paso a paso.

---

### 16. Instalación de Windows Server y AD DS

**Requisitos previos:**

- ISO de Windows Server 2019 o 2022
- Mínimo 4 GB de RAM y 2 vCPUs para la VM
- IP estática configurada (ej: `192.168.1.10/24`)
- Nombre del servidor: `MINDVERSE-DC`

**Instalación del rol AD DS desde PowerShell:**

```powershell
Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools
```

**O desde el Asistente (Server Manager):**

1. Abrir Server Manager → Manage → Add Roles and Features
2. Seleccionar `Active Directory Domain Services`
3. Instalar y reiniciar si es necesario

---

### 17. Configuración del dominio AD

Una vez hayamos instalado el rol de AD DS se promueve el servidor a controlador de dominio.

**Desde PowerShell:**

```powershell
Import-Module ADDSDeployment

Install-ADDSForest `
  -DomainName 'mindverse.local' `
  -DomainNetbiosName 'MINDVERSE' `
  -SafeModeAdministratorPassword (ConvertTo-SecureString 'Mindverse2025!' -AsPlainText -Force) `
  -InstallDns `
  -Force
```

El servidor se reinicia automáticamente. Tras el reinicio el dominio `mindverse.local` está operativo.

**Verificación desde PowerShell:**

```powershell
Get-ADDomain
Get-ADDomainController
```

---

### 18. Creación de usuarios y grupos en AD

Se crean las unidades organizativas, grupos y usuarios equivalentes a los del directorio LDAP.

**Crear OUs:**

```powershell
New-ADOrganizationalUnit -Name 'Usuarios' -Path 'DC=mindverse,DC=local'
New-ADOrganizationalUnit -Name 'Grupos'   -Path 'DC=mindverse,DC=local'
```

**Crear grupos:**

```powershell
New-ADGroup -Name 'it'   -GroupScope Global -Path 'OU=Grupos,DC=mindverse,DC=local'
New-ADGroup -Name 'rrhh' -GroupScope Global -Path 'OU=Grupos,DC=mindverse,DC=local'
```

**Crear usuarios:**

```powershell
New-ADUser -Name 'alumno1' `
  -SamAccountName 'alumno1' `
  -UserPrincipalName 'alumno1@mindverse.local' `
  -Path 'OU=Usuarios,DC=mindverse,DC=local' `
  -AccountPassword (ConvertTo-SecureString 'Mindverse2025!' -AsPlainText -Force) `
  -Enabled $true

Add-ADGroupMember -Identity 'it' -Members 'alumno1'

New-ADUser -Name 'alumno2' `
  -SamAccountName 'alumno2' `
  -UserPrincipalName 'alumno2@mindverse.local' `
  -Path 'OU=Usuarios,DC=mindverse,DC=local' `
  -AccountPassword (ConvertTo-SecureString 'Mindverse2025!' -AsPlainText -Force) `
  -Enabled $true

Add-ADGroupMember -Identity 'rrhh' -Members 'alumno2'
```

**Verificación:**

```powershell
Get-ADUser -Filter * -SearchBase 'OU=Usuarios,DC=mindverse,DC=local'
Get-ADGroupMember -Identity 'it'
```

---

### 19. Unión de un cliente Linux al dominio AD

Desde una máquina Ubuntu cliente se instalan las herramientas necesarias y se une al dominio `mindverse.local`.

**Instalar dependencias en el cliente Ubuntu:**

```bash
sudo apt install realmd sssd sssd-tools adcli samba-common-bin -y
```

**Descubrir el dominio:**

```bash
realm discover mindverse.local
```

**Unirse al dominio:**

```bash
sudo realm join mindverse.local -U Administrator
```

> Introducir la contraseña del Administrador de AD cuando se solicite.

**Verificar la unión:**

```bash
realm list
id alumno1@mindverse.local
```

---

### 20. Verificación de autenticación AD desde Linux

Se comprueba que los usuarios del dominio AD pueden autenticarse en el cliente Ubuntu.

**Resolución de usuarios AD:**

```bash
getent passwd alumno1@mindverse.local
```

**Autenticación:**

```bash
su - alumno1@mindverse.local   # Contraseña: Mindverse2025!
whoami
id
exit
```

**Logs de autenticación:**

```bash
sudo tail -20 /var/log/auth.log
```

En un entorno real con Windows Server, estos comandos devolverían el usuario resuelto desde el controlador de dominio AD y la sesión se abriría correctamente con los grupos del dominio asignados.

Como el servidor lo teníamos en clase hemos utilizado el servidor para hacer la práctica en el aula, hemos realizado esta práctica para .
