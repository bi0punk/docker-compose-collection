# COL — Stack de infraestructura con Docker Compose

Colección de servicios listos para desplegar, cada uno en su propio directorio con `docker-compose.yml` y `.env.example`.

## Servicios incluidos

| Directorio            | Servicio                  | Puerto(s)          |
|-----------------------|---------------------------|--------------------|
| `gitlab/`             | GitLab CE (git + CI/CD)   | 8080, 8443, 8022   |
| `grafana-prometheus/` | Monitoreo (métricas)      | 3000, 9090         |
| `n8n/`                | Automatización de flujos  | 5678               |
| `portainer/`          | Gestión de Docker (UI)    | 9000, 9443         |
| `postgres/`           | Base de datos PostgreSQL  | 5432               |
| `rabbitmq/`           | Message broker            | 5672, 15672        |

## Inicio rápido

```bash
# 1. Entra al directorio del servicio que quieres levantar
cd postgres

# 2. Copia el archivo de variables y edítalo
cp .env.example .env
nano .env   # o vim, code, etc.

# 3. Levanta el servicio
docker compose up -d

# 4. Verifica el estado
docker compose ps
docker compose logs -f
```

## Antes de desplegar en producción — checklist

- [ ] **Secretos**: reemplaza TODOS los valores marcados con `C4mbia_esto_AHORA!` en cada `.env`
- [ ] **Claves de cifrado**: genera las claves aleatorias indicadas en cada `.env` (comandos `openssl` incluidos)
- [ ] **Versiones**: los tags de imagen ya están pinned; actualiza solo después de probar
- [ ] **Red**: si los servicios necesitan comunicarse entre sí, colócalos en la misma red Docker externa:
  ```bash
  docker network create col-net
  ```
  y agrega a cada compose:
  ```yaml
  networks:
    default:
      external: true
      name: col-net
  ```
- [ ] **Firewall**: expón solo los puertos estrictamente necesarios al exterior
- [ ] **Backups**: monta los volúmenes de datos en una ruta conocida y planifica snapshots

## Generar secretos rápidamente

```bash
# Contraseña aleatoria (16 bytes, base64)
openssl rand -base64 16

# Clave hex (32 bytes, para N8N_ENCRYPTION_KEY, GRAFANA_SECRET_KEY, etc.)
openssl rand -hex 32

# Cookie Erlang para RabbitMQ
openssl rand -hex 32
```
