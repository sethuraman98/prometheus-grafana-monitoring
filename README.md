# AWS EC2 Monitoring with Prometheus and Grafana

## Project Overview

This project implements a Linux server monitoring solution using AWS EC2, Prometheus, Grafana, and Node Exporter.

Prometheus collects system metrics from Node Exporter, while Grafana visualizes the collected metrics through an interactive monitoring dashboard.

## Technologies Used

- AWS EC2
- Amazon Linux 2023
- Prometheus 3.13.5
- Grafana 13.3.1
- Node Exporter 1.12.1
- Linux systemd

## Architecture

```text
  Node Exporter
  Port 9100
      |
      | Exposes metrics
      v
Prometheus
  Port 9090
      |
      | Scrapes Node Exporter
      | Grafana queries Prometheus
      v
Grafana
  Port 3000
      |
      v
Monitoring Dashboard
```

## EC2 Configuration

| Configuration | Value |
|---|---|
| Instance type | t3.micro |
| Operating System | Amazon Linux 2023 |
| AWS Region | ap-southeast-2 |
| Storage | 20 GB gp3 |
| Swap Memory | 2 GB |

## Installation and Configuration

### 1. Prometheus

- Created a dedicated Linux user named `prometheus`.
- Downloaded and installed Prometheus.
- Configured Prometheus using `prometheus.yml`.
- Created a systemd service.
- Configured a 30-second scrape interval.
- Configured 3-day metric retention.

### 2. Node Exporter

- Installed Node Exporter 1.12.1.
- Created a dedicated Linux user.
- Configured Node Exporter as a systemd service.
- Exposed Linux metrics on port 9100.

### 3. Grafana

- Installed Grafana 13.3.1.
- Started and enabled the Grafana service.
- Configured Prometheus as the data source.
- Imported Node Exporter Full dashboard (Dashboard ID: 1860).

## Prometheus Configuration

The Prometheus configuration is available at:

`prometheus/prometheus.yml`

Configured monitoring targets:

- localhost:9090 – Prometheus
- localhost:9100 – Node Exporter

## Monitoring Metrics

The Grafana dashboard monitors:

- CPU utilization
- Memory utilization
- Swap utilization
- Disk utilization
- Network traffic
- System uptime

## Service Management

Check Prometheus:

```bash
systemctl status prometheus
```

Check Node Exporter:

```bash
systemctl status node_exporter
```

Check Grafana:

```bash
systemctl status grafana-server
```

## Access URLs

- Prometheus: http://52.65.104.142:9090
- Grafana: http://52.65.104.142:3000

Note: These are the current EC2 public IP-based URLs. Access is restricted by the configured AWS security group. The IP may change if the instance is stopped and restarted.

## Repository Structure

```text
prometheus-grafana-monitoring/
│
├── prometheus/
│   └── prometheus.yml
│
├── systemd/
│   ├── prometheus.service
│   └── node_exporter.service
│
├── screenshots/
│
└── README.md
```

## Project Outcome

Successfully deployed a monitoring solution on AWS EC2 using Prometheus, Grafana, and Node Exporter.

Both Prometheus monitoring targets were verified as UP, and the Grafana dashboard successfully displayed Linux server metrics.

## Security Notes

- SSH access is restricted to the administrator's IP.
- Monitoring ports should not be exposed publicly without appropriate security controls.
- Credentials and private keys are not included in this repository.

---

**Project:** Linux Server Monitoring using Prometheus and Grafana  
**Platform:** AWS EC2  
**Purpose:** DevOps Monitoring Assessment
