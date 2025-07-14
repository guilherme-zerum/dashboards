# 📊 Dashboards: Prometheus & Grafana

[![Docker](https://img.shields.io/badge/docker-ready-blue?logo=docker)](https://www.docker.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## ⚡ Quick Start

```sh
# Clone the repository
 git clone <repo-url>
 cd dashboards
 # Start all services
 docker-compose up -d
```

---

## 🧰 Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/)
- (Optional) [Make](https://www.gnu.org/software/make/) for convenience commands

---

## 💡 Example Use Cases

- Monitoring microservices in development
- Visualizing resource usage on a local server
- Testing Prometheus/Grafana integrations before production

---

This project orchestrates a monitoring environment using **Prometheus** and **Grafana** via Docker Compose, making it easy to set up observability for your applications or infrastructure.

## 📁 Project Structure

```
dashboards/
├── README.md
├── docker-compose.yml         # Orchestrates Prometheus & Grafana containers
├── grafana/
│   ├── Dockerfile
│   ├── Makefile
│   └── config/                # (Optional) Custom Grafana configurations
└── prometheus/
    ├── Dockerfile
    ├── Makefile
    ├── prometheus.yml         # Prometheus configuration file
    └── config/                # (Optional) Additional Prometheus 

## 🚀 Getting Started

1. **Start the services:**
   ```sh
   docker-compose up -d 
   ```

2. **Access the dashboards:**
   - Prometheus: [http://localhost:9090](http://localhost:9090)
   - Grafana: [http://localhost:3000](http://localhost:3000)

3. **Useful commands:**
   - `make build` (inside each service folder): Build the Docker image for that service

   - `make up` / `make down`: Start/stop the service using Makefile shortcuts

## ⚙️ Configuration
- Use `.env` files for sensitive variables (and add them to `.gitignore`).
- Separate configurations by environment if needed (e.g., dev, staging, prod).
- Customize Prometheus targets in `prometheus/prometheus.yml`.
- Add custom Grafana dashboards or datasources in `grafana/config/`.

## 🔍 Prometheus Monitoring Targets

Prometheus is configured to monitor the following services out-of-the-box:

- **Grafana** (`grafana:3000`): Prometheus scrapes metrics from the Grafana container, allowing you to monitor Grafana's health and performance. This is defined in the `prometheus/prometheus.yml` file under the `grafana` job.
- **cAdvisor** (`cadvisor:8080`): Collects resource usage and performance metrics from running containers.
- **Node Exporter** (`node-exporter:9100`): Gathers hardware and OS metrics exposed by *nix kernels, providing insights into the host system.

You can customize or extend these targets by editing the `prometheus/prometheus.yml` file.

## 📈 Grafana Basics

Grafana is a powerful visualization tool for your monitoring data. Here are some basics to get you started:

- **Login:**
  - Default URL: [http://localhost:3000](http://localhost:3000)
  - Default credentials (unless changed):
    - Username: `admin`
    - Password: `admin`

- **Importing Dashboards:**
  1. Log in to Grafana.
  2. Click the "+" icon in the left sidebar and select **Import**.
  3. You can:
     - Paste a dashboard ID from [Grafana.com](https://grafana.com/grafana/dashboards/)
     - Upload a JSON file
     - Paste dashboard JSON directly
  4. Select the Prometheus data source and click **Import**.

- **Adding Data Sources:**
  - Go to **Configuration > Data Sources** and add Prometheus (usually auto-detected as `http://prometheus:9090`).

- **Creating Panels:**
  - Use the **+ > Dashboard** menu to create new dashboards and add panels for your metrics.

For more details, see the [Grafana documentation](https://grafana.com/docs/grafana/latest/).

## 🛠️ Best Practices
- Use Makefiles to standardize commands across services.
- Version control only non-sensitive configuration files.
- Document any customizations or extensions in this README.

## 🛠️ Troubleshooting

- **Ports already in use:** Make sure ports 3000 (Grafana) and 9090 (Prometheus) are free.
- **Grafana not connecting to Prometheus:** Check that the Prometheus container is running and accessible at `http://prometheus:9090`.
- **Permission errors:** Try running Docker commands with `sudo` or as an administrator.

---

## 🤝 Contributing
Feel free to open issues, suggest improvements, or submit pull requests! Contributions are welcome.

---

## 📄 License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

Happy monitoring! 🚦 