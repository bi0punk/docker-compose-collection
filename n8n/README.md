# n8n

Plataforma de automatización de flujos de trabajo con conectores para cientos de servicios.

## Uso

```bash
cp .env.example .env
# Editar N8N_ENCRYPTION_KEY en .env (generar una clave única)
docker compose up -d
```

## Acceso

| Servicio | URL                         |
|----------|-----------------------------|
| n8n UI   | http://localhost:5678       |

## Volúmenes

| Volumen      | Propósito                                        |
|--------------|--------------------------------------------------|
| `n8n_data`   | Base de datos SQLite, workflows y credenciales   |

## Notas

- Los datos se persisten en SQLite (embebido). No requiere base de datos externa.
- La variable `N8N_ENCRYPTION_KEY` debe ser una clave única para cifrar credenciales. Generar con:
  ```bash
  openssl rand -hex 32
  ```
- `WEBHOOK_URL` es necesaria si n8n recibe webhooks desde internet (ej: `https://tu-dominio.com/`).
- La imagen Alpine (`latest`) mantiene el tamaño reducido.
