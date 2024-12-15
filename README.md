# Apache Web Server - Self-Hosted on Proxmox VM

This README outlines the deployment of an Apache self-hosted web server. The setup leverages Proxmox for virtualization, Ansible for provisioning, IONOS as the domain provider and dynamic DNS updater, and Grafana for monitoring using `apache_exporter` and `node_exporter`.

---

## Table of Contents
- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Architecture](#architecture)
- [Deployment Steps](#deployment-steps)
- [Monitoring Setup](#monitoring-setup)
- [Domain Configuration](#domain-configuration)
- [Future Improvements](#future-improvements)

---

## Overview
The Apache web server is deployed on a Proxmox virtual machine (VM) with dynamic domain resolution through IONOS. Ansible automates the provisioning process, ensuring the entire server setup, including Grafana provisioning, is completed upon executing the playbook. Server performance is monitored using Grafana with metrics from `apache_exporter` and `node_exporter`.

---

## Prerequisites

### Software Requirements
- **Proxmox VE**
- **Ansible**
- **IONOS** account for domain management and dynamic DNS
- **Apache Web Server**
- **Grafana** with `apache_exporter` and `node_exporter`

### Hardware Requirements
- **4 CPU cores**
- **2 GB RAM**
- **8 GB Storage**
- **Gigabit internet connection**

---

## Architecture

1. **Proxmox VM**: Hosts the Apache server and exporters.
2. **Ansible**: Automates VM provisioning and complete server setup.
3. **IONOS**: Manages domain records and dynamic DNS updates.
4. **Monitoring**: Grafana with `apache_exporter` and `node_exporter`.

---

## Deployment Steps

### Step 1: Provision the VM on Proxmox
- Create a VM in Proxmox with the desired specifications.
- Install a Linux distribution (Ubuntu).
- Configure the VM to allow SSH access using keys (disable password authentication).

### Step 2: Execute Ansible Playbooks
- Use Ansible to automate:
  - Apache installation.
  - Creation of virtual hosts.
  - Firewall rules (e.g., UFW for port 443).
  - User permissions and server hardening.
  - Full provisioning of Grafana dashboards and data sources.

### Step 3: Configure Dynamic DNS with IONOS
- Update DNS records in the IONOS portal.
- Use a dynamic DNS updater to ensure the IP address is synced with the domain.

### Step 4: Validate Apache Server
- Access the server via the domain or public IP.
- Ensure `/var/www/html` serves the expected content.

---

## Monitoring Setup

### Step 1: Install and Configure `apache_exporter`
- Download and install the `apache_exporter` binary.
- Run the exporter as a service, ensuring it points to Apache’s status page.

### Step 2: Install and Configure `node_exporter`
- Download and install `node_exporter` for system metrics.
- Run the exporter as a service on the VM.

### Step 3: Grafana Dashboards Provisioning
- Ansible automatically provisions Grafana dashboards and data sources during server setup.
- Metrics from `apache_exporter` and `node_exporter` are pre-configured in Grafana.

---

## Domain Configuration
- Domain: Managed via IONOS.
- Dynamic DNS: Keeps the public IP updated for the domain.
- HTTPS: Configured using IONOS certificates, ensuring secure communication.
- Apache Virtual Host Configuration:
  ```apache
  <VirtualHost *:443>
      ServerName yourdomain.com
      DocumentRoot /var/www/html
      SSLEngine on
      SSLCertificateFile /etc/ssl/certs/yourdomain.com.crt
      SSLCertificateKeyFile /etc/ssl/private/yourdomain.com.key
      <Directory /var/www/html>
          Options Indexes FollowSymLinks
          AllowOverride All
          Require all granted
      </Directory>
  </VirtualHost>
  ```

---

## Future Improvements
- Configure a load balancer for high availability.
- Enable advanced logging and analytics.

---

**Maintained by**: egenerei
