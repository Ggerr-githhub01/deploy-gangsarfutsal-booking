# Deployment Process

## Overview

This section of the document will explain the process of deploying a futsal booking website to an Ubuntu server.

The deployment was performed on a Virtual Private Server using Apache2 as the web server, PHP 8.2 as the runtime environment, and MySQL as the database server. The goal was to provide a stable production environment accessible through the public domain.

## Deployment Workflow

```text
Login to VPS
        │
        ▼
Update System Packages
        │
        ▼
Install Server Components
        │
        ▼
Upload Project via SCP
        │
        ▼
Configure Laravel Environment
        │
        ▼
Initialize Database
        │
        ▼
Configure Apache VirtualHost
        │
        ▼
Configure Firewall
        │
        ▼
Validate Application
        │
        ▼
Harden SSH Configuration
        │
        ▼
Configure SSL Certificate
        │
        ▼
Final Validation
```

# Login to VPS

This deployment process begins by logging into the VPS via secure shell (SSH) using the obtained public IP.

By using the following command:

```bash
ssh username@server-IP
```

Example: 

```bash
ssh root@154.19.37.170
```
