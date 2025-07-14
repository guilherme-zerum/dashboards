# Use Ubuntu as the base image
FROM ubuntu:22.04

# Set environment variables to avoid user interaction during install
ENV DEBIAN_FRONTEND=noninteractive

# Install dependencies and Grafana
RUN apt-get update && \
    apt-get install -y wget gnupg2 software-properties-common && \
    wget -q -O - https://packages.grafana.com/gpg.key | apt-key add - && \
    add-apt-repository "deb https://packages.grafana.com/oss/deb stable main" && \
    apt-get update && \
    apt-get install -y grafana && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Expose Grafana's default port
EXPOSE 3000

# Start Grafana server
CMD ["/usr/sbin/grafana-server", "--homepath=/usr/share/grafana", "--config=/etc/grafana/grafana.ini"]
