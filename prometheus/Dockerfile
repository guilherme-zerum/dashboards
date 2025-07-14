# Use Ubuntu as the base image
FROM ubuntu:22.04

# Set environment variables to avoid user interaction during install
ENV DEBIAN_FRONTEND=noninteractive

# Install dependencies and Prometheus
RUN apt-get update && \
    apt-get install -y wget tar curl && \
    useradd --no-create-home --shell /bin/false prometheus

# Set Prometheus version
ENV PROMETHEUS_VERSION=2.51.2

# Download and install Prometheus
RUN wget https://github.com/prometheus/prometheus/releases/download/v${PROMETHEUS_VERSION}/prometheus-${PROMETHEUS_VERSION}.linux-amd64.tar.gz && \
    tar xvf prometheus-${PROMETHEUS_VERSION}.linux-amd64.tar.gz && \
    mv prometheus-${PROMETHEUS_VERSION}.linux-amd64/prometheus /usr/local/bin/ && \
    mv prometheus-${PROMETHEUS_VERSION}.linux-amd64/promtool /usr/local/bin/ && \
    mv prometheus-${PROMETHEUS_VERSION}.linux-amd64/consoles /etc/prometheus/ && \
    mv prometheus-${PROMETHEUS_VERSION}.linux-amd64/console_libraries /etc/prometheus/ && \
    mv prometheus-${PROMETHEUS_VERSION}.linux-amd64/prometheus.yml /etc/prometheus/prometheus.yml && \
    rm -rf prometheus-${PROMETHEUS_VERSION}.linux-amd64* 

# Set up directories and permissions
RUN mkdir -p /etc/prometheus /prometheus && \
    chown -R prometheus:prometheus /etc/prometheus /prometheus

USER prometheus

# Expose Prometheus default port
EXPOSE 9090

# Start Prometheus server
CMD ["/usr/local/bin/prometheus", "--config.file=/etc/prometheus/prometheus.yml", "--storage.tsdb.path=/prometheus"]
