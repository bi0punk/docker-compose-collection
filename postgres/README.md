# PostgreSQL

Base de datos PostgreSQL 16 Alpine con persistencia y scripts de inicialización.

## Uso

```bash
cp .env.example .env
# Editar credenciales en .env
docker compose up -d
```

## Conexión

| Parámetro     | Valor por defecto |
|---------------|-------------------|
| Host          | localhost         |
| Puerto        | 5432              |
| Usuario       | app_user          |
| Contraseña    | app_password      |
| Base de datos | app_db            |

### Conectar desde consola

```bash
docker compose exec postgres psql -U app_user -d app_db
```

### Conectar desde otra aplicación

```
postgresql://app_user:app_password@localhost:5432/app_db
```

## Inicialización

Los scripts en `init/` se ejecutan automáticamente la primera vez que se crea el volumen. Útil para crear tablas, indices o datos iniciales.

## Volúmenes

| Volumen         | Propósito             |
|-----------------|-----------------------|
| `postgres_data` | Datos persistentes    |
