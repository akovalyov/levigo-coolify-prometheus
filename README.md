# Prometheus Coolify Service

A monitoring stack for [Coolify](https://coolify.io/) deployments featuring Prometheus, Node Exporter, cAdvisor, and NVIDIA GPU monitoring.

Based on the guide at [peturgeorgievv.com](https://peturgeorgievv.com/blog/deploy-prometheus-and-grafana-in-coolify-code-example).

## 📋 Components

- **Prometheus** - Time-series database and monitoring server
- **Node Exporter** - System metrics collector (CPU, memory, disk, network)
- **cAdvisor** - Container metrics collector
- **DCGM Exporter** - NVIDIA GPU metrics collector

## 🚀 Quick Start

### Prerequisites

- Docker and Docker Compose installed
- [Coolify](https://coolify.io/) instance (for deployment)
- For GPU monitoring: [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html)

### Local Development

1. Clone the repository:
   ```bash
   git clone https://github.com/akovalyov/levigo-coolify-prometheus.git
   cd levigo-coolify-prometheus
   ```

2. Start the stack:
   ```bash
   docker compose up -d
   ```

3. Access the services:
   - **Prometheus**: http://localhost:9090
   - **cAdvisor**: http://localhost:8080
   - **DCGM Exporter**: http://localhost:9400/metrics

### Deploy to Coolify

1. Create a new project in Coolify
2. Add a new service using "Docker Compose"
3. Point to this repository or paste the `docker-compose.yml` content
4. Deploy the service

## 📊 Default Metrics

### Node Exporter Metrics
- CPU usage and load
- Memory utilization
- Disk I/O and space
- Network traffic

### cAdvisor Metrics
- Container CPU/memory usage
- Container network I/O
- Docker container statistics

### GPU Metrics (DCGM Exporter)
- GPU utilization
- GPU memory usage
- GPU temperature
- Power consumption
- SM clock speeds

## 🔧 Configuration

### Prometheus Configuration

Edit `config/prometheus.yml` to add custom scrape targets:

```yaml
scrape_configs:
  - job_name: "your-app"
    static_configs:
      - targets: ["your-app:port"]
```

### GPU Monitoring Setup

The DCGM Exporter requires NVIDIA GPUs and the NVIDIA Container Toolkit installed on the host. If you don't have NVIDIA GPUs, you can comment out or remove the `dcgm-exporter` service from `docker-compose.yml`.

## 📁 Project Structure

```
.
├── docker-compose.yml          # Main Docker Compose configuration
├── config/
│   └── prometheus.yml          # Prometheus configuration
└── README.md                   # This file
```

## 🔒 Security Notes

- Consider adding authentication to Prometheus for production use
- Use Coolify's built-in SSL/TLS for HTTPS access

## 📚 Resources

- [Prometheus Documentation](https://prometheus.io/docs/)
- [Coolify Documentation](https://coolify.io/docs/)
- [Node Exporter](https://github.com/prometheus/node_exporter)
- [cAdvisor](https://github.com/google/cadvisor)
- [DCGM Exporter](https://github.com/NVIDIA/dcgm-exporter)

## 📝 License

MIT License