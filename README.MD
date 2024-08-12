# Monitoring and Observability Stack

This repository contains a Docker Compose setup for a complete monitoring and observability stack using Grafana, Prometheus, Loki, Tempo, and Alloy.

## Architecture

### Services

1. **Grafana**
   - **Image**: `grafana/grafana-oss:11.1.1`
   - **Configuration**: Mounted from `./grafana/` to `/etc/grafana/`
   - **Data Storage**: Mounted from `grafana-storage` volume to `/var/lib/grafana`
   - **Exposed Ports**: `3000` (Grafana UI)

2. **Prometheus**
   - **Image**: `prom/prometheus:v2.54.0`
   - **Configuration**: Mounted from `./prometheus/` to `/etc/prometheus/`
   - **Data Storage**: Mounted from `prometheus-storage` volume to `/prometheus`
   - **Exposed Ports**: None (can be uncommented in `docker-compose.yaml`)

3. **Loki**
   - **Image**: `grafana/loki:3.1.0`
   - **Configuration**: Mounted from `./loki/` to `/etc/loki/`
   - **Data Storage**: Mounted from `loki-storage` volume to `/loki`
   - **Exposed Ports**: None (can be uncommented in `docker-compose.yaml`)

4. **Tempo**
   - **Image**: `grafana/tempo:2.5.0`
   - **Configuration**: Mounted from `./tempo/tempo.yaml` to `/etc/tempo.yaml`
   - **Data Storage**: Mounted from `tempo-storage` volume to `/var/tempo`
   - **Exposed Ports**: None (can be uncommented in `docker-compose.yaml`)

5. **Alloy**
   - **Image**: `grafana/alloy:latest`
   - **Configuration**: Mounted from `./alloy/config.alloy` to `/etc/alloy/config.alloy`
   - **Exposed Ports**:
     - `12345` (HTTP)
     - `4317` (GRPC)
     - `4318` (HTTP)

### Networks

All services are connected to a Docker network named `back-tier`.

### Volumes

- `grafana-storage`: Persistent storage for Grafana data.
- `prometheus-storage`: Persistent storage for Prometheus data.
- `loki-storage`: Persistent storage for Loki data.
- `tempo-storage`: Persistent storage for Tempo data.

## Configuration Files

- **Grafana**: [grafana/grafana.ini](grafana/grafana.ini)
- **Prometheus**: [prometheus/prometheus.yml](prometheus/prometheus.yml)
- **Loki**: [loki/local-config.yaml](loki/local-config.yaml)
- **Tempo**: [tempo/tempo.yaml](tempo/tempo.yaml)
- **Alloy**: [alloy/config.alloy](alloy/config.alloy)

## Usage

To start the stack, run:

```sh
docker-compose up -d
```
To stop the stack, run:

```sh
docker-compose down
```

## Exposed Ports

* **Grafana**: 3000
* **Alloy**: 4317 (OTEL Grpc), 4318 (OTEL HTTP)

Uncomment the relevant lines in docker-compose.yaml to expose additional ports for Prometheus, Loki, and Tempo if needed.


