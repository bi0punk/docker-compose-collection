# GitLab CE

GitLab Community Edition completo con almacenamiento persistente.

## Requisitos

- Mínimo 4 GB de RAM
- Docker Compose v2+

## Uso

```bash
# Copiar y editar variables de entorno
cp .env.example .env
# Editar contraseñas y host en .env

# Iniciar GitLab (la primera vez tarda varios minutos)
docker compose up -d

# Ver logs del proceso de inicialización
docker compose logs -f
```

## Acceso

| Servicio   | URL                                |
|------------|------------------------------------|
| UI Web     | http://localhost:8080              |
| SSH        | puerto 8022                        |

## Credenciales por defecto

- **Usuario:** `root`
- **Contraseña:** la definida en `GITLAB_ROOT_PASSWORD` (default: `changeme123`)

## Volúmenes

| Volumen          | Propósito                |
|------------------|--------------------------|
| `gitlab_config`  | Configuración de GitLab  |
| `gitlab_logs`    | Logs del servicio        |
| `gitlab_data`    | Repositorios y base de datos |

## Notas

- La primera inicialización puede tardar **3-5 minutos**. Monitorea con `docker compose logs -f` hasta que veas el mensaje de inicio.
- Para cambiar la URL externa, edita `GITLAB_HOST` en `.env` antes del primer inicio.
