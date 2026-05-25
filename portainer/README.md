# Portainer CE

Interfaz web para administrar contenedores Docker, imágenes, volúmenes, redes y más.

## Uso

```bash
cp .env.example .env
docker compose up -d
```

## Acceso

| Servicio  | URL                           |
|-----------|-------------------------------|
| UI HTTP   | http://localhost:9000         |
| UI HTTPS  | https://localhost:9443        |

## Primer uso

1. Abrir http://localhost:9000
2. Crear usuario admin (solicitará contraseña en la primera visita)
3. Seleccionar entorno **Local** (usa el socket de Docker)

## Volúmenes

| Volumen           | Propósito                |
|-------------------|--------------------------|
| `portainer_data`  | Configuración y datos de Portainer |

## Notas

- El contenedor necesita acceso al socket de Docker (`/var/run/docker.sock`) para gestionar el motor Docker local.
- No expongas Portainer en redes públicas sin HTTPS y autenticación.
