# docker-compose-collection

Colección de docker-compose listos para usar, cada uno en su propio directorio con documentación independiente.

## Servicios

| Directorio           | Servicios                 | Puertos expuestos              |
|----------------------|---------------------------|--------------------------------|
| [gitlab/](gitlab/)   | GitLab CE + Runner        | `8022` (SSH), `8080` (HTTP)    |
| [grafana-prometheus/](grafana-prometheus/) | Grafana + Prometheus | `3000` (Grafana), `9090` (Prom) |
| [postgres/](postgres/) | PostgreSQL 16           | `5432`                         |
| [portainer/](portainer/) | Portainer CE           | `9000` (HTTP), `9443` (HTTPS)  |
| [rabbitmq/](rabbitmq/) | RabbitMQ + Management   | `5672` (AMQP), `15672` (UI)    |

## Cómo usar

```bash
# Entrar al directorio del servicio deseado
cd gitlab

# Copiar entorno de ejemplo
cp .env.example .env

# Editar credenciales si es necesario
# $EDITOR .env

# Levantar el servicio
docker compose up -d

# Ver logs
docker compose logs -f

# Detener
docker compose down
```

Cada directorio tiene su propio `README.md` con instrucciones detalladas.

## Requisitos

- Docker Engine 24+
- Docker Compose v2+
