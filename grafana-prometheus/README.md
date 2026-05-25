# Grafana + Prometheus

Stack de monitoreo con Prometheus (recolección de métricas) y Grafana (visualización y dashboards).

## Uso

```bash
cp .env.example .env
docker compose up -d
```

## Acceso

| Servicio   | URL                     | Puerto |
|------------|-------------------------|--------|
| Grafana    | http://localhost:3000   | 3000   |
| Prometheus | http://localhost:9090   | 9090   |

## Credenciales Grafana

- **Usuario:** `admin` (o el definido en `GRAFANA_ADMIN_USER`)
- **Contraseña:** `admin123` (o el definido en `GRAFANA_ADMIN_PASSWORD`)

## Estructura

| Ruta                               | Propósito                        |
|------------------------------------|----------------------------------|
| `prometheus/prometheus.yml`        | Configuración de Prometheus      |
| `grafana/datasources/datasource.yml` | Datasource Prometheus precargado |
| `grafana/dashboards/`              | Coloca aquí tus dashboards JSON  |

## Notas

- El datasource de Prometheus se provisiona automáticamente en Grafana.
- Para agregar dashboards predefinidos, copia archivos `.json` en `grafana/dashboards/` y crea un provisioner.
