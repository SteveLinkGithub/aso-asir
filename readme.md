# GLPI Docker - Proyecto Final ASIR

## Docker Hub (Mis Imágenes)
- **DB:** `steven32/mariadb-asir:10.6` → [https://hub.docker.com/r/steven32/mariadb-asir](https://hub.docker.com/r/steven32/mariadb-asir)
- **GLPI:** `steven32/glpi-asir:latest` → [https://hub.docker.com/r/steven32/glpi-asir](https://hub.docker.com/r/steven32/glpi-asir)

## GitLab
[https://gitlab.com/steven32/proyecto_glpi](https://gitlab.com/steven32/proyecto_glpi)

## Despliegue
Para desplegar la aplicación utilizando mis imágenes personalizadas de Docker Hub, ejecuta los siguientes comandos:

```bash
git clone [https://gitlab.com/steven32/proyecto_glpi.git](https://gitlab.com/steven32/proyecto_glpi.git)
cd proyecto_glpi
docker compose up -d

