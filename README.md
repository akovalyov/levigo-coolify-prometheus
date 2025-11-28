# Prometheus Coolify Service

A complete monitoring stack for [Coolify](https://coolify.io/) deployments featuring Prometheus, Grafana, Node Exporter, and cAdvisor.

Based on the guide at [peturgeorgievv.com](https://peturgeorgievv.com/blog/deploy-prometheus-and-grafana-in-coolify-code-example).

## 📋 Components

- **Prometheus** - Time-series database and monitoring server
- **Grafana** - Visualization and dashboards
- **Node Exporter** - System metrics collector (CPU, memory, disk, network)
- **cAdvisor** - Container metrics collector

## 🚀 Quick Start

### Prerequisites

- Docker and Docker Compose installed
- [Coolify](https://coolify.io/) instance (for deployment)

### Local Development

1. Clone the repository:
   ```bash
   git clone https://github.com/akovalyov/levigo-coolify-prometheus.git
   cd levigo-coolify-prometheus
   ```

2. Copy and configure environment variables:
   ```bash
   cp .env.example .env
   # Edit .env with your credentials
   ```

3. Start the stack:
   ```bash
   docker compose up -d
   ```

4. Access the services:
   - **Prometheus**: http://localhost:9090
   - **Grafana**: http://localhost:3000 (default: admin/admin)
   - **cAdvisor**: http://localhost:8080

### Deploy to Coolify

1. Create a new project in Coolify
2. Add a new service using "Docker Compose"
3. Point to this repository or paste the `docker-compose.yml` content
4. Configure environment variables in Coolify's settings
5. Deploy the service

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

## 🔧 Configuration

### Prometheus Configuration

Edit `config/prometheus.yml` to add custom scrape targets:

```yaml
scrape_configs:
  - job_name: "your-app"
    static_configs:
      - targets: ["your-app:port"]
```

### Grafana Datasources

Prometheus is pre-configured as the default datasource. Additional datasources can be added in `config/grafana/provisioning/datasources/`.

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `GRAFANA_ADMIN_USER` | Grafana admin username | `admin` |
| `GRAFANA_ADMIN_PASSWORD` | Grafana admin password | `admin` |

## 📁 Project Structure

```
.
├── docker-compose.yml          # Main Docker Compose configuration
├── config/
│   ├── prometheus.yml          # Prometheus configuration
│   └── grafana/
│       └── provisioning/
│           └── datasources/
│               └── prometheus.yml  # Grafana datasource config
├── .env.example                # Example environment variables
└── README.md                   # This file
```

## 🔒 Security Notes

- Change default Grafana credentials before deploying to production
- Consider adding authentication to Prometheus for production use
- Use Coolify's built-in SSL/TLS for HTTPS access

## 📚 Resources

- [Prometheus Documentation](https://prometheus.io/docs/)
- [Grafana Documentation](https://grafana.com/docs/)
- [Coolify Documentation](https://coolify.io/docs/)
- [Node Exporter](https://github.com/prometheus/node_exporter)
- [cAdvisor](https://github.com/google/cadvisor)

## 📝 License

MIT License