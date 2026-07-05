# COL — Stack de infraestructura con Docker Compose

[![License](https://img.shields.io/badge/License-MIT-yellow)](LICENSE)
[![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?logo=docker)](https://docs.docker.com/compose/)
[![YAML](https://img.shields.io/badge/YAML-1.2-CB171E)](https://yaml.org/)
[![CI](https://github.com/drbash/docker-compose-collection/actions/workflows/ci.yml/badge.svg)](https://github.com/drbash/docker-compose-collection/actions)

Colección de servicios listos para desplegar con Docker Compose, cada uno en su propio directorio con `docker-compose.yml` y `.env.example`. Ideal para entornos de desarrollo, laboratorios y homelabs.

## Contenido

- [Servicios incluidos](#servicios-incluidos)
- [Inicio rápido](#inicio-r%C3%A1pido)
- [Características](#caracter%C3%ADsticas)
- [Stack](#stack)
- [Estructura](#estructura)
- [Requisitos](#requisitos)
- [Instalación](#instalaci%C3%B3n)
- [Uso](#uso)
- [Tests](#tests)
- [Configuración](#configuraci%C3%B3n)
- [CI/CD](#cicd)
- [Antes de producción](#antes-de-producci%C3%B3n)
- [Generar secretos](#generar-secretos-r%C3%A1pidamente)
- [Limitaciones / Roadmap](#limitaciones--roadmap)
- [Licencia](#licencia)

## Servicios incluidos

| Directorio | Servicio | Puerto(s) |
|---|---|---|
| `gitlab/` | GitLab CE (git + CI/CD) | 8080, 8443, 8022 |
| `grafana-prometheus/` | Monitoreo (métricas) | 3000, 9090 |
| `n8n/` | Automatización de flujos | 5678 |
| `portainer/` | Gestión de Docker (UI) | 9000, 9443 |
| `postgres/` | Base de datos PostgreSQL | 5432 |
| `rabbitmq/` | Message broker | 5672, 15672 |

## Características

- **Plug-and-play**: cada servicio se levanta con un solo comando
- **Configuración sensible**: `.env.example` con valores marcados para reemplazar
- **Seguridad**: secretos generables con `openssl`
- **Versiones pinned**: imágenes con tag fijo para evitar breaking changes
- **Redes**: preparados para integrarse en una misma red Docker externa

## Stack

| Componente | Tecnología |
|---|---|
| Contenedores | Docker Compose (V2) |
| Servicios | GitLab, Grafana, Prometheus, n8n, Portainer, PostgreSQL, RabbitMQ |
| SO base | Alpine Linux (imágenes oficiales) |

## Estructura

```
docker-compose-collection/
├── gitlab/                 # GitLab CE
│   ├── docker-compose.yml
│   └── .env.example
├── grafana-prometheus/     # Stack de monitoreo
│   ├── docker-compose.yml
│   └── .env.example
├── n8n/                    # Automatización
│   ├── docker-compose.yml
│   └── .env.example
├── portainer/              # Gestión Docker
│   ├── docker-compose.yml
│   └── .env.example
├── postgres/               # Base de datos
│   ├── docker-compose.yml
│   └── .env.example
├── rabbitmq/               # Message broker
│   ├── docker-compose.yml
│   └── .env.example
├── tests/
│   └── test_smoke.py
├── .env.example
├── .github/workflows/ci.yml
├── pyproject.toml
└── README.md
```

## Requisitos

- Docker Engine >= 24.0
- Docker Compose >= 2.20 (plugin `docker compose`)
- Sistema Linux / macOS / Windows (WSL2)
- Puertos disponibles (ver tabla de servicios)

## Instalación

```bash
git clone https://github.com/drbash/docker-compose-collection.git
cd docker-compose-collection
```

## Uso

```bash
# 1. Entra al directorio del servicio que quieres levantar
cd postgres

# 2. Copia el archivo de variables y edítalo
cp .env.example .env
nano .env

# 3. Levanta el servicio
docker compose up -d

# 4. Verifica el estado
docker compose ps
docker compose logs -f
```

## Tests

```bash
pip install pytest
pytest tests/ -v
```

## Configuración

Cada servicio tiene su propio `.env.example` con variables documentadas. Variables comunes:

| Variable | Descripción |
|---|---|
| `POSTGRES_PASSWORD` | Contraseña de base de datos |
| `GITLAB_ROOT_PASSWORD` | Contraseña root de GitLab |
| `GRAFANA_SECRET_KEY` | Clave de cifrado de Grafana |
| `N8N_ENCRYPTION_KEY` | Clave de cifrado de n8n |
| `RABBITMQ_ERLANG_COOKIE` | Cookie Erlang para RabbitMQ |

## CI/CD

GitHub Actions ejecuta lint (Ruff) y tests (pytest) en cada push/PR:

- **Ruff check**: linting de Python
- **Pytest**: smoke tests básicos

## Antes de producción — checklist

- [ ] **Secretos**: reemplaza TODOS los valores marcados con `C4mbia_esto_AHORA!`
- [ ] **Claves de cifrado**: genera claves aleatorias con `openssl`
- [ ] **Versiones**: los tags de imagen ya están pinned
- [ ] **Red**: si los servicios necesitan comunicarse, colócalos en la misma red externa
- [ ] **Firewall**: expón solo los puertos estrictamente necesarios
- [ ] **Backups**: monta volúmenes en rutas conocidas y planifica snapshots

## Generar secretos rápidamente

```bash
# Contraseña aleatoria (16 bytes, base64)
openssl rand -base64 16

# Clave hex (32 bytes)
openssl rand -hex 32

# Cookie Erlang para RabbitMQ
openssl rand -hex 32
```

## Limitaciones / Roadmap

- [x] Servicios básicos de infraestructura
- [ ] HTTPS automático con Traefik/Caddy
- [ ] Script de deploy completo con `docker compose up -d` para todo el stack
- [ ] Monitoreo centralizado con logs agregados
- [ ] Respaldo automatizado de volúmenes
- [ ] Soporte para stacks adicionales (Redis, MongoDB, Elasticsearch)

## Licencia

MIT
